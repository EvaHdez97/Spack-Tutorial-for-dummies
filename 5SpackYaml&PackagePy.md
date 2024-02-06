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

