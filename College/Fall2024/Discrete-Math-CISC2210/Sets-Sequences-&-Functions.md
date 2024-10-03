Sections covered:
- [1.3 Some Special Sets](#special-sets) 
- [1.4 Set Operations](#set-operations) 
- [1.5 Functions](#functions) 
- [1.6 Sequences](#sequences) 
- [1.7 Properties of Functions](#properties-of-functions)

# Some Special Sets

### Set Notation

| Symbol   |  Meaning  |
|--------------- | --------------- |
| $\mathbb{P}$  | Positive integers (exclusion of 0) |
| $\mathbb{N}$  | Natural integers (inclusion of 0) |
| $\mathbb{Z}$  | All integers (positive, negative, or zero) |
| $\mathbb{Q}$  | Quotient numbers (fractions) |
| $\mathbb{R}$  | All real numbers |
| $\empty$  | Empty set |

### Element-of $\in$

The element-of symbol is used to signify an object of a set. It can be read as "is an 
element of." An $\in$ with a strikethrough is usually the opposite, "is not an 
element of."

### General Sets and General Members of Sets

**Generic sets** are denoted by a capital letter, such as (*A, B, S
or X*).

The **generic members** of the set, the individual elements, are denoted via lowercase
letters (*a, b, s, or x*).

For example, s $\in$ S or t $\in$ T. 

### (Improper) Subset $\subseteq$ 

Consider $A \subseteq B$. This can simply be read as "A is a subset of B"
> Note: Subset-of may also be read as "is contained in".
> Also: This symbol is an IMPROPER subset, not a PROPER subset ($\subset$).

Now consider $S \subseteq T$: Since $s \in S$, this implies that $s \in T$.

### Power Set

The set of all subsets of a set of S is a power set and can be denoted as P(S).

The total size of a power set will generally be $2^n$ size.

![PowerSet](assets/PowerSet.png)

### Sigma $\Sigma$

Sigma sets can contain any combination of letters, numbers and symbols.

We could define the alphabet within $\sum$, such that

$\sum = {a, b, c, d, ... , z}$

### Sigma Star $\Sigma^*$

A "super set" of sigma, sigma star contains all combinations of a sigma set.

Since there's an infinite number of ways to combine letters and symbols, sigma star
is infinite in size.

##### Lambda $\lambda$
The first letter of sigma star, lambda simply represents an empty word.

### Restrictions of $\Sigma$

Sigma sets are not allowed to contain elements of strings which **begin with the 
same letter as an existing element**. 

We can allow $\sum = {a, b, c}$, however we cannot allow $\sum = {a, b, c, cd}$

<br>

## Set Operations

> $x$ may be any member of sets $A$ and $B$

### Union $\cup$

$A \cup B = (x : x \in A$ *OR* $x \in B)$

$A$ unites $B$ such that $x$ is an element of $A$ or $B$. 

All elements in A or B

### Intersect $\cap$

$A \cap B = (x : x \in A$ *AND* $x \in B)$

$A$ intersects with $B$ such that $x$ is an element of $A$ and $B$ simultaneously. 

All elements in A and B

##### Example 
![Unions and Intersection](assets/union-intersect.png)

> A and B are said to be **disjoint** should they have no elements in common
> $A \cap B = \empty$

### Relative Compliment $\backslash$
> Relative in the sense that we are only concerned in two particular sets.

$A \backslash B = (x : x \in A$ *but* $x \not\in B)$

$A$ and $B$ are relative compliments if $x$ is in $A$ but NOT in $B$.

> All elements in A that are not in B

### Symmetric Difference $\oplus$

$A \oplus B = (x : x \in A$ *or* $x \in B)$, *but not both!*

$x$ is an element of $A$ or $B$, but it cannot be an element of both.

All elements in A or B that are not in both.

##### Example 

![Symemetric Difference and Reletive Compliments](assets/compli-diff.png)

### Universe $U$

A Universe is a combination of all elements across all sets, denoted by U.

### Absolute Compliment $A^c$
> Otherwise known simply as the "compliment" of a set.

$A^c = (x \in U : U \backslash A)$

All the elements in universe that are not present in A.

### Venn Diagrams

It is can be useful to have a visual representation of how set operations relate one
set to another.

##### Example (a)

![Venn Diagram of Set Operations](assets/venndiagram.png)

##### Example (b)

![Venn Diagram of Compliments](assets/diagramcompliments.png)

### Rules of Set Operations

$$
A \cup B = B \cup A
$$

$$
A \cap B = B \cap A 
$$

$$
A \oplus B = B \oplus A
$$

$$
A \backslash B \neq B \backslash A
$$

These rules are the same rules as the assosciative and complimentary examples.

Furthermore:

$$
A^c \cap B^c = (A \cup B)^c
$$

Both expressions can be read as: All elements that are not in A and B.

### Product Sets and Ordered Pairs

$$
S * T = {(s, t) : s \in S, t \in T}
$$

### Finite Set (Length of Set) $|A|$

$$
|\empty| = 0
$$ 

$$
|{1, 2, ... , n}| = n : n \in P
$$

$$
|U| = (|A| \cup |A^c|) \cup (|B| \cup |B^c|) \cup ...
$$

<br>

# Functions

Functions in discrete math are **defined of set A** with **values in set B**.

Set A is considered the domain of the function and can be written as **Dom(f)** (and 
it often is).

For every x in Dom(f), f(x) is called the image of x under f. The set of all these 
images is a subset of B called the image of f, written as **Im(f)**

$$
Im(f) = { f(x) : x \in Dom(f) }
$$
> Im(f) is a set of f(x) such that x is an element of Dom(f) (or set A)

##### Example

![functionexample](assets/functionexample.png)

## Image $Im(f)$

For every x in $Dom(f)$, $f(x)$ is called the image of x under $f$. We can put these 
transformations together to make an **image set** $Im(f)$, **or the set of
all values taken by the function f(x)**.

$$
Im(f) = { f(x) : x \in Dom(f) }
$$
> Im(f) is a set of f(x) such that x is an element of Dom(f) (or set A)

### Map

Sometimes, functions are refered to as **maps**. This is because the behavior of a 
function $f$ **maps** S into T.

![mapping](assets/mapping.png)

## Codomain

Codomains are a **set of images which derive from S after a transformation of $f$**.
In other words, they are the output after a transformation of $S$

$$
f : S \rightarrow T
$$
> This is read as "$f$ is a function with domain S and codomain T".

### Graph $G$

A function with domain S and codomain T may be graphed, or a subset of G, such that;

for each $x \in S$ there is exactly one $y \in T$ such that
$(x, y) \in G$

## Characteristic Function $\chi_A$

Characteristic functions contain unique elements. When a condition is met, the input
will produce a particular output. 

A piecewise function is a good example of a characteristic function.

$$
\chi_A = \left\{\begin{array}{rcl} 1 & if & x \in A, \\
0 & if & x \in U \backslash A. 
\end{array} \right.
$$

For computers in particular, characteristic functions are particularly useful, as they 
can describe subsets of characteristic elements with bits 0 and 1.

## Composition Functions $g(f(x))$ 

Consider following functions $f$ and $g$: 

$$
f : S \rightarrow T
$$

$$
g : T \rightarrow U
$$

Composition of $f$ and $g$ would give us the following:

$$
(g \circ f) : S \rightarrow U
$$

$$
(g \circ f)(s) = g(f(s))
$$

#### Example

![Composition Function](assets/composition.png)

### Note: Assosciative Property of Functions

Functions are assosciative. This means that no matter which way you choose to
compute a composite function, you will always end with the same result.

$$
h \circ (g \circ f) = (h \circ g) \circ f
$$

# Sequences

Sequences are algebraic concepts such that a transformation, $f$, is invoked on 
$n$ amount of elements.

For example, $n!$ is a sequence of $\mathbb{N}$ such that $n! = n * n-1 * n-2 ... 3 * 2 * 1$ 

## Sum $\sum$

Another example of a sequence is summation.

![summation](assets/summation.png)

# Properties of Functions

Certain functions may have the following properties which make it unique in 
some way. Consider the following.

## One-to-One

Every element s hits a member of T exactly once.

Def: A function $f : S \rightarrow T$ is *one-to-one* if each element $s$
corresponds to any $t$ value **once at most**.

If $s1 \neq s2$, then $f(s1) \neq f(s2)$ 

Else if $f(s1) = f(s2)$, then $s1 = s2$ 

## Onto 

Every element s hits a member of T.

Def: A function $f : S \rightarrow T$ is *onto* $Im(f) = T$ for all $t \in T$
such that $f(s) = T$

## One-one Correspondance

Every member of set S corresponds to every member of set T.

Def: A function $f : S \rightarrow T$ is a *one-to-one correspondance*
if $f$ is one-one and onto.

## Inverse functions

Def: Let $f : S \rightarrow T$ be a function. A inverse function of $f$ is
the function $f^{-1}: T \rightarrow S$

For all $s \in S, f^{-1}(f(s)) = s$ 
