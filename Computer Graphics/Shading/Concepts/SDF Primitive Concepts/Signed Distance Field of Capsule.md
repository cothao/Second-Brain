A capsule is a pretty simple concept as it only involves two spheres and connecting the two.

To start, let's take a look at the below image.

![[capsule_raymarch_1.png]]

Say we have our point and our two spheres. What we want to do is get the distance of our point from our two spheres as well as the distance to the distance of the spheres. Say that twice as fast. 

We first have to grab the vector of both A to B and A to P.

![[capsule_raymarch_2.png]]

Grabbing these vectors is the result of subtract the target vector with the base vector (i.e. B - A).

Now that we have these vectors, what we want to do is make sure that our point is capped at the distance of AB, because if not, then our capsule won't go from A to B as expected. To do this, we have to grab the dot product of AB and AP and project the vectors. If the value is less than 0, it's closer to A and if it's more than 1 it's closer to B

```
float d = dot(ap, ab)/dot(ab, ab);
```

Now this is good, but the values can still become more than we need, causing the capsule to move on infinitely. We want to cap our value from 0 to 1 because the vectors may not be normalized.

```
float d = clamp(dot(ap, ab)/dot(ab,ab), 0., 1.);
```

We then want to calculate a point on the axis of AB that is closest to our point p. The below formula performs this action:

```
vec3 c = a + d * ab;
```

And finally, we calculate the distance from our point to that closest point.

```
length(p-c) - s;
```

the reason why we subtract s is because we want the surface and not the center of the capsule, s being our radius.

The complete code looks like so:

```
float SDCapsule(vec3 p, vec3 a, vec3 b, float s)
{

	vec3 ab = b - a;
	vec3 ap = p - a;

	float d = clamp(dot(ab, ap)/dot(ab, ab), 0., 1.);

	vec3 c = a + d * ab;

	return length(p-c) - s;

}
```

