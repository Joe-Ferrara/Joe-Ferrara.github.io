---
layout: post
title:  "Intro II: L-series and Class Number Formula"
comment_issue_id: 2
sub: "lfunctions"
---

# $L$-series

The modern perspective on studying the Riemann zeta function is to study a class of functions that contains the Riemann zeta function and such that all functions in the class satisfy similar properties to the Riemann zeta function including having a Riemann hypothesis. The functions in this class are known as $L$-functions.

The simplest way to define an $L$-function is by an $L$-series,

$$L(\{a_n\}_{n = 1}^\infty, s) = \sum_{n = 1}^\infty \frac{a_n}{n^s},$$

where $s$ is a complex variable and the $a_n$ are a sequence of complex numbers. The Riemann zeta function is an $L$-series where the $a_n$ are all $1$. Usually $L$-series are made from sequences that have some sort of arithmetic meaning or importance. I will give two examples of simple $L$-series that are not much different from the Riemann zeta function in their definitions. In these two examples, the sequence $a_n$ comes from simple conditions using modular arithmetic.

For the first example define

$$a_n = \begin{cases} 1 &\text{ if } n\text{ is } 1 \text{ or } 5\text{ more than a multiple of } 8\\
					  -1 &\text{ if } n\text{ is } 3 \text{ or } 7\text{ more than a multiple of } 8\\
            0 &\text{otherwise.}\end{cases}$$

The conditions defining $a_n$ can be said more simply using modular arithmetic. In that language $a_n$ is $1$ if $n$ is $1$ or $5\bmod 8$ (which is the same as $1\bmod 4$), $a_n$ is $-1$ if $n$ is $3$ or $7\bmod 8$ (which is the same as $3\bmod 8$), and $a_n$ is $0$ otherwise. The $L$-series associated to this sequence is denoted $L(\chi_{-4}, s)$, and its first few terms are

$$L(\chi_{-4}, s) = 1 - \frac{1}{3^s} + \frac{1}{5^s} - \frac{1}{7^2} + \frac{1}{9^s} - \frac{1}{11^s} + \frac{1}{13^s} - \frac{1}{15^s} + \cdots.$$

Because $a_n$ is $0$ if $n$ is even and alternates between $1$ and $-1$ when $n$ is odd, the series converges when $s = 1$. It turns out that the number it converges to is $\frac{\pi}{4}$:

\begin{equation} L(\chi_{-4}, 1) = 1 - \frac{1}{3} + \frac{1}{5} - \frac{1}{7} + \frac{1}{9} - \frac{1}{11} + \frac{1}{13} - \frac{1}{15} + \cdots = \frac{\pi}{4}. \end{equation}

This equality is our first example of a special value formula for an $L$-function.

The next example is a slight alteration of the previous one. For this example, define the sequence $a_n$ as

$$a_n =  \begin{cases} 1 &\text{ if } n\text{ is } 1 \text{ or } 7\text{ more than a multiple of } 8\\
					  -1 &\text{ if } n\text{ is } 3 \text{ or } 5\text{ more than a multiple of } 8\\
            0 &\text{otherwise.}\end{cases}$$

In this example, the $L$-function is denoted $L(\chi_8, s)$ and its first few terms are

$$L(\chi_8, s) = 1 - \frac{1}{3^s} - \frac{1}{5^s} + \frac{1}{7^s} + \frac{1}{9^s} - \frac{1}{11^s} - \frac{1}{13^s} + \frac{1}{15^s} + \frac{1}{17^s} - \cdots.$$

For $L(\chi_8, s)$, $a_n$ is $0$ if $n$ is even just like for $L(\chi_{-4},s)$. For odd $n$, starting with $a_3$, the pattern for $a_n$ is $-1,-1,1,1,-1,-1,1,1\cdots$. This is a slight change from $L(\chi_{-4}, s)$. There is also a special value formula for $L(\chi_8, s)$ at $s=1$, and this time the formula is

