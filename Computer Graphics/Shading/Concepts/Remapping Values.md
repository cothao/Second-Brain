Remapping values is a very important concept in shaders as it allows us to attenuate values or remap to another domain.

To remap values, we first want to normalize our values between a range of 0 and 1. The equation for that will be:

$r = \frac {t - a} {b - a}$

where t is the value we want to normalize, $a$ is our current range start, and $b$ is our range end.

Using the formula, if our range was (-.5, .5), when t is -.5, it will return 0, and when t is .5, it will return 1. In code, this would look like this:

```
float remap01(float a, float b, float t)
{

    return (t - a) / (b - a);

}
```

This is our first step to remapping to the values that we want. Next, we have to then remap our normalized values to the range that we are looking for. The equation for this would look like so:

$v = r \times (d - c) + c$

where $r$ is our previously mentioned formula, $d$ is our end number, and $c$ is our start number. Taking a closer look at this, we want the total range of our numbers, so we subtract $c$ from $d$ to get the number we want to start at. We then add $c$ last, ensuring a value of 0 would remap to the beginning of our range. The code for this looks like so:

```
float remap(float a, float b, float c, float d, float t)
{

    return remap01(a, b, t) * (d - c) + c;

}
```