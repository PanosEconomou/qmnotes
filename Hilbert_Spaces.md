# Hilbert Spaces

The time has come. What is a Hilbert space? What happens when a Hilbert space becomes Infinite dimensional? Here we will answer these questions and give some cool physics consequences.

[toc]



# Abstract Definition

We have developed some intuition about Hilbert spaces through our toy examples like the qubit $\mathcal H= \mathbb{C}^2$, the qutrit $\mathcal{H} = \mathbb{C}^3$ and so on. But leaving the comfy land of finite dimensional examples behind we can uncover something much cooler.

## Definitions of Vector Spaces

Let’s start with an abstract definition of a vector space. Please don’t close this tab! I will explain what it means intuitively right after. 

**<u>Definition:</u>** A **vector space** over a field $\mathbb{K}$ (either the real numbers $\mathbb{K} = \mathbb{R}$, or the complex numbers $\mathbb{K} = \mathbb{C}$) is a set $V$ with two operations:

1. **Vector Addition:** A map $+:V\times V \to V$ such that $(u,v) \in V\times \mapsto u+v \in V$ 
2. **Scalar Multiplication:** A map $\cdot:\mathbb{K}\times V \to V$ such that $(a,v) \in \mathbb{K}\times V \mapsto a\cdot v = av \in V$,

 Such that they follow the properties below for any vectors $v,u,w \in V$ and any scalars $a,b \in \mathbb{K}$

1. **Associativity of Addition:** $v+(u+w) = (v+u)+w = v+u+w$
2. **Commutativity of Addition:** $v+u = u+v$
3. **Additive Identity:** There exists $0\in V$ such that $u+0 = u$ for any $u\in V$
4. **Additive Inverses:** For any $u\in V$ there exists an element $-u \in V$ such that $u+(-u) = 0$. 
5. **Compatibility of Multiplication:** $a(bv) = (ab)v$. 
6. **Multiplicative Identity:** for $1\in \mathbb{K}$ we have that $1\cdot v = v$ for any $v\in V$
7. **Distributivity of Multiplication:** $a(v+u) = av+au$
8. **Distributivity of Scalar Addition:** $(a+b)v = av+bv$.

Also the elements of a vector space are called **vectors**.



PHEW! So this was long but here is what it really means: **A vector space is a set $V$ where I can add vectors as I expect, and multiply them by the numbers in a set $\mathbb{K}$ as I expect**. That’s all! It’s the setting of scalar and vector multiplication. 

*At no point we talked about dimension or finite or infinite dimensions etc.* Meaning that as long as I can add and multiply as I expect, the vector space doesn’t care about dimension. 

Here are some examples.

**<u>Example:</u>** *(Complex Vector Spaces)* Any cartesian product of the complex numbers forms a vector space. For example $\mathbb{C}^k$ is a vector space of dimension $k \in \mathbb{N}$, where each vector can be multiplied by complex numbers. 

**<u>Example:</u>** *(Space of Functions)* Consider a set $S$ and all the functions that map to the complex plane $f:S\to \mathbb{C}$. The mathematical notation for such a space is $\mathbb{C}^S$ (which looks backwards, I know). $\mathbb{C}^S$ is a vector space with the following addition and multiplication operations:

1. **Poitnwise Addition:** Take any two vectors $f,g:S\to \mathbb{C}$ (or functions in this case), then we can create the vector $f+g$ such that for any $x\in S$ 
   $$
   (f+g)(x) = f(x) + g(x).
   $$
   This completely defines a function $f+g : S\to \mathbb{C}$ and thus an element of $\mathbb{C}^S$. 

2. **Pointwise Scalar Multiplication:** Let $f:S\to \mathbb{C}$ be any vector and $c\in \mathbb{C}$ be a scalar. Then we define the vector $cf$ to be the function such that for any $x \in S$ 
   $$
   (cf)(x) = cf(x).
   $$
   This is another vector in $\mathbb{C}^S$! 

