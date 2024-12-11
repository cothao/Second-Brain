**BEFORE YOU FOLLOW ALONG** - if you haven't already, make sure you understand basic raymarching and the math behind it. You will be lost if you don't. This is more so a follow up to my note [[Simple Raymarching]]. This is also very similar to how we implement the Phong model (in [[Phong Model]]). See that if you haven't already.

After creating a simple scene with a simple sphere, we want to make things look more realistic. Currently without lighting, a simple raymarch scene with a sphere would look like this:

![[raymarch_example5.png]]

A little foggy, but that's because we have no light logic. Let's implement it.

To implement lighting, we have to imagine a light is shooting hundreds of rays (or vectors) in the direction of our object. The image below demonstrates the concept:

![[lighting_example1.png]]

The light shoots vectors in the direction of our object. We then take this vector and compare it to the objects vector normals, grabbing the difference in angle. The color is then calculated by the angle at which the light vector hits our objects surface. 

But how do we calculate this?

First, we have to create the light. We just create a vector that is in our desired light position:

```

vec3 lp = vec3(0., 6., 6.);

```

We then have to create our light direction vector. This is done by subtracting the position in our scene the pixel is at (our point) from the light position:

```
vec3 lv = normalize(lp - p);
```

We also normalize it so that it stays a unit vector, ensuring there are no miscalculations.

After this, we have to create our normal vector.

The normal vector is a vector that is perpendicular to the surface area, and this is calculated per point. There is a note explaining how to implement creating a normal vector, so you can head [[Creating Normal Vectors |here]] if you're lost.

The value would look like so:

```
vec3 n = GetNormal(p);
```

Now that we have our normal, we want the difference in angle between our light direction vector and the normal vector on the object. Below is the implementation using the dot product:

```
float d = dot(n, lv);
```

And lastly, we will clamp this number between 0 and 1 because the dot product can be in the negatives if the angle is too large:

```
d = clamp(d, 0., 1.);
```

and we return the value, the entire function looks like so:

```
float GetLight(p)
{

	vec3 lp = vec3(0., 6., 6.);
	vec3 lv = normalize(lp - p);
	vec3 n = GetNormal(p);
	float d = dot(lv, n);
	return clamp(d, 0., 1.);
}
```

# Adding Shadows

Adding shadows now is fairly simple. If we imagine a point that's on the plane where a shadowed pixel should be, we want to measure the length of that point to the nearest object, which can be accomplished through ray marching from our point in the direction of our light vector. It will stop at the lower half surface of our object as that's as far as it can go, and return to us the distance from that point to the object.

We then want to compare this value with the distance from our light position to our point and if the ray march distance is smaller than our distance from the point to the lights position, we want to make that fragment darker as that means that it's under the object. After this, we want to attenuate this value by the normal and some smaller value as adding the normal will allow the fragments new value to adjust based off the position of the point from the object.

Let's first create our ray march to march from the point in the direction of our light vector:

```
float s = RayMarch(p, lv);
```

Then we compare this to the length of our point to the light position and decrease the fragment color based on if the RayMarch distance is smaller:

```
if (s < length(p - lp)) d *= .1;
```

Let's go back to our "float s" and attenuate it based on the normals:

```
float s = RayMarch(p + n * 0.01 * 2., lv);
```

The entire code will look like this:

```
float s = RayMarch(p + n * 0.01 * 2., lv);
if (s < length(p - lp)) d *= .1;
```

And the result should be:

![[lighting_example2.png]]
