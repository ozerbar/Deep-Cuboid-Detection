**fatal error: THC/THC.h: No such file or directory**
THC/THC.h was removed after pytorch version 1.11. Migration guide for newer (I have 2.3.1) pytorch versions:

1. remove #include <THC/THC.h>
2. replace
   
THCudaCheck(...);

   with
   
AT_CUDA_CHECK(...);

**THCCeilDiv is undefined**
1. #include <ATen/ceil_div.h>
2. replace
   
THCCeilDiv(...)

   with
   
at::ceil_div(...)

**THCudaMalloc/THCudaFree/THCState  is undefined**
1. #include <ATen/cuda/ThrustAllocator.h>
2. remove the line with THCState
3. replace
   
THCudaMalloc(param1, param2)

   with
   
c10::cuda::CUDACachingAllocator::raw_alloc(param2)

4. replace
   
THCudaFree(param1, param2)

   with
   
c10::cuda::CUDACachingAllocator::raw_delete(param2)
