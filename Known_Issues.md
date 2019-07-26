# Known Issues

All platforms
-------------
1)  Radeon Developer Panel will NOT capture profiles from AMD multi-GPU configurations (e.g. two AMD GPUs). It will work with one AMD GPU and other non-AMD cards installed in the same machine. Please note that the primary monitor will need to be configured for the AMD GPU/monitor combination. For systems consisting of an AMD APU and AMD discrete GPU, capturing profiles should work, but an error may be logged in the Radeon Developer Panel regarding not being able to set peak clock mode. It is recommended that the GPU in the APU be disabled in the BIOS.
2)  Radeon Developer Panel can only capture a profile on a single AMD GPU at a time.
3)  Radeon Developer Panel cannot capture profiles from non-AMD GPUs.
4)  Radeon Developer Panel will NOT capture profiles from Windows Insider Editions.
5)  Anti-virus may impede key-based capture (Ctrl+Shift+C)
6)  Applications that call Present() from the async compute queue are not supported. A fix will be available soon.
7)  When using RGP with RenderDoc, please make sure that RenderDoc is terminated between RenderDoc capture sessions (generating a RenderDoc capture file or loading a RenderDoc capture file is considered a session for the purpose here). While it is possible to take multiple RGP profiles of a RenderDoc capture file, it is not possible to take RGP profiles between RenderDoc sessions. If this is attempted, RenderDoc will pop up an error dialog box indicating that an RGP profile can't be taken and to restart RenderDoc
8)  If an instance of Radeon GPU Profiler is spawned from RenderDoc, it must be closed before restarting RenderDoc. The menu option to create new RGP profiles will not be enabled otherwise.
9)  OpenCL captures may include an extra DMA command buffer in the Profile Summary. This issue will be fixed in a future version.
10) Launching the RadeonDeveloperPanel, clicking "connect" and starting an application may cause a hang or reboot when using 3 or more attached monitors (especially if they are 4K). Please use a dual-monitor configuration at most to avoid this from happening. This issue is currently being investigated.
11) Detailed instruction timing is not yet supported on OpenCL.
12) The last 2 arguments to vkDrawIndexed may contain incorrect values on Vega and Radeon 7 GPU's. This issue is currently under investigation.

Windows
-------
1)  Queue synchronization data will be missing from DirectX12 apps running on Windows 10 Home.
2)  D3D12 command list calls of ExecuteIndirect() may show in RGP as multiple compute events. This will be corrected in a future release after obtaining more information from the driver.
3)  The Radeon Overlay hotkey, Alt+R, conflicts with the Radeon GPU Profiler shortcut key used to select the Pipeline state pane.  The Radeon Overlay hotkey can be reconfigured by opening the Radeon Settings panel (from the system tray), selecting the Preferences tab then clicking the "Toggle Radeon Overlay Hotkey" button.

Linux
-----
1)  If the Developer Panel or the Developer Service crash while running with the root account, it may be necessary to restart/exit them again with the root account in order to cleanup shared memory.
2)  The Radeon Developer Service and Panel are only officially supported using the standard desktop managers (GDM and Unity). Other desktop managers should work but a dialog box indicating that the service is running in headless mode may pop up. However, it should still be possible to capture profiles.
3)  If the RadeonDeveloperServiceCLI application crashes, shared memory may need to be cleaned up by running the RemoveSharedMemory.sh script located in the script folder of the RGP release kit. Run the script with elevated privileges using sudo.
4)  The Radeon Developer Panel may fail to start the Radeon Developer Service when the Connect button is clicked. If this occurs, manually start the Radeon Developer Service, select localhost from the the Recent connections list and click the Connect button again.

Navi
----
1) Some shaders that write to the execute mask register may not have instruction timing data.
2) The Device configuration does not show the correct Work group processor per Shader engine for certain parts with harvested CUs.
