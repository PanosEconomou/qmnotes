# Differential Equations for Quantum Mechanics

Before we phrase quantum mechanics more elegantly using the language of Linear Algebra, we need to understand how it works under the hood! We will do this using Ordinary and Partial Differential equations. These notes contain an accumulation of relevant results (and some proofs) for being able to talk comfortably about wavefunctions, the Schrodinger equation, eigenfunctions and so on. 

[toc]



# Ordinary Differential Equations

At the end of the day, in physics, we only ask one question:

> I am *here*, where will I be *then*?

This is a really hard question to form precisely. Sometimes *'here'* is fully described by some coordinates in $\mathbb R^n$, sometimes it is described by complicated mathematical objects that rotate slower than one would like. No matter the object the way we choose to describe evolution is by telling you where to go next. Mathematically, we express is as a condition that involves rates of change. These conditions that involve differential operators are called differential equations.



## Terminology

To that end here is some terminology 

**<u>Definition:</u>** Let $u : U\subset \mathbb R^n \to \mathbb R^m$ for some $n,m \in \mathbb N$. We say that $u$ is **smooth** iff all its partial derivatives are defined and are continuous. The **set of smooth functions** from $U\to \mathbb R^m$ is denoted by $C^\infty(U,\mathbb R^m)$. In the case where $m=1$ we often write $C^\infty(U)$ instead of $C^\infty(U,\mathbb R)$. 

Ok, why introduce smooth functions? Because when we take derivatives we take derivatives of smooth functions! This will allow us to define a differential operator as a map that takes a smooth function and spits out another smooth function.

**<u>Definition:</u>** A **linear ordinary differential operator** $L$ of order $n \in \mathbb N$ on $\mathbb R$ is a linear map $L:C^\infty(\mathbb R) \to C^\infty(\mathbb R)$ such that for any function $u\in C^\infty(U)$, i.e. a smooth function $u:\mathbb R\to \mathbb R$ is mapped to:
$$
Lu = \sum_{k=0}^n a_k \cdot \frac{d^ku}{dx^k}.
$$
where $a_k \in C^\infty(\mathbb R)$ are some other smooth functions on $\mathbb R$. If $a_k$ is constant for all $k$ then we say that $L$ has **constant coefficients**. If the operator takes in complex valued functions and output complex valued functions is called **complex.** A linear ordinary differential operator is called **non-degenerate** if $a_n$ does not vanish anywhere.

**<u>Notation:</u>** We often write
$$
L = \sum_{k=0}^n a_k \frac{d^k}{dx^k}.
$$
to denote the differential operator.

**<u>Example:</u>** Here is a list of examples

1. **The first derivative:** The first derivative is the ordinary differential operator $\frac{d}{dx}$. 

2. **The $k^{\text{th}}$ derivative:** It is given by the following operator $\frac{d^k}{dx^k}$.

3. **The Kinetic energy operator:** We will use it in quantum mechanics super soon, and is usually denoted by
   $$
   T= -\frac{m}{2} \frac{d^2}{dx^2}.
   $$

4. **The Cauchy-Euler operator:** This is a super cool operator that will cause (or has already caused) you pain and suffering throughout your physics career and it is given by
   $$
   L = \sum_{k=0}^n x^k \frac{d^k}{dx^k}.
   $$

5. 



Ok cool, so now we can write operators. Here are some cool constructions that are super useful.

**<u>Definition:</u>** Let $L$ be a linear ordinary differential operator, and $u:\mathbb R\to \mathbb R$ a smooth function such that
$$
Lu = \lambda u,
$$
for some $\lambda \in \mathbb C$. We then call $u$ an **eigenfunction** of $L$ and $\lambda$ and **eigenvalue** of $L$.

This is terminology that you might have seen in your linear algebra class, and because $L$ is a linear operator it makes sense to adopt the same notation. We are now ready to talk about differential equations!

**<u>Definition:</u>** An **Ordinary Linear Differential Equation** is an equation of the form
$$
Lu = f,
$$
 where $f \in C^\infty(\mathbb R)$ is some known smooth function and we are trying to solve for $u \in C^\infty(\mathbb R)$. The **order of the equation** is the order of $L$. If $L$ has constant coefficients then the equation is known as an **Ordinary Linear Differential Equation with Constant Coefficients.** If $f=0$ then the equation is **homogeneous** and the $u \in C^\infty(\mathbb R)$ is known as a **homogeneous solution**. Otherwise, $u$ is known as a **particular solution**. 

> ***Exercise:*** Make up an ordinary linear differential equation that has no nontrivial (aka $u=0$) solution. Make up an ordinary linear differential equation that has **exactly two** solutions. Can you? Why or why not?



