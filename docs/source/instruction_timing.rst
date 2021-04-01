Instruction Timing
------------------

The Instruction Timing pane shows the average issue latency of each instruction of a single shader.
The Instruction Timing information is generated using hardware support on AMD RDNA and GCN GPUs.
Generating Instruction Timing does not require recompilation of shaders or insertion of any
instrumentation into shaders.

The Instruction Timing pane shows RDNA or GCN ISA. For a description of ISA, refer to the shader
programming guides at
`GPUOpen <https://gpuopen.com/documentation/amd-isa-documentation/>`_.
The Instruction Timing view for a shader is shown below.

.. image:: media_rgp/RGP_Instruction_Timing_1.png

\ **Average Latency**

Each shader line in the Instruction Timing view shows the time taken between the issue of an
instruction and the one after that. To provide information on what Average Latency means some
sample ISA statements are shown below.

**Best Case Instruction Issue:** In the below image, we see three instructions. The *4 clocks*
denote the latency between the issue of the *s_mov_b32* instruction and the issue of the following
*v_lshlrev_b32_e32* instruction. Similarly, the interval between the issue of *v_lshlrev_b32_e32*
and *s_lshr_b32* instruction is 6 clocks. This example shows the best performance case where each
instruction is issued at an interval of 4 clocks.

.. image:: media_rgp/RGP_Instruction_Timing_Example_1.png

**Delays in Instruction Issue:** In the below image, we see three export instructions. The
*exp pos0* has a rather long interval of 11,121 clocks.  This can be expected since  the
*exp pos0* instruction's issue can be delayed for reasons such as unavailable memory resources
which may be in use by other wavefronts. As a result, there is a long duration in the instruction.
Since the latency waiting for memory resources was seen for the first export instruction,
subsequent exports have a much shorter duration.

.. image:: media_rgp/RGP_Instruction_Timing_Example_2.png

**Waitcounts and Instruction Issue:** In the below image, we see seven instructions. The
*v_mov_b32_e32*  and the *v_perm_b32* instructions issue in 4 clocks as expected. We then see a
*tbuffer_load* followed by a *s_waitcnt*. The *s_waitcnt* has a longer issue interval of 721
clocks. The *tbuffer_load* instruction also has a relatively short latency of only 19 cycles which
may seem counter intuitive since it's a memory load instruction. However, this is expected as
*s_waitcnt* is a shader instruction used for synchronization to wait for previous instructions such
as the previous buffer load to finish. The *s_waitcnt* instruction will issue and then wait (in this
case 721 clocks) until the next instruction which is the *ds_write2_b32* can be issued.

.. image:: media_rgp/RGP_Instruction_Timing_Example_3.png

The Average Latency between any two instructions shown is an average of the latency (between those
instructions) measured for all the wavefronts analyzed.

\ **Hit Count**

The *Hit count* for each instruction shows the number of times the instruction was executed for the
selected event. Any basic blocks that have zero hit counts will be displayed as disabled in the
Instruction timing view, as shown below.

.. image:: media_rgp/RGP_Instruction_Timing_DisabledBlock.png

\ **Instruction Cost Percent**

The *Instruction Cost* for each ISA instruction shows the percentage of the Total Issue Latency of
the whole shader. For shaders with branches where consecutive instructions can have varying hit
counts, the Instruction Cost incorporates the extra hit counts for that instruction. This allows us
to find the hot-spot in the shader.

The Instruction Cost for an ISA instruction is calculated as follows:

*Instruction Cost = 100 * (Sum of All Latencies for ISA Instruction) / (Sum of All Latencies for
the shader)*

\ **Instruction Timing Capture Granularity**

Instruction Timing information is generated for the whole RGP profile, but data is limited to a
single shader engine. Only waves executed by a single shader engine contribute to the hit counts
and timing information shown in the Instruction timing pane. Please see the Radeon Developer Panel
documentation for more information on how to capture instruction timing information.

To view all the events that have Instruction Timing information, the developer can choose the
"Color by Instruction Timing" option in the Wavefront Occupancy or the Event Timing views.

\ **Availability of Instruction Timing**

In certain cases it is possible that the Instruction Timing information may not be available for
all events. The main reasons why Instruction Timing information may not be present
for an event are described below.

\ **Hardware Architecture and Draw Scheduling**: Instruction Timing information is only sampled
from some of the compute units on a single shader engine of the GPU. As a result, it is possible
for events with very few waves to not have instruction data. This can happen if the
GPU schedules the waves on a shader engine or compute unit that doesn't have instruction trace enabled.

\ **Internal Events**: It should be noted that it is not possible to view Instruction Timing
information for internal events such as Clear().

\ **Navigation**

The Instruction Timing for an event can be accessed by right clicking on that event and choosing
the "View In Instruction Timing" option. Since it is common to use the same shader in multiple
events, RGP provides an easy way to toggle between multiple events that use the same shader using
the event drop down shown below.

.. image:: media_rgp/RGP_Instruction_Timing_2.png

This allows the developer to study the behavior of the shader for different events. It is
recommended to use the keyboard shortcuts, (Shift + Up and Shift + Down) to change API PSO
selection and (Shift + Left and Shift + Right) to move across different events using the same
shader.

\ **Navigation of Raytracing events**