\begin{equation}L(\chi_8, 1) = 1 - \frac{1}{3} - \frac{1}{5} + \frac{1}{7} + \frac{1}{9} - \frac{1}{11} - \frac{1}{13} + \frac{1}{15} + \cdots = \frac{\log(1 + \sqrt{2})}{\sqrt{2}}.\end{equation}

By just slightly changing the $a_n$, we obtained two surprisingly different values, $\frac{\pi}{4}$ and $\frac{\log(1 + \sqrt{2})}{\sqrt{2}}$. In my next post I will explain where the two numbers $\frac{\pi}{4}$ and $\frac{\log(1 + \sqrt{2})}{\sqrt{2}}$ come from, and the arithmetic significance of the identities (1) and (2).

It is easy to write code to verify (1) and (2). I have posted a script, ``lseries_exs.py``, at the github repository [here](https://github.com/Joe-Ferrara/IntroToLfunctions), that shows the convergence of (1) and (2) when you sum different numbers of terms from the defining series for $L(\chi_{-4}, 1)$ and $L(\chi_{8}, 1)$. For instance, the first 5 decimals of the sum of the first 100,000 terms of $L(\chi_{-4}, 1)$ agrees with the first 5 decimals of $\frac{\pi}{4}$, and the first 9 decimals of the sum of the first 100,000 terms of $L(\chi_8,1)$ agrees with the first 9 decimals of $\frac{\log(1 + \sqrt{2})}{\sqrt{2}}$.


# Class Number Formula

Dirichlet's class number formula is one of the first general special value formula for an $L$-function. The identities (1) and (2) above are related to this class number formula, and the relation will be explored in the my next post. Unfortunately in order to state the class number formula, the math gets much more technical than it has been so far. If you do not have a large math background (in specifically abstract algebra and linear algebra), just try to get the big picture ideas. In my next post, I hope to make many of the abstract notions much more explicit.

Dirichlet's class number formula addresses the question of unique factorization in other number systems, which was brought up in my previous post. The formula relates whether or not a number system has unique factorization to the special value of an $L$-function. To define a new number system, let $K/\mathbb Q$ be a finite field extension of the rational numbers $\mathbb Q$. This means that $K$ is a set of numbers where we can add, subtract, multiply, and divide, and such that $\mathbb Q$ as a subset of $K$ makes $K$ a finite dimensional vector space over $\mathbb Q$.

More generally than addressing the question of unique factorization in $K$, Dirichlet's class number formula relates the special value of an $L$-function associated to $K$ to multiple invariants of the field $K$, which we now introduce.

Let

$$\mathscr O_K = \{\alpha \in K: \text{there exists monic }f(x)\in\mathbb Z[x] \text{ with } f(\alpha) = 0\},$$

so $\mathscr O_K$ is the set of all elements of $K$ that are the solution to a monic polynomial with integer coefficients. It is a fact that $\mathscr O_K$ is a ring, which means that one may add, subtract, and multiply in $\mathscr O_K$ just like in the integers $\mathbb Z$. We call $\mathscr O_K$ the ring of integers of $K$ because $\mathscr O_K$ is very similar to the integers $\mathbb Z$. These $\mathscr O_K$'s are the number systems studied in algebraic number theory.

One can extend the notion of prime numbers in $\mathbb Z$ to prime numbers in $\mathscr O_K$ in order to make sense of the question of whether or not $\mathscr O_K$ has unique factorization. One major difference between $\mathscr O_K$ and $\mathbb Z$ is that $\mathscr O_K$ does not in general have unique factorization into prime numbers like $\mathbb Z$ does. To measure how much $\mathscr O_K$ does not have unique factorization we define what is called the class group of $\mathscr O_K$. The class group is defined as

$$\text{Cl}(K) = \{\text{group generated by ideals of } \mathscr O_K\}/\{\text{group generated by principal ideals of } \mathscr O_K\},$$

and is a finite abelian group. Let $h_K$ be the size of the group $\text{Cl}(K)$. If you do not know what an ideal is, then think of $h_K$ as a number that measures how much the number system $\mathscr O_K$ does not have a fundamental theorem of arithmetic. The larger $h_k$ is, the further $\mathscr O_K$ is from from having a fundamental theorem of arithmetic.

Two other important invariants of $\mathscr O_K$ are the roots of unity of $\mathscr O_K$:

$$\mu(\mathscr O_K) = \{\alpha\in\mathscr O_K: \alpha^n = 1\text{ for some }n\in\mathbb N\},$$

and the units of $\mathscr O_K$:

$$\mathscr O_K^\times = \{ \alpha\in\mathscr O_K: \exists\beta\in\mathscr O_K, \alpha\beta = 1\}.$$

It turns out that there are only finitely many roots of unity in $\mathscr O_K$. Since $x^n - 1$ is a monic polynomial with integer coefficients, all the roots of unity in $K$ are in $\mathscr O_K$. Let $\mu_K$ be the number of roots of unity in $\mathscr O_K$ (which is also the number of roots of unity in $K$). The set $\mathscr O_K^\times$ is in general infinite (though there are some $K$ for which it is finite, namely the rational numbers and imaginary quadratic fields).

Dirichlet's unit theorem is a theorem that describes the "size" of $\mathscr O_K^\times/\mu(\mathscr O_K)$. In order to state it, let $r_1$ be the number of embeddings of $K$ into $\mathbb R$ and let $r_2$ be half of the number of embeddings of $K$ into $\mathbb C$ that do not land in $\mathbb R$. Dirichlet's unit theorem says that $\mathscr O_K^\times/\mu(\mathscr O_K)$ is a free abelian group of rank $r_1 + r_2 - 1$. This is like saying $\mathscr O_K^\times/\mu(\mathscr O_K)$ is a vector space of $\mathbb Z$ of dimension $r_1 + r_2 - 1$. Since $\mathbb Z$ is not a field we say free of finite rank instead of dimension.

We now define an invariant of $K$ that precisely measures the co-volume of $\mathscr O_K^\times$ in $K^\times$. Let $r = r_1 + r_2 - 1$, and let $u_1,\ldots, u_r$ be a $\mathbb Z$-basis for $\mathscr O_K^\times/\mu(\mathscr O_K)$. Let $\sigma_0,\ldots,\sigma_{r_1 - 1}$ be the $r_1$ embeddings of $K$ into $\mathbb R$. The embeddings of $K$ into $\mathbb C$ that do not land in $\mathbb R$ come in complex conjugate pairs. Let $\sigma_{r_1},\ldots, \sigma_r$ be one of each of the complex conjugate pairs. The invariant that measures the co-volume of $\mathscr O_K^\times$ in $K$ is called the regulator of $K$, denoted $\text{Reg}_K$, and defined as the absolute value of the determinant of an $r\times r$ matrix which we now define. For $1\leq i\leq r_1 - 1$, $1\leq j\leq r$ let

$$r_{i,j} = \log|\sigma_i(u_j)|$$

and for $r_1\leq i\leq r$, $1\leq j\leq r$ let

$$r_{i,j} = \log|\sigma_i(u_j)|^2.$$

Then

$$\text{Reg}_K := |\det(r_{i,j})_{1\leq i,j\leq r}|.$$

These are the invariants we need, and we know introduce the $L$-function. For $s\in\mathbb C$ with real part greater than $1$, define the Dedekind zeta function associated to $K$ as

$$\zeta_K(s) = \sum_{\mathfrak a\subset\mathscr O_K}\frac{1}{\text{N}\mathfrak a^s} = \prod_{\mathfrak p\subset\mathscr O_K}\left(1 - \frac{1}{\text{N}\mathfrak p^s}\right)^{-1},$$

where the sum is over all nonzero ideals of $\mathscr O_K$, the product is over all nonzero prime ideals of $\mathscr O_K$, and for an ideal $\mathfrak a\subset\mathscr O_K$, $\text{N}\mathfrak a$ is the size of $\mathscr O_K/\mathfrak a$, which is finite. Just like the Riemann zeta function, the series or product expansion above converges for $s\in\mathbb C$ with real part of $s$ greater than $1$. Further, $\zeta_K(s)$ also has a meromorphic continuation to all of $\mathbb C$ with a pole at $s = 1$, and satisfies a functional equation relating the values $\zeta_K(s)$ and $\zeta_K(1 - s)$. The Dedekind zeta function can be realized as an $L$-series by taking $a_n$ to be the number of ideals $\mathfrak a$ in $\mathscr O_K$ such that $\mathscr O_K/\mathfrak a$ has size $n$.

 Dirichlet's class number formula is about the value of $\zeta_K(s)$ at $s = 0$, or equivalently via the functional equation, about the residue of the pole of $\zeta_K(s)$ at $s = 1$. First I will explain the formula at $s = 0$. At $s = 1$, I will need to introduce one more invariant, so I will explain that formula second.

At $s = 0$, it turns out that $\zeta_K(s)$ is $0$, and the first $r-1$ (where $r = r_1 + r_2 - 1$) derivatives of $\zeta_K(s)$ are also $0$. Let $\zeta_K^{(i)}(s)$ denote the $i$th derivative of $\zeta_K(s)$. Then Dirichlet's class number formula says

$$\frac{\zeta_K^{(r)}(0)}{r!} = -\frac{h_K\text{Reg}_K}{\mu_K}.$$

Another way to say this is that the leading term of the Taylor series expansion of $\zeta_K(s)$ at $s = 0$ is $-\frac{h_K\text{Reg}_K}{\mu_K}$, and $\zeta_K(s)$ vanishes at $s = 0$ with order $r$.
This is a remarkable formula because it relates the value of the analytic function $\zeta_K(s)$ defined by an infinite product over all the primes of $\mathscr O_K$ to the global invariants $r, h_K, \text{Reg}_K$, and $\mu_K$ of the ring $\mathscr O_K$.

To state Dirichlet's class number formula at $s = 1$, we need to introduce one more invariant of $\mathscr O_K$. This last invariant measures the covolume of $\mathscr O_K$ in $K$. Let $d$ be the dimension of $K$ as a $\mathbb Q$-vector space. It turns out that $d = r_1 + 2r_2$ and that $\mathscr O_K$ is a free $\mathbb Z$-module of rank $d$. To measure the covolume of $\mathscr O_K$ in $K$ we do something similar to what we did when measuring the covolume of $\mathscr O_K^\times$ in $K^\times$ but we omit the logarithm. Let $\beta_1,\ldots,\beta_d$ be a basis for $\mathscr O_K$ over $\mathbb  Z$, and let $\sigma_1,\ldots,\sigma_d$ be all the embeddings of $K$ into $\mathbb C$. We define the discriminant of $\mathscr O_K$, denoted $D_K$, to be the square of the $d\times d$ matrix with $i,j$ entry $\sigma_i(\beta_j)$:

$$D_K = \det((\sigma_i(\beta_j))_{1\leq i,j \leq d})^2.$$

Then Dirichlet's class number formula at $s = 1$ says that $\zeta_K(s)$ has a pole of order $1$ at $s = 1$ with residue

$$\frac{2^{r_1}(2\pi)^{r_2}h_K\text{Reg}_K}{\sqrt{|D_K|}\mu_K}.$$

The square root of the absolute value of the discriminant of $K$ measures the covolume of $\mathscr O_K$ in $K$. The terms $2^{r_1}$ and $(2\pi)^{r_2}$ have to do with the embeddings of $K$ into $\mathbb R$ and the embeddings of $K$ into $\mathbb C$ that do not land in $\mathbb R$. An equivalent way to state Dirichlet's class number formula at $s = 1$ is the following:

$$\lim_{s\to 1}(s-1)\zeta_K(s) = \frac{2^{r_1}(2\pi)^{r_2}h_K\text{Reg}_K}{\sqrt{|D_K|}\mu_K}.$$
