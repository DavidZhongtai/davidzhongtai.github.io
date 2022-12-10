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

#### 2.2 Triangle Inequality

List how it ties w cauchy schwarz

#### 2.3 Chebyshev's Inequality

#### 2.4 Inequality of Arithmetic and Geometric Means

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
