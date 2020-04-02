---
layout: post
title: "Introduction to L-functions IV: Units and Imaginary Quadratic Class Numbers"
comment_issue_id: 4
---

Let $K$ be the quadratic field $\mathbb Q(\sqrt{d})$ and let $D$ be $K$'s discriminant. In my previous post I gave a formula for the class number of $K$ in terms of the special value of the $L$-function $L(\chi_D, s)$ at $s = 1$. When $K$ is imaginary quadratic the formula is

$$\begin{equation}h_K = \frac{L(\chi_D, 1) \mu_K \sqrt{|D|}}{2\pi}\end{equation}$$

and when $K$ is real quadratic the formula is

$$\begin{equation}h_K = \frac{\sqrt{D}}{2\log|u_K|}\end{equation}$$

where $u_K$ is a fundamental unit of $K$ (which means $u_K$ generates $\mathscr O_K^\times/\mu(\mathscr O_K))$ as a $\mathbb Z$-module). In this and the following post I will use these formulas to calculate class numbers in practice. In order to do this, I'll need to discuss the units $\mathscr O_K^\times$ in more depth to determine $\mu_K$ and $u_K$.

In this post specifically, I will first relate determining $\mathscr O_K^\times$ to finding the integer solutions to a polynomial equation with two variables, then using this I'll determine the units of an imaginary quadratic field. Once the units of an imaginary quadratic fields are determined, I will use (1), along with some code I wrote, to calculate the class numbers of imaginary quadratic fields with $\left\lvert d\right\rvert < 100$. In the following post, I'll address the same questions for real quadratic fields and use (2) to calculate class numbers of real quadratic fields.

# Units of $\mathscr O_K$

Assume $d\equiv 2$ or $3\bmod 4$. Then

$$\mathscr O_K = \{\alpha + \beta\sqrt{d} : \alpha, \beta\in\mathbb Z\},$$

and so for $\alpha + \beta\sqrt{d}\in\mathscr O_K$, $\alpha + \beta\sqrt{d}\in \mathscr O_K^\times$ if and only if $1/(\alpha + \beta\sqrt{d})\in \mathscr O_K$. We write $1/(\alpha + \beta\sqrt{d})$ in terms of the basis $1, \sqrt{d}$ by rationalizing the denominator:

$$\frac{1}{\alpha + \beta\sqrt{d}} = \frac{1}{\alpha + \beta\sqrt{d}}\frac{\alpha - \beta\sqrt{d}}{\alpha - \beta\sqrt{d}} = \frac{\alpha}{\alpha^2 - d\beta^2} - \frac{\beta}{\alpha^2 - d\beta^2}\sqrt{d}.$$

Then by the above expression, $\alpha + \beta\sqrt{d}\in\mathscr O_K^\times$ if and only if

$$\frac{\alpha}{\alpha^2 - d\beta^2}, \frac{\beta}{\alpha^2 - d\beta^2}\in\mathbb Z$$

which is if and only if $\alpha^2 - d\beta^2$ divides $\alpha$ and $\beta$ in $\mathbb Z$.

It is clear that if $\alpha^2 - d\beta^2 = \pm1$, then $\alpha + \beta\sqrt{d}$ is a unit in $\mathscr O_K$ since $\pm1$ divide any integer. It turns out the converse is true as well, which I'll show with a quick proof.

Assume $\alpha + \beta\sqrt{d}$ is a unit in $\mathscr O_K$, so $\alpha^2 - d\beta^2$ divides $\alpha$ and $\beta$. Either $\alpha^2 - d\beta^2$ is $\pm 1$ or $\alpha^2 - d\beta^2$ is divisible by some prime number. Let's assume $\alpha^2 - d\beta^2$ is divisible by a prime number and proceed to get a contradiction. Let $p$ be a prime that divides $\alpha^2 - d\beta^2$. Then $p$ divides $\alpha$ and $p$ divides $\beta$. Let $p^k$ be the largest power of $p$ dividing both $\alpha$ and $\beta$. Then $p^{2k}$ divides $\alpha^2 - d\beta^2$. But since $\alpha^2 - d\beta^2$ divides $\alpha$ and $\beta$, then $p^{2k}$ divides $\alpha$ and $\beta$. This is a contradiction because $2k > k$ and $p^k$ is the largest power of $p$ that divides both $\alpha$ and $\beta$.

We've now shown that $\alpha + \beta\sqrt{d}\in \mathscr O_K$ is a unit if and only if $\alpha^2 - d\beta^2 = \pm 1$. Therefore determining the units in $\mathscr O_K$ amounts to determining the integer solutions to the equation $x^2 - dy^2 = \pm 1$. Before proceeding to analyze what the solutions are, let's address the case when $d\equiv 1\bmod 4$.

If $d\equiv 1\bmod 4$, then

$$\begin{equation} \mathscr O_K = \left\{ \alpha + \beta \frac{1 + \sqrt{d}}{2} : \alpha, \beta\in \mathbb Z\right\}.\end{equation}$$

