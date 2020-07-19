---
layout: post
title:  "The Riemann Zeta Function"
comment_issue_id: 1
sub: "lfunctions"
---

# The Riemann zeta Function

Number theory is one of the oldest areas of mathematics, and at the heart of number theory is the study of prime numbers. A prime number is a whole number larger than $1$ such that the only positive whole numbers that divide it evenly are $1$ and itself. For example $5$ is prime number, but $6$ is not because $2$ divides $6$. The first few prime numbers are

$$2,3,5,7,11,13,17,19,23,29,31,37,41,43,47,53,59,61,67,71,73,79,\ldots.$$

Euclid in about 300 B.C.E. was the first to show that there are infinitely many prime numbers.

One reason prime numbers are of interest in the study of numbers is that prime numbers are the atoms of whole numbers. The fundamental theorem of arithmetic, also proved by Euclid, says that every every whole number greater that $1$ can be written uniquely as a product of prime numbers. For example $6$ from before is written as a product of prime numbers as $6 = 2\cdot 3$. A few other examples are $12 = 2^2\cdot3$, $869 = 11\cdot 79$, and $7735 = 5\cdot 7\cdot 13\cdot 17$.

The infinitude of primes and the fundamental theorem of arithmetic lead to two natural questions: How are the prime numbers distributed among all the whole numbers? Do other number systems exist with their own prime numbers and a fundamental theorem of arithmetic? The study of $L$-functions is central in addressing and studying these two questions in modern number theory. In this series of posts, I will explain some of the roles $L$-functions play classically in addressing the aforementioned questions, introduce the modern perspective on $L$-functions, and explain how my research fits into the modern picture. In this first post I consider the first $L$-function, known today as the Riemann zeta function and denoted $\zeta(s)$.

The Riemann zeta function, $\zeta(s)$, was first studied by Leonhard Euler in the 1700s. He gave its definition as the infinite series

$$\zeta(s) = \sum_{n = 1}^\infty\frac{1}{n^s},$$

where $s$ is a real variable greater than $1$. Note that if we plug in $s = 1$, we get the harmonic series that diverges.

Euler used this divergence at $s=1$ to give a new proof of the infinitude of primes, exhibiting some of the interesting properties of $\zeta(s)$. His argument was the following: Using unique factorization of the integers in the denominators of the sum defining $\zeta(s)$, we have

$$\zeta(s) = \sum_{n = 1}^\infty \frac{1}{n^s} = \prod_{\substack{p\\ \text{prime}}}\sum_{n=0}^\infty\frac{1}{p^{ns}}.$$

Then, using the geometric series formula

$$\sum_{n=0}^\infty x^n = \frac{1}{1 - x}$$

with $x = \frac{1}{p^s}$, we can rewrite $\zeta(s)$ as an infinite product over all the prime numbers:

$$\zeta(s) = \prod_{p-\text{prime}}\left(1 - \frac{1}{p^s}\right)^{-1}.$$

We now apply the natural logarithm to this, distribute it over the product and use the power series expansion

$$-\log(1 - x) = \sum_{n = 1}^\infty\frac{x^n}{n}$$

with $x = \frac{1}{p^s}$ to get

$$\log(\zeta(s)) = \sum_{\substack{p\\ \text{prime}}}\sum_{n=1}^\infty \frac{1}{p^{ns}}.$$

Plugging in $s = 1$ and rearranging the sums gives

$$\infty = \log(\zeta(1)) = \sum_{\substack{p\\ \text{prime}}}\frac{1}{p} + \sum_{\substack{p\\\text{prime}}}\sum_{n=2}^\infty\frac{1}{p^{n}}.$$

We can simplify the second sum to get

$$\sum_{\substack{p\\\text{prime}}}\sum_{n=2}^\infty\frac{1}{p^n} = \sum_{\substack{p\\\text{prime}}}\frac{1}{p^2}\sum_{n=0}^\infty\frac{1}{p^n} = \sum_{\substack{p\\\text{prime}}}\frac{1}{p^2}\frac{1}{1 - \frac{1}{p}} = \sum_{\substack{p\\\text{prime}}}\frac{1}{p(p - 1)},$$

and then bound it via

$$\sum_{\substack{p\\\text{prime}}}\frac{1}{p(p-1)}\leq \sum_{n = 2}^\infty\frac{1}{n(n-1)} = 1.$$

In the appendix below, I show that $\displaystyle \sum_{n=2}^\infty \frac{1}{n(n-1)} = 1$. We've then shown that

$$\infty = \sum_{\substack{p\\\text{prime}}}\frac{1}{p},$$

which implies that there are infinitely many prime numbers since if there were finitely many then the above sum could not be infinite.

Euler's proof is the tip of the iceberg in the relation of $\zeta(s)$ to the prime numbers. Another important example is the relationship between the Riemann zeta function and the distribution of primes.  One can observe that there are fewer primes amongst large numbers than amongst the small ones. For example in the list of primes above, the second half of the list has more jumps of size $6$ than the first half of the list. Gauss in the late 1700s and early 1800s studied this phenomenon and made precise statements about the rate at which the prime numbers become more spread out. He conjectured that asymptotically the number of prime numbers less than $x$ is

