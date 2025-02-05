Monicoin: This software is for entertainment purposes only
===========================================================

This is not a real cryptocurrency.

Files in the Repo
=================

1. aclocal.m4: Some sort of automatically generated file. Some answer [here](https://stackoverflow.com/questions/1970926/whats-the-point-of-aclocal#1971156a)
2. .appveyor.yml: Some sort of continuous integration file, looks to be for windows environments. The tool is made by [this](https://www.appveyor.com/docs/) company
3. autogen.sh: Script used to generate the configure script. It's unclear when it is necessary to call this script or if it's even necessary.
4. autom4te.cache: (directory) - Temporary directory used by the GNU Autotools build system when generating the 'configure' script.
5. build-aux: (directory) - Contains auxiliary files and scripts used during the build process. 
6. build-msvc: (directory) - Contains files/tools for building with MS Visual Studio
7. ci: (directory) - Contains scripts for each build stage. 
8. .cirrus.yml: Used by Cirrus CI to automatically build and test the project every time code is pushed to the repository
9. CODEOWNERS: File to denote who should review changes to various parts of the source code.
10. config.log: Used for debugging errors during the build process


Autotools Stuff
===============

So the steps generally go like this:

1. Write configure.ac and Makefile.am and check them in. 
2. Run autoconf to generate configure from configure.ac. 
3. Run automake to generate Makefile.in from Makefile.am. 
4. Run configure to generate Makefile from Makefile.in. 
5. Run make to build the product.

Minimal Configure
=================

1. This seems to help save disk space when we compile: ./configure --with-gui=no --disable-maintainer-mode --disable-tests

Minimal Execute
===============

1. To see what litecoind is doing without downloading the entire blockchain: ./litecoind -testnet


Tracing the Code
================

1. bitcoind.cpp: Around like 169 or so, AppInitMain() is called; declaration defined init.h
2. init.cpp -> AppInitMain() -> LogInstance().StartLogging() -> Logging.h (next is to understand the class def)
3. logging.h: Logger class defined here
4. logging.cpp: line 45 appears to be the next spot to trace from; line 70 appears to be the string def, 's'


Litecoin Core integration/staging tree
=====================================

[![Build Status](https://travis-ci.org/litecoin-project/litecoin.svg?branch=master)](https://travis-ci.org/litecoin-project/litecoin)

https://litecoin.org

What is Litecoin?
----------------

Litecoin is an experimental digital currency that enables instant payments to
anyone, anywhere in the world. Litecoin uses peer-to-peer technology to operate
with no central authority: managing transactions and issuing money are carried
out collectively by the network. Litecoin Core is the name of open source
software which enables the use of this currency.

For more information, as well as an immediately useable, binary version of
the Litecoin Core software, see [https://litecoin.org](https://litecoin.org).

License
-------

Litecoin Core is released under the terms of the MIT license. See [COPYING](COPYING) for more
information or see https://opensource.org/licenses/MIT.

Development Process
-------------------

The `master` branch is regularly built (see `doc/build-*.md` for instructions) and tested, but it is not guaranteed to be
completely stable. [Tags](https://github.com/litecoin-project/litecoin/tags) are created
regularly from release branches to indicate new official, stable release versions of Litecoin Core.

The https://github.com/litecoin-project/gui repository is used exclusively for the
development of the GUI. Its master branch is identical in all monotree
repositories. Release branches and tags do not exist, so please do not fork
that repository unless it is for development reasons.

The contribution workflow is described in [CONTRIBUTING.md](CONTRIBUTING.md)
and useful hints for developers can be found in [doc/developer-notes.md](doc/developer-notes.md).

The developer [mailing list](https://groups.google.com/forum/#!forum/litecoin-dev)
should be used to discuss complicated or controversial changes before working
on a patch set.

Developer IRC can be found on Freenode at #litecoin-dev.

Testing
-------

Testing and code review is the bottleneck for development; we get more pull
requests than we can review and test on short notice. Please be patient and help out by testing
other people's pull requests, and remember this is a security-critical project where any mistake might cost people
lots of money.

### Automated Testing

Developers are strongly encouraged to write [unit tests](src/test/README.md) for new code, and to
submit new unit tests for old code. Unit tests can be compiled and run
(assuming they weren't disabled in configure) with: `make check`. Further details on running
and extending unit tests can be found in [/src/test/README.md](/src/test/README.md).

There are also [regression and integration tests](/test), written
in Python, that are run automatically on the build server.
These tests can be run (if the [test dependencies](/test) are installed) with: `test/functional/test_runner.py`

The Travis CI system makes sure that every pull request is built for Windows, Linux, and macOS, and that unit/sanity tests are run automatically.

### Manual Quality Assurance (QA) Testing

Changes should be tested by somebody other than the developer who wrote the
code. This is especially important for large or high-risk changes. It is useful
to add a test plan to the pull request description if testing the changes is
not straightforward.

Translations
------------

We only accept translation fixes that are submitted through [Bitcoin Core's Transifex page](https://www.transifex.com/projects/p/bitcoin/).
Translations are converted to Litecoin periodically.

Translations are periodically pulled from Transifex and merged into the git repository. See the
[translation process](doc/translation_process.md) for details on how this works.

**Important**: We do not accept translation changes as GitHub pull requests because the next
pull from Transifex would automatically overwrite them again.
