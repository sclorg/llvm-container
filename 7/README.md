LLVM Docker image
===================

This repository contains the source for building various versions of
the LLVM application as a reproducible Docker image.
Users can choose between RHEL and CentOS based builder images.
The resulting image can be run using [Docker](http://docker.io).


Usage
---------------------
To use the llvm-toolset s2i image build with your project, you will need to
define write your own assemble and run scripts and place them in the
.s2i/bin directory in the root of your source tree.

Example assemble and run scripts can be found in:
7/test/hello-world/app/.s2i/bin
