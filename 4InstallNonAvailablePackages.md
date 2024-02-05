# How to install non-available packages in Spack

There may be situations where Spack does not have a built-in package recipe for the software of interest.
In this case, we may encounter two different scenarios:
- The package we are looking for is a dependency of an already installed package, and Spack does not indicate it.
- The package is not present in Spack or in any already installed package.

## First option

The package we are looking for is a dependency of an already installed package, and Spack does not indicate it.
For example, we want to install the `datetime` package, which is a package related to Python.

```
spack list datetime
perl-datetime                 perl-datetime-format-mysql   perl-datetime-format-pg        perl-datetime-locale    perl-rose-datetime  py-metomi-isodatetime  r-assertive-datetimes
perl-datetime-format-builder  perl-datetime-format-oracle  perl-datetime-format-strptime  perl-datetime-timezone  py-jdatetime        py-parsedatetime
==> 13 packages
```
Spack provides 13 available packages for the `datetime` package, but none of the available options is suitable for the `datetime` package we are looking for.
REMEMBER: You can search for information on Spack packages at: https://packages.spack.io/

Before installing the `datetime` package through official channels and importing it into Spack, let's check if this package already exists in the dependencies of the Python package in Spack.

You can find information about all installed packages in this directory. NOTE: The last two directories can change depending on your operating system and compiler.
```
cd /home/ehernandez/spack/opt/spack/linux-ubuntu22.04-zen3/gcc-11.4.0
ls

utoconf-2.72-p3ypj4gzk5rlkjkonhh6f6x2douure65                       libunistring-1.1-uskpngh2hhhu4qainoib4ovycjfznx6y                   py-hatchling-1.21.0-z3ce65y25osvr36uvhrpef4i7hniba2u
automake-1.16.5-nkrysyz444rr5sbyu2g4cjfhogrhoipi                     libxcrypt-4.4.35-mqqhrwkp7bxu7e75lyjr5nnaez6trg3e                   py-hatch-vcs-0.3.0-x5pki2wuv4w2q6krwyn5qmgu7tszynfc
berkeley-db-18.1.40-hgsftwpjj3hppgloqnmocehvbpoefmgv                 libxml2-2.10.3-tjbcjhhr5sjgxhgr7fydveet76ibla2s                     py-idna-3.4-lpstrupg2dwav33thuetohqrhn3n22li
bison-3.8.2-3dqskzapemyvkvhbggyeifn2a2nb4pho                         lz4-1.9.4-zjhtdf3ifafrew2vh4sycijn4ql7idty                          py-mpi4py-3.1.5-li6zksko7x3yttf6xaex7xgn4yiaeegg
bzip2-1.0.8-lxtgn6gib42rffsmifomp6hbev7fp5o6                         m4-1.4.19-yf3ekzchxpzzl72swltgw453gq6w32bp                          py-packaging-23.1-37ztm7ix25nu2gzjr63whns26kz6a7wf
ca-certificates-mozilla-2023-05-30-q2v7g4xqfujzqrfpztkaq4rwxzo4je3l  ncurses-6.4-sp2arqfc4rxfjsuzw3rt7lszywv5husq                        py-pathspec-0.11.1-5an657rlt724owpkdao2iqxxq43uiaeo
c-blosc-1.21.5-boefecnyml25qypm464tk3n7yvtwkrad                      netcdf-c-4.9.2-ps4dvcluegr7fv7tvidtlpm4q5igbe4z                     py-pip-23.1.2-kpz5plbq7zc4dryrjmwbt4dictp6uhnf
cmake-3.27.9-7xqlwsrqbh4yfqceceoci4iamn5uslv2                        nghttp2-1.57.0-gt74nas4ahvmejbm26zelguuiuudteuu                     py-pluggy-1.0.0-umndg6rtp3rivulk6akkcvoui5zk3zmb
curl-8.4.0-sjr6emmfyvfcmy767hofhuygnjgk3ca6                          ninja-1.11.1-e3g7bylwelpirchanxh4gjbxuphakt7p                       py-pycparser-2.21-ul46w3v3ex3o4njol4s7lvy64hbjtcys
diffutils-3.9-h3ezqvbnxfc4onkosrgwdjtqzho2iflr                       numactl-2.0.14-c3vazzp7gvjg3go7fswfjonm45ybetho                     py-pyproject-metadata-0.7.1-zsmjw4eotrkypfrnt4pgbhnhkcfkn62k
ecbuild-3.7.2-ww7am4pwxmiehfj7vy5w2wzk4agx6ewb                       openblas-0.3.26-abivaw3sb5kmklguh7r426okcidk6a2r                    py-python-dateutil-2.8.2-ocy2bdj2p2kq7iyccikflcbhtndu5g7z
eccodes-2.32.0-4ojk6jljpkd4x2bh6zkvtc5hxwhppqmz                      openjpeg-2.3.1-jb3dypailcg34u7qjac6knlkmwkgn7d3                     py-pytz-2023.3-dosor2i3j244c7e7nvy2p5ndvctkdazl
expat-2.5.0-gsmestxu4daopnnb32z3bavv36fetsjq                         openmpi-5.0.1-qecqeughxmhs24ikd53hopiuefgecthk                      py-requests-2.31.0-ka7eyxg6ibar4welbnpl774nqgfkkver
findutils-4.9.0-4z5otqlnuhnh5v2ppyow4vk2264z6dxv                     openssh-9.5p1-h5t4ulsiats625bbpktgc4nj7i6l2i2w                      py-setuptools-68.0.0-iqm5i253xztvnofqquiizezvpece4fu6
gcc-runtime-11.4.0-by6vupskncx4shv4qf4ov3ujhv2ywga3                  openssl-3.1.3-2j5fan23u77vegefozwslhl7yydpvnb5                      py-setuptools-scm-7.1.0-xw6kzosd4ial6ygzbvfgmap5mlb7phca
gdbm-1.23-oe6gpg4v644w6htk6ynkwczsklgzgv42                           pcre2-10.42-opv5y2szclegl6dssra6ininrixjomim                        py-six-1.16.0-ptxowocr7byngx3rb72rvohtdwijsjbe
gettext-0.22.4-mqe3g6xucnwhzod2p5ymlt4twjldff6x                      perl-5.38.0-5b43jclbbvyux6alyfzn66dmjhbtrmb2                        python-3.11.6-7m5ejfpgt5ze5lj6awiv2inm6lxomzvh
git-2.42.0-ap622qpky543sba33j6kkz2oncorv5hd                          pigz-2.8-cr4ilc56fkjlg3atag3ab2hdlqwi7cgz                           py-tomli-2.0.1-iv5o6d422nhaby4lw7kqdmtcplhrfgzr
gmake-4.4.1-c75375jvpaabbzeawfh5pxgwv2qqpyzs                         pkgconf-1.9.5-nfuyb4idnqqowmgaq4f5sn5awlllcxqa                      py-trove-classifiers-2023.8.7-qbeltcsi5dnuzslgrgnjed7ljkbc6poa
hdf5-1.14.3-dybrb5g5olif3bgku4rhpknuda53n7jv                         pmix-5.0.1-rgmgo2ckwgvo4hvomsmxxcjfqzsakal3                         py-typing-extensions-4.8.0-wxhdqmja4yx5bul4ppt5dj7fpd2er5a2
hwloc-2.9.1-hoduqqxdxeftpz6ugf67mzanulyz5onz                         py-attrs-23.1.0-qlgr5ta4ir7o3ref2b37ckh53uext2ab                    py-urllib3-2.1.0-3lko647wv5ncdddt27byfaf6f4nnbg4g
krb5-1.20.1-zrrrflvolozhyu6z3i4lxu5kteudsj4o                         py-calver-2022.6.26-i5tqma2bp2jyy35krit76duepv2he7fs                py-versioneer-0.29-tgggpjpdfb3gnvhbz7a66brabitonznp
libaec-1.0.6-holprx2q2wsj5r2wmhqvovhztphj3y2o                        py-certifi-2023.7.22-5d2ql22xo2u35acxxsdoplsht54i4vbq               py-wheel-0.41.2-qtfa76btwfayzvanpa3o75aqw3vl6rj5
libbsd-0.11.7-qwdv5lkxzlzhvkbkyx2eclfc3uv3y5fd                       py-cffi-1.15.1-nj6pgnyk3nodkwtvtja7und6om2mqlzz                     re2c-2.2-t75kos7mf35vzb4ymusstirgqwyag3fm
libedit-3.1-20210216-pab62nnnyhvwp5nkx7yzw7exfertuzfi                py-charset-normalizer-3.3.0-wb7mobatahdtk73n7ysntc65obp4woam        readline-8.2-icxntbarpsiikvt5erulrgygavue3rn2
libevent-2.1.12-rjsfgqew2wsbhykf4ofgdohgc6gthmad                     py-click-8.1.7-ox6vxmgn4xio2mz5ciqy2cxlldnsstkh                     snappy-1.1.10-m7zl3nzlrsiwcspcz7qnxehht2r4wefu
libffi-3.4.4-h3hsz5wtuxxqrtytpmk7sko4u56dutfi                        py-cython-0.29.36-wwyqvirbf4o26dvgx3ov7nne7epyrybl                  sqlite-3.43.2-p6vfaqjinpqcs4nmy2i3tmd4ja6p3lm4
libiconv-1.17-mi6csqhr6dmz2oxnivlgiitapgbzn7jb                       py-dtcv2-util-0.0.60-3cfi46c7w5efvcecbkm4luzm3riaapsi               tar-1.34-dxmcefjvtochnl4qaw5ibazvlc4zz4wt
libidn2-2.3.4-vfg4vcivbq4jutifgncfxlm52pdcb2ap                       py-ecmwflibs-0.5.3-6asbof67gd7uxsn6f343mvwtw4p7uxol                 util-linux-uuid-2.38.1-2eayeglipzm6gqwtc5i47u76keztbwd4
libmd-1.0.4-z2cgmz7htjzldorzgu5xuhcsckvpcytg                         py-editables-0.3-kmvq4eytnj6jybubulyejhkwljjbkzmi                   util-macros-1.19.3-oqfpy65ylf67uh7fajtn2eh34kuicsnk
libpciaccess-0.17-z27uhqrpalyvjdlz6cwsqzast5mhtq4s                   py-findlibs-0.0.2-qj6b4xswyjqct62saoaldipzanz2wpng                  xz-5.4.1-chthbuhxasm3wcdl2qk44z3r26l3ebjh
libsigsegv-2.14-5icouuknhpgq7atycscj4rbybqwqlh45                     py-flit-core-3.9.0-g2qnxes4c7ipvnhe26otz734ldjbv3w6                 zlib-ng-2.1.5-6xvag3igdnqz7vogs37h4znmdqcaomwq
libtool-2.4.7-xh5ixusiijq4fv3rm4upax77z625owbh                       py-hatch-fancy-pypi-readme-23.1.0-geft3yonwonmyozni4t5jhwvqvg5lx2s  zstd-1.5.5-pucqyot464qxc3l46wx7n2xe6zojslwy
```
Now, we are going to check if `datetime` is inside the Python package
```
ls python-3.11.6-7m5ejfpgt5ze5lj6awiv2inm6lxomzvh/include/python3.11
abstract.h         compile.h              enumobject.h   genericaliasobject.h  marshal.h       opcode.h      py_curses.h    pymacconfig.h  pystrtod.h     sliceobject.h   tupleobject.h
bltinmodule.h      complexobject.h        errcode.h      import.h              memoryobject.h  osdefs.h      pydtrace.h     pymacro.h      Python.h       structmember.h  typeslots.h
boolobject.h       cpython                exports.h      internal              methodobject.h  osmodule.h    pyerrors.h     pymath.h       pythonrun.h    structseq.h     unicodeobject.h
bytearrayobject.h  datetime.h             fileobject.h   intrcheck.h           modsupport.h    patchlevel.h  pyexpat.h      pymem.h        pythread.h     sysmodule.h     warnings.h
bytesobject.h      descrobject.h          fileutils.h    iterobject.h          moduleobject.h  pybuffer.h    pyframe.h      pyport.h       pytypedefs.h   token.h         weakrefobject.h
ceval.h            dictobject.h           floatobject.h  listobject.h          object.h        pycapsule.h   pyhash.h       pystate.h      rangeobject.h  traceback.h
codecs.h           dynamic_annotations.h  frameobject.h  longobject.h          objimpl.h       pyconfig.h    pylifecycle.h  pystrcmp.h     setobject.h    tracemalloc.h

```
As we can see, the `datetime` package is included, so there's no need to install it.
Another option to check if the `datetime` package is installed is, with the environment active and the Python package already installed, execute Python in the command line and try to import the `datetime` package. 
If it does not throw an error, this indicates that it is included.
```
ehernandez@ehernandez-TITAN:~$ python
Python 3.11.6 (main, Jan 24 2024, 13:09:23) [GCC 11.4.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import datetime
>>> 
```
## Second option
The package is not present in Spack or in any already installed package. 

