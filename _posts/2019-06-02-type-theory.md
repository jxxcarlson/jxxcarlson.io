---
title: "Type Theory, Agda and Some Good Books Thereon"
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
which stays close to the type theory of Swedish philosopher-logician
Per Martin-Löf, is an attractive feature of these references.

### Some progress

For the last few days I've been working on both
Wadler's notes (PLFA) and Stump's book (VFPA), going through
all the examples with Agda (in Emacs).  If you
are an Agda && type-theory novice, as am I, I'd
recommend working through the first three
chapters of VFPA before starting PLFA.  VFPA
has very detailed explanations of the Agda proofs,
as well as practical advice on using Agda.  I found
the explanation of `rewrite` om VFPA especially
helpful.

My current *modus operandi* is to have an Emacs
window open on the left, and either PLFA or VFPA
open on the right.

### Notes

I've found Emacs to work more reliably with Agda than Atom.
I'd be interested to hear what the experience of others is.
See Appendix C below for the Emacs macros in Stump's book.
They go in your .emacs file.

You will
need to install the Iowa Agda Library to do the exercises in
_Verified Programming_.  The README for the
[IAL GithHUb repo](https://github.com/cedille/ial) has
installation instructions. After the library is installed,
tedit the file `$HOME/.agda/libraries` so that
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

Here is a little shell script for switching back and forth between libraries: [gist](https://gist.github.com/jxxcarlson/8202938cd4c5eb72d8b5086995880700).

### Other Agda resources

- [Agda User Manual 2.6.1](https://buildmedia.readthedocs.org/media/pdf/agda/latest/agda.pdf)
- [Iowa Agda Library](https://github.com/cedille/ial)
- [Learn You an Agda](http://learnyouanagda.liamoc.net/pages/introduction.html)
- [Learn You an Agda, markdown edition](http://learnyouanagda.liamoc.net/)

There is some interesting material at [Introduction to Dependent Types and Agda,
8th Summer School on Formal Techniques](http://www.cse.chalmers.se/%7Eabela/ssft18/).
Unfortunately, some of the files are corrupted -- a text encoding problem?

### Appendix C of VFPA

**NOTE:** I'm on Mac OS and found that for some reason C-c C-,
doesn't work.  I changed C-, to C-j in the below; that works fine.

```
; This defines backslash commands for some extra symbols.
(eval-after-load "quail/latin-ltx"
  '(mapc (lambda (pair)
        (quail-defrule (car pair) (cadr pair) "TeX"))
  '( ("\\bb" "B") ("\\bl" "L") ("\\bs" "S")
     ("\\bt" "T") ("\\bv" "V") ("\\cv" "g")  

     ("\\comp" "◦") ("\\m" "↦") ("\\om" "ω"))))

; This sets the Ctrl+c Ctrl+k shortcut to
; describe the character under your cursor.
(global-set-key "\C-c\C-k" 'describe-char)
; Change Ctrl+c Ctrl+, and Ctrl+c Ctrl+.
; in Agda mode so they show the normalized rather
; than the "simplified" goals
(defun agda2-normalized-goal-and-context ()
  (interactive)
  (agda2-goal-and-context '(3)))
(defun agda2-normalized-goal-and-context-and-inferred ()
  (interactive)
  (agda2-goal-and-context-and-inferred '(3)))
(eval-after-load "agda2-mode"
  '(progn
    (define-key agda2-mode-map (kbd "C-c C-,")
      'agda2-normalized-goal-and-context)
    (define-key agda2-mode-map (kbd "C-c C-.")
      'agda2-normalized-goal-and-context-and-inferred)))


; This sets the Agda include path.
; Change YOUR-PATH to the path on your computer
; to the Iowa Agda Library directory. Use forward
; slashes to separate subdirectories.
(custom-set-variables '(agda2-include-dirs (quote ("." "YOUR-PATH/ial"))) )

Stump, Aaron. Verified Functional Programming in Agda (p. 252).
Association for Computing Machinery and Morgan & Claypool Publishers. Kindle Edition.
```
