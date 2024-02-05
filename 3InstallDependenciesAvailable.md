# How to install dependencies available in Spack

## List of available packages in Spack
```
spack list
```
### Search for a specific package in Spack
```
spack list eccodes
eccodes py-eccodes
==> 2 packages
```
To find out which Spack package among the available options best suits your needs, you can search for information about Spack packages at this URL.
https://packages.spack.io/

### Add a package to your environment

```
spack add py-numpy
==> Adding py-numpy to environment myproject
```
Check if package has been added correctly
```
spack find
==> In environment myproject
==> Root specs
py-numpy 

==> 0 installed packages
```

### Install a package in your environment

Let's install the previously added package, py-numpy.
```
spack install py-numpy
```
Now check if the environment has been updated.
```
spack find
==> In environment myproject
==> Root specs
py-numpy 

==> Installed packages
-- linux-ubuntu22.04-zen3 / gcc@11.4.0 --------------------------
berkeley-db@18.1.40                 gcc-runtime@11.4.0  libffi@3.4.4      ncurses@6.4      pigz@2.8            py-packaging@23.1            python@3.11.6  util-linux-uuid@2.38.1
bzip2@1.0.8                         gdbm@1.23           libiconv@1.17     ninja@1.11.1     pkgconf@1.9.5       py-pip@23.1.2                re2c@2.2       xz@5.4.1
ca-certificates-mozilla@2023-05-30  gettext@0.22.4      libmd@1.0.4       openblas@0.3.26  py-cython@0.29.36   py-pyproject-metadata@0.7.1  readline@8.2   zlib-ng@2.1.5
diffutils@3.9                       gmake@4.4.1         libxcrypt@4.4.35  openssl@3.1.3    py-flit-core@3.9.0  py-setuptools@68.0.0         sqlite@3.43.2  zstd@1.5.5
expat@2.5.0                         libbsd@0.11.7       libxml2@2.10.3    perl@5.38.0      py-numpy@1.26.3     py-wheel@0.41.2              tar@1.34
==> 39 installed packages
```
You can add and install a package at the same time too.
```
spack install --add py-numpy
```
### How to add a specific version of a package

Sometimes, due to software requirements, it is necessary to install a specific version of a package because the software demands it. 
You can install a specific version of a Spack package as follows:

```
spack install --add py-numpy@1.26.3
```
### How to upgrade a package

In Spack, there isn't a specific command to upgrade packages within an environment. 
The only way to achieve this is by uninstalling and removing the existing package, and then adding and installing the new version.

```
spack uninstall py-numpy
spack remove py-numpy
```
One of the possible errors that can occur with this action is that it may not be able to uninstall it properly due to dependencies. 

```
spack remove py-numpy
==> Refusing to uninstall the following specs
    -- linux-ubuntu22.04-zen3 / gcc@11.4.0 --------------------------
    havquus py-numpy@1.26.3

==> The following dependents are still installed:
    -- linux-ubuntu22.04-zen3 / gcc@11.4.0 --------------------------
    aigfqu4 py-bottleneck@1.3.7  2ik62py py-cftime@1.0.3.4  jzdrj5l py-netcdf4@1.6.2  s7abjru py-pandas@1.5.3
    gs35sc6 py-cfgrib@0.9.9.0    b3g5m2l py-eccodes@1.5.0   kr4gqp6 py-numexpr@2.8.4  seqorzg py-xarray@2023.7.0

==> Error: There are still dependents.
  use `spack uninstall --dependents` to remove dependents too
  use `spack uninstall --force` to override
==> py-numpy has been removed from /home/ehernandez/spack/var/spack/environments/myproject/spack.yaml
```
In this case, the following command is used to uninstall them:
```
spack uninstall --dependents py-numpy
```
Now it works:
```
    -- linux-ubuntu22.04-zen3 / gcc@11.4.0 --------------------------
    aigfqu4 py-bottleneck@1.3.7  2ik62py py-cftime@1.0.3.4  jzdrj5l py-netcdf4@1.6.2  havquus py-numpy@1.26.3  seqorzg py-xarray@2023.7.0
    gs35sc6 py-cfgrib@0.9.9.0    b3g5m2l py-eccodes@1.5.0   kr4gqp6 py-numexpr@2.8.4  s7abjru py-pandas@1.5.3

==> 9 packages will be uninstalled. Do you want to proceed? [y/N] y
==> Successfully uninstalled py-xarray@2023.7.0%gcc@11.4.0~io~parallel build_system=python_pip arch=linux-ubuntu22.04-zen3/seqorzg
==> Successfully uninstalled py-cfgrib@0.9.9.0%gcc@11.4.0~xarray build_system=python_pip arch=linux-ubuntu22.04-zen3/gs35sc6
==> Successfully uninstalled py-pandas@1.5.3%gcc@11.4.0~excel build_system=python_pip arch=linux-ubuntu22.04-zen3/s7abjru
==> Successfully uninstalled py-numexpr@2.8.4%gcc@11.4.0 build_system=python_pip arch=linux-ubuntu22.04-zen3/kr4gqp6
==> Successfully uninstalled py-netcdf4@1.6.2%gcc@11.4.0+mpi build_system=python_pip patches=255b5ae arch=linux-ubuntu22.04-zen3/jzdrj5l
==> Successfully uninstalled py-cftime@1.0.3.4%gcc@11.4.0 build_system=python_pip arch=linux-ubuntu22.04-zen3/2ik62py
==> Successfully uninstalled py-eccodes@1.5.0%gcc@11.4.0 build_system=python_pip arch=linux-ubuntu22.04-zen3/b3g5m2l
==> Successfully uninstalled py-bottleneck@1.3.7%gcc@11.4.0 build_system=python_pip arch=linux-ubuntu22.04-zen3/aigfqu4
==> Successfully uninstalled py-numpy@1.26.3%gcc@11.4.0 build_system=python_pip patches=873745d arch=linux-ubuntu22.04-zen3/havquus
==> Updating view at /home/ehernandez/spack/var/spack/environments/myproject/.spack-env/view
```
Now if we check the environment we won't see the py-numpy package within the installed packages section:
```
==> In environment myproject
==> No root specs
==> Installed packages
-- linux-ubuntu22.04-zen3 / gcc@11.4.0 --------------------------
berkeley-db@18.1.40                 gcc-runtime@11.4.0  libffi@3.4.4      ncurses@6.4      pigz@2.8            py-pip@23.1.2                re2c@2.2                xz@5.4.1
bzip2@1.0.8                         gdbm@1.23           libiconv@1.17     ninja@1.11.1     pkgconf@1.9.5       py-pyproject-metadata@0.7.1  readline@8.2            zlib-ng@2.1.5
ca-certificates-mozilla@2023-05-30  gettext@0.22.4      libmd@1.0.4       openblas@0.3.26  py-cython@0.29.36   py-setuptools@68.0.0         sqlite@3.43.2           zstd@1.5.5
diffutils@3.9                       gmake@4.4.1         libxcrypt@4.4.35  openssl@3.1.3    py-flit-core@3.9.0  py-wheel@0.41.2              tar@1.34
expat@2.5.0                         libbsd@0.11.7       libxml2@2.10.3    perl@5.38.0      py-packaging@23.1   python@3.11.6                util-linux-uuid@2.38.1
==> 38 installed packages
```






