+++
title = "Generalizing exponentation laws"
date = 2022-10-07
description = "An exploration into some of the definitions we take for granted in mathematics, which in the process uncovers some interesting ideas, interesting-er proofs and more."

[extra]
math = true

[taxonomies]
tags = ["advanced", "math", "algebra", "arithmetic", "combinatorics"]
+++

*Note: This article, despite it's elementary nature, assumes some basic familiarity with sum notation, infinite sums, combinatorics ($n$ choose $k$) and logarithms*

First, you were taught basic arithmetic: counting, multiplying, dividing and such. Then, you learned the "rules" governing it.
Eventually, you learned about a fairly useful operation, known as exponentation. Exponentation, most would agree, is a very useful operation in Mathematics,
appearing everywhere from polynomials, to complex numbers, to number theory, combinatorics and more.
The most common definition of exponentation is as repeated multiplication. For instance, $2^4$ is $2 \times 2 \times 2 \times 2$. In "general":

$$x^n = \underbrace{x \times x \times \dots \times x \times x}_{\text{$n$ times}}$$

Alongside exponentation, students usually learn the exponentation laws, which are certain identities governing the operation.
These laws allow you for example, to simplify $2^3 \times 2^4$ into the much simpler $2^7$.

### The heros of this story
* Sum law: $a^b \times a^c = a^{b + c}$
* Evil sum law: $\frac{a^b}{a^c} = a^{b - c}$
* Product law: $(a^b)^c = a^{b \times c}$
* Distributive law: $(a \times b)^c = a^c \times b^c$
* Division law: $\frac{a^c}{b^c}=(\frac{a}{b})^c$
* ~~Commutative law: $a^b = b^a$~~
* ~~Associative law: $a^{(b^c)} = (a^b)^c$~~
* ~~Distributive law 2 - Electric Boogalo: $(a + b)^n = a^n + b^n$~~

Okay, those last ones aren't all that true, but the rest are absolutely fine. In most classes, they are also proved (kind of)!
For the sake of brevity, I won't show the usual proofs for all of them, but instead, give an example.

## A first attempt at a proof
Let's say we were trying to prove the sum law, how might we do it? We might first look back to the definition we gave exponentation, and continue. Basically:
$$a^b \times a^c = \underbrace{(a \times a \times \dots \times a \times a)}\_{\text{$b$ times}} \times \underbrace{(a \times a \times \dots \times a \times a)}_{\text{$c$ times}}$$

But look! There is no real separator between the two groups of products in here, so we should be able to say this equals:
$$\underbrace{a \times a \times \dots \times a \times a \times a \times a \times \dots \times a \times a}_{\text{$b + c$ times}}$$

Now notice again, by our original definition, this is the same as just writing $a^{b + c}$.
As required! Just like that, using some simple reasoning, we were able to prove a really useful identity!

## The troubles with non-natural powers
All of what we have seen is absolutely fine, but begins to break down once students start learning about non-natural powers.
The first problem, is that we haven't actually defined yet what it means to raise a number to a non-natural number.
The second one is that we still need to show our rules even hold for these non-natural powers (assuming they do at all).

This is where pedagogy fails, often neglecting to explain to students how non-natural powers work and why our laws here still work with them.
In this article however, we will tread where teachers dare not, and shed some lights on this problem. Before we proceed however, we should make some definitions.

## On the natural base, limits and $\exp(x)$
If we are going to define exponentation in any way, we should probably first look for a starting point, such as $e$.
It has many definitions, but one of the most common ones is as this infinite sum: $\sum_{n = 0}^{\infty} \frac{1}{n!}$.

Now that we have $e$, the next step is to acquire $e^x$, which is sometimes also written as $\exp(x)$. I will use this notation for the time being,
to clairify this is just a definition, not an "equality" or identity by the traditional sense.

Again, a common definition for $\exp(x)$, which is quite *natural* to use after our first definition for $e$ is $\sum_{n = 0}^{\infty} \frac{x^n}{n!}$.
Questions should immediately start popping up, such as:
"Is there a reason define $\exp(x)$ as such?", "Can we use $e$ to define all of exponentation?" and
"When are the other definitions (such as $\lim_{n \to \infty} (1 + \frac{1}{n})^n$) useful?".

As it turns out, the answer to the first two questions, is yes! The last however, is a bit out of scope for this article.
During the rest of this article, we will spend most of our time showing why this is the case. However, as you will see, it will be best to first show something more fundemental.

