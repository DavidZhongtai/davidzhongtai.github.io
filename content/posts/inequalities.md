---
title: "Fun with Inequalities"
---

# Inequality Fun and Their Applications (WIP)

Article is in WIP. This article assumes the reader has basic knowledge of calculus, analysis, and statistics. Covers topics ranging from basic Cauchy Schwarz to Lipschitz, culminating in us pulling out a mathematical rabbit out of an algebraic hat.

## 1. What is an Inequality?

An inequality compares two values, showing if one is less than, greater than, or simply not equal to another value. Literally, it does not get more simpler than that. For example: \\(3 \leq 5\\) directly reads "3 is less than or equal to 5." Whereas \\(14 \geq 2\\) reads "14 is greater than or equal to 2."

## 2. Inequalities in Calculus

Now, we cover some basic and interesting inequalities in calculus and discuss their implications in a bigger picture. We will be utlizing the concept of vectors and spaces.

#### 2.1 Cauchy-Schwarz Inequality

One of the first (and most important) inequalities we cover is known as the Cauchy Schwarz Inequality. We first define two vectors \\(u\\) and \\(v\\) in \\(\mathbb{R}^n\\) given the following form:

$$ u = ( u_1, u_2, ..., u_n) \quad v = ( v_1, v_2, ..., v_n) $$
Given these two vectors, Cauchy Schwarz states that: 
$$|u \cdot v| \leq |u| |v|$$
And in coordinates, this is written as: 
$$ |u_1v_1 + u_2v_2 + ... + u_nv_n| \leq \sqrt{u_1^2 + u_2^2 + ... u_n^2}\sqrt{v_1^2 + v_2^2 + ... v_n^2} $$
While this inequality has no significant real world applications, this inequality comes in particularly handy for many max/min problems with constraints as well as math olympiad questions. For example, if we know that \\(x^2 + y^2 + z^2 = 1\\) and we want to find the maxmimum \\(x + 2y + 3z\\), we can utilize the inequality by finding different vectors that represent the over equation.

Take the vectors
$$u = (1,2,3) \quad \text{and} \quad v = (x,y,z)$$

We can see that \\(u\cdot v = x + 2y + 3z\\) which is our original equation we want to maximize. We invoke Cauchy Schwarz and arrive at the inequality that:
{{<math>}}
\begin{align*}
x + 2y + 3z &\leq \sqrt{x^2 + y^2 + z^2}\sqrt{1^2 + 2^2 + 3^2}\\
&\leq \sqrt{1}\sqrt{1^2 + 2^2 + 3^2} \\
x+2y + 3z &\leq \sqrt{14}
\end{align*}
{{</math>}}
We see that the maximal value is obtained at:
$$x = \frac{1}{\sqrt{14}}\quad y = \frac{2}{\sqrt{14}} \quad z = \frac{3}{\sqrt{14}}$$
which satisfies the constraint as well. One can also note that when plugging in generic variables, a general form of the equation can be found with the constraint \\(x^2 + y^2 + z^2 = 1\\) to maximum \\(ax + by + cz\\) where \\(x,y,z\\) are:
$$x = \frac{a}{\sqrt{a^2 + b^2 + c^2}}\quad y = \frac{b}{\sqrt{a^2 + b^2 + c^2}} \quad z = \frac{c}{\sqrt{a^2 + b^2 + c^2}}$$
Now, we continue onto the triangle inequality; another fun application.

#### 2.2 Triangle Inequality

The triangle inequality is also an extremely well known inequality in math. Geometrically, it states that the sum of the lengths two sides of the triangle cannot exceed the length of the largest side. Through the triangle inequality, one can find a reasonable range of distances and quantities something can be given knowns and unknowns. For example, given the unknown difference between two cities, one can use the triangle inequality to indirectly calculate the distances between two cities. For example, below, one can use the triangle inequality to get a rough estimate of the distance between two cities without knowing the true distance.

<!-- ![distances](/distance.png) -->

#### 2.3 Chebyshev's Inequality

Another fun inequality is also a pretty important tool for solving Math Olympiad similar problems. This is known as Chebyshev's inequality. If we are given two monotone sequences (sequences constantly increasing and decreasing): \\(\left\\{x_i\right\\}, \left\\{y_i\right\\}\\) and the sequences are similarly ordered, then:
$$n\sum^n\_{i=1}x_iy_i \geq \sum^n\_{i=1}x_i\sum^n\_{i=1}y_i$$
If the two sequences are oppositely ordered, then we get the result of
$$n\sum^n\_{i=1}x_iy_i \leq \sum^n\_{i=1}x_i\sum^n\_{i=1}y_i$$
When both sequences are constants, then the sums are equal. To use this, we can explore a similar problem. Assume that \\(a,b,c \in \mathbb{R}\\), then we want to show the following result:
$$\frac{ab}{a+b}+\frac{bc}{b+c}+\frac{ca}{c+a}\leq\frac{3(ab+bc+ca)}{2(a+b+c)}$$
We assume that \\(a,b,c\\) all belong to a monotonic sequence (i.e. \\(a\geq b\geq c\\)). Thus, we can use a form of Chebyshev's Inequality. We note that:
$$a +b \geq a + c \geq b+c$$
Because of the properties of fractions, we can also see that
$$\frac{ab}{a+b}\geq \frac{ac}{a+c} \geq \frac{bc}{b+c}$$
Combining both sequences, we see that the desired quantity is acheived:
$$\frac{ab}{a+b}+\frac{bc}{b+c}+\frac{ca}{c+a}\leq\frac{3(ab+bc+ca)}{2(a+b+c)}$$

#### 2.4 All Things Means

One last type of inequality (more of a subsection that deserves its own article potentially later) is the concept of a mean. We will only discuss a few main means, however, the methods of averaging a set are endless. Usually, most people are familiar with the following mean: add a number of items up, then divide by the number of items \\(n\\). In mathematical notation, that is described as:
$$\frac{1}{n}\sum^nx_i = \text{the Arithmatic Mean}$$

## 3. Inequalities in Analysis

#### 3.1 Triangle Inequality Applications

#### 3.2 Lipschitz Functions

## 4. Inequalities in Statistics

#### 4.1 Estimation

###### 4.1.1 Method of Moments

###### 4.1.2 Maximum Likelihood Estimation

#### 4.2 Jensen's Inequality for Estimators

#### 4.3 Chebyshev's Inequality (Revisited)

## 5. Conclusion

#### 5.1 A Mathematical Rabbit out of an Algebraic Hat
