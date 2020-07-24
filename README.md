# Farm-SVE: A scalar C++ implementation of the ARM® Scalable Vector Extension (SVE)

The Farm-SVE package provides a header that implements the ARM C language extensions (ACLE) for the ARM Scalable Vector Extension (SVE) in standard C++. ARM-based CPUs are expected to be widely used in HPC. However, having access to an ARM CPU that supports SVE is actually (in 2020) not easy. Moreover, debugging vectorized applications is also not straightforward, and this is even more tricky when this is done remotely.

Therefore, the aims of this package are:

- To allow developing SVE-based code without having an ARM CPU, without cross-compiling, without the need of an emulator, etc;
- To compile, debug and execute on any hardware (including x86, but not only);
- To ease the vectorization of code before/in preparation of having access to a real machine;
- For educational purpose, to teach how to vectorize code using ARM SVE without having an ARM CPU;
- To debug more easily by having access to the variables without them to be in registers;
- To share SVE-based code with anyone and allowing that person to run the code and actually get the results without an ARM-based CPU (that could be useful for the review process).

However, as the implementation of Farm-SVE is naive and scalar, it is of course not made to achieve high-performance.

An alternative, could be to use a vectorization library, such as Inastemp (https://gitlab.inria.fr/bramas/inastemp).

# Official repository and bug/issues tracking

Please visit the official GIT repository to let us know if you find any bug or would like to propose any improvement:

https://gitlab.inria.fr/bramas/farm-sve

Feel free to open an issue here:

https://gitlab.inria.fr/bramas/farm-sve/-/issues

# Citing

We would appreciate that any publication that presents a software (that uses ARM SVE, obviously) where Farm-SVE was used at some point in the project (to facilitate the development or to debug, or anything else) refer to the following reference:
Bérenger Bramas. Farm-SVE: A scalar C++ implementation of the ARM® Scalable Vector Extension (SVE). 2020. ⟨hal-02906179⟩

Simply an acknowledgment to express the fact that this tool was used in the development process of your project and that it was useful to you would be great.

# Authors:
- Berenger Bramas (berenger.bramas@inria.fr)

# Under MIT License.

Copyright 2020 Inria

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:
The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NON INFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

# Tiny help

One can include Farm-SVE using:
```
#ifdef __ARM_FEATURE_SVE
#include <arm_sve.h>
#else
#include "farm_sve.h"
#endif /* __ARM_FEATURE_SVE */
```

The macro `FARM_NB_BITS_IN_VEC` set the number of bits. It is 512 by default, but can be overwritten (passing `-DFARM_NB_BITS_IN_VEC=X` to the compiler for example).

When Farm-SVE is used the following macro are define in the header: `USE_FARM_SVE` and `__FARM_SVE__`.

Additionally, this macro `FARM_USE_F16C` is defined when F16 is enabled.

# Current limitations

- Faults are not managed;
- `float16_t` is actually a `float` when f16 is enabled (`-mf16c` compiler flag) or a dumb float cut to 16 bits otherwise;
- `mulx`, `subr`, `tmad`, `recp[e,s]` and `recpx` do not really respect SVE definitions, and they are marked with a `TODO`;
- There are bugs for sure, as the implementation was generated semi-automatically.



# Useful references

- ARM C Language Extensions for SVE
- ARM Architecture Reference Manual Supplement, The Scalable Vector Extension (SVE), for ARMv8-A
- Arm Scalable Vector Extension and application to Machine Learning
- Stephens, Nigel, et al. "The ARM scalable vector extension." *IEEE Micro* 37.2 (2017): 26-39.