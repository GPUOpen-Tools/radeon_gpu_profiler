Frame summary (DX12 and Vulkan)
-------------------------------

This window describes the structure of a profile from a number of
different perspectives.

.. image:: media_rgp/RGP_FrameSummary_1.png

The System activity section displays a system-level view of sync
operations and when command buffers were submitted to the GPU. Speaking
in general terms, all profiles contain two types of data: command buffer
timing data and SQTT timing data. This pane displays the former, and the
rest of RGP displays the latter.

Along the top, we find a series of controls:

-  **GPU and CPU based frames:** Controls how to display frame
   boundaries, which are also bracketed by black markers. The difference
   in time between both modes can help to visualize latency between
   workload submission and execution. The driver provides each command
   buffer with a frame number, a CPU submit timestamp, a GPU start
   timestamp, and a GPU end timestamp.

   -  **GPU-based frames:** Interprets frame boundaries to begin when
      a present finished on the GPU.

   -  **CPU-based frames:** Interprets frame boundaries to begin when
      a present was submitted on the CPU.

-  **Workload views:** Provide twelve different ways to view the same data:

   -  **Command buffers:** Shows a list of all command buffers in a
      submission. Disabling this will condense all command buffers into
      a single submission block which also specifies the number of
      contained command buffers.

   -  **Sync objects**: Toggles whether to display signals and waits.

   -  **Sequential**: An alternate view which shows data linearly as
      opposed to stacked. The dark right-most portion of command buffers
      and submits indicates execution time on the GPU.

   -  **GPU only**: A flat view of the data which represents solely GPU
      work. This helps visualize parallelism among all GPU queues.

-  **CPU submission markers:** Draw vertical lines to help visualize
   when the CPU issued certain types of workloads to the GPU.

-  **Zoom controls:** Consistent with the rest of the tool, these allow
   users to drill down into points of interest. More information can be
   found under the :ref:`Zoom Controls<zoom_controls>` section.

In the middle, we find the actual view. Each queue (Graphics,
Compute, Copy) gets its own section. The alternating grey and white
backgrounds indicate frame boundaries. The blue region indicates
which command buffers were profiled with SQTT data, for more detailed
event analysis in other sections of the tool. Note that command
buffers are visualized using two shades of the same color. The
lighter shade represents time spent prior to reaching the GPU, and
the darker shade represents actual execution.

Please note that the view is interactive, making it possible for users to
select and highlight command buffers, sync objects, and submission
points.

Users can correlate between command buffer timing data and SQTT data by
right-clicking on a command buffer within the "Detailed GPU events" region.
This will bring up a context menu which contains three menu items for
finding the first event within the selected command buffer. Selecting one
of the menu items will navigate to the appropriate pane and set focus on
the specified event.

Along the bottom, we find information about user selections:

-  **Submit time:** Specifies when work was issued by the CPU

-  **Submit duration:** Specifies the full duration of the submit

-  **Enqueue duration:** Specifies how long the work was queued before
   beginning on the GPU

-  **GPU duration:** Specifies how long the GPU took to execute it.

Below the queue timings view we find the following summary:

.. image:: media_rgp/RGP_FrameSummary_2.png
..

This shows an interpretation of queue timings data to determine which
processor is the bottleneck. By default, if the GPU is idle more than
5% of the time then the profile is considered to be CPU-bound. This
percentage may be adjusted in RGP settings.

Please note that the values displayed for **Frame duration** and
**Frame rate** are sourced from SQTT data. In other words, they are
based on duration and shader clock frequency used in other RGP panes
such as Wavefront occupancy.

The **Profiling overhead** shows the amount of profiling data that was
written to video memory by the hardware while gathering the RGP profile.
The profiling overhead is also expressed in terms of memory bandwidth used
to write the data. The profiling overhead is comprised of the SQTT data
collected while profiling.

The **Queue submissions** and **Command buffers** pie charts show the
number of queue submissions and command buffers in the frame broken down
by the Direct and Compute queues. Compute submissions are colored in yellow
and graphics submissions are colored in light blue. The **Sync Primitives**
section counts how many unique signal and wait objects were detected
throughout the profile. Please note that only signals and waits from queue
operations are included in the profile data. For instance, any Vulkan
signals originating from vkAcquireNextImageKHR will not appear since that is
not a queue operation.

.. image:: media_rgp/RGP_FrameSummary_3.png
..

The **Event statistics** pie chart and table show the event counts
colored by type. In the above example there are 281 Dispatch and
1,633 DrawIndexedInstanced events. The **Instanced primitives**
histogram shows the number of events that drew N (1 to 16+)
instances. In the example above we see that most events drew just a
single instance, whereas a lesser number of events drew 2-9 and 16
instances.

.. image:: media_rgp/RGP_FrameSummary_4.png
..

**Geometry breakdown** gives a summary of the vertices,
shaded primitives, shaded pixels, and instanced primitives. In the
above example we can see that the GS is being used to expand the
number of shaded primitives. Also, looking at the **Rendered
Primitives** histogram we can see that one draw uses between 0 and 1K
primitives, and the other draw call uses 11k or more primitives. This
makes sense given that the profile is from the D3D12nBodyGravity SDK
sample.