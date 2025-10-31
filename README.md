# Radeon™ GPU Profiler

The Radeon GPU Profiler (RGP) is a ground-breaking low-level optimization tool from AMD. It provides detailed timing information on Radeon Graphics using custom, built-in, hardware thread-tracing, allowing the developer deep inspection of GPU workloads.

This unique tool generates easy to understand visualizations of how your DirectX®12 and Vulkan® games interact with the GPU at the hardware level. Profiling a game is both a quick, and simple process using the Radeon Developer Panel and the public display driver.

In order to use the latest features of RGP, it is strongly recommended that users update to the latest driver.


## Getting Started

1. Install the latest AMD Video/display driver.
2. Unzip/Untar the download file. The directory contains the following:
   * Radeon Developer Service (RDS)
   * RadeonDeveloperServiceCLI (RDS headless)
   * Radeon Developer Panel (RDP)
   * Radeon GPU Profiler (RGP)
3. To capture a profile from a game, run the Radeon Developer Panel and follow the instructions in the Help. Help can be found in the following locations:
   * Help web pages exist in the "help" subdirectory
   * Help web pages can be accessed from the **Help** button in the Radeon Developer Panel
   * Help web pages can be accessed from the Welcome screen in the Radeon GPU Profiler, or from the **Help** menu
   * The documentation is hosted publicly at:
     * https://gpuopen.com/manuals/rdp_manual/rdp_manual-index/
     * https://gpuopen.com/manuals/rgp_manual/rgp_manual-index/

## Graphics APIs, RDNA™ hardware, and operating systems
### Supported APIs
 * DirectX12
 * Vulkan

### Supported RDNA hardware
* AMD Radeon RX 9000 series
* AMD Radeon RX 7000 series
* AMD Radeon RX 6000 series
* AMD Radeon RX 5000 series
* AMD Ryzen™ Processors with Radeon Graphics

### Supported Operating Systems
* Windows® 10
* Windows® 11
* Ubuntu® 24.04 LTS (Vulkan only)
  * With the introduction of 25.20-based Linux drivers, the AMDVLK driver is no longer included in the amdgpu-pro driver package. This is a result of the AMDVLK open-source project being discontinued as mentioned [here](https://github.com/GPUOpen-Drivers/AMDVLK/discussions/416). Instead, the RADV open-source Vulkan® driver is installed by default. Consequently, the Radeon Developer Panel does not support capturing data from Vulkan applications when using these newer driver releases. To analyze Linux Vulkan workloads with Radeon GPU Profiler (RGP), Radeon Raytracing Analyzer (RRA), or Radeon Memory Visualizer (RMV), users can opt for a 25.10-based driver. Alternatively, analysis can be performed using the data capture mechanism integrated within the RADV driver, although this method is not supported by the Radeon Developer Panel. For more information on configuring RADV, refer to the environment variable documentation, specifically the [MESA_VK_TRACE_* environment variables](https://docs.mesa3d.org/envvars.html#envvar-MESA_VK_TRACE) which can be utilized for enabling and configuring tracing.

## Compute APIs, RDNA hardware, and operating systems
### Supported APIs
* OpenCL™
* HIP

### Supported RDNA hardware
* AMD Radeon RX 9000 series
* AMD Radeon RX 7000 series
* AMD Radeon RX 6000 series
* AMD Radeon RX 5000 series
* AMD Ryzen Processors with Radeon Graphics

### Supported Operating Systems
* Windows 10
* Windows 11

