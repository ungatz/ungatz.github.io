+++
title = "Category Theory or: How to live without elements, using arrows instead (Part II)"
author = ["Sanad"]
date = 2023-06-26T11:59:00-04:00
lastmod = 2023-07-29T18:02:41-04:00
tags = ["math", "category-theory"]
categories = ["blog"]
draft = false
math = true
license = ""
+++

In the preceding post, we did a rudimentary survey of the principal elements comprising the apparatus of category theory. Henceforth, we shall direct our gaze towards the intricate constituents conjured by these foundational elements, plunging further into the intricate labyrinth of interwoven components in the machinery of category theory.

<div class="ox-hugo-toc toc">

<div class="heading">Table of Contents</div>

- [Higher Category Theory](#higher-category-theory)
    - [**Cat** : Category of _small_ categories](#cat-category-of-small-categories)
    - [**2** Category](#2-category)
- [Universal Construction](#universal-construction)
    - [Universal Property](#universal-property)
    - [Example of Universal Property](#example-of-universal-property)
        - [Products](#products)
- [Adjunctions](#adjunctions)
    - [Equivalence of Categories Once more...](#equivalence-of-categories-once-more-dot-dot-dot)
    - [Adjunctions](#adjunctions)
    - [Example of Adjunctions](#example-of-adjunctions)
        - [Curry in Haskell](#curry-in-haskell)
        - [Connections of Galois](#connections-of-galois)
- [Monads](#monads)
    - [Monoid](#monoid)
        - [Classical monoid](#classical-monoid)
        - [Category of Monoids](#category-of-monoids)
    - [Monad](#monad)
        - [Examples of Monads](#examples-of-monads)
            - [A Monad for moniod in the \\(\textbf{Set}\\)](#a-monad-for-moniod-in-the-textbf-set)
            - [Monads in Computer Science](#monads-in-computer-science)
                - [Monads in Haskell](#monads-in-haskell)
- [References](#references)

</div>
<!--endtoc-->



## Higher Category Theory {#higher-category-theory}

Higher category theory deals with the generalization of parts that make up machinery. In this realm, we erect structures in a context where, between objects, we have not only mere _morphisms_ but **k**-_morphisms_, which are maps between **(k - 1)** of those morphisms where \\(k \in \mathbb{N}\\).


### **Cat** : Category of _small_ categories {#cat-category-of-small-categories}

-   This is the realm wherein categories, whose assemblage of objects coalesces into a mere set, find their dwelling. Functors serve as the conduits between these categories, linking them in \\(\textbf{Cat}\\).


### **2** Category {#2-category}

-   **2**-Category is the generalization of the notion of _category_ itself. Since **2**-Category is a category, it has objects and 1-morphisms; additionally, it has morphisms between 1-morphisms called 2-morphisms. Just as one can compose  1-morphisms along objects (horizontal composition), one can also compose 2-morphisms along 1-morphisms (vertical  composition) as shown below.
    -   Horizonal Composition, if \\(F\_1, G\_1 : A \to B\\), \\(F\_2, G\_2 : B \to C\\) and \\(\alpha : F\_1 \Rightarrow G\_1\\), \\(\beta : F\_2 \Rightarrow G\_2\\) then
        \\(\beta \circ \alpha : (F\_2 \circ F\_1) \Rightarrow (G\_2 \circ G\_1)\\),
    -   Vertical Composition, if \\(F, G, H : A \to B\\) and \\(\alpha : F \Rightarrow G\\), \\(\beta : G \Rightarrow H\\) then,

        <style>.org-center { margin-left: auto; margin-right: auto; text-align: center; }</style>

        <div class="org-center">

        ![](/draws/horizcomp.png)
        ![](/draws/verticomp.png)

        </div>


## Universal Construction {#universal-construction}


### Universal Property {#universal-property}

-   Meandering through a category, one is bound to find similar patterns among different constructions. A universal property abstracts these similarities and  bestows significance on a generalized construction within the vast universe it inhabits. It is universal in the same sense that it describes an object in relation to the  entire universe in which it lives. The universal construction encapsulates our idea of the concept that the construction conveys by determining it up-to-isomorphism; since this idea happens to come up again and again in mathematics, so do the universal constructions (maybe in a different form). In the last post, we described representable functors, limits, and co-limits; all of these are universal constructions. Here are some more constructions:


### Example of Universal Property {#example-of-universal-property}


#### Products {#products}

-   In any category \\(\mathbb{C}\\) the following diagram is called the product diagram, where \\(A, B, \pi\_1, \pi\_2, X, f, g
      \in\mathbb{C}\\),

    <style>.org-center { margin-left: auto; margin-right: auto; text-align: center; }</style>

    <div class="org-center">

    ![](/draws/prod.png)
    ![](/draws/prodx.png)
    ![](/draws/prodump.png)

    </div>

    This diagram must satisfy the following universal property: if we have a similar diagram,  then there **exists a unique** morphism \\(h: X \to A \times B\\) such that,

    -   \\(h \circ \pi\_1 = f\\)
    -   \\(h \circ \pi\_2 = g\\)
    -   Given any \\(u : X \to A \times B\\) such that \\(u \circ \pi\_1 = f\\) &amp; \\(u \circ \pi\_2 = g\\) then \\(u=h\\).
-   In almost every programming languages, you'll find products implemented as pairs, with their distinct types and two constructors much like \\(\pi\_1\\) and $&pi;_2", granting access to the pair's first and second elements, respectively.
    ```haskell
     example :: (Int, String)
     example = (111, "Apples")

     number  = fst example
     string  = snd example
    ```


## Adjunctions {#adjunctions}


### Equivalence of Categories Once more... {#equivalence-of-categories-once-more-dot-dot-dot}

-   In the last post, we described the [equivalence of categories](https://ungatz.github.io/posts/2023-06-04-category-theory-or-how-to-live-without-elements-using-arrows-instead/#equivalence-of-categories) via the functors going in and through two categories. But functors alone cannot capture  this idea of equivalence completely, for they are made of two things objects and morphisms, and can at the same time be  those two things. Since functors are morphisms in the category of small categories , **Cat** it makes sense to think about  functor equivalence in terms of morphisms between functors, i.e. natural transformations. With this new knowledge, here is a better definition of the equivalence of categories. Two categories \\(\mathbb{C}\\) and \\(\mathbb{D}\\) are equal if one can find two functors \\(F\\) and \\(G\\) that go back and forth between these categories such that their composition is _[naturally isomorphic](https://ungatz.github.io/posts/2023-06-04-category-theory-or-how-to-live-without-elements-using-arrows-instead/#natural-isomorphisms)_ to the identity functor.
    -   \\(G \circ F \cong \mathbb{1}\_{\mathbb{C}}\\)
    -   \\(F \circ G \cong \mathbb{1}\_{\mathbb{D}}\\)


### Adjunctions {#adjunctions}

-   An adjunction is a weaker notion of equivalence defined above in the sense that it does not impose the natural isomorphism  between composition of functors and identity. Instead, it imposes the existence of the following isomorphism: for  \\(c\in\mathbb{C}\\) and \\(d\in\mathbb{D}\\),

    <style>.org-center { margin-left: auto; margin-right: auto; text-align: center; }</style>

    <div class="org-center">

    \\(hom\_{\mathbb{d}} (fc, d) \cong hom\_{\mathbb{c}} (c, gd)\\)

    </div>

    <style>.org-center { margin-left: auto; margin-right: auto; text-align: center; }</style>

    <div class="org-center">

    {{< figure src="/draws/adjnc.png" >}}

    </div>
-   Here, \\(F\\) is called the left adjoint of functor \\(G\\) written as \\(F \dashv G\\) if whenever for \\(c \in \mathbb{C}\\) and \\(d \in  \mathbb{D}\\) all the maps from
    \\(Fc \to d\\) are the same as maps from \\(c \to Gd\\). This structure with two functors and the above isomorphism is called an adjunction.


### Example of Adjunctions {#example-of-adjunctions}


#### Curry in Haskell {#curry-in-haskell}

-   In the category of sets (\\(\textbf{Set}\\)) all the objects can be combined by forming their Cartesian product.  Which is just another object in \\(\textbf{Set}\\): \\(A \times B\\) which is the set of all ordered pairs \\((x, y)\\) such that \\(x \in A\\) and \\(y  \in B\\). This construction is the same as [ products](#products) described earlier.
-   We can also express another set or object as \\(B^A\\) in that it is the same as \\(hom\_{\textbf{Set}}(A, B)\\) i.e. it has all the functions between \\(A\\) and \\(B\\).
-   Now, let's fix the set \\(B\\) we get from the following functors:

    <style>.org-center { margin-left: auto; margin-right: auto; text-align: center; }</style>

    <div class="org-center">

    \\(\\\_ \times b : \textbf{Set} \to \textbf{Set}\\)
    \\((\\\_)^b : \textbf{Set} \to \textbf{Set}\\)

    </div>
-   If one thinks of types as sets, then the morphism \\(\lambda.g : \\\_ \to (\\\_)^B\\) represents the function that takes in a value from some arbitrary type and returns the _function type_. Moreover, if we are given this \\(\lambda g\\) then we can easily get \\(g: \\\_ \times B \to C\\) and vice versa,
    -   From, \\(g: \\\_ \times B \to C\\)
    -   We can define a \\(g' : \\\_ \to C^B\\) as \\((g'(a))(b) = g (a,b)\\) where \\(a \in \\\_\\) and \\(b\in B\\).
    -   Similarly from, \\(f: \\\_ \to C^B\\)
    -   We can define a \\(f': \\\_ \times B \to C\\) as \\(f'(a, b) = (f(a))(b)\\) where \\(a \in \\\_\\) and \\(b\in B\\).

        <style>.org-center { margin-left: auto; margin-right: auto; text-align: center; }</style>

        <div class="org-center">

        ![](/draws/curry.png)
        ![](/draws/curryii.png)

        </div>
-   This method of obtaining a function (with one argument) that returns another function (which takes
    two arguments) is called currying, and its reverse is called uncurry.
    ```haskell
    curry :: ((a, b) -> t) -> a -> b -> t
    curry f a b = f (a, b)

    uncurry :: (t1 -> t2 -> t3) -> (t1, t2) -> t3
    uncurry g (a, b) = g a b
    ```

-   Similarly, one can show that there is a canonical bijection here that programmers can understand intuitively, i.e.,

    <style>.org-center { margin-left: auto; margin-right: auto; text-align: center; }</style>

    <div class="org-center">

    \\(hom\_{\textbf{Set}} (A \times B, C) \cong hom\_{\textbf{Set}} (A, C^B)\\)

    </div>
-   Since we now have two functors and an isomorphism, we've got ourselves an adjunction here for every set \\(B\\).

    <style>.org-center { margin-left: auto; margin-right: auto; text-align: center; }</style>

    <div class="org-center">

    {{< figure src="/draws/curryadj.png" >}}

    </div>


#### Connections of Galois {#connections-of-galois}

-   This example requires some jargon,
    -   **Partially Ordered Sets**: A set where elements have order among them, i.e., some way to compare every single element
        but it is partial in the sense that pairs of elements need not be comparable.
    -   **Monotone Functions**: These are the functions between ordered sets that preserve the order, i.e., when plotted, they either increase or decrease throughout their domains.
-   Now, let \\((A, \leq)\\) and \\((B, \leq)\\) be two partially ordered sets, and then the (monotone) Galois connection between these posets consists of two monotone functions: \\(f : A \to B\\) and \\(g : B \to A\\), such that for all \\(a \in A\\) and \\(b \in B\\),

    <style>.org-center { margin-left: auto; margin-right: auto; text-align: center; }</style>

    <div class="org-center">

    \\(f(a) \leq b\\) if and only if \\(a \leq g(b)\\)

    </div>

    From the lens of category theory, one can say that a Galois connection is nothing but an adjoint \\(f \dashv g\\) equipped with the essential property that an upper or lower adjoint of a Galois connection uniquely determines the other:

    -   \\(f(a)\\) is the least element \\(minB\\) in set \\(B\\) when \\(a \leq g(minB)\\).
    -   \\(g(b)\\) is the largest element \\(maxA\\) in set \\(A\\) when \\(f(maxA) \leq b\\).


## Monads {#monads}


### Monoid {#monoid}


#### Classical monoid {#classical-monoid}

-   A _monoid_ is defined as a set with an associative binary operation and a special element that acts as a unit with respect
    to that set.
-   Example: the set of natural numbers \\(\mathbb{N}\\) for a monoid with addition or multiplication as the operation and \\(0\\) or \\(1\\)  as the unit, respectively.


#### Category of Monoids {#category-of-monoids}

-   We want to think of classical monoid in terms of morphisms. So, imagine we
    have a set (\\(S\\)) and a binary function (\\(f\\)) that operates on the elements of that set. Moreover, if one of the inputs to this function is a special element of \\(S\\) called _unit_ then the output of the function is the same as the second input, whatever that may be.
-   We thus define _monoid_ as a single object category. Since it's a single object, we have a single hom-set which is the set  that has all the morphisms from the object to itself.
-   The interesting thing is that we can get the same results from going inside the object and using the function (multiply or  add etc.) and composing the function in the before-mentioned hom-set.


### Monad {#monad}

-   A monad on some category \\(\mathbb{C}\\) is a triple \\((T,\eta,\mu)\\)  which consists of,

    -   A functor, \\(T : \mathbb{C} \to \mathbb{C}\\).
    -   A unit natural transformation, \\(\eta : \mathbb{1}\_{\mathbb{C}} \Rightarrow T\\).
    -   A multiplication natural transformation, \\(\mu : T \times T \Rightarrow T\\).

    such that the following diagrams in the functor category \\(\mathbb{C}^{\mathbb{C}}\\) commute, i.e. to say for all \\(c \in
      \mathbb{C}\\) the following diagrams commute when functors are applied to \\(c\\) (\\(Tc\\)) and when components of natural transformations (\\(\eta\_c\\), \\(\mu\_c\\)) are considered, then these diagrams commute in \\(\mathbb{C}\\),

    <style>.org-center { margin-left: auto; margin-right: auto; text-align: center; }</style>

    <div class="org-center">

    Associativity Square:
     ![](/draws/monadi.png)

    </div>

    <style>.org-center { margin-left: auto; margin-right: auto; text-align: center; }</style>

    <div class="org-center">

    Unit Triangles:
     ![](/draws/monadii.png)

    </div>
-   One may also say that a monad is a generalization of [monoid](#category-of-monoids).


#### Examples of Monads {#examples-of-monads}


##### A Monad for moniod in the \\(\textbf{Set}\\) {#a-monad-for-moniod-in-the-textbf-set}

-   \\(\mathbb{C} = \textbf{Set}\\)
-   \\(T : X \to X^\star\\) where \\(X\\) is a [classical monoid](#classical-monoid) in \\(\textbf{Set}\\) and \\(X^\star\\) is the [kleene star](https://en.wikipedia.org/wiki/Kleene_star) over \\(X\\).
-   \\(\eta\_x : Tx \to x^\star\\)  for all \\(x \in X\\)
-   \\(\mu\_x : x^{\star\star} \to x\\) for all \\(x \in X\\)
-   For unit triangles, consider, \\(x = (a, b, c)\\) where \\(x \in X\\) then,
    -   \\(T (\eta (x)) = ((a), (b), ( c))\\)
    -   \\(\mu (T (\eta (x))) = x\\)
    -   Similarly,
    -   \\(\mu (\eta (T x)) = x\\)
-   Similarly, associativity square.


##### Monads in Computer Science {#monads-in-computer-science}

-   In this world, programs denote the morphisms between objects \\(A\\) and \\(TB\\) where \\(A\\) is the object of **values** of _type_ \\(A\\)  and \\(TB\\) is the object of **computations** of type \\(B\\). These programs are functions that are generated through a maze of computations.
-   For the existence of a monad in such a category, these programs must form a **kliesli category**.
-   A **kliesli triple** over \\(\mathbb{C}\\) is the triple \\((T, \eta, \\\_^\star)\\) where,

    -   \\(T: Obj(\mathbb{C}) \to Obj(\mathbb{C})\\)
    -   To give values to a computation: \\(\eta\_A : A \to TA\\) where \\(A \in \mathbb{C}\\).
    -   An extension to \\(f\\) from _values_ to _computation_ to _computation_ to _computation:_ \\(f^\star : TA \to TB\\) for \\(f: TA \to TB\\)
    -   \\(\eta\_A^\star = \mathbb{1}\_{TA}\\)
    -   \\(\eta\_A;f^\star = f\\)
    -   \\(f^\star ; g^\star = (f;g)^\star\\)

    The equations for _kliesli triples_ form a category, i.e. the **kliesli category** (\\(\mathbb{C}\_T\\)) such that given a kliesli
    triple \\((T, \eta, \\\_^\star)\\) , \\(\mathbb{C}\_T\\) is defined as,

    -   \\(Obj(\mathbb{C}\_T) = Obj(\mathbb{C})\\)
    -   \\(hom\_{\mathbb{C}\_T} (A,B)\\) of the programs between \\(A\\) to \\(B\\) is the same as the hom set \\(hom\_{\mathbb{C}} (A, TB)\\).
    -   The identity of \\(A \in \mathbb{C}\_T\\) is \\(\eta\_A : A \to TA\\).
    -   \\(\forall f \in hom\_{\mathbb{C}\_T}(A,B), g \in hom\_{\mathbb{C}\_T}(B,C)\\) we have that \\(f \circ g^\star: A \to TC\\).


###### Monads in Haskell {#monads-in-haskell}

-   In Haskell,
    -   \\(T\\) corresponds to a [parameterized type](https://stackoverflow.com/questions/69827115/parameterized-types-in-haskell).
    -   \\(\eta\\) corresponds to [return](https://hackage.haskell.org/package/base-4.18.0.0/docs/Prelude.html#v:return) in Prelude.
        -   **\`return:** a &rarr; Ta\`
    -   \\(\\\_^\star\\) corresponds to [&gt;&gt;=](https://hackage.haskell.org/package/base-4.18.0.0/docs/Prelude.html#v:-62--62--61-).
        -   **~&gt;&gt;=:** (a &rarr; Tb) -&gt; (Ta &rarr; Tb)~

<!--listend-->

```haskell
class Monad where
  return :: a -> m a
  (>>=)  :: m a -> (a -> m b) -> m b
```

-   Monad of partiality, \\(TA = A + {\bot}\\) where \\(\bot\\) denotes _divergent computation_ is expressed in Haskell as the algebraic
    data type \`Maybe\`,
    ```haskell
    instance Monad Maybe where
      return a = Just a
      m >>= f = case m of
                  Just x  -> f x
                  Nothing -> Nothing

    divide :: Maybe Int -> Maybe Int -> Maybe Int
    divide a b = a >>= \m -> b >>= \n -> if n == 0 then Nothing else return (a `div` b)
    ```
-   Monad for side effects: A side effect is a form of computation where the computation changes state. It can be changing stuff inside variables or
    raising an exception. We can express such a notion by \\(TA = (A \times S)^S\\) where \\(S\\) is a set of states.

    -   \\(\eta\_A\\) maps \\(a \mapsto (\lambda (s:S). \llbracket a, s \rrbracket)\\)
    -   if \\(f : A \to TB\\) and \\(c \in TA\\) then \\(f^\star( c)= \lambda (s:S).(\text{let} \ \llbracket a, s' \rrbracket = c(s) \ \text{in} \ f(a)(s'))\\)

    <!--listend-->

    ```haskell
    instance Monad (State s) where
      return a = State (\s -> (s, a))
      State m >>= f = State (\s -> let (s', a) = m s
                                     State m' = f a
                                    in m' s')

    readState :: State s s
    readState = State (\s -> (s, s))

    writeState :: s -> State (s, ())
    writeState s = State (\s -> (s, ()))

    -- Example
    increment :: State Int ()
    increment = readState >>= \s -> writeState (s + 1)
    ```


## References {#references}

The above material comes from my notes made while reading, watching,

-   Tom Leinster, [Basic Category Theory](https://arxiv.org/abs/1612.09375)
-   Eugenia Cheng, [TheCatsters: Monads](https://www.youtube.com/playlist?list=PL0E91279846EC843E)
-   Bartosz Milewski, [Category Theory for Programmers](https://bartoszmilewski.com/category/category-theory/)
-   Emily Riehl, [Category Theory in Context](https://math.jhu.edu/~eriehl/context.pdf)
-   Eugenio Moggi, [Computational Lambda Calculus and Monads](https://www.cs.cmu.edu/~crary/819-f09/Moggi89.pdf)
-   Eugenio Moggi, Nick Benton and John Hughes [Monads and Effects](https://www.researchgate.net/publication/2806790_Monads_and_Effects)
