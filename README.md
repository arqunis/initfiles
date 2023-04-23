# Init files

This repository provides a set of files for setting up the initial layout of a
project for a given language and their build system(s).

## Layouts

Layouts are written such that after cloning this repository (or downloading a
source distribution), you only need to `cp -R <layout>/* -t <your-folder>`, or
in other words, copy all of the files to your project directory.

Note: Some files are opinionated (such as format configuration files) as these
layouts are primarily written for my own projects. If you do not like how
certain things were configured, you are free to change them after copying the
files.

Currently supported layouts:

- [C and C++](c_cpp/README.md):
   1. Binary and library example using the CMake meta build system.
   2. Binary and library example using the Meson meta build system.

Other layouts may be added in the future.

## License

All of the files in this repository are in the Public Domain.

For countries that do not recognize surrendering copyright, or for lawyers who
want a proper legal document to quote, then this repository is licensed under
the [0BSD license](LICENSE). Its text should be provided alongside this
repository (or source distribution). If it is not, you may find a copy at
https://opensource.org/license/0bsd/
