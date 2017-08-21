# Known Issues

1)  Radeon Developer Panel will NOT capture profiles from AMD multi-GPU configurations (e.g. two AMD GPUs). 
    It will work with one AMD GPU and other competitor cards installed in the same machine. Please note that the primary monitor will need to be configured for the AMD GPU/monitor combination.
2)  Radeon Developer Panel can only capture a profile on a single AMD GPU at a time. 
3)  Radeon Developer Panel cannot capture profiles from competitor GPUs.
4)  Radeon Developer Panel will NOT capture profiles from Windows Insider Editions.
5)  Anti-virus may impede key-based capture (Ctrl+Shift+C)
6)  There are no driver settings available for Vulkan yet.
7)  Applications that call Present() from the async compute queue are not supported. A fix will available soon.
8)  Queue synchronization data will be missing from DirectX12 apps running on Windows 10 Home.
9)  If the Developer Panel or the Developer Service crash on Linux while running with the root account, it may be necessary to restart/exit them again with the root account in order to cleanup shared memory.
10)  Radeon Developer Panel my fail to retrieve GPU clock frequencies when connected to a target application running on Linux. In such cases, the Clocks tab will display “-“ for Shader Clock and Memory Clock frequencies. A fix will be available soon.
11) Only the R9-380X, RX-480, RX-580 and RX-Vega64 GPUs will show the correct CU count and wavefront occupancy. The incorrect compute unit count, and therefore the incorrect wavefront occupancy, will be shown for GPUs with reduced CU's (R9-285, R9-380, RX-470, RX-460, RX-570, RX-560, RX-Vega56). 
