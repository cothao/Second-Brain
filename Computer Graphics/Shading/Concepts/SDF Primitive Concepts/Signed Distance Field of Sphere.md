The signed distance field of a sphere is the easiest of the signed distance functions for 3d shapes that we get into.

To implement it, we have to first imagine our point and a circle in a distance.

![[circle_raymarch_1.png]]
Where P is our point, we want to grab the vector between C and A, which would look like:

```

vec3 dist = a - p;

```

After we do this, we want to grab length of this vector:

```
float d = length(dist);
```

Now this is good, but our issue is that this will give us the length from the point to the center of circle, which is not what we want. We want to grab the length from the point to the surface of the circle and to do so we have to subtract the radius.

![[circle_raymarch_2.png]]

If we subtract the radius, we'll get a length that is from vector P to the surface of A:

![[circle_raymarch_3.png]]

The full code implementation looks like so:

```
float SDCircle(vec3 p, vec4 s)
{

	return length(p - s.xyz) - s.w;

}
```

We grab the length of the vector and make s a 4 component vector to use the w component as the radius, which we subtract from our length to get the distance to the surface rather than the center of the circle.