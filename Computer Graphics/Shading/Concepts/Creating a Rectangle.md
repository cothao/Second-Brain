 To create a rectangle in GLSL, we first have to create a function for creating a band, which involves smoothstepping (see [[GLSL Functions]] for more info).

It's important to recognize how the smoothstep function looks on a graph, as it interpolates between the given x and y coordinate.

![[smoothstep.png]]

With this we can create a function that has a smoothstep (for now)

```
function Band(float t, float start, float end, float blur)
{

	float step1 = smoothstep(start - blur, start + blur, t)

	return step1;

}
```

We use argument t to act as our value to check, a start to specify where to start, end to specify where to end, and blur to manage how much blur or horizontal interpolation we have.

We can finish the function by adding a second smoothstep function and return the product of the two functions

```
function Band(float t, float start, float end, float blur)
{

	float step1 = smoothstep(start - blur, start + blur, t)

	float step2 = smoothstep(end + blur, end - blur, t);

	return step1 * step2;

}
```

The reason why we start with adding blur instead of subtracting the blur is because we want the smoothstep to go down, basically reverse of the first graph.

![[invert_smoothstep.gif]]
(The blue represents the inversion that we want)

Calling this function gives us a band with black on the sides.

Now that we've created this band, we want to make a function that creates a rectangle from two bands!

```
float Rect(vec2 uv, float left, float right, float bottom, float top, float blur)
{

    float band1 = Band(uv.x, left, right, blur); 
    
    float band2 = Band(uv.y, bottom, top, blur); 
    
    return band1 * band2;

}
```

Above is our completed Rect function. It takes in the uv coordinates that we'll use for positioning the rectangle, left, right, bottom, and top for how much size we want on each side, as well as a blur to give us how much blur we want. We then return the product of the two bands to give us our rectangle.