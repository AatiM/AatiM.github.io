---
title: QuickStart
permalink: /QuickStart/
---

# Quickstart Guide

Our computing library is a Python library build on top of PyCOMPSs that provides distributed mathematical and machine learning algorithms through an easy-to-use interface. There are two ways that you can get started with our library. You can follow a [manual installation](), or you can download our ready-to-use [docker image]().

## Manual Installation
-----------------------------------------------------
### Requirements
--------------------------------------------------
Our library requires:
* pyCOMPSs>=2.7
* Scikit-learn>=0.19.1
* Scipy>=1.0.0
* NumPy>=1.15.4
* cvxpy>=1.1.5


Note: Some of the examples also require matplotlib>=2.0.0.

### Installation Steps
-------------------------------------------------
1. Check the pyCOMPSs version to install.
  * Our latest library requires pyCOMPSs 2.7 or greater (check [here]() for information about other releases.)
2. Install pyCOMPSs following these [instructions]().
3. Install our latest library version with `pip3 install library`
  * package requires the 'pycompss' Python module.
4. You can check whether everything is working fine by running one of these examples:
  * Download the latest source code [here]().
  * Run an example application.
  <br>
  `runcompss --python_interpreter=python3 our library-X.Y.Z/examples/kmeans.py`
<br>

## Set-up Docker
-------------------------------------------------------
### 1. Installing Docker and Docker-py
---------------------------------------------------
1.Follow these instructions:
  * [Docker for Mac]()
  * [Docker for Ubuntu]()
  * [Docker for Arch Linux]()

2.Add user to docker group to run our library as a non-root user.
  * [Instruction]()

3.Check that Docker is correctly installed

```
docker --version
docker ps # this should be empty as no docker processes are running yet
```

4.Install [docker-py]()

`pip3 install library`


### 2. Installing our Library
--------------------------------------------------------
`pip3 install library`

This should add our library executable to your path.


### 3. Starting our Library in your Development Directory
----------------------------------------------------------
Initialize our library where your source code will be. Then this will allow Docker to access your local code and run it inside the container.

```
# Without a path it operates on the current working directory.
our library init

# You can also provide a path
our library init/home/user/replace/path/
```  


### 4. Running Applications
---------------------------------------------------------
* Note: running the docker library does not work with applications with GUI or with visual plots such as `examples/clusteriing_comparison.py`

1.Clone our library repo and check out release branch vX.Y.Z:

`git clone https://github.com/bsc-wdc/library.git`

2.Init our library environment in the root of the repo. Initialize the library in a current directory and check whether the paths are correct running the file with `python3 path-to/file.py`

```
cd our library
our library Init
our library exec example/rf_iris.py
```
3.You can also init the library inside the example folder. This will mount the examples directory inside the container so you can execute it without adding the path:
```
cd library/examples
library init
library exec rf_iris.py
```
### 5. Running Jupyter Notebooks
----------------------------------------------------------
1.Run the following snippet from the root of the project:

```
our library init
our library jupyter ./notebooks
```
  * An alternative way of starting jupyter is using `our library run` command in the following way:
  `our library run jupyter-notebook ./notebooks --ip=0.0.0.0  --allow-root`

2.Access to your notebook by ctrl-clicking or copy pasting into the browser the link shown on the CLI(e.g. http://127.0.0.1:8889/?token=TOKEN_VALUE).

3.If you encounter this warning
`The port 8889 is already in use, trying another port`, you can fix it by restarting our library container with `our library init`.

### 6. Adding More Nodes
--------------------------------------------------------
There are two ways to add more computing nodes:

1.Let docker create more workers for you:
  * Issue the desired number of workers to be added. For example, `our library components add worker 2`

2.Manually create and config a custom node:
  * If you want to add a custom node, it is necessary to be reachable through ssh without user. Our library will try to copy the `working_dir` there, so it needs to write permissions for the scp. As an example:
  `our library components add worker 127.0.0.1:6`
