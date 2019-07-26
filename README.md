# Radeon-GPUProfiler

The Radeon GPU Profiler (RGP) is a ground-breaking low-level optimization tool from AMD.  It provides detailed timing information on Radeon Graphics using custom, built-in, hardware thread-tracing, allowing the developer deep inspection of GPU workloads.

This unique tool generates easy to understand visualizations of how your DirectX®12 and Vulkan® games interact with the GPU at the hardware level. Profiling a game is both a quick, and simple process using the Radeon Developer Panel and the public display driver.

In order to use the latest features of RGP, it is strongly recommended that users update to the latest driver.


## Getting Started

1. Install the latest AMD Video/display driver.
2. Unzip/Untar the download file. The directory contains the following:
* Radeon Developer Service (RDS)
* RadeonDeveloperServiceCLI (RDS headless)
* Radeon Developer Panel (RDP)
* Radeon GPU Profiler (RGP)
3. To gather a profile from a game run the Radeon Developer Panel and follow the instructions in the Help - Help can be found in the following locations:
* Help web pages exist in the "docs" sub directory
* Help web pages can be accessed from the Help button in the Developer Panel
* Help web pages can be accessed from the Welcome screen in the Radeon GPU Profiler, or from the help menu
* The documentation is hosted publicly at:
  http://devdrivertools.readthedocs.io/en/latest/
  http://radeon-gpuprofiler.readthedocs.io/en/latest/

## Supported ASICs
* AMD Radeon™ RX 5700 and RX 5700 XT
* AMD Radeon™ VII
* AMD RX Vega 64 and RX Vega 56
* AMD Ryzen 5 2400G and Ryzen 3 2200G Processors with Radeon Vega Graphics
* AMD Radeon™ R9 Fury and Nano series  
* AMD Radeon™ RX 400, RX 500 series
* AMD Tonga R9 285, R9 380
 
## Supported OS's and API's
### Windows10  
* DirectX12  
* Vulkan
    
### Windows7  
* Vulkan  - User must install latest VC 2015 redistributables from https://www.microsoft.com/en-us/download/details.aspx?id=53840
    
### Ubuntu 18.04.2 LTS
* Vulkan

## Supported compute APIs, GCN hardware, and operating systems
### Supported APIs
* OpenCL

### Supported GCN hardware for graphics APIs
* AMD Radeon™ VII
* AMD RX Vega 64 and RX Vega 56
* AMD Ryzen 5 2400G and Ryzen 3 2200G Processors with Radeon Vega Graphics

### Supported Operating Systems
* Windows 10
* Windows 7
* Ubuntu 18.04.2 LTS
