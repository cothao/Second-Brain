To get the signed distance field of a torus, we have to make make two radius, one for the inside and one for the outside.

![[torus_raymarch_1.png]]

The dot below the point will represent how far on the xz plane we are from the torus, as we want to eventually grab the distance from it using x and y values. To do that we'd just grab our x and z components of our point for the x and subtract the radius to make sure we are on the surface of the circle:

![[torus_raymarch_3.png]]

The y is the points (P) y-coordinate (as long as it's an axis-aligned plane).

![[torus_raymarch_2.png]]

We then want to grab the length of our vector as this will give us the D component. After that we simply subtract the second radius. This looks like so in code:

```
length(vec2(x,y)) - r2;
```

The entire function looks like so:

```
float SDTorus(vec3 p, vec2 r)
{

	float d = length(p.xz) - r.x;

	float y = p.y;

	return length(vec2(x,y)) - r.y;

}
```