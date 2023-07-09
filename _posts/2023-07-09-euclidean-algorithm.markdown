---
layout: post
title: "Euclidean Algorithm"
comment_issue_id: 21
sub: "none"
---

The Euclidean Algorithm is taught in elementary number theory and discrete math in college. It's simple enough to teach it to grade school students, where it is taught in number theory summer camps and I'd imagine in fancy grade schools. Even though it's incredibly simple, the ideas are very deep and get re-used in graduate math courses on number theory and abstract algebra. The importance of the Euclidean algorithm to elementary number theory is the role it plays in proving that an integer can be uniquely factored into prime numbers. In higher math that is usually only learned by people that study math in college, the Euclidean algorithm is used to prove that there exists unique prime factorization in other more complicated arithmetic systems than the integers. The Euclidean algorithm is also used to find multiplicative inverses in modular arithmetic. This has many applications to the real world in computer science and software engineering, where finding multiplicative inverses modulo some modulus is used in RSA and elliptic curve cryptography amongst other things. 

The Euclidean algorithm starts with the simple intuitive statement of the division algorithm.

**Division Algorithm**: Given positive integers $a,b \in \mathbb{N}$, with $b < a$ there exist nonnegative integers $q,r \in \mathbb{Z}_{\geq 0}$ such that

$$ a = bq + r $$

where $0 \leq r < b$.

The division algorithm says that given two positive integers you can divide the smaller one ($b$) into the larger one ($a$) with a remainder that's less than the smaller integer. To carry out the division algorithm you take multiples of the smaller integer, $b$, until you get a larger number than $a$, and then $qb$ is the multiple one less than that. The remainder, $r$, is whatever is left over between $a$ and $bq$, i.e.  $r = a - bq$.

With the division algorithm in hand, we can prove the Euclidean algorithm.

**Euclidean Algorithm**: Let $a,b \in \mathbb{N}$, with $b < a$ and let $r$ be the greatest common divisor of $a$ and $b$. Then there exists $x,y \in \mathbb{Z}$ such that

$$r = ax + by$$. 

Strictly speaking, the Euclidean algorithm is the algorithm used to prove the existence of $x$ and $y$ by giving an algorithm, the Euclidean algorithm, that starts with $a$ and $b$ then finds $r$ and then finds $x$ and $y$. In two sentences, the Euclidean algorithm consists of repeatedly applying the division algorithm to determine $r$. Then reversing the repeated division algorithm allows one to express $r$ in terms of $a$ and $b$ giving one an explicit algorithm for determining $x$ and $y$. Proving that the $r$ obtained by the Euclidean algorithm is truly the greatest common divisor of $a$ and $b$ takes a slight diversion in the form of a lemma.

Let's repeat the division algorithm a few times


$$
\begin{array}{ll} a = bq_0 + r_1 &r_1 < b \\
​                 b = r_1q_1 + r_2 &r_2 < r_1 \\
                  r_1 = r_2q_2 + r_3 &r_3 < r_2\end{array}
$$


where each time in the new division algorithm we replace the $b$ with the remainder and replace the $a$ with the $b$.  Generally speaking if we repeat this over and over, the pattern of the equations looks like


$$
\begin{array}{ll} r_{n-2} = r_{n-1}q_{n-1} + r_n &r_n < r_{n-1} \label{ref1}\tag{1} \\
                  r_{n-1} = r_n q_n + r_{n + 1} &r_{n + 1} < r_n  \end{array}
$$


for $n = 1$, when $a = r_{-1}$ and $b = r_0$, until $n$ gets large enough that the sequence of equations terminates. To see why the sequence of equations terminates, note that the sequence of $r_i$'s

$$a > b > r_1 > r_2 > r_3 \ldots $$

is a strictly decreasing sequence of nonnegative integers (remember in the division algorithm that $0 \leq r < b$). Any strictly decreasing sequence of nonnegative integers must eventually end with 0. In the Euclidean algorithm case, this means eventually we get $r_{N + 1} = 0$ for some $N$. The choice of $N$ here is so that $r_N$ is the last positive remainder. The last two steps of repeatedly applying the division algorithm are


$$
\begin{array}{ll} r_{N - 2} = r_{N - 1}q_{N - 1} + r_N &r_N < r_{N - 1} \label{ref2}\tag{2} \\ r_{N - 1} = r_N q_N \end{array}
$$


where $r_{N + 1}$ is not written because it's zero. 

Before we show that $r_N$ is the greatest common divisor of $a$ and $b$, let's see how we find $x, y \in \mathbb{Z}$ such that $r_N = ax + by$. If we look at the first equation in $(\ref{ref1})$ and solve for $r_{n+1}$ we get

$$r_{n+1} = -q_nr_n + r_{n-1},$$

