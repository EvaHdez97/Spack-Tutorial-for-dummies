# Create an independent environment and activate it

## Create environments

An environment is like a virtualized Spack instance that you can use to aggregate package installations for a project or other purpose. 
It has an associated view, which is a single prefix where all packages from the environment are linked.

### Create environment
```
spack env create myproject
==> Created environment 'myproject' in /home/spack/spack/var/spack/environments/myproject
==> You can activate this environment with:
==>   spack env activate myproject
```
### List environments in Spack

```
spack env list
==> 1 environments
    myproject
```
### Activate an environment

```
spack env activate myproject
```
### List packages inside environment

```
spack find
```
### Check what environment you are in

```
spack check status
```
### Deactivate an environment
```
spack env deactivate
```
### Create an independent environment

Environments do not have to be created in or managed by a Spack instance. Rather, their environment files can be placed in any directory. 
This feature can be quite helpful for use cases such as environment-based software releases and CI/CD.
```
cd

mkdir code

spack env create -d code
==> Created environment in /home/spack/code
==> You can activate this environment with:
==>   spack env activate /home/spack/code
```
Notice that the command shows Spack created the environment, updated the view, and printed the command needed to activate it. As we can see in the activation command, since the environment is independent, it must be referenced by its directory path.

Let’s see what really happened with this command by listing the directory contents and looking at the configuration file:
```
ls
spack.yaml

cat spack.yaml

This is a Spack Environment file.
It describes a set of packages to be installed, along withconfiguration settings.
spack:
add package specs to the `specs` list
  specs: []
  view: true
  concretizer:
    unify: true
```
Notice that Spack created a spack.yaml file in the code directory. Also note that the configuration file has an empty spec list (i.e., []). 
That list is intended to contain only the root specs of the environment.

To activate the independent environment:
```
spack env activate .
```



