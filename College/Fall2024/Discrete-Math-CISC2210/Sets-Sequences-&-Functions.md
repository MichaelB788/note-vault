Sections covered:
- [1.3 Some Special Sets](#special-sets) 
- [1.4 Set Operations](#set-operations) 
- [1.5 Functions](#functions) 
- [1.6 Functions](#sequences) 

# Some Special Sets

## Set Notation

| Symbol   |  Meaning  |
|--------------- | --------------- |
| $\mathbb{P}$  | Positive integers (zero exclusive) |
| $\mathbb{N}$  | Natural numbers (zero inclusive) |
| $\mathbb{Z}$  | Real numbers (positive, negative, or zero) |
| $\mathbb{Q}$  | Quotient numbers (fractions) |
| $\mathbb{R}$  | All numbers |
| $\empty$  | Empty set |


## Reading Set Notation

### Element-of $\epsilon$

The element-of symbol is used to signify an object of a set. It can be read as "is an 
element of." An $\epsilon$ with a strikethrough is usually the opposite, "is not an 
element of."

### General Sets and General Members of Sets

**Generic sets** are denoted by a capital letter, such as (*A, B, S
or X*).

The **generic members** of the set, the individual elements, are denoted via lowercase
letters (*a, b, s, or x*).

For example, s $\epsilon$ S or t $\epsilon$ T. 

### (Improper) Subset $\subseteq$ 

Consider $A \subseteq B$. This can simply be read as "A is a subset of B"
> Note: Subset-of may also be read as "is contained in".
> Also: This symbol is an IMPROPER subset, not a PROPER subset ($\subset$).

Now consider $S \subseteq T$: Since $s \epsilon S$, this implies that $s \epsilon T$.

### Power Set

The set of all subsets of a set of S is a power set and can be denoted as P(S).

The total size of a power set will generally be $2^n$ size.

![PowerSet](assets/PowerSet.png)

### Sigma $\sum$

Sigma sets can contain any combination of letters, numbers and symbols.

We could define the alphabet within $\sum$, such that

$\sum = {a, b, c, d, ... , z}$

### Sigma Star $\sum*$

A "super set" of sigma, sigma star contains all combinations of a sigma set.

Since there's an infinite number of ways to combine letters and symbols, sigma star
is infinite in size.

##### Lambda $\lambda$
The first letter of sigma star, lambda simply represents an empty word.

### Restrictions of Sigma

Sigma sets are not allowed to contain elements of strings which **begin with the 
same letter as an existing element**. 

We can allow $\sum = {a, b, c}$, however we cannot allow $\sum = {a, b, c, cd}$

<br>

## Set Operations

> $x$ may be any member of sets $A$ and $B$

### Union $\cup$

$A \cup B = (x : x \epsilon A$ *OR* $x \epsilon B)$

$A$ unites $B$ such that $x$ is an element of $A$ or $B$. 

Unite all the elements in both sets.

### Intersect $\cap$

$A \cap B = (x : x \epsilon A$ *AND* $x \epsilon B)$

$A$ intersects with $B$ such that $x$ is an element of $A$ and $B$ simultaneously. 

Combine all elements that are exclusively in both A and B.

##### Example 
![Unions and Intersection](assets/union-intersect.png)

> A and B are said to be **disjoint** should they have no elements in common
> $A \cap B = \empty$

### Relative Compliment $\backslash$
> Relative in the sense that we are only concerned in two particular sets.

$A \backslash B = (x : x \epsilon A$ *and* $x !\epsilon B)$

If $x$ is in $A$, but $x$ is NOT in $B$, $A$ and $B$ are relative compliments.

Take all the elements that are in A and not in B.

### Symmetric Difference $\oplus$

$A \oplus B = (x : x \epsilon A$ *or* $x \epsilon B)$, *but not both!*

$x$ is an element of $A$ or $B$, but it cannot be an element of both.

Combine all the elements in A and B but leave out the elements that appear in both!

##### Example 

![Symemetric Difference and Reletive Compliments](assets/compli-diff.png)

### Universe $U$

A Universe is a combination of all elements across all sets, denoted by U.

### Absolute Compliment $A^c$
> Otherwise known simply as the "compliment" of a set.

$A^c = (x \epsilon U : U \backslash A)$

All the elements in universe that are not present in A.

### Venn Diagrams

It is can be useful to have a visual representation of how set operations relate one
set to another.

##### Example (a)

![Venn Diagram of Set Operations](assets/venndiagram.png)

##### Example (b)

![Venn Diagram of Compliments](assets/diagramcompliments.png)

### Rules off Set Operations

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

> Rules 1 to 3 are complimentary examples

Further:

$$
A \cup (B \cup C) = A \cup (B \cup C)
$$

$$
A \cap (B \cap C) = A \cap B 
$$

$$
A \oplus B = B \oplus A
$$

$$
A \backslash B \neq B \backslash A
$$
