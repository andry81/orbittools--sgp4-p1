* README_EN.txt
* 2020.01.24
* sgp4

1. DESCRIPTION
2. LICENSE
3. REPOSITORIES
4. INSTALLATION
5. AUTHOR EMAIL

-------------------------------------------------------------------------------
1. DESCRIPTION
-------------------------------------------------------------------------------
SGP4 patched sources fork from:
https://github.com/dnwrnr/sgp4

Web access:
  https://www.danrw.com/sgp4/

From authors:

  C++ SGP4 Satellite Library

The original library patched to fix only these critical (p1) issues:

1. Fix trigonometric range before call and after call to triginometric
   functions because of sloppy QD arithmetic outside and inside a function
   call.

All patches improved precision from ~1 meter per 100km altitude along
velocity vector in certain routines up to 10^-7 meters per 100km altitude along
velocity vector.

Cmake scripts uses the cmake modules from the tacklelib library:

https://svn.code.sf.net/p/tacklelib/cmake/trunk

Third-party QD library hosts here:

https://svn.code.sf.net/p/orbittools/qd_/trunk

-------------------------------------------------------------------------------
2. LICENSE
-------------------------------------------------------------------------------
The MIT license (see included text file "license.txt" or
https://en.wikipedia.org/wiki/MIT_License)

-------------------------------------------------------------------------------
3. REPOSITORIES
-------------------------------------------------------------------------------
Primary:
  * https://sf.net/p/orbittools/sgp4-p1/HEAD/tree/trunk
    https://svn.code.sf.net/p/orbittools/sgp4-p1/trunk
First mirror:
  * https://github.com/andry81/orbittools--sgp4-p1/tree/trunk
    https://github.com/andry81/orbittools--sgp4-p1.git
Second mirror:
  * https://bitbucket.org/andry81/orbittools-sgp4-p1/src/trunk
    https://bitbucket.org/andry81/orbittools-sgp4-p1.git

-------------------------------------------------------------------------------
4. INSTALLATION
-------------------------------------------------------------------------------
N/A

-------------------------------------------------------------------------------
5. AUTHOR EMAIL
-------------------------------------------------------------------------------
Andrey Dibrov (andry at inbox dot ru)
