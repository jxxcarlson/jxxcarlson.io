---
title: "Type Theory, Agda and Some Good Books"
tags: fp
---



In my quest to understand type theory, I came across
links to two very good books. The first,
_[Programming Language Foundations in Agda](https://plfa.github.io/)_,
by Philip Wadler, is available online.  The second,
_Verified Functional Programming in Agda_, by Aaron Stump, is
also quite good, though pricey: $79.95 paperback, $51.19 kindle.
Ouf! I recommend both; they are certainly helping me to understand
the subject better.  The approach using Agda,
which stays close to the type theory of Per Martin-Löf, is
an attractive feature of these books.

### Notes

I've found Emacs to work more reliably with Agda than Atom.
I'd be interested to hear what the experience of others is.

You will
need to install the Iowa Agda Library to do the exercises in
_Verified Programming_.  Then edit the file `$HOME/.agda/libraries` so that
it looks like the below.

```
/usr/local/lib/agda/standard-library.agda-lib
/Users/carlson/dev/agda/ial/.agda-lib
```

Once this is done, the file `$Home/.agda/defaults` must consist of the
line `standard-library` or `ial` as the case may be.  You will have to
create the file corresponding to `/Users/carlson/dev/agda/ial/.agda-lib`:

```
name: ial
include: .
```

### Other Agda resources

- [Agda User Manual 2.6.1](https://buildmedia.readthedocs.org/media/pdf/agda/latest/agda.pdf)
- [Iowa Agda Library](https://github.com/cedille/ial)

There is some interesting material at [Introduction to Dependent Types and Agda,
8th Summer School on Formal Techniques](http://www.cse.chalmers.se/%7Eabela/ssft18/).
Unfortunately, some of the files are corrupted -- a text encoding problem?
