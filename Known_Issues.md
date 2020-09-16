# Known Issues

All platforms
-------------
1)  Radeon™ Developer Panel will NOT capture profiles from AMD multi-GPU configurations (e.g. two AMD GPUs). It will work with one AMD GPU and other non-AMD cards installed in the same machine. Please note that the primary monitor will need to be configured for the AMD GPU/monitor combination. For systems consisting of an AMD APU and AMD discrete GPU, capturing profiles should work, but an error may be logged in the Radeon Developer Panel regarding not being able to set peak clock mode. It is recommended that the GPU in the APU be disabled in the BIOS.
2)  Radeon Developer Panel can only capture a profile on a single AMD GPU at a time.
3)  Radeon Developer Panel cannot capture profiles from non-AMD GPUs.
4)  Radeon Developer Panel will NOT capture profiles from Windows® Insider Editions.
5)  Anti-virus may impede key-based capture (Ctrl+Shift+C)
6)  Applications that call Present() from the async compute queue are not supported.
7)  When using RGP with RenderDoc, please make sure that RenderDoc is terminated between RenderDoc capture sessions (generating a RenderDoc capture file or loading a RenderDoc capture file is considered a session for the purpose here). While it is possible to take multiple RGP profiles of a RenderDoc capture file, it is not possible to take RGP profiles between RenderDoc sessions. If this is attempted, RenderDoc will show an error dialog box indicating that an RGP profile can't be taken and to restart RenderDoc
8)  If an instance of Radeon GPU Profiler is spawned from RenderDoc, it must be closed before restarting RenderDoc. The menu option to create new RGP profiles will not be enabled otherwise.
9)  OpenCL™ captures may include an extra DMA command buffer in the Profile Summary.
10) Launching the RadeonDeveloperPanel, clicking "connect" and starting an application may cause a hang or reboot when using 3 or more attached monitors (especially if they are 4K). Please use a dual-monitor configuration at most to avoid this from happening.
11) Detailed instruction timing is not yet supported on OpenCL.

Windows®
-------
1)  Queue synchronization data will be missing from DirectX®12 apps running on Windows 10 Home.
2)  D3D12 command list calls of ExecuteIndirect() may show in RGP as multiple compute events.
3)  Some Radeon Software hotkeys may conflict with Radeon GPU Profiler shortcut keys. The Radeon Software hotkeys can be reconfigured by opening the Radeon Software panel (from the system tray), selecting the Hotkeys tab under Settings then changing or unbinding any conflicting hotkeys.

Linux®
-----
1)  Installations of Ubuntu 20.04 or newer may have the RADV open source Vulkan® driver installed by default on the system. As a result, after an amdgpu-pro driver install, the default Vulkan ICD may be the RADV ICD. In order to capture a profile, Vulkan applications must be using the amdgpu-pro Vulkan ICD. The default Vulkan ICD can be overridden by setting the following environment variable before launching a Vulkan application: VK_ICD_FILENAMES=/etc/vulkan/icd.d/amd_icd64.json
2)  After launching RGP from the Developer Panel to view a captured profile, the panel may fail to connect the next time it is launched. The workaround is to close RGP before relaunching the panel.
3)  If the Developer Panel or the Developer Service crash while running with the root account, it may be necessary to restart/exit them again with the root account in order to cleanup shared memory.
4)  When running with the root account, the Developer Panel may output error or warning messages to the terminal. These should not prevent the panel from functioning properly.
5)  The Radeon Developer Service and Panel are only officially supported using the standard desktop managers (GDM and Unity). Other desktop managers should work but a dialog box indicating that the service is running in headless mode may pop up. However, it should still be possible to capture profiles.
6)  If the RadeonDeveloperServiceCLI application crashes, shared memory may need to be cleaned up by running the RemoveSharedMemory.sh script located in the script folder of the RGP release kit. Run the script with elevated privileges using sudo.
7)  The Radeon Developer Panel may fail to start the Radeon Developer Service when the Connect button is clicked. If this occurs, manually start the Radeon Developer Service, select localhost from the the Recent connections list and click the Connect button again.

RDNA
----
1)  The Device configuration does not show the correct Work group processor per Shader engine for certain parts with harvested CUs.
