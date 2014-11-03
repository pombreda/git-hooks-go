git pre-commit hook for Golang projects
=======================================

`presubmit_impl.py` runs multiple tests on a go project to ensure code health
*before committing*. It also includes tooling to run automated testing on
travis-ci.org and code coverage on coveralls.io.

It is designed to be called on pre-commit so that the committed code is clean.
It:

  * [Build](https://golang.org/pkg/go/build/) all directories with .go files found
  * Run [all test found](https://golang.org/pkg/testing/)
  * Run [errcheck](https://github.com/kisielk/errcheck)
  * Run [gofmt](https://golang.org/cmd/gofmt/) and [goimports](https://godoc.org/code.google.com/p/go.tools/cmd/goimports) (redundant except for gofmt -s)
  * (optionally) Run [govet](https://godoc.org/code.google.com/p/go.tools/cmd/vet)
  * (optionally) Run [golint](https://github.com/golang/lint)


Hook Installation
-----------------

To install the git pre-commit hook which runs `presubmit.py` automatically on
commit, run:

    ./install.py


Pre commit hook setup
---------------------

The normal workflow to setup git-hooks-go for a golang repository is:

    git submodule init
    git submodule add https://github.com/maruel/git-hooks-go
    # On Windows, use copy git-hooks-go\presubmit.py . since symlinks are not
    # supported.
    ln -s git-hooks-go/presubmit.py
    git add presubmit.py
    python git-hooks-go/install.py
    git commit -a -m "Add github.com/maruel/git-hooks-go pre-commit git hook."


Post commit hook setup
----------------------

Post commit CI works with travis-ci.org and coveralls.io. Do:

    cp git-hooks-go/sample.travis.yml .travis.yml
    git add .travis.yml
    git commit -m "Added .travis.yml"


Visit https://travis-ci.org and connect your github account (or whatever git
host provider) to travis. Then do the same via https://coveralls.io.
