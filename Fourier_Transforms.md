# Fourier Transforms

A Fourier transform is such a cool tool! It is a (mostly) invertible map that takes in a function and spits out another function that is often easier to work with, but still contains all the information we want to extract from our problem. The formula for the Fourier transform of an appropriate function $f(x)$ is given by
$$
\hat f(\omega)= \int_{-\infty}^\infty f(x)e^{i\omega x} dx.
$$
In these notes we will go over the derivation of the Fourier Transform play with some cute pictures, and show how powerful of a tool it can be in quantum mechanics.

[toc]

# Intuition

Before we go into writing a bunch of scary math, let's see some cute pictures. We will intuitively introduce the Fourier transform form the point of view of spinning stuff. After we are comfortable with spinning circles in the complex plane, we will proceed with looking at what happens to scaling these spinning circles, and then see some surprising properties that will make Fourier transforms natural. 

## Spinning Complex Circles

A complex number is $z = a + bi$, where $a,b\in \mathbb R$ are some real numbers. The thing we immediately notice by looking at this representation, is that $a$ and $b$ will never mix with each other. It's like they live in their own separate copies of the real line. In fact it looks like we could say that $z = \binom ab$ is some vector in the plane $\mathbb R^2$. This idea is, in fact, rigorously supported, and we can picture complex numbers as little vectors that are stuck in the plane. 

Therefore, I can define a circle using complex numbers. A circle $S^1 $ is comprised out of all the vectors in the plane that have length $\norm{z}= \sqrt{z\bar z} = \sqrt{a^2 + b^2}= 1$. We know that these points can be parameterized using one number $\theta \in \mathbb R$ like so
$$
z \in S^1 \iff z = \cos\theta + i \sin \theta = e^{i\theta}.
$$
The fact that the circle can be parameterized by $e^{i\theta}$ where $\theta$ is the angle is so cool!



<iframe scrolling="no" title="Circle" src="https://www.geogebra.org/material/iframe/id/w79fdxez/width/567/height/405/border/fff/sfsb/true/smb/false/stb/false/stbh/false/ai/false/asb/false/sri/false/rc/false/ld/false/sdz/false/ctl/false" width="567px" height="405px" style="border:0px;display: flex; justify-content: center;"> </iframe>



As you can see, this is a counterclockwise rotating guy. As $\theta$ increases the point on the circle moves counter clockwise along it with a certain speed. **How can I change the speed?**, well we multiply it by a number! For example, $e^{i\theta}$ takes $\Delta \theta = 2\pi$ to do a full rotation, but $e^{2i\theta}$ takes only $\Delta \theta = \pi$ to do a full rotation. As a result, we can multiply the $\theta$ by a number $\omega$  to get $e^{i\omega \theta}$ which is a point on a circle that rotates with frequency $\omega$! Check this out. 



<iframe scrolling="no" title="Circle" src="https://www.geogebra.org/material/iframe/id/ruayvw7z/width/567/height/405/border/fff/sfsb/true/smb/false/stb/false/stbh/false/ai/false/asb/false/sri/false/rc/false/ld/false/sdz/false/ctl/false" width="567px" height="405px" style="border:0px;display: flex; justify-content: center;"> </iframe>

make 

So we can multiply with a number and we get faster spinning circles. All of this is perhaps obvious, but we are about to start playing by doing a simple thing. Changing the radius.

extract 

## Drawing With Circles

So far the radius of our circle was $\norm{z} = \norm{e^{i\theta}} = 1$. But it should be clear that if we want to change the radius of the circle, all we need to do is to multiply by a real number $r\in \mathbb R$. So $re^{i\theta}$ can trace a circle of radius $r$. The cool thing is we can use this to **wrap functions around a circle.** Here is how we can do this.

Take a function $f : \mathbb R \to \mathbb R$. We can *wrap it around a circle* by the following procedure. For each angle $x$, we will scale the radius by $f(x)$. In other words, we have parameterized our circle like so
$$
z(x) = f(x) e^{ix}.
$$
  Here is how this looks for some function.