which writes $r_{n+1}$ as a linear combination of $r_n$ and $r_{n-1}$. We then plug the first equation of ($\ref{ref1}$) into this equation by isolating $r_n$ in the first equation, giving

$$r_{n+1} = -q_n(r_{n-2} - r_{n-1}q_{n-1}) +r_{n-1}.$$

Carrying out the multiplication and rewriting the right hand side in terms of $r_{n-1}$ and $r_{n-2}$ gives

$$r_{n+1} = (1 + q_{n-1}q_n)r_{n-1}-q_nr_{n-2}$$.

This shows that we can inductively write $r_{n+1}$ as a linear combination of any $r_{i}$ and $r_{i +1}$ for $i<n$. Applying this to $r_N$ and going all the way to the beginning of the Euclidean algorithm gives $r_N$ as a linear combination of $a$ and $b$ (remember $a = r_{-1}$ and $b=r_0$) for some $x, y \in \mathbb{Z}$:

$$r_N = ax + by$$. The $x$ and $y$ are long expressions involving all the of the $q_i$'s.

This is the end of the story as far as explaining how to do and use the Euclidean algorithm to find the greatest common divisor, $r$, of $a$ and $b$ and to find $x$ and $y$ such that $r = ax + by$. To finish things up mathematically, we need to show that $r_N$ actually is the greatest common divisor of $a$ and $b$.

For this, we also use an inductive argument chaining together the steps of the Euclidean algorithm. We need the following lemma.

**Lemma**: If $a = bq + r$, then the greatest common divisor of $a$ and $b$ is the same as the greatest common divisor of $b$ and $r$.

To prove this lemma we show that the set of divisors of $a$ and $b$ is the same as the set of divisors of $b$ and $r$. If these two sets are the same, then greatest number in each of them is the same. To see why these two sets are the same, let $d$ divide $a$ and $b$. Then since $r = a -bq$, then $d$ divides $r$. Similarly if $d$ divides $r$ and $b$ then because $a = bq + r$ then $d$ divides $a$.

Back to the Euclidean algorithm. Let $\gcd(x, y)$ denote the greatest common divisor of two integers $x$ and $y$. The second equation of $(\ref{ref2})$ says that $r_N$ divides $r_{N-1}$ so $\gcd(r_N, r_{N-1}) = r_N$. We then apply the lemma in a chain up the equations in the Euclidean algorithm. For example the first equation of $(\ref{ref2})$ implies by the lemma that $\gcd(r_N, r_{N-1}) = \gcd(r_{N-1}, r_{N-2})$. We get a chain of equalities going all the way to $\gcd(a, b)$:

$$r_N = \gcd(r_N, r_{N-1}) = \gcd(r_{N-1}, r_{N-2}) = \ldots = \gcd(r_2, r_1) = \gcd(r_1, b) = \gcd(b, a),$$

which finishes the proof of the Euclidean algorithm.

In computer programming running the Euclidean algorithm to get $r$ is an efficient algorithm to find the greatest common divisor of $a$, and $b$. Further, given the equation

$$1 = ax + by$$

for $a$ and $b$ with greatest common divisor $1$, doing the Euclidean algorithm and then reversing it is an efficient algorithm to find a solution for $x$ and $y$. Let's see how this leads to finding multiplicative inverses in modular arithmetic. Let $a$ and $m$ be positive integers such that the greatest common divisor of $a$ and $m$ is $1$. Then by the Euclidean algorithm, there exist integers $x, y$ such that

$$1 = ax + my.$$

Rearranging this says that $ax - 1 = my$, which is the equation that says $ax \equiv 1 \bmod m$ or that $x$ is the multiplicative inverse of $a$ modulo $m$. Therefore when $a$ and $m$ have greatest common divisor $1$, then the Euclidean algorithm constructs a multiplicative inverse of $a$ modulo $m$. In fact the only integers that have multiplicative inverses modulo $m$ are those that have a greatest common divisor of $1$ with $m$. To quickly prove this, let $d$ be the greatest common divisor of $a$ and $m$ and assume that $a$ has a multiplicative inverse modulo $m$. Then there exists $x,y \in \mathbb{Z}$ such that $ax - 1 = my$ or $ax - my = 1$. Since $d$ divides $a$ and $m$, then by the equation $ax - my = 1$, $d$ divides $1$. The only divisor of $1$ is $1$, so $d=1$, saying that the greatest common divisor of $a$ and $m$ is $1$. Therefore, we've see that an integer $a$ has a multiplicative inverse modulo $m$ if and only if the greatest common divisor of $a$ and $m$ is $1$, and the Euclidean algorithm explicitly constructs the multiplicative inverse of $a$ modulo $m$. 