### Download the correct package version

In this section of the tutorial, we will install the package `dtcv2_utils` with their dependencies from the source by finding the appropriate version from official sources. 
For Python packages, we can refer to https://pypi.org/. 
In the download section of each package on PyPi, you can find various download options depending on the operating system where it needs to be installed.
- For Windows: win_amd64
- For macOS: macosx
- For Linux: manylinux

Some packages don't have different download links for each version. In these cases, search for the package with "none-any.whl" extension.

To download the last version of the package go to https://test.pypi.org/project/dtcv2-util/ and download the package with "none-any.whl" extension.

Once the download has finished, open the file on your system using a file manager and access the "METADATA" in the dtcv2_util-0.0.60.dist-info folder.

```
Metadata-Version: 2.1
Name: dtcv2-util
Version: 0.0.60
Summary: Library for workflow management
Home-page: https://gitlab.geo3bcn.csic.es/dtgeo/dtc-v2/meteo-gfs
Author: Alejandra Guerrero - DTGEO
Author-email: aguerrero@geo3bcn.csic.es
License: MIT
Description-Content-Type: text/markdown
Requires-Dist: datetime
Requires-Dist: eccodes
Requires-Dist: ecmwflibs
Requires-Dist: cfgrib
Requires-Dist: xarray
Requires-Dist: requests
Requires-Dist: netcdf4

# DTCV2-utils
The library 
```
Each "Requires-Dist" label indicates the dependencies of the dtcv2-util package. You must install all of them before installing this package.
Once all dependencies are installed, let's create the package.py file for the "dtcv2-util" package using the link of the package within download page.

