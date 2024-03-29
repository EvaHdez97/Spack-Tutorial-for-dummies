# Spack tutorial for Dummies

This is a guide for learning how to install Spack and set up an independent environment. The goal is to extract all package.py files from the software's dependencies and generate the spack.yaml file.

ATTENTION: If you are using Python PyPI packages, add them to the 'pip' subsection of the 'spack.yaml' file. In case you have packages that require parallelism and/or use vectors or matrices, create a Spack package and add it to the 'specs' section of the 'spack' subsection of the 'spack.yaml' file.

## Repository structure

1. Install and activate spack
2. Create an independent environment and activate it
3. How to install available packages in Spack
4. How to install non-available packages in Spack
5. Spack.yaml file and package.py
