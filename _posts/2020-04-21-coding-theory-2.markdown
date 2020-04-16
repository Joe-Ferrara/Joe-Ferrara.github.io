---
layout: post
title:  "Coding Theory: The Hamming Code"
---

# Parity Check Matrix

Before we get to the Hamming code, we need to introduce a few more general concepts. Let $C$ be an $(n,k,d)\_q$-code. To give an encoding function

$$E:\mathbb F_q^k\longrightarrow\mathbb F_q^n$$

for $C$ is to pick a basis for $C$. That is, let $\boldsymbol{v}\_1,\ldots,\boldsymbol{v}\_k$ be a basis for $C$ and let $\boldsymbol{E}$ be the matrix with rows $\boldsymbol{v}\_1,\ldots,\boldsymbol{v}\_k$. Then we define an encoding function for $C$ as $E(\boldsymbol{x}) = \boldsymbol{x}\boldsymbol{E}$ where $\boldsymbol{x}\boldsymbol{E}$ is matrix multiplication.

Another useful matrix to associate to $C$ is what's called a parity check matrix for $C$.

**Definition** Let $C$ be an $(n,k,d)\_q$ code. A **parity check matrix** for $C$ is an $n-k\times n$ matrix $\boldsymbol{F}$, such that $\boldsymbol{F}\boldsymbol{y} = \boldsymbol{0}$ if and only if $\boldsymbol{y}\in C$. A parity check matrix for $C$ checks whether or not an element $\boldsymbol{y}\in \mathbb F\_q^n$ is in $C$.

Parity check matrices always exist. Indeed, on $\mathbb F\_q^n$, we may consider the standard inner product: for $\boldsymbol{y} = (y\_1,\ldots, y\_n), \boldsymbol{z} = (z\_1,\ldots,z\_n)\in\mathbb F\_q^n$,

$$\boldsymbol{y}\cdot\boldsymbol{z} = \sum_{i = 1}^n y_iz_i.$$

Let $C^\perp$ be the orthogonal complement to $C$ with respect to this standard inner product. Then a parity check matrix for $C$ is defined by picking a basis for $C^\perp$ and setting that basis as the rows of $\boldsymbol{F}$.

Given a parity check matrix $\boldsymbol{F}$ for a code $C$, we can recover $C$ from $\boldsymbol{F}$ as the kernel of the linear map

$$\begin{array}{rcl} F:\mathbb F_q^n&\longrightarrow&\mathbb F_q^{n-k} \\ \boldsymbol{y} &\longmapsto &\boldsymbol{F}\boldsymbol{y}.\end{array}$$

Algorithmically, we may also produce an encoding function from $\boldsymbol{F}$ by row reducing $\boldsymbol{F}$ into row reduced echelon form, from which it is easy to write down a basis for the kernel of $F$.

# Construction of the Hamming Code

We use the notion of a parity check matrix to construct the Hamming code. Let $\boldsymbol{F}$ be a parity check matrix for a code $C$ with length $n$ and dimension $k$. For $1\leq i\leq n$, let $\boldsymbol{e}\_i$ be the $i$th standard basis vector, so $\boldsymbol{e}\_i$ has $0$ for every coordinate except for its $i$th coordinate where $\boldsymbol{e}\_i$ has a $1$. The scalar multiples of the standard basis vectors are the vectors in $\mathbb F\_q^n$ that have Hamming distance $1$ from the zero vector, $\boldsymbol{0}$. Since $\boldsymbol{0}\in C$ because $C$ is a linear subspace of $\mathbb F\_q^n$, in order for the minimum distance of $C$ to be greater than $0$ it must be the case that $\boldsymbol{e}\_i\not\in C$ for all $i$, which in terms of the parity check matrix says that $\boldsymbol{F}\boldsymbol{e}\_i\not=\boldsymbol{0}$ for all $i$. Since $\boldsymbol{F}\boldsymbol{e}\_i$ is the $i$th column of $\boldsymbol{F}$, this says that no column of $\boldsymbol{F}$ may be all zeros.

We can continue reasoning this way, giving conditions that $\boldsymbol{F}$ must satisfy in order to increase the minimum distance of $C$. The vectors in $\mathbb F\_q^n$ that have Hamming distance $2$ from the zero vector are vectors of the form $\alpha \boldsymbol{e}\_i + \beta\boldsymbol{e}\_j$ for $i\not= j$ and $\alpha,\beta\in\mathbb F\_q^n - \{\boldsymbol{0}\}$. Therefore in order for $C$ to have minimum distance greater than $2$ it must be the case that $\boldsymbol{F}(\alpha\boldsymbol{e}\_i + \beta\boldsymbol{e}\_j)\not=\boldsymbol{0}$, which is true if and only if $\boldsymbol{F}\boldsymbol{e}\_i \not= -\frac{\beta}{\alpha}\boldsymbol{F}\boldsymbol{e}\_j$. This is true if and only if the columns of $\boldsymbol{F}$ are all pairwise linearly independent.