### Create package.py 
```
spack create https://test-files.pythonhosted.org/packages/4b/75/9956049142e7d07eaa7bde7baccf6fcb9beec7d3bc21466c165386808ebe/dtcv2_util-0.0.60-py3-none-any.whl
```
Once this command is executed, Spack will have created the following file.
```
#
# You can edit this file again by typing:
#
#     spack edit py-dtcv2-util
#
# See the Spack documentation for more information on packaging.
# ----------------------------------------------------------------------------

from spack.package import *


class PyDtcv2Util(PythonPackage):
    """FIXME: Put a proper description of your package here."""

    # FIXME: Add a proper url for your package's homepage here.
    homepage = "https://www.example.com"
    url = "https://test-files.pythonhosted.org/packages/4b/75/9956049142e7d07eaa7bde7baccf6fcb9beec7d3bc21466c165386808ebe/dtcv2_util-0.0.60-py3-none-any.whl"

    # FIXME: Add a list of GitHub accounts to
    # notify when the package is updated.
    # maintainers("github_user1", "github_user2")

    # FIXME: Add the SPDX identifier of the project's license below.
    # See https://spdx.org/licenses/ for a list. Upon manually verifying
    # the license, set checked_by to your Github username.
    license("UNKNOWN", checked_by="github_user1")

    version("0.0.60", sha256="c8a27488103d62f48ad739c576a223ab5c23f3972a0ce2037fb99bf756aa6fcc", expand=False)

    # FIXME: Only add the python/pip/wheel dependencies if you need specific versions
    # or need to change the dependency type. Generic python/pip/wheel dependencies are
    # added implicity by the PythonPackage base class.
    # depends_on("python@2.X:2.Y,3.Z:", type=("build", "run"))
    # depends_on("py-pip@X.Y:", type="build")
    # depends_on("py-wheel@X.Y:", type="build")

    # FIXME: Add a build backend, usually defined in pyproject.toml. If no such file
    # exists, use setuptools.
    # depends_on("py-setuptools", type="build")
    # depends_on("py-hatchling", type="build")
    # depends_on("py-flit-core", type="build")
    # depends_on("py-poetry-core", type="build")

    # FIXME: Add additional dependencies if required.
    # depends_on("py-foo", type=("build", "run"))

    def config_settings(self, spec, prefix):
        # FIXME: Add configuration settings to be passed to the build backend
        # FIXME: If not needed, delete this function
        settings = {}
        return settings
```
When you add a new package to Spack, it automatically assigns a name to the package; in this case, py-dtcv2-util. You can find the name at the top of the file.
For now, we have to edit two sections; the first one to modify is the "url" and "homepage" section.
We have the following:
```
 # FIXME: Add a proper url for your package's homepage here.
    homepage = "https://www.example.com"
    url = "https://test-files.pythonhosted.org/packages/4b/75/9956049142e7d07eaa7bde7baccf6fcb9beec7d3bc21466c165386808ebe/dtcv2_util-0.0.60-py3-none-any.whl"
```
Change it for this:
```
homepage = "https://test.pypi.org/project/dtcv2-util/"
url      = "https://test-files.pythonhosted.org/packages/4b/75/9956049142e7d07eaa7bde7baccf6fcb9beec7d3bc21466c165386808ebe/dtcv2_util-0.0.60-py3-none-any.whl"
list_url = "https://test.pypi.org/project/dtcv2-util/#files"
```
Save the file.

