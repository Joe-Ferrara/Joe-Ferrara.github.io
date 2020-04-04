---
layout: post
title: "Introduction to L-functions III: Quadratic Fields"
comment_issue_id: 3
---

In this post, I will connect the two sections of my previous post, and show how to produce many more special value formulas like the ones for $L(\chi_{-4}, 1)$ and $L(\chi_8, 1)$. Recall that these two special value formulas are

\begin{equation} L(\chi_{-4}, 1) = 1 - \frac{1}{3} + \frac{1}{5} - \frac{1}{7} + \frac{1}{9} - \frac{1}{11} + \frac{1}{13} - \frac{1}{15} + \cdots = \frac{\pi}{4} \end{equation}

and

\begin{equation}L(\chi_8, 1) = 1 - \frac{1}{3} - \frac{1}{5} + \frac{1}{7} + \frac{1}{9} - \frac{1}{11} - \frac{1}{13} + \frac{1}{15} + \cdots = \frac{\log(1 + \sqrt{2})}{\sqrt{2}}.\end{equation}

I will also explain where the sequences defining $L(\chi_{-4}, s)$ and $L(\chi_8, s)$ come from as well as where the numbers $\frac{\pi}{4}$ and $\frac{\log(1 + \sqrt{2})}{\sqrt{2}}$ come from. To do this, the most simple number systems that are not the integers will be introduced and used.

# Quadratic Fields

Quadratic fields are the first fields after the rational numbers to study. As a $\mathbb Q$-vector space, they have dimension $2$, and are obtained by adjoining the square root of an integer to $\mathbb Q$.

Let $d$ be a square free integer. (This means that no squares in $\mathbb Z$ divide $d$.) The quadratic field associated to $d$ is

$$\mathbb Q(\sqrt{d}) = \{ \alpha + \beta\sqrt{d} : \alpha, \beta \in \mathbb{Q}\}.$$

Let $K = \mathbb Q(\sqrt{d})$. In $K$ one can add, subtract, multiply and divide:

$$(\alpha + \beta\sqrt{d}) \pm (\gamma + \delta\sqrt{d}) = \alpha + \gamma \pm (\beta + \delta)\sqrt{d}$$

$$ (\alpha + \beta\sqrt{d})(\gamma + \delta\sqrt{d}) = \alpha\gamma + \beta\delta d + (\alpha\delta + \beta\gamma)\sqrt{d}$$

$$\frac{\alpha + \beta \sqrt{d}}{\gamma + \delta\sqrt{d}} = \frac{\alpha\gamma - \delta\beta d}{\gamma^2 - d\delta^2} + \frac{\beta\gamma - \alpha\delta}{\gamma^2 - d\delta^2}\sqrt{d},$$

where to divide, we rationalized $\frac{\alpha + \beta\sqrt{d}}{\gamma + \delta\sqrt{d}}$ by multiplying by $\frac{\gamma - \delta\sqrt{d}}{\gamma - \delta\sqrt{d}}$.

The ring of integers of $K$ comes in two different types depending on what $d$ is modulo $4$. If $d\equiv 2$ or $3\bmod 4$, then

$$\mathscr O_K = \{\alpha + \beta\sqrt{d} : \alpha, \beta \in \mathbb Z\},$$

and if $d\equiv 1\bmod 4$, then

$$\mathscr O_K = \left\{\alpha + \beta\frac{1 + \sqrt{d}}{2} : \alpha, \beta \in \mathbb Z\right\}.$$

If one were to apriori guess the ring of integers of $\mathscr O_K$, the natural candidate is the representation written for when $d\equiv 2$ or $3\bmod 4$. To see that $\frac{1 + \sqrt{d}}{2}$ is an algebraic integer when $d\equiv 1\bmod 4$, consider the polynomial

$$\left(x - \frac{1 + \sqrt{d}}{2}\right)\left(x - \frac{1 - \sqrt{d}}{2}\right) = x^2 - x + \frac{1-d}{4},$$

which is a monic polynomial that has integer coefficients if and only if $d\equiv 1\bmod 4$ since $\frac{1-d}{4}\in \mathbb Z$ if and only if $d\equiv 1\bmod 4$. It turns out that you cannot get more than this denominator of $2$ showing up in the ring of integers of these quadratic fields.

The first invariant of $\mathscr O_K$ I'll discuss is the discriminant of $\mathscr O_K$. Recall that the discriminant measures the covolume of $\mathscr O_K$ in $K$, and since the definition of $\mathscr O_K$ differs whether or not $d$ is congruent to $1\bmod 4$, the discriminant will differ as well. In general we have the inclusion of sets

