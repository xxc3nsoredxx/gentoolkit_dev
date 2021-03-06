Contributing
============
Gentoo Developers have full priviledges to the gentoolkit repository and
any Gentoo developer can do work on the gentoolkit source. We only ask that you
keep the following in mind:

- If you want to do a major change (i.e rewrite/refactor something), please talk
  to us before pushing any commits. If you break something, please fix it.
- All members of the Portage or Portage Tools projects are authorized to create
  a new release of gentoolkit or gentoolkit-dev.
- All other Gentoo Developers are authorized to create a new release if it is
  coordinated with fuzzyray and/or dolsen.
- If you create a release and it breaks, please fix it.

Any non Gentoo developers who wish to contribute, the best way to get
started is by cloning a copy of the repository and submitting patches to
bugzilla.  Additionally, we can be found in the #gentoo-portage IRC
channel.

Formatting
==========
We use [black](https://pypi.org/project/black/) to format the code
base. Please make sure you run it against any PRs prior to submitting
(otherwise we'll probably reject it).

There are [ways to integrate](https://black.readthedocs.io/en/stable/integrations/editors.html)
black into your text editor and/or IDE.

You can also set up a git hook to check your commits, in case you don't want
editor integration. Something like this:

```sh
# .git/hooks/pre-commit (don't forget to chmod +x)

#!/bin/bash
black --check --diff .
```

To ignore reformatting commits (which are listed in `.gitignorerevs`) you can do
the following:

```sh
git config blame.ignoreRevsFile .gitignorerevs
```

Adding or modifying code
========================
- If you add new code, best practice is to write a test for it.
- If you're modifying code that doesn't have a test and you can write a test
  for it, please do.
- Before committing your changes, run "tox" to ensure that you didn't break
  tests or introduced a flake8 error.
- If flake8 raises a warning or error that you don't agree with, it's probably
  better to just change your code. If you're sure you have a good reason for
  doing what you're doing, you can add "# noqa" at the end of the line to
  silence it.

Creating a release
==================
Note: We are using VERSION="0.3.0" simply as an example.

```sh
# Run Gentoolkit's test suite, make sure it passes:
# Note: requires dev-python/snakeoil
./setup.py test

# Create a source distribution (you need to add VERSION here):
VERSION="0.3.0" ./setup.py sdist
# Transfer dist/gentoolkit-0.3.0.tar.gz to dev.gentoo.org:/space/distfiles-local
# scp dist/gentoolkit-0.3.0.tar.gz username@dev.gentoo.org:/space/distfiles-local

# Clean up temporary files:
./setup.py clean -a
git status
# rm or mv any untracked files/directories

# Create a tag for the release
git tag gentoolkit-0.3.0
git push origin gentoolkit-0.3.0
```
