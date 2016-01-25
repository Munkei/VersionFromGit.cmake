# VersionFromGit.cmake #

> **DEPRECATED!**
>
> VersionFromGit is now part of
> [`munkei-cmake`](https://github.com/Munkei/munkei-cmake). This repository will
> *not* be updated.

---

Get a [CMake](http://www.cmake.org/) project's version number from the latest
[Git](http://git-scm.com) tag.

This module uses Git to set the version number of a project (using [`git
describe --tags`](http://git-scm.com/docs/git-describe)).  It is meant to be
used in projects that are in a Git repository and have tags for each version.
The version format must follow [Semantic Versioning](http://semver.org).

Builds in between tags get some added metadata;  the current Git hash and
optionally a timestamp.

## Usage ##

There's just the one function; `version_from_git()`.

### `version_from_git()` ###

```cmake
version_from_git(
  [GIT_EXECUTABLE command]
  [INCLUDE_HASH bool]
  [LOG bool]
  [TIMESTAMP format]
)
```

Gets the version information from Git.

#### Options ####

*   `GIT_EXECUTABLE` *(optional)*

    The name of, or full path to, Git. If not defined it will be found using
    `find_package( Git )`.

*   `INCLUDE_HASH` *(optional)*

    Whether to include the current Git hash as part of the metadata, *if* the
    current HEAD is *not* at a tag, à la `git describe`.

    Default: `ON`

*   `LOG` *(optional)*

    Whether to log the different parts obtained from Git.

    Default: `OFF`

*   `TIMESTAMP` *(optional)*

    A timestamp format (see CMake’s `string( TIMESTAMP ... )`), that, if
    defined, will be added as a part of the metadata.

#### Variables Set ####

*   `GIT_TAG`

    The current (latest) Git tag.

*   `SEMVER`

    The full semantic version, including identifiers and metadata.

*   `VERSION`

    The full three-part version, suitable for use with `project()`.

*   `VERSION_MAJOR`

    The major version number.

*   `VERSION_MINOR`

    The minor version number.

*   `VERSION_PATCH`

    The patch version number.

### Example ###

```cmake
# Make sure CMake can find the file
list( APPEND CMAKE_MODULE_PATH /where/you/put/it/ )

# Load it
include( VersionFromGit )

# Use it
version_from_git(
  LOG       ON
  TIMESTAMP "%Y%m%d%H%M%S"
)

# Use `VERSION` for your project
project( MyProject
  VERSION ${VERSION}
)

# Use the full semantic version for things like package name, etc.
set( CPACK_PACKAGE_FILE_NAME MyProject-v${SEMVER} )
```

## Requirements ##

*   CMake v3.0.0 or later
*   Git

## License ##

The MIT License (MIT)

Copyright (c) 2015 Theo Willows

Permission is hereby granted, free of charge, to any person obtaining a copy of
this software and associated documentation files (the "Software"), to deal in
the Software without restriction, including without limitation the rights to
use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of
the Software, and to permit persons to whom the Software is furnished to do so,
subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS
FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR
COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER
IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
