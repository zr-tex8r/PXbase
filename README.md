PXbase Package Bundle
=====================

LaTeX: Tools for use with (u)pLaTeX

The main purpose of this package is to provide auxiliary functions which
are utilized by packages created by the same author. This package also
provides a few user commands to assist in creating Japanese document on
(u)pLaTeX.

### System Requirements

  * TeX format: LaTeX.
  * TeX engine: pTeX and upTeX.
  * DVI-ware (in DVI output): Anything.

### Package content

  * `pxbase.sty`: the pxbase package
  * `pxbase.def`: a submodule (no longer used)
  * `pxbabel.sty`: the pxbabel package
  * `pxbasenc.def`: a submodule
  * `pxjsfenc.def`: a submodule
  * `pxbsjc.def`: a helper file for pxbase
  * `pxbsjc1.def`: a helper file for pxbase
  * `upkcat.sty`: the upkcat package

Some files are kept present for compatibility with other packages.

### Installation

In a system compliant to TDS 1.1, move the files as follows:

  - `*.sty` → $TEXMF/tex/platex/pxbase

And rehash your TEXMF trees if necessary.

### License

This package is distributed under the MIT License.


pxbase package ― the (quondam) base library for pTeX
-----------------------------------------------------

The package used to provide pTeX-specific features required by other
packages. However, it has been merged with the [bxbase] package since
v0.9, and currently it simply loads bxbase internally.

[bxbase]: https://www.ctan.org/pkg/bxbase


pxbabel package ― To help use Babel with Japanese document
-----------------------------------------------------------

Currently the documentation is available only in Japanese (see
pxbabel.pdf).


upkcat package ― To safely operate with kcatcode
-------------------------------------------------

Currently the documentation is available only in Japanese (see
README-ja.md).


Revision History
----------------

  * Version 1.4  〈2023/02/25〉
  * Version 1.3  〈2021/05/31〉
  * Version 1.2  〈2021/05/22〉
  * Version 1.1b 〈2017/07/03〉
  * Version 1.1a 〈2017/06/19〉
  * Version 1.1  〈2017/05/29〉
  * Version 0.5i 〈2017/05/04〉 ― for CTAN
  * Version 0.9b 〈2012/08/19〉
  * Version 0.5  〈2010/06/15〉
  * Version 0.4a 〈2010/02/07〉
  * Version 0.4  〈2009/07/05〉
  * Version 0.3  〈2008/04/06〉
  * Version 0.2b 〈2008/03/28〉
  * Version 0.2a 〈2008/03/18〉
  * Version 0.2  〈2008/03/14〉

--------------------
Takayuki YATO (aka. "ZR")  
https://github.com/zr-tex8r