It is easy to show that these operations follow the rules for a vector space, and we didn’t need to talk about arrows, nor dimension to do it! Now we have a vector space where each of the elments can be though of both as an arrow and as a function.

> **<u>Exercise:</u>** Show that if $S=\{-1,1\}$ then the vector space $\mathbb{C}^S$ is the same as $\mathbb{C}^2$. Can you come up with a general formula for the vector space $\mathbb{C}^S$ where $S$ is a *finite set* (i.e. $|S| = n \in \mathbb{N}$)?

**<u>Example:</u>** *(Polynomials)* A complex polynomial on some variable $x \in \mathbb{C}$ is a function of the form
$$
p(x) =p_0 + p_1x + p_2x^2 +\cdots = \sum_{k=0}^\infty p_k x^k,
$$
where all the $p_k \in \mathbb{C}$ are some (possibly zero) complex numbers. The set of all complex polynomials with the addition and multiplication described above is still a vector space!

**<u>Example:</u>** *(Meaning)* Yes! It is possible to describe a vector space where each point is a sentence. We can add sentences together by concatenating them and multiplying them by a number could denote the intensity by which they are pronounced. As a result, we have created a vector space where certain areas are aggressive, because all the vectors in that region represet aggressive sentences that are pronounced loudly, or about quantum mechanics and so on. While this might seem way too abstract to think about, it is super useful in machine learning! That’s how LLMs find how to respond to your question. Each of your questions is a vector, and the LLM is looking for vectors *nearby* to spit out to you as answer! 



## Length and Perpendicularity

Already in some of the examples mentioned above I used words like *‘nearby’* which imply some notion of closesness. What does it mean for a vector to be close or perpendicular to another? With our current definition of a vector space it means nothing. 

To be able to make judgements such as a vector is “close” or “bigger” than another we need to have to **introduce extra structure.** These structures are known as norms and inner producs, and their definitions are given below. 

**<u>Definition:</u>** A **norm** (also known as a metric) on a vector space $V$ over a field $\mathbb{K}$ (either real or complex numbers) is a map $||\cdot|| : V\to \mathbb{R}$ such that for any vectors $v,w\in V$ and any scalars $a \in \mathbb{K}$ the following is true

1. **Absolute Homogeneity:** $||av|| = |a|\cdot ||v||$
2. **Positive Definiteness:** $||v|| \geq 0$ and $||v|| = 0 \iff v = 0$
3. **Triangle Inequality:** $|| v + u || \leq ||v|| + ||u||$.

A vector space $V$ with a norm $||\cdot ||$ is known as a **normed space**.



Intuitively a norm is simply a way to extract a quantity that behaves similarly to length. In quantum mechanics we have seen a norm that instead of length, means probability. This is the same thing.

However, using a norm we can talk about **how close** two vectors are. In other words the vectors $v,w \in V$ are close, in a particular norm, if the length of there differece is small, i.e. $||v-w||$ is small. So a norm, doesn’t only give us a notion of lenght, it also gives us a notion of closeness!

What about a notion of perpendicularity, or orthogonality if you’re Greek?

**<u>Definition:</u>** An **inner product** on a vector space $V$ over a field $\mathbb{K}$ is a map $\langle \cdot, \cdot \rangle : V\times V \to \mathbb{K}$ such that the following are true for any $v,u,w \in V$ abd $a,b \in \mathbb{K}$

1. **Conjugate Symmetry:** $\langle u,v\rangle = {\langle v,u\rangle}^\ast$ 
2. **Linearity in the Second Argument:** $\langle w, au+bv\rangle = a\langle w,u\rangle + b\langle w,v\rangle$.
3. **Positive Definiteness:** $\langle v,v\rangle \geq 0$ and $\langle v,v\rangle = 0 \iff v = 0$.

A vector space $V$ with an inner product $\langle\cdot,\cdot\rangle$ is known as an **inner product space**. Two vectors such that $\langle u,v\rangle = 0$ are called **orthogonal**. 



