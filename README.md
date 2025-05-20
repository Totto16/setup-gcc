# Set up GCC

[![Test](https://github.com/Totto16/setup-gcc/actions/workflows/test.yml/badge.svg)](https://github.com/Totto16/setup-gcc/actions/workflows/test.yml)

Forked from [egor-tensin/setup-gcc/](https://github.com/egor-tensin/setup-gcc/)

This GitHub action sets up GCC in your workflow run.

1. Installs either 32-bit or 64-bit GCC on either Ubuntu or Cygwin.
2. Specify a version to install using the `version` parameter.
3. For installing GCC on Windows please see my action [setup-mingw].

[setup-mingw]: https://github.com/egor-tensin/setup-mingw

Use it in your workflow like this:

    - name: Set up GCC
      uses: Totto16/setup-gcc@v1
      with:
        version: latest
        platform: x64

* `latest` is the default value for the `version` parameter and can be omitted.
* `x64` is the default value for the `platform` parameter and can be omitted.
Use `x86` if you want to build 32-bit binaries.
* Set the `cygwin` parameter to `1` to set up GCC inside an existing Cygwin
installation (you can set up Cygwin itself using my action [setup-cygwin]).
* `cc` and `c++` executables are set up, pointing to the `gcc` and `g++`
executables.
Disable this by setting the `cc` parameter to `0`.

[setup-cygwin]: https://github.com/egor-tensin/setup-cygwin

## API

| Input     | Value  | Default | Description                                               |
| --------- | ------ | ------- | --------------------------------------------------------- |
| version   | latest | ✓       | Install the latest version available in the repository.   |
|           | *any*  |         | Install a specific version if it's available (see below). |
| platform  | x64    | ✓       | Install the x86_64 toolchain.                             |
|           | *any*  |         | Install the i686 toolchain.                               |
| cygwin    | *any*  | ✓       | Install native binaries.                                  |
|           | 1      |         | Install Cygwin packages.                                  |
| cc        | 1      | ✓       | Set up `cc`/`gcc`/`c++`/`g++` executables.                |
|           | *any*  |         | Don't set up the executables.                             |
| hardlinks | *any*  | ✓       | Cygwin: don't convert any symlinks.                       |
|           | 1      |         | Cygwin: convert symlinks in /usr/bin to hardlinks.        |

### Supported versions

Unless the `version` parameter value is `"latest"`, the ubuntu-toolchain-r/test
PPA is used to make more versions available.
You can pass the version number as the `version` parameter value (`8`,
`9`, `14`, etc.), and this action will install the corresponding packages.

The `version` parameter value is not checked for being an available version for
the current distribution.
The supported versions for a particular distribution are those found in that
distro's repositories & those in the PPA.
For example, you can find the list of available versions as of January 2023
below.

We only support The currently supported action images, see [available-images](https://github.com/actions/runner-images?tab=readme-ov-file#available-images)


| `version` | Ubuntu 22.04 | Ubuntu 24.04 |
| --------- | ------------ | ------------ |
| 9         | TODO         |              |
| 10        |              |              |
| 11        |              |              |
| 12        |              |              |
| 13        |              |              |
| 14        |              |              |
| 15        |              |              |

This table should be updated periodically; it's a work-in-progress.

On Cygwin, the `version` parameter is ignored.

## License


Distributed under the MIT License.
See [LICENSE.txt] for details.

[LICENSE.txt]: LICENSE.txt