## Initial Value Problems

So far, we have answered the second half of the most fundamental question in physics; the *'where will I be.'* But to actually give an answer, or to even tell if there is one, we need to incorporate the *'I am here'* part. We do this through initial value problems. 

**<u>Definition:</u>** An **initial value problem** for a linear ordinary differential equation is a system composed of an ordinary differential equation $Lu=f$ for some ordinary differential operator $L$ of order $n$ and smooth function $f\in C^\infty$ and a **boundary condition** $B(u) = 0$ often denoted by
$$
(IVP): \begin{cases}
L u = f\\
B(u) = 0.
\end{cases}
$$
In particular, the boundary condition is a map $B:C^\infty(\mathbb R) \to \mathbb R^n$.

**<u>Notation:</u>** We will often not write the boundary condition as a map, but rather as a set of explicit conditions.

**<u>Example:</u>** *(Newton's second law)* Let the position of a particle of mass $m$ over time be given by a function $x:\mathbb R\to \mathbb R$. Then we can write the **Newton's second law** differential operator given by
$$
N = m\frac{d^2}{dt^2}.
$$
If we know that the particle has a sum of forces $F:\mathbb R\to \mathbb R$ exerted to it over time, then we can form Newton's second law as the differential equation:
$$
Nx=F \iff m \frac{d^2 x}{dt^2} = F.
$$
If in addition, we know that the particle at time $t=t_0$ passed through position $x(t_0) = x_0$ we can write the boundary condition $B:C^\infty(\mathbb R) \to \mathbb R$, given by 
$$
B(x) = x(t_0) - x_0,
$$
and finally express Newton's second law as the following initial value problem
$$
(N2) : \begin{cases} Nx = F\\ B(x) = 0 \end{cases} = \begin{cases} m\frac{d^2x}{dt^2} = F \\ x(t_0) = x_0. \end{cases}
$$


**<u>Note:</u>** Solving an ODE and solving an IVP for an ODE are two different tasks! Usually ODEs have infinite solutions. Think, for example, the ODE
$$
\frac{df}{dx} = g.
$$
if $f$ is a solution, so is $f+C$ for any $C\in \mathbb R$. However, almost all IVPs are constructed such that the boundary condition limits the possible functions that you can consider to the point that they have a unique solution. For example, we can construct an IVP for the above ODE with the boundary condition $B:C^\infty(\mathbb R) \to \mathbb R$ such that for any smooth function $u \in C^\infty(\mathbb R)$ 
$$
B(u) = u(0).
$$
Then if $f \in C^\infty(U)$ is a solution of the ODE above, such that $B(f) = f(0) = 3$. Then only the function $u(x) = f(x) - 3$ solves the IVP, because it is the only solution of the differential equation such that $B(u) = 0$.

In Quantum Mechanics we will focus on solving both situations, with an emphasis on solving ODEs instead of  IVPs.



## First Order ODEs

### Integration

For first order ODEs we can take advantage of the fundamental theorem of calculus to get our solution for free. Here it is by the way.

**<u>Theorem:</u>** *(Fundamental Theorem of Calculus)* Let $f \in C^\infty(\mathbb R)$ be a smooth function. Then there exists a smooth function $F \in C^\infty(\mathbb R)$ such that $f = \frac{dF}{dx}$ and
$$
\int_a^b f(x) dx = F(b) - F(a).
$$


Now we can use this fact to solve any first order linear ODE like so. 

**<u>Theorem:</u>** *(Integration Theorem)* Given any first order linear ordinary differential equation of the form
$$
a \frac{df}{dx}= g,
$$
for smooth functions $a,g\in C^\infty(\mathbb R)$ and $a$ nonvanishing, the function $f:\mathbb R\to \mathbb R$ given for any $x\in \mathbb R$ by
$$
f(x) = \int_{c}^x\frac{g(t)}{a(t)} dt
$$
for any constant $c\in \mathbb R$ is a solution to the ODE.

**<u>Example:</u>** I mean... Take this one
$$
\frac{df}{dx}(x) = \sin(x) \implies f = -\cos(x) + C,
$$
for some $C\in \mathbb R$.

> **Exercise:** Solve the following ODE
> $$
> \sin(x)\frac{df}{dx} - \cos(x) f =  \cos (x)
> $$
> *Hint:* Consider the solution of $fg'+gf' = h$ for some known functions $g,h \in C^\infty(\mathbb R)$. 



### Integration Factors

Now it is time to solve the most general first order ODEs. In particular we know that any first order linear differential operator $L$ can be written, by definition, as
$$
L = a\frac{d}{dx} + b,
$$
for known smooth functions $a,b\in C^\infty(\mathbb R)$. This means that all the equations can be written as
$$
a\frac{df}{dx} + b = c,
$$
for known smooth functions $a,b,c\in C^\infty$. This is a pretty interesting coincidence because of product rule.

**<u>Lemma</u>** *(Product rule)* Given two smooth functions $f,g \in C^\infty(\mathbb R)$ the derivative of their product satisfies
$$
\frac{dfg}{dx} = g\frac{df}{dx} + f\frac{dg}{dx}.
$$
Now we can write the following theorem that solves ANY first order linear differential equation.

**<u>Theorem:</u>** *(Method of Integrating Factors)* Let $L = a \frac{d}{dx} + b$ where $a,b \in C^\infty(\mathbb R)$ are smooth functions, be any first order non-degenerate linear operator. Then the function $f : \mathbb R\to \mathbb R$ given by
$$
f(x) = \frac{1}{\mu(x)} \int_0^x \frac{g(x) \mu(x)}{a(x)} dx,
$$
is a solution to the ODE
$$
Lf = g,
$$
for some known smooth function $g \in C^\infty(\mathbb R)$, and where $\mu : \mathbb R\to \mathbb R$ is given by
$$
\mu(x) = \exp\left[\int_0^x \frac{b(x)}{a(x)} dx\right].
$$
***Proof:*** The goal of this procedure is to convert the problem to a product rule. In particular, since $a(x) \neq 0$ for any $x \in \mathbb R$ we can rewrite the equation as
$$
Lf = g \iff \frac{df}{dx} + \frac{b}{a} f = \frac{g}{a}.
$$
Now we would like to find some function $\mu : \mathbb R\to \mathbb R$ such that when we multiply both sides of the equation we get
$$
\mu \frac{df}{dx} + \frac{b}{a} \mu f = \frac{\mu g}{a},
$$
where it makes the left hand side look like a product rule. i.e. 
$$
\mu \frac{df}{dx} + \frac{b}{a} \mu f = \frac{d\mu f}{dx} \implies \frac{d\mu }{dx} = \frac{b}{a} \mu.
$$
By noticing that
$$
\frac{d\log \mu }{dx} = \frac{1}{\mu} \frac{d\mu}{dx}
$$
we can proceed and find $\log \mu$ using the integration theorem
$$
\frac{d\log\mu}{ dx} = \frac{b}{a} \implies \log \mu(x) = \int_0^x \frac{b(t)}{a(t)} dt \iff \mu(x) =\exp\left[\int_0^x \frac{b(t)}{a(t)} dt\right].
$$
Now we can substitute $\mu$ on the ODE to obtain:
$$
\frac {d\mu f}{dx} =  \mu \frac{df}{dx} + \frac{d\mu}{dx} f = \frac{\mu g}{a} \implies (\mu f)(x) = \int_0^x\frac{\mu(t) g(t)}{a(t)}dt \iff \boxed{f(x) = \frac{1}{\mu(x)} \int_0^x\frac{\mu(t) g(t)}{a(t)}dt.}
$$
And we are done!
$$
\begin{equation}\tag*{$\Box$}\end{equation}
$$
What we have managed to do with this theorem is to **solve all first order ODEs!** This is amazing news! In fact because we are so good at solving first order ODEs, a lot of our techniques for solving higher order ODEs will be to try our hardest to convert them into 1st order.



### Linearity

One of the most amazing properties of ordinary **linear** differential equations is that the sum of homogeneous solutions is a solution. In other words the following theorems.

**<u>Theorem:</u>** *(Sum of Homogeneous Solutions)* Let $L$ be some linear ordinary differential operator and $u,v \in C^\infty(\mathbb R)$ be solutions of the equation
$$
Lu = 0.
$$
Then $\alpha u + \beta v \in C^\infty(\mathbb R)$ is a solution for any $\alpha,\beta \in \mathbb R$. 

***Proof:*** $L(\alpha u + \beta v) = \alpha Lu + \beta Lv = 0$.
$$
\begin{equation}\tag*{$\Box$}\end{equation}
$$


 **<u>Theorem:</u>** *(Sum of particular Solutions)* Let $L$ be some linear ordinary differential operator and $u,v \in C^\infty(\mathbb R)$ be solutions of the following equations
$$
\begin{align*}
Lu = f && Lv = g,
\end{align*}
$$
for some fixed functions $f,g \in C^\infty(\mathbb R)$. Then $\alpha u + \beta v \in C^\infty(\mathbb R)$ is a solution for any $\alpha,\beta \in \mathbb R$ of the equation
$$
L (\alpha u + \beta v ) = \alpha f + \beta g.
$$
***Proof:*** Do it
$$
\begin{equation}\tag*{$\Box$}\end{equation}
$$
**<u>Corollary:</u>** If $u$ is a homogeneous solution and $v$ is a particular solution, then $u+v$ is a particular solution. 

These might seem obvious, so if you ever see an equation of the form
$$
Lu = (\text{something weird}) + (\text{something weirder}),
$$
try to split it! Don't try to solve it in one go.

Linearity has a bunch more interesting properties that we are going to use very often in quantum mechanics, so we will come back to this with spicier theorems. 



### Integration Techniques Sidenote

Since solving first order ODEs is basically integration don't forget to use Integration techniques to solve them! Things like substitutions, by parts, as well as other calculus theorems like chain rule and the inverse of a derivative can all be applied when solving such equations!

**<u>Example:</u>** *(An almost nonlinear ODE)* Consider the disgustingly looking nonlinear differential equation
$$
\frac{df}{dx} e^f = e^{ x}.
$$
Before we panic we can take a breath and notice that
$$
\frac{de^f}{dx} = \frac{df}{dx}e^f.
$$
Therefore if we call $u = e^f$ we actually have a linear equation of the form:
$$
\frac{du}{dx} = e^{x},
$$
that we can calculate a general solution in our sleep to be
$$
u = e^x + C,
$$
for any $C\in \mathbb R$. Therefore our equation has as a solution
$$
u=e^f = e^x + C \implies f=\log(e^x + C).
$$
If we were to solve the IVP with the boundary condition $f(0) = 0$ we have $C = 0$ and the ridiculous solution $f = x$. 
$$
\begin{equation}\tag*{$\Box$}\end{equation}
$$
Things like substitutions and so on go a long way for solving ODEs. Always be on the lookout of such cool tricks to apply especially when solving physics. Here is another example:

**<u>Example:</u>** *(Ugly trigonometric functions)* Consider the following equation
$$
\frac{df}{dx} = x^2 + \sin^2 (\arccos(x)),
$$
where $f \in C^\infty(0,1)$. Here if one tries use linearity will probably cry. Before we brute force we can take a second to look at the super annoying term on the right. I think $\sin(\arccos(x))$ is terrible. Yet again, I see that $x \in (0,1)$, which makes me feel a bit better. Because if $x = \cos \theta$ then all my problems will be solved, because the right hand side will become
$$
(\cos\theta)^2 + \sin^2(\arccos(\cos\theta)) = \cos^2\theta + \sin^2\theta = 1.
$$
Ok so why don't we try it? If we let $x = \cos\theta$ we have to change the derivative using chain rule. In other words we have
$$
\begin{align*}
\frac{df}{dx} 
&= \frac{df}{d\cos\theta}\\
&= \frac{df}{d\theta} \frac{d\theta}{d\cos\theta}\\
&= \frac{df}{d\theta} \left(\frac{d\cos\theta}{d\theta}\right)^{-1}\\
&= -\frac{1}{\sin\theta} \frac{df}{d\theta}.
\end{align*}
$$
Plugging this back to the equation we get
$$
-\frac{1}{\sin\theta}\frac{df}{d\theta} = 1 \implies f(\theta) = \cos\theta \implies f(x)=x.
$$
WHAT? How is this even possible? We know that $\frac{df}{dx} = 1$ so could it be that the disgusting right hand side is actually 1? Here is a picture. 

![ode-picture](_Differential_Equation_Review.assets/ode-picture.svg)

Well in hindsight, what we could have noticed is that if $x \in (0,1)$, then we can think of it as the side of a right angle triangle that is formed by connecting a point on the unit circle and the $x$-axis.

The function $\arccos(x)$ gives us the angle of the right angle triangle between the $x$-axis and the point on the circle. We know that $\sin$ of that angle gives us the other side. Summing the squares of both sides gives us the hypotenuse, which in this case is *always* $1$ since the triangle is on the unit circle. 

Now a genius, I guess, could have seen it from the beginning. But for the rest of us mortals, the trig trick should be cool enough!
$$
\begin{equation}\tag*{$\Box$}\end{equation}
$$

> **<u>Exercise:</u>** 



**<u>Sidenote:</u>** Since to solve the 1st order ODEs we integrated, this term has stuck for when solving other differential equations in general. When a physicist tells you to *'integrate a Differential Equation'* they most likely mean to solve it. 



## Second Order ODEs

First   







