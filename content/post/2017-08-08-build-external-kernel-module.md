+++

css = []
date = "2017-08-08T20:35:42+08:00"
description = ""
draft = false
highlight = true
scripts = []
tags = []
title = "Build external kernel module"

+++

First, apply patches if any.
```
git am --whitespace=nowarn ${patches}/*.patch
```

Second, built the module
```
# take amdgpu as an example
cd drivers/gpu/drm/amd/amdgpu/
make -C /lib/modules/`uname -r`/build M=$PWD
```

1. https://www.kernel.org/doc/Documentation/kbuild/modules.txt