$$\frac{x}{\log x}.$$

Since $\log x$ grows slower than $x$, this matches the observation that primes become more spread out amongst larger numbers. Further, it gives a candidate function to measure the rate at which primes grow. In more precise terms, Gauss' conjecture said the following: let $\pi(x)$ be the number of primes less than the real number $x$. Then

$$\lim_{x\to\infty}\frac{\pi(x)}{\frac{x}{\log x}} = 1.$$

Gauss' conjecture is true, and it turns out that there is a better function to use than $\frac{x}{\log(x)}$ to approximate $\pi(x)$. This function is known as $\text{Li}(x)$, and defined by the integral

$$\text{Li}(x) = \int_{2}^x\frac{dt}{\log t}.$$

The function $\text{Li}(x)$ was introduced by Dirichlet in a letter to Gauss.

In the mid 1800s Riemann developed the tools necessary to prove that

$$\lim_{x\to\infty}\frac{\pi(x)}{\text{Li}(x)} = 1,$$

showing that $\text{Li}(x)$ is asymptotically a good approximation of $\pi(x)$. The theorem that $\displaystyle\lim_{x\to\infty}(\pi(x)/\text{Li}(x)) = 1$ is known as the prime number theorem, and the main ingredient of the proof comes from a study of the aforementioned Riemann zeta function

$$\zeta(s) = \sum_{n = 1}^\infty\frac{1}{n^s}.$$

Riemann's study of $\zeta(s)$ is why the function bears his name, and one of Riemann's key insights is to view $s$ as a not just a real variable but as a complex variable. Riemann found a way to make sense of the function $\zeta(s)$ at complex numbers for which the sum does not converge. This idea of defining a complex analytic function given by a series at points where the series does not converge is known as meromorphic (or analytic) continuation.

Riemann's work on the distribution of prime numbers went further than just considering the limit $\displaystyle\lim_{x\to\infty}(\pi(x)/\text{Li}(x))$. He considered how good of an approximation $\text{Li}(x)$ is to $\pi(x)$, and conjectured that as $x$ goes to infinity,

$$|\pi(x) - \text{Li}(x)| < x^{1/2 + \varepsilon} \text{ for any }\varepsilon > 0.$$

This is much better than the prime number theorem because it gives a bound for how much $\text{Li}(x)$ is off from $\pi(x)$. Riemann showed that a certain conjectural property of the Riemann zeta function implies the above bound. This property of $\zeta(s)$ is known as the Riemann hypothesis and is arguably the biggest open problem in number theory.

The Riemann hypthesis says that all of the zeros of the function $\zeta(s)$ in the complex plane with real part greater than $0$ have real part $\frac{1}{2}$. The Riemann hypothesis was one of 7 millennium problems stated in the year 2000 by the Clay math institute as the most important open problems in mathematics. The Clay math institute offered a prize of 1 million dollars to anyone who solved one of the problems. Of the 7 problems only 1 (as of now) has been solved.

# References

L.J. Goldstein, *A History of the Prime Number Theorem*. The American Mathematical Monthly, Vol. 80, No. 6 (Jun. - Jul., 1973), pp 599-615.

# Appendix: Power Series Stuff

In this brief appendix, I'll record some power series facts that were used in the post, and I'll prove that

$$\sum_{n=2}^\infty \frac{1}{n(n-1)} = 1.$$

We have the geometric series identity

$$\frac{1}{1-x} = \sum_{n = 0}^\infty x^n.$$

The series converges for $x$ such that $-1<x<1$. If we integrate both sides of the equation, we get

$$-\log(1-x) = \sum_{n = 1}^\infty \frac{x^n}{n}.$$

If we integrate again, we get

$$-\int_0^x\log(1 - t)dt = \sum_{n=2}^\infty\frac{x^n}{n(n-1)}.$$

Taking the limit of both sides as $x$ goes to $1$ gives

$$-\lim_{x\to 1}\int_0^x\log(1-t)dt = \sum_{n=2}^\infty\frac{1}{n(n-1)}.$$

Therefore to evaluate $\displaystyle \sum_{n=2}^\infty\frac{1}{n(n-1)}$, we evaluate the limit, $\displaystyle\lim_{x\to1}\int_0^x\log(1-t)dt$.

Integrating by parts with $u = \log(1-t)$, and $dv = dt$, gives that

$$\int\log(1-t)dt = t\log(1-t) + \int\frac{t}{1-t}dt.$$

Integrating more gives

$$\int\frac{t}{1-t}dt = \int\frac{t-1+1}{1-t}dt = -\int dt + \int\frac{dt}{1-t} = -t-\log(1-t),$$

so

$$\int\log(1-t)dt = (t-1)\log(1-t) - t,$$

and so

$$\lim_{x\to 1}\int_0^x\log(1-t)dt = \lim_{x\to 1}(x-1)\log(1-x) - 1.$$

Using l'Hospital's rule, we get that

$$\lim_{x\to 1}(x-1)\log(1-x) = 0,$$

and so we conclude that

$$\sum_{n=2}^\infty\frac{1}{n(n-1)} = -\lim_{x\to 1}\int_0^x\log(1-t)dt = 1.$$
