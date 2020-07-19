---
layout: post
title: "Real Quadratic Fields: Units and Class Numbers"
comment_issue_id: 5
sub: "lfunctions"
---

Let $K = \mathbb Q(\sqrt{d})$ be a quadratic field and let $D$ be its discriminant. In my last post I analyzed the units of $K$ when $d < 0$ and used the formula for $L(\chi_D, 1)$ to calculate class numbers for $K$ when $\left\lvert d\right\rvert<100.$ In this post, I'll do the same analysis when $d > 0$.

In this case, the unit group $\mathscr O_K^\times$ is not finite and the formula for $h_K$ is

$$\begin{equation}h_K = \frac{L(\chi_D, 1)\sqrt{D}}{2\log(u_K)}\end{equation}$$

where $u_K$ is the fundamental unit of $K$ (which means $u_K$ generates $\mathscr O_K^\times/\mu(\mathscr O_K)$ as a $\mathbb Z$-module and $\left\lvert u_K\right\rvert > 1$). From last post, we know that if $d\equiv 2$ or $3\bmod 4$, then $\alpha + \beta\sqrt{d}\in\mathscr O_K$ is a unit if and only if $\alpha^2 - d\beta^2 = \pm 1$, and if $d\equiv 1\bmod 4$, then $\frac{1}{2}(\alpha + \beta\sqrt{d})\in \mathscr O_K$ is a unit if and only if $\alpha^2 - d\beta^2 = \pm 4$. Before I get into a more in depth discussion about $\mathscr O_K^\times$ and integer solutions to $x^2 - dy^2 = \pm 1$ and $x^2 - dy^2 = \pm 4$, let's look at an example.

# Example $K =\mathbb Q(\sqrt{2})$

To find the units in this example, we look for solutions to $x^2 - 2y^2 = \pm 1$. The first solution that does not yield $\pm 1\in\mathscr O_K^\times$ is $x = 1, y = 1$, which gives us $1 + \sqrt{2}\in \mathscr O_K^\times$. Three other solutions are $x = -1, y = -1$, $x = 1, y = -1$, and $x = -1, y = 1$ giving the elements $-1-\sqrt{2}$, $1 - \sqrt{2}$, and $-1 + \sqrt{2}$ in $\mathscr O_K^\times$. We have the relations

$$(1 + \sqrt{2})(-1 + \sqrt{2}) = 1 \text{   and   } (1 - \sqrt{2})(-1-\sqrt{2}) = 1,$$

which says that the multiplicative inverse of $1 + \sqrt{2}$ is $-1 + \sqrt{2}$ and the multiplicative inverse of $1 - \sqrt{2}$ is $-1-\sqrt{2}$.

Raising any of these four elements to positive powers gives families of solutions to $x^2 - 2y^2 = \pm 1$. You can see a few low power examples in the following tables.

| $1 + \sqrt{2}$ | $x^2 - 2y^2$ |
| --- | --- |
| $(1 + \sqrt{2})^2 = 3 + 2\sqrt{2}$ | $3^2 - 2\cdot 2^2 = 1$ |
| $(1 + \sqrt{2})^3 = 7 + 5\sqrt{2}$ | $7^2 - 2\cdot 5^2 = -1$ |
| $(1 + \sqrt{2})^4 = 17 + 12\sqrt{2}$ | $17^2 - 2\cdot 12^2 = 1$ |
| $(1 + \sqrt{2})^5 = 41 + 29\sqrt{2}$ | $41^2 - 2\cdot 29^2 = -1$ |

|$1 - \sqrt{2}$ | $x^2 - 2y^2$ |
| --- | ---|
|$(1 - \sqrt{2})^2 = 3 - 2\sqrt{2}$ | $3^2 - 2\cdot (-2)^2 = 1$|
|$(1 - \sqrt{2})^3 = 7 - 5\sqrt{2}$ | $7^2 - 2\cdot (-5)^2 = -1$ |
| $(1 - \sqrt{2})^4 = 17 - 12\sqrt{2}$ | $17^2 - 2\cdot (-12)^2 = 1$ |
| $(1 + \sqrt{2})^5 = 41 - 29\sqrt{2}$ | $41^2 - 2\cdot (-29)^2 = -1$ |

It turns out that $1 + \sqrt{2}$, $1 - \sqrt{2}$, $-1 + \sqrt{2}$, and $-1-\sqrt{2}$ are the four possible generators of $\mathscr O_K^\times/\\{\pm 1\\}$. Raising these elements to positive powers gives all the solutions to $x^2 - 2y^2 = \pm 1$. As can be seen in the table, the powers alternate between solutions to $x^2 - 2y^2 = 1$ and $x^2 - 2y^2 = -1$. Odd powers give all the solutions to $x^2 - 2y^2 = -1$, and even powers give all the solutions to $x^2 - 2y^2 = 1$.

