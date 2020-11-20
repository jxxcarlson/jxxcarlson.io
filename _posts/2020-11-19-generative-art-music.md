---
title: Generative Art and Music 
tags: code fp music art rc
---

# RC Friday Show

*November 19, 2020* 

The three pieces below, *Duet*, *Nervous Chase*, and *Space Invaders*, were written using Paul Hudak's Haskell library, *Euterpea*. I've learned everything that went into these compositions from *The Haskell School of Music*, by Paul Hudak and Donya Quick, and also from [Donya Quick's website](http://donyaquick.com/) and other resources she has published on the web.

Here is the [repo for the code](https://github.com/jxxcarlson/euterpea-exercises).  It is badly in need of some cleanup and editing.  Soon!

Below is a short snippet of Euterpea code, the "theme" from which *Duet* is composed.  It reads as follows: *Make a line of music beginning with a whole note D in octave 1, playing first a D minor triad in whole notes.  Follow this by a 5-note passage in quarter notes and end with half-note whole-note resolution.*

```haskell
bass1 :: Music Pitch
bass1 = line $ [ d 1 wn, f 1 wn, a 1 wn,  g 1 1, f 1 qn, e 1 qn, d 1 qn
               , c 1 qn, e 1 hn, d 1 wn]
```	

## Duet


<audio controls>
  <source src="/audio/duet.mp3" type="audio/mpeg">
  Your browser does not support the audio element.
</audio>

This piece is a duet between two bassoon-tuba combos, with a later entrance by a trombone ostinato.  It is composed using quasi-traditional rather than algorithmic methods, building up the piece by successive application of operators like `:+:` and `:=:` — the first joins pieces of music in series while the second stacks them in parallel. Here is a fragment derived from `bass1`:

```haskell
bass2 d = instrument Bassoon $ bass1 
       :=: (instrument Tuba $ transpose 19 $ offset d $ retro $ bass1)
```

It reads as follows: play `bass1` on bassoon and stack it against a line derived from it played on Tuba.  To derive that line, offset `bass1` by `d` whole notes and then transpose it up 19 semitones, that is, an octave and a perfect fifth.  While the delayed entrance can be any rational multiple of a whole note, we use small integer multiples here.  

Note that `bass2` is a function of type `Rational -> Music Pitch`.  We use it to derive a set of four lines which we subsequently join end-to-end:

```haskell
b1 = bass2 0 :+: rest wn
b2 = transpose 5 $ bass2 2 :+: rest wn
b3 = retro $ transpose 7 $ bass2 4 :+: rest wn
b4 = retro $ transpose 5 $ bass2 2 :+: rest wn 
```
Each phrase ends with a whole-note rest so that when the pieces are joined end-to-end, there is 
a bit of intervening silence.  The function `retro :: Music Pitch -> Music Pitch` re-arranges
the given notes in reverse order.  This is a [classic compositional technique](https://en.wikipedia.org/wiki/Retrograde_(music)):

> Retrograde was not mentioned in theoretical treatises prior to 1500.[1] Nicola Vicentino (1555) discussed the difficulty in finding canonic imitation: "At times, the fugue or canon cannot be discovered through the systems mentioned above, either because of the impediment of rests, or because one part is going up while another is going down, or because one part starts at the beginning and the other at the end. In such cases a student can begin at the end and work back to the beginning in order to find where and in which voice he should begin the canons."[2] Vicentino derided those who achieved purely intellectual pleasure from retrograde (and similar permutations)."

A long line is constructed using these derived parts:

```haskell
bass3 = b1 :+: b2 :+: b3 :+: b4 :+: dim 0.6 b1
```

The operator `dim 0.6` applies a *diminuendo* to its argument, the line `b1`. A second part is composed as follows.

```haskell
ostinato1 = instrument Trombone $ sta 0.9 $  
   line [a 3 hn, d 3 hn, c 3 hn,  g 2 hn, e 3 hn, d 3 wn, rest wn]

ostinato2 = mSequence [0, 2, 7, 5, 0] ostinato1 
   :+: (instrument Trombone $ dim 0.5 $ transpose (-5) 
       $ line [a 3 hn, d 3 hn, c 3 hn,  g 2 hn, e 3 wn, d 3 2])
```

The functions `sta 0.9` renders its argument with staccato articulation.  The function
`mSequence` makes a sequence out of the given phrase using the supplied list of intervals
to transpose the phrase:

```haskell
mSequence :: [Int] -> Music a -> Music a
mSequence [] m = rest 0
mSequence (i:is) m = (transpose i m) :+: (mSeq is m)
```

The last step is to stack the parts on top of one another:

```haskell
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

## Space Invasion

<audio controls>
  <source src="/audio/spaceInvasion.mp3" type="audio/mpeg">
  Your browser does not support the audio element.
</audio>


