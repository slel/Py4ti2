# Py4ti2 - An interface to 4ti2

## What is Py4ti2

Py4ti2 provides a Python interface to some of the computations performed by 4ti2 (http://www.4ti2.de).

By now, it is possible to use:

* groebner,
* hilbert,
* graver,
* zsolve

## Requirements and installation 

First, 4ti2 is required with the groebner and zsolve components enabled. As well, GLPK (https://www.gnu.org/software/glpk/) is needed by 4ti2. Both library folders should be specified to build Py4ti2. 

For GNU/Linux or OSX users, open a ``terminal window'', select Py4ti2 as working directory to introduce the make command to build the Py4ti2 modules.

```shell
your_prompt$ cd WHERE_Py4ti2_IS_LOCATED
```

The variables GLPK_DIR and FTI2_DIR are used to provide the path where GLPK and 4ti2 libraries are installed.

The make command to build and install the modules could be:

```shell
prompt...Py4ti2$ GLPK_DIR=ROOT_OF_GLPK_INSTALLATION_HIERARCHY FTI2_DIR=ROOT_OF_4ti2_INSTALLATION_HIERARCHY make install
```

## Documentation

It is recommended to read the manual page of the corresponding 4ti2 command to know which parameters are valid. Here, we show how to execute some examples that can be found in the 4ti2 source tree folder _test_.

There is a module **Py4ti2int64** for 64 bit precision architecture, **Py4ti2int32** for 32 bits, and **Py4ti2gmp** for arbitrary precision computations.


### Gröbner bases

```python
# cuww1.1
from Py4ti2int32 import *
r=groebner("mat", [[12223, 12224, 36674, 61119, 85569]],\
           "mar", [[12224, -12223, 0, 0, 0], [2, -5, 1, 0, 0],\
                   [1, -9, 1, 1, 0], [1, -8, 0, 0, 1]], "sign", [1, 0, 1, 1, 1])

print([e for e in r])
[[-4075, -8155, 4074, 0, 1], [-4074, -8152, 4075, 0, 0], [-1, -4, 0, 1, 0], [0, -11, -1, 0, 2], [1, -8, 0, 0, 1], [1, 3, 1, 0, -1], [4076, 8147, -4074, 0, 0]]
```

```python
# cuww2.trunc1
from Py4ti2int64 import *
mar=[[-7339, 2444, 0, 2, 0, 0], [-7334, 2446, -1, 0, 0, 0], [-7333, 2445, 0, 1, -1, 0],\
     [-7, 0, -1, 0, 2, 0], [-7, 0, 0, -1, 1, 1], [-6, -1, 0, 1, 1, 0], [-6, -1, 1, 0, 0, 1],\
     [-5, -2, 1, 2, 0, 0], [-5, 0, -1, -1, 0, 2], [-4, -1, -1, 1, 0, 1], [-3, -2, -1, 3, 0, 0],\
     [-2, 0, 1, 0, 1, -1], [-2, 0, 2, -1, 0, 0], [-1, 1, -1, -1, 1, 0], [-1, 1, 0, -2, 0, 1]]

r=groebner("mat",[[12228, 36679, 36682, 48908, 61139, 73365]], "cost", [[1, 0, 0, 0, 0, 0]],\
          "lat", [[8, 4, 0, -5, 0, 0], [3, 2, 1, -3, 0, 0], [12221, 12224, 0, -12223, 0, 0],\
                  [2, 3, 0, -4, 1, 0], [-1, 1, 0, -2, 0, 1]], "mar", mar,\
           "weights", [[12228, 36679, 36682, 48908, 61139, 73365]], "weightsmax", [[1000000]])

print([e for e in r])
[[0, -3, -2, 5, -1, 0], [0, -2, 2, 3, 0, -2], [0, -2, 3, 2, -1, -1], [0, -2, 4, 1, -2, 0], [0, -2, 5, 0, -3, 1], [0, -1, -5, 3, 0, 1], [0, -1, -4, 2, -1, 2], [0, -1, -3, 1, -2, 3], [0, -1, -2, 0, -3, 4], [0, -1, 7, 0, 0, -3], [0, 0, -1, 1, 1, -1], [1, -1, 0, 2, 0, -1], [1, -1, 1, 1, -1, 0], [1, -1, 2, 0, -2, 1], [1, 0, 4, 0, 1, -3], [1, 0, 5, -1, 0, -2], [1, 1, -3, 0, 1, 0], [1, 1, -2, -1, 0, 1], [1, 2, 3, -4, 0, 0], [2, 0, -2, 1, 0, 0], [2, 0, -1, 0, -1, 1], [2, 1, 3, -2, 0, -1], [3, 0, 3, 0, 0, -2], [3, 2, 1, -3, 0, 0], [4, 1, 1, -1, 0, -1], [5, 0, 2, 0, -1, -1], [5, 2, -1, -2, 0, 0], [6, 1, -1, 0, 0, -1], [7, 0, 1, 0, -2, 0]]
```

### Hilbert bases

```python
# 44.mat

from Py4ti2int64 import *
mat=[[1, 1, 1, 1, -1, -1, -1, -1, 0, 0, 0, 0, 0, 0, 0, 0], 
     [1, 1, 1, 1, 0, 0, 0, 0, -1, -1, -1, -1, 0, 0, 0, 0],
     [1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, -1, -1, -1, -1],
     [0, 1, 1, 1, -1, 0, 0, 0, -1, 0, 0, 0, -1, 0, 0, 0],
     [1, 0, 1, 1, 0, -1, 0, 0, 0, -1, 0, 0, 0, -1, 0, 0],
     [1, 1, 0, 1, 0, 0, -1, 0, 0, 0, -1, 0, 0, 0, -1, 0],
     [1, 1, 1, 0, 0, 0, 0, -1, 0, 0, 0, -1, 0, 0, 0, -1],
     [0, 1, 1, 1, 0, -1, 0, 0, 0, 0, -1, 0, 0, 0, 0, -1],
     [1, 1, 1, 0, 0, 0, -1, 0, 0, -1, 0, 0, -1, 0, 0, 0]]
r=hilbert("mat", mat)

print([e for e in r])
['zhom', [[0, 1, 0, 1, 2, 0, 0, 0, 0, 1, 1, 0, 0, 0, 1, 1], [1, 0, 1, 0, 0, 0, 0, 2, 0, 1, 1, 0, 1, 1, 0, 0], [0, 0, 1, 1, 0, 1, 1, 0, 2, 0, 0, 0, 0, 1, 0, 1], [1, 1, 0, 0, 0, 1, 1, 0, 0, 0, 0, 2, 1, 0, 1, 0], [0, 0, 1, 1, 0, 1, 0, 1, 1, 0, 1, 0, 1, 1, 0, 0], [1, 0, 0, 1, 0, 0, 1, 1, 1, 0, 1, 0, 0, 2, 0, 0], [0, 0, 0, 1, 0, 1, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0], [0, 1, 0, 0, 0, 0, 1, 0, 1, 0, 0, 0, 0, 0, 0, 1], [0, 0, 2, 0, 0, 1, 0, 1, 1, 1, 0, 0, 1, 0, 0, 1], [1, 0, 0, 0, 0, 0, 0, 1, 0, 1, 0, 0, 0, 0, 1, 0], [0, 0, 1, 0, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1], [0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0], [0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 1, 0, 0, 0], [1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 1, 0, 0], [0, 2, 0, 0, 1, 0, 1, 0, 0, 0, 1, 1, 1, 0, 0, 1], [0, 1, 0, 1, 1, 1, 0, 0, 0, 0, 1, 1, 1, 0, 1, 0], [0, 0, 1, 0, 0, 1, 0, 0, 0, 0, 0, 1, 1, 0, 0, 0], [1, 1, 0, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 0, 1, 1], [1, 0, 1, 0, 0, 0, 1, 1, 1, 1, 0, 0, 0, 1, 0, 1], [1, 0, 0, 1, 1, 1, 0, 0, 0, 1, 0, 1, 0, 0, 2, 0]], 'zfree', []]
```

```python
# a1.mat

from Py4ti2int64 import *
mat=[[ 0,  0, -1,  1,  0,  0,  0,  0, -2,  0,  0,  1,  0,  1,  2,  0,  0,  1,  0, -1, -1, -1,  0, -1],
[ 0,  0,  1, -1,  0,  0, -2, -2,  0,  2,  2,  1,  2,  1,  0,  2,  2,  1, -2, -1, -1, -1, -2, -1],
[ 0,  0, -1, -1,  0, -2,  0,  0,  0,  0,  0,  1,  0, -1,  0,  0,  0,  1,  0,  1,  1,  1,  0,  1],
[ 0,  0,  1, -1, -2,  0,  0,  0,  0,  0,  0, -1,  0,  1,  0,  0,  0, -1,  0,  1, -1,  1,  0,  1],
[ 0, -2, -1,  1,  0,  0,  0, -2,  0,  0,  2,  1,  0,  1,  0,  0,  2,  1,  0, -1,  1, -1,  0, -1],
[-2,  0, -1, -1,  0,  0,  0,  2,  0,  0, -2, -1,  0, -1,  0,  0, -2, -1,  2,  1,  1,  1,  2,  1],
[ 0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0, -1, -1, -1,  0,  0,  0,  0,  1,  1],
[ 0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0, -1],
[ 0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0, -1,  0,  0,  0,  0,  0,  0],
[ 0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0, -1,  0,  0,  0,  0,  0,  0,  0],
[ 0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  1,  1,  0,  0,  0,  0, -1,  0],
[ 0,  0,  1, -1,  0,  0,  0,  0,  0,  0,  0, -1,  0, -1, -2,  0,  0, -1,  0,  1,  1,  1,  0,  1],
[ 0,  0, -1,  1,  0,  0,  0,  0,  0,  0,  0,  1, -2, -1,  0,  0,  0,  1,  0, -1,  1,  1,  0, -1],
[ 0,  0, -1,  1,  0,  0,  0,  0,  0,  0,  0,  1,  0, -1,  0,  0,  0,  1,  0, -1,  1, -1,  0, -1],
[ 0,  0,  1, -1,  0,  0,  0,  0,  0,  0,  0, -1,  0,  1,  0,  0,  0, -1,  0,  1, -1, -1,  0,  1],
[ 0,  0, -1,  1,  0,  0,  0,  0,  0,  0,  0,  1,  0,  1,  0,  0,  0,  1,  0, -1, -1, -1,  0, -1],
[ 0,  0,  1, -1,  0,  0,  0,  0,  0,  0,  0, -1,  0, -1,  0,  0,  0, -1,  0,  1, -1,  1,  0,  1],
[ 0,  0,  0,  0,  0,  0,  0, -1,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0],
[ 0,  0,  0,  0,  0,  0,  0,  1,  0, -1, -1, -1,  0,  0,  0,  0,  0,  0,  1,  1,  0,  0,  0,  0],
[ 0,  0,  1,  1,  0,  0,  0,  0,  0,  0,  0, -1,  0,  1,  0,  0,  0, -1,  0, -1, -1, -1,  0, -1],
[ 0,  0, -1, -1,  0,  0,  0,  0,  0,  0,  0,  1,  0, -1,  0,  0,  0,  1,  0, -1,  1,  1,  0,  1],
[ 0,  0, -1, -1,  0,  0,  0,  0,  0,  0,  0, -1,  0, -1,  0,  0,  0,  1,  0,  1,  1,  1,  0,  1],
[ 0,  0,  0,  0,  0,  0,  0,  1,  0,  0, -1,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0],
[ 0,  0,  1,  1,  0,  0,  0, -2,  0,  0,  2,  1,  0,  1,  0,  0,  0, -1, -2, -1, -1, -1,  0, -1]]
rel=[-1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1]
sign=[0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
r=hilbert("mat", mat, "rel", rel, "sign", sign)

print([e for e in r])
['zhom', [[1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0], [0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0], [0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0], [0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0], [0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0], [0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0], [1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0], [0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0], [0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0], [1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0], [0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1], [1, 1, 1, 1, 1, 1, 1, 0, 1, 1, 0, 1, 1, 1, 1, 0, 0, 0, 1, 1, 1, 1, 0, 0]], 'zfree', []]
```

### Graver bases

```python
# small

from Py4ti2int64 import *

r=graver("mat", [[1, 1, 1, 1, 1], [1, 2, 3, 4, 5]], "sign", [-1, 2, 1, 1, 0])

print([e for e in r])
[[0, -1, 0, 3, -2], [0, -2, 3, 0, -1], [-1, 0, 2, 0, -1], [-3, 4, 0, 0, -1], [-2, 2, 1, 0, -1], [-1, 1, 0, 1, -1], [0, -1, 1, 1, -1], [-1, 0, 1, 2, -2], [-1, 0, 0, 4, -3]]
```
### Zsolve

```python
# affine

from Py4ti2int64 import *

r=zsolve("lat",[[1, -1, 1, 0], [2, -3, 0, 1]],"sign",[1, 2, 2, 0])

print([e for e in r])
['zinhom', [[0, 0, 0, 0]], 'zhom', [[1, 0, 3, -1], [0, -1, -2, 1], [0, 1, 2, -1], [1, -1, 1, 0], [1, -2, -1, 1], [2, -3, 0, 1]], 'zfree', []]
```

```python
# hppi6

from Py4ti2int32 import *

zsolve("mat",[[1, 1, 1, 1, 1, 1], [1, 2, 3, 4, 5, 6]],"sign",[1, 1, 1, 2, 2, 2], "rel", [-1, -1], 
      "lb", [0, 0, 0, 1, -1, -1], "ub", [1, 4, -1, -1, 2, 1])

print([e for e in r])
['zinhom', [[0, 0, 0, 0]], 'zhom', [[1, 0, 3, -1], [0, -1, -2, 1], [0, 1, 2, -1], [1, -1, 1, 0], [1, -2, -1, 1], [2, -3, 0, 1]], 'zfree', []]
```

```python
# m33

from Py4ti2gmp import *

problem=["mat",[[0, 0, 0, 0, 0, 3, -4, -1, 2], [0, 0, 0, 0, 1, -1, 1, 0, -1], [0, 0, 0, 1, 2, 0, 0, -1, -2], 
                 [0, 0, 1, 0, 1, 0, 0, -1, -1], [0, 1, 2, 0, 0, 0, 0, -1, -2], [1, 0, 2, 0, 0, 0, 0, -2, -1], 
                 [-2, 0, -2, 0, 0, 0, 0, 3, 0], [-2, 0, 0, 0, 0, 0, 0, 1, 0], [0, 0, -2, 0, 0, 0, 0, 1, 0], 
                 [0, 0, 0, 0, 0, 0, 0, -1, 0]], 
          "rel", [0, 0, 0, 0, 0, 0, -1, -1, -1, -1], 
          "sign", [0, 0, 0, 0, 0, 0, 0, 0, 0]]

r=zsolve(*problem)

print([e for e in r])
['zinhom', [[0, 0, 0, 0, 0, 0, 0, 0, 0]], 'zhom', [[1, 0, 2, 2, 1, 0, 0, 2, 1], [2, 0, 1, 0, 1, 2, 1, 2, 0], [1, 2, 0, 0, 1, 2, 2, 0, 1], [1, 1, 1, 1, 1, 1, 1, 1, 1], [0, 2, 1, 2, 1, 0, 1, 0, 2]], 'zfree', []]

```