<iframe scrolling="no" title="Circle" src="https://www.geogebra.org/material/iframe/id/up2kvfdr/width/700/height/404/border/fff/sfsb/true/smb/false/stb/false/stbh/false/ai/false/asb/false/sri/true/rc/false/ld/false/sdz/false/ctl/false" width="700px" height="404px" style="border:0px;"> </iframe>



> Try and play around with this and see where each point is mapped to! By default, this is plotting the function 
> $$
> f(x) = \frac{\cos(x)}{x^2 + 1}.
> $$
> As you can see, for $x=0$ we have that $f(0) = 1$ and $z(0) = f(0) e^{i0} = f(0) + 0 i = 1 + 0i$, therefore it is a vector pointing at the right of the circle. But as we increase $x$ this changes. The radius decreases as the angle increases drawing this circle looking thing. 



We saw before that we can traverse the circle faster and slower depending on the frequency, which was simply multiplying a real number $\omega \in \mathbb R$ to the angle. What if we add a frequency over the way we place the function on the circle? Play around with this plot to see what happens when you change the frequency.



<iframe scrolling="no" title="Circle" src="https://www.geogebra.org/material/iframe/id/bu2yaeus/width/785/height/478/border/fff/sfsb/true/smb/false/stb/false/stbh/false/ai/false/asb/false/sri/true/rc/false/ld/false/sdz/false/ctl/false" width="785px" height="478px" style="border:0px;"> </iframe>



> **<u>Exercise:</u>** Try and plug in $f(x) = \cos(x)$ and $f(x) = \sin(x)$ and see what happens when you change the frequency! Doesn't it look pretty? Check out what happens when you do $f(x) = \cos(4 x)$. For what $\omega$ does the plot simplify? Try a different number. Isn't that so cool? 

These are really cute pictures, but we are physicists, so we want to extract meaningful numbers from them.



## Information from Wrapping Around a Circle

We want to extract information from wrapping these functions around a circle. Turns out there is a pretty cool coincidence for periodic functions. To understand this please do *"exercise"* above, by playing around with wrapping $\cos(Ax)$ for different $A\in \mathbb R$ around a circle and fiddling with the frequency. 

As you saw, when the frequency of the cosine wave matches the frequency of which we rotate around the circle, with $e^{i\omega t}$ then (and only then) we get a circle out of it. In other words, if I could play only with $\omega$ I would be able to find out what $A$ is by seeing for what $\omega$ the graph looks like a pretty circle. 

However, there has to be a better way to glean this than looking at infinite plots for different $\omega \in \mathbb R$ until the graph looks like some version of pretty. The answer, believe it or not, came from physics. We want to look at the **center of mass** of the graph that is wrapped around the circle. 

Say that wrapped around graph was made out of copper or something. Then we could calculate the center of mass by multiplying the displacement of each point with the mass and adding them together. If the graph was discrete, and it were to have $n$ evenly spaced points, then the center of mass, which I will call $\tilde f_n(\omega)$ for totally no particular reason, can be calculated by 
$$
\tilde f_n(\omega) = \frac{1}{n}\sum_{k=-\frac{n}{2}}^{\frac{n}{2}} e^{i\omega k} f(k).
$$
The plot of the center of mass, would then look like this. 



<iframe scrolling="no" title="Circle" src="https://www.geogebra.org/material/iframe/id/tk4ms7a9/width/782/height/477/border/fff/sfsb/true/smb/false/stb/false/stbh/false/ai/false/asb/false/sri/true/rc/false/ld/false/sdz/false/ctl/false" width="782px" height="477px" style="border:0px;"> </iframe> 



In here, the **blue** arrow is the average of all the black points, that are evenly generated around the red wire. You can change their number to see a more accurate estimate of the center of mass. The more points you include (in general) the better the estimate for the center of mass of that wire is!

