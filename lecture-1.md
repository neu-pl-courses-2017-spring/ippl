# Goals

We want to know:

* if a program is correct;
* if refactoring yields equivalent program;
* if optimization yields equivalent program;
* etc.

We would like to have *formal tools* to assist int this.

## Topics

### Different styles of semantics?

1. Dynamic (operational) semantics of a program -- how program is going to be evaluated,
2. axiomatic s. -- start from a number of equations, define the consequences.
3. denotational s. -- define a functions which denotes the meaning of eash program 
construct. Becomes infeasible for real-world languages.

### Dynamic vs. static

In this course we'll focus on p. 1. We will use untyped languages at the begining. 
Than we'll come to the idea of a type system and static semantics.

### Language features

Exceptions, continuations, polymorphism, objects, subtyping.

# Admission

6-7 assignments in pairs, switch a partner in the middle.

1 mini-project, also with a partner: pick up a research paper, dig in it deeply.

## References

See [off. site](http://www.ccs.neu.edu/home/amal/course/7400-s17/). Check out the Blog there also.

Midterm (March 17) + final exam (April 24 + or - week).

# A Language for Boolean Expressions

    e ::= tru | fls | e or e | not e

(You could also put `e1 or e2` instead of `e or e`.) Tell me some examples of programs
in this language. Try to do it ``inductively'' (``in layers'').

We used BNF above but we also could go inductively, define a set `T` of valid terms in this language:

1. `{tru, fls} \subset T.`
2. If `e1 \in T and e2 \in T` then `e1 or e2 \in T.`
3. If `e \in T` then `not e \in T.`

We could also go axiomatically:

    ------------
    tru \in T


    ------------
    fls \in T

    e1 \in T, e2 \in T
    -------------------
    e1 or e2 \in T

    e \in T
    -------------------
    not e \in T


As an example of terms we encountered one with *parenthesis*. These are the part of 
**concrete syntax**. Our grammar instead gives an **abstract syntax** -- rules for
building ASTs. In order to recover particular AST from a term we have to give a hint,
what we meant. Parenthesis do just this.

## Axiomatic semantics for the languages

    tru or e == tru
    fls or e == e
    not e == ???

(== stands for $\equiv$) Here we define *a realtion* between valid terms of our languages. Its ought to be 
an equivalence relation: the refl., symm., trans. rules were omited.

## Operational semantics

Define relation `↪` on terms.

    tru or e ↪ tru
    fls or e ↪ e

We also would like to use `↪*` -- a transitive closure (multi-step version of 
`↪`-relation).

Our set of rules is actually incomplete: not all the complex expressions can be 
simplified. We would like to allow apply our rules to *subexpressions*. In order 
to formalize we will invent a notion of **expression context**:

    C ::= [] | [] or e | e or []     // WRONG

This in fact is wrong, because again we cant get a hole somewere in the leaf nodes
of AST. THe right grammar is not much more complex:

    C ::= [] | C or e | e or C     // WRONG

Now we could define a mapping for filling-in the holes: $(e, C) \to C[e]$ 
(the result is expression, of course) and extend ↪:

    e1 ↪ e2, C is a context
    ------------------------------
    C[e1] ↪ C[e2]

