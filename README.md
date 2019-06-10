Introduction
============

This is a simple Python script designed to *build and install ROCm OpenCl ICD* in a Fedora 30 distribution.
It is based on the original AMD installation script work, as can be found in 
https://github.com/RadeonOpenCompute/Experimental_ROC

Currently it is *nasty* and just _works for me_. Characteristics are as follow:
 
 *  My main goals where:
     +  To be able to make Darktable work on my Radeon RX 570 (OpenCL accel)
     +  To understand the ROCm build process 
 *  Installs artifacts to `/opt/rocm`.
 *  Output folder (`/opt/rocm`) is assumed to be owned by the non-root user executing this script.
 
Does not:
 
 *  Try to build RPM packages.
 *  Does not build the FULL ROCm. Only that needed for OpenCL runtime.
 *  I haven't bothered yet to check OpenCL dev headers / tools operation.
     +  ATM, the built ICD OpenCL works, I can run `clinfo` on top of it, and was able to discovered that a key 
        Darktable capability (`CL_DEVICE_IMAGE_SUPPORT`) is missing.

ROCm installation
=================

Multiple "components" form AMD's ROCm. Just a few of them are needed to build ROCm OpenCL support. From the 
OpenCL-Runtime component repo `README.md` these seem to be:

 *  From RadeonOpenCompute repo:
     +  ROCm-OpenCL-Runtime
     +  ROCm-Device-Libs 
     +  ROCm-OpenCL-Driver 
     +  llvm 
     +  clang
     +  lld 
 *  From the KhronosGroup repo: 
     +  OpenCL-ICD-Loader

The ROCm OpenCL runtime component is a relatively complex beast. The ROCm-OpenCL-Runtime repo is just a meta-repo 
referencing various other repositories (including LLVM). The references are stored in an `opencl.xml` file in the 
OpenCL-Runtime repo. This file is understood by the Google `repo` tool, which the scripts uses.
