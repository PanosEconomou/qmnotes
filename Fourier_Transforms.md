# Fourier Transforms

A Fourier transform is such a cool tool! It is a (mostly) invertible map that takes in a function and spits out another function that is often easier to work with, but still contains all the information we want to extract from our problem. In these notes we will go over the derivation of the Fourier Transform play with some cute pictures, and show how powerful of a tool it can be in quantum mechanics.

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



So we can multiply with a number and we get faster spinning circles. All of this is perhaps obvious, but we are about to start playing by doing a simple thing. Changing the radius.



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



## Information from wrapping around a circle

We want to extract information from wrapping these functions around a circle. Turns out there is a pretty cool coincidence for periodic functions. To understand this please do *"exercise"* above, by playing around with wrapping $\cos(Ax)$ for different $A\in \mathbb R$ around a circle and fiddling with the frequency. 

As you saw, when the frequency of the cosine wave matches the frequency of which we rotate around the circle, with $e^{i\omega t}$ then (and only then) we get a circle out of it. In other words, if I could play only with $\omega$ I would be able to find out what $A$ is by seeing for what $\omega$ the graph looks like a pretty circle. 

However, there has to be a better way to glean this than looking at infinite plots for different $\omega \in \mathbb R$ until the graph looks like some version of pretty. The answer, believe it or not, came from physics. We want to look at the **center of mass** of the graph that is wrapped around the circle. 

Say that wrapped around graph was made out of copper or something. Then we could calculate the center of mass by multiplying the displacement of each point with the mass and adding them together. If the graph was discrete, and it were to have $n$ points, then finding the center of mass, would look like this. 

 













