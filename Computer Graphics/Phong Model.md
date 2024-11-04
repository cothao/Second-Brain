
**This section requires a basic understanding of vectors, please see [[Vectors]] if you're having any trouble**
# Table of Contents
-  Ambient
-  Diffuse
-  Specular

Lighting in computer graphics is based on the approximations of reality using simplified models that are easier to process. Within the Phong model exists 3 components:

**Ambient Lighting**: even when it is dark there is usually still some light somewhere in the world (the moon, a distant light) so objects are almost never completely dark. To simulate this we use an ambient lighting constant that always gives the object some color.

**Diffuse Lighting**: simulates the directional impact a light object has on an object. This is the most visually significant component of the lighting model. The more a part of an object faces the light source, the brighter it becomes.

**Specular Lighting**: simulates the bright spot of a light that appears on shiny objects. Specular highlights are more inclined to the color of the light than the color of the object.

![[basic_lighting_phong.png]]
(The image above shows an example of the 3 types of light as well as the combined (Phong) version of them)


# Ambient Lighting

Ambient Lighting is a simple lighting algorithm that creates a color when no light is shown. The algorithm is simple:

$\vec f = a \times \vec l$

where $\vec f$ is the final output, $a$ is the ambient strength that we apply, and $\vec l$ is the light color, meaning that if the light color was red $(1., 0., 0.)$ and our ambient was $a = 0.1$, then the resulting ambient color will be $(.1, 0., 0.)$.

