---
layout: post
title:  "Coding Theory: Reed-Solomon Codes"
comment_issue_id: 9
---


Reed-Solomon codes are maximum distance separable codes which can be constructed with arbitrarily large minimum distance. The fact that the minimum distance can be arbitrarily large is a huge step up from Hamming codes. On the other hand, in order to increase the minimum distance we need to increase the size of the alphabet. That is, to obtain a large minimum distance, one needs to work with $\mathbb F\_q$ where $q$ is large. As we will see, Reed-Solomon codes use polynomials over $\mathbb F\_q$ to encode and have a clever decoding algorithm. The parameters of a Reed-Solomon code are integers $k$, $n$, and $q$ such that $k\leq n\leq q$ and $q$ is a prime power, and these parameters produce an $(n, k, n-k+1)\_q$-code.

# Encoding

Let $k$, $n$, and $q$ be integers such that $k\leq n\leq q$ and $q$ is a prime power. We denote the encoding function for our Reed-Solomon code as $\varphi:\mathbb F\_q^k\rightarrow \mathbb F\_q^n$ since the letter $E$ will be used to mean something different later. Let $a\_1,a\_2,\ldots,a\_n\in \mathbb F\_q$ be $n$ distinct elements, which are fixed throughout. If the characteristic of $\mathbb F\_q$ is $p$ and $p > n$, then we can take $0, 1, 2,\ldots, n-1$ as the $a\_1,a\_2,\ldots,a\_n$. When programming Reed-Solomon codes this is the approach we use. Let

$$\boldsymbol{x} = (x_0,x_1,\ldots,x_{k-1})\in\mathbb F_q^k$$

be a message, and define the polynomial

$$P_{\boldsymbol{x}}(z) = \sum_{j = 0}^{k-1}x_jz^j\in\mathbb F_q[z].$$

Define $\varphi(\boldsymbol{x})$ as

$$\varphi(\boldsymbol{x}) = (P_\boldsymbol{x}(a_1), P_\boldsymbol{x}(a_2), \ldots, P_\boldsymbol{x}(a_n))\in \mathbb F_q^n.$$

Let's check that $\varphi$ is linear and injective.

Linearity: let $\boldsymbol{x},\boldsymbol{x}'\in\mathbb F\_q^k$ and $\lambda\in\mathbb F\_q$. Then

