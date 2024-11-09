In GLSL, creating 3D Scenes require a fundamental knowledge of linear algebra. Let's start with the concepts first.

Typically, what we'll have is a camera. We want a camera because we want it to shoot out rays into our virtual world. So we'd have to make a camera position.

We then also want the point of intersection (where the camera ray has intersected the screen) as well as the color of the object we hit in the scene if we hit an object.

![[camera_example.png]]
(Here we have our camera, it intersects the screen and if a ray touches an object then it returns to us its color).

So in order to get the direction of our ray from the camera to the screen, we have to convert our uv coordinates to rays (point to ray). 

# Let's start implementing this!

In GLSL, what we can do is we can make a vector first that represents the camera (or ray origin):

```
vec3 ro = vec3(0., 0., -2);
```

We say -2 for the z because we want the camera to be 2 units away from the screen.

Now to get the direction of our ray (or at which point we intersect the screen from our camera), we have to subtract the ray origin from the intersection point:

```
vec3 i = vec3(uv.x, uv.y, 0.); // intersection point
vec3 rd = i - ro; // get our ray direction
```

Now that we have the direction, we want to move our ray direction to a point in the 3D space that we specify and test it against all the ray direction. 
![[Distance_of_ray_to_point.png]]
In the above visual, we have our ray direction and what we want to do is translate it to our point. As you can see, what it does is it creates a parallelogram when connecting the lines. This parallelogram will help us in finding the height (ray direction distance from point p). Now the area of a parallelogram is denoted by the length of the cross product of the ray to point vector (ROP) and the base (Ray Direction):

$||\vec {ROP} \times \vec {RD}||$ 

Another way  would be the base times the height(distance):

$||\vec {ROP} \times \vec {RD}|| = b \times h$

Knowing what we know, we know that the base is the length of our Ray Direction ($\vec {RD}$), so our equation would look like this:

$||\vec {ROP} \times \vec {RD}|| = ||\vec{RD}|| \times h$

With this, we can cancel out RD and solve for h:

$\frac{||\vec {ROP} \times \vec {RD}||} {{\vec {RD}}} = h$

And this equation will help us in finding our distance (or height). Now the entire implementation looks like this:

```
float Distance(vec3 ro, vec3 rd, vec3 p)
{

	return length(cross(p - ro, rd))/length(rd) // our length formula

}

void main()
{

	vec3 ro = vec3(0., 0., -2.); // our camera

	vec3 i = vec3(uv.x, uv.y, 0.); // our point of intersection

	vec3 rd = i - ro; //grab the direction of our ray

	vec3 p = vec3(0., 0., -2); // our point to test

	float d = Distance(ro, rd, p);

	fragColor = vec4(d);

}

```