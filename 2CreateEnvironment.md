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


