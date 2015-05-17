# BETA SOFTWARE

This is barely a beta.  There are currently no versioned releases, only `master`.  I push to master with impunity.  There are no tests.  If anything works at all, consider yourself lucky.

Feature contributions and bugfixes are both very welcome :)

# pwndbg

A PEDA replacement.  In the spirit of our good friend `windbg`, `pwndbg` is pronounced `pwnd-bag`.

- Speed
- Resiliency
- Clean code

Best supported on Ubuntu 14.04 with default `gdb` or `gdb-multiarch` (e.g. with Python3).

## Installation

1. Clone the repo: `git clone https://github.com/zachriggle/pwndbg`
2. Add to `~/.gdbinit`: `echo "source $PWD/pwndbg/gdbinit.py" >> ~/.gdbinit`

### Prerequisites

#### GDB 7.9

As of changes made May 17 you must have GDB 7.9 or newer.  Ubuntu Vivid users already have this.  Otherwise, you'll have to build it from source.  This works for Ubuntu 14.04:

```sh
$ sudo apt-get build-dep gdb
$ wget http://archive.ubuntu.com/ubuntu/pool/main/g/gdb/gdb_7.9.orig.tar.gz
$ tar xf gdb_7.9.orig.tar.gz
$ cd gdb-7.9
$ wget http://archive.ubuntu.com/ubuntu/pool/main/g/gdb/gdb_7.7-0ubuntu3.debian.tar.gz
$ tar xf gdb_7.7-0ubuntu3.debian.tar.gz
$ DEB_BUILD_OPTIONS=nocheck dpkg-buildpackage -j -us -uc -nc
$ sudo dpkg -i gdb-*.deb
```

#### Capstone 4.0

Currently this is only available via a source build.

1. Clone the repo: `git clone https://github.com/aquynh/capstone`
2. Select the `next` branch: `cd capstone && git checkout -t origin/next`
3. Build and install libcapstone: `sudo ./make.sh install`
4. Build and install Python bindings: `cd bindings/python && python setup.py install`

#### pycparser

`pip install pycparser`

## Features

Does most things that PEDA does.  Doesn't do things that PEDA does that [pwntools](https://github.com/Gallopsled/pwntools) or [binjitsu](https://binjit.su) (my fork of pwntools) do better.

Also has a basic windbg compat layer for e.g. `dd`, `eb`, `da`, `dps`.  Now you can even [`eb eip 90`](https://twitter.com/ebeip90)!

For most standard function calls, it knows how many arguments there are and can print out the function call args.

## Screenshots

Here's a few screenshots of some of the cool things pwndbg does.

![d](caps/d.png?raw=1)

![e](caps/e.png?raw=1)

![f](caps/f.png?raw=1)

![g](caps/g.png?raw=1)

Here's a screenshot of `pwndbg` working on an aarch64 binary running under `qemu-user`.

![a](caps/a.png?raw=1)

Here's a screenshot of `PEDA`.  That it's aarch64 doesn't matter -- it chokes in the same way for everything qemu-user.

![c](caps/b.png?raw=1)

And here's a screenshot of GDB's built-in commands failing horribly.  Note that while, yes, it gives output -- the addresses it does give are all wrong, and are just file offsets.

![c](caps/c.png?raw=1)
