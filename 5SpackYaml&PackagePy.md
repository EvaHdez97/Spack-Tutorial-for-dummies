# Spack.yaml file and package.py files

## Package.py files 

In Spack, both the native Spack packages and the added packages that were not originally available have a package.py file that defines how to perform their installation and lists their dependencies.
In the following path, you can find the directories for all available Spack packages, including those installed externally. Inside each folder, you will find the package.py file.
```
ls /home/ehernandez/spack/var/spack/repos/builtin/packages
```
```
ls /home/ehernandez/spack/var/spack/repos/builtin/packages/py-dtcv2-util/
package.py  __pycache__
```
In the package.py file, there are several important sections to make it work:

1. The source and the information of the package
```
   # FIXME: Add a proper url for your package's homepage here.
    homepage = "https://test.pypi.org/project/dtcv2-util"
    url = "https://test-files.pythonhosted.org/packages/4b/75/9956049142e7d07eaa7bde7baccf6fcb9beec7d3bc21466c165386808ebe/dtcv2_util-0.0.60-py3-none-any.whl"
    list_url = "https://test.pypi.org/project/dtcv2-util/#files"
```
2.  The software version
```
    version("0.0.60", sha256="c8a27488103d62f48ad739c576a223ab5c23f3972a0ce2037fb99bf756aa6fcc", expand=False)
```
3. The dependencies
   
In this case, they have been added because a specific version of Python was required, there were pre-installation PyPI dependency packages that this package needed, and the wheel package to avoid the need to compile the source code of the package during installation, which is faster and easier.
```
   # FIXME: Only add the python/pip/wheel dependencies if you need specific versions
    # or need to change the dependency type. Generic python/pip/wheel dependencies are
    # added implicity by the PythonPackage base class.
    depends_on("python@3.8", type=("build", "run"))
    depends_on("py-pip", type="build")
    depends_on("py-wheel", type="build")
```
## Spack.yaml 

An environment is more than just a list of root specs. It includes configuration settings that affect the way Spack behaves when the environment is activated.
In environments created inside Spack, you can find their spack.yaml files in ~/spack/var/spack/environments/nameoftheproject. 
On the other hand, in independent environments, you can find the spack.yaml file inside the custom directory of the environment.
Environment inside spack:
```
ls ~/spack/var/spack/environments/myproject
spack.lock  spack.yaml

```
Independent environment:
```
ls ~/demodtgeo
spack.lock  spack.yaml

cat ~/demodtgeo/spack.yaml
# This is a Spack Environment file.
#
# It describes a set of packages to be installed, along with
# configuration settings.
spack:
  # add package specs to the `specs` list
  specs:
  - python
  - py-ecmwflibs
  - py-netcdf4
  - py-requests
  - py-xarray
  - py-cfgrib
  - eccodes
  - py-dtcv2-util
  view: true
  concretizer:
    unify: true
```
The output shows the special spack.yaml configuration file that Spack uses to store the environment configuration.

There are several important parts of this file:

    specs:: the list of specs to install

    view:: this controls whether the environment has a view. You can set it to false to disable view generation.

    concretizer:unify:: This controls how the specs in the environment are concretized.

The specs list should look familiar; these are the specs we’ve been modifying with spack add.

concretizer:unify:true, the default, means that they are concretized together, so that there is only one version of each package in the environment. Other options for unify are false and when_possible. false means that the specs are concretized independently, so that there may be multiple versions of the same package in the environment. when_possible lies between those options. In this case, Spack will unify as many packages in the environment, but will not fail if it cannot unify all of them.