In general, for $C$ to have minimum distance $d$, if must be the case that for any $I\subset \{1,\ldots,n\}$, $\|I\| = d-1$,

$$\boldsymbol{F}\left(\sum_{i\in I} \lambda_i\boldsymbol{e}_i\right)\not=\boldsymbol{0}$$

since the linear combinations $\sum\_{i\in I} \lambda\_i\boldsymbol{e}\_i$ are the vectors with Hamming distance less than $d$ from $\boldsymbol{0}$. This amounts to constructing an $\boldsymbol{F}$ such that any $d-1$ of the columns of $\boldsymbol{F}$ are linearly independent.

We note that since $\boldsymbol{F}$ is an $n-k\times n$ matrix, at most $n-k$ columns of $\boldsymbol{F}$ are linearly independent. If you construct an $n-k\times n$ matrix with this property, then the code $C$ would be an $(n, k, n-k + 1)$-code, which are exactly the codes that satisfy the Singleton bound.

We now focus on constructing the best $C$ of minimum distance $3$ by constructing a maximal $\boldsymbol{F}$ such that any two columns of $\boldsymbol{F}$ are linearly independent. To do this we fix $\ell = n-k$, the number of rows of $\boldsymbol{F}$. Then to pick the columns of $\boldsymbol{F}$, we write down all the vectors in $\mathbb F\_q^{\ell} - \{\boldsymbol{0}\}$ that have coordinates made up of only $0$'s and $1$'s. We put these as the columns of $\boldsymbol{F}$. We claim that any two columns of $\boldsymbol{F}$ are linearly independent. Indeed, consider two columns of $\boldsymbol{F}$. Either these two columns have the same number of nonzero coordinates or a different number of nonzero coordinates. If they have the same number of nonzero coordinates, then the nonzero coordinates must be in different places and so they are linearly independent. If they have a different number of nonzero coordinates and are both not the zero vector, then they are linearly independent.

Thinking of these vectors of length $\ell$ with coordinates $0$'s and $1$'s as subsets of $\\{1,\ldots, \ell\\}$ (a vector corresponds to a subset where the elements in the subset of the coordinates where the vector is $1$), we see that there are $2^\ell - 1$ vectors since we got every subset of $\\{1,\ldots, \ell\\}$ except for the empty set (which corresponds to the zero vector). Therefore $\boldsymbol{F}$, is an $\ell\times 2^\ell - 1$ matrix, and so determines an $(\ell, 2^\ell - 1, 3)\_q$-code $C$. We should check that $C$ does have minimum distance larger than $3$ since our arguments so far show that $C$ has minimum distance at least $3$. We do this by writing down a vector with three nonzero entries in the kernel of $\boldsymbol{F}$, which is not hard to do.

Let's now calculate how far from being perfect $C$ is. Writing down the Hamming bound with the parameters $()\ell, 2^\ell - 1, 3)\_q$ gives

$$\begin{array}{ll} \displaystyle q^k\sum_{i = 0}^{\lfloor \frac{d - 1}{2}\rfloor} \binom{n}{i}(q - 1)^i & \displaystyle= q^k\binom{n}{0} + q^k\binom{n}{1}(q-1)\\
										& = \displaystyle q^{2^\ell - \ell - 1}(1 + (2^\ell - 1)(q - 1))\\
										& \leq q^{2^\ell-1}.\end{array}$$

In general, $q^{2^\ell - \ell - 1}(1 + (2^\ell - 1)(q - 1))$ is less than $q^{2^{\ell} - 1}$, but if $q = 2$, we get

$$q^{2^\ell - \ell - 1}(1 + (2^\ell - 1)(q - 1)) = 2^{2^\ell - 1.}$$

Therefore if $q = 2$, this construction gives us a perfect code! This perfect code is known as the Hamming code. A nice property of this code, since $q = 2$, is that the columns of $\boldsymbol{F}$ are the binary digits of the numbers $1,2,\ldots, 2^\ell - 2, 2^\ell - 1$, though not necessarily in that order.

**Definition:** The **Hamming code** of parameter $\ell$, is the $(2^{2^\ell - 1}, 2^{2^\ell - 1 - \ell}, 3)\_2$-code which has parity check matrix with columns the binary digits of the numbers $1,2,\ldots, 2^{\ell} - 1$.

The Hamming code is an example of a perfect code, but if $\ell >1$, then the Hamming code is not an MDS code, since then $k + d = 2^{2^\ell - 1 - \ell} + 3 < 2^{2^\ell - 1} + 1 = n + 1$.

# Decoding the Hamming Code

Now the we have the Hamming code the question is how to decode it. In practice, a code is only as good as its decoding algorithm. As explained in the previous section, we can write down parity check matrices for codes with various minimum distances, but actually decoding a code defined by a certain parity matrix can be extremely difficult. Thankfully in the Hamming code case, there is a nice decoding algorithm.

