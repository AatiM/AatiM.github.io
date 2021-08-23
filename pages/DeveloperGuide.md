---
title: Developer's Guide
permalink: /DeveloperGuide/
---

# Developer's Guide
## Contributing to our Library
------------------------------------------------------------
The preferred workflow for contributing to our library is following steps:

1.Fork the project repository by clicking on the 'Fork' button near the top right of the page. This can create a copy of the code under your GitHub user account.

2.Clone your fork of our library repo from your GitHub account to your local disk:

```
$ git clone git@github.com:YourLogin/ourlibrary.git
$ cd ourlibrary
```

3.Create a `feature` branch to hold your development changes:

```
$ git checkout -b my-feature
```
4.Develop the feature on your feature branch.
 * Add changed files by using `git add`
 * Then using `git commit` files

```
$ git add modified_files
$ git commit
```

 in order to record all changes in Git, Push the changes to your GitHub account:
 ```
 $ git push -u origin my-features
 ```

5.Follow [these instructions](these instructions) to create a pull request from your fork. This will send an email to the committers.

## Drafting New Releases
------------------------------------------------------------
Before drafting a new release, ensure the latest version of the documentation built properly.
Follow these steps when drafting a new release:

1.Create and switch to a new branch named `release-x.y.`

2.Update in different steps:
* Update the release number accordingly in the [VERSION]() FILE.
* Update the required PyCOMPSs version in the [QuickStart Guide](http://localhost:4000/ati-portfolio/QuickStart/)
* Update the [change log]()
* Update the [performance plot]()in the documentation.

3.Push the release branch with the changes.

4.Merge the newly created branch to the master branch.

5.Draft a new release in [GitHub](GitHub) using this [template]() and also tag name `vX.Y.Z`

6.Create and tag a docker image for release running at the repo's root:

* Create an image:

```
docker build -t bscwdc/ourlibrary:vX.Y.Z .
# Create also new 'latest' tag using newly created image
docker tag bscwdc/ourlibrary.vX.Y.Z bscwdc/ourlibrary:latest
```
* Log in and push it to dockerhub

```
docker login -u DOCKERHUB_USER -p DOCKERHUB_PASSWORD
docker push bscwdc/ourlibrary:vX.Y.Z
docker push bscwdc/ourlibrary:latest
```
<br>
<br>

7.Create a pip package and upload it to PyPi:

* Ensure that you have the latest version of `setuptools, wheel, ` and `twine` installed:
`pip3 install --upgrade setuptools wheel twine`

<br>
* Create and upload the pip package:

```
python3 setup.py sdist bdist_wheel
pyhton3 -m twine upload dist/ourlibrary-X.Y.Z*
```
