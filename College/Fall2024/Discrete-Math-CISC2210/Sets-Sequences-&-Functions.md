Topics covered:
- [Set Notation](set-notation) 
- [Reading Set Notation](reading-set-notation) 
- [General Sets and General Members of Sets](general-sets-and-general-memebers-of-sets) 
- [Advanced Set Notation](advanced-set-notation) 

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
element of." An $\epsilon$ with a strikethrough is usually the opposite, "is not an element of."

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
