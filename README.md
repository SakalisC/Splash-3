Splash-3 Benchmark Suite
========================

Splash-3 is a benchmark suite based on Splash-2 but without data races. It was
first presented at [ISPASS'16](http://ieeexplore.ieee.org/abstract/document/7482078/).

The version found here is a refined version of the one used in the ISPASS paper.
The main difference is that it is based on the [Modified
Splash-2](http://www.capsl.udel.edu/splash/index.html) suite, which, among other
things, fixes issues related to running Splash-2 on x86-64, as well as lots of
warnings.  While working on the release version of Splash-3 we realized that we
are duplicating a lot of the effort already taken by Modified Splash-2, so we
decided to port our Splash-3 patchset on top of Modified Splash-2. 

Modified Splash-2 also changes every `int` to `long`, which is something that we
only partially did for the version discussed in the paper, so we do expect some
differences in the memory footprint of the applications. However, everything
else, such as the algorithms or the synchronization characteristics of the
applications remain unchanged, making the overall performance difference between
this version and the ISPASS version minimal.

## Installation

There is no need to install Splash-3. All you need to do is set the `BASEDIR`
variable in `codes/Makefile.config` to point to the full path of the `codes`
directory.

## Tarballs

For tarball releases please visit our website at
[etascale.com](https://argodsm.com/software/splash-3.html).

## Citing Splash-3

To properly cite Splash-3 please cite our ISPASS'16 paper.

	C. Sakalis, C. Leonardsson, S. Kaxiras, and A. Ros, “Splash-3: A
	properly synchronized benchmark suite for contemporary research,”
	in Performance Analysis of Systems and Software (ISPASS), 2016
	IEEE International Symposium On, IEEE, 2016.

## Building and Running Splash-3

In order to build Splash-3, a relatively modern C compiler with C11 support is
required. In addition, the M4 macro processor is necessary for generating the
source files in the first place. On Ubuntu and similar systems, you can install
the `m4` and `ivtools-dev` packages.

If you are wanting to use a cross-compile toolchain, set the `TOOLCHAIN_PREFIX`
environment variable to the prefix required to find the cross-compile tools,
e.g. `${TOOLCHAIN_PREFIX}gcc` should be found for a cross-compiling `gcc`.

Some benchmarks expect their inputs to be at very specific paths relative to the
working directory, so it is recommended to change the working directory to the
benchmark folder before executing it.

## Different Versions

The first release of Splash-3 is tagged as `v3.0`. Small fixes might be
published untagged on the master branch, as long as they do not significantly
affect the performance or other characteristics of the applications.

The current Splash-3 version, referred to as Splash-3x, is tagged as `v3.0X`.
Splash-3x is based on Splash-2x from the PARSEC benchmark suite, which enables
support for bigger input sets. In addition, Splash-3x contains some small
changes that enable support for running with a higher number of threads. Note
that Splash-2x also includes the fixes from the Modified Splash-2 and that
Splash-3x is build on top of Splash-3.

It is also possible to access the original and the Modified Splash-2 codes.
They are tagged as `v2.0` and `v2.0M` respectively.

## Recommended Inputs

The following are the recommended inputs for running Splash-3 in a simulator.
The symbol '#' is a placeholder for the number of threads. These inputs are
based on the original Splash-2 characterization paper by Woo et al. [1].

	APPS:
	./BARNES < inputs/n16384-p#
	./FMM < inputs/input.#.16384
	./OCEAN -p# -n258
	./RADIOSITY -p # -ae 5000 -bf 0.1 -en 0.05 -room -batch
	./RAYTRACE -p# -m64 inputs/car.env
	./VOLREND # inputs/head 8
	./WATER-NSQUARED < inputs/n512-p#
	./WATER-SPATIAL < inputs/n512-p#
	KERNELS:
	./CHOLESKY -p# < inputs/tk15.O
	./FFT -p# -m16
	./LU -p# -n512
	./RADIX -p# -n1048576

## Known Issues

* If OCEAN (either version) segfaults during initialization, try reducing the
  `IMAX` and `JMAX` values in `decs.h`.
* It is recommended to change the working directory to the benchmark's
  directory.



## Removing the locks around some of the "benign" races

Due to popular demand, some of the locks around some of the "benign" assignment
races have been marked as optional. If you want to disable those locks, pass the
option `-DWITH_NO_OPTIONAL_LOCKS` to the compiler. **IT IS HIGHLY DISCOURAGED TO
DO SO. The applications have not been tested without those locks, and even the
"benign" data races can cause undefined behavior.**

## PARSEC Inputs

The inputs named 'parsec\_' are part of the [PARSEC 3.0 benchmark
suite](http://parsec.cs.princeton.edu/) and are not covered by the Splash-3
licenses. Instead they are covered by the following license:

```
Copyright (c) 2006-2012, Princeton University
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are met:
    * Redistributions of source code must retain the above copyright
      notice, this list of conditions and the following disclaimer.
    * Redistributions in binary form must reproduce the above copyright
      notice, this list of conditions and the following disclaimer in the
      documentation and/or other materials provided with the distribution.
    * Neither the name of Princeton University nor the
      names of its contributors may be used to endorse or promote products
      derived from this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY PRINCETON UNIVERSITY ``AS IS'' AND ANY
EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED
WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED. IN NO EVENT SHALL PRINCETON UNIVERSITY BE LIABLE FOR ANY
DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES
(INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES;
LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND
ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
(INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
```

## Original source code from the ISPASS'16 paper

If you are interested in the exact source code used for the ISPASS'16 paper,
please contact Christos Sakalis directly.

---

[1] Steven Cameron Woo, Moriyoshi Ohara, Evan Torrie, Jaswinder Pal Singh, and
Anoop Gupta. 1995. The SPLASH-2 programs: characterization and methodological
considerations. In Proceedings of the 22nd annual international symposium on
Computer architecture (ISCA '95). ACM, New York, NY, USA, 24-36.
DOI=http://dx.doi.org/10.1145/223982.223990 
