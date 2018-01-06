# lektory

This is a skeleton Lektor website to be used as the scaffolding for building and deploying more complex sites. It is based on [Lektor 3.0.1](https://www.getlektor.com/) (the latest version at the time of writing) and Python 2.7 (for reasons explained below), served on [Github Pages](https://pages.github.com/), and automatically deployed via [Travis-CI](https://travis-ci.org/).

The use of Python 2.7 goes against current trends and indeed against the recommendation of the Lektor documentation itself. But Python 3.5 fails to deploy when using Travis, and it only succeeded after reverting to Python 2.7.

In particular, the following changes were needed to the settings suggested in the documentation.

### Contents of `.travis.yml`

```
language: python
python: 2.7
install: "pip install Lektor"
script: "lektor build"
deploy:
  provider: script
  script: "lektor deploy ghpages-https"
cache:
  directories:
    - $HOME/.cache/pip
    - $HOME/.cache/lektor/builds
```

### Contents of `Lektory.lektorproject`

```
[project]
name = Lektory

[servers.ghpages-https]
target = ghpages+https://gauden/lektory
```

The discussion on [this bug](https://github.com/lektor/lektor/issues/418) on the Lektor development repo and [this answer](https://stackoverflow.com/a/38216821/1290420) on StackOverflow helped in my solution. Neither of them worked without the configuration changes above.
