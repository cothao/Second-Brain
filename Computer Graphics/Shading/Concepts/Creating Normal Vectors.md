
Normal vectors are unit length vectors that are perpendicular to the surface of an object. They are extremely important in things such as lighting calculations.

To implement the creation of a normal vector, we first need a point we are checking. This point is typically where our point is in a raymarch. We want to use this point to create the distance that point is current from the nearest surface:

```
float d = GetDist(p);
```
(If you are unfamiliar with how to obtain the distance of a point to the nearest object surface, please see [[Simple Raymarching]] before continuing)

After we grab the distance, we want to create a vector that will be used for grabbing similar values around our point by subtracting the p from this vector.

```
vec2 e = vec2(0.1, 0.);
```

Now, we create our normal vector. This is done by subtracting our vector that is close to the point with the distance. We'll retrieve the distance of each new vector to use the values as the x, y, and z components of our vector.

```
vec3 n = d - vec3(
	GetDist(p - e.xyy),
	GetDist(p - e.yxy),
	GetDist(p - e.yyx)
);
```

We also make sure to subtract the distance from the vector, giving us our normal vector.

There are times when the vector falls out of being a unit length vector, so we make sure to normalize it:

```
normalize(n);
```

Our end function looks like so:

```
vec3 GetNormal(vec3 p)
{

	float d = GetDist(p);

	vec2 e = vec2(.1, .0);

	vec3 n = vec3(
		GetDist(p - e.xyy),
		GetDist(p - e.yxy),
		GetDist(p - e.yyx),
	);

	return normalize(n);

}
```

