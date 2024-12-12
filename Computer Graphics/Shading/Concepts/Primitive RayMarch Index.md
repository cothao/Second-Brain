# <u>Table of Contents</u>

[[#^995d21|Sphere]]
[[#^c98a61|Cube]]
[[#^6181ba|Torus]]
[[#^e62da9|Capsule]]
[[#^5989f7|Cylinder]]



# [[Signed Distance Field of Sphere|Sphere ]]

^995d21

![[sphere_sdf.png]]
```
float SDSphere(vec3 p, vec4 s)
{

	return length(s.xyz - p) - s.w;

}
```

# [[Signed Distance Field of Cube|Cube ]]

^c98a61

![[cube_sdf.png]]
```
float SDCube(vec3 p, float s)
{

	return length(max(abs(p) - s, 0.0));

}
```

# [[Signed Distance Field of Capsule|Capsule ]]

^e62da9

![[capsule_sdf.png]]
```
float SDCapsule(vec3 p, vec3 a, vec3 b, float r)
{

	vec3 ab = b - a;

	vec3 ap = p - a;

	float d = clamp(dot(ap, ab)/dot(ab,ab), 0., 1.);

	vec3 c = a + d * ab;

	return length(p - c) - r;

}
```

# [[Signed Distance Field of Torus|Torus ]]

^6181ba

![[torus_sdf.png]]
```
float SDTorus(vec3 p, vec2 r)
{

	float x = length(p.xz) - r.x;

	float y = p.y;

	float d = length(vec2(x,y)) - r.y;

	return d;

}
```