Since we are providing a url, we can confirm the checksum, or sha256 calculation. Exit your editor to return to the command line and use the spack checksum command:
```
spack checksum py-dtcv2-util
==> Found 1 version of py-dtcv2-util
==> Fetching https://test-files.pythonhosted.org/packages/4b/75/9956049142e7d07eaa7bde7baccf6fcb9beec7d3bc21466c165386808ebe/dtcv2_util-0.0.60-py3-none-any.whl

    version("0.0.60", sha256="c8a27488103d62f48ad739c576a223ab5c23f3972a0ce2037fb99bf756aa6fcc", expand=False)
```
From the command line, we can check the build and run dependencies required by this new package.

```
spack info py-dtcv2-util

PythonPackage:   py-dtcv2-util

Description:
    FIXME: Put a proper description of your package here.

Homepage: https://www.example.com

Preferred version:  
    0.0.60    https://test-files.pythonhosted.org/packages/4b/75/9956049142e7d07eaa7bde7baccf6fcb9beec7d3bc21466c165386808ebe/dtcv2_util-0.0.60-py3-none-any.whl

Safe versions:  
    0.0.60    https://test-files.pythonhosted.org/packages/4b/75/9956049142e7d07eaa7bde7baccf6fcb9beec7d3bc21466c165386808ebe/dtcv2_util-0.0.60-py3-none-any.whl

Deprecated versions:  
    None

Variants:
    build_system [python_pip]        python_pip
        Build systems supported by the package

Build Dependencies:
    py-pip  py-wheel  python

Link Dependencies:
    None

Run Dependencies:
    python

Licenses: 
    UNKNOWN

```
In this case, we don't need to add the dependencies py-pip, python, and py-wheel within dtcv2-util package.py because we don't require a specific version of each package, as indicated in the package.py file.
If needed, you can add the build and run dependencies following the examples inside the package.py file.