In order to determine $\mathscr O_K^\times$, I would like to follow the same line of reasoning followed when $d\equiv 2$ or $3\bmod 4$. To do this, we first rewrite the representation of $\mathscr O_K$ above, so that is is similar to the representation of $\mathscr O_K$ when $d\equiv 2$ or $3\bmod 4$.

Specifically, I claim that when $d\equiv 1\bmod 4$,

$$\begin{equation}\mathscr O_K = \left\{\frac{1}{2}(\alpha + \beta\sqrt{d}) : \alpha, \beta\in \mathbb Z, \alpha\equiv \beta\bmod 2\right\}.\end{equation}$$

Indeed, I'll prove it by showing that each representation of $\mathscr O_K$ is contained in the other one. Given $\alpha + \beta\frac{1 + \sqrt{d}}{2}$ we can rewrite is as

$$\alpha + \beta\frac{1 + \sqrt{d}}{2} = \alpha + \frac{\beta}{2} + \beta\frac{\sqrt{d}}{2} = \frac{1}{2}(2\alpha + \beta + \beta\sqrt{d}).$$

Then since $2\alpha + \beta \equiv \beta\bmod 2$, this writes $\alpha + \beta\frac{1 + \sqrt{d}}{2}$ as in (4). Conversely, if we have $\frac{1}{2}(\gamma + \delta\sqrt{d})$ where $\gamma,\delta\in\mathbb Z$ with $\gamma\equiv \delta\bmod 2$, then $\gamma = \delta + 2\alpha$ for some $\alpha\in\mathbb Z$, and so

$$\frac{1}{2}(\gamma + \delta\sqrt{d}) = \frac{1}{2}(2\alpha + \delta + \delta \sqrt{d}) = \alpha + \delta\frac{1 + \sqrt{d}}{2},$$

which writes $\frac{1}{2}(\gamma + \delta\sqrt{d})$ as in (3).

Now with the representation (4), we can calculate the units $\mathscr O_K^\times$ as we did when $d\equiv 2$ or $3\bmod 4$. Let $\frac{1}{2}(\alpha + \beta\sqrt{d})\in\mathscr O_K$. Then $\frac{1}{2}(\alpha + \beta\sqrt{d})\in\mathscr O_K^\times$ if and only if

$$\frac{2}{\alpha + \beta\sqrt{d}} = \frac{2}{\alpha + \beta\sqrt{d}}\frac{\alpha - \beta\sqrt{d}}{\alpha - \beta\sqrt{d}} = \frac{1}{2}\left(\frac{4\alpha}{\alpha^2 - d\beta^2} - \frac{4\beta}{\alpha^2 - d\beta^2}\sqrt{d}\right) \in \mathscr O_K.$$

With similar reasoning as when $d\equiv 2$ or $3\bmod 4$, one shows that $\frac{1}{2}(\frac{4\alpha}{\alpha^2 - d\beta^2} - \frac{4\beta}{\alpha^2 - d\beta^2}\sqrt{d}) \in \mathscr O_K$ if and only if $\alpha^2 - d\beta^2 = \pm4$. Then the units of $\mathscr O_K$ are determined by the integer solutions to the equation $x^2 - dy^2 = \pm4$.

To conclude and summarize, we've shown that if $d\equiv 2$ or $3\bmod 4$, then $\mathscr O_K^\times$ is determined by the integral solutions to $x^2 - dy^2 = \pm1$, and if $d\equiv1\bmod 4$, then $\mathscr O_K^\times$ is determined by the integral solutions of $x^2 - dy^2 = \pm4$.

# The Imaginary Quadratic Case

Assume $d < 0$, so $K$ is an imaginary quadratic field. Let's determine $\mathscr O_K^\times$. Since $d < 0$, for $x$, $y\in\mathbb Z$, $x^2 - dy^2 \geq 0$, so there are no solutions to $x^2 - dy^2 = -1$ or $x^2 - dy^2 = -4$. We are then to look for solutions to $x^2 - dy^2 = 1$ when $d\equiv 2$ or $3\bmod 4$ and $x^2 - dy^2 = 4$ when $d\equiv 1\bmod 4$. We'll see that for either case of $d$, there is one outlier $K$, and when $K$ is not the outlier, the only units are $\pm 1$.

First assume $d\equiv 2$ or $3\bmod 4$ and let $\alpha,\beta\in\mathbb Z$ be a solution to $x^2 - dy^2 = \pm 1$. If $d < -1$ and $\beta\not=0$, then $\alpha^2 - d\beta^2 > 1$, so if $d < -1$, then $\alpha^2 = 1$. Therefore the only possible solutions are $\alpha = \pm1$ and $\beta = 0$, and so we've shown that if $d\equiv 2$ or $3\bmod 4$ and $d < -1$, then

$$\mathscr O_K^\times = \{\pm 1\}.$$

The outlier case is when $d = -1$, which we now consider. If $d = -1$, then $\alpha^2 + \beta^2 = 1$. The only possible $\alpha,\beta\in\mathbb Z$ that satisfy this are $\alpha = \pm 1$ and $\beta = 0$ or $\alpha = 0$ and $\beta = \pm 1$. Therefore when $d = -1$,

