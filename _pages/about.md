---
title: "The MiniLaTex Project"
---

![Image](/img/k2b.png)


  <script type="text/x-mathjax-config">
  (function () {

  MathJax.Hub.Config({
  	'showProcessingMessages': false,
  	'messageStyle': 'none'
  });

  if (typeof MathJaxListener !== 'undefined') {
  	MathJax.Hub.Register.StartupHook('End', function () {
  		MathJaxListener.invokeCallbackForKey_('End');
  	});
  }

  })();
  </script>

  <script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.1/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>

[MiniLaTeX Demo](https://demo.minilatex.app/) | [MiniLaTeX Reader](https://reader.minilatex.app/)
| [KNODE.IO](https://knode.io)

The aim of the MiniLaTex project is to provide a way for authors to write LaTeX documents directly on the web. MathJax does a beautiful job of rendering formulas.  But what about the rest?  Sections, tables, cross-references, hyperlinks, etc.? MiniLaTeX, building on MathJax, handles these and many other elements in a  defined subset of LaTeX, sufficient for writing class materials, [lecture notes](https://knode.io/427), etc.

$$
\int_0^1 x^n dx = \frac{1}{n+1}
$$

Take a look at [MiniLaTeX Demo](https://demo.minilatex.app/) for a little editor that you can experiment with.  Two panels: source text on the left, rendered text on the right. No login required.

**Delivering content**

There are many ways to deliver MiniLaTeX content to colleagues, students, or the general public. One vehicle is the [MiniLaTeX Reader](https://reader.minilatex.app/).  It can sit inside any web page, along with other material.  The app itself is configured to point at MiniLaTeX Notebook: a set of related documents such as a set of lecture notes.  The Reader can be used to access other MiniLaTeX documents as well those to which it points by default.  An institution can deploy as many Readers on its pages as it needs.

Another vehicle is [knode.io](https://knode.io) — *k* for knowldge.  This is a full content management system. To create content, an author simply registers for an account and begins using  the two-panel editor as with [MiniLaTeX Live](https://jxxcarlson.github.io/app/miniLatexLive/index.html).  Once the author makes the document public, it is accessible to everyone.

 While [knode.io](https://knode.io) has its own search engine, which is one way to discover MiniLaTeX documents, there are several other ways to publish: (1)  Authors have a home page on  knode.io where their documents are listed. (2) every document has a numerical ID, just as we have Social Security numbers. It suffices to provide that ID, like this: [knode.io/427](https://knode.io/427).  (3) Embed a link in any web page, e.g., [Lecture 2: Wave Packets](https://knode.io/427).

**Use in courses**

 MiniLaTeX has been used for courses at the Beijing International Center For Mathematical Research (BICMR), Ohio State University and Colorado State University. Here is one example, a set of lecture notes for a course I taught at BICMR and OSU: [Notes on Quantum Field Theory](https://knode.io/427).


**Contact**
If you have questions or comments regarding MiniLaTeX or the MiniLaTeX services above, please contact Jim Carlson:

 - **Email:** jxxcarlson at gmail
 - **Phone:** 617-852-7490
 - **Twitter:** @epsilon2718

We plan to make substantial improvements to all parts of the project over the summer of 2019.

— [Jim](https://jxxcarlson.io)

PS. I am giving a talk on MiniLaTeX on Friday, June 9 at [Lambda Conf 2019](https://lambdaconf.zohobackstage.com/LambdaConf2019?lang=en#/agenda?day=3&lang=en&sessionId=6967000000359716) in Boulder Colorado.

[Talks on MiniLaTeX](https://minilatex.io/talks.html)
