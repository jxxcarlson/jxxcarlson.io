---
title: "A Fake Drum Language App"
tags: elm
---

![Slit drum](http://noteimages.s3.amazonaws.com/jim_images/slit-drums.png)

[>> Fake Drum Language App](https://jxxcarlson.github.io/app/drumlanguage.html) — only works in Firefox

## The Information (James Gleick)

Some time ago, I read James Gleick's book *The Information: a History,
a Theory, a Flood.*  In the first chapter, he recounts the remarkable
discovery of John F. Carrington, an English missionary, who took up
residence in the Congo in 1938, working for the Baptist Missionary Society.
On a trip from the Society's Yakutsu station on the Upper Congo River
through the Bambole Forest, he realized that the local people were able to
use drums to send detailed messages over long distances.  Here
is an example, a funeral announcement:

> _La nkesa laa mpombolo, tofolange benteke biesala, tolanga bonteke bolokolo bole nda elinga l’enjale baenga, basaki l’okala bopele pele. Bojende bosalaki lifeta Bolenge wa kala kala, tekendake tonkilingonda, tekendake beningo la nkaka elinga l’enjale. Tolanga bonteke bolokolo bole nda elinga l’enjale, la nkesa la mpombolo._

> In the morning at dawn, we do not want gatherings for work, we want a meeting of play on the river. Men who live in Bolenge, do not go to the forest, do not go fishing. We want a meeting of play on the river, in the morning at dawn.

It took Carrington some time to decipher the secret of the drums.  The key
fact was that the local language
was a tonal one, with two tones, high and low.  The drummers, using slit drums,
would sound the tones of the words to be sent.  Thus
*alambaka boili*, meaning "he watched the riverbank," was rendered as
**H L H H L L L**, where **H** is a high-pitched sound and **L** is low-pitched.
While much information is lost in this pitch encoding, that which remains,
plus the context, plus the use of many conventional formulae, gives the listener enough
information to reconstruct the original sentence.

## An App

As a completely useless but fun exercise, I decided to make a
little app that will turn text into (a fake) drum language.  My approach
was to map each letter a--z to a phonetic class, then map phonetic
classes to musical pitches.  The phonetic class of *a, e, i, o, u*
is VOWEL.  Consonants are divided into various classes, e.g., *m, n*
of type NASAL.  Each class is assigned a pitch, and so any string of
characters is mapped to a sequence of pitch names.  For example, *Hello*
is assigned the sequence **G3 G2 C3 C3 G2**.  Here the numerical part
of a pitch name refers to its octave.  Thus G3 is one octave higher than G2.
The pitches used to represent the pitch classes are **G2 C3, E3, F3, G3, Bb3, D**
— a dominant ninth chord.  This choice of mapping makes the drumming sound
relatively harmonius.

The string "G3 G2 C3 C3 G2" in the example just given is
sent to the computer's audio processor to be rendered for the
user's listening enjoyment.  The app, which you may try out
**[(HERE)](https://jxxcarlson.github.io/app/drumlanguage.html)**, looks like this:

![Drum app](http://noteimages.s3.amazonaws.com/jim_images/drum_app.png)

The code is available on [GitHub](https://github.com/jxxcarlson/DrumLanguage).
The app is written in [Elm](https://elm-lang.org/) and renders audio
by sending a string of note values to `Tone.js` using ports.

NOTE: The mapping of letters to phonetic classes is crude, since
English spelling is far from phonetic.  A better implmenetation
would employ a more faithful mapping.

## Postscript

Gleick writes that Carrington eventually learned to drum, mainly in Kele, a
Bantu language in what is now Eastern Zaire.  He recounts this story:

> *A Lokele villager said of Carrington "He is not really
European, despite the color of his skin. He used to be from
our village, one of us. After he died, the spirits made a mistake
and sent him off far away to a village of whites to enter the
body of a little baby who was born of a white woman instead
of one of ours. But he belongs to us, he could not forget where
he came from, and so he came back.  If he is a bit awkward on the
drums, this is because of the poor education that the whites gave him."*

There is much more in Gleick's book. It is really good read.
