# 🔍 arm-float-detector

Utility to detect soft float/double math library inclusion in arm binaries
(objects/archives/elfs).

```bash
# install
$ pip install arm-float-detector

# run
$ arm-float-detector --double a.out && echo OK
No soft double libs found!
OK
```

## Requirements

Besides python, needs the `nm` utility. If you're on *nix, you probably have it.

## What is this

Some processors do not have single- and/or double-precision floating point
hardware, but instead rely on float math software libraries, which are
relatively slow and add take up additional space in the application.

Unfortunately I can't find options for gcc/ld to detect and prohibit (eg
warnings/errors/configuration options) using these functions; I believe the
definitions are in the compiler somehow (TODO actually research this).

This utility enables detecting usage of this soft floating point libraries in
binaries, suitable for being integrated into a CI check to prevent them.

## Features

1. detect presence of single- or double-precision soft floating point libraries
2. _TODO_ whitelist objects allowed to reference these libs (eg vsprintf)
3. _TODO_ enable printing objects containing the references for simpler
   elimination

**NOTE** only tested on linux, where grep supports `-E 'string|string'`. You use
a mac, good for you, no idea if this will work there. Dependency on grep will
probably be removed in the future.