$$\{\alpha + \beta\sqrt{d} : \alpha,\beta\in\mathbb Z\}\subset\left\{\alpha + \beta \frac{1 + \sqrt{d}}{2} : \alpha,\beta\in\mathbb Z\right\}$$

since $\sqrt{d} = -1 + 2\frac{1 + \sqrt{d}}{2}$. This inclusion shows that when $d\equiv 1\bmod 4$, the size of $\mathscr O_K$ relative to $K$ is larger than when $d\equiv 2$ and $3=\bmod 4$, so the covolume will be smaller.

To precisely calculate the discriminant, I need to say something about embeddings of $K$ into $\mathbb C$. An embedding of $K$ into $\mathbb C$ is a function from $K$ to $\mathbb C$ that preserves the arithmetic operations of $K$. Let $\varphi :K\rightarrow \mathbb C$ be an embedding of $K$ into $\mathbb C$. Then it turns out that $\varphi$ must be the identity on $\mathbb Q$, and $\varphi$ is determined by where it sends $\sqrt{d}$. The two possibilities for $\varphi(\sqrt{d})$ are $\sqrt{d}$ and $-\sqrt{d}$. I'm abusing notation a bit here by apriori not thinking of $K$ as a subset of $\mathbb C$ and saying that the two ways to make $K$ a subset of $\mathbb C$ such that the arithmetic operations in $K$ agree with those in $\mathbb C$ are to send $\sqrt{d}\in K$ (thought of abstractly as an element of $K$) to either $\sqrt{d}\in \mathbb C$ or $-\sqrt{d}\in \mathbb C$ (now thought of as concrete complex numbers).

Before calculating the discriminant of $\mathscr O_K$, I want to mention an important dichotomy that happens with quadratic fields. When $d >0$, $\sqrt{d}$ and $-\sqrt{d}$ are real numbers, so both of the embeddings of $K$ into $\mathbb C$ land in $\mathbb R$. In this case $K$ is called a *real quadratic field* and the invariants $r_1$ and $r_2$ are $r_1 = 2, r_2 = 0$. When $d < 0$, $\sqrt{d}$ and $-\sqrt{d}$ are purely imaginary complex numbers, so both the embeddings of $K$ into $\mathbb C$ do not land in $\mathbb R$. Further, $-\sqrt{d}$ is the complex conjugate of $\sqrt{d}$. In this case $K$ is called an *imaginary quadratic field* and the invariants $r_1$ and $r_2$ are $r_1 = 0, r_2 = 1$.

Now to calculate the discriminant of $\mathscr O_K$. If $d\equiv 2$ or $3\bmod 4$, then $1$, $\sqrt{d}$ is a basis for $\mathscr O_K$ over $\mathbb Z$ and the embeddings of $K$ into $\mathbb C$ either send $1$ to $1$ and $\sqrt{d}$ to $\sqrt{d}$ or send $1$ to $1$ and $\sqrt{d}$ to $-\sqrt{d}$. Then the discriminant of $\mathscr O_K$ is

$$D_K = \det\begin{pmatrix} 1 & 1\\ \sqrt{d} &-\sqrt{d}\end{pmatrix}^2 = 4d.$$

If $d\equiv 1\bmod 4$, then $1$, $\frac{1 + \sqrt{d}}{2}$ is a basis for $\mathscr O_K$ over $\mathbb Z$ and the embeddings of $K$ into $\mathbb C$ either send $1$ to $1$ and $\frac{1 + \sqrt{d}}{2}$ to $\frac{1 + \sqrt{d}}{2}$ or send $1$ to $1$ and $\frac{1 + \sqrt{d}}{2}$ to $\frac{1 - \sqrt{d}}{2}$. Then the discriminant is

$$D_K = \det\begin{pmatrix} 1 & 1\\ \frac{1 + \sqrt{d}}{2} & \frac{1 - \sqrt{d}}{2}\end{pmatrix}^2 = d.$$

The covolume of $\mathscr O_K$ in $K$ is the square root of the absolute value of the discriminant, and these calculations match the observation that the covolume of $\mathscr O_K$ in $K$ should be smaller when $d\equiv 1\bmod 4$.

# Associated $L$-series

Before I discuss the other terms in the class number formula for $K$, I will associate an $L$-series to $K$. Let $D = D_K$ be the discriminant of $K$. I will define a function

