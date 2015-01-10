# CUDA Runtime 6.5

## CUDA error types  

| cudaError | value | Description |
|:---|---:|---|
| cudaSuccess | 0 |  The API call returned with no errors. In the case of query calls, this can also mean that the operation being queried is complete (see cudaEventQuery() and cudaStreamQuery()).|
| cudaErrorMissingConfiguration | 1 | The device function being invoked (usually via cudaLaunch()) was not previously configured via the cudaConfigureCall() function. |
| cudaErrorMemoryAllocation | 2 |	The API call failed because it was unable to allocate enough memory to perform the requested operation. |
| cudaErrorInitializationError | 3 | The API call failed because the CUDA driver and runtime could not be initialized. |
| cudaErrorLaunchFailure | 4 | An exception occurred on the device while executing a kernel. Common causes include dereferencing an invalid device pointer and accessing out of bounds shared memory. The device cannot be used until cudaThreadExit() is called. All existing device memory allocations are invalid and must be reconstructed if the program is to continue using CUDA. |
| cudaErrorPriorLaunchFailure | 5 | This indicated that a previous kernel launch failed. This was previously used for device emulation of kernel launches. Deprecated This error return is deprecated as of CUDA 3.1. Device emulation mode was removed with the CUDA 3.1 release. |
| cudaErrorLaunchTimeout | 6 | This indicates that the device kernel took too long to execute. This can only occur if timeouts are enabled - see the device property kernelExecTimeoutEnabled for more information. The device cannot be used until cudaThreadExit() is called. All existing device memory allocations are invalid and must be reconstructed if the program is to continue using CUDA. |
| cudaErrorLaunchOutOfResources | 7 | This indicates that a launch did not occur because it did not have appropriate resources. Although this error is similar to cudaErrorInvalidConfiguration, this error usually indicates that the user has attempted to pass too many arguments to the device kernel, or the kernel launch specifies too many threads for the kernel's register count. |
| cudaErrorInvalidDeviceFunction | 8 | The requested device function does not exist or is not compiled for the proper device architecture. |
| cudaErrorInvalidConfiguration | 9 | This indicates that a kernel launch is requesting resources that can never be satisfied by the current device. Requesting more shared memory per block than the device supports will trigger this error, as will requesting too many threads or blocks. See cudaDeviceProp for more device limitations. |
| cudaErrorInvalidDevice | 10 | This indicates that the device ordinal supplied by the user does not correspond to a valid CUDA device. |
| cudaErrorInvalidValue | 11 | This indicates that one or more of the parameters passed to the API call is not within an acceptable range of values. |
| cudaErrorInvalidPitchValue | 12 | This indicates that one or more of the pitch-related parameters passed to the API call is not within the acceptable range for pitch. |
| cudaErrorInvalidSymbol | 13 | This indicates that the symbol name/identifier passed to the API call is not a valid name or identifier. |
| cudaErrorMapBufferObjectFailed | 14 | This indicates that the buffer object could not be mapped. |
| cudaErrorUnmapBufferObjectFailed | 15 | This indicates that the buffer object could not be unmapped.|
| cudaErrorInvalidHostPointer | 16 | This indicates that at least one host pointer passed to the API call is not a valid host pointer. |
| cudaErrorInvalidDevicePointer | 17 | This indicates that at least one device pointer passed to the API call is not a valid device pointer. |
| cudaErrorInvalidTexture | 18 | This indicates that the texture passed to the API call is not a valid texture. |
| cudaErrorInvalidTextureBinding | 19 | This indicates that the texture binding is not valid. This occurs if you call cudaGetTextureAlignmentOffset() with an unbound texture. |
| cudaErrorInvalidChannelDescriptor | 20 | This indicates that the channel descriptor passed to the API call is not valid. This occurs if the format is not one of the formats specified by cudaChannelFormatKind, or if one of the dimensions is invalid. |
| cudaErrorInvalidMemcpyDirection | 21 | This indicates that the direction of the memcpy passed to the API call is not one of the types specified by cudaMemcpyKind. |
| cudaErrorAddressOfConstant | 22 | This indicated that the user has taken the address of a constant variable, which was forbidden up until the CUDA 3.1 release. Deprecated This error return is deprecated as of CUDA 3.1. Variables in constant memory may now have their address taken by the runtime via cudaGetSymbolAddress(). |
| cudaErrorTextureFetchFailed | 23 | This indicated that a texture fetch was not able to be performed. This was previously used for device emulation of texture operations. Deprecated This error return is deprecated as of CUDA 3.1. Device emulation mode was removed with the CUDA 3.1 release. |
| cudaErrorTextureNotBound | 24 | This indicated that a texture was not bound for access. This was previously used for device emulation of texture operations. Deprecated This error return is deprecated as of CUDA 3.1. Device emulation mode was removed with the CUDA 3.1 release. |
| cudaErrorSynchronizationError | 25 | This indicated that a synchronization operation had failed. This was previously used for some device emulation functions. Deprecated This error return is deprecated as of CUDA 3.1. Device emulation mode was removed with the CUDA 3.1 release. |
| cudaErrorInvalidFilterSetting | 26 | This indicates that a non-float texture was being accessed with linear filtering. This is not supported by CUDA. |
| cudaErrorInvalidNormSetting | 27 | This indicates that an attempt was made to read a non-float texture as a normalized float. This is not supported by CUDA. |
| cudaErrorMixedDeviceExecution | 28 | Mixing of device and device emulation code was not allowed. Deprecated This error return is deprecated as of CUDA 3.1. Device emulation mode was removed with the CUDA 3.1 release. |
| cudaErrorCudartUnloading | 29 | This indicates that a CUDA Runtime API call cannot be executed because it is being called during process shut down, at a point in time after CUDA driver has been unloaded. |
| cudaErrorUnknown | 30 | This indicates that an unknown internal error has occurred. |
| cudaErrorNotYetImplemented | 31 | This indicates that the API call is not yet implemented. Production releases of CUDA will never return this error. Deprecated This error return is deprecated as of CUDA 4.1. |
| cudaErrorMemoryValueTooLarge | 32 | This indicated that an emulated device pointer exceeded the 32-bit address range. Deprecated This error return is deprecated as of CUDA 3.1. Device emulation mode was removed with the CUDA 3.1 release. |
| cudaErrorInvalidResourceHandle | 33 | This indicates that a resource handle passed to the API call was not valid. Resource handles are opaque types like cudaStream_t and cudaEvent_t. |
| cudaErrorNotReady | 34 | This indicates that asynchronous operations issued previously have not completed yet. This result is not actually an error, but must be indicated differently than cudaSuccess (which indicates completion). Calls that may return this value include cudaEventQuery() and cudaStreamQuery(). |
| cudaErrorInsufficientDriver | 35 | This indicates that the installed NVIDIA CUDA driver is older than the CUDA runtime library. This is not a supported configuration. Users should install an updated NVIDIA display driver to allow the application to run. |
| cudaErrorSetOnActiveProcess | 36 | This indicates that the user has called cudaSetValidDevices(), cudaSetDeviceFlags(), cudaD3D9SetDirect3DDevice(), cudaD3D10SetDirect3DDevice, cudaD3D11SetDirect3DDevice(), or cudaVDPAUSetVDPAUDevice() after initializing the CUDA runtime by calling non-device management operations (allocating memory and launching kernels are examples of non-device management operations). This error can also be returned if using runtime/driver interoperability and there is an existing CUcontext active on the host thread. |
| cudaErrorInvalidSurface | 37 | This indicates that the surface passed to the API call is not a valid surface. |
| cudaErrorNoDevice | 38 | This indicates that no CUDA-capable devices were detected by the installed CUDA driver. |
| cudaErrorECCUncorrectable | 39 | This indicates that an uncorrectable ECC error was detected during execution. |
| cudaErrorSharedObjectSymbolNotFound | 40 | This indicates that a link to a shared object failed to resolve. |
| cudaErrorSharedObjectInitFailed | 41 | This indicates that initialization of a shared object failed. |
| cudaErrorUnsupportedLimit | 42 | This indicates that the cudaLimit passed to the API call is not supported by the active device. |
| cudaErrorDuplicateVariableName | 43 | This indicates that multiple global or constant variables (across separate CUDA source files in the application) share the same string name. |
| cudaErrorDuplicateTextureName | 44 | This indicates that multiple textures (across separate CUDA source files in the application) share the same string name. |
| cudaErrorDuplicateSurfaceName | 45 | This indicates that multiple surfaces (across separate CUDA source files in the application) share the same string name. |
| cudaErrorDevicesUnavailable | 46 | This indicates that all CUDA devices are busy or unavailable at the current time. Devices are often busy/unavailable due to use of cudaComputeModeExclusive, cudaComputeModeProhibited or when long running CUDA kernels have filled up the GPU and are blocking new work from starting. They can also be unavailable due to memory constraints on a device that already has active CUDA work being performed. |
| cudaErrorInvalidKernelImage | 47 | This indicates that the device kernel image is invalid. |
| cudaErrorNoKernelImageForDevice | 48 | This indicates that there is no kernel image available that is suitable for the device. This can occur when a user specifies code generation options for a particular CUDA source file that do not include the corresponding device configuration. |
| cudaErrorIncompatibleDriverContext | 49 | This indicates that the current context is not compatible with this the CUDA Runtime. This can only occur if you are using CUDA Runtime/Driver interoperability and have created an existing Driver context using the driver API. The Driver context may be incompatible either because the Driver context was created using an older version of the API, because the Runtime API call expects a primary driver context and the Driver context is not primary, or because the Driver context has been destroyed. Please see Interactions with the CUDA Driver API" for more information. |
| cudaErrorPeerAccessAlreadyEnabled | 50 | This error indicates that a call to cudaDeviceEnablePeerAccess() is trying to re-enable peer addressing on from a context which has already had peer addressing enabled. |
| cudaErrorPeerAccessNotEnabled | 51 | This error indicates that cudaDeviceDisablePeerAccess() is trying to disable peer addressing which has not been enabled yet via cudaDeviceEnablePeerAccess(). |
| cudaErrorDeviceAlreadyInUse | 54 | This indicates that a call tried to access an exclusive-thread device that is already in use by a different thread. |
| cudaErrorProfilerDisabled | 55 | This indicates profiler is not initialized for this run. This can happen when the application is running with external profiling tools like visual profiler. |
| cudaErrorProfilerNotInitialized | 56 | Deprecated This error return is deprecated as of CUDA 5.0. It is no longer an error to attempt to enable/disable the profiling via cudaProfilerStart or cudaProfilerStop without initialization. |
| cudaErrorProfilerAlreadyStarted | 57 | Deprecated This error return is deprecated as of CUDA 5.0. It is no longer an error to call cudaProfilerStart() when profiling is already enabled. |
| cudaErrorProfilerAlreadyStopped | 58 | Deprecated This error return is deprecated as of CUDA 5.0. It is no longer an error to call cudaProfilerStop() when profiling is already disabled. |
| cudaErrorAssert | 59 | An assert triggered in device code during kernel execution. The device cannot be used again until cudaThreadExit() is called. All existing allocations are invalid and must be reconstructed if the program is to continue using CUDA. |
| cudaErrorTooManyPeers | 60 | This error indicates that the hardware resources required to enable peer access have been exhausted for one or more of the devices passed to cudaEnablePeerAccess(). |
| cudaErrorHostMemoryAlreadyRegistered | 61 | This error indicates that the memory range passed to cudaHostRegister() has already been registered. |
| cudaErrorHostMemoryNotRegistered | 62 |	This error indicates that the pointer passed to cudaHostUnregister() does not correspond to any currently registered memory region. |
| cudaErrorOperatingSystem | 63 | This error indicates that an OS call failed. |
| cudaErrorPeerAccessUnsupported | 64 | This error indicates that P2P access is not supported across the given devices. |
| cudaErrorLaunchMaxDepthExceeded | 65 | This error indicates that a device runtime grid launch did not occur because the depth of the child grid would exceed the maximum supported number of nested grid launches. |
| cudaErrorLaunchFileScopedTex | 66 | This error indicates that a grid launch did not occur because the kernel uses file- scoped textures which are unsupported by the device runtime. Kernels launched via the device runtime only support textures created with the Texture Object API's. |
| cudaErrorLaunchFileScopedSurf | 67 | This error indicates that a grid launch did not occur because the kernel uses file- scoped surfaces which are unsupported by the device runtime. Kernels launched via the device runtime only support surfaces created with the Surface Object API's. |
| cudaErrorSyncDepthExceeded | 68 | This error indicates that a call to cudaDeviceSynchronize made from the device runtime failed because the call was made at grid depth greater than than either the default (2 levels of grids) or user specified device limit cudaLimitDevRuntimeSyncDepth. To be able to synchronize on launched grids at a greater depth successfully, the maximum nested depth at which cudaDeviceSynchronize will be called must be specified with the cudaLimitDevRuntimeSyncDepth limit to the cudaDeviceSetLimit api before the host-side launch of a kernel using the device runtime. Keep in mind that additional levels of sync depth require the runtime to reserve large amounts of device memory that cannot be used for user allocations. |
| cudaErrorLaunchPendingCountExceeded | 69 | This error indicates that a device runtime grid launch failed because the launch would exceed the limit cudaLimitDevRuntimePendingLaunchCount. For this launch to proceed successfully, cudaDeviceSetLimit must be called to set the cudaLimitDevRuntimePendingLaunchCount to be higher than the upper bound of outstanding launches that can be issued to the device runtime. Keep in mind that raising the limit of pending device runtime launches will require the runtime to reserve device memory that cannot be used for user allocations. |
| cudaErrorNotPermitted | 70 | This error indicates the attempted operation is not permitted. |
| cudaErrorNotSupported | 71 | This error indicates the attempted operation is not supported on the current system or device. |
| cudaErrorHardwareStackError | 72 | Device encountered an error in the call stack during kernel execution, possibly due to stack corruption or exceeding the stack size limit. The context cannot be used, so it must be destroyed (and a new one should be created). All existing device memory allocations from this context are invalid and must be reconstructed if the program is to continue using CUDA. |
| cudaErrorIllegalInstruction | 73 | The device encountered an illegal instruction during kernel execution The context cannot be used, so it must be destroyed (and a new one should be created). All existing device memory allocations from this context are invalid and must be reconstructed if the program is to continue using CUDA. |
| cudaErrorMisalignedAddress | 74 | The device encountered a load or store instruction on a memory address which is not aligned. The context cannot be used, so it must be destroyed (and a new one should be created). All existing device memory allocations from this context are invalid and must be reconstructed if the program is to continue using CUDA. |
| cudaErrorInvalidAddressSpace | 75 | While executing a kernel, the device encountered an instruction which can only operate on memory locations in certain address spaces (global, shared, or local), but was supplied a memory address not belonging to an allowed address space. The context cannot be used, so it must be destroyed (and a new one should be created). All existing device memory allocations from this context are invalid and must be reconstructed if the program is to continue using CUDA. |
| cudaErrorInvalidPc | 76 | The device encountered an invalid program counter. The context cannot be used, so it must be destroyed (and a new one should be created). All existing device memory allocations from this context are invalid and must be reconstructed if the program is to continue using CUDA. |
| cudaErrorIllegalAddress | 77 | The device encountered a load or store instruction on an invalid memory address. The context cannot be used, so it must be destroyed (and a new one should be created). All existing device memory allocations from this context are invalid and must be reconstructed if the program is to continue using CUDA. |
| cudaErrorInvalidPtx | 78 | A PTX compilation failed. The runtime may fall back to compiling PTX if an application does not contain a suitable binary for the current device. |
| cudaErrorInvalidGraphicsContext | 79 | This indicates an error with the OpenGL or DirectX context. |
| cudaErrorStartupFailure | 0x7f | This indicates an internal startup failure in the CUDA runtime. |
| cudaErrorApiFailureBase | 10000 | Any unhandled CUDA driver error is added to this value and returned via the runtime. Production releases of CUDA should not return such errors. Deprecated This error return is deprecated as of CUDA 4.1. |

