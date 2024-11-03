A matrix is a rectangular array of numbers or mathematical expressions. Each item in a matrix is called an element of the matrix. Below is an example of a 2x3 matrix

$\begin{pmatrix}1 & 2 & 3\\\ 4 & 5 & 6\end{pmatrix}$

Matrices are indexed by (i, j) where i is the row and j is the column, which is why the above matrix is 2x3 (2 rows, 3 columns). Value 4 would be at location (2, 1).
# <u>Table of Contents</u>

[[#^615da9| 1. Adding and Subtracting]]
[[#^a844d0| 2. Matrix Scalar Products]]
[[#^441ff4| 3. Matrix-Matrix Multiplication]]
[[#^9ed9f2| 4. Matrix-Vector Multiplication]]
[[#^5989f7| 5. Scaling]]
[[#^c1f3df| 6. Translation]]
[[#^95629b| 7. Rotation]]






## Adding and Subtracting

Adding and subtracting between two matrices is done on a per-element basis. It is done on the elements of both matrices with the same index. This means that matrix addition and subtraction can only be done on matrices of the same dimensions. A 3x2 and a 2x3 matrix cannot be added or subtracted together.

With two 2x2 matrixes, the results look like this:

$\begin{pmatrix}1 & 2\\\ 3 & 4\end{pmatrix} + \begin{pmatrix}5 & 6\\\ 7 & 8\end{pmatrix}  = \begin{pmatrix}1 + 5 & 2 + 6 \\\ 3 + 7 & 4 + 8\end{pmatrix} = \begin{pmatrix}6 & 8\\\ 10 & 12\end{pmatrix}$

The same applies to matrix subtraction:

$\begin{pmatrix}4 & 2\\\ 1 & 6\end{pmatrix} - \begin{pmatrix}2 & 4\\\ 0 & 1\end{pmatrix}  = \begin{pmatrix}4 - 2 & 2 - 4 \\\ 1 - 0 & 6 - 1\end{pmatrix} = \begin{pmatrix}2 & -2\\\ 1 & 5\end{pmatrix}$


## Matrix-Scalar Products

^a844d0

A matrix scalar product multiplies each element of the matrix by a scalar. The follow example illustrates the multiplication:

 $2 \cdot \begin{pmatrix} 1 & 2\\3 & 4 \end{pmatrix} = \begin{pmatrix} 2 \cdot 1 & 2 \cdot 2\\ 2 \cdot 3 & 2 \cdot 4\end{pmatrix} = \begin{pmatrix} 2 & 4\\ 6 & 8\end{pmatrix}$

For reference, scalars are individual numbers that scale all elements in an matrix or a [[Vectors| vector]].


## Matrix-Matrix Multiplication

^441ff4

With Matrix-Matrix Multiplication, there are a few rules to be followed before you can perform it:

1. You can only multiply two matrices if the number of columns on the left-hand side matrix is equal to the number of rows on the right-hand side matrix.
2. Matrix Multiplication is not commutative which means that $A \cdot B \neq B \cdot A$

Multiplying 2 2x2 matrices would look like the following:

$\begin{pmatrix} 1 & 2\\3 & 4 \end{pmatrix} \cdot \begin{pmatrix} 5 & 6\\7 & 8 \end{pmatrix}= \begin{pmatrix} 1 \cdot 5 + 2 \cdot 7 & 1 \cdot 6 + 2 \cdot 8\\ 3 \cdot 5 + 4 \cdot 7 & 3 \cdot 6 + 4 \cdot 8\end{pmatrix} = \begin{pmatrix} 19 & 22\\ 43 & 50\end{pmatrix}$

To make sense of this, take a look at the following figure:

![[M-M Multiplication.png]]

As you can see for the red pathway, we apply normal vector multiplication on the pathway and add the products together. We continue to do this for the rest of the pathways in the matrix.

## Matrix-Vector Multiplication

^9ed9f2

A vector is basically a Nx1 Matrix, given that N is the number of components the vector has. Matrix-Vector Multiplication has a lot of applications when it comes to 2D/3D transformations and multiplying a matrix by a vector transforms the vector. 

### Identity Matrix

Most vectors happen to be of size 4. Because of this, we will work with 4x4 Matrices. The most simple transformation matrix we can use for transforming vectors is an identity matrix. The identity matrix is a NxN matrix that has only 0s except for along its diagonal. Below shows an example of an identity matrix multiplied by a size 4 vector, leaving it unharmed:

![[M-V Multiplication.png]]

As you can see the result is a vector that is completely untouched.

### Scaling

^5989f7

When we scale a vector, we increase the length of the vector by the amount we'd like to scale it, keeping the same direction. We can scale a vector where each individual scale factor is not the same, known as a non-uniform scale, or have the scalar the same across all axes, known as a uniform scale. 

Let's take a look at $\vec v = (3,2)$:

![[vectors_scale.png]]

In the above plane, we performed a non-uniform scale, scaling the x axis by 0.5 and the y axis by 2.

Using the above information, we can create a transformation matrix that can scale all 3 components of a vector. Below is an example of a matrix that does just so:

![[t-matrix.png]]\

If we were to change the components $(S_1, S_2, S_3)$ to 3, then we've created a transformation matrix that scales all components of the vector (except for the w-component 1) by 3.

### Translation

^c1f3df

Translation is the process of adding another vector onto another to return a new vector that is a different position. Like scaling a matrix, we can perform certain operations to translate a vector and that is by changing the top 3 values of the 4th column. With a vector $(T_x, T_y, T_z)$ we can define the translation matrix as so:

![[trans-matrix.png]]

**Note**: the w-component of a vector is known as a [[Homogeneous Coordinates & Projective Geometry|homogenous coordinate]].
In order for us to get a 3D vector from a homogenous vector we must divide the x, y, and z component by the homogenous coordinate (the w-component).

### Rotation

^95629b

#### Rotation along 2D
We can rotate a vector along any axis using a certain Transformation Matrix. Take a look at the following vectors:

![[Rotation.png]]

When we draw a right triangle from the 2 vectors, we'll notice that we know one side (the hypotenuse, which stays at length 1) but do not know the other two. In order for us to find these out, we have to use a bit of trigonometry.

From what we know, to get the opposite side of an angle $\Theta$, we have to use cosine, which is $\cos\theta = \frac {adjecent} {hypotenuse}$ which becomes $\cos\theta = \frac {adjecent} {1}$ as we know the hypotenuse is 1. If we simplify this, we can deduct that the adjacent side is equal to $cos \theta$. If we do the same for the opposite side, we will send up with the opposite being equal to $sin\theta$. This means that our transformation matrix will look something like so to start:

$\begin{pmatrix} cos\theta\\ sin\theta \end{pmatrix}$

Because we are in R2 space, we will be using a complete 2x2 matrix. Let's look at the following example:

![[RotationE2.png]]

If we draw a right triangle from the two vectors, we notice that our opposite is now on the horizontal axis and now pulling towards the negative axis. Because of this, the translation unit for the horizontal (x component) is now $-sin\theta$. Our Adjacent is now along the y-Axis, so it is now $cos\theta$. Because of this, our transformation matrix for rotating a vector is completed as:

$\begin{pmatrix} cos\theta & -sin\theta\\ sin\theta & cos\theta\end{pmatrix}$

#### Rotation along 3D

To perform rotations in 3D, we must first define different matrices for both rotating along the x-axis and rotating along the y-axis. 

To rotate along the x axis, we first have to define what components change when we rotate over certain axes.

If we look at our identity matrix, whenever we rotate along the x axis, things stay unchanged, rotating x changes nothing about vectors in the 3D space on the x-plane. So the two components that would be changed our z and y. Looking at a graph:

![[zy-graph.png]]

If we were to rotate the x, we'll notice how vectors on the z and y axes would rotate clockwise or counter clock wise depending on the angle. This means that the only calculations we would do are on y and z component of our matrix.

Just like we did with out 2D Rotation, we applying the transformations to the right components of the matrix:

$\begin{pmatrix} 1 & 0 & 0 \\ 0 & cos\theta & -sin\theta\\ 0 & sin\theta & cos\theta\end{pmatrix}$


To Rotate along the Y-Axis you would perform the same action, doing such action will give you this matrix:

$\begin{pmatrix} cos\theta & 0 & sin\theta \\ 0 & 1 & 0\\ -sin\theta & 0 & cos\theta\end{pmatrix}$

Viewing the below image and performing the operations we had previously will help understand the matrix that it had given (though it looks different than others).

![[z-x.png]]

## Combining Matrices

With matrix transformations, the most efficient thing you can perform with it is combining multiple transformations. Say for example the below transformations:

![[Trans.Scale.png]]

With this, if we wanted to scale a vector by $(2,2,2)$ and then translate it by $(1,2,3)$, We would perform the above operations.

With our final result being:

![[fresultmatrix.png]]



