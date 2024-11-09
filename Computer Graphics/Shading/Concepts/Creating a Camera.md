*This note follows up directly after  "[[Creating 3D]]". Please see that note before continuing.*

When creating a camera for perspective in GLSL, we have to consider a few factors. When we create 3d, we're using a camera at an arbitrary point behind the screen and then getting the ray direction of the camera (ray origin) from the intersection point of the screen. This point will always be represented as some point that is $x$ distance away to the right of the center and $y$ distance up from the center. This is our first step in making our screen perspective change. Now to grab this changed intersection point when the camera moves is given by the following formula:

$i = c + x * rv + y * uv$

where rv is the right vector and uv is the up vector.

Now how do we get the right and up vectors?

Well, let's focus on what we know.

We know that we can create a forward vector (our z vector) from getting the lookat vector (where we want the camera to look) minus the ray origin:

$\vec fv = \vec {lv} - \vec {ro}$

with this, we can calculate our right and up vectors.

Following vector products (see [[Vectors]]), we know that the cross product can give us a vector orthogonal to two given vectors. While we only have the forward vector for now, one vector we know for sure is orthogonal to it is the world up vector $(0. , 1., 0.)$. We can use this vector to give us our right vector:

$rv = (0., 1., 0.) \times fv$

and now that we have the right vector, we can solve for our camera up vector:

$\vec uv = \vec {rv} \times \vec {fv}$

and this will give us our last vector that we need for the equation.

Now all we have to do is solve for c (which is our center). And to accomplish this, we just have to take our forward vector and add the ray origin and multiply by a zoom factor:

$c = \vec {fv} + \vec {ro} \times zoom$

with this our equation is complete. Now we solve for i and subtract the ray origin (ro) from it as usual:

$\vec {rd} = \vec i - \vec {ro}$

And we are complete! The complete (somewhat) code for the camera looks something like this:

```
    vec3 la = vec3(.5); // lookat vector
   
    vec3 fv = normalize(la - ro); // normalize our forward vector to keep it within unit vector range
       
    vec3 wu = vec3(0., 1., 0.); // world up vector
       
    vec3 rv = cross(wu, fv); // cross product between world up and forward vector to get righ vector
       
    vec3 cu = cross(fv, rv); // cross product between forward vector and right vector to get camera up vector
       
    float zoom = 1.; // zoom factor
       
    vec3 c = ro + fv * zoom; // center; ray origin + forward vector times the zoom
       
    vec3 i = c + uv.x * rv + uv.y * cu; // equation for i
       
    vec3 rd = i - ro;
       
```