# Generalities

To begin to discuss the general picture, I need to make some observations about nonzero real numbers and their multiplicative inverses. Let $u\in \mathbb R$, $u\not=0,1,-1$. Then $u^{-1} = 1/u\in\mathbb R$ and $u^{-1} \not= 0, 1, -1$. By definition of $u^{-1}$ we have the relation $uu^{-1} = 1$. This relation implies that either $u$ and $u^{-1}$ are both positive, or $u$ and $u^{-1}$ are both negative. If $u$ and $u^{-1}$ are both positive, then one must be greater than $1$ and the other one less than $1$. Similarly, if $u$ and $u^{-1}$ are both negative, then one is less than $-1$ and one is greater than $-1$.

Let's now see the implications of these observations for $\mathscr O_K^\times$. Let $u\in \mathscr O_K^\times$ be such that $u\not= 1, -1$. Then $u$ produces three other units $u^{-1}$, $-u$, and $-u^{-1}$ in $\mathscr O_K^\times$ ($-u$ and $-u^{-1}$ are units because $-u\cdot-u^{-1} = 1$). By the above remarks, of the four units $u$, $u^{-1}$, $-u$, and $-u^{-1}$ exactly one is greater than $1$. Now let $u$ be a generator of $\mathscr O_K^\times/\\{\pm 1\\}$. Then $u^{-1}$, $-u$, and $-u^{-1}$ also generate $\mathscr O_K^\times/\\{\pm1\\}$ and these are the four possible generators of $\mathscr O_K^\times/\\{\pm 1\\}$. We let $u_K$ be the generator that is larger than $1$, and call $u_K$ the fundamental unit of $K$.

Next let's get a little bit more explicit with the elements of $\mathscr O_K^\times$. I'll do the details for $d \equiv 2$ or $3\bmod 4$ and state what happens for $d\equiv 1\bmod 4$.

Assume $d \equiv 2$ or $3\bmod 4$. Let $\alpha + \beta\sqrt{d}\in\mathscr O_K$, so $\alpha,\beta\in \mathbb Z$. We define the *conjugate* of $\alpha + \beta\sqrt{d}$ as $\alpha - \beta\sqrt{d}$. The term conjugate comes from complex conjugation. If $d < 0$, then $\alpha - \beta\sqrt{d}$ is the complex conjugate of $\alpha + \beta\sqrt{d}$.

Let $x = \alpha$, $y = \beta$ be a solution to $x^2 - dy^2 = \pm 1$, and assume $\alpha,\beta > 0$. Given a solution to $x^2- dy^2 = \pm 1$, we can always find a solution $x = \alpha$, $y = \beta$ with $\alpha,\beta > 0$ because $x = -\alpha$, $y = -\beta$, $x = \alpha$, $y = -\beta$, and $x = -\alpha$, $y = \beta$ are also solutions to $x^2 - dy^2 = \pm 1$. These four solutions correspond to the four elements

$$\alpha + \beta\sqrt{d}, \text{ } -\alpha - \beta\sqrt{d}, \text{ } \alpha - \beta\sqrt{d}, \text{ } -\alpha + \beta\sqrt{d}$$

of $\mathscr O_K^\times$. If we multiply $\alpha + \beta\sqrt{d}$ by its conjugate, we get

$$(\alpha + \beta\sqrt{d})(\alpha - \beta\sqrt{d}) = \alpha^2 - d\beta^2 = \pm1,$$

so the multiplicative inverse of $\alpha + \beta\sqrt{d}$ is either $\alpha - \beta\sqrt{d}$ or $-\alpha + \beta\sqrt{d}$. This shows that the four elements

$$\alpha + \beta\sqrt{d}, \text{ } -\alpha - \beta\sqrt{d}, \text{ } \alpha - \beta\sqrt{d}, \text{ } -\alpha + \beta\sqrt{d}$$

are an example of a quadruple $u, u^{-1}, -u, -u^{-1}$ (though not in the same order).

If we start raising any of these four elements to powers, then the absolute values of the new coefficients of $1$ and $\sqrt{d}$ are all the same and they grow in absolute value for each new power. For example:

|$\alpha + \beta\sqrt{d}$ |
| --- |
| $(\alpha + \beta\sqrt{d})^2 = \alpha^2 + \beta^2d + 2\alpha\beta\sqrt{d}$|
|$(\alpha + \beta\sqrt{d})^3 = \alpha^3 + 3\alpha\beta^2d + (\beta^3d + 3\alpha^2\beta)\sqrt{d}$|

