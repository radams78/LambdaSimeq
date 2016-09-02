# LambdaSimeq

This is an implementation of the syntax and semantics of the type theory $\lambda \simeq$ by Andrew Polonsky [1].  It is done in the same style as the project Kipling by Conor McBride [2]; such that definitionally equal terms in the syntax being formalised are mapped to *definitionally* equal terms in the metalanguage (Agda).

# Syntax and Semantics

We define a universe U : Type whose objects are names of types, and a function T : U -> Type; given a name A : U, T A is the type named by A.

We now define simultaneously:
* the contexts Gamma; 
* the interpretation [[ Gamma ]]C : Type of each context Gamma
* the type Type Gamma of types over Gamma

thus:

* The contexts are defined inductively by:
* * The empty context is a context
* * If A is a type over Gamma, then (Gamma, A) is a context
* A type over Gamma is a function [[ Gamma ]]C -> U.
* [[ empty context ]]C = Unit
* [[ Gamma , A ]]C = Sigma gamma : [[ Gamma ]]C. T (A gamma)

Thus, [[ A_1, A_2, A_3 ]] is the type of all triples (x, y, z) such that
x : T A_1,  y : T (A_2 x), and z : T (A_3 x y).

Finally, we define simultaneously:
* The type tj Gamma A of terms in A, for every type A over Gamma
* The interpretation function [[_]] : tj Gamma A -> \forall gamma -> T (A gamma)

We write gamma : Gamma |- A as sugar for tj Gamma (lambda gamma -> A).

This is done in such a way that, if M and N terms in tj Gamma A that are definitionally equal in $\lambda \simeq$,
then [[ M ]] and [[ N ]] are definitionally equal Agda objects.  (Note: this cannot be proved as an Agda proposition,
because definitional equality is a concept on the metalevel.  It must be proved on the metaleval, on paper.)

# files

Internalization.pdf --- The paper [1].  See pages 6-8 for the type theory being implemented.

EqSim.agda --- Defines the universe (U, T) 

Kipling.agda --- Defines contexts, types and terms, as well as semantics for all three.

# References

[1] A. Polonsky.  Internalization of External Equality.  http://arxiv.org/abs/1401.1148  2015

[2] C. McBride.  Outrageous but Meaningful Coincidences: Dependent Type-Safe Syntax and Evaluation.  Proceedings of the 6th ACM SIGPLAN Workshop
on Generic Programming.  New York, 2010.  pp. 1-12