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

# Other useful libraries

In this section we review some additional libraries that are very useful for scientific computing.

## `scipy` 

This module contains a collection of numerical algorithms and domain-specific toolboxes, 
including signal processing, optimization, statistics and much more. 
It is built on top of `numpy` and extends it with additional functionality.

`scipy` is organized in submodules, each one with a specific purpose, which are imported separately as,

```python
import scipy.submodulename
#or
from scipy import submodulename
```

The algorithms provided by `scipy` are included in the following submodules:

- `cluster`: Clustering algorithms
- `fft`: Fast Fourier Transform routines (this should replace the still existing `fftpack` module)
- `integrate`: Integration and ordinary differential equation solvers
- `interpolate`: Interpolation and smoothing splines
- `linalg`: Linear algebra
- `ndimage`: N-dimensional image processing
- `odr`: Orthogonal distance regression
- `optimize`: Optimization and root-finding routines
- `signal`: Signal processing
- `sparse`: Sparse matrices and associated routines
- `spatial`: Spatial data structures and algorithms
- `special`: Special functions
- `stats`: Statistical distributions and functions

Additionally, `scipy` also provides the following submodules:
- `constants`: Physical and mathematical constants
- `io`: Input and Output
- `misc`: Miscellaneous utilities that don’t have another home.


## `sympy`

This module is a computer algebra system (CAS), such as [Maxima](https://maxima.sourceforge.io) 
or Mathematica.

## `pandas`

This module provides high-performance, easy-to-use data structures and data analysis tools.

## `h5py`

This module provides support to manipulate [HDF5](https://en.wikipedia.org/wiki/HDF5) files, 
a format specifically designed to store large amounts of numerical data. 
There are other formats that are also very useful for this purpose, such as
[netCDF](https://www.unidata.ucar.edu/software/netcdf/),
[JSON](https://en.wikipedia.org/wiki/JSON) or
[XML](https://en.wikipedia.org/wiki/XML),

