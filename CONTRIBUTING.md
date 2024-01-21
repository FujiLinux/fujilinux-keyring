# Contributing

These are the contribution guidelines for fujilinux-keyring.
All code contributions fall under the terms of the GPL-3.0-or-later (see
[LICENSE](LICENSE)).

Please read our distribution-wide [Code of
Conduct](https://terms.archlinux.org/docs/code-of-conduct/) before
contributing, to understand what actions will and will not be tolerated.

fujilinux-keyring is forked from archlinux-keyring, any bug fixes
or contributions unrelated to enabling this package for use with
Fuji Linux should be submitted upstream on Arch Linux' Gitlab:
https://gitlab.archlinux.org/archlinux/fujilinux-keyring.

Otherwise Fuji Linux specific changes (e.g. adding new keys) happens on
the [Fuji Linux GitHub organization](https://github.com/FujiLinux/fujilinux-keyring).

## Discussion

Discussion around fujilinux-keyring may take place on the [arch-projects
mailing list](https://lists.archlinux.org/listinfo/arch-projects) and in
[#archlinux-projects](ircs://irc.libera.chat/archlinux-projects) on [Libera
Chat](https://libera.chat/).

## Requirements

The following additional packages need to be installed to be able to lint
and develop this project:

* python-black
* python-coverage
* python-isort
* python-pytest
* python-tomli
* flake8
* mypy

## Keyringctl

The `keyringctl` script is written in typed python, which makes use of
[sequoia](https://sequoia-pgp.org/)'s `sq` command.

The script is type checked, linted and formatted using standard tooling.
When providing a merge request make sure to run `make lint`.

## Testing

Test cases are developed per module in the [test](test) directory and should
consist of atomic single expectation tests. A Huge test case asserting various
different expectations are discouraged and should be split into finer grained
test cases.

To execute all tests using pytest
```bash
make test
```

To run keyring integrity and consistency checks
```bash
make check
```

## Web Key Directory

Only tagged releases are built and exposed via WKD. This helps to ensure, that
inconsistent state of the keyring is not exposed to the enduser, which may make
use of it instantaneously.