Before we do that though, you will have to know you about a very interesting technique, known as the "Cauchy product".
Briefly, the Cauchy product of two infinite, *convergent*, sums, $a$ and $b$ is:

$$(\sum_{i = 0}^\infty a_i)(\sum_{j = 0}^\infty b_j) = \sum_{k = 0}^\infty \sum_{l = 0}^k a_l b_{k - l}$$

"Wait, what? A sum of sums?" Indeed. This might look intimidating at first, so it might be worth it to take some time just to understand what is even being said here.

Ready for more? In the spirt of this post, we should probably prove this that this equality above is indeed true.

### The (highly informal) proof, to give you some intuition
Let us consider for a moment the distributive law for multiplication and addition:

$$a(b + c) = ab + ac$$

A more general version of it works for expressions of the form $(a_1 + a_2 + \dots + a_{n - 1} + a_n)(b_1 + b_2 + \dots + b_{n - 1} + b_n)$, and turns them into:

$$\sum_{i = 0}^n \sum_{j = 0}^n a_i b_j$$

An obvious idea now is to use something in the spirit of this identity, but this quickly fails, as we get a resulting sum that looks like
$\sum_{i = 0}^\infty \sum_{j = 0}^\infty a_i b_j$. Whilst this is not wrong, it is not useful to us, because each term of this new sum is actually a sum of infinitely many terms,
which is something we want to avoid, in order to be able to do more things later on. Despite this, our efforts will not be in vain,
because constructing the same terms seen in the distributive law, i.e: going over all all combinations,
is really the core of the Cauchy product (alongside compressing two infinite sums, two limits, into one).

With this in mind, we now have a clear goal of what we want to do. We want to show that no two combinations of elements from each series are the same
(and of course that we visit all combinations, although this is quite obvious and will not be shown here). As for how we show that, this turns out to be quite easy.

If we fix a particular value for $k$ (in the Cauchy Product, far above), then only $n$ can change, obviously. For every $n$, each second index, $n - k$ is also different.
Therefore, each choice of first index, $k$, yields a unique second index, for different $n$. Since $k$ cannot be the same value under the same $n$, this proves what we want.
And because of that, it proves the Cauchy product, as required.

### The fundemental property of $\exp(x)$
Do you remember the "fundemental" thing we talked about? I hope you do. It is known as the fundemental exponential identity,
which is the "sum law" for exponentation base $e$. To show it to be true, we will use the recently proven Cauchy product. Let's begin:

$$e^x e^y = (\sum_{i = 0}^\infty \frac{x^i}{i!})(\sum_{j = 0}^\infty \frac{x^j}{j!})$$

Now, by the Cauchy product, we get:

$$\sum_{n = 0}^\infty \sum_{k = 0}^n \frac{x^k y^{n - k}}{k!(n - k)!}$$

We are now very close to finishing the proof. Notice, that the inner sum here resembles quite closely the sum seen in the binomial theorem, except that the $n!$ term is missing.
Using this fact, we can transform this into:

$$\sum_{n = 0}^\infty \frac{1}{n!} \sum_{k = 0}^n \frac{n! x^k y^{n - k}}{k!(n - k)!}
= \sum_{n = 0}^\infty \frac{1}{n!} \sum_{k = 0}^n \binom{n}{k} x^k y^{n - k}
= \sum_{n = 0}^\infty \frac{(x + y)^n}{n!}$$

"Hang on...", you may be asking, "what is this binomial theorem thing, why should it be true?" That is fair enough,
as we are trying to be relatively elementary, I shouldn't expect you to know that. Let's prove it, quickly!

### A blazingly-fast Binomial theorem proof 
The binomial theorem states that when you have two numbers, $x$ and $y$, and some natural number $n$, the following is true:

$$(x + y)^n = \underbrace{xx \dots xx}\_{\text{$n$ times}} +
\underbrace{yx \dots xx}\_{\text{$n$ times}} +
\dots +
\underbrace{yy \dots yx}\_{\text{$n$ times}} +
\underbrace{yy \dots yy}\_{\text{$n$ times}} =
\sum_{k = 0}^n \binom{n}{k} x^k y^{n - k}$$