## CUDA Version Management

| Function | Description |
|---|---|
| cudaError_t cudaDriverGetVersion (int *driverVersion) | Returns the CUDA driver version. <BR> cudaError_t = cudaSuccess, cudaErrorInvalidValue |
| cudaError_t cudaRuntimeGetVersion (int *runtimeVersion) | Returns the CUDA Runtime version. <BR> cudaError_t = cudaSuccess, cudaErrorInvalidValue |

## CUDA Error Handling

| Function | Description |
|---|---|
| const __cudart_builtin__ char *cudaGetErrorName (cudaError_t error) | Returns the string representation of an error code enum name. |
| const __cudart_builtin__ char *cudaGetErrorString (cudaError_t error) | Returns the description string for an error code. |
| cudaError_t cudaGetLastError (void) | Returns the last error that has been produced by any of the runtime calls in the same host thread and resets it to cudaSuccess. |
| cudaError_t cudaPeekAtLastError (void) | Returns the last error that has been produced by any of the runtime calls in the same host thread. <BR> Note that this call does not reset the error to cudaSuccess like cudaGetLastError(). |

## CUDA Profiler Control

| Function | Description |
|---|---|
| cudaError_t cudaProfilerInitialize (const char *configFile, const char *outputFile, cudaOutputMode_t outputMode) | Initialize the CUDA profiler. <BR> cudaError_t = 	cudaSuccess, cudaErrorInvalidValue, cudaErrorProfilerDisabled |
| cudaError_t cudaProfilerStart (void) | Enable profiling. <BR> cudaError_t = cudaSuccess |
| cudaError_t cudaProfilerStop (void) | Disable profiling. <BR> cudaError_t = cudaSuccess |