| $\alpha - \beta\sqrt{d}$ |
|  --- |
| $(\alpha - \beta\sqrt{d})^2 = \alpha^2 + \beta^2d - 2\alpha\beta\sqrt{d}$ |
| $(\alpha - \beta\sqrt{d})^3 = \alpha^3 + 3\alpha\beta^2d - (\beta^3d + 3\alpha^2\beta)\sqrt{d}$ |

In general, if $\alpha,\beta > 0$ and $a,b$ are either $1$ or $0$, then using the binomial theorem we have

$$((-1)^a\alpha + (-1)^b\beta\sqrt{d})^n = \sum_{i = 0}^n\binom{n}{i}(-1)^{ai + b(n-i)}\alpha^i\beta^{n-i}(\sqrt{d})^{n-i}.$$

Grouping the terms with $\sqrt{d}$ and without $\sqrt{d}$ gives

$$((-1)^a\alpha + (-1)^b\beta\sqrt{d})^n = (-1)^{na}\sum_{i\equiv n\bmod 2}\binom{n}{i}\alpha^i\beta^{n-i}d^{(n-i)/2} + $$

$$ + (-1)^{a(n-1) + b}\left(\sum_{i\equiv n-1\bmod 2}\binom{n}{i}\alpha^i\beta^{n-i}d^{(n-1-i)/2}\right)\sqrt{d}.$$

The point of this calculation here, is that the terms in the sum are the same no matter what $a$ and $b$ are, and those terms are getting larger as $n$ gets larger. We conclude from this that the fundamental unit of $K$ is $\alpha + \beta\sqrt{d}$, where $x = \alpha$, $y = \beta$ is the minimal positive integer solution to $x^2 - dy^2 = \pm 1$.

When $d\equiv 1\bmod 4$ we can make the same arguments and conclude that the fundamental unit of $K$ is $\frac{1}{2}(\alpha + \beta\sqrt{d})$ where $x = \alpha, y = \beta$ is the minimal positive integer solution to $x^2 - dy^2 = \pm 4$.

The last thing to address in general before calculating class groups is the difference between solutions to $x^2 - dy^2 = 1$ and $x^2 - dy^2 = -1$ (and between $x^2 - dy^2 = 4$ and $x^y - dy^2 = -4$). If $u\in \mathscr O_K^\times$ corresponds to a solution to $x^2 - dy^2 = -1$ or $-4$, then as is seen in the example of $\mathbb Q(\sqrt{2})$, the odd powers of $u$ will correspond to solutions to $x^2 - dy^2 = -1$ or $-4$ and the even powers of $u$ will correspond to solutions to $x^2 - dy^2 = 1$ or $4$. On the other hand, if $u$ corresponds to a solution to $x^2 - dy^2 = 1$ or $4$, then all of the powers of $u$ correspond to solutions to $x^2 - dy^2 = 1$ or $4$. In general, if the fundamental unit corresponds to a solution to $x^2 - dy^2 = -1$ or $-4$, then we'll say that the fundamental unit has sign $-1$. In this case, there are solutions to both the equations $x^2 - dy^2 = 1$ and $x^2 - dy^2 = -1$ when $d\equiv 2$ or $3\bmod 4$ and $x^2 - dy^2 = 4$ and $x^2 - dy^2 = -4$ when $d\equiv 1\bmod 4$. When the fundamental unit corresponds to a solution to $x^2 - dy^2 = 1$ or $4$,  then we'll say that the fundamental units has sign $1$. In this case, there are no solutions to the equation $x^2 - dy^2 = -1$ when $d\equiv 2$ or $3\bmod 4$ or $x^2 - dy^2 = -4$ when $d\equiv 1\bmod 4$.

# Real Quadratic Class Numbers

In order to use (1) to calculate class numbers, the main difficulty lies in calculating the fundamental unit $u_K$. One way to do this is to search the positive integers for the minimal positive solution to $x^2 - dy^2 = \pm 1$ or $x^2 - dy^2 = \pm 4$. This works, but there is a more efficient way to find the minimal solution that uses something called continued fractions. I won't get into what continued fractions are, but want to mention that in the code I wrote to calculate the fundamental unit of a real quadratic field, I use continued fractions to find the minimal solution to $x^2 - dy^2 = \pm 1$ or $\pm 4$.

