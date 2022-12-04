---
title: "Harmonic Functions"
---

# A (Fun) Discussion on Harmonic Functions

Some introductions into harmonic functions. This post is meant to be an approchable read into these phenomena.

## 1. Introduction on Harmonic Functions

A mass on a spring, measuring fluid flow, even the cosine wave, are all examples of where harmonic functions can be found within our world. The name itself stems from an object or force going through some type of harmonic (or oscillating) motion from a steady state equilibrium. From a graphical standpoint, it is merely an oscillation between two points, in an infinitesimal manner. To simply state, a repeated motion until the system continues indefinitely or reaches an equilibrium point.

#### 1.1 Defining Harmonic Functions

In two dimensions, a harmonic function is one that satisfies the following equation that given the following function \\( u(x,y) \\), it satisfies the Laplace equation (i.e. it is twice differentiable and satisfies the given equation):
$$ \Delta = \triangledown(\triangledown f) = \triangledown^2f = f\_{xx} + f\_{yy} = 0$$
In its essence, the equation merely states that the sum of second partial derivatives with respect to \\(x\\) and \\(y\\) have to sum up to 0. For example, the function \\(x^3 - 3xy^2\\) is a function that is harmonic:

{{< math >}}
\begin{align*}
\frac{\partial^2f}{\partial x^2} = 6x \quad&\quad \quad\frac{\partial^2f}{\partial y^2} = -6x \\
\newline
6x - 6x &= 0
\end{align*}
{{< /math >}}

Interestingly enough, while \\(\sin(x)\\) and \\(\cos(x)\\) describe harmonic functions graphically, they do not explicitly satisfy the conditions of a harmonic function. However, they are only defined as harmonic at certain points. However, this is only for two dimensions (\\(\mathbb{R}^2\\)). in a more general term, a harmonic function in \\(\mathbb{R}^n\\) satisfies the condition where:
$$ \Delta f(x_1, x_2,\dots, x_n) = \sum^n\_{i = 1}\frac{\partial^2f}{\partial x_i^2} = 0$$

## 2. Properties of Harmonic Functions

Harmonic functions themselves are just an equation, something that satisfies a condition. However, these equations preserve many more useful properties that give insight into how useful they exactly are. Now, if \\(f\\) is a harmonic function and such a landscape is defined for \\(f\\) which is continuous and gapless, that is the harmonic landscape. We start off with one of the first properties:

#### 2.1 Mean Value Property

One remarkable property of a harmonic function is known as the mean value property. What the property states is that given any point in the harmonic function, one can determine the value of the function by averaging the value of the circle found around the point. However, the term average depends on the space which is defined on. For example, given a linear (harmonic) function present on \\(\mathbb{R}\\), the average of it is by simply taking it over the interval as follows:
$$f(x_0) = \frac{1}{b-a} \int_a^b f \space ds$$
Now, given a function in \\(\mathbb{R}^2\\), the definition can be generalized as follows. Given any point \\((x_0, y_0) \in \mathbb{R}^2\\) and any circle \\(C_a\\) of radius \\(a > 0\\), we have
$$ f(x_0,y_0) = \frac{1}{2\pi a} \int\_{C_a}f\space ds$$

#### 2.2 Uniqueness

Another property of harmonic functions is that the values on the boundary of a domain determine the values inside the domain. If we define the values of a harmonic function on the boundary domain only, the rest of the values inside of the surface follow because of the uniqueness property. Only one harmonic surface exists to fit the set of all boundary values.

#### 2.3 Flatness

From 2.2, suppose we had the boundary values and curve defined within a field of \\(\mathbb{R}^n\\) and wanted to construct the _flattest_ possible landscape possible. However, how do we define a "flat" landscape? The gradient of a surface \\(|\triangledown f|\\) represents the rate of ascent (or descent) upon a particular surface. At a certain point, this can represent the steepness in this case. If we want the total _steepness_ across a surface, we can show the total by integrating across the surface:
$$ \int\int_D |\triangledown f|^2\space dA = \text{steepness of the surface }f(x,y)\text{ over }D$$
Now, harmonic functions are among all functions with that specific boundary curve, having the minimal total steepenss, thus the flattest landscape.

A side consequence of this is that the landscape itself would not have any local minima and maxima as well.

##### 2.3.1 Flatness and the Dirichlet Energy Integral

In physics, the measure of steepness is common in energy integrals. If \\(|\triangledown f|\\) was a velocity field, then multiplying that with \\(0.5m\\) yields the total kinetic energy at a certain point. With some algebra, the above formula can also be adapted to the total kinetic energy in a surface to. These appear in a another phenomena known as the Dirichlet Energy Integral. Problems of this type involve solving some form of a partial differential equation (PDE). In this case, harmonic functions that solve the energy integral also happen to minimize the energy as well.

## 3. Temperature and Harmonic Functions

After all this discussion on some theoretical properties of harmonic functions, we turn to discuss some of the more practical applications of harmonic functions and how one can apply them in a real life scenario. We cover one of the most important ones--temperature. Another main application is measuring voltage represented as a graph. As graphs were not covered previously, we will subsequently not be covering this as well.

Suppose we carry a hypothetical sheet of metal that has a defined boundary and a certain landscape. We call this shape a _lamina_. For a system in equilibrium, this sheet of metal will be at a equilibrium temperature, say room temperature. Then, we introduce a source of heat on the _boundary of the lamina_. From 2.3, we see that one consequence is that there is no local minima and maxima. We create a steady state temperature distribution \\(T(x,y)\\). Because of the local minima and maxima property, no one point will have a certain temperature higher than those around it. Instead, the heat will even out.

Thinking about it from a physics perspective, as you heat up a sheet of metal from the edge and touch it, there would not be a certain point where the heat is much more drastic than other points. Instead, it will evenly heat up. However, I do not encourage heating up metal surfaces to demonstrate harmonic function properties.

## 4. Conclusion

From here, now what? Harmonic functions have many more applications and fun theory-esque things besides the thigns above listed. Their applications are endless; from flow to animation, they can be found all around. From here, one can adventure into harmonic forms, more Dirichlet problems, and Fourier series as well!

[Back to writing](../../blog)
