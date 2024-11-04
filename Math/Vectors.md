
Vectors are a key concept when it comes to Linear Algebra (see [[Linear Algebra Table of Contents]]). Vectors always take in what's known as a weight and a magnitude (Weight being length and magnitude being direction). 2D Vectors are represented by 2 numbers, typically an x and y component, and 3D Vectors are represented by 3 numbers, typically x, y, and z.
# <u>Table of Contents</u>

^c1d916

[[#^1f65c2 | 1. Scalar Vector Operations]]
[[#^fc7e07| 2. Vector Negation]]
[[#^628b72| 3. Adding and Subtracting Vectors]]
[[#^50ba35| 4. Length]]
[[#^fb203f| 5. Unit Vector]]
[[#^819c47| 6. Dot Product]]
[[#^725cd6| 7. Cross Product]]


## Scalar vector operations

^1f65c2

When arithmetic operations are performed on a vector, they are performed by what's known as a scalar, which applies the operation to every component in the vector.

Example:

![[Vector Arithmetic.png]]
(Notice how adding x applies addition arithmetic to ALL components)

## Vector Negation

^fc7e07

Negating a vector results in the negation of all components of the vector. This reverses the direction of the vector.

![[Vector Negation.png]]

## Adding and Subtracting Vectors

^628b72

Vector addition and subtraction is known as component wise. This basically means that each component is applied (just like with arithmetic) with the operation.

Example:

![[Vector Addition & Subtraction.png]]

When we apply this operation on vector $\vec v = (4,2)$ and vector $\vec k= (1,2)$, it adds the vectors on top of each other:

![[Vector Addition Visual.png]]

With Subtraction, we take the vector that is between the two given vectors, as shown in the next example:

![[Vector Subtraction Visual.png]]

## Length

^50ba35

Getting a vector length uses the Pythagoras Theorem, as shown below, the length is simply the hypotenuse.

![[Vector Length.png]]

This shows the length as:
![[Length Equation.png]]

Where $\Vert v \Vert$ is the length of the vector $\vec v$. This can be extended to 3D by simply adding the $z^2$ component.

## Unit Vector

^fb203f

A Unit Vector is a vector who's length is exactly 1. We can calculate a unit vector by dividing each of the vector's components by its length:

![[Unit Vector Formula.png]]

This means to get a unit vector from vector $\vec j = (3,7)$, we must first get the length of the vector and run the following operation on the vector:

$\hat j = \vec j / \Vert j \Vert = (\frac 3 {\Vert j \Vert},\frac 7 {\Vert j \Vert})$

## Vector Vector Multiplication

When multiplying vectors, there are two methods of multiplication we can use, both with their own unique use cases. One is the dot product, denoted as $\vec a \cdot \vec b$ and the cross product, denoted as $\vec a \times \vec b$.

## Dot Product

^819c47

The dot product of two vectors is equal to the scalar product of their lengths (the length) times the cosine of the angle between them.  This is denoted by the below formula:

$\vec v \cdot \vec k = \Vert \vec v \Vert \cdot \Vert \vec k \Vert \cdot cos\Theta$

If both $\vec v$ and $\vec k$ were unit vectors, then their length would be 1, resulting in the formula becoming this:

$\hat v \cdot \hat k = 1 \cdot 1 \cdot cos\Theta = cos\Theta$

In this sense, it'd be easier to calculate the unit vectors of each vector first before calculating the Dot Product

To calculate the dot product, we can use a component-wise multiplication where we add the results together:

$\begin{pmatrix} 0.6 \\\ -0.8 \\\ 0.0 \end{pmatrix}\cdot \begin{pmatrix} 0.0 \\\ 1.0 \\\ 0.0\end{pmatrix} = (0.6 \times 0.0) + (-0.8 \times 1.0) + (0.0 \times 0.0) = -0.8$

To find the angle between the two vectors, we simply use the inverse of the  $cos$ function $cos^{-1}$:

$\cos^{-1}(-0.8)$


## Cross Product

^725cd6

The cross product is only defined in 3D space and takes to non-parallel vectors as input and produces third vector that is orthogonal to the input vectors. If both inputs are orthogonal, the resulting vector would produce three orthogonal vectors. The following image is what this would look like in 3D space:

![[vectors_crossproduct.png]]
The below formula is how we can calculate the cross product:

![[Cross_Product.png]]

