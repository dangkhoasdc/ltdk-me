---
layout: "post.njk"
title: "The repertoire method"
date: 2017-12-26
tags:
    - math
---
The repertoire method is a method of finding closed-form solutions to recurrence relations
and sums of a series. The method is introduced in Chapter 1 of ConMath but
most readers at first seem to struggle with it. Throughout the book,
especially Chapters 1 and 2, the repertoire method demonstrates its ability to
solve many sums and recurrences. However, I honestly admit that it is quite
difficult to apply and fully understand how it works. In this note, I try to
figure the way to effectively apply the method for solving recurrences.

# Definition

In essence, the main goal of the method is to find coefficients for a **linear
combination** of a set of recurrences. This method works very well on linear
recurrences, in the sense that the solutions can be expressed as a sum of
coefficients multiplied by functions of $n$. Therefore,
if we have to find a closed-form of a linear recurrence, this is worth trying.

The method is not described clearly in ConMath because the authors always come
up with a set of recurrences and get their coefficients but they do not
mention how they figure it out. Regarding this aspect, Sedgewick's book provides
accessible clarification and systematic examples. Therefore, I use the procedure
in Sedgewick's book as a recipe for the repertoire method:

1. Relax the recurrence by adding an extra function term.
2. Substitute known functions into the recurrence to derive identities similar to the recurrence.
3. Take linear combinations of such identities to derive an equation identical to the recurrence.

At first glance, it is quite abstract. However, some examples carried out
in the book illustrate how we manipulate the steps. Suppose that we have
recurrence $a_{n} = a_{n-1} + {\text{stuff}}$. First we generalize the
identity by replacing ${\text{stuff}}$ with $f(n)$, i.e., $a_{n} = a_{n-1} + f(n)$.
We easily obtain $f(n) =  a_{n} - a_{n-1}$. The next step is to build a table
of ingredients from which we can construct $f(n)$. Finally, we determine coefficients
of each component so that they satisfy $f(n)$ and the basis of the
recurrence.

For more details and explanations, I strongly recommend reading
[Markus Scheuer's answer](https://math.stackexchange.com/a/1023510/397515). Of
course, ConMath (Chapter 1, 2, 6) is a good material for practicing the method
for understanding purposes. Section 2.5 from Sedgewick's book summarizes
some approaches to finding the closed-form, including the repertoire method.
Examples in the book are recommended reading.

The best way to fully understand the method is to work through examples.

# Examples

## Closed-form of sums

We can easily convert the sum of a sequence into a linear recurrence. Let's begin
with the first example, which only contains the term $n^3$.

$ S_{n} = \sum_{k=0}^n k^3$

This sum can be seen as:

$ a_{0} = 0$
$ a_{n} = a_{n-1} + n^3$

Next,  we build a table of $a_{n}$ and $a_n - a_{n-1}$.

| $a_n$ | $a_n -a_{n-1}$   |
|-------|------------------|
| 1     | 0                |
| n     | 1                |
| $n^2$ | $2n-1$           |
| $n^3$ | $3n^2-3n+1$      |
| $n^4$ | $4n^3-6n^2+4n-1$ |

How can I fill $a_n$? Since we want $f(n)$ to obtain $n^3$
and we observe that $f(n) = a_n - a_{n-1}$ depends on the degree of $n$ in
$a_n$ and hence we come up with some simple sequences, i.e., computing $a_n - a_{n-1}$.
Turns out $f(n)$ has a smaller degree of $n$ than $a_n$ by exactly 1. $f(n)$ obtaining $n^3$
means that $a_n$ has to obtain $n^4$. The simplest form we can come up with
is $n^3 = \alpha (4n^3-6n^2+4n-1)$. So $\alpha = {1\over 4}$, we need to eliminate $n^2$,
$n$, and constants. In the second attempt, we add $n^3$ and $n^2$ into the
linear combination:

$$
\alpha (4n^3-6n^2+4n-1) + \beta(3n^2-3n+1) + \lambda (2n-1) = n^3
$$

$$
\begin{cases}
-6\alpha + 3\beta = 0\newline
4\alpha -3\beta + 2\lambda = 0\newline
-\alpha + \beta - \lambda = 0
\end{cases}
$$

The solution is $(\alpha, \beta, \lambda) =({1\over 4}, {1\over 2}, {1\over 4}) $
and hence $a_n = \alpha n^3 + \beta n^2 + \lambda n = {1\over 4}n^2(n+1)^2$.
Also, since $a_0 = 0$, it is the final solution.

Let's try another example, this time we use an exercise in ConMath:

$$ S_{n} = \sum_{k=0}^{k} (-1)^kk^2$$

|$a_n$      | $a_n-a_{n-1}$     |
|-----------|-------------------|
|$(-1)^nn^2$|$(-1)^n(2n^2-2n+1)$|
|$(-1)^n$  |$2(-1)^n$          |
|$(-1)^nn$ |$(-1)^n(2n-1)$     |

The solution is $S_n = {1\over 2}(-1)^n n(n+1)$ since we just add the first term
and the last term together and then divide by 2, we get $f(n)$. When I first saw
the sum, I could not think of any sequences which help me find $f(n)$. After
playing with some sequences, I realized that assigning $a_n = f(n) = (-1)^nn^2$
actually lets other patterns be discovered.

## Linear Recurrences

$$ a_0 = 7 $$

$$ a_n = a_{n-1} + 2n^2 + 7 \; n > 0 $$

Based on the table we built in previous examples, we can construct a linear
combination for the recurrence:

$$ \alpha(3n^2-3n+1) + \beta(2n-1) + \lambda 1 = 2n^2+7 $$

$$
\begin{cases}
3\alpha = 2 \newline
-3\alpha + 2\beta = 0 \newline
\alpha - \beta + \lambda = 7
\end{cases}
$$

The solution is $(\alpha, \beta, \lambda) = ({2\over 3}, 1, {22\over 3})$. However,
at this time $a_0= 0 \neq 7$, we have to add the constant $7$ to the final form.
The closed-form is $a_n = {2\over 3}n^3+n^2+{22\over 3}n+7$.

## Exercise 1.16 (ConMath)

$$
g(1) = \alpha
$$
$$
g(2n+j) = 3g(n) + \gamma n + \beta \; j = 0, 1 ; n \geq 1
$$

# Related Materials

After hours searching on the Internet, I found some useful links which actually
help me understand the method:

- [Wakatta's post](http://blog.wakatta.jp/blog/2012/01/14/concrete-mathematics-repertoire-method/)
- [Math stackexchange answer](https://math.stackexchange.com/a/1023510/397515):
this one is damn good.
- [Pindancing's post](http://pindancing.blogspot.sg/2011/02/repertoire-method-in-concrete.html)
- Sedgewick, Robert, and Philippe Flajolet. An introduction to the analysis of algorithms. Pearson Education India, 1996. [IMO,
the explanation in this book is much better than in ConMath.]
- Graham, Ronald L., et al. "Concrete mathematics: a foundation for computer science."
Computers in Physics 3.5 (1989): 106-107.