**<u>Example:</u>** For real vector spaces a common inner product is the dot product that when it is combined with the traditional way of measuring length it has the property that for any two vectors $v,u \in V$ then
$$
v\cdot u = ||v|| \cdot ||u|| \cos\theta,
$$
where $\theta$ is interpreted as the angle in between the vectors. So in a sense, adding an inner product gave us a notion of angle! This makes sense, because an angle is a great way to measure perpendicularity.

**<u>Example:</u>** *(Special Relativity)* Einstein discovered that light must move with the same speed for all observers, In other words, light rays must remain perpendicular in any reference frame. This required a way to redefine orthogonality hence he got rid of the Eucledian inner product and its notion of orthogonality, and added a new inner product in spacetime that preserved the angles of light rays across reference frames. 

This ended up being the following inner product. For any two vectors $u,v \in \mathbb{R}^2$, their inner product is now 
$$
\langle u,v\rangle = -u_1v_1 + u_2v_2.
$$
 Which is the same as the Eucledian one, but with a negative sign on the first component. 

**<u>Example:</u>** *(Perpendicularity in QM)* In Quantum Mechanics we also introduced a notion of orthogonality in the Hilbert space using an inner product. But that orthogonality was not about angles, but about probability. We called two states orthogonal, if there was no probability that one state could collapse to the other!

> **Summary:** Norms give a notion of length to the hilbert space, and inner products a sense of orthogonality.

A vector space that has both is known as a **normed inner product space**. One important distinction we have to make, is that the notions of length and orthogonality are independent of each other. All the examples we have seen use an inner product to define a lenght, but that doesn’t have to be the case. 



## Hilbert Spaces

A Hilbert space is a place that combines both a notion of length and orthogonality but with some extra spice. In particular, having a notion of lenght can help us define sequences where each term gets ‘closer and closer’ to each other. If you have seen anything in real analysis is that this is dangerous! You can follow a sequence that ends up limiting outside your space! 

Here is an example. Consider a the following sequence
$$
S = \left\{\left(1 + \frac{1}{n}\right)^n\right\}_{n=1}^\infty.
$$
This sequence limits to $e$ which is an irrational number. However, every one of its terms is rational. So we have a sequence of rational numebers that the limit falls out of the rational numbers! That can totally happen to our vector space. Therefore, we would like to think of vector spaces where this doesn’t happen at all. 

With that, we can **finally** introduce a Hilbert space.

**<u>Definition:</u>** A **Hilbert space** $\mathcal{H}$ over a field $\mathbb{K}$ is a normed inner product space, with inner product $\langle \cdot,\cdot\rangle : \mathcal{H}\times \mathcal{H} \to \mathbb{K}$ and norm given by $||v|| = \sqrt{\langle v,v\rangle}$ for any $v \in \mathcal{H}$ such that any convergent sequence of elements of $\mathcal{H}$ converges in $\mathcal{H}$.

In quantum physics we also assume that there exists a *countable* basis (this is not necessarily implied by the above definition, but we will never see an example where it isn’t). Such Hilbert spaces are formally called **separable**. 

> **<u>Intuition:</u>** The intuition for a Hilbert space, is a *nice* vector space equipped with a notion of orthogonality and a compatible notion of length in such a way that you can follow sequences to your heart’s contempt and never fall outside of it. 

Here are some examples. 

**<u>Example:</u>** *(Qubit)* The complex vector space $\mathbb{C}^2$ with the Hermitian inner product $\langle \cdot, \cdot \rangle : \C ^2 \times \mathbb{C}^2 \to \mathbb{C}$ is a Hilbert space.

**<u>Example:</u>** *(Hermiatian Spaces)* Similarly any complex vector space $\mathbb{C}^k$ for $k\in \mathbb{N}$ with the same Hermitian inner product is a Hilbert space.

