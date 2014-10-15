## Arrowhead and Diagonal-plus-rank-one Eigenvalue Solvers

[![Build Status](https://travis-ci.org/ivanslapnicar/Arrowhead.jl.svg?branch=master)](https://travis-ci.org/ivanslapnicar/Arrowhead.jl?branch=master)

### Basics

The package contains routines for forward stable algorithms which compute all
eigenvalues and eigenvactors of a real symmetric arrowhead matrices and
matrices which are a rank-one modification of diagonal matrices (DPR1). The
algorithms and their analysis are given in the references. 

Eigenvalues are computed to almost full relative accuracy.  Eigenvectors are
computed entrywise to almost full accuracy, so they are automatically mutually
orthogonal.The algorithms are based on a shift-and-invert approach.Only a
single element of the inverse of the shifted matrix eventually needs to
becomputed with double the working precision. 


### Contents

The file `arrowhead1.jl` contains definitions of types `SymArrow` (arrowhead) and `SymDPR1`. Full matrices are accessible with the command `full(A)`.

The file `arrowhead3.jl` contains routines to generate random symmetric
arrowhead and DPR1 matrices, ` GenSymArrow` and `GenSymDPR1`, respectively,
three routines called `inv` which compute various inverses of _SymArrow_
matrices, two routines called `bisect` which compute outer eigenvalues of
_SymArrow_ and _SymDPR1_ matrices, main computational routine `aheig` which
computes the k-th eigenpair of an ordered unreduced  _SymArrow_, 
and the driver routine `aheigall` which computes all eigenvalues and
eigenvectors of a _SymArrow_. 

The file `arrowhead4.jl` contains three routines called `inv` which compute
various inverses of _SymDPR1_ matrices, main computational routine `dpr1eig`
which computes the k-th eigenpair of an ordered unreduced _SymDPR1_, 
and the driver routine `dpr1eigall` which computes all eigenvalues and
eigenvectors of a _SymDPR1_. 

The file `arrowhead5.jl` contains definition of type `HalfArrow`. 
_HalfArrow_ is of the form _[diagm(A.D) A.z]_ where either 
_length(A.z)=length(A.D)_
or _length(A.z)=length(A.D)+1_, thus giving two possible different forms of
SVD rank one update.  The file `arrowhead6.jl` contains the routine
`doubledot`, three routines called `inv` which compute
various inverses of _HalfArrow_ matrices, main computational routine `ahsvd`
which computes the k-th singular value triplet _u, sigma, v_ of an ordered
unreduced _HalfArrow_,  and the driver routine `ahsvdall` which computes all 
singular values and vectors of a _HalfArrow_. 

### Authors

The routines were developed and analysed by [Jakovcevic Stor, Barlow and
Slapnicar (2013)][JSB2013] (see also the [preprint][JSB2013a] and [Jakovcevic
Stor, Barlow and Slapnicar (2014)][JSB2014]. The Matlab version of the
routines used in the papers are written Ivan Slapnicar and Nevena Jakovcevic
Stor. This version of Julia routines is written by Ivan Slapnicar during visit
to MIT. 

Double the working precision is implemeted by using routines by 
[T. J. Dekker (1971)][dekker1971] from the package [DoubleDouble][byrne2014]
by Simon Byrne. 

### Thanks

Highly appreciated help and advice came from [Jiahao Chen][jiahao], 
[Andreas Noack][andreasnoack], [Jake Bolewski][jakebolewski] and 
[Simon Byrne][simonbyrne].   


[JSB2013]: http://www.sciencedirect.com/science/article/pii/S0024379513006265 "Nevena Jakovcevic Stor, Ivan Slapnicar and Jesse L. Barlow, 'Accurate eigenvalue decomposition of real symmetric arrowhead matrices and applications', Linear Algebra and its Applications, to appear, DOI: 10.1016/j.laa.2013.10.007"

[JSB2013a]: http://arxiv.org/abs/1302.7203 "Nevena Jakovcevic Stor, Ivan Slapnicar and Jesse L. Barlow, 'Accurate eigenvalue decomposition of arrowhead matrices and applications', arXiv:1302.7203v3"

[JSB2014]:#1 "Nevena Jakovcevic Stor, Ivan Slapnicar and Jesse L. Barlow, 'Forward stable eigenvalue decomposition of rank-one modifications of diagonal matrices', submitted"

[dekker1971]: http://link.springer.com/article/10.1007%2FBF01397083  "T.J. Dekker (1971) 'A floating-point technique for extending the available precision', Numerische Mathematik, Volume 18, Issue 3, pp 224-242"

[byrne2014]: https://github.com/simonbyrne/DoubleDouble.jl

[jiahao]: https://github.com/jiahao
[andreasnoack]: https://github.com/andreasnoack
[jakebolewski]: https://github.com/jakebolewski
[simonbyrne]: https://github.com/simonbyrne