## CUDA Device Management

| Function | Description |
|---|---|
| cudaError_t cudaGetDeviceCount (int *count) | Returns the number of compute-capable devices. <BR> cudaError_t = cudaSuccess, cudaErrorNoDevice, cudaErrorInsufficientDriver |
| cudaError_t cudaDeviceGetAttribute (int *value, cudaDeviceAttr attr, int device) | Returns information about the device. <BR> cudaError_t = cudaSuccess, cudaErrorInvalidDevice, cudaErrorInvalidValue <BR> 
		cudaDevAttrMaxThreadsPerBlock: Maximum number of threads per block;
		cudaDevAttrMaxBlockDimX: Maximum x-dimension of a block;
		cudaDevAttrMaxBlockDimY: Maximum y-dimension of a block;
		cudaDevAttrMaxBlockDimZ: Maximum z-dimension of a block;
		cudaDevAttrMaxGridDimX: Maximum x-dimension of a grid;
		cudaDevAttrMaxGridDimY: Maximum y-dimension of a grid;
		cudaDevAttrMaxGridDimZ: Maximum z-dimension of a grid;
		cudaDevAttrMaxSharedMemoryPerBlock: Maximum amount of shared memory available to a thread block in bytes;
		cudaDevAttrTotalConstantMemory: Memory available on device for __constant__ variables in a CUDA C kernel in bytes;
		cudaDevAttrWarpSize: Warp size in threads;
		cudaDevAttrMaxPitch: Maximum pitch in bytes allowed by the memory copy functions that involve memory regions allocated through cudaMallocPitch();
		cudaDevAttrMaxTexture1DWidth: Maximum 1D texture width;
		cudaDevAttrMaxTexture1DLinearWidth: Maximum width for a 1D texture bound to linear memory;
		cudaDevAttrMaxTexture1DMipmappedWidth: Maximum mipmapped 1D texture width;
		cudaDevAttrMaxTexture2DWidth: Maximum 2D texture width;
		cudaDevAttrMaxTexture2DHeight: Maximum 2D texture height;
		cudaDevAttrMaxTexture2DLinearWidth: Maximum width for a 2D texture bound to linear memory;
		cudaDevAttrMaxTexture2DLinearHeight: Maximum height for a 2D texture bound to linear memory;
		cudaDevAttrMaxTexture2DLinearPitch: Maximum pitch in bytes for a 2D texture bound to linear memory;
		cudaDevAttrMaxTexture2DMipmappedWidth: Maximum mipmapped 2D texture width;
		cudaDevAttrMaxTexture2DMipmappedHeight: Maximum mipmapped 2D texture height;
		cudaDevAttrMaxTexture3DWidth: Maximum 3D texture width;
		cudaDevAttrMaxTexture3DHeight: Maximum 3D texture height;
		cudaDevAttrMaxTexture3DDepth: Maximum 3D texture depth;
		cudaDevAttrMaxTexture3DWidthAlt: Alternate maximum 3D texture width, 0 if no alternate maximum 3D texture size is supported;
		cudaDevAttrMaxTexture3DHeightAlt: Alternate maximum 3D texture height, 0 if no alternate maximum 3D texture size is supported;
		cudaDevAttrMaxTexture3DDepthAlt: Alternate maximum 3D texture depth, 0 if no alternate maximum 3D texture size is supported;
		cudaDevAttrMaxTextureCubemapWidth: Maximum cubemap texture width or height;
		cudaDevAttrMaxTexture1DLayeredWidth: Maximum 1D layered texture width;
		cudaDevAttrMaxTexture1DLayeredLayers: Maximum layers in a 1D layered texture;
		cudaDevAttrMaxTexture2DLayeredWidth: Maximum 2D layered texture width;
		cudaDevAttrMaxTexture2DLayeredHeight: Maximum 2D layered texture height;
		cudaDevAttrMaxTexture2DLayeredLayers: Maximum layers in a 2D layered texture;
		cudaDevAttrMaxTextureCubemapLayeredWidth: Maximum cubemap layered texture width or height;
		cudaDevAttrMaxTextureCubemapLayeredLayers: Maximum layers in a cubemap layered texture;
		cudaDevAttrMaxSurface1DWidth: Maximum 1D surface width;
		cudaDevAttrMaxSurface2DWidth: Maximum 2D surface width;
		cudaDevAttrMaxSurface2DHeight: Maximum 2D surface height;
		cudaDevAttrMaxSurface3DWidth: Maximum 3D surface width;
		cudaDevAttrMaxSurface3DHeight: Maximum 3D surface height;
		cudaDevAttrMaxSurface3DDepth: Maximum 3D surface depth;
		cudaDevAttrMaxSurface1DLayeredWidth: Maximum 1D layered surface width;
		cudaDevAttrMaxSurface1DLayeredLayers: Maximum layers in a 1D layered surface;
		cudaDevAttrMaxSurface2DLayeredWidth: Maximum 2D layered surface width;
		cudaDevAttrMaxSurface2DLayeredHeight: Maximum 2D layered surface height;
		cudaDevAttrMaxSurface2DLayeredLayers: Maximum layers in a 2D layered surface;
		cudaDevAttrMaxSurfaceCubemapWidth: Maximum cubemap surface width;
		cudaDevAttrMaxSurfaceCubemapLayeredWidth: Maximum cubemap layered surface width;
		cudaDevAttrMaxSurfaceCubemapLayeredLayers: Maximum layers in a cubemap layered surface;
		cudaDevAttrTextureAlignment: Alignment requirement; texture base addresses aligned to textureAlign bytes do not need an offset applied to texture fetches;
		cudaDevAttrTexturePitchAlignment: Pitch alignment requirement for 2D texture references bound to pitched memory;
		cudaDevAttrMaxRegistersPerBlock: Maximum number of 32-bit registers available to a thread block;
		cudaDevAttrClockRate: Peak clock frequency in kilohertz;
		cudaDevAttrGpuOverlap: 1 if the device can concurrently copy memory between host and device while executing a kernel, or 0 if not;
		cudaDevAttrMultiProcessorCount: Number of multiprocessors on the device;
		cudaDevAttrKernelExecTimeout: 1 if there is a run time limit for kernels executed on the device, or 0 if not;
		cudaDevAttrIntegrated: 1 if the device is integrated with the memory subsystem, or 0 if not;
		cudaDevAttrCanMapHostMemory: 1 if the device can map host memory into the CUDA address space, or 0 if not;
		cudaDevAttrComputeMode: Compute mode is the compute mode that the device is currently in. Available modes are as follows:
			cudaComputeModeDefault: Default mode - Device is not restricted and multiple threads can use cudaSetDevice() with this device.
			cudaComputeModeExclusive: Compute-exclusive mode - Only one thread will be able to use cudaSetDevice() with this device.
			cudaComputeModeProhibited: Compute-prohibited mode - No threads can use cudaSetDevice() with this device.
			cudaComputeModeExclusiveProcess: Compute-exclusive-process mode - Many threads in one process will be able to use cudaSetDevice() with this device.
		cudaDevAttrConcurrentKernels: 1 if the device supports executing multiple kernels within the same context simultaneously, or 0 if not. It is not guaranteed that multiple kernels will be resident on the device concurrently so this feature should not be relied upon for correctness;
		cudaDevAttrEccEnabled: 1 if error correction is enabled on the device, 0 if error correction is disabled or not supported by the device;
		cudaDevAttrPciBusId: PCI bus identifier of the device;
		cudaDevAttrPciDeviceId: PCI device (also known as slot) identifier of the device;
		cudaDevAttrTccDriver: 1 if the device is using a TCC driver. TCC is only available on Tesla hardware running Windows Vista or later;
		cudaDevAttrMemoryClockRate: Peak memory clock frequency in kilohertz;
		cudaDevAttrGlobalMemoryBusWidth: Global memory bus width in bits;
		cudaDevAttrL2CacheSize: Size of L2 cache in bytes. 0 if the device doesn't have L2 cache;
		cudaDevAttrMaxThreadsPerMultiProcessor: Maximum resident threads per multiprocessor;
		cudaDevAttrUnifiedAddressing: 1 if the device shares a unified address space with the host, or 0 if not;
		cudaDevAttrComputeCapabilityMajor: Major compute capability version number;
		cudaDevAttrComputeCapabilityMinor: Minor compute capability version number;
		cudaDevAttrStreamPrioritiesSupported: 1 if the device supports stream priorities, or 0 if not;
		cudaDevAttrGlobalL1CacheSupported: 1 if device supports caching globals in L1 cache, 0 if not;
		cudaDevAttrGlobalL1CacheSupported: 1 if device supports caching locals in L1 cache, 0 if not;
		cudaDevAttrMaxSharedMemoryPerMultiprocessor: Maximum amount of shared memory available to a multiprocessor in bytes; this amount is shared by all thread blocks simultaneously resident on a multiprocessor;
		cudaDevAttrMaxRegistersPerMultiprocessor: Maximum number of 32-bit registers available to a multiprocessor; this number is shared by all thread blocks simultaneously resident on a multiprocessor;
		cudaDevAttrManagedMemSupported: 1 if device supports allocating managed memory, 0 if not;
		cudaDevAttrIsMultiGpuBoard: 1 if device is on a multi-GPU board, 0 if not;
		cudaDevAttrMultiGpuBoardGroupID: Unique identifier for a group of devices on the same multi-GPU board; |