**<u>Example:</u>** *(Eucledian Spaces)* The space $\mathbb{R}^k$ for $k\in \mathbb{N}$ with the Eucledian inner product is a Hilbert space. 

**<u>Example:</u>** *(The Set of Square Integrable Functions)* Consider the set of functions $f: \mathbb R^k \to \mathbb C$ where $k\in \mathbb{N}$. As we have seen before they form a vector space with pointwise addition and scalar multiplication. Now let’s restrict our attention to the functions that have the property that
$$
\int_{\mathbb{R}^k} f(x) f^\ast(x) dx < \infty,
$$
i.e. their square integral is finite. These functions are called square **integrable** and the set of all square integrable functions from $\mathbb{R}^k \to \mathbb{C}$ is often denoted as $\mathcal{L}^2(\mathbb{R}^k,\mathbb{C})$ or $\mathcal{L}^2$ when the context is not ambiguous. We can see that with addition and scalar multiplication  $\mathcal{L}^2$ is still a vector space. In fact is is a vector subspace of the bigger vector space of all functions $\mathbb{C}^{(\mathbb{R}^k)}$. The cool thing is that we can introduce an inner product in $\mathcal{L}^2$ and turn it into a vector space! The inner product is given for any two square integrable functions by $f,g : \mathbb{R}^k \to \mathbb{C}$ as
$$
\langle f,g\rangle \coloneqq \int_{\mathbb{R}^k} f^\ast(x) g(x) dx.
$$
This is often called the $\mathcal{L}^2$**-inner product**. One can verify that this is indeed an inner product with all the requirements to convert $\mathcal{L}^2$ to a Hilbert space.

**<u>Example:</u>** *(Polynomials in a Bounded Domain)* Say one considers the set of polynomials $p(x)$ where $x\in [-1,1]$. Together with the inner product defined above, they also form a Hilbert space!



An interesting example is the hilbert space of wavefunctions on a line. 

**<u>Example</u>** *(Particle on a Line)* We know that a wavefunction of a single is a function $\psi:\mathbb{R}\to \mathbb{C}$ such that 
$$
\int_{\mathbb{R}}\psi^\ast (x) \psi(x)dx < \infty,
$$
or in other words such that it is normalizable. We see here that normalizable means square integrable! As we saw in the previous examples, all normalizable wavefunctions must form a hilbert space under the $\mathcal{L}^2$ inner product! So this is the Hilbert space of a particle in a line. 

Ok enough examples, it is time to actually play with them. 



# Linear Maps

We have already seen linear maps from 100 different points of view when it comes to finite dimensional vector spaces. We saw how they can be represented by matrices, how changing a basis gives us a different matrix, eigenvalues, eigenvectors,  determinants, and so on. Here we will play with them, but in the context of Hilbert spaces where dimensions can be infinite, and bases hard to understand. 

## Bases of Hilbert Spaces

Let’s start by thinking of bases. Anyway, if we know a basis, we can always define any linear map by how it acts on this basis. Let’s start with the difference between a spanning set and a basis.

**<u>Definition:</u>** A **spanning set** $B \subset \mathcal{H}$ is a subset of a Hilbert space $\mathcal{H}$ such that every vector can be written as a linear combination of the vectors in $B$. If for every finite subset $S \subset B$ the vectors in $S$ are linearly independent, then we call $B$ a **linearly independent spanning set** or a **basis**.

If a basis $B$ is finite then we call $\mathcal{H}$ a **finite dimesnional Hilbert space** with dimension $|B|$ (i.e. the number of vectors in the basis).

Finite bases behave as you might expect, but infinite bases can be much weirder. 

