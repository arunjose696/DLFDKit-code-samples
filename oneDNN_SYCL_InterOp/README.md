# oneDNN SYCL Interop sample
 This oneDNN SYCL Interop sample code is implemented using C++ and DPC++ language for CPU and GPU. 

| Optimized for                       | Description
|:---                               |:---
| OS                                | Linux Ubuntu 18.04; 
| Hardware                          | Kaby Lake with GEN9 or newer
| Software                          | Intel oneAPI Deep Neural Network Library (oneDNN), Intel oneAPI DPC++ Compiler, Intel oneAPI DPC++ Library (oneDPL), Intel oneAPI Threading Building Blocks (oneTBB)
| What you will learn               | oneDNN SYCL extensions API programming for both Intel CPU and GPU
| Time to complete                  | 15 minutes


## What you will learn
* How to create a GPU or CPU engine. It uses SYCL as the runtime in this sample.
* How to create a memory descriptor/object.
* How to create a SYCL kernel for data initialization.
* How to access a SYCL buffer via SYCL interoperability interface.
* How to access a SYCL queue via SYCL interoperability interface.
* How to execute a SYCL kernel with related SYCL queue and SYCL buffer
* How to create operation descriptor/operation primitives descriptor/primitive.
* How to execute the primitive with the initialized memory.
* How to validate the result through a host accessor.

## Pre-requirement

The sample below require the following components, which are part of the [Intel oneAPI Base Toolkit (Base Kit)](https://software.intel.com/en-us/oneapi/oneapi-kit)
*  Intel oneAPI Deep Neural Network Library (oneDNN)
*  Intel oneAPI DPC++ Compiler
*  Intel oneAPI DPC++ Library (oneDPL)
*  Intel oneAPI Threading Building Blocks (oneTBB)

The sample also requires OpenCL driver. Please refer [System Requirements](https://software.intel.com/en-us/articles/intel-oneapi-base-toolkit-system-requirements) for OpenCL driver installation.


You can refer to this page [oneAPI](https://software.intel.com/en-us/oneapi) for toolkit installation.


## How to Build  


### Using DPC++ Compiler  

------

By using DPC++ compiler, this sample supports a SYCL custom kernel both on Intel CPU and GPU.

#### on Linux  

- Build SYCL Interops program with DPC++  \
  please replace ${ONEAPI_ROOT} for your installation path. \
  ex : /opt/intel/inteloneapi 
   
  First, please use a clean console environment without exporting any none default environment variables.
```
    source ${INTEL_ONEAPI_INSTALL_FOLDER}/setvars.sh --dnnl-configuration=cpu_dpcpp_gpu_dpcpp
```
or 

```
    source ${INTEL_ONEAPI_INSTALL_FOLDER}/setvars.sh 
```
  dnnl-configuration is set cpu_dpcpp_gpu_dpcpp to by default if users don't input --dnnl-configuraition argument.
  
  Make sure that both the enviroments of compiler and dnnl are properly set up before you process following steps.
  If setvars.sh complains "not found" for compiler or dnnl, please check your installation first.
  
```    
    cd DLDevKit-code-samples/oneDNN_SYCL_InterOp
    mkdir dpcpp
    cd dpcpp
    cmake .. -DCMAKE_C_COMPILER=clang -DCMAKE_CXX_COMPILER=dpcpp 
    make sycl-interop-cpp
```
## How to Run 

### on Linux  
- Run the program  on CPU
  ```
  ./out/sycl-interop-cpp cpu  
  ```
- Run the program  on GPU

  ```
  ./out/sycl-interop-cpp gpu  
  ```


## Result Validation 

### on Linux  

- Enable oneDNN Verbose log

  ```
  export DNNL_VERBOSE=1
  ```
- Run the program on CPU or GPU following [How to Run Session](#how-to-run)
- CPU Results

  ```
  dnnl_verbose,info,DNNL v1.90.1 (commit 9151ddc657e4c6775f17f3bcec46872e5fac47ee)
  dnnl_verbose,info,Detected ISA is Intel AVX2
  dnnl_verbose,exec,cpu,eltwise,jit:avx2,forward_training,data_f32::blocked:abcd:f0 diff_undef::undef::f0,,alg:eltwise_relu alpha:0 beta:0,2x3x4x5,700.608
  Example passes
  ```

- GPU Results

  ```
  dnnl_verbose,info,DNNL v1.90.1 (commit 9151ddc657e4c6775f17f3bcec46872e5fac47ee)
  dnnl_verbose,info,Detected ISA is Intel AVX2
  dnnl_verbose,exec,gpu,eltwise,ocl:ref:any,forward_training,data_f32::blocked:abcd:f0 diff_undef::undef::f0,,alg:eltwise_relu alpha:0 beta:0,2x3x4x5
  Example passes
  ```

