---
title: "Math Markdown"
tags: minilatex
---


 <script type="text/x-mathjax-config">
  (function () {

    MathJax.Hub.Config(
  				{ tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]},
  					processEscapes: true,
  					messageStyle: "none",
  					processSectionDelay: 0,
  					processUpdateTime: 0,
  					"fast-preview": {disabled: true},
  					TeX: { equationNumbers: {autoNumber: "AMS"},
  						   noErrors: {disabled: true},
  						   extensions: ["mhchem.js"]
  						  }
  				}
  	        );

  if (typeof MathJaxListener !== 'undefined') {
  	MathJax.Hub.Register.StartupHook('End', function () {
  		MathJaxListener.invokeCallbackForKey_('End');
  	});
  }

  })();
  </script>

  <script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.1/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>


MathMarkdown is a dialect of Markdown that renders
mathematical source text written in TeX/LaTeX.  Thus,
if one writes

```
$$
  f(a) = \frac{1}{2\pi i} \oint\frac{f(z)}{z-a}dz
$$
```

it appears as

$$
  f(a) = \frac{1}{2\pi i} \oint\frac{f(z)}{z-a}dz
$$

See [markdown.minilatex.app](https://markdown.minilatex.app)
for an interactive demo.

## Using Math Markdown

Math Markdown on open-source Elm package:
[jxxcarlson/math-markdown](https://package.elm-lang.org/packages/jxxcarlson/math-markdown/latest/).
Once installed, you can say

```
MMarkdown.toHtml [ ] "This *is* a test $a^2 + b^2 = c^2$."
``

to produce the rendered text: This *is* a test: $a^2 + b^2 = c^2$

For interactive editing, as in the demo app, one uses a somewhat
more elaborate setup wherein only changes to the text are parsed
and rendered.
Code for the demo app is in this package under the `./app` directory.

## Status and Plans

Math Markdown is a very young project, with its
initial commit on June 13, 2019.  It is still experimental.
After some more testing, I plan to add it to [knode.io](https://knode.io)
Please send comments and bug reports jxxcarson at gmail.