> **<u>Exercise:</u>** Change the frequency $\omega$. Can you see that the center of mass is pretty much around the origin as you increase the number of points? For what value of $\omega$ is that not the case? What does this tell you? Try different shapes, and different periodic functions. What do you observe?
>
> For what frequencies $\omega \in \mathbb R$ Is the center of mass not in the origin in the following function?
> $$
> f(x) = \cos(x) + \frac{1}{2} \sin(3x).
> $$
> Is the position center of mass (the blue vector) a good predictor of the frequencies composing $f$?

**This is pretty nifty!** Now we can get the information about frequency at which the shape is pretty only by looking at the blue vector. So now if someone gives us this vector instead of the plot for every frequency that's all we need to have in order to tell you the frequency of the cosine wave.



## Almost Rigorous Definition

We are almost there. In fact we have stumbled upon what the *Fourier transform* without even noticing. The **Fourier transform** of a function $f(x)$ at any $\omega \in \mathbb R$ is the **center of mass vector** we constructed above! Since it is a vector in the plane $\mathbb R^2$ we can also turn it into a complex number and voila! 

Let's see how to put math in the sentence above. The center of mass vector (which I am going to call $\tilde f_n(\omega)$) of $n \in \mathbb N$ evenly distributed points on the plot of $f(x)$ wrapped around a circle with frequency $\omega \in \mathbb R$, can be calculated by summing them like so
$$
\tilde f_n(\omega) = \frac{1}{n}\sum_{k=-\frac{n}{2}}^{\frac{n}{2}} e^{i\omega k} f(k).
$$
In fact, one will notice that this is **so tantalizingly close** to the definition of the Fourier transform. In fact one can sort of see that if we take $n\to \infty$ this sum will be replace with an integral from $-\infty$ to $\infty$ like so
$$
\hat f(\omega) = \int_{-\infty}^\infty e^{i\omega x} f(x) dx.
$$
*For the math people who are screaming at me that I am waving details under the rug like a physicist, please see the next section for a rigorous definition.* 

The intuition, however, is still the same. If I give a function to the Fourier transform, for every frequency it will spit out a vector (aka a complex number) that is the center of mass of wrapping the function around the circle with a particular frequency. And we have found that that vector is directly related to frequency properties of the original function.

> **<u>Exercise:</u>** Plug in $f(x) = \cos(3x)$ and $f(x) = \sin(3x)$ in the plot above, you should find that the vector with the maximum length is at $\omega = \pm 3$. However, it should not be the same vector for the two cases. What is the same vector but for the function
> $$
> f(x) = \frac{1}{2}\cos(3x) - \sin(3x). 
> $$
> What does this tell you about how the Fourier transform represents frequency? How about
> $$
> f(x) = \cos(x + \frac{\pi}{4}).
> $$
> ***Answer:*** The imaginary component of the Fourier transform seems to measure how much $\sin$ of a particular frequency you have, and the real component seems to measure how much $\cos$. In other words, the phase of the Fourier transform, seems to measure the phase of the wave at that frequency, and the magnitude of the Fourier transform seems to measure the amount of that frequency. 

In essence, the Fourier transform tells us what frequencies compose our function and, their relative amplitude and phase. 



## Picturing a Fourier Transform

As we have seen so far, the Fourier transform of a function, gives for every frequency $\omega$ an arrow $\hat f(\omega)$. It would be nice if we could create a representation for it. And we can. 

In the following image I have plotted the function
$$
f(x) = e^{-x^2} \left[\sin(ax) + \cos(bx)\right],
$$
and below it, its Fourier transform in 3D. 

<iframe scrolling="no" title="3D Fourier" src="https://www.geogebra.org/material/iframe/id/uvthhr4d/width/936/height/652/border/fff/sfsb/true/smb/false/stb/false/stbh/false/ai/false/asb/false/sri/true/rc/false/ld/false/sdz/true/ctl/false" width="936px" height="652px" style="border:0px;"> </iframe>

The axis shown is the frequency axis $\omega$ where on each point I have attached the Fourier transform vector $\hat f(\omega)$ and because they are infinite I am only showing the tip of their arrows which forms this niece curve. Check out what happens when you adjust the frequencies of the signs and cosines. 



# Definition

