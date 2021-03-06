## Arrowhead and Diagonal-plus-rank-one Eigenvalue Solvers

[![Build Status](https://travis-ci.org/ivanslapnicar/Arrowhead.jl.svg?branch=master)](https://travis-ci.org/ivanslapnicar/Arrowhead.jl?branch=master)

### Basics

The package contains routines for __forward stable__ algorithms which compute:
* all eigenvalues and eigenvectors of a real symmetric arrowhead matrices,
* all eigenvalues and eigenvectors of rank-one modifications of diagonal matrices (DPR1), and
* all singular values and singular vectors of half-arrowhead matrices.

The last class of matrices typically appears in SVD updating problems.
The algorithms and their analysis are given in the references.

Eigen/singular values are computed in a forward stable manner. Eigen/singular vectors are
computed entrywise to almost full accuracy, so they are automatically mutually
orthogonal.  The algorithms are based on a shift-and-invert approach.  Only a
single element of the inverse of the shifted matrix eventually needs to
be computed with double the working precision.

The package also contains routines for applications:
* divide-and-conquer routine for symmetric tridiagonal eigenvalue problem
* roots of real polynomials with real distinct roots.


### Contents

The file `arrowhead1.jl` contains definitions of types `SymArrow` (arrowhead) and `SymDPR1`. Full matrices are accessible with the command `full(A)`.

The file `arrowhead3.jl` contains routines to generate random symmetric
arrowhead and DPR1 matrices, ` GenSymArrow` and `GenSymDPR1`, respectively,
three routines called `inv()` which compute various inverses of _SymArrow_
matrices, two routines called `bisect()` which compute outer eigenvalues of
_SymArrow_ and _SymDPR1_ matrices, main computational routine `eig()` which
computes the k-th eigenpair of an ordered unreduced  _SymArrow_,
and the driver routine `eig()` which computes all eigenvalues and
eigenvectors of a _SymArrow_.

The file `arrowhead4.jl` contains three routines called `inv()` which compute
various inverses of _SymDPR1_ matrices, main computational routine `eig()`
which computes the k-th eigenpair of an ordered unreduced _SymDPR1_,
and the driver routine `eig()` which computes all eigenvalues and
eigenvectors of a _SymDPR1_.

The file `arrowhead5.jl` contains definition of type `HalfArrow`.
_HalfArrow_ is of the form _[diagm(A.D) A.z]_ where either
_length(A.z)=length(A.D)_
or _length(A.z)=length(A.D)+1_, thus giving two possible different forms of
SVD rank one update.  The file `arrowhead6.jl` contains the routine
`doubledot()`, three routines called `inv()` which compute
various inverses of _HalfArrow_ matrices, main computational routine `svd()`
which computes the k-th singular value triplet _u, sigma, v_ of an ordered
unreduced _HalfArrow_,  and the driver routine `svd()` which computes all
singular values and vectors of a _HalfArrow_.

The file `arrowhead7.jl` contains a simple routine `tdc()` which implements
divide-and-conquer method for `SymTridiagonal` matrices by spliting the matrix
in two parts  and connecting the parts via eigenvalue decomposition of
arrowhead matrix.

The file `arrowhead7.jl` conatains the routine `rootsah()` which computes the
roots of real polynomials with all distinct real roots. The computation is
forward stable. The program uses `SymArrow` form of companion matrix in
barycenntric coordinates and
the corresponding `eig()` routine specially designed for this case.
The file also contains three routines called `inv()`.


### Authors and References

The routines for arrowhead and half-arrowhead matrices
were developed and analysed by [Jakovcevic Stor, Barlow and
Slapnicar (2013)][JSB2013]
(see also [arXiv:1302.7203][JSB2013a]).
The routines for DPR1 matrices are described and analysed in [Jakovcevic
Stor, Barlow and Slapnicar (2015)][JSB2015] (the paper is [freely downloadable](http://authors.elsevier.com/a/1Rmlt5YnCLEdU) until
Nov 15, 2015, see also [arXiv:1405.7537][JSB2015a]). The polynomial root finder is described and analyzed
in [Jakovcevic Stor and Slapnicar (2015)][JS2015].

The Matlab version of the
routines used in the papers are written Ivan Slapnicar and Nevena Jakovcevic
Stor. The first version of Julia routines was written by Ivan Slapnicar during a visit
to MIT, and later version were written by Ivan Slapnicar and Nevena Jakovcevic Stor.


Double the working precision is implemented by using routines by
[T. J. Dekker (1971)][dekker1971] from the package [DoubleDouble][byrne2014]
by Simon Byrne.

### Thanks

Highly appreciated help and advice came from [Jiahao Chen][jiahao],
[Andreas Noack][andreasnoack], [Jake Bolewski][jakebolewski] and
[Simon Byrne][simonbyrne].


[JSB2013]: http://www.sciencedirect.com/science/article/pii/S0024379513006265 "Nevena Jakovcevic Stor, Ivan Slapnicar and Jesse L. Barlow, 'Accurate eigenvalue decomposition of real symmetric arrowhead matrices and applications', Linear Algebra and its Applications, Vol. 464 (2015) 62-89, DOI: 10.1016/j.laa.2013.10.007"

[JSB2013a]: http://arxiv.org/abs/1302.7203 "Nevena Jakovcevic Stor, Ivan Slapnicar and Jesse L. Barlow, 'Accurate eigenvalue decomposition of arrowhead matrices and applications', arXiv:1302.7203v3"

[JSB2015]: http://www.sciencedirect.com/science/article/pii/S0024379515005406 "Nevena Jakovcevic Stor, Ivan Slapnicar and Jesse L. Barlow, 'Forward stable eigenvalue decomposition of rank-one modifications of diagonal matrices', Linear Algebra and its Applications, Vol. 487 (2015) 301-315, DOI: 10.1016/j.laa.2015.09.025"

[JSB2015a]: http://arxiv.org/abs/1405.7537 "Nevena Jakovcevic Stor, Ivan Slapnicar and Jesse L. Barlow, 'Forward stable eigenvalue decomposition of rank-one modifications of diagonal matrices', arXiv:1405.7537v2"

[JS2015]: http://arxiv.org/abs/1509.06224 "Nevena Jakovcevic Stor and Ivan Slapnicar, 'Forward stable computation of roots of real polynomials with only real distinct roots', arXiv:1509.06224v1"

[dekker1971]: http://link.springer.com/article/10.1007%2FBF01397083  "T.J. Dekker (1971) 'A floating-point technique for extending the available precision', Numerische Mathematik, Volume 18, Issue 3, pp 224-242"

[byrne2014]: https://github.com/simonbyrne/DoubleDouble.jl

[jiahao]: https://github.com/jiahao
[andreasnoack]: https://github.com/andreasnoack
[jakebolewski]: https://github.com/jakebolewski
[simonbyrne]: https://github.com/simonbyrne