The code used for these calculates is found [here](https://github.com/Joe-Ferrara/IntroToLfunctions). The script ``fundamental_unit.py`` has the continued fraction algorithm, as well as the algorithm to determine the fundamental unit using continued fractions. The interested read can find the math details of this in Rosen's number theory book which I put in as a reference below. I reference the specific theorems and pages used from Rosen's book in ``fundamental_unit.py``. The script ``real_quad_class_numbers.py`` uses ``fundamental_unit.py`` and ``quad_Lfunctions.py`` to calculate class numbers. Once the fundamental unit is determined, this is straitfowrad and the same as was done in my previous post.

In the following table I've recorded the fundamental unit, sign of the fundamental unit, and class number for real quadratic fields with $d < 100$.

| d | Fundamental Unit of $\mathbb Q(\sqrt{d})$ | Sign | Class Number of $\mathbb Q(\sqrt{d})$ |
| --- | --- | --- | --- |
| $2$ | $1 + \sqrt{2}$ | $-1$ | $1$ |
| $3$ | $2 + \sqrt{3}$ | $1$ | $1$ |
| $5$ | $\frac{1}{2}(1 + \sqrt{5})$ | $-1$ | $1$ |
| $6$ | $5 + 2\sqrt{6}$ | $1$ | $1$ |
| $7$ | $8 + 3\sqrt{7}$ | $1$ | $1$ |
| $10$ | $3 + \sqrt{10}$ | $-1$ | $2$ |
| $11$ | $10 + 3\sqrt{11}$ | $1$ | $1$ |
| $13$ | $\frac{1}{2}(3 + \sqrt{13})$ | $-1$ | $1$ |
| $14$ | $15 + 4\sqrt{14}$ | $1$ | $1$ |
| $15$ | $4 + \sqrt{15}$ | $1$ | $2$ |
| $17$ | $\frac{1}{2}(8 + 2\sqrt{17})$ | $-1$ | $1$ |
| $19$ | $170 + 39\sqrt{19}$ | $1$ | $1$ |
| $21$ | $\frac{1}{2}(5 + \sqrt{21})$ | $1$ | $1$ |
| $22$ | $197 + 42\sqrt{22}$ | $1$ | $1$ |
| $23$ | $24 + 5\sqrt{23}$ | $1$ | $1$ |
| $26$ | $5 + \sqrt{26}$ | $-1$ | $2$ |
| $29$ | $\frac{1}{2}(5 + \sqrt{29})$ | $-1$ | $1$ |
| $30$ | $11 + 2\sqrt{30}$ | $1$ | $2$ |
| $31$ | $1520 + 273\sqrt{31}$ | $1$ | $1$ |
| $33$ | $\frac{1}{2}(46 + 8\sqrt{33})$ | $1$ | $1$ |
| $34$ | $35 + 6\sqrt{34}$ | $1$ | $2$ |
| $35$ | $6 + \sqrt{35}$ | $1$ | $2$ |
| $37$ | $\frac{1}{2}(12 + 2\sqrt{37})$ | $-1$ | $1$ |
| $38$ | $37 + 6\sqrt{38}$ | $1$ | $1$ |
| $39$ | $25 + 4\sqrt{39}$ | $1$ | $2$ |
| $41$ | $\frac{1}{2}(64 + 10\sqrt{41})$ | $-1$ | $1$ |
| $42$ | $13 + 2\sqrt{42}$ | $1$ | $2$ |
| $43$ | $3482 + 531\sqrt{43}$ | $1$ | $1$ |
| $46$ | $24335 + 3588\sqrt{46}$ | $1$ | $1$ |
| $47$ | $48 + 7\sqrt{47}$ | $1$ | $1$ |
| $51$ | $50 + 7\sqrt{51}$ | $1$ | $2$ |
| $53$ | $\frac{1}{2}(7 + \sqrt{53})$ | $-1$ | $1$ |
| $55$ | $89 + 12\sqrt{55}$ | $1$ | $2$ |
| $57$ | $\frac{1}{2}(302 + 40\sqrt{57})$ | $1$ | $1$ |
| $58$ | $99 + 13\sqrt{58}$ | $-1$ | $2$ |
| $59$ | $530 + 69\sqrt{59}$ | $1$ | $1$ |
| $61$ | $\frac{1}{2}(39 + 5\sqrt{61})$ | $-1$ | $1$ |
| $62$ | $63 + 8\sqrt{62}$ | $1$ | $1$ |
| $65$ | $\frac{1}{2}(16 + 2\sqrt{65})$ | $-1$ | $2$ |
| $66$ | $65 + 8\sqrt{66}$ | $1$ | $2$ |
| $67$ | $48842 + 5967\sqrt{67}$ | $1$ | $1$ |
| $69$ | $\frac{1}{2}(25 + 3\sqrt{69})$ | $1$ | $1$ |
| $70$ | $251 + 30\sqrt{70}$ | $1$ | $2$ |
| $71$ | $3480 + 413\sqrt{71}$ | $1$ | $1$ |
| $73$ | $\frac{1}{2}(2136 + 250\sqrt{73})$ | $-1$ | $1$ |
| $74$ | $43 + 5\sqrt{74}$ | $-1$ | $2$ |
| $77$ | $\frac{1}{2}(9 + \sqrt{77})$ | $1$ | $1$ |
| $78$ | $53 + 6\sqrt{78}$ | $1$ | $2$ |
| $79$ | $80 + 9\sqrt{79}$ | $1$ | $3$ |
| $82$ | $9 + \sqrt{82}$ | $-1$ | $4$ |
| $83$ | $82 + 9\sqrt{83}$ | $1$ | $1$ |
| $85$ | $\frac{1}{2}(9 + \sqrt{85})$ | $-1$ | $2$ |
| $86$ | $10405 + 1122\sqrt{86}$ | $1$ | $1$ |
| $87$ | $28 + 3\sqrt{87}$ | $1$ | $2$ |
| $89$ | $\frac{1}{2}(1000 + 106\sqrt{89})$ | $-1$ | $1$ |
| $91$ | $1574 + 165\sqrt{91}$ | $1$ | $2$ |
| $93$ | $\frac{1}{2}(29 + 3\sqrt{93})$ | $1$ | $1$ |
| $94$ | $2143295 + 221064\sqrt{94}$ | $1$ | $1$ |
| $95$ | $39 + 4\sqrt{95}$ | $1$ | $2$ |
| $97$ | $\frac{1}{2}(11208 + 1138\sqrt{97})$ | $-1$ | $1$ |

# Open Problems

If you compare this table with the table for imaginary quadratic fields, you'll notice that their are way more real quadratic fields with class number $1$, and that class numbers do not grow with $\left \lvert d\right\rvert$ at the same rate for real quadratic fields as for imaginary quadratic fields. In fact, there are fundamentally different behaviors for real and imaginary quadratic fields.

It is conjectured (and people generally believe) that there are infinitely many real quadratic fields with class number one. This is an open problem in number theory that no one knows how to prove. A more refined question is, "Given a class number, what percentage of real quadratic fields have that class number?" For imaginary quadratic fields, the answer is 0 for any class number since for any class number there are only finitely many imaginary quadratic fields with that class number. In the real quadratic case there are conjectures, known as the Cohen-Lenstra heuristics, that predict the percentage of real quadratic fields with a given class number.

The equation $x^2 - dy^2 = 1$ is known as Pell's equation, and it's solutions have been studied and understood going back to 1700s. The equations $x^2 - dy^2 = \pm 4$ and $x^2 - dy^2 = -1$ are known as generalized Pell equations. As we vary $d$, the solutions to $x^2 - dy^2 = -1$ and $x^2 - dy^2 = -4$ are less well understood than the solutions to $x^2 - dy^2 = 1$ and $x^2 - dy^2 = 4$. As we've seen, for any squarefree integer $d \equiv 2$ or $3\bmod 4$, there are integer solutions to $x^2 - dy^2 = 1$, and for any squarefree integer $d\equiv 1\bmod 4$, there are integer solutions to $x^2 - dy^2 = 4$. On the other hand there may or may not be solutions to $x^2 - dy^2 = -1$ when $d\equiv 2$ or $3\bmod 4$, or to $x^2 -dy^2 = -4$ when $d\equiv 1\bmod 4$. It is an open problem to determine the percentage of $d\equiv 2$ or $3\bmod 4$ for which $x^2 - dy^2 = -1$ has a solution, and to determine the percentage of $d\equiv 1\bmod 4$ for which $x^2 - dy^2 = -4$ has a solution.

# What Brought Us Here

At the beginning of my posts on $L$-functions, I motivated their study by saying that they are used to determine whether number systems other than $\mathbb Z$ have a fundamental theorem of arithmetic. Since then I've introduced the number systems known as quadratic fields, and we've calculated an invariant (the class number), that measures how far the number system is from having a fundamental theorem of arithmetic. In doing this, I've hoped to convey that this is an interesting application of special values of $L$-functions.

Up until this point I've tried to keep these posts as elementary as possible. All the mathematics I've written about was known to Gauss and Dirichlet in the 1800s. In my next and last (for now) post on $L$-functions, I'd like to say something about the research in my thesis. In order to do this, I'll have to cover over 200 years of math, so the math will unfortunately  get much more technical.

# Reference

K. H. Rosen, *Elementary Number Theory and Its Applications*, 5th Edition. Pearson/Addison Wesley, 2005.