Hopefully, by now you have an intuitive idea of what the Fourier transform is and why it is the right thing to calculate in order to extract a function's frequency and phase information. Now let's be more rigorous about how these objects are defined and how we can use them in math.



## Square Integrable Functions

**<u>Definition:</u>** Consider a function $f:\mathbb R\to \mathbb R$. If the following integral is well defined, i.e.
$$
\int_{-\infty}^\infty |f(x)|^2 dx < \infty
$$
then we call $f$ **square integrable.** The **set of square integrable functions** from $\mathbb R$ to itself is known as $L^2(\mathbb R,\mathbb R)$, or simply $L^2$.

Here is a cool property of square integrable functions.

**<u>Proposition:</u>** Any square integrable function $f \in L^2$ satisfies
$$
\lim_{x\to \pm \infty} f(x) = 0.
$$
In other words it doesn't *blow up* as $x\to \pm \infty$.

***Proof:*** Let $f \in L^2$ be a square integrable function such that $ \lim_{x\to \infty} f(x) = C \in \mathbb R$ for some nonzero $C\neq 0$. Then by the definition of the limit for any $\epsilon > 0$ there exists $x_0 \in \mathbb R$ such that 
$$
f(x) > C - \epsilon,\ \ \forall x > x_0.
$$
Therefore we can see that
$$
\int_{x_0}^\infty |f(x)|^2 dx > \int_{x_0}^\infty |C - \epsilon|^2 dx \to \infty.
$$
This implies that
$$
\int_{-\infty}^\infty |f(x)|^2 dx \geq \int_{x_0}^\infty |f(x)|^2 dx \geq \infty.
$$
Therefore the function $f$ is not square integrable, which is a contradiction. The same argument works for the limit $x\to -\infty$.
$$
\begin{equation}\tag*{$\Box$}\end{equation}
$$
These are particularly nice functions and they are the functions we encounter most often in quantum mechanics. So it is nice to know some of their properties.



## Fourier Transform of Square Integrable Functions

We are finally ready.

**<u>Definition:</u>** The **Fourier Transform** is a linear map $\mathcal F : L^2 \to L^2$ given for any $f\in L^2 $ by 
$$
\mathcal F[f](\omega) = \hat f(\omega) = \int_{-\infty}^\infty f(x)e^{i\omega x} dx.
$$

Then we can see that there is an inverse of this map.  

**<u>Theorem:</u>** *(Inverse Fourier Transform)* The fourier transform is skew involutive, i.e. the **inverse fourier transform** is given by
$$
\mathcal F^{-1}[\hat f](x) = \frac{1}{2\pi}\int_{-\infty}^\infty e^{-i\omega x} \hat f(\omega) d\omega = f(x).
$$


Now that we have both, of them we can move on to discover some properties.



## Properties

Here is a collection of properties of the Fourier transform.

**<u>Proposition:</u>** *(Fourier transform properties)* Let $f,g \in L^2$ be square integrable functions and $a,b \in \mathbb R$ be constants. Then the Fourier transform has the following properties.

1. **Linearity:** $\mathcal F[af + b g] = a\hat f + b\hat g$. 
2. **Translation:** $\mathcal F[f(x-a)](\omega)= e^{-ia\omega}\hat f(\omega)$
3. **Scaling:** $\mathcal F[f(ax)](\omega) = \frac{1}{|a|}\hat f\left(\frac{\omega}{a}\right)$
4. **Zero Component:** $\hat f(0) = \int_{-\infty}^\infty f(x) dx$.
5. **Product:** $\mathcal F[f\ast g] = \hat f \hat g$.
6. 

where $f\ast g$ is the convolution given by 
$$
f\ast g(x) = \int_{-\infty}^\infty f(x-y)g(y)\, dy.
$$
***Proof:*** Hell no! Check out [Wikipedia](https://en.wikipedia.org/wiki/Fourier_transform#Properties_of_the_Fourier_transform).
$$
\begin{equation}\tag*{$\Box$}\end{equation}
$$


# Applications in Quantum Mechanics

TBD I don’t have time now! 





