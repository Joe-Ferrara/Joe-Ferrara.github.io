---
layout: post
title: "(p-adic) Stark's Conjectures"
comment_issue_id: 6
sub: "lfunctions"
---

The goal of this post is to state some background and say what my thesis is about. In order to do this the post must be very technical, and I assume a high level of mathematical background. The reader has been warned. I will start out each section with a paragraph or two that gives an idea of what I'm talking about without needing much math background though. I also continue the narrative and build off of what I've introduced in previous posts.

# Artin $L$-functions

One way to define an $L$-function is to generalize the representation of $\zeta(s)$ by the product

$$\zeta(s) = \prod_{p-\text{prime}}\left(1 - \frac{1}{p^s}\right)^{-1}.$$

Since Euler was the first person to consider representing $\zeta(s)$ by the above product formula, this type of representation is called an Euler product. Artin $L$-functions are $L$-functions associated to representations of finite Galois groups, and defined using an Euler product.

Let $K/F$ be a Galois extension of number fields with Galois group $G$, and let

$$\rho:G\longrightarrow\text{GL}(V)$$

be a finite dimensional complex representation of $G$ with character $\chi$. The $L$-function of $\chi$ is defined by the Euler product

$$L(\chi,s) = \prod_{\mathfrak p\subset \mathscr O_F}\det(1 - \text{N}\mathfrak p^{-s}\rho(\sigma_\mathfrak P)\rvert_{V^{I_\mathfrak P}})^{-1}$$

where the product is over all nonzero prime ideals of $\mathscr O_F$, $\text{N}\mathfrak p$ is the absolute norm of $\mathfrak p$, $\mathfrak P$ is a prime of $K$ above $\mathfrak p$, $\sigma_\mathfrak P$ denotes the Frobenius of $\mathfrak P$ over $\mathfrak p$, $I_\mathfrak P\subset G$ is the intertia group of $\mathfrak P$ over $\mathfrak p$, and $V^{I_\mathfrak P}$ is the invariants of $V$ under $I_\mathfrak P$.

Let's consider the case when the base field $F$ is $\mathbb Q$, $K$ is the cyclotomic field $\mathbb Q(\zeta_n)$. Let

$$\chi:\text{Gal}(\mathbb Q(\zeta_n)/\mathbb Q)\cong(\mathbb Z/n\mathbb Z)^\times\longrightarrow\mathbb C^\times$$

be a $1$-dimensional representation. Such a $\chi$ is known as a *Dirichlet character* and $L(\chi,s)$ is known as a *Dirichlet $L$-function*. The $L$-functions, $L(\chi_D,s)$, from my previous posts are examples of these where $n = \left\lvert D\right\rvert$. In this case, $L(\chi,s)$ is defined as

$$L(\chi,s) = \prod_{\substack{p-\text{prime}\\ \gcd(p,n)=1}}\left(1 - \frac{\chi(p)}{p^s}\right)^{-1},$$

which is a clear generalization of $\zeta(s)$.

In this example, we can extend $\chi$ to a function on all integers by defining $\chi(a) = 0$ if $\gcd(a, n) > 1$. Then just as with the Riemann zeta function, we may also represent $L(\chi,s)$ as an $L$-series. This works by using the fact that $\chi$ is multiplicative: for all $a, b\in\mathbb Z$, $\chi(ab) = \chi(a)\chi(b)$. The relation between the $L$-series and Euler product representatiosn is:

$$L(\chi,s) = \sum_{n = 1}^\infty\frac{\chi(n)}{n^s} = \prod_{p-\text{prime}}\left(1 - \frac{\chi(p)}{p^s}\right)^{-1}.$$

We recover the example from my previous posts, $L(\chi_{-4},s)$, by defining $\chi_{-4}$ as

$$\chi_{-4}:\text{Gal}(\mathbb Q(i)/\mathbb Q) \cong (\mathbb Z/4\mathbb Z)^\times\longrightarrow \mathbb C^\times$$

$$\chi_{-4}(3 + 4\mathbb Z) = -1, \chi_{-4}(1 + 4\mathbb Z) = 1.$$

The Euler products in the definition of Artin $L$-functions do not converge for all $s\in\mathbb C$ just as the one for the Riemann zeta function doesn't. The Euler products converge for $s$ with large enough real part, and usually $\text{Re}(s) > 1$ will do. Artin's conjecture states that if $\chi$ is not the trivial character, then $L(\chi,s)$ has an analytic continuation to all of $\mathbb C$, and satisfies a functional equation relating $L(\chi,s)$ and $L(\overline{\chi},s)$. Artin's conjecture is known when the extension $K/F$ is abelian, but is open in general. It is known though that $L(\chi,s)$ has a meromorphic continuation to all of $\mathbb C$ and satisfies a functional equation.

# Stark's Conjectures

