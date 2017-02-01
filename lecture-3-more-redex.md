# Redex tool (cont.)

`term` is just a quote.

When defining programs use the HDtP recipe.

Lists in Redex: `(x ...)` for list of trees defined by non-terminal `x`(so the lists are homogeneous).

Try to avoid escaping to Racket from Redex as much as possible. E.g. to concate two lists you'd better pattern match on them to extract contents and put them in one list:

    (x1 ... x2 ...)
    (where (x1 ...) l1)
    (where (x2 ...) l2)

instead of using Racket `list-append`.

If you have `x` in your grammar, you can use `x_1`, `x_2`, etc.

Comments in Racket: 

* `#| ... |#` -- ordinary multiline comments.
* `#; ( ... )` -- for commenting out everything in parens.

Consider beautiful function to lookup in a list:

    (lookup x ((y ... x z ...) 'found)

`a ...` should be read like `a*` in regular exprs.