$$\begin{array}{rl} \varphi(\boldsymbol{x} + \lambda\boldsymbol{x}') &= (P_{\boldsymbol{x} + \lambda\boldsymbol{x}'}(a_i))_{1\leq i\leq n}\\
											   &= (P_\boldsymbol{x}(a_i) + \lambda P_{\boldsymbol{x}'}(a_i))_{1\leq i\leq n}\\
											   &= \varphi(\boldsymbol{x}) + \lambda\varphi(\boldsymbol{x}').\end{array}$$

Injectivity: Assume $\varphi(\boldsymbol{x}) = \varphi(\boldsymbol{x}')$ for $\boldsymbol{x},\boldsymbol{x}'\in \mathbb F\_q^k$. Then $(P\_\boldsymbol{x} - P\_{\boldsymbol{x}'})(a\_i) = 0$ for all $i = 1,\ldots,n$. The polynomial $P\_\boldsymbol{x} - P\_{\boldsymbol{x}'}$ is of degree at most $k-1$, and so it has at most $k-1$ roots unless it is the zero polynomial. But $a\_1,\ldots,a\_n$ are $n$ roots and $n\geq k> k-1$, so $P\_\boldsymbol{x} - P\_{\boldsymbol{x}'}$ is the zero polynomial. Hence $P\_\boldsymbol{x} = P\_{\boldsymbol{x}'}$. It follows that $\boldsymbol{x} = \boldsymbol{x}'$ since two polynomials are the same if and only if their coefficients are the same. Therefore, we have shown that $\varphi$ is linear and injective.

Let $C$ be the image of $\varphi$ so $C$ is a code and $\varphi$ is an encoding function for $C$. We now determine the minimum distance of $C$. Given $\boldsymbol{x}\in\mathbb F\_q^k$, we need to see how many coordinates of $\varphi(\boldsymbol{x})$ differ from $0$. Again we argue using the degree of $P\_\boldsymbol{x}(z)$: $P\_\boldsymbol{x}(z)$ has degree $k-1$ and so has at most $k-1$ roots. Therefore since the $a\_i$ are distinct and there are $n$ of them, $\varphi(\boldsymbol{x})$ must differ from $0$ at at least $n-(k-1) = n - k + 1$ coordinates. Hence the minimum distance of the image of $\varphi$ is at least $n-k + 1$. On the other hand, if we take $\boldsymbol{x}$ to have coordinates the coefficients of the polynomial

 $$P(z) = \prod_{i = 1}^{k-1} (z - a_i),$$

then $\varphi(\boldsymbol{x})$ is $0$ at exactly $k-1$ coordinates, so the minimum distance of $C$ is at most $n - (k - 1) = n - k + 1$. Therefore, we have shown that the minimum distance of $C$ is $n-k + 1$.

We have now constructed an $(n, k, n-k+1)\_q$ code for any $k\leq n\leq q$. This code meets the Singleton bound since $k + n-k+1 = n + 1$, and so is a maximum distance separable code. On the other hand, Reed-Solomon codes are not perfect codes. This can be seen by example, by taking $k = 3, n = 5$, and $q = 5$. Then $d = 3$ and

$$q^k\sum_{i = 0}^{\lfloor \frac{d-1}{2}\rfloor}\binom{n}{i}(q-1)^i = 5^3\cdot 21 = 2625$$

while

$$q^n = 5^5 = 3125.$$

The construction of Reed-Solomon codes is much simpler than that of the Hamming code, but uses more heavy machinery in its use of large finite fields and polynomials over those finite fields.

# Decoding

Let $C$ be the Reed-Solomon code with parameters $k\leq n\leq q$ and elements $a\_1,\ldots,a\_n\in \mathbb F\_q$ used to encode $C$. Since the minimal distance is $n-k + 1$, we can correct $\lfloor \frac{n-k}{2}\rfloor$ many errors. Let $\tilde{\boldsymbol{y}} \in \mathbb F\_q^n$ be an element that differs from a $\boldsymbol{y}\in C$ at $e\leq \lfloor \frac{n-k}{2}\rfloor$ places, so to decode, we need to determine $\boldsymbol{y}$ from $\tilde{\boldsymbol{y}}$. To do this, we introduce the peculiar notation $\tilde{\boldsymbol{y}} = (b\_1,b\_2,\ldots, b\_n)$; it will become clear momentarily why we do this. We have two vectors $(a\_1,\ldots,a\_n), (b\_1,\ldots,b\_n)\in\mathbb F\_q^n$ and we know there exists a polynomial $P(z)\in\mathbb F\_q[z]$ such that $P(a\_i) = b\_i$ for all but $e$ of the $a\_i$. If we can determine $P(z)$, then we can decode $\tilde{\boldsymbol{y}}$ since the original message is retrieved from the coefficients of $P(z)$.

To determine $P(z)$ we define what's called the error locator polynomial

$$E(z) = \prod_{\substack{a_i\text{ such that}\\ P(a_i)\not=b_i}}(z-a_i)\in \mathbb F_q[z],$$

which has the property that $E(a\_i) = 0$ if $P(a\_i)\not=b\_i$. Hence the name error locator polynomial. The error locator polynomial, $E(z)$, also has the property that

$$b_iE(a_i) = P(a_i)E(a_i)$$

for all $i$, since if $P(a\_i) = b\_i$ then $P(a\_i)E(a\_i) = b\_iE(a\_i)$ and if $P(a\_i)\not=b\_i$ then both sides of the equality are $0$.

Define $Q(z) = P(z)E(z)$. The polynomial $Q(z)$ satisfies $Q(a\_i) = b\_iE(a\_i)$ for all $i$, and is degree $e + k - 1$ since $E$ has degree $e$ and $P$ has degree $k-1$. Since we do not know $P(z)$, we also do not know $Q(z)$ and $E(z)$, but it is easier to solve for $Q(z)$ and $E(z)$, and then determine $P(z)$ as $P(z) = \frac{Q(z)}{E(z)}$. Let $Q(z)$ and $E(z)$ be generic degree $e + k - 1$ and $e$ polynomials, so their coefficients are the variables we will solve for:

$$Q(z) = \sum_{i = 0}^{e + k - 1} u_iz^i \text{ and }E(z) = \sum_{i=0}^ev_iz^i.$$

The equalities $Q(a\_i) = b\_iE(a\_i)$ yield equations

$$\begin{equation}\sum_{j = 0}^{e + k - 1}a_i^ju_j = \sum_{j=0}^eb_ia_i^jv_j.\end{equation}$$

This gives a linear system of $n$ equations with $e + k + e + 1 = 2e + k + 1$ unknowns $u\_0,\ldots,u\_{l + k-1},v\_0,\ldots,v\_e$, which we know has a solution. The solution may not be unique, but by the following proposition, any solution will do.

**Proposition** If $Q\_1,E\_1$ and $Q\_2,E\_2$ satisfy $Q\_j(a\_i) = b\_iE\_j(a\_i)$ for all $i$ and $j=1,2$, then $\frac{Q\_1}{E\_1} = \frac{Q\_2}{E\_2}$.

***proof:*** We have that $\frac{Q\_1}{E\_1} = \frac{Q\_2}{E\_2}$ if and only if $Q\_1E\_2 - Q\_2E\_1 = 0$. Let $R(z) = Q\_1(z)E\_2(z) - Q\_2(z) E\_1(z)$. The degree of $R$ is less than or equal to $e + k - 1 + e = 2e + k - 1$ which in turn is less than or equal to $n - k + k - 1 = n - 1 < n$. On the other hand, $R(a\_i) = 0$ for all $i = 1,2,\ldots,n$, so $R$ has $n$ distinct roots. Hence $R$ must be the zero polynomial.$\square$

Therefore to decode $\tilde{\boldsymbol{y}}$, we need to solve the equations (1) for the $u\_j$ and $v\_j$. A solution to this equation gives us a $Q(z)$ and $E(z)$ which we then determine $P(z)$ from via polynomial division. Solving the equations in (1) amounts to writing down the $n\times 2e + k$ matrix $\boldsymbol{A} = (a\_{ij})$ where

$$a_{ij} = \begin{cases} a_{i + 1}^j & \text{ for } 0\leq j\leq e+k-1\\ -a_{i + 1}^{j-e-k}b_{i+1} &\text{ for } e+k\leq j\leq 2e + k,\end{cases}$$

and finding a nonzero vector in the nullspace of $\boldsymbol{A}$.

# Programming Reed-Solomon Codes

The scripts for programming Reed-Solomon codes are found [here](https://github.com/Joe-Ferrara/CodingTheoryIntro). The scripts written contain the following:

* The same finite field class ``FpClass.py`` used for the Hamming code scripts.

* The same matrices class ``Matrices.py`` used for the Hamming code scripts.

* A polynomial class ``Polynomials.py`` which represents polynomials over and field $\mathbb F$ and has the following functionality: polynomial addition, subtraction, multiplication, and (floor, //) division.

* The same abstract linear code class ``LinearCode.py`` used for the Hamming code scripts.

* A Reed-Solomon code class ``ReedSolomonCode.py`` which is a subclass of the linear code class. The Reed-Solomon code class produces the Reed-Solomon code of parameters $k\leq n\leq q$ where $q$ is a prime and $a\_i = i-1\bmod q$. To produce this Reed-Solomon code, one inputs the parameters $k,n$, and $q$. If it is not true that $k\leq n\leq q$, then an exception is raised. The Reed-Solomon code class has the functionality of encoding vectors in $\mathbb F\_q^k$ and decoding vectors in $\mathbb F\_q^n$ when the vecotrs are stored as $1\times k$ or $1\times n$ matrices over $\mathbb F\_q$ respectively.

I tested the Reed-Solomon code scripts on the first three paragraphs of the novel *A Tale of Two Cities*, just as we did with the Hamming code. The script for the test is ``TaleOfTwoCitiesRSTest.py``. I used the Read-Solomon code with parameters $k = 154, n = 257$, and $q = 257$. With these parameters, we can encode the $256$ ASCII characters as elements of $\mathbb F\_{257}$ via the ord function in python. Since $k = 154$, we encode $154$ characters of *A Tale of Two Cities* at a time. This is a lot more than the Hamming code, where we encoded only $1$ character at a time. With these parameters, we can correct up to $51$ errors in an $\mathbb F\_{257}^{257}$-vector. This allows for an error rate of $51/257$ which is (after rounding) 20%. This seems to me like a substantial amount of errors to allow. As with the Hamming code, after each block of text was encoded, it was corrupted using the random package in python, and then decoded using the above algorithm. Thankfully, we got back the original text. The process took 9 minutes and 46 seconds.

# References

There are a lot of good references for coding theory. What I've written is all standard material that I learned from blogs or webpages for courses on coding theory. Here are a couple I found particularly useful:

* Jeremy Kun's blog, which is found at [jeremykun.com](https://jeremykun.com), and has a lot of good stuff on various topics. He wrote a series of posts on coding theory, the first of which is found [here](https://jeremykun.com/2015/02/16/a-proofless-introduction-to-information-theory/). His posts had a strong influence on what I've written.

* A course given at Central Michigan University during Srping 2010 by Venkatesan Guruswami is another great reference with a lot of information on coding theory and links to other sources of information on coding theory. There webpage of the course is [here](https://www.cs.cmu.edu/~venkatg/teaching/codingtheory/).
