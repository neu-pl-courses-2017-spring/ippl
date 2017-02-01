## Formalizing Substituion and Accompaining

We often put function being defined into a box -- that is on purpose: we are interested in the *shape* of definition.

    FV(x) = {x}
    FV(\x.e) = FV(e) - {x}
    FV(e1 e2) = FV(e1) \cup FV(e2)
    
Note that we are recursive *but*: each time recursive call appeals to smaller term. That insures termintation.

Make sure that substitution cannot be defined naively... Not let us define “capture-avoiding substitution”: 

    e[e' / x]

We do it inductively again and the induction goes on `e`.

    x[e' / x] = e'
    y[e' / x] = y     // y != x
    e1 e2[e' / x] = e1[e' / x] e2[e' / x]
    (\x.e)[e' / x] = \x.e // note: we substitute things in place of 
                          //       *free* occurencesof a variable
    (\y.e)[e' / x] = \y.e[e' / x],  y != x, 
                                    y \not\in FV(e')  // note: we always hit
                                                      // this case when subst.
                                                      // in lambda given 
                                                      // call-by-value strategy
    ... // last, hairy case

Though LC was born in 30-x it was not until 50-s when people got right definition of substitution.

### Equivalences for lambda-term

    \x.e =_α \y.e[y/x]          // y \not\in FV(e)
    (\x.e) e' =_β e[e' /x]
    \x.ex =_η e                 // x \not\in FV(e)


**General notion of equivalence for l-terms**

    C ::= [] | \x.C | C e2 | e1 C
    
    e ⇓ v iff e ->* v

Now, the climax:
    
    e1 \equiv_{ctx} e2 =_{def} \forall C. C[e1] ⇓ v ⇔ C[e2] ⇓ v
    
It is not good: v could be different, but alpha-equivalent to each other. Try instead (and this time it is correct):

    e1 \equiv_{ctx} e2 =_{def} \forall C. C[e1] ⇓ ⇔ C[e2] ⇓

where ⇓ means temination. The trick here: if C[e1] and C[e2] is going to end up with substantially different values  then you always can build a larger context `C'` which diverges when plugging in `e1` and happily converges with `e2`.

Note on terminology: `e1 \equiv_{ctx} e2` sometimes called `e1 \equiv_{obs} e2`, that is *context equivalence* is exactly *observational equivalence*.

## Nameless lambda-notations

**Stoy diagramm:** erase lambda-captured names and put arrows between places and corresponding lambdas.

We do not like arrows, so we introduce **De Brujin notation**...


## 

Recall that we defined reduction strategies by means of logical relations. We can try another way (already presented for BOR language).

First, define *computational context*:

    E :== [] | E e | v E

Then, the whole CBV is formulated like this:

    -----------------
    (\x.e)v -> e[v/x]
    
    e -> e'
    -------------
    E[e] => E[e']

*Maditation*: the grammar of `E` is lead by an idea, you put `E` in spots of original grammar which you want to be reduced first. Then you add corresponding cases with `v` in place of `E`.