**<u>Example:</u>** *(Basis for Single Particle Hilbert Space)* Let’s consider again the Hilbert space of a single particle trapped in an interval $[0,2\pi] \subset \mathbb{R}$ given in the example above. One obvious basis we could pick is the states $\{\ket{x}\}_{x \in [0,2\pi]}$ that are defined by their inner product with any other state to give the value
$$
\braket{\psi}{x} = \psi(x).
$$
These do form a basis, because they are orthogonal to each other, but they are not countable! There is 1 such state for each real number in $[0,2\pi]$. However, we could find a countable basis for $\mathcal{H}$. We know that each wavefunction can be written in terms of Fourier modes! So we can pick the following basis
$$
\{\ket{n} = e^{inx}\}_{n \in \mathbb{Z}}.
$$
This is a basis since each of these is orthogonal to each other (by the properties we have already discussed) and we know that each wavefunction has a Fourier expansion! In ther words any wavefunction can be written uniquely as 
$$
\ket{\psi} = \sum_{n\in \mathbb{Z}} c_n e^{inx} =  \sum_{n\in \mathbb{Z}} c_n \ket{n}. 
$$
This basis, unlike the other one is tooootally countable. This means that we have found two qualitatively very different bases for our Hilbert space. This is quite an interesting result. We will use it a lot in a sec. 



## Operators

Linear maps, or some times called *Operators*, in Hilbert spaces are defined identically to Operators in vector spaces. 

**<u>Defintion:</u>** A **linear map** or **operator** between two Hilbert spaces $\mathcal{H}$ and $\mathcal{G}$ over a common field $\mathbb{K}$ is a map $A:\mathcal{H} \to \mathcal{G}$ such that for any two vectors $f,g \in \mathcal{H}$ and any two scalars $a,b \in \mathbb{K}$ the following is true
$$
A(af+bg) = aA(f) + bA(g).
$$
**<u>Notation:</u>** We often drop the parenthesis to write $A(f) = Af$, just like any linear operator. 



Before we talk about some caveats let’s talk about interesting examples.

**<u>Example:</u>** *(Linear Differential Operators)* Any ordinary linear differential operator
$$
L = \sum_{k\in \mathbb{N}} a_k \frac{d^k }{d x^k},
$$
is a linear map in the Hilbert space of square integrable smooth functions. 

This is really cool! We can now port all of our intuition for solving equations involving matrices in finite dimensional vector spaces, to solving differential equations using the language of Hilbert spaces!

The obvious caveat here is that there is no matrix notion for an operator acting on an infinite dimensional Hilbert space. So we have to be a bit more creative. Yet our intuition still holds!



## Adjoints and Hermitian Operators

Since there isn’t a matrix representation of operators acting on infinite dimensional vector spaces, how can we even define the *transpose conjugate*? This is what we called an adjoint and we said that Hermitian operators are the self adjoint ones. Let’s see the trick to extend these defintions.

**<u>Definition:</u>** Let $A:\mathcal{H}\to \mathcal{H}$ be an operator in Hilbert space $\mathcal{H}$ over a field $\mathbb{K}$ with inner product $\langle \cdot, \cdot\rangle : \mathcal{H}\times \mathcal{H} \to \mathbb{K}$, then the **adjoint** of $A$ is an operator $A^\dagger : \mathcal{H}\to \mathcal{H}$ such that for any $f,g \in \mathcal{H}$ 
$$
\langle f,Ag\rangle = \langle A^\dagger f,g\rangle.
$$
Such an operator is called **Hermitian** if $A = A^\dagger$. 

So in essense, an Adjoint is the version of the operator that acts from the left side of the inner product. 

The theorems that we know about Hermitian operators are still true. For example one can still find a basis for a Hilbert space using orthonormal eigenvectors of a Hermitian operator.

**<u>Example:</u>** *(Orthonormal Basis)* Consider the basis of the 1 particle Hilbert space described above as $\ket{x}$. The operator $\hat x:\mathcal{H} \to \mathcal{H}$ is a hermitian operator and it acts by pointwise multiplication. In particular the vector $\hat x\ket{\psi}$ is the function 
$$
\phi(x) = x\psi(x),
$$
for any $x \in \mathbb{R}$. The vectors $\ket{x}$ are eigenvectors of the operator $\hat x$, and as we can see they form an orthonormal basis. 