For certain Raytracing events, an additional **Export name** drop down will be available. Whether
or not this drop down is shown depends on the compilation mode chosen by the AMD driver and compiler
for the selected event. There are two possible compilation modes: **Unified** and **Indirect**. The
compilation mode chosen for a particular event will be evident in the event name: events which use
the Unified mode will have a **<Unified>** suffix, while events which use the Indirect mode will have
an **<Indirect>** suffix. In the case of DirectX Raytracing, the full event names are
**DispatchRays<Unified>** and **DispatchRays<Indirect>**. The main difference between these two
compilation modes has to do with how the individual shaders in the raytracing pipeline are compiled.
In Unified mode, the individual shaders are inlined into a single shader, resulting in a single set
of ISA. In Indirect mode, the individual shaders are compiled separately, and the functions in each
shader end up as their own set of ISA instructions. Function call instructions are generated in the
ISA to allow one function to call another.

The way the ISA code is presented in the Instruction timing UI follows the way the driver and compiler
handle the shaders. For Unified mode, there is a single stream of ISA and the Instruction timing view
treats it as a single shader. For Indirect mode, there are multiple streams of instructions, one for
each shader in the raytracing pipeline. The instruction streams and their associated costs are displayed
per-shader and appear one after the other in the Instruction timing view. Only shader functions with
non-zero cost are displayed in the Instruction timing view. Shaders with zero cost can still be viewed
in the Pipeline state pane.

To help with navigation among the various shader functions, the **Export name** drop down is available
for any events that use the indirect compilation mode. This drop down allows the developer to toggle
between the multiple shaders. The drop down contains the list of exports along with their Instruction
cost. The exports will be sorted by the Instruction cost. Ctrl + Shift + Up and Ctrl + Shift + Down
can be used to move among the list of Export names. This **Export name** drop down is shown below.

.. image:: media_rgp/RGP_Instruction_Timing_Exports.png

Display of line numbers can be toggled using (Ctrl + Shift + L) and lines can be navigated to
directly using the (Ctrl + G) shortcut

\ **Search and Go to Line**

Individual instructions can be searched for and the developer can navigate directly to a specific
line using the controls displayed below.

.. image:: media_rgp/RGP_Instruction_Timing_Find.png

\ **Instruction Timing Side Panel**

The Instruction Timing side panel provides additional information about the shader shown.

.. image:: media_rgp/RGP_Instruction_Side_Panel.png

The main sections in the side panel are:

\ **Identifiers**: This section includes multiple hashes that can be used to identify the shaders
used and the pipeline that they are a part of.

\ **Hardware Utilization**: The Hardware Utilization bar charts show the utilization of each
functional unit of the GPU on a per-shader basis.

It should be noted that utilization shown is only for the shader being viewed. For example, in the
image shown, the VALU utilization of the shader is 55.3%. This means that the Compute Shader shown
used 55.3% of the VALU capacity of the GPU. Other shaders may be concurrently executing on the GPU.
Their usage of the VALU is not considered when showing the bar charts.

A functional unit's utilization is calculated as follows:

*Utilization % = 100 * (Hit Count of all instructions executed on the functional unit) / (Duration
of analyzed wavefronts)*

\ **Instruction Types**: This section provides information about the dynamic instruction mix of the
shader's execution. The columns denote the different types of instructions supported by RDNA and GCN.
The counts denote the number of instructions of each category.

Each category's count denote the instruction count for that shader's invocation in the event.
Different executions of the same shader could have different Instruction statistics based on
factors such as the number of wavefronts launched for the shader and loop parameters. The
instruction categories are briefly described below. Please see the Shader Programming Guides for
more details.

- VALU: Includes vector ALU instructions

- SALU: Includes scalar ALU instructions

- VMEM: Includes vector memory and flat memory instructions

- SMEM: Includes scalar memory instructions

- LDS: Includes Local Data Share instructions

- IMMEDIATE: Includes the immediate instructions such as s_nop and s_waitcnt.

- EXPORT: Includes export instructions

- MISC: Includes other miscellaneous instructions such as s_endpgm

- RAYTRACE: Includes the BVH instructions used during raytracing.

The instruction types table provides a useful summary of the shader's structure especially for very
long shaders.

\ **Shader Statistics**: The shader statistics section provides useful information about the shader

- Shader Duration: This denotes the execution duration of the whole shader. It can be correlated
  with the timings seen for the same shader in other RGP views such as the Wavefront Occupancy and
  the Event Timing views.

- Wavefronts: This denotes the total number of wavefronts in the shader and the number of
  wavefronts analyzed as part of building the Instruction Trace visualizations. It is expected that
  not all waves in the shader will be analyzed. This is for the same reasons described above when
  discussing the availability of Instruction Timing.

- Branches: This denotes the number of branch instructions in the shader and the percentage of
  the total number of branches that were taken by the shader.

- Theoretical Occupancy: From the register information and knowledge about the GPU architecture we
  can calculate the theoretical maximum wavefront occupancy for the shader.

- Vector and Scalar Registers: The register values indicate the number of registers that the shader
  is using. The value in parentheses is the number of registers that have been allocated for the
  shader.

- Local Data Share Size: This value indicates how many bytes of local data share are used by the
  shader. This is only displayed for Compute Shaders.

\ **Instruction Timing for RNDA**

On RDNA GPUs, Instruction Timing can include certain instructions with a hit count of 0. Usually
this will be an instruction called *s_code_end* and may also be present after the shader's
*s_endpgm* instruction. This is expected since this is an instruction added by the compiler to
allow for instruction prefetching or for padding purposes. The hardware does not execute this
instruction.

Such instructions may also be present in the ISA view in the Pipeline state pane.

\ **Note**

Instruction timing data is currently unavailable on OpenCL
