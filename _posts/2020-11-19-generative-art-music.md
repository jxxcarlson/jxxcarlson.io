---
title: Generative Art and Music 
tags: code fp music art rc
---

# RC Friday Show

*November 19, 2020* 

The three pieces below, *Duet*, *Nervous Chase*, and *Space Invaders*, were written using Paul Hudak's Haskell library, *Euterpea*. I've learned everything that went into these compositions from *The Haskell School of Music*, by Paul Hudak and Donya Quick, and also from [Donya Quick's website](http://donyaquick.com/) and other resources she has published on the web.

The last piece, *Space Invaders*, is based on the notion of random walk (Brownian motion), which can be viewed as a way of generating sequences of random numbers.  One can use random sequences to ake artwork as well as music.  We illustrate this with remarks and images in the last section.

Here is the [repo for the code](https://github.com/jxxcarlson/euterpea-exercises).  It is badly in need of some cleanup and editing.  Soon!

Below is a short snippet of Euterpea code, the "theme" from which *Duet* is composed.  It reads as follows: *Make a line of music beginning with a whole note D in octave 1, playing first a D minor triad in whole notes.  Follow this by a 5-note passage in quarter notes and end with half-note whole-note resolution.*

```
bass1 :: Music Pitch
bass1 = line $ [ d 1 wn, f 1 wn, a 1 wn,  g 1 1, f 1 qn, e 1 qn, d 1 qn
               , c 1 qn, e 1 hn, d 1 wn]
```	

## Duet


<audio controls>
  <source src="/audio/duet.mp3" type="audio/mpeg">
  Your browser does not support the audio element.
</audio>

[Code](https://github.com/jxxcarlson/euterpea-exercises/blob/master/src/Duet.hs)

This piece is a duet between two bassoon-tuba combos, with a later entrance by a trombone ostinato.  It is composed using quasi-traditional rather than algorithmic methods, building up the piece by successive application of operators like `:+:` and `:=:` — the first joins pieces of music in series while the second stacks them in parallel. Here is a fragment derived from `bass1`:

```
bass2 d = instrument Bassoon $ bass1 
       :=: (instrument Tuba $ transpose 19 $ offset d $ retro $ bass1)
```

It reads as follows: play `bass1` on bassoon and stack it against a line derived from it played on Tuba.  To derive that line, offset `bass1` by `d` whole notes and then transpose it up 19 semitones, that is, an octave and a perfect fifth.  While the delayed entrance can be any rational multiple of a whole note, we use small integer multiples here.  

Note that `bass2` is a function of type `Rational -> Music Pitch`.  We use it to derive a set of four lines which we subsequently join end-to-end:

```
b1 = bass2 0 :+: rest wn
b2 = transpose 5 $ bass2 2 :+: rest wn
b3 = retro $ transpose 7 $ bass2 4 :+: rest wn
b4 = retro $ transpose 5 $ bass2 2 :+: rest wn 
```
Each phrase ends with a whole-note rest so that when the pieces are joined end-to-end, there is 
a bit of intervening silence.  The function `retro :: Music Pitch -> Music Pitch` re-arranges
the given notes in reverse order.  This is a [classic compositional technique](https://en.wikipedia.org/wiki/Retrograde_(music)):

> Retrograde was not mentioned in theoretical treatises prior to 1500.[1] Nicola Vicentino (1555) discussed the difficulty in finding canonic imitation: "At times, the fugue or canon cannot be discovered through the systems mentioned above, either because of the impediment of rests, or because one part is going up while another is going down, or because one part starts at the beginning and the other at the end. In such cases a student can begin at the end and work back to the beginning in order to find where and in which voice he should begin the canons."[2] Vicentino derided those who achieved purely intellectual pleasure from retrograde (and similar permutations)." — *Wikipedia*

A long line is constructed using these derived parts:

```
bass3 = b1 :+: b2 :+: b3 :+: b4 :+: dim 0.6 b1
```

The operator `dim 0.6` applies a *diminuendo* to its argument, the line `b1`. To achieve
a somewhat richer texture, a second part is composed as follows.

```
ostinato1 = instrument Trombone $ sta 0.9 $  
   line [a 3 hn, d 3 hn, c 3 hn,  g 2 hn, e 3 hn, d 3 wn, rest wn]

ostinato2 = mSequence [0, 2, 7, 5, 0] ostinato1 
   :+: (instrument Trombone $ dim 0.5 $ transpose (-5) 
       $ line [a 3 hn, d 3 hn, c 3 hn,  g 2 hn, e 3 wn, d 3 2])
```

The functions `sta 0.9` renders its argument with staccato articulation.  The function
`mSequence` makes a sequence out of the given phrase using the supplied list of intervals
to transpose the phrase:

```
mSequence :: [Int] -> Music a -> Music a
mSequence [] m = rest 0
mSequence (i:is) m = (transpose i m) :+: (mSeq is m)
```

The last step is to stack the parts on top of one another:

```
duet = bass3 :=: (offset 6 $ transpose 12 $ bass3) :=: (offset 12 $ ostinato2)
```

One plays the piece like this:

```
playDev 6 duet
```

Here the number 6 is the device ID for the synthesizer I happen to be using (fluidsynth).
For MIDI output, I used

```
writeMidi "duet.MID" duet
```

I imported the MIDI file into Logic Pro for processing: balancing the parts, adding more reverb, etc.
The edited MIDI file was exported to an audio file in AIFF format and then converted to MP3:


```
ffmpeg -i duet.aiff duet.mp3
```




## Nervous Chase

 <audio controls>
  <source src="/audio/nervousChase.mp3" type="audio/mpeg">
  Your browser does not support the audio element.
</audio>

[Code](https://github.com/jxxcarlson/euterpea-exercises/blob/master/src/NervousChase.hs)

*Nervous Chase* is an exercise in the use of L-systems in musical composition, per Haskell School of Music, 
chapter 13.  [L-systems](https://en.wikipedia.org/wiki/L-system) were developed in 1968 
by the Dutch-Hungarian theoretical biologist Aristid Lindenmayer as a matheamtical model to describe
the growth and development of organisms such as algae and trees.  Here is a simple example.  The L-system
has two symbols, A and B, where A is the *axiom*.  It also has two *production rules*, A -> AB and B -> A.
Starting with the axiom, one uses the rules to generate ever more complex sequences of symbols:

```
A -> AB -> ABA -> ABAAB -> ABAABABA -> ...
```

One can use a system like this to generate a long string of symbols that can then be transcribed to music.
Here is the *RedAlgae* formal grammar of *The Haskell School of Music:*

```
redAlgae = DetGrammar 'a'
  [('a', "b|c"), ('b', "b"), ('c', "b|d"),
   ('d', "e\\d"), ('e', "f"), ('f', "g"),
   ('g', "h(a)"), ('h', "h"), ('|', "|"),
   ('(', "("), (')', ")"), ('/', "\\"),
   ('\\', "/")]
```

The twelve symbols "a" through "h" represent the twelve notes of a major scale with given starting pitch,
"/" maps to a rest, "\" maps to rest four times as long.
The other symbols map to operators on `Music Pitch` values, with "(" mapping to the operator "transpose up 9 semitones" (a major sixth), and ")" mappping to "transpose down a major sixth."   These are slight variations on the text of Hudak, pp. 186-7.

The function below generates music from the `redAlgae` grammar
 given a length parameter `n`, an absolute pitch `ap`, and a duration value 
for notes, `dur`:

```
lsMusic :: Int -> AbsPitch -> Dur -> Music Pitch
lsMusic n ap dur = 
    strToMusic ap dur $ mconcat $ take n $ detGenerate redAlgae
```

The final piece is constructed from `lsMusic` using the operators `:+:` and `:=:` as well as
functions to modify the performance, e.g., `cre` for crescendo:

```
nervousChase :: Int -> AbsPitch -> Dur -> Music Pitch
nervousChase n ap dur = 
      cre 0.4 $ (instrument Xylophone $ phrase [Dyn (Loudness 70)] $ rest 2 :+: lsMusic n (ap + 7) (dur))
      :=: (cre 0.4 $ (dim 0.2 $ instrument Bassoon $ phrase [Dyn (Loudness 70), Art (Staccato 0.7)] $ lsMusic n ap (dur)))
```

It is important in a piece like this to have some kind of sectional structure.  Quite simple here, but it makes a difference.
The piece is played like this:

```
playDev 6 $ nervousChase 15 40 sn
```

Here `sn` stands for "sixteenth note," i.e., the rational number 1/16.



## Space Invasion


<audio controls>
  <source src="/audio/spaceInvasion.mp3" type="audio/mpeg">
  Your browser does not support the audio element.
</audio>


[Code](https://github.com/jxxcarlson/euterpea-exercises/blob/master/src/SpaceInvasion.lhs)


*Space Invasion* is based on the code and ideas in  [some notes of Donya Quick](https://github.com/Euterpea/Euterpea2-Examples/blob/master/NoteLevel/RandomMusic.lhs).  The main new element here is the 
use of sequences of integers generated by bounded random walk as well as uniformly distributed sequences
of integers.  Here is the bounded random walk generator:

```
boundedRandomWalk :: (Int, Int) -> Int -> Int -> Int -> [Int]
boundedRandomWalk (lowerBound, upperBound) start step seed = 
    recInts (seed + magicNumber) (mkStdGen seed) where
        recInts current g = 
            let 
                (i,g') = next g 
                delta = (2 * (mod i 2) - 1) * step
                current' = bounce (lowerBound, upperBound) 
                           start step $ current + delta
            in current' : recInts current' g'
```

The function of `bounce` is to "bounce" integers into the specified range if they stray from it.
Music is generated from a random walk by the function below:

```
melGen2 :: (Int, Int) -> Int -> Int -> Int -> Music (Pitch, Volume)
melGen2 (lowerBound, upperBound) start step seed = 
    let 
        pitches = map pitch $ boundedRandomWalk2 
                 (lowerBound, upperBound) start step seed
        vols = randIntsRange (40,100) (seed + 1)
    in  line $ map (note sn) $ zip pitches vols
```

There is a similar function `mel1` for generating music from the uniform distribution.
With this code in hand, one can construct the final piece:

```
spaceInvasion s = chord [xylo s, bells s, marimba 12 s]

xylophone :: Dur -> Int -> Int -> Dur -> Dur -> Int -> Music (Pitch, Volume)
xylophone  n l h d r s = 
  instrument Xylophone $ dim d $ rit r $ cut n $ melGen1 (l, h) (345 + s)

marimba :: Dur -> Int -> Music (Pitch, Volume)
marimba n s = 
   instrument Marimba $ cre 0.5 $ acc 0.4  
      $ cut n $ melGen2 (30, 80) 30 2 (234 + s)

tubularBells n l h s = 
   instrument TubularBells $ cut n $ melGen2 (l, h) 45 4 (789 + s)

xylo s =  xylophone 5 10 110 0 0 s :+: rest 2 
          :+: xylophone (2 + hn) 10 110 0.5 0.5 (2 * s)

bells s = rest 1 :+: tubularBells 2 30 60 s :+: rest 1 
          :+: tubularBells 2 20 100 (2 * s)
```

## Using Random Walk to Generate Images


### Random Walk in the Euclidean Plane

<img src="/img/brownianPath.png" width=500>

### Cloud Shapes Generated by Random Walk

<img src="/img/brownianCloud.png" width=500>


##3 Abstract Art Generated by Random Walk

<img src="/img/dark.png" width=500>