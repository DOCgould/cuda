# CUDA Runtime 6.5

## CUDA Error Types  

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
| cudaError_t cudaDeviceGetAttribute (int *value, cudaDeviceAttr attr, int device) | Returns information about the device. <BR> cudaError_t = cudaSuccess, cudaErrorInvalidDevice, cudaErrorInvalidValue |
| cudaError_t cudaSetDevice (int device) | Set device to be used for GPU executions. <BR> cudaError_t = cudaSuccess, cudaErrorInvalidDevice, cudaErrorDeviceAlreadyInUse |
| cudaError_t cudaSetDeviceFlags (unsigned int flags) | Sets flags to be used for device executions. <BR> cudaError_t = cudaSuccess, cudaErrorInvalidDevice, cudaErrorSetOnActiveProcess |
| cudaError_t cudaSetValidDevices (int *device_arr, int len) | Set a list of devices that can be used for CUDA. <BR> cudaError_t = cudaSuccess, cudaErrorInvalidValue, cudaErrorInvalidDevice |
| cudaError_t cudaGetDeviceProperties (cudaDeviceProp *prop, int device) | Returns information about the compute-device. <BR> cudaError_t = cudaSuccess, cudaErrorInvalidDevice |
| cudaError_t cudaChooseDevice (int *device, const cudaDeviceProp *prop) | Select compute-device which best matches criteria. <BR> cudaError_t = cudaSuccess, cudaErrorInvalidValue |
| cudaError_t cudaGetDevice (int *device) | Returns which device is currently being used. <BR> cudaError_t = cudaSuccess |
| cudaError_t cudaDeviceGetCacheConfig (cudaFuncCache *pCacheConfig) | Returns the preferred cache configuration for the current device. <BR> cudaError_t = cudaSuccess, cudaErrorInitializationError |
| cudaError_t cudaDeviceSetCacheConfig (cudaFuncCache cacheConfig) | Sets the preferred cache configuration for the current device. <BR> cudaError_t = cudaSuccess, cudaErrorInitializationError |
| cudaError_t cudaDeviceGetLimit (size_t *pValue, cudaLimit limit) | Returns resource limits. <BR> cudaError_t = cudaSuccess, cudaErrorUnsupportedLimit, cudaErrorInvalidValue |
| cudaError_t cudaDeviceSetLimit (cudaLimit limit, size_t value) | Set resource limits. <BR> cudaError_t = cudaSuccess, cudaErrorUnsupportedLimit, cudaErrorInvalidValue, cudaErrorMemoryAllocation |
| cudaError_t cudaDeviceGetPCIBusId (char *pciBusId, int len, int device) | Returns a PCI Bus Id string for the device. <BR> cudaError_t = cudaSuccess, cudaErrorInvalidValue, cudaErrorInvalidDevice |
| cudaError_t cudaDeviceGetByPCIBusId (int *device, const char *pciBusId) | Returns a handle to a compute device. <BR> cudaSuccess, cudaErrorInvalidValue, cudaErrorInvalidDevice |
| cudaError_t cudaDeviceGetSharedMemConfig (cudaSharedMemConfig *pConfig) | Returns the shared memory configuration for the current device. <BR> cudaSuccess, cudaErrorInvalidValue, cudaErrorInitializationError |
| cudaError_t cudaDeviceSetSharedMemConfig (cudaSharedMemConfig config) | Sets the shared memory configuration for the current device. <BR> cudaError_t = cudaSuccess, cudaErrorInvalidValue, cudaErrorInitializationError |
| cudaError_t cudaDeviceGetStreamPriorityRange (int *leastPriority, int *greatestPriority) | Returns numerical values that correspond to the least and greatest stream priorities. <BR> cudaError_t = cudaSuccess, cudaErrorInvalidValue |
| cudaError_t cudaDeviceReset (void) | Destroy all allocations and reset all state on the current device in the current process. <BR> cudaError_t = cudaSuccess |
| cudaError_t cudaDeviceSynchronize (void) | Wait for compute device to finish. <BR> cudaError_t = cudaSuccess |
| cudaError_t cudaIpcOpenEventHandle (cudaEvent_t *event, cudaIpcEventHandle_t handle) | Opens an interprocess event handle for use in the current process. <BR> cudaError_t = cudaSuccess, cudaErrorMapBufferObjectFailed, cudaErrorInvalidResourceHandle |
| cudaError_t cudaIpcGetEventHandle (cudaIpcEventHandle_t *handle, cudaEvent_t event) | Gets an interprocess handle for a previously allocated event. <BR> cudaError_t = cudaSuccess, cudaErrorInvalidResourceHandle, cudaErrorMemoryAllocation, cudaErrorMapBufferObjectFailed |
| cudaError_t cudaIpcOpenMemHandle (void **devPtr, cudaIpcMemHandle_t handle, unsigned int flags) | Opens an interprocess memory handle exported from another process and returns a device pointer usable in the local process. <BR> cudaError_t = cudaSuccess, cudaErrorMapBufferObjectFailed, cudaErrorInvalidResourceHandle, cudaErrorTooManyPeers |
| cudaError_t cudaIpcGetMemHandle (cudaIpcMemHandle_t *handle, void *devPtr) | Gets an interprocess memory handle for an existing device memory allocation. <BR> cudaError_t = cudaSuccess, cudaErrorInvalidResourceHandle, cudaErrorMemoryAllocation, cudaErrorMapBufferObjectFailed |
| cudaError_t cudaIpcCloseMemHandle (void *devPtr) | Close memory mapped with cudaIpcOpenMemHandle. <BR> cudaError_t = cudaSuccess, cudaErrorMapBufferObjectFailed, cudaErrorInvalidResourceHandle |

