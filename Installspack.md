# Install and activate Spack

## System Prerequisites

Spack has the following minimum system requirements, which are assumed to be present on the machine where Spack is run:

These requirements can be easily installed on most modern Linux systems; on macOS, the Command Line Tools package is required, and a full XCode suite may be necessary for some packages such as Qt and apple-gl. 
Spack is designed to run on HPC platforms like Cray. Not all packages should be expected to work on all platforms.

## Debian/Ubuntu
```
apt update
apt install build-essential ca-certificates coreutils curl environment-modules gfortran git gpg lsb-release python3 python3-distutils python3-venv unzip zip
```
## macOS Brew
```
brew update
brew install curl gcc git gnupg zip
```

## Installation

Getting Spack is easy. You can clone it from the github repository using this command:
```
git clone -c feature.manyFiles=true https://github.com/spack/spack.git
```
This will create a directory called spack.
