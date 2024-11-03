A projection matrix is a matrix that transforms all vertex data from the eye coords to the clip coords. Then these clip coords are transformed to NDC by dividing the clip coords by the w-component.

This means we have to keep in mind that clipping (frustum culling) and NDC transformations are integrated into the projection matrix.

The clipping is performed in the clip coords, right before dividing by $w$. The clip coords $x_c, y_c, z_c$ are tested by comparing them with $w$. 

![[gl_frustumclip.png]]
In perspective projection, a 3D point in the frustum (eye coords) is mapped to a cube (NDC); the range of x-coords from [l,r] to [-1,1] and z-coords from [-n, -f] to [-1,1]

![[gl_projectionmatrix01.png]]

The eye coords use what's called a right hand coordinate system, where the camera at the origin looks along the +Z axis in eye space. NDC uses the left hand coordinate system, where the camera looks along the -Z axis in eye space. What we need to do is negate this sign.

In Computer Graphics, a 3D point in eye space is projected onto the near plane (projection plane). Below is a diagram showing how a point in eye space $(x_e, y_e, z_e)$ in eye space is projected to the near plane $(x_p, y_p, z_p)$.

![[gl_projectionmatrix03.png]]

If we take a look at the above diagram, in order to map the point $x_e$ to $x_p$, we have to use the ratio of [[Similar Triangles|similar triangles]]:

First, we grab the points we know we want to map, we'll start with the x coordinates:

![[gl_projectionmatrix_eq01.png]]

We first take the similar triangles of the x and near plane. Then, we cancel out the $x_e$ value and add it to the right side. We then negate the sign on $-n$and give it to $-z_e$.

![[gl_projectionmatrix04.png]]

We then perform the same operation for y. 

![[gl_projectionmatrix_eq02.png]]

Notice how $x_p$ and $y_p$ are both divided by $-z_e$, after the eye coordinates are transformed by multiplying the projection matrix, the clip coordinates are still homogenous coordinates. They become normalized (NDC) after dividing by the w-component of the clip coordinates.

![[gl_transform08.png]]
(Transforming the eye coordinates to clip coordinates)

![[gl_transform12.png]]
(Transforming the clip coordinates to NDC by dividing by its w-component)

This now means that we can set the w-component of our clip coordinates to $-z_e$ as this is what we will divide by:

![[gl_projectionmatrix_eq03.png]]

Next, we want to project the $x_p, y_p$ coordinates to $x_n, y_n$ of <abbr title="Lower left is 0,0. Top right is 1,1">NDC</abbr> with [[Linear Relationships|linear relationships]]; [l,r] => [-1,1] and [b,t] => [-1, 1].

![[gl_projectionmatrix05.png]]

The equation goes as follows:

![[gl_projectionmatrix_eq04.png]]

First, we map the linear relationships. The linear relationship of two points is represented with the equation y = mx+b where $m=\frac {(x2​−x1​)}{(y2​−y1​)}$ which gives us:

$m=\frac {(1​−(-1​)}{(r​−l​)}$

$x = x_p$ 

$B = y-intercept$

We then substitute $(r,1)$ for $(x_p, x_n)$ and solve for $b$.

After we solve for $b$ we are left with out final equation.

We then do the same for mapping $y_p$ to $y_n$:



![[gl_projectionmatrix_eq05.png]]



After getting these equations, we substitute $x_p$ and $y_p$:

![[gl_projectionmatrix_eq07.png]]


After simplifying and getting the answer we desire, we'll get the system of equations that we can input into our 1st and 2nd rows of the matrix:

![[gl_projectionmatrix_eq08.png]]


Find the 3rd row is a little tricky. $z_n$ will be hard to find because $z_e$ in eye space is always projected to $-n$ on the near plane (refer to the perspective frustum). We need a unique z-value for clipping and depth tests. To find the 3rd row, we have to use the w-component as z does not rely on an x or y value. So we would have to specify the 3rd row as follows:

![[gl_projectionmatrix_eq10.png]]

Because in eye space, $w_e = 1$, our equation becomes:

![[gl_projectionmatrix_eq11.png]]

We now have to find coefficients A & B, so we'll use the linear relationship ($z_e, z_n$): $(-n, -1) and (-f, 1)$. 

![[gl_projectionmatrix_eq12.png]]

To solve A & B, first rewrite equation 1 to solve for B:

![[gl_projectionmatrix_eq13.png]]

Then, substitute equation 1 onto B in equation 2, and then solve for A:

![[gl_projectionmatrix_eq14.png]]

First, what we do is add n to both sides.

$−Af+An−n+n=f+n$

$−Af+An=f+n$

$-f$ and $n$ have a common variable, so we factor it out (A).

$-(f - n)A = f + n$

Now we can divide both sides by $-(f-n)$ and get our answer.

$A = \frac {f + n}{-(f - n)}$

And then we put the equation into B we solve for $B$:

![[gl_projectionmatrix_eq15.png]]

First, we can multiply both sides by $f - n$:

$-2fn = Bf - Bn$

Flip the equation:

$Bf - Bn = -2fn$

Factor out B:

$B(f - n) = {-2fn}$ 

And divide by $f-n$:

$B = \frac {-2fn}{f - n}$

Now that we've found A and B, the relation between $z_e$ and $z_n$ is:

![[gl_projectionmatrix_eq17.png]]

Now that we've found all entries, our complete matrix is:

![[gl_projectionmatrix_eq16.png]]