## CUDA Stream Management

| Function | Description |
|---|---|
| cudaError_t cudaStreamAddCallback (cudaStream_t stream, cudaStreamCallback_t callback, void *userData, unsigned int flags) | Add a callback to a compute stream. <BR> 	cudaError_t = cudaSuccess, cudaErrorInvalidResourceHandle, cudaErrorNotSupported |
| cudaError_t cudaStreamAttachMemAsync (cudaStream_t stream, void *devPtr, size_t length, unsigned int flags) |	Attach memory to a stream asynchronously. <BR> 	cudaError_t = cudaSuccess, cudaErrorNotReady, cudaErrorInvalidValue cudaErrorInvalidResourceHandle |
| cudaError_t cudaStreamCreate (cudaStream_t *pStream) | Create an asynchronous stream. <BR> cudaError_t = cudaSuccess, cudaErrorInvalidValue |
| cudaError_t cudaStreamCreateWithFlags (cudaStream_t *pStream, unsigned int flags) | Create an asynchronous stream. <BR> cudaError_t = cudaSuccess, cudaErrorInvalidValue |
| cudaError_t cudaStreamCreateWithPriority (cudaStream_t *pStream, unsigned int flags, int priority) | Create an asynchronous stream with the specified priority. <BR> 	cudaError_t = cudaSuccess, cudaErrorInvalidValue |
| cudaError_t cudaStreamGetFlags (cudaStream_t hStream, unsigned int *flags) | Query the flags of a stream. <BR> cudaError_t = cudaSuccess, cudaErrorInvalidValue, cudaErrorInvalidResourceHandle |
| cudaError_t cudaStreamGetPriority (cudaStream_t hStream, int *priority) | Query the priority of a stream. <BR> cudaError_t = cudaSuccess, cudaErrorInvalidValue, cudaErrorInvalidResourceHandle |
| cudaError_t cudaStreamQuery (cudaStream_t stream) | Queries an asynchronous stream for completion status. <BR> cudaError_t = cudaSuccess, cudaErrorNotReady, cudaErrorInvalidResourceHandle |
| cudaError_t cudaStreamSynchronize (cudaStream_t stream) | Waits for stream tasks to complete. <BR> cudaError_t = cudaSuccess, cudaErrorInvalidResourceHandle |
| cudaError_t cudaStreamWaitEvent (cudaStream_t stream, cudaEvent_t event, unsigned int flags) | Make a compute stream wait on an event. <BR> cudaError_t = cudaSuccess, cudaErrorInvalidResourceHandle |
| cudaError_t cudaStreamDestroy (cudaStream_t stream) | Destroys and cleans up an asynchronous stream. <BR> cudaError_t = cudaSuccess, cudaErrorInvalidResourceHandle |









