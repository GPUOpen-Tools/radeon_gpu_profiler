The Radeon™ GPU Profiler
========================

The Radeon GPU Profiler is a performance tool that can be used by
developers to optimize DirectX®12, Vulkan®, OpenCL™ and HIP applications for
AMD RDNA™ hardware. It is part of a suite of tools comprised of the
following software:

-  **Radeon Developer Mode Driver** - This is shipped as part of the AMD
   public Adrenalin driver and supports the developer mode features required for
   profiling.

-  **Radeon Developer Service (RDS)** - A system tray application that
   unlocks the Developer Mode Driver features and supports
   communications with high level tools. A headless version is also
   available called RadeonDeveloperServiceCLI.

-  **Radeon Developer Panel (RDP)** - A GUI application that allows the
   developer to configure driver settings and generate profiler data
   from DirectX12, Vulkan, OpenCL and HIP applications.

-  **Radeon GPU Profiler (RGP)** - A GUI tool used to visualize and
   analyze the profile data.

   This document describes how to generate a profile using the Radeon
   Developer Panel and how the Radeon GPU Profiler can be used to
   examine the output profiles. The Radeon GPU Profiler is currently
   designed to work with compute applications and frame based graphics
   applications. It is specifically designed to address the issues that
   developers are dealing with in the move from traditional graphics
   APIs to explicit APIs. It also provides the visualization of RDNA
   hardware-specific information allowing the developer to tune an
   application to the full potential of the architecture. The tool
   provides unique visualizations of queue synchronization using fences
   and semaphores, asynchronous compute, and barrier timings. Currently,
   it supports the explicit graphics APIs (DirectX12 and Vulkan), compute
   APIs (OpenCL and HIP) and will NOT work with older graphics APIs such as
   DirectX11 or OpenGL.

.. toctree::
   :maxdepth: 2
   :caption: Contents:

   quickstart.rst
   settings.rst
   overview_windows.rst
   events_windows.rst
   api_shader_stage_control.rst
   isa_view.rst
   zoom_controls.rst
   user_debug_markers.rst
   rga_and_rgp_interop.rst
   renderdoc_and_rgp_interop.rst

Graphics APIs, RDNA hardware, and operating systems
---------------------------------------------------

.. rubric:: Supported APIs

-  DirectX12

-  Vulkan

.. rubric:: Supported RDNA hardware

-  AMD Radeon RX 7000 series

-  AMD Radeon RX 6000 series

-  AMD Radeon RX 5000 series

-  AMD Ryzen™ Processors with Radeon Graphics

.. rubric:: Supported Operating Systems

-  Windows® 10

-  Windows® 11

-  Ubuntu 22.04 LTS (Vulkan only)

Compute APIs, RDNA hardware, and operating systems
--------------------------------------------------

.. rubric:: Supported APIs

-  OpenCL

-  HIP

.. rubric:: Supported RDNA hardware

-  AMD Radeon RX 7000 series

-  AMD Radeon RX 6000 series

-  AMD Radeon RX 5000 series

-  AMD Ryzen Processors with Radeon Graphics

.. rubric:: Supported Operating Systems

-  Windows 10

-  Windows 11

Disclaimer
----------

The information contained herein is for informational purposes only, and is subject to change without notice. While every
precaution has been taken in the preparation of this document, it may contain technical inaccuracies, omissions and typographical
errors, and AMD is under no obligation to update or otherwise correct this information. Advanced Micro Devices, Inc. makes no
representations or warranties with respect to the accuracy or completeness of the contents of this document, and assumes no
liability of any kind, including the implied warranties of noninfringement, merchantability or fitness for particular purposes, with
respect to the operation or use of AMD hardware, software or other products described herein. No license, including implied or
arising by estoppel, to any intellectual property rights is granted by this document. Terms and limitations applicable to the purchase
or use of AMD's products are as set forth in a signed agreement between the parties or in AMD's Standard Terms and Conditions
of Sale.

AMD, the AMD Arrow logo, Radeon, Ryzen, CrossFire, RDNA and combinations thereof are trademarks of Advanced Micro Devices, Inc.
Other product names used in this publication are for identification purposes only and may be trademarks of their respective companies.

DirectX is a registered trademark of Microsoft Corporation in the US and other jurisdictions.

Vulkan and the Vulkan logo are registered trademarks of the Khronos Group Inc.

OpenCL is a trademark of Apple Inc. used by permission by Khronos Group, Inc.

Microsoft is a registered trademark of Microsoft Corporation in the US and other jurisdictions.

Windows is a registered trademark of Microsoft Corporation in the US and other jurisdictions.

© 2016-2024 Advanced Micro Devices, Inc. All rights reserved.