$$\chi_D:\mathbb N\longrightarrow \{-1, 0, 1\}$$

which determines the sequence $a_n = \chi_D(n)$. Then the $L$-series associated to $K$ is defined as

$$L(\chi_D, s) = \sum_{n = 1}^\infty\frac{\chi_D(n)}{n^s}.$$

This is where the functions $L(\chi_{-4}, s)$ and $L(\chi_8, s)$ from the previous post come from.

Let $n\in\mathbb N$. If $\gcd(n, D) > 1$, define $\chi_D(n) = 0$. If $p$ is a prime, and $p\nmid 2d$, define

$$\chi_D(p) = \begin{cases} -1 & \text{ if } d \text{ is not a square} \bmod p\\ 1 & \text{ if } d \text{ is a square} \bmod p.\end{cases}$$

If $d\equiv 1\bmod 4$, define $\chi_D(2)$ as

$$\chi_D(2) = \begin{cases} 1 &\text{ if } d\equiv 1\bmod 8\\ -1 &\text{ if } d\equiv 5\bmod 8.\end{cases}$$

$\chi_D$ is now defined on all prime numbers, and we extend $\chi_D$ to all of $\mathbb N$ multiplicatively. That is, if $n$ has prime factorization $n = p_1^{a_1}p_2^{a_2}\cdots p_m^{a_m}$, then define

$$\chi_D(n) = \prod_{i = 1}^m\chi_D(p_i)^{a_i}.$$

The function $\chi_D$ is known as the Kronecker symbol and it is a generalization of the Legendre symbol. It is related to the arithmetic of $\mathscr O_K$ in the following way. If $p$ is a prime number that does not divide $D$, then $\chi_D(p) = -1$ if the ideal $p\mathscr O_K$ is a prime ideal of $\mathscr O_K$, and $\chi_D(p) = 1$ if the ideal $p\mathscr O_K$ is the product of two distinct prime ideals of $\mathscr O_K$.

You may wonder why the subscript on $\chi_D$ is $D$ and not $d$. Using some language from abstract algebra I can explain one reason for this. Using $\chi_D$, we can define a function

$$\widetilde{\chi}_D:(\mathbb Z/|D|\mathbb Z)^\times \longrightarrow \{\pm 1\}$$

$$\widetilde{\chi}_D(a + |D|\mathbb Z) = \chi_D(a),$$

which is a well defined group homomorphism ($\left\lvert D\right\rvert$ is the absolute value of $D$). The number $\left\lvert D\right\rvert$ has the following property: among all positive integers $N$, such that the function

$$\widetilde{\chi}:(\mathbb Z/N\mathbb Z)^\times\longrightarrow \{\pm 1\}$$

$$\widetilde{\chi}(a + N\mathbb Z) = \chi_D(a)$$

is a well-defined group homomorphism, $\left\lvert D\right\rvert$ is the smallest one. This is one reason why $\chi_D$ is written with the subscript $D$ and not $d$.

# Relation to Class Number Formula

Since $\chi_D$ is defined to be multiplicative (means that for all $a,b$, $\chi_D(ab) = \chi_D(a)\chi_D(b)$), $L(\chi_D,s)$ may be written like the Riemann zeta function as a product over all the prime numbers:

$$L(\chi_D,s) = \sum_{n=1}^\infty\frac{\chi_D(n)}{n^s} = \prod_{p-\text{prime}}\left(1 - \frac{\chi_D(p)}{p^s}\right)^{-1}.$$

We've considered three $L$-functions related to the two fields $K = \mathbb Q(\sqrt{d})$ and $\mathbb Q$: $L(\chi_D, s)$, the Riemann zeta function, $\zeta(s)$, and the Dedekind zeta function associated to $K$, $\zeta_K(s)$. It turns out that among these three functions the following relation holds:

\begin{equation}\zeta_K(s) = \zeta(s)L(\chi_D,s).\end{equation}

If you know some algebraic number theory and/or commutative algebra, then you can see why this relation holds by looking at the product representation of each function, and using the property of $\chi_D$ that for a prime $p$, $\chi_D(p)$ is related to the behavior of the ideal $p\mathscr O_K$. (If you do this, it is important to note that $\zeta(s)$ and $L(\chi_D,s)$ are products over primes of $\mathbb Z$, and $\zeta_K(s)$ is a product over prime ideals of $\mathscr O_K$.) Using (3), the class number formula for $\mathbb Q$ and $K$ tells us what $L(\chi_D, 1)$ is.

