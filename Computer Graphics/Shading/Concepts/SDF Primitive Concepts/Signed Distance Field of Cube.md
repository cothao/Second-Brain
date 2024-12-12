Let's imagine we have a square in our scene and an arbitrary point that we want to test.

![[cube_raymarch_1.png]]

To grab the signed distance of a cube or square, we want to grab the distance our point is from the cube. To do this, we have to first grab the x and y values (vertical distance and horizontal distance) from the cube.

![[cube_raymarch_2.png]]

Where D (our hypotenuse)  the distance from the nearest surface.

To start, we can retrieve the X by solving for how far the point is from the surface horizontally. This is done by getting the absolute value of point P's x coordinate and subtracting the radius from this value. This can be done with the y as well and would look something like this:

```
vec3 sq = abs(p) - s;
```

where s is the cube vector, and we grab the absolute value oof the vector to have a vector of all the distances (x and y)

Now all we have to do to grab the hypotenuse is grab the length of vector (x,y):

```
float d = length(abs(p) - s);
```

So we have our length, great. But we still run into some issues. Take for example the bottom image:

![[cube_raymarch_3.png]]

In the above image, the value of y is negative because we are inside the cube vertically. Our y-distance will end up being negative as there is less distance than the length of the radius. So to fix this, we have to ensure the distance never goes below 0:

```
float d = length(max(abs(p) - s, 0.0));
```

Our entire function will look like so:

```
float SDCube(vec3 p, float s)
{

	return length(max(abs(p) - s,0.0));

}
```

