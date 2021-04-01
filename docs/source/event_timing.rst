
Event timing
------------

The event timing window shows a list of events and their corresponding
timings. The tree view in the left-hand column shows each event name and
its unique index, starting at 0, and are listed in sequential order.
Events can be ordered into groups, and group categories are shown in
bold text.

.. image:: media_rgp/rgp_event_timing_1.png

The pane to the right of the tree view shows a graphical representation
of the duration for each event. The darker blue span to the right of
each tree node shows the duration of all the events in that node.

In the graphic for each event (shown in light blue above) the first
small block at the left is the CP marker, indicating when the event was
issued. This is followed, some time later, by actual work done by the
shaders. The delay between the CP marker and the start of actual work
may indicate bottlenecks in the application. One of the shaders may be
waiting for a resource which is currently being used by another wave in
flight and cannot start until it obtains that resource. The time when
the first shader started work and the last shader finished work is the
number indicated in this column. Each shader stage is represented by a
rectangular block. The longer the block, the longer the shader took to
execute. Shaders are linked by a solid line to show that they are
connected in the pipeline. For groups, a dark line spans all events
within the group, showing the time taken for that group to complete
work.

Zoom settings on this pane are similar to the Wavefront occupancy pane.
More information can be found under the :ref:`Zoom Controls<zoom_controls>`
section.

\ **Grouping modes**

The events can be grouped together. Normally these groups don't affect
the event ordering but sometimes can (sort by state bucket).

-  **Group by pass** will show events depending on the render
   target or attachment type (color, depth-only, compute, raytrace).

-  **Group by hardware context** will group events by their hardware
   context, making it easy to see which events caused the context to
   change.

-  **Group by state bucket** **(unsorted)** will order the events by
   state bucket but won't sort the state buckets by duration.
   Theoretically, all events in a state bucket use the same shaders. The
   duration of a state bucket is represented by the dark blue line
   corresponding to the state bucket group text.

-  **Group by state bucket** **(serialized)** will take all the event
   timings within the group and sum the total time that the shaders were
   busy, ignoring all empty space between events. This has the effect of
   serializing the shader work and doesn't take into account that some
   shaders will be executing in parallel. This is used to highlight when
   you have a lot of small shaders whose cumulative work can be
   extensive. As an example, if you have 2 shaders which start at the
   same time and one takes 2000 clks and another takes 10000 clks, the
   total duration would be 12000 clks.

-  **Group by state bucket (overlapped)** takes into account the
   parallelism of the shader execution so will highlight shaders which
   take a long time to execute. Using the same example above, since both
   shaders start together, the total duration in this case would be
   10000 clks.

-  **Group by command buffer** will group events depending on which
   command buffer they are on.

-  **Group by user events** will group the events depending on which
   user event(s) they are surrounded by.

-  **Group by PSO** will group events by their API PSO hash values.

The default grouping mode is by user event if user events are present in
the profile. Otherwise the default will be to group by pass.

Note that grouping by hardware context or command buffer will group
events by queue first. Grouping by pass or user event will
chronologically group events irrespective of which queue they originated
from. Grouping by state bucket just shows events in the graphics queue.
Grouping by hardware context is shown below:

.. image:: media_rgp/rgp_event_timing_2.png

**Color modes**

The events can be rendered using different color schemes in the same manner
as in the Wavefront occupancy view.

The user can also right-click on any of the events and navigate to
Wavefront occupancy or Pipeline state panes, as well as Barriers, Most
expensive events and Context rolls panes within Overview tab, and view
the selected event in these panes, as well as in the side panels.

**Wavefront occupancy and event timing window synchronization**

Zooming of the time scale and horizontal panning of the Wavefront occupancy
view and Event timing view can be synchronized or adjusted independently. More
information on synchronization can be found under the
:ref:`Zoom Synchronization heading <zoom_synchronization>`

The anatomy of an event
-----------------------
Two examples of typical draw call events are shown below:

.. image:: media_rgp/rgp_event_1.png
.. image:: media_rgp/rgp_event_2.png

**A** shows the CP marker. This is the point the command processor in the
GPU issues work to be done. It is then queued up until the GPU can process
the workload.

**B** shows the work being done by the various shader stages. The gap between
the CP marker and the start of **B** indicates that the GPU didn't start on
the workload straight away and was busy doing other things, for example, previous
draw calls.

**C** shows any fixed-function work that needs doing after the shaders have
finished executing. This occurs when a draw call is doing depth-only rendering.
The fixed function work shown is the primitive assembly and scan conversion
of the vertices shaded by the vertex shader.

Users may also obtain information about an event's parent command buffer
by right-clicking on an event. This will bring up a context menu which
contains a menu item to find the event's parent command buffer. Selecting
this menu item will navigate to the Frame Summary and set focus on the selected
event's parent command buffer. Once here, users can obtain valuable system-level
insight about the surrounding context for the event in question.

Compute dispatches for both graphics APIs and OpenCL have a simpler structure.
A sample compute event is shown below.

.. image:: media_rgp/rgp_compute_event.png

In a compute event, only compute shader waves are launched.
Also, compute dispatches do not have any fixed function work after the shader
work is finished.
