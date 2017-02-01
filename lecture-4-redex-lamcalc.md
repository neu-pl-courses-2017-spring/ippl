## Redex (contd. #2)

Accumulator-based metafunctions. `redex-check`.

## Lambda Calculus

    e ::= x | \x.e | e e

Strategies for \beta-reduction:

1. Full \beta-reduction -- non-deterministic choise of next redex.

2. Call by value (CBV, strict, eager). -- reduce ??? first. We need to define what *value* is:

        v ::= \x.e

    We'll use a formal notation to define CBV, namely, SOS. 
    
        e1 -> e1'
        ---------
        e1 e2 -> e1' e2

        e2 -> e2'
        ---------
        v e2 -> v e2'
        
        -------------
        (\x.e) v -> e[v/x] 
        
3. Call by name (CBV, non-strict, sometimes, falsly reffered as lazy). -- reduce ??? first. 

        e1 -> e1'
        ---------
        e1 e2 -> e1' e2

        -------------
        (\x.e) e' -> e[e'/x] 

Different strategies can yield different results when term under consideration is diverging.

## Encoding in Lambda

If-then-else.

