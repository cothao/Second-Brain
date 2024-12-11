Raymarching is a rendering technique that is primary used with shaders (GLSL & HLSL). The technique involves shooting a ray from our camera, similar to creating simple 3D as we have earlier (see [[Creating 3D]]) and creating distance fields that are able to detect where an object is and trace that path and distance back to the camera to render it.

# How it works

Imagine our basic setup as this:
![[raymarch_example1.png]]
Just like creating 3D, we have our camera which we always do and our ray direction (View Ray) which will be determined by our intersection point. We then use these two vectors to determine our distance from an object, at which that distance value is what will be a component to what determines the color of that fragment.

First, we want to get the intersection point from the object. But before that, we want to grab the closest point from our camera to our scene.

![[raymarch_example2.png]]

We make a distance field starting from our camera to retrieve the closest point. From our vector, we plot our point forward from that closest point distance. We do this to test our surroundings, checking to see if we are close to any objects

![[raymarch_example3.png]]

We continue to do this until we have a distance field that is so small that we count it as a hit to the object.

The code for the raymarch looks something like this:

```
float RayMarch(vec3 ro, vec3 rd)
{

	float dO = 0.;

	for (int i = 0; i < MAX_STEPS; i++)
	{

		vec3 p = ro + dO * rd;

		float ds = GetDist(p);

		dO += ds;

		if (ds < SURFACE_DIST || dO > MAX_DIST) break;

	}

return dO;

}
```


First, we make our Distance from the origin (dO). Then after, we have our for loop that runs up until a certain number of steps that we set. In the for loop, we calculate our point (p) from the closest distance from the scene and then create a distance field to the next closest point in the scene (ds). With this, we then add that distance to our distance from the origin and return the distance from the origin, which will ultimately give us how far we are from that object.

Now the GetDist function from above has a few parameters. Take a look at this image:

![[raymarch_example4.png]]


The GetDist function returns us the distance we are currently from an object. In the following image, we have our camera and we have a sphere. What we want to do is grab the distance from the sphere, calculated as:

$dS = (\vec{p} - \vec{spherePos}) - radius$

where p is our point that we are subtracting the spherePosition from to get the distance from the sphere, and we then subtract the radius as the position is in the center of the sphere and we really want the distance from the sphere surface. 

We also need the distance from the plane which for axis-aligned objects is just the point y position as the plane will always be "y" away from the point.

We then return the minimum of the distance to the scene and distance to the plane as we want whichever is closest to render, giving us this function:

```
float GetDist(float p)
{

	vec4 sphere = vec4(0., 1., 6., 1.); // w is our radius

	float ds = length((p - sphere.xyz) - sphere.w);

	float dp = p.y;

	float d = min(dp, ds);

	return d;

}

```

Plugging this into our code gives us a scene that looks like this:

![[raymarch_example5.png]]

The sphere is at the position we specified, and it even draws out the plane, showing how the code has worked. Of course this isn't complete and mostly just conceptual to understand how ray marching works, but feel free to play around with it how you like.