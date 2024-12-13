Creating a cylinder follows the same concept as creating a capsule, but this time we want to cap our ends with flat endings. Let's look at the concept first.

![[cylinder_raymarch1.png]]

If we have a point P, what we want to do is find the distance of P to the closest surface on the cylinder. This distance is represented as E. To do so, we must first find X and Y.

If you followed along in [[Signed Distance Field of Capsule]], you would know the distance to the surface is represented as:

```
float d = length(p - c) - r;
```

Where c is the center, p is our point and r is our radius. Because this is the straight horizontal distance, we can use this value as our X. 

Now the Y component is a little tricky. We want to make sure that our Y-distance from the cylinder is correct. So what we do is we take the absolute value of the distance so that the negative values overlap with the positive. We then subtract .5 from this value and then .5 again from the latest result to get our capped value, making sure the y distance is negative on the inside and positive on the outside. This looks something like this:

```
float y = (abs(d) - 0.5) - 0.5;
```

Now this is great but this value is still normalized between the length of AB. We have to un-normalize it by multiplying it by the length of AB:

```
float y = ((abs(d) - 0.5) - 0.5) * length(ab);
```

Now that we have our x and y, we can work on getting our e value.

It's as simple as getting the length of the vector (x,y) but with some extra steps. Similar to the cube (see [[Signed Distance Field of Cube]]), when the x or y is negative, we want to make sure we get the absolute value of the distance as this will give us the true distance from the cylinder.

```
float e = length(max(vec2(x,y), 0.0));
```

Now that we have this, we'll get our cylinder, but we want to make sure we also get the right distances on the inside. Now if we don't test any distance on the inside of the cylinder, it'll look wonky. 

![[cylinder_raymarch2.png]]

To fix this, we have to make sure that we are staying as close to zero as possible, we grab the largest of the two components x & y so that we grab the number closest to 0. We also grab the number less than or equal to 0 as we only want to provide this test and make sure distances inside the cylinder are the only ones being tested:

```
float i = min(max(x ,y), 0.0);
```

And we are done, the entire code looks like so:

```
float SDCylinder(vec3 p, vec3 a, vec3 b, float r)
{

	vec3 ab = b - a;
	vec3 ap = p - a;
	float d = dot(ab, ap)/dot(ab,ab);

	vec3 c = a + d * ab;

	float x = length(p - c) - r;

	float y = ((abs(d) - 0.5) - 0.5) * length(ab);

	float e = length(max(vec2(x, y), 0.));

	float i = min(max(x, y), 0.0);

	return e + i;
	
}
```