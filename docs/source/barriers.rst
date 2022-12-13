
Barriers
--------

The developer is now responsible for the use of barriers in their
application to control when resources are ready for use in specific
parts of the frame. Poor usage of barriers can lead to poor performance
but the effects on the frame are not easily visible to the developer -
until now. The Barriers UI gives the developer a list of barriers in use
on the graphics queue, including the additional barriers inserted by the
driver.

Note that in older profiles or if the barrier origin isn't known, all
barriers and layout transitions will be shown as 'N/A'. Using an up-to-date
display driver will ensure that this information is available.

.. image:: media_rgp/rgp_barriers_1.png

The summary at the top left of the UI quickly lets
the developer know if there is an issue with barrier usage in the frame.
When calculating the percentage, only portions of a barrier's duration
which are not overlapped by one or more events from any queue are taken
into consideration. For instance, if a barrier has a duration of 100 ns,
but 80 ns of that barrier's duration are overlapped by other events (on
the same queue or on a different queue), then only 20 ns of that
particular barrier contributes to the percentage calculation.
In the case shown above, the barrier usage is taking up 0% of the frame.

This summary also displays the average number of barriers
per draw or dispatch and the average number of
events per barrier issue.

The table shows the following information:

#. **Event Numbers** - ID of the barrier - selecting an event in this
   UI will select it on the other Events windows

#. **Duration** - Lifetime of the barrier

#. **Drain time** - This is the amount of time the barrier spends waiting
   for the pipeline to drain, or work to finish. Once the pipeline is empty,
   new wavefronts can be dispatched

#. **Stalls** - The type of stalls associated with the barrier - where
   in the graphics pipe we need the work to drain from

#. **Layout transitions** - A blue check box indicates if the barrier is
   associated with a layout transition. There are six columns indicating the
   type of layout transition. These are described in the Layout transition
   section below.

#. **Invalidated** - A list of invalidated caches

#. **Flushed** - A list of flushed caches

#. **Barrier type** - Whether the barrier originated from the application
   or from the driver (or 'N/A' if unknown)

#. **Reason for barrier** - In the case of driver-inserted barriers, a brief
   description of why this barrier was inserted

   The rows in the table can be sorted by clicking on a column header.

   **NOTE**: Selecting a barrier in this list will select the same event
   in the other Event windows.

   The user can also right-click on any of the rows and navigate to
   the Wavefront occupancy, Event timing, Instruction timing or Pipeline
   state panes and view the event represented by the selected row in these
   panes, as well as in the side panels. The user can also see the parent
   command buffer in the Frame summary pane or navigate to the Render/depth
   targets view and view the event in the timeline.

   Below is a screenshot of what the right-click context menu looks like:

.. image:: media_rgp/rgp_barriers_2.png

Layout Transitions
~~~~~~~~~~~~~~~~~~

The following Layout Transition columns are shown in the Barriers table:

#. **Depth/Stencil Decompress**: This barrier is emitted when a depth/stencil
   surface is decompressed. Depth/stencil surfaces are often stored compressed
   to reduce bandwidth to and from the color and depth hardware units.
#. **HiZ Range Resummarize**: This barrier is emitted when a depth/stencil buffer,
   which has corresponding hierarchical Z-buffer data, is modified. This barrier
   ensures that the modified data is reflected into the hiZ-buffer, allowing for
   correct culling and depth testing.
#. **DCC Decompress**: This barrier is emitted when `Delta Color Compression` compressed
   color data needs to be decompressed.
#. **FMask Decompress**: This barrier is emitted when FMask data is decompressed.
   FMask is used to compress MSAA surfaces. These surfaces must be decompressed
   before they can be read by texture hardware units.
#. **Fast Clear Eliminate**: This barrier is emitted when the driver performs a fast clear.
   For fast clears, a barrier is needed to read the clear color before filling the
   render target. Clearing to specific values (typically 0.0 or 1.0) may allow the GPU to
   skip the eliminate operation.
#. **Init Mask RAM**: This barrier is emitted when the driver uses a shader to initialize
   memory used for compression.

See `https://gpuopen.com/dcc-overview/ <https://gpuopen.com/dcc-overview/>`_ for more information
on what may cause a **DCC Decompress** or what "clear" values can be used to skip **Fast Clear Eliminates**.

Barriers and OpenCL/HIP
~~~~~~~~~~~~~~~~~~~~~~~

Barriers for OpenCL or HIP profiles provide visibility into how the driver scheduled
dispatches to the GPU and dependencies between kernel dispatches. These barriers
are the same synchronization primitives used by DirectX12 and Vulkan that are described above.

The barriers shown in an OpenCL or HIP profile correspond to the barriers
inserted by the OpenCL or HIP driver for one of the following reasons.

#. **Data Dependencies** - There are data dependencies between subsequent dispatches. For
   example, reading the results of a previous kernel dispatch. This causes barriers to be inserted
   so that caches can be invalidated.

#. **Queue Profiling** - (OpenCL-specific) The application has enabled profiling CL_QUEUE_PROFILING_ENABLE
   property when creating a command queue. This causes barriers to be inserted so that timestamps can be
   recorded.

OpenCL command queues process dispatches one after another and it is common for a
subsequent kernel dispatch to use the results of a previous kernel dispatch. For this reason, it
can be expected that an RGP profile will have a large number of barriers.

A typical OpenCL profile's barriers are shown below.

.. image:: media_rgp/rgp_barriers_opencl_1.png

As we see, the time taken due to barriers is typically very small since inter-dispatch dependencies only cause cache invalidations.

.. image:: media_rgp/rgp_barriers_opencl_2.png


It should be noted that the meaning of barriers in RGP for OpenCL/HIP is different from
OpenCL or HIP built-in synchronization APIs. For example, barriers that appear in an
OpenCL RGP profile are not related to the OpenCL synchronization APIs based on cl_event
or cl_barrier. For this reason, the barriers seen in OpenCL/HIP profiles are displayed
as **CmdBarrier()** which is not a part of the OpenCL or HIP API. For these profiles,
RGP does not currently show API-specific events or host synchronization.
