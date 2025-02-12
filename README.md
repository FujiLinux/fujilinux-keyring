# fujilinux-keyring

Forked from [archlinux-keyring](https://gitlab.archlinux.org/archlinux/archlinux-keyring) to verify Fuji Linux packaging.

The fujilinux-keyring project holds PGP packet material and tooling
(`keyringctl`) to create the distribution keyring for Fuji Linux.
The keyring is used by pacman to establish the web of trust for the packagers
of the distribution.

The PGP packets describing the main signing keys can be found below the
[keyring/main](keyring/main) directory, while those of the packagers are located below the
[keyring/packager](keyring/packager) directory.

## Requirements

The following packages need to be installed to be able to create a PGP keyring
from the provided data structure and to install it:

Build:

* make
* findutils
* pkgconf
* systemd

Runtime:

* python
* sequoia-sq >= 0.31.0

Optional:

* hopenpgp-tools (verify)
* git (ci)

## Usage

### Build

Build all PGP artifacts (keyring, ownertrust, revoked files) to the build directory
```bash
./keyringctl build
```

### Import

Import a new packager key by deriving the username from the filename.
```bash
./keyringctl import <username>.asc
```

Alternatively import a file or directory and override the username
```bash
./keyringctl import --name <username> <file_or_directory...>
```

Updates to existing keys will automatically derive the username from the known fingerprint.
```bash
./keyringctl import <file_or_directory...>
```

Main key imports support the same options plus a mandatory `--main`
```bash
./keyringctl import --main <username>.asc
```

### Export

Export the whole keyring including main and packager to stdout
```bash
./keyringctl export
```

Limit to specific certs using an output file
```bash
./keyringctl export <username_or_fingerprint_or_directory...> --output <filename>
```

### List

List all certificates in the keyring
```bash
./keyringctl list
```

Only show a specific main key
```bash
./keyringctl list --main <username_or_fingerprint...>
```

### Inspect

Inspect all certificates in the keyring
```bash
./keyringctl inspect
```

Only inspect a specific main key
```bash
./keyringctl inspect --main <username_or_fingerprint_or_directory...>
```

### Verify

Verify certificates against modern expectations and assumptions
```bash
./keyringctl verify <username_or_fingerprint_or_directory...>
```

## Installation

To install fujilinux-keyring system-wide use the included `Makefile`:

```bash
make install
```

## Contribute

Read our [contributing guide](CONTRIBUTING.md) to learn more about guidelines and
how to provide fixes or improvements for the code base.

## Releases

[Releases of
fujilinux-keyring](https://github.com/FujiLinux/fujilinux-keyring/tags)
are exclusively created by maintainers.

The tags are signed with one of the following legitimate keys:

```
Evan Welsh <ewlsh@fujilinux.org>
<key>
```

To verify a tag, first import the relevant PGP keys:

```bash
gpg --auto-key-locate wkd --search-keys <email-from-above>
```

Afterwards a tag can be verified from a clone of this repository. Please note
that one **must** check the used key of the signature against the legitimate
keys listed above:

```bash
git verify-tag <tag>
```

## License

fujilinux-keyring is licensed under the terms of the **GPL-3.0-or-later** (see
[LICENSE](LICENSE)).