This is the case because as we have seen previously, a product of these same term-size sums is the same picking out all combinations of element products from these sums
(this is another generalization of the distributive law), e.g: $(1 + x)(1 + x)(1 + x)$ equals all of the ways to pick a single $x$ from these sums times that $x$,
two $x$s, now times $x^2$, three $x$s, times $x^3$ and of course, zero $x$s (technically, we were also picking ones, but they don't matter in our product). 

So what this theorem is is essentially fancy notation for: "all of the different ways to pick 0 $x$s and the remaining $y$s, plus all the ways to pick 1 $x$ and the remaining $y$s...".
We multiply the binomial coefficient ($n$ choose $k$) part with the product of the $x$s and $y$s because that's the same as adding up every single way to pick out these
collection of terms.

With that cleared, we can finish our original proof by rewriting the final expression to get:

$$\exp(x + y) = e^{x + y} = e^x e^y$$

By definition of $e^x$, and transitivity.

From this proof, we can actually answer question 1 for free, which asked why we defined $\exp(x)$ this way.
The reason is, because this the fundemental property of exponentation is then kept.
So $\exp(n)$, where $n$ is a natural number is just a product $e$s. $n$ of them to be exact.

Likewise, this proof, and one more definition, which answers question 2 will finally put us on track to prove all the exponentation laws.
This definition, is of general exponentation, which we have to define, otherwise identities such as ${(e^x)}^y = e^{xy}$ won't be proveable, because they aren't even defined.

## Real exponentation and the final stretch
Interestingly, the backbone of real exponentation is the logarithm. In this case, the natural one. Using it, we can define real exponentation as $e^{x \ln{b}}$.
This may make sense to you, if you remember your logarithm laws, but of course, these laws rely on the exponentation laws.
Despite this, it may be helpful to make sure this fits our common definition of $b^x$ where $x$ is natural.

If $x$ is natural, then this expression above is the same as $e^{\ln{b^x}}$, because $\ln x + \ln y  = \ln xy$ can be proved using the fundemental property of exponentation,
which we know to be true. Then, by the natural logarithm's definition we get $b^x$.

So indeed, when $x$ is natural, we get the expected result.

Can you feel the excitement? With this useful definition, we can finally begin proving the laws from the start, as we have all the tools we need.

### Product law
By our definition of real exponentation, and the definition of the natural logarithm, we get: $(a^b)^c = e^{c \ln {e ^{b \ln a}}} = e^{bc \ln a}$.
Finally, by our same exponentation definition we get: $a^{bc}$.

### Sum law
Proving the sum law is fairly simple as well. First, notice that: $a^b a^c = e^{b \ln a} e^{c \ln a}$.
Then, using our fundemental property of exponentation and the exponentation definition, we get: $e^{b \ln a + c \ln a} = e^{(b + c) \ln a} = a^{b + c}$.

### Evil sum law
In order to show the evil sum law. We must first do a tiny bit of algebra.

$$a^0 = a^{b - b} = a^b a^{-b} = 1 \iff a^{-b} = \frac{1}{a^b}$$

Note that this division is only valid because $a^b$ is always non-zero (assuming $a \neq 0$).
Using this, we can now prove the evil sum law: $\frac{a^b}{a^c} = a^b \frac{1}{a^c} = a^b a^{-c} = a^{b - c}$. As required.

### Distributive law
The distributive law is actually really similar to our sum law in the way we prove it. Just as last time, we will turn the two terms to their $e$ counterparts and continue from there:
$a^c b^c = e^{c \ln a} e^{c \ln b} = e^{c \ln a + c \ln b} = e^{c (\ln a + \ln b)}$.
Now, to finish, remember that logarithm law in start of this section? Let's use it: $e^{c \ln ab} = (ab)^c$. This ends our proof.

#### Divsion law
The division law is actually equivalent to our distributive law. I urge you to try and prove it yourself, as an exercise.

## What's next? What's next? What's N-X-E-T?
After quite the long journey, covering a variety of topics, an obvious thing to ask is, "what's next?".
Wether or not this article feels complete, theres plenty more to talk about, and do.
Maybe try creating a Cauchy product proof that's more formal and complete, and then see when the product doesn't actually hold.
Or maybe, go back to our $e$ definitions, learn about other ones and show they are all equivalent. Finally, try figuring out when exponentation, as described here, is in fact, undefined.
It might make you wonder why that's the case, and drive you to see how that effects the laws laid out in here.

I hope you can use this article as a jumping point, to learn about new topics, and that you appreciated this look into what might first appear as dull mathematics.
As mathematicians, even amateur ones, one of the most powerful things we can do is "think deeply of simple things", or in this case perhaps supposedly simple things,
and I hope this article gave you a glimpse of what it's like to really do that.