$$\mathscr O_K^\times = \{\pm 1, \pm \sqrt{-1}\}.$$

This finishes the cases when $d\equiv 2$ or $3\bmod 4$.

Now assume $d\equiv 1\bmod 4$, and let $\alpha,\beta\in\mathbb Z$ be a solution to $x^2 - dy^2 = \pm 4$. If $d < -4$ and $\beta \not=0$, then $\alpha^2 - d\beta^2 > 4$, so if $-d > 4$, $\alpha^2 = 4$. Therefore the only possible solutions are $\alpha = \pm 2$ and $\beta = 0$, and so we've shown that if $d \equiv 1 \bmod 4$ and $d < -4$, then

$$\mathscr O_K^\times = \left\{\frac{1}{2}(\pm 2)\right\} = \{\pm 1\}.$$

The only $d$ such that $-4\leq d<0$ and $d\equiv 1\bmod 4$ is $d = -3$. This is the outlier case when $d\equiv 1\bmod 4$. Let $d = -3$, and let $\alpha,\beta \in\mathbb Z$ be such that $\alpha^2 - d\beta^2 = \pm 4$. This says that $\alpha^2 + 3\beta^2 = \pm 4$. Then $\left\lvert\alpha\right\rvert$ cannot be larger than $2$ and $\left\lvert\beta\right\rvert$ cannot be larger than $1$. Therefore the possible choices for $\alpha$ and $\beta$ are $\alpha = \pm 2$, $\beta = 0$ or $\alpha = \pm 1$, $\beta = \pm 1$ or $\alpha = \pm 1$, $\beta = \mp 1$. Hence when $d = -3$,

$$\mathscr O_K^\times = \left\{\pm 1, \frac{1 \pm \sqrt{-3}}{2}, \frac{-1 \pm \sqrt{-3}}{2}\right\}.$$

# Imaginary Quadratic Class Numbers

Now that we've determined the units of any imaginary quadratic field, we can use (1) to calculate class numbers. Let's note that if $d = -1$ then $\mu_K = 4$, if $d = -3$ then $\mu_K = 6$, and otherwise $\mu_K = 2$. (Note that $(\frac{1}{2}(1 + \sqrt{-3}))^6 = 1$ so $\frac{1}{2}(1 + \sqrt{-3})$ is a root of unity. Similar relations hold for the other 3 units involving $\sqrt{-3}$.)

At the github repository [here](https://github.com/Joe-Ferrara/IntroToLfunctions), I wrote code to calculate the class numbers. Specifically, the script quad_Lfunctions.py has a function quad_Lval(d, n), which calculates the first $n$-terms of the sum for the value $L(\chi_D, 1)$. The script imag_quad_class_numbers.py then calculates the class numbers of $\mathbb Q(\sqrt{d})$ for all $d$ such that $d<0$ and $\left\lvert d\right\rvert < 100$. The class numbers have been recorded in the following table.

| d | Class Number of $\mathbb Q(\sqrt{d})$ | | d | Class Number of $\mathbb Q(\sqrt{d})$|
| --- | --- | | --- | --- |
| -1 | 1 | | -51 | 2 |
| -2 | 1 | | -53 | 6 |
| -3 | 1 | | -55 | 4 |
| -5 | 2 | | -57 | 4 |
| -6 | 2 | | -58 | 2 |
| -7 | 1 | | -59 | 3 |
| -10 | 2 | | -61 | 6 |
| -11 | 1 | | -62 | 8 |
| -13 | 2 | | -65 | 8 |
| -14 | 4 | | -66 | 8 |
| -15 | 2 | | -67 | 1 |
| -17 | 4 | | -69 | 8 |
| -19 | 1 | | -70 | 4 |
| -21 | 4 | | -71 | 7 |
| -22 | 2 | | -73 | 4 |
| -23 | 3 | | -74 | 10 |
| -26 | 6 | | -77 | 8 |
| -29 | 6 | | -78 | 4 |
| -30 | 4 | | -79 | 5 |
| -31 | 3 | | -82 | 4 |
| -33 | 4 | | -83 | 3 |
| -34 | 4 | | -85 | 4 |
| -35 | 2 | | -86 | 10 |
| -37 | 2 | | -87 | 6 |
| -38 | 6 | | -89 | 12 |
| -39 | 4 | | -91 | 2 |
| -41 | 8 | | -93 | 4 |
| -42 | 4 | | -94 | 8 |
| -43 | 1 | | -95 | 8 |
| -46 | 4 | | -97 | 4 |
| -47 | 5 | | | |

It appears that the class numbers get larger on average as $\left\lvert d\right\rvert$ gets larger. This is true in general, and it turns out that for any $h$, there are only finitely many imaginary quadratic fields which class number $h$. The $d$'s that have class number $1$ are $d = -1, -2, -3, -7, -11, -19, -43, -67, -163$. All of which are in the above table except $d = -163$.