For purposes of decoding the Hamming code it is useful to assume that the parity check matrix, $\boldsymbol{F}$, has columns ordered so that the $i$th column of $\boldsymbol{F}$ is the binary digits of $i$. Let $\boldsymbol{F}$ be the parity check matrix of the Hamming code of parameter $\ell$, with its columns ordered this way, and let $C = \ker(\boldsymbol{F})$ be the Hamming code. Let $\widetilde{\boldsymbol{y}}\in \mathbb{F}\_2^n$. Since $C$ is a perfect code of minimum distance $3$, either $\widetilde{\boldsymbol{y}}\in C$ of $\widetilde{\boldsymbol{y}}$ differs from an element $\boldsymbol{y}\in C$ at one coordinate. Assume that $\widetilde{\boldsymbol{y}}$ differs from $\boldsymbol{y}\in C$ at the $i$th coordinate. Then

$$\widetilde{\boldsymbol{y}} = \widetilde{\boldsymbol{y}} + \boldsymbol{e}_i,$$

and if we compute $\boldsymbol{F}\widetilde{\boldsymbol{y}}$, we get

$$\boldsymbol{F}\widetilde{\boldsymbol{y}} = \boldsymbol{F}\boldsymbol{y} + \boldsymbol{F}\boldsymbol{e}_i = \boldsymbol{F}\boldsymbol{e}_i$$

since $\boldsymbol{F}\boldsymbol{y} = \boldsymbol{0}$. Since $\boldsymbol{e}\_i$ is the $i$th standard basis vector, $\boldsymbol{F}\boldsymbol{e}\_i$ is the $i$th column of $\boldsymbol{F}$ which is by assumption the binary digits of $i$. Therefore by evaluating $\boldsymbol{F}\widetilde{\boldsymbol{y}}$ we can determine what $\boldsymbol{y}$ is.

The decoding algorithm is the following: Let $\widetilde{\boldsymbol{y}}\in \mathbb F\_2^n$. If $\boldsymbol{F}\widetilde{\boldsymbol{y}} = \boldsymbol{0}$, then define $D(\widetilde{\boldsymbol{y}}) = \widetilde{\boldsymbol{y}}$. Otherwise, for $i = 1, 2,\ldots, 2^\ell - 1$, if $\boldsymbol{F}\widetilde{\boldsymbol{y}} = \boldsymbol{F}\boldsymbol{e}\_i$, then $D(\widetilde{\boldsymbol{y}}) = \widetilde{\boldsymbol{y}} - \boldsymbol{e}\_i$.

# Programming the Hamming Code

The scripts for programming the Hamming code are found [here](https://github.com/Joe-Ferrara/CodingTheoryIntro). The scripts written contain the following:
* A finite field class ``FpClass.py`` that represents the finite field $\mathbb F\_q$ for $q$ a prime number. The scripts for the finite field class use techniques taken from Jeremy Kun (taken from [here](https://jeremykun.com/2014/03/13/programming-with-finite-fields/)) for writing classes of number types. The Hamming code uses the finite field class to represent the field $\mathbb F\_2$.

* A matrices class ``Matrices.py`` that represents matrices over any field $\mathbb F$. The matrices class has the following functionality: addition, subtraction, scalar multiplication, multiplication of matrices, determinants, row reduced echelon form, inversion, and writing down a basis of the nullspace of the matrix. For the Hamming code we use matrices over $\mathbb F\_2$.

* An abstract linear code class ``LinearCode.py`` with the following functionality: It produces the encoding matrix of a code given the parity matrix by row reducing the parity matrix and writing down a basis for its kernel, and an encoding function given the encoding matrix as well as a vector to encode.

* A Hamming code class ``HammingCode.py`` which is a subclass of the linear code class. The Hamming code class produces the Hamming code of parameter $\ell$ with parity check matrix $\boldsymbol{F}$, such that the $i$th column of $\boldsymbol{F}$ is the binary digits of $i$. To produce the Hamming code class, one inputs the parameter $\ell$. The Hamming code class has the functionality of encoding vectors in $\mathbb F\_2^k$ where $k = 2^{2^\ell - 1 - \ell}$ and decoding vectors in $\mathbb F\_q^n$ where $n = 2^{2^\ell - 1}$ when the vectors are stored as $1\times k$ or $1\times n$ matrices over $\mathbb F\_2$ respectively.


I tested the Hamming code scripts on the first three paragraphs of the novel *A Tale of Two Cities*.  The script for the test is ``TaleOfTwoCitiesHammingTest.py``. To do this, I used the Hamming code of parameter $\ell = 4$. Then the size of $C$ is $2^{11} = 256$. With this size, we can encode any ASCII characters by using the ord function in python and then converting the number to an element of $\mathbb F\_2^{11}$ via its binary digits. In this system, a message is a letter of the alphabet (or more generally any ASCII character). Once an element of $\mathbb F\_2^{11}$ is obtained, it is corrupted by using the random package in python to pick a coordinate to change. The decoding algorithm then decodes the corrupted vectors and translates them back to ASCII characters. After doing this, the script prints the decoded text which (thankfully) was the original *Tale of Two Cities* text. The process took 1.86 seconds.
