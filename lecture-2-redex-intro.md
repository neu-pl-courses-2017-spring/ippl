# Redex tool

We will use *Redex* to define languages and their semantics. Links:

* [PDF](https://plt.eecs.northwestern.edu/snapshots/current/pdf-doc/redex.pdf),
* [Off. doc](http://redex.racket-lang.org/).

...

To make semantics determinitstic we evolve our grammar for contextes:

    E := [] | E or e
    
    e ↪ e'
    -------------
    E[e] => E[e']

