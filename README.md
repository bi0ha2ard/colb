# colb

A [colcon](https://colcon.readthedocs.io/en/released/) wrapper that makes building and testing single packages more convenient during development.

## Overview

While working on package, one typically performs the following steps:

1. Build all the dependent packages
2. Make some changes
3. Rebuild the package
4. Run the tests

This usually requires multiple colcon invocations.
With this tool, it is enough to run:


```console
colb test -r my_package
```

## Examples

To get an overview over the available options:

```console
colb help
colb help <verb>
```

Rebuilding just the current package:

```console
colb build -s my_package
```

Building and running only a single unit test (only works after the package has been built once):

```console
colb test my_package --test my_unit_test
```

To minimize the steps involved in getting a test output, this will directly invoke `ninja` and `ctest`.

If the current directory is already somewhere inside a package, the package name may be omitted from the command line:

```console
cd my_ws/src/my_repo/my_package/src
colb build
```

Building multiple packages at once:

```console
colb build my_package my_other_package my_third_package
```

## Requirements

The invoked commands make use of the `colcon-common-extensions` and [colcon mixins](https://github.com/colcon/colcon-mixin-repository) by default, so they should be installed.
By default, the `ccache`, `ninja` and `mold` mixins are enabled, so the associated programs should be installed.

## Installation

```console
cargo install --path .
```

## Configuration

It is possible to customize the options used for the dependency build and for the active package.
The default settings can be written to a `.colb.toml` file using the `colb init` command.
Further invocations will then load the options from this file, which also doubles as a workspace root marker.
