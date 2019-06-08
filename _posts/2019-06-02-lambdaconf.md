---
title: "LambdaConf 2019"
tags: minilatex
---

I'm giving a [talk on MiniLaTex Friday](https://lambdaconf.zohobackstage.com/LambdaConf2019?lang=en#/agenda?day=3&amp;lang=en&amp;sessionId=6967000000359716), June 7
on MiniLaTeX at LambdaConf 2019. Mostly about
the parser, some about rendering the AST,
the diffing algorithm used to speed up the parse-render pipeline,
and a little bit about some abstractions that
make the code a lot easier to work with, e.g.:

```
{-| Given an initial state and list of inputs of type a,
produce a list of outputs of type b and a new state
-}
type alias Accumulator state a b =
    state -> List a -> ( List b, state )
```

MiniLaTeX is written in [Elm](https://elm-lang.org/) and uses the
[elm/parser](https://package.elm-lang.org/packages/elm/parser/latest/) package.

[Slides (keynote)](http://jxxslides.s3.amazonaws.com/Lambda_Conf_2019b.key) |
[Slides (powerpoint)](http://jxxslides.s3.amazonaws.com/Lambda_Conf_2019.pptx)
