---
layout: post
title:  "Coding Theory: Introduction"
comment_issue_id: 7
---

During my postdoc, I've done research involving the mathematical objects called Drinfeld modules ([wiki](https://en.wikipedia.org/wiki/Drinfeld_module), [general reference](http://www-math.mit.edu/~poonen/papers/drinfeld.pdf) explaining their importance in the context of more well known number theory). Upon learning about Drinfeld modules, I learned that they have a theoretical application to the very practical area of math known as coding theory. (Warning: in coding theory the word code does not mean the same thing as in computer science.) Interested in learning practical math that's applied using computer science, I decided to learn exactly how Drinfeld modules are used in coding theory in hopes of programming codes that use Drinfeld modules.

It turns out that programming codes that use Drinfeld modules is a bit more complicated than I initially hoped. While possible, these codes require a lot of technical mathematics groundwork be programmed, and so I've decided to put off that goal for now.

On the other hand, while learning the basics of coding theory I did program two canonical examples of codes, the Hamming codes and Reed-Solomon codes. This post and my following two posts are write ups that build coding theory from the ground up in order to understand the scripts I wrote for Hamming codes and Reed-Solomon codes which can be found [here](https://github.com/Joe-Ferrara/CodingTheoryIntro).

In writing the posts, I've assumed the reader is familiar with linear algebra over finite fields (one only really needs to be familiar with linear algebra over the prime field $\mathbb F_p = \mathbb Z/p\mathbb Z$), and for the Reed-Solomon codes post, polynomials over finite fields. Otherwise, everything is fleshed out and explained. In this first, post I lay the mathematical framework of coding theory.

# Motivation

Suppose you are communicating through an unstable channel where when you send information, the information is corrupted and changed in some way. Coding theory tries to determine under these circumstances the best way to encode the information and send it through the channel such that after corruption the original information can be recovered.

For example, say that you want to send a message that consists of letters, and you know that no matter what letters you send through the channel, one in every three letters is changed. One way to encode the message would be to send every letter twice. Upon receiving the message, one can tell with high probability which letters were changed because they would be the pairs of letters sent that do not match. An issue with this scheme is that it is not clear what the correct letter is when the two letters do not match. To correct this, you could send each letter three times. Now for each triplet of letters, two are the same and one is different, so you know that the two letters that are the same give you the letter in the original message.

The natural question arises: Depending on the likelihood of error in the transmitted message, what is the most efficient way to transmit a message such that after being corrupted the original message can still be recovered? Coding theory answers this question by formalizing the set up into a mathematical framework and using techniques from various areas of mathematics.

# Formalized Setup

Assume person A has a message, $\boldsymbol{x}$, consisting of $k$ bits of information. For our purposes, "bit" is the word we are using to denote one piece of information. A bit conceivably could be a letter, a number, or the usual meaning of $0$ or $1$. Say person $A$ encodes the $k$-bit message, $\boldsymbol{x}$, into an $n$-bit message, $\boldsymbol{y}$, and sends $\boldsymbol{y}$ to person B. During transmission, $\boldsymbol{y}$ is changed to the $n$-bit message $\widetilde{\boldsymbol{y}}$. The question is, given parameters on the number of errors in $\widetilde{\boldsymbol{y}}$, what's the best (meaning most efficient) way to encode $\boldsymbol{x}$ to $\boldsymbol{y}$ such that person B can determine $\boldsymbol{y}$ from $\widetilde{\boldsymbol{y}}$?

From here, there are two ways to phrase how errors occur, which lead to slightly different practical answers to the question. The first is the probabilistic setup. In the probabilistic setup we assume that each bit of $\boldsymbol{y}$ has a certain probability, $p$, of being changed. The second setup is the deterministic setup, where for a fixed $e$, we assume that $\widetilde{\boldsymbol{y}}$ differs from $\boldsymbol{y}$ at, at most $e$ places. The deterministic setup was introduced by Hamming after theoretical but not practical progress was made in the probabilistic setup.

I will focus on the deterministic setup because it has concrete solutions in the form of specific codes that can be described and programmed. The probabilistic setup seemingly is what occurs in real life problems. Given the probabilistic setup, one can choose $n$ and $e$ in the deterministic setup so that a solution to the deterministic set up will work most of the time for the given probabilistic setup.

# Mathematical Definitions and Notions

Let $q$ be a power of a prime number $p$ and let $\mathbb{F}_q$ be the finite field with $q$-elements.

**Definitions**
* A **(linear) code**, $C$, is a subspace $C\subset \mathbb{F}_q^n$ for some $n$.
* The **length** (or **block length**) of $C$ is $n$. The **dimension** of $C$ is $\log_q\|C\|$, which is the dimension of $C$ as an $\mathbb{F}_q$-vector space. The dimension of $C$ is denoted by the letter $k$.
* The **alphabet** of $C$ is $\mathbb{F}_q$, and so the size of the alphabet is $q$.
* Let $C$ be a code and let $k$ be the dimension of $C$. An injective linear function $E:\mathbb{F}_q^k\rightarrow \mathbb{F}_q^n$ with image $C$ is called an **encoding function** for $C$.

Let's relate these definitions to the Formalized Setup section. A bit is an element of $\mathbb{F}_q$. If $q=2$, then this is the usual notion of a bit. A message, $\boldsymbol{x}$, is an element of $\mathbb{F}_q^k$. If $E$ is an encoding function, then $\boldsymbol{y} = E(\boldsymbol{x})$ is the message with $n$ bits that is sent from person A to person B. Assume that during transmission, the message $\boldsymbol{y}$ is corrupted in at most $e$ places. This means that $\widetilde{\boldsymbol{y}}$ differs from $\boldsymbol{y}$ at at most $e$ coordinates. Since $E$ is injecture, if we can determine $\boldsymbol{y}$ from $\widetilde{\boldsymbol{y}}$, then we can determine $\boldsymbol{x}$ from $\boldsymbol{y}$ using $E$.

Let $C\subset\mathbb{F}_q^n$ be a code. An $e$-**decoding function** is a function $D:\mathbb{F}_q^n\rightarrow \mathbb{F}_q^n$ such that if $\widetilde{\boldsymbol{y}}\in F_q^n$ differs from a $\boldsymbol{y}\in C$ in at most $e$ places, then $D(\widetilde{\boldsymbol{y}}) = \boldsymbol{y}$. We note that such a $D$ is absolutely not linear. This notion of how to decode, motivates the definition of the Hamming distance.

**Definition**: Define the following norm on $\mathbb{F}_q^n$:

$$\|(y_1,\ldots,y_n)\| = |\{y_i : y_i\not=0\}|.$$

The norm of a $\boldsymbol{y}\in\mathbb{F}_q^n$ is the number of coordinates of $\boldsymbol{y}$ that differ from $0$. This defines a norm of $\mathbb{F}_q^n$, which in turn defines a distance function on $\mathbb{F}_q^n$ known as the **Hamming distance**. The Hamming distance between two points $\boldsymbol{y},\boldsymbol{y'}\in\mathbb{F}_q^n$ is the number of coordinates where $\boldsymbol{y}$ and $\boldsymbol{y'}$ differ.

Let's consider what a closed ball of radius $r$, where $0\leq r\leq n$ and $r\in\mathbb Z$, with respect to this metric looks like:

$$\begin{array}{rl}B_r(\boldsymbol{y}) &=\text{  }\{\widetilde{\boldsymbol{y}}\in\mathbb{F}_q^n: \|\widetilde{\boldsymbol{y}} - \boldsymbol{y}\| \leq r\}\\
							&=\text{  }\{\widetilde{\boldsymbol{y}}\in\mathbb{F}_q^n : \widetilde{\boldsymbol{y}} \text{ differs from }\boldsymbol{y}\text{ at at most }r\text{ places}\}.\end{array}$$

If we know for each encoded $\boldsymbol{y} = E(\boldsymbol{x})$ that $\boldsymbol{y}$ will be changed at at most $e$ coordinates during transmission, then the possible $\widetilde{\boldsymbol{y}}$'s that result from $\boldsymbol{y}$ being corrupted is $B_e(\boldsymbol{y})$.

Let $C$ be a code in $\mathbb{F}_q^n$. We now have a condition on $C$ that must be satisfied in order for an $e$-decoding function for $C$ to exist. If an $e$-decoding function for $C$ exists, then it must be the case that for all $\boldsymbol{y}, \boldsymbol{y'}\in C$, $\boldsymbol{y}\not=\boldsymbol{y'}$, the intersection of $B_e(\boldsymbol{y})$ and $B_e(\boldsymbol{y'})$ is empty. This is actually an if and only if statement. Conversely, if for all $\boldsymbol{y},\boldsymbol{y'}\in C$, $\boldsymbol{y}\not=\boldsymbol{y'}$, $B_e(\boldsymbol{y})\cap B_e(\boldsymbol{y'}) = \emptyset$, then we define an $e$-decoding function by sending each $B_e(\boldsymbol{y})$ to $\boldsymbol{y}$ and any point not in a $B_e(\boldsymbol{y})$ for $\boldsymbol{y}\in C$ anywhere we want. This function is well defined precisely because for $\boldsymbol{y},\boldsymbol{y'}\in C$, $\boldsymbol{y}\not=\boldsymbol{y'}$, $B_e(\boldsymbol{y})\cap B_e(\boldsymbol{y'}) = \emptyset$. In order to start with a code $C$ and determine the maximum $e$ for which an $e$-decoding function exists for $C$ we introduce the minimum distance of $C$.

**Definition**: Let $C\subset \mathbb{F}_q^n$ be a code. The **minimum distance** of $C$ is

$$\min_{\boldsymbol{y}, \boldsymbol{y'}\in C}\|\boldsymbol{y} - \boldsymbol{y'}\|.$$

Since $C$ is a subspace of $\mathbb F_q^n$, this the the same as $\displaystyle\min_{\boldsymbol{y}\in C}\\|\boldsymbol{y}\\|$.

Let $C$ be a code in $\mathbb{F}_q^n$, let $d$ be its minimal distance, and let $\boldsymbol{y}, \boldsymbol{y'}\in C, \boldsymbol{y}\not=\boldsymbol{y'}$. Then by definition of minimum distance,

$$\|\boldsymbol{y} - \boldsymbol{y'}\| \geq d.$$

On the other hand, for any $e$,

$$B_e(\boldsymbol{y})\cap B_e(\boldsymbol{y'}) = \emptyset \text{ if and only if } \|\boldsymbol{y} - \boldsymbol{y'}\| > 2e.$$

Therefore, there exists an $e$-decoding function for $C$ if and only if $2e < d$, and since $e$ is a whole number, this is if and only if $e \leq \lfloor \frac{d-1}{2} \rfloor$.

We now have the four most important invariants of a code. Given a code $C\subset \mathbb{F}_q^n$ of dimension $k$ and minimum distance $d$, we say that $C$ is an $(n, k, d)\_q$-code. If $C$ is an $(n,k,d)\_q$-code, then there exists an $e$-decoding function for $C$ if and only if $e \leq \lfloor\frac{d-1}{2}\rfloor$.

Given $C$, we now ask "how optimally $C$ is spaced out in $\mathbb{F}\_q^n$ if $C$ has minimal distance $d$?" We know that if $\boldsymbol{y}, \boldsymbol{y'}\in C$, $\boldsymbol{y}\not=\boldsymbol{y'}$, then $\|\boldsymbol{y} - \boldsymbol{y'}\| \geq d$, which implies that $B_{\lfloor \frac{d-1}{2}\rfloor}(\boldsymbol{y})\cap B_{\lfloor\frac{d-1}{2}\rfloor}(\boldsymbol{y'}) = \emptyset$. Then $C$ is optimally spaced out if

$$\bigcup_{\boldsymbol{y}\in C}B_{\lfloor \frac{d-1}{2}\rfloor}(\boldsymbol{y})$$

is as large as possible because then the wasted space in $\mathbb{F}_q^n$ is minimal. Since $\|\mathbb F_q^n\| = q^n$, the largest the above union can be is $q^n$.

For a given $r\in\mathbb Z$, $0\leq r\leq n$ and $\boldsymbol{y}\in\mathbb{F}_q^n$, let's determine how large $B_r(\boldsymbol{y})$ is. Each ball of radius $r$ has the same size, and the size of $B_r(\boldsymbol{y})$ is easiest to calculate when $\boldsymbol{y}$ is the zero vector, so we assume $\boldsymbol{y} = \boldsymbol{0} = (0,0,\ldots,0)$. Then $\boldsymbol{z}\in B_r(\boldsymbol{0})$ if and only if $\boldsymbol{z}$ differs from zero at at most $r$ coordinates. Counting all of these $\boldsymbol{z}$'s we see that $\boldsymbol{z}$ could differ from $\boldsymbol{0}$ at $0,1,2,\ldots, \text{ or } r$ coordinates. For $i$, $0\leq i\leq r$ there are $\binom{n}{i}(q-1)^i$ vectors which differ from $\boldsymbol{0}$ at exactly $i$ coordinates. Explanation: there are $\binom{n}{i}$ ways to choose the $i$ nonzero coordinates, and for each nonzero coordinates that are $q-1 = \|\mathbb{F}_q - \{\boldsymbol{0}\}\|$ choices for the coordinate. Therefore for $\boldsymbol{y}\in \mathbb{F}\_q^n$,

$$\begin{equation}|B_r(\boldsymbol{y})| = |B_r(0)| = \sum_{i = 0}^r\binom{n}{i}(q-1)^i.\end{equation}$$

(1) and the fact that $\|C\| = q^n$ tells us that if $C$ is an $(n,k,d)\_q$-code, then

$$\begin{equation}\left| \bigcup_{\boldsymbol{y}\in C}B_{\lfloor \frac{d-1}{2}\rfloor}(\boldsymbol{y})\right| = q^k\sum_{i = 0}^{\lfloor\frac{d-1}{2}\rfloor}\binom{n}{i}(q-1)^i\leq q^n,\end{equation}$$

and so $C$ is most optiomally spaced out if the above sum equals $q^n$. The inequality (2) is known as the the **Hamming bound**.

**Definition** Let $C$ be an $(n,k,d)\_q$ code. Then $C$ is said to be a **perfect code** if

$$q^k\sum_{i = 0}^{\lfloor\frac{d-1}{2}\rfloor}\binom{n}{i}(q-1)^i= q^n.$$

That is, a code is perfect if the Hamming bound inequality is an equality.


Let $C$ be an $(n,k,d)\_q$-code. Intuitively and by the above bound, there is a trade off between $k$ and $d$ with respect to $n$. If $n$ is fixed, the larger $k$ is, the smaller $d$ must be and vice-versa.

The Singleton bound is another bound that displays this property.

**Proposition**:(Singleton bound) Let $C$ be an $(n,k,d)\_q$-code. Then $k + d \leq n + 1$.

***proof:*** Consider the subspace

$$H = \{(y_1,y_2,\ldots,y_n)\in\mathbb{F}_q^n : y_1 = y_2 = \cdots = y_{n - d + 1} = 0\}.$$

Then $H$ is a $(d-1)$-dimensional subspace of $\mathbb{F}_q^n$. We claim that $H\cap C = \{0\}$. Then $\dim C + \dim H = k + d - 1 \leq n$ which proves the proposition. Let $\boldsymbol{y}\in H\cap C$. If $\boldsymbol{y}\not=0$, then $\boldsymbol{y}$ must differ from $0$ at at least $d$ coordinates since $d$ is the minimum distance of $C$ and $0\in C$. Then $\boldsymbol{y}$ is not in $H$, since elements of $H$ differ from $\boldsymbol{0}$ at at most $d-1$ places. Hence we have a contradiction so $\boldsymbol{y} = \boldsymbol{0}$. $\square$

A code that meets the Singleton bound is known as a **maximum distance separable** (MDS) code.

Let $C$ be an $(n, k, d)\_q$-code. We now have two different bounds on $\|C\| = q^k$. The Hamming bound tells use that

$$q^k \leq q^n/\left(\displaystyle \sum_{i = 0}^{\lfloor\frac{d-1}{2}\rfloor}\binom{n}{i}(q-1)^i\right),$$

and the Singleton bound tells us that

$$q^k\leq q^{n + 1 - d}.$$

These two bounds are independent in the sense that there exists and we will see examples of codes that satisfy the Hamming bound (perfect codes) but do not satisfy the Singleton bound, and codes that satisfy the Singleton bound (MDS codes) but do not satisfy the Hamming bound.

This concludes my introduction to the mathematical basics of the framework of coding theory. In my next two posts, we'll see two specific families of codes in practice.