```
# depends_on("py-foo", type=("build", "run"))
# depends_on("python@2.X:2.Y,3.Z:", type=("build", "run"))
```
Now, you can add and install the package py-dtcv2-util in your environment.
```
spack install --add py-dtcv2-util
```
When finished, we can check if it appears in the installed packages section.
```
spack find

==> In environment /home/ehernandez/demodtgeo
==> Root specs
eccodes   py-cfgrib   py-dtcv2-util   py-ecmwflibs   py-netcdf4   py-requests   py-xarray   python 

==> Installed packages
-- linux-ubuntu22.04-zen3 / gcc@11.4.0 --------------------------
autoconf@2.72                       gettext@0.22.4        libtool@2.4.7     pcre2@10.42                  py-eccodes@1.5.0                   py-pip@23.1.2                  py-xarray@2023.7.0
automake@1.16.5                     git@2.42.0            libunistring@1.1  perl@5.38.0                  py-ecmwflibs@0.5.3                 py-pluggy@1.0.0                python@3.11.6
berkeley-db@18.1.40                 gmake@4.4.1           libxcrypt@4.4.35  pigz@2.8                     py-editables@0.3                   py-pycparser@2.21              re2c@2.2
bison@3.8.2                         hdf5@1.14.3           libxml2@2.10.3    pkgconf@1.9.5                py-findlibs@0.0.2                  py-pyproject-metadata@0.7.1    readline@8.2
bzip2@1.0.8                         hwloc@2.9.1           lz4@1.9.4         pmix@5.0.1                   py-flit-core@3.9.0                 py-python-dateutil@2.8.2       snappy@1.1.10
c-blosc@1.21.5                      krb5@1.20.1           m4@1.4.19         py-attrs@23.1.0              py-hatch-fancy-pypi-readme@23.1.0  py-pytz@2023.3                 sqlite@3.43.2
ca-certificates-mozilla@2023-05-30  libaec@1.0.6          ncurses@6.4       py-bottleneck@1.3.7          py-hatch-vcs@0.3.0                 py-requests@2.31.0             tar@1.34
cmake@3.27.9                        libbsd@0.11.7         netcdf-c@4.9.2    py-calver@2022.6.26          py-hatchling@1.21.0                py-setuptools@68.0.0           util-linux-uuid@2.38.1
curl@8.4.0                          libedit@3.1-20210216  nghttp2@1.57.0    py-certifi@2023.7.22         py-idna@3.4                        py-setuptools-scm@7.1.0        util-macros@1.19.3
diffutils@3.9                       libevent@2.1.12       ninja@1.11.1      py-cffi@1.15.1               py-mpi4py@3.1.5                    py-six@1.16.0                  xz@5.4.1
ecbuild@3.7.2                       libffi@3.4.4          numactl@2.0.14    py-cfgrib@0.9.9.0            py-netcdf4@1.6.2                   py-tomli@2.0.1                 zlib-ng@2.1.5
eccodes@2.32.0                      libiconv@1.17         openblas@0.3.26   py-cftime@1.0.3.4            py-numexpr@2.8.4                   py-trove-classifiers@2023.8.7  zstd@1.5.5
expat@2.5.0                         libidn2@2.3.4         openjpeg@2.3.1    py-charset-normalizer@3.3.0  py-numpy@1.26.3                    py-typing-extensions@4.8.0
findutils@4.9.0                     libmd@1.0.4           openmpi@5.0.1     py-click@8.1.7               py-packaging@23.1                  py-urllib3@2.1.0
gcc-runtime@11.4.0                  libpciaccess@0.17     openssh@9.5p1     py-cython@0.29.36            py-pandas@1.5.3                    py-versioneer@0.29
gdbm@1.23                           libsigsegv@2.14       openssl@3.1.3     py-dtcv2-util@0.0.60         py-pathspec@0.11.1                 py-wheel@0.41.2
==> 108 installed packages
```








