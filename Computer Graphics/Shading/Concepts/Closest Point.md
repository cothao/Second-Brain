If we wanted to grab the closest point on a vector to another point, we can use the  following formula:

$\vec c = \vec {ro} + max(0, ((\vec p - \vec {ro}) \cdot \vec {rd})) * \vec rd$

Where ro is our ray origin, p is our point, and rd is our ray direction. 

We first calculate the dot product between the ray of the point from the origin and the ray direction, which should give us how how close or far the rays are from each other. We clamp this value with $max$ between 0 and 1 to ensure it doesn't stay negative. We then scale $\vec {rd}$ by the max value and then add the value to our center to get the closest point.