Let us quickly determine the class number formula for $\mathbb Q$. The class number of $\mathbb Z$ is $1$ since there is unique factorization in $\mathbb Z$. The units of $\mathbb Z$ are $1$ and $-1$, so the regulator term in the class number formula for $\mathbb Q$ is $1$ and $\mu_\mathbb Q = 2$. There is only one embedding of $\mathbb Q$ into $\mathbb C$, and it is the identity on $\mathbb Q$, so it lands in $\mathbb R$. Hence $r_1 = 1, r_2=0$. Finally, using the one embedding and that $1$ is a $\mathbb Z$-basis for $\mathbb Z$ over $\mathbb Z$ gives use that the discriminant of $\mathbb Z$ is $1$. Putting this all together, the class number formula for $\mathbb Q$ says

$$\lim_{s\to1}(s-1)\zeta(s) = 1.$$

Then using the class number formula for $K$, the equality (3) gives us that

\begin{equation}L(\chi_D, 1) = \lim_{s\to 1}(s-1)\zeta_K(s) = \frac{2^{r_1}(2\pi)^{r_2}h_K\text{Reg}_K}{\sqrt{\left\lvert D\right\rvert}\mu_K},\end{equation}

where $r_1$ and $r_2$ are the invariants of $K$. To further analyze this formula, we need to break into the two cases of $d > 0$ and $d < 0$.

When $d < 0$ $r_1 = 0$ and $r_2 = 1$, so by Dirichlet's unit theorem $\mathscr O_K^\times/\mu(\mathscr O_K)$ is a free $\mathbb Z$-module of rank 0, so $\mu(\mathscr O_K) = \mathscr O_K^\times$ and $\text{Reg}_K = 1$. It turns out, and I will say more about this in my next post, that $\mu(\mathscr O_K) = \{\pm 1\}$ unless $d = -1$ or $-3$. When $d = -1$, $$\mu(\mathscr O_K) = \{\pm 1, \pm\sqrt{-1}\}$$ and when $d = -3$, $$\mu(\mathscr O_K) = \{\pm 1, \pm e^{2\pi i/3}, \pm e^{4\pi i/3}\}$$. Equation (4), then says the following: if $d = -1$

$$L(\chi_{-4}, 1) = h_K\frac{\pi}{4},$$

if $d = -3$

$$L(\chi_{-3}, 1) = h_K\frac{\pi}{3\sqrt{3}},$$

and if $d \not= -1, -3$

$$L(\chi_D, 1) = h_K\frac{\pi}{\sqrt{|D|}}.$$

These are remarkable formulas and explain where the formula (1) for $L(\chi_{-4}, 1)$ comes from (using in addition the fact that $h_K = 1$ in this case).

Now we consider when $d>0$. In this case $r_1 = 2$, $r_2 = 0$, $\mu(\mathscr O_K) = \{\pm 1\}$, and $\mathscr O_K^\times/\mu(\mathscr O_K)$ is a free $\mathbb Z$-module of rank $1$. Let $u_K\in\mathscr O_K^\times$ be an element of $\mathscr O_K^\times$ that generates $\mathscr O_K^\times/\mu(\mathscr O_K)$ as a $\mathbb Z$-module and such that $\left\lvert u_K\right\rvert > 1$. The element $u_K$ is called the fundamental unit of $K$. More about these will be said in my following posts. In this case, equation (4) says

$$L(\chi_D, 1) = \frac{2h_K\log(u_K)}{\sqrt{D}}.$$

This recovers the formula (2) for $L(\chi_8, 1)$, if we assume that we may take $u_K = 1 + \sqrt{2}$ for $K = \mathbb Q(\sqrt{2})$.

These remarkable formulas give tons of special value formulas resulting in identities for the infinite series $L(\chi_D, 1)$. Further, they give use a way to calculate $h_K$ (if in the real quadratic case we can determine $u_K$). Dirichlet was the first to prove these formulas, and that is why the class number formula is known as Dirichlet's class number formula. (Further, functions such as $L(\chi_D, s)$ are known as Dirichlet $L$-functions.) In my following post, I will use these formulas and write code to calculate the class numbers, $h_K$, for real and imaginary quadratic fields with $\left\lvert d\right\rvert < 100$.

Below is a reference that goes through all of this material in gory detail from a theoretical math perspective.

# Reference

H. Davenport, *Multiplicative Number Theory*. Graduate Texts in Mathematics, Springer New York, 2000.