Stark's conjectures refine Dirichlet's class number formula in the case when there is a subfield $F\subset K$ such that $K/F$ is Galois. The idea behind them is to use the Galois group of $K/F$ to factor the regulator term in Dirichlet's class number formula, and then relate the factors to corresponding Artin $L$-functions. Stark's conjectures were stated by Stark in the 1970s ([[St1]](#St1),[[St2]](#St2),[[St3]](#St3)), and are mostly open except for the cases when the field $F$ is $\mathbb Q$ or imaginary quadratic and $K$ is an abelian extension.

Let $K/F$ be a Galois extension of number fields with Galois group $G$ and let $\chi$ be the character of a finite dimensional complex representation $\rho:G\rightarrow\text{GL}(V)$ of $G$. To obtain the factor of $\text{Reg}\_K$ corresponding to $\rho$ we introduce the following formalism. Let $Y$ be the free abelian group generated by the infinite places of $K$ (the real embeddings of $K$ into $\mathbb C$ and the complex conjugate pairs of embeddings). Let $X$ be the quotient of $Y$ by the subgroup generated by the vector $(1,1,\ldots, 1)$, and let $S_\infty$ be the infinite places of $K$. We define the logarithm map, which is a $G$-equivariant map, as

$$\lambda:\mathscr O_K^\times\longrightarrow \mathbb R X = \mathbb R\otimes_\mathbb Z X$$

$$\lambda(u) =  \sum_{v\in S_\infty}\log\left\lvert u\right\rvert_v v,$$

where $\left\lvert u\right\rvert_v = \left\lvert v(u)\right\rvert$ if $v$ is real and $\left\lvert u\right\rvert_v = \left\lvert v(u)\right\rvert^2$ if $v$ is complex. Dirichlet's equivariant unit theorem says that after tensoring with $\mathbb C$, $\lambda$ is an isomorphism. Then by character theory, there exists a $G$-equivariant isomorphism $f:\mathbb Q X = \mathbb Q\otimes_\mathbb Z X\longrightarrow \mathbb Q\mathscr O_K^\times = \mathbb Q\otimes_\mathbb Z\mathscr O_K^\times$. Fix such an $f$.

Let $V^\*$ be the $\mathbb C$-linear dual to $V$ with the contravariant $G$-action. The $G$-module $\text{Hom}\_G(V^{\*}, \mathbb C X)$ corresponds to the part of $\mathscr O_K^\times$ corresponding to $\rho$. This makes sense since after tensoring with $\mathbb C$, $\lambda$ is a $G$-equivariant isomorphism. Let $r(\chi)$ be the order vanishing of $L(\chi,s)$ at $s = 0$ and let $c(\chi)$ be the leading term of the Taylor expansion of $L(\chi,s)$ at $s = 0$.  It turns out that the $\mathbb C$-dimension of $\text{Hom}\_G(V^{\*}, \mathbb C X)$ is $r(\chi)$, which shows a connection between $L(\chi,s)$ at $s=0$ and $\text{Hom}\_G(V^{\*}, \mathbb C X)$. The connection is conjecturally much deeper.

Define the Stark regulator of $\chi$ and $f$ as the determinant of the map

$$(\lambda\circ f)_{V^*}:\text{Hom}_G(V^*,\mathbb C X)\longrightarrow \text{Hom}_G(V^*,\mathbb C X).$$

The regulator is denoted by $R(\chi, f)$. Stark's conjectures are that the ratio $\frac{R(\chi, f)}{c(\chi)}$ (which is a complex number) is in the subfield of $\mathbb C$ generated by the values of $\chi$. This field is denoted $\mathbb Q(\chi)$. The Stark regulator $R(\chi, f)$, or the normal regulator $\text{Reg}_K$, is a determinant of a matrix of logarithms of algebraic numbers, so it is highly transcendental. Stark's conjectures state that $R(\chi, f)$ is the transcendental part of the leading term of $L(\chi, s)$ at $s = 0$, and that the ratio, $\frac{R(\chi,f)}{c(\chi)}$ is an algebraic number in the field $\mathbb Q(\chi)$.

# $p$-adic Stark's Conjectures

In this this section I'll explain what a $p$-adic $L$-function is in the context of my research, and give some of the ideas of my research. Vaguely, a $p$-adic $L$-function is a function of a $p$-adic variable that is related to a complex $L$-function in some way. Given a complex $L$-function, in many cases it is not clear how to define the corresponding $p$-adic $L$-function, and the existence of $p$-adic $L$-functions is an area of current research in number theory. In many of the cases where $p$-adic $L$-functions are defined, they have been shown to satisfy similar properties to complex $L$-functions. In particular, there should be a way to state $p$-adic Stark's conjectures that are similar to the conjectures in the previous section but use the $p$-adic logarithm instead of the normal logarithm. The goal of my thesis was is to define a $p$-adic $L$-function in the case when $\chi$ is the character of a mixed signature abelian extension of a real quadratic field or a nontrivial character of an abelian extension of an imaginary quadratic field, and to state a $p$-adic Stark conjecture for the $p$-adic $L$-function.

If you've never seen the $p$-adic numbers before, then here is a super brief description. Let $p$ be a prime number. The $p$-adic rational numbers, denoted $\mathbb Q_p$, are a set that contains the rational numbers as a subset, and that "fills in the holes" in the rational numbers with respect to a certain way of measuring distance in $\mathbb Q$. The $p$-adic numbers are analogous to the real numbers in this filling the holes property. The real numbers fill in the holes that exist when we measure the distance between rationals by the usual notion of distance between two numbers. For the $p$-adic numbers, we measure the distance between two integers by saying two integers are close if their difference is divisible by a large power of $p.$ This is then extended to all rational numbers by representing rational numbers as the fraction of two integers. In mathematical terminology, we say that $\mathbb Q_p$ and $\mathbb R$ are completions of $\mathbb Q$ with respect to the $p$-adic and real metric. We denote $\mathbb Z_p$ as the completion of $\mathbb Z$ with respect to the $p$-adic metric, and we denote the completion of the algebraic closure of $\mathbb Q_p$ by $\mathbb C_p$. $\mathbb C_p$ is analogous to the complex numbers, $\mathbb C$, because $\mathbb C_p$ is a complete and algebraically closed field. Just like for the real or complex numbers, we consider continuous, analytic, and meromorphic functions with domain and codomain, $\mathbb Z_p,\mathbb Q_p$, or $\mathbb C_p.$

It is difficult to state as general a definition of a $p$-adic $L$-function as we did for Artin $L$-functions. Therefore we restrict ourselves to the case where $p$-adic $L$-functions exist and are of interest to us. Let $F$ be a quadratic field, and let $K/F$ be an abelian extension with Galois group $G$. Let $\chi:G\rightarrow\overline{\mathbb Q}^\times$ be a nontrivial 1-dimensional representation. We view an algebraic closure of $\mathbb Q$, $\overline{\mathbb Q}$, simultaneously as a subset of $\mathbb C$ and $\mathbb C_p$.

Assume $F$ is real quadratic. Then the types of $\chi$ that exist fall into three categories: even, odd, or of mixed signature. The category $\chi$ falls into depends on the value of $\chi$ on complex conjugations in $G$. If $\chi$ is even (respectively odd), the numbers

$$L(\chi, n) \text{ where } n\in \mathbb Z_{\leq 0} \text{ is an odd (resp. even) number}$$

are nonzero algebraic numbers ([[Si]](#Si)). Deligne-Ribet ([[DR]](#DR)) and Cassou-Nogues ([[Ca]](#Ca)) defined a $p$-adic analytic function $L_p(\chi, s)$ with domain $\mathbb Z_p$ and codomain $\mathbb C_p$, that for $n\in\mathbb Z_{\leq 0}$ takes the values of the complex $L$-functions just mentioned. More precisely, let $\chi$ be an even character of $G$. Then there exists an analytic function
$$L_p(\chi,s):\mathbb Z_p\longrightarrow\mathbb C_p$$
such that for all $n\in\mathbb Z_{\leq 0},$

$$L_p(\chi, n) = \prod_{\mathfrak p\mid p} \left(1 - \frac{\chi\omega^{n-1}(\mathfrak p)}{\text{N}\mathfrak p^n}\right)L(\chi\omega^{n-1}, n),$$

where $\omega$ is the Teichmuller character and the product is over all prime ideals $\mathfrak p\subset\mathscr O_F$ above the prime number $p$. We call $L_p(\chi,s)$ the $p$-adic $L$-function of $\chi$ and say that $L_p(\chi,s)$ interpolates the complex $L$-values $L(\chi\omega^{n-1}, n)$. It is remarkable that such a function exists because the definition of $L(\chi, s)$ is complex transcendental by nature. There is no apriori reason why its values at negative integers should satisfy any $p$-adic continuity properties.

There is a Stark conjecture for $L_p(\chi,s)$ at $s = 0$ and at $s = 1$. The conjecture at $s = 0$ is known as the Gross-Stark conjecture ([[Gr]](#Gr)), and the formula for the leading term of $L_p(\chi,s)$ at $s = 0$ is a recent theorem of Dasgupta-Kakde-Ventullo ([[DKV]](#DKV)) following earlier partial results of Darmon-Dasgupta-Pollack ([[DDP]](#DDP)). The conjecture at $s = 1$ is known as the Serre-Solomon-Stark conjecture ([[So]](#So)) and is open. The conjecture for $L_p(\chi,s)$ at $s = 0$ concerns the odd characters of $G$ and the conjecture at $s = 1$ concerns the even characters.

My research, when $F$ is a real quadratic field, concerns the case of a mixed signature character. Let $\chi$ be a mixed signature character of $G$. In this case there has not been a $p$-adic $L$-function defined, and one of the reasons for this is that $L(\chi, n) = 0$ for all $n\in\mathbb Z_{\leq 0}$. Therefore because the negative integers are dense in $\mathbb Z_p$, if a $p$-adic $L$-function interpolated them, then the function would be identically zero. Defining $p$-adic $L$-functions when there are no interpolation points coming from complex $L$-functions is a difficult problem in general, and an area of active current research. In the case of a mixed signature character, we make the definition by using the theory of modular forms and $p$-adic variation of modular forms.

Specifically, if $\chi$ is a mixed signature character, then the $q$-expansion

$$\theta_\chi = \sum_{\mathfrak a\subset\mathscr O_F}\chi(\mathfrak a)q^{N\mathfrak a}$$

is a weight one Hecke eigenform and the $L$-function of $\theta_\chi$ is the same as the $L$-function of $\chi$. There do not exist $p$-adic $L$-functions of weight one modular forms, but there do exist $p$-adic $L$-functions of higher weight Hecke eigenforms. By putting $\theta_\chi$ into a $p$-adic family of modular forms, taking the two-variable $p$-adic $L$-function of the family, and specializing the two-variable $p$-adic $L$-function to weight one we obtain a definition of a $p$-adic $L$-function of $\theta_\chi$ and so in turn of $\chi$. Making the Stark conjecture is then easy by looking at the Stark conjecture in the complex case and replacing the usual logarithm with the $p$-adic logarithm. This is exactly what I do in my thesis.

I should say something as well about the case when $F$ is imaginary quadratic. When $F$ is imaginary quadratic, $K$ is an abelian extension of $F$, and $\chi$ is a nontrivial character of $G$, then $L(\chi, n) = 0$ for all $n\in\mathbb Z_{\leq 0}$ as well. In this case, when $p$ is split in $F$ Katz defined a $p$-adic $L$-function ([[Ka]](#Ka)), stated, and proved a $p$-adic Stark conjecture known as Katz's $p$-adic Kronecker's second limit formula. In the case when $p$ is split or inert, the above construction using $p$-adic modular forms works to define a $p$-adic $L$-function and state a $p$-adic Stark conjecture just as it does when $F$ is real quadratic and $\chi$ is mixed signature. I do this in my thesis. When $p$ is split the $p$-adic $L$-function obtained is the same as Katz's and when $p$ is inert a new $p$-adic $L$-function is obtained.

# References

<a name="Ca">[Ca]</a> P. Cassou-Nogues, *Valeurs aux entiers negatifs des fonctions zeta et fonctions zeta $p$-adiques*. Invet. Math **51**(1) (1979), 29-59.

<a name="DDP">[DDP]</a> S. Dasgupta, H. Darmon, R. Pollack, *Hilbert modular forms and the Gross-Stark conjecture*, Ann. of Math., **174**(1) (2011), 439-483.

<a name="DKV">[DKV]</a> S. Dasgupta, M. Kakde, K. Ventullo, *On the Gross-Stark conjecture*, Ann. of Math., **188** (2018), no. 3, 833-870.

<a name="DR">[DR]</a> P. Deligne, K. Ribet, *Values of abelian $L$-functions at negative integers over totally real fields*, Inventiones Math., **59** (1980), 227-286.

<a name="Gr">[Gr]</a> B. Gross, *$p$-adic $L$-series at $s=0$*. Fac. Sci. Univ. Tokyo Sect. IA Math., **28**(3) (1981-82) 979-994.

<a name="Ka">[Ka]</a> N. Katz, *$p$-adic Interpolation of Real Analytic Eisenstein Series*. Ann. of Math., **104**(3) (1976), 459-571.

<a name="Si">[Si]</a> C. L. Siegel, *Uber die Fourierschen Koeffizienten von Modulformen*, Nachr. Akad. Wiss. Gottingen, No. 3 (1970) 15-56 (Ges. Abh. IV, No. 90).

<a name="So">[So]</a> D. Solomon, *p-adic Abelian Stark conjectures at s = 1*, Ann. De L'institut Fourier, Tome 52, n2 (2002), 379-417.

<a name="St1">[St1]</a> H.M. Stark, *L-Functions at s = 1. II. Artin L-functions with Rational Characters*, Adv. Math. **17** (1975), 60-92.

<a name="St2">[St2]</a> H.M. Stark, *L-Functions at s = 1. III. Totally Real Fields and Hilbert's 12th Problem*, Adv. Math. **22** (1976), 64-84.

<a name="St3">[St3]</a> H.M. Stark, *L-Functions at s = 1. IV. First Derivatives at s = 0.*, Adv. Math. **35** (1980), 197-235.
