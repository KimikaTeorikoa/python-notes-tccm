---
jupytext:
  text_representation:
    extension: .md
    format_name: myst
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

# Useful libraries for scientific computing

One of the strongest points of Python is the flourishing *ecosystem* of libraries it 
comes with. We have already seen some of them, such as [`numpy`](numpy.md) and
 [`matplotlib`](plotting.md). This chapter reviews other libraries that are handy 
to code scientific computing applications, including computational chemistry ones.
We will mostly focus on `scipy`, highlighting some of its submodules that provide 
a huge set of numerical algorithms, and also briefly mention other projects that
 you will likely find useful.
The classification of these libraries as integral components of Python's core or
 specialized tools might provoke debate, yet you'll undoubtedly benefit from
 the diverse array of supplementary features accessible across various layers. 
![ecosystem](https://jupytearth.org/_images/python-stack.png)

## `scipy` 

This module contains a collection of numerical algorithms such as integration,
optimization, interpolation, linear algebra, statistics, and much more.
It is built on top of `numpy`, i.e., it mainly uses numpy arrays as the main
data structure.

`scipy` is organized in submodules, each one with a specific purpose, which can be imported separately as,

```python
import scipy.submodulename
#or
from scipy import submodulename
```

The submodules that normally fulfill the needs of a computational chemist are:

- `integrate`: Integration and ordinary differential equation solvers
- `interpolate`: Interpolation and smoothing splines
- `optimize`: Optimization and root-finding routines
- `linalg`: Linear algebra, which actually provides an interface to BLAS and LAPACK libraries.
Note that it generally supports all `numpy.linalg` functions, and `scipy.linalg` versions are preferred.

In this chapter we will focus on the first three submodules. The list of submodules is more extensive,
including `fft` (Fast Fourier Transform), `special` (special functions, such as Hermite polynomials). 
A complete list can be found in the [official documentation](https://docs.scipy.org/doc/scipy/reference/).

### `scipy.integrate`

This submodule provides several integration routines, including an ordinary 
differential equation integrator.

**Integration** of a 1D function, can be done with the `quad` method. It takes a function
and the integration limits as arguments, and returns the integral and an estimate of the error.
Let's see an example:
    
```{code-cell} python
from scipy.integrate import quad
import numpy as np

def gaussian(x, mu, sigma):
    return 1/np.sqrt(2*np.pi*sigma**2)*np.exp(-(x-mu)**2/(2*sigma**2))

mu = 0
sigma = 1
norm, err = quad(gaussian, -np.inf, np.inf, args=(mu, sigma))
print(norm)
```

Another method to integrate 1D functions is `fixed_quad`.

Instead, integration of a discrete function (1D), i.e., a set of points,
can be done with the `trapezoid`, `romb` and `simpson` functions. In the case, the
functions take as arguments the `x` and `y` arrays with the grid and function values, 
and return the integral.
For instance,

```{code-cell} python
from scipy.integrate import simpson
import numpy as np

def gaussian(x, mu, sigma):
    return 1/np.sqrt(2*np.pi*sigma**2)*np.exp(-(x-mu)**2/(2*sigma**2))

x = np.linspace(-100, 100, 5000)
mu = 0
sigma = 1
y = gaussian(x, mu, sigma)
print(simpson(y, x=x))
```

```{exercise}
:nonumber:
:class: dropdown

Write a program to check the orthogonality of the vibrational eigenfunctions of the
harmonic oscillator.

*Hint*: The eigenfunctions of the harmonic oscillator can be written as:

$$
\psi_n(Q) = 
\frac{1}{\sqrt{2^n n!}} 
\left(\frac{\omega}{\pi\hbar}\right)^{1/4} 
e^{-\omega Q^2/2\hbar} 
H_n\left(\sqrt{\frac{\omega}{\hbar}}Q\right)
$$
where $H_n$ are the Hermite polynomials, which can be evaluated with the function
`scipy.special.eval_hermite`.

```

Functions for multidimensional integration are also available, such as `dblquad` (double integral),
`tplquad` (triple integral) and `nquad` (integration over multiple variables).

This submodule also provides methods to integrate **ordinary differential equations**. 
The recommended method is `solve_ivp` (solve initial value problem),
which gives an interface to different integration algorithms.
As an example, consider a **harmonic oscillator**: a particle of mass $m$ attached to a
spring with force constant $k$. Newton's equation, $m\,\ddot{x} = -kx$, is a second-order
equation, but `solve_ivp` only handles first-order ones. The standard trick is to use the
velocity, $v = \dot{x}$, as a second variable, so that the *state* of the oscillator is the
pair $(x, v)$ and the equations of motion become

$$
\begin{align}
\frac{dx}{dt} &= v \\
\frac{dv}{dt} &= -\frac{k}{m}\,x
\end{align}
$$

Starting from rest at $x(0) = 1$, the exact solution is $x(t) = \cos(\omega t)$, with
$\omega = \sqrt{k/m}$. We can integrate these equations with the following code,

```{code-cell} python
from scipy.integrate import solve_ivp
import numpy as np
import matplotlib.pyplot as plt

def harmonic(t, state, m, k):
    x, v = state            # unpack the state vector
    dxdt = v
    dvdt = -k/m*x
    return [dxdt, dvdt]

m = 1.0                     # mass
k = 1.0                     # force constant
state0 = [1.0, 0.0]         # initial position and velocity
t0, tf = 0, 10
t_eval = np.linspace(t0, tf, 100)

sol = solve_ivp(harmonic, [t0, tf], state0, t_eval=t_eval, args=(m, k))

x, v = sol.y                # sol.y has one row per variable
plt.plot(sol.t, x, label='position, x')
plt.plot(sol.t, v, label='velocity, v')
plt.xlabel('t')
plt.legend()
plt.show()
```

A few things to note in this example:

- The function with the equations of motion must take the time `t` as its **first** argument,
  even if, as here, it does not use it, followed by the state vector. Extra parameters (`m`
  and `k`) are passed with `args`, as we did with `quad`.
- The function returns the **derivatives** of the state, $(\dot{x}, \dot{v})$. The solver
  works out the state itself.
- `t_eval` only sets the times at which the solution is reported. The solver chooses its own
  (adaptive) time steps internally.
- `sol.t` contains the times and `sol.y` the solution, with **one row per variable** and one
  column per time. Note this is the opposite of the layout returned by `np.loadtxt`.

The integration algorithm is set with the `method` argument. The default, `RK45`, is an
explicit Runge-Kutta method of order 5(4), which adapts the time step to keep the error
estimate within the tolerances `rtol` and `atol`. By default these are rather loose
(`rtol=1e-3`, `atol=1e-6`).

```{exercise}
:nonumber:
:class: dropdown

The total energy of the oscillator, $E = \frac{1}{2}mv^2 + \frac{1}{2}kx^2$, should be
conserved. Compute $E(t)$ from the solution above and plot it. Then integrate for a much
longer time (e.g. `tf = 1000`) and check how $E$ drifts. How does this change if you
use tighter tolerances, e.g. `rtol=1e-8, atol=1e-10`?
```

### `scipy.interpolate`

This submodule provides several interpolation routines. In the case of 1D interpolation, i.e.
from a discrete set of $(x,y)$ points, the most common method is `interp1d`. This function takes
as arguments the `x` and `y` arrays, and returns a function object that can be evaluated at any point,
within the range of `x` (values out of this range can be managed with the `fill_value` argument).
For instance,

```{code-cell} python
from scipy.interpolate import interp1d
import numpy as np
import matplotlib.pyplot as plt

x = np.linspace(0, 10, 10)
y = np.sin(x)
f = interp1d(x, y, kind='cubic')

xnew = np.linspace(0, 10, 100)
ynew = f(xnew)

plt.plot(x, y, 'o', xnew, ynew, '-')
plt.show()
```

As shown in the above example, the `kind` argument specifies the type of interpolation. Possible
values include `linear` (which is the default), `quadratic` or `cubic` (a complete list
can be found in the [official documentation](https://docs.scipy.org/doc/scipy/reference/interpolate.html)).

```{note}
Recent versions of SciPy label `interp1d` as *legacy*: it still works, but it will not
receive new features. For new code, the recommended alternatives are `np.interp` (linear),
`CubicSpline` or `make_interp_spline` (splines), all of which return values or callable
objects in the same way.
```

```{exercise}
:nonumber:
:class: dropdown

Write a program that sums two spectra defined over different 
wavelength ranges. Use interpolation to generate a common wavelength
grid, and then sum the spectra.

*Note*: spectra to test your code can be obtained from 
[PhotochemCAD](http://omlc.org/spectra/PhotochemCAD).
You can use the `requests` module to download the files (install it
with `conda install requests` if it is not in your environment).
Note that `response.content` is *bytes*, so the file must be opened in binary
mode, `"wb"`:

```python
import requests

# Azobenzene
URL = "https://omlc.org/spectra/PhotochemCAD/data/117-abs.txt"
response = requests.get(URL)
with open("spc1.dat", "wb") as f:
    f.write(response.content)

# 9,10-Diphenylanthracene
URL = "https://omlc.org/spectra/PhotochemCAD/data/021-abs.txt"
response = requests.get(URL)
with open("spc2.dat", "wb") as f:
    f.write(response.content)

```

For 2D interpolation of data on a rectangular grid we can use `RectBivariateSpline`
(older material uses `interp2d`, which was removed in SciPy 1.14).
This function takes as arguments the two 1D arrays of coordinates, `x` and `y`, which
do not have to be equally spaced, and a 2D array of values, `z`, with shape
`(len(x), len(y))`. As in the 1D case, it returns an object that can be evaluated
at any point within the grid.

```{code-cell} python
from scipy.interpolate import RectBivariateSpline
import numpy as np
import matplotlib.pyplot as plt

x = np.linspace(0, 10, 10)
y = np.linspace(0, 10, 10)
X, Y = np.meshgrid(x, y)
Z = np.sin(X) + np.cos(Y)   # shape (len(y), len(x))

f = RectBivariateSpline(x, y, Z.T, kx=3, ky=3)   # cubic in x and y

xnew = np.linspace(0, 10, 100)
ynew = np.linspace(0, 10, 100)
znew = f(xnew, ynew).T      # back to shape (len(ynew), len(xnew)) for plotting

plt.pcolormesh(X, Y, Z)
plt.colorbar()
plt.title('Original')
plt.show()
plt.pcolormesh(xnew, ynew, znew)
plt.colorbar()
plt.title('Interpolated')
plt.show()
```

As you can see, we use some kind of *advanced* `matplotlib` features in this example. 
You can refresh them going back to the [previous chapter](plotting.md).
For instance, use the `np.meshgrid` function, which generates 2D arrays with 
the grid points, (`x`,`y`), from the corresponding 1D arrays, `x` and `y`. Note that
`meshgrid` returns arrays with shape `(len(y), len(x))`, while `RectBivariateSpline` expects
`(len(x), len(y))`, hence the transposes (`.T`). The degree of the spline in each direction
is set with `kx` and `ky` (1 for linear, 3 for cubic).
An alternative with the same purpose is `RegularGridInterpolator`, which also works in more
than two dimensions.

To interpolate unstructured data we can use the function `griddata`. 
It takes as arguments the coordinates of the data points as a tuple of 1D arrays,
`(x,y)` and the values at these points, `z`, also a 1D array. 
It also takes the coordinates of the points where the interpolation is required, `(Xi,Yi)`. 
In this case, it returns the interpolated values at these points as a 2D array `Zi`.
The interpolation method is specified with the `method` argument. Possible values are `linear`,
`nearest` and `cubic`.

### `scipy.optimize`

This module provides several algorithms for optimization (locating minima and maxima) and 
root-finding.

The function `minimize` provides a common interface to all the **optimization** algorithms.
It takes as arguments the function to be minimized, `f(x)`, the initial guess, `x0`, and
the method to be used, `method`. The function to be minimized must take as argument a 1D array
with the values of the variables to be optimized, and return a scalar. For instance,

```{code-cell} python 
from scipy.optimize import minimize
import numpy as np

def f(x):
    return np.sum(x**2)
    
x0 = np.array([1, 2, 3])
res = minimize(f, x0, method='Nelder-Mead')
print(res.x)
```

As shown above, the `minimize` function returns an object with the results of the optimization.
The `x` attribute contains the values of the variables that minimize the function. Other 
attributes of the result object are `fun`, which contains the value of the function at the
minimum, `success`, which is a boolean indicating if the optimization was successful, or the
number of iterations, `nit`, among others.

Different optimization algorithms can be used with the `method` argument, including `BFGS` (default
for unconstrained problems) or `Newton-CG`. The choice of the method
depends on the problem (stiffness, dimensionality, etc.), and the need of adding constraints
A complete list is given in the 
[documentation](https://docs.scipy.org/doc/scipy/reference/generated/scipy.optimize.minimize.html#scipy.optimize.minimize).

A very common problem in science is **fitting** a model with some parameters to data.
The function `curve_fit` does a (non-linear) least-squares fit. It takes as arguments the
model function, whose first argument is the independent variable followed by the parameters,
and the arrays of data, `xdata` and `ydata`. An initial guess for the parameters, `p0`, is
optional, but for non-linear models it is often needed to get a sensible result.
For instance, we can fit a Morse potential,
$V(r) = D_e \left(1 - e^{-a(r - r_e)}\right)^2$, to some noisy synthetic data:

```{code-cell} python
from scipy.optimize import curve_fit
import numpy as np
import matplotlib.pyplot as plt

def morse(r, De, a, re):
    return De*(1 - np.exp(-a*(r - re)))**2

# synthetic data with some random noise
rng = np.random.default_rng(42)
r = np.linspace(0.5, 3.0, 30)
V = morse(r, 4.7, 1.9, 0.74) + rng.normal(0, 0.1, r.size)

popt, pcov = curve_fit(morse, r, V, p0=[5.0, 2.0, 0.7])
perr = np.sqrt(np.diag(pcov))
for name, value, error in zip(["De", "a", "re"], popt, perr):
    print(f"{name} = {value:.3f} +/- {error:.3f}")

rfit = np.linspace(0.5, 3.0, 200)
plt.plot(r, V, 'o', label='data')
plt.plot(rfit, morse(rfit, *popt), '-', label='Morse fit')
plt.xlabel('r')
plt.ylabel('V(r)')
plt.legend()
plt.show()
```

`curve_fit` returns two arrays: `popt`, with the optimal values of the parameters, and `pcov`,
their covariance matrix. The square roots of the diagonal of `pcov` are estimates of
the standard errors of the parameters. Try a bad initial guess, such as `p0=[1, 1, 3]`
(an equilibrium distance beyond the minimum), and check what happens to the fit.

For **root-finding** of scalar functions (univariate functions, i.e., which depend on only 
one variable), we can use the general interface function `root_scalar`.
It takes as arguments the function to be solved, `f(x)` and some other arguments depending
on the method to be used, `method`. For instance, with `method=bisect`, we need to provide
the closed interval where the solution lies, `bracket`. Other methods may require the
derivative of the function, `fprime` and/or an initial guess, `x0`.
The function to be solved must take as argument a scalar
and return a scalar. For instance,

```{code-cell} python
from scipy.optimize import root_scalar
import numpy as np

def f(x):
    return np.exp(x) + x
    
res = root_scalar(f, bracket=[-2.0,2.0], method='bisect')
print(res.root)
```

Again, the `root_scalar` function returns an object with the results of the root-finding.
The `root` attribute contains the value of the variable that solves the equation.

The function `root` provides a common interface to all the root-finding algorithms
for vector functions (i.e, a system of `N` equations that depend on `N` variables).
It takes as arguments the function to be solved, `f(x)`, which depends on a 1D array (vector) 
of `N` variables, `x`, the initial guess, `x0`, and
the method to be used, `method`. The function to be solved must take as argument a 1D array
with the values of the variables to be solved, and returns a 1D array with the same shape.
For instance, the following system of equations:

$$
\begin{align}
x^2 + y^2 = 1 \\
x - y = 0
\end{align}
$$
can be solved as follows:

```{code-cell} python
from scipy.optimize import root
import numpy as np

def f(x):
    return np.array([x[0]**2 + x[1]**2 - 1, x[0] - x[1]])

x0 = np.array([1, 2])
res = root(f, x0, method='hybr')
print(res.x)
```

Available methods are summarized in the [documentation](https://docs.scipy.org/doc/scipy/reference/optimize.html#root-finding)
of this function.

## `sympy`

This module is a computer algebra system (CAS), similar to [Maxima](https://maxima.sourceforge.io) 
or Mathematica. It allows performing symbolic calculations, such as derivatives, integrals,
solving equations, etc.

We will not go into details here, but we will show some examples of the capabilities of this
module. For instance, lets compute the derivative of the function $f(x) = \sin(x) \cos(x)$:

```{code-cell} python
from sympy import symbols, sin, cos, diff

x = symbols('x')
f = sin(x)*cos(x)
df = diff(f, x)
df
```

Many other symbolic operations are possible, such as integrals, limits, series expansions, etc.
Check the [documentation](https://docs.sympy.org/latest/index.html) for more details.

(pandas)=
## `pandas`

This module provides high-performance, easy-to-use data structures and data analysis tools, allowing 
to manipulate and analyze large amounts of data. You can read and write data sets from file formats such 
as csv, excel, hdf5, etc. For instance, to read a csv file:

```python
import pandas as pd

# Read a csv file
df = pd.read_csv('file.csv')
# Get the values of column labelled 'Col1' as a numpy array
x = df['Col1'].values
```

You can check the [documentation](https://pandas.pydata.org/docs/)
for more details.

(ase)=
## `ase`

ASE stands for Atomic Simulation Environment. 
This module provides a set of tools for setting up, manipulating, running,
visualizing and analyzing atomistic simulations. It supports many
codes through the `Calculator` interface, e.g. Gaussian or Gromacs, 
allowing to perform a wide range of calculations from a single Python script.

It also provides functions to read and write files in different formats (xyz, pdb...), 
through the `ase.io` submodule. For instance, to read a file in xyz format:

```python
# The io submodule must be imported separately
import ase.io

# Generate an ASE Atom object from a file
molec = ase.io.read('file.xyz')
# Get the atomic coordinates as a numpy array:
xyz = molec.get_positions()
```

You can take a further look into the powerful capabilities of this library in the
[documentation](https://wiki.fysik.dtu.dk/ase/).

## `h5py`

This module provides support to manipulate [HDF5](https://en.wikipedia.org/wiki/HDF5) files, 
a format specifically designed to store large amounts of numerical data. 
There are other formats that are also very useful for this purpose, such as
[netCDF](https://www.unidata.ucar.edu/software/netcdf/),
[JSON](https://en.wikipedia.org/wiki/JSON) or
[XML](https://en.wikipedia.org/wiki/XML), which are also supported by Python modules.

