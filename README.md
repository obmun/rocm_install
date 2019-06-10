Multiple "components" are needed to build ROCm OpenCL support. From the OpenCL-Runtime component repo README.md:

From RadeonOpenCompute repo:
 *  ROCm-OpenCL-Runtime
 *  ROCm-Device-Libs 
 *  ROCm-OpenCL-Driver 
 *  llvm 
 *  clang
 *  lld 
 From the KhronosGroup repo: 
 *  OpenCL-ICD-Loader
 
The references to the repos are stored in an `opencl.xml` file in the OpenCL-Runtime repo. This file is understood by the Google `repo` tool.
