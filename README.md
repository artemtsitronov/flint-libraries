# Flint Libraries

A collection of libraries for the Flint programming language.
By Artem Tsitronov and Soumalya Das.

For now, only the math.fl library is implemented.
All the libraries are written in Flint.

## Math.fl

### Functions
 
| Function | Notes |
| --- | --- |
| `exp(x)` | e^x |
| `log(x)` | natural log; `log(0)` is `-inf`, `log(-1)` is `nan` |
| `sin(x)`, `cos(x)`, `tan(x)` | radians |
| `asin(x)`, `acos(x)` | `nan` outside [-1, 1] |
| `atan(x)` | result in (-pi/2, pi/2) |
| `atan2(y, x)` | result in [-pi, pi], handles zeros and infinities |

### Exposed constants

```
export const math_inf = 1e308 * 10
export const math_nan = math_inf - math_inf

export const math_pi      = 3.141592653589793
export const math_tau     = 6.283185307179586      # 2*pi
export const math_pi_2    = 1.5707963267948966     # pi/2
export const math_pi_4    = 0.7853981633974483     # pi/4
export const math_1_pi    = 0.3183098861837907     # 1/pi
export const math_2_pi    = 0.6366197723675814     # 2/pi

export const math_e       = 2.718281828459045
export const math_ln2     = 0.6931471805599453
export const math_ln10    = 2.302585092994046
export const math_log2e   = 1.4426950408889634     # 1/ln2
export const math_log10e  = 0.4342944819032518     # 1/ln10

export const math_sqrt2   = 1.4142135623730951
export const math_sqrt1_2 = 0.7071067811865476     # 1/sqrt2

export const math_deg2rad = 0.017453292519943295   # pi/180
export const math_rad2deg = 57.29577951308232      # 180/pi

export const math_epsilon = 2.220446049250313e-16      # gap between 1 and the next double
export const math_max     = 1.7976931348623157e308     # largest finite double
export const math_min     = 2.2250738585072014e-308    # smallest normal double
export const math_tiny    = 5e-324                     # smallest subnormal double
```

### Limitations

- `sin`, `cos` and `tan` return `nan` for `|x|` above about 1.6e6.
- All names live in one global table (Flint doesn't have private)
- `trig_reduce` returns its results through the globals `trig_n`, `trig_y0` and `trig_y1`, so the trig functions are not reentrant.

### Tests
 
`test_usage.fl` prints results for every function, including edge cases (subnormals, infinities, NaN, huge trig arguments) and a set of exact `==` checks.
