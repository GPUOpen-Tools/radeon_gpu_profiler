Wavefront occupancy
-------------------

This section presents users with an interactive timeline that shows GPU
utilization and all events in the profile.

.. image:: media_rgp/RGP_WavefrontOccupancy_1.png

There are three components, the Wavefront timeline view, the Events
timeline view, and the Details panel.

\ **Wavefront timeline view**

This section shows how many wavefronts were in flight. All wavefronts
are grouped into buckets which are represented by vertical bars. The top
half shows wavefronts on the graphics queue, and the bottom half shows
wavefronts on the async compute queue.

.. image:: media_rgp/RGP_WavefrontOccupancy_2.png

Users may examine regions by selecting ranges within the graph and using
the zoom buttons on the top right. Users may also hover over this view
and use mouse wheel to zoom and center in on a particular spot. A region
of wavefronts can be selected by using either mouse button to drag over
the desired region as shown below.

.. image:: media_rgp/RGP_WavefrontOccupancy_3.png

You can zoom into the region by selecting Ctrl + Z, or by clicking on
“Zoom to selection” (result shown below).

.. image:: media_rgp/RGP_WavefrontOccupancy_4.png

You can also drag the graph if you are zoomed in. Hold down the space
bar first, then hold the mouse button down. The graph will now move with
the mouse.

Users may use the combo-box on the top left to visualize wavefronts in
different ways:

-  **Color by API stage.** Default, and shows which wavefronts
   correspond to which Vulkan/DX12 pipeline stage.

-  **Color by GCN stage.** Shows which wavefronts correspond to which
   GCN pipeline stage.

-  **Color by hardware context.** Shows which GCN context (0-7) the
   wavefronts ran on. This can be useful to visualize the amount of
   context rolls that occurred.

-  **Color by shader engine.** Shows which shader engine the wavefronts
   ran on.

-  **Color by event.** Shows which wavefronts correspond to which event
   of the profile. Each event is assigned a unique color.

-  **Color by pass.** Groups wavefronts into different passes depending
   on which render target or attachment type (color, depth-only,
   compute). These three types are assigned a base color, and each pass
   within each type is assigned a different shade of the base color.
   This can be useful to visualize when the application attempted to
   render different portions of a scene.

-  **Color by API PSO** will color events by their API PSO hash values.

-  **Color by instruction timing** will only colorize events which contain
   detailed instruction timing information. All other events will be grayed
   out.

Additionally, there are filters along the top intended to help visualize
the occupancy of only certain GCN pipeline stages. Lastly, there are
colored legends on the bottom which serve as color reminders. Note these
colors can be customized within Settings.

The RGP wavefront occupancy for OpenCL has only compute in the wavefront occupancy.
This is because compute APIs such as OpenCL only dispatch compute shader waves.
For this same reason, a number of the coloring options  such as hardware context
and GCN stages are not applicable for OpenCL.

.. image:: media_rgp/RGP_WavefrontOccupancy_OpenCL_1.png

\ **Events timeline view**

This section shows all events in your profile. This includes both
application-issued and driver-issued submissions. Each event can consist
of one or more active shader stages and these are shown with rectangular
blocks. The longer the block, the longer the shader took to execute. If
there is more than 1 shader active, then each shader stage is connected
with a thin line to indicate they belong to the same event. This view
just shows actual shader work; it doesn't show when the event was
submitted.

.. image:: media_rgp/RGP_WavefrontOccupancy_5.png

Users may single-click on individual events to see detailed information
on the details pane described below. Zooming into this graph is done by
selecting the desired region in the wavefront graph above. Additionally,
zooming in on a single event can be done by selecting the event and
clicking on ‘Zoom to selection’.

Users may use the combo-box on the top left to visualize events in
different ways:

-  **Color by queue.** Default, and shows which events were submitted to
   graphics or async compute queues. In addition, the CP marker is shown
   in a unique color, as well as the barriers and layout transitions so
   they can be easily distinguished. Note that barrier and layout transitions
   originating from the driver are colored differently to those from the
   application, and this is shown in the legend below the timeline view.

-  **Color by hardware context.** Shows which events ran on which
   context. This can be useful to visualize the amount of context rolls
   that occurred.

-  **Color by event.** Will show each event in a unique color.

-  **Color by pass.** Groups events into different passes depending on
   which render target or attachment type (color, depth-only, compute).
   These three types are assigned a base color, and each pass within
   each type is assigned a different shade of the base color. This can
   be useful to visualize when the application attempted render
   different portions of a scene.

-  **Color by command buffer.** Shows each event in a color associated
   with its command buffer, so making it easy to see events are in the same
   command buffer.

-  **Color by user events.** Will colorize each event depending on which
   user event it is surrounded by.

Additionally, there are also filters to help visualize only certain
types of events. For example, users can select to see draws, dispatches,
barriers, clears, copies, resolves user markers and events containing
instruction trace data. There is also an option to switch the CP marker
on or off. Switching the CP marker off will just show the active shader
blocks.

The event duration percentile filter allows users to only see events
whose durations fall within a certain percentile. For example, selecting
the rightmost-region of the slider will highlight the most expensive
events. One will also find a textbox to filter out by event name.

In the case that user events are available, they will be drawn above
all other events. The user events are stacked according to the nesting
level, and a cross pattern indicates multiple overlapping user event
regions. Moving the mouse cursor over one of the user events will show a
tool-tip listing all user events under the cursor including timing
information for each user event interval.

.. image:: media_rgp/RGP_WavefrontOccupancy_7.png

The same zooming and dragging that is available on the wavefront
timeline view is also available here.

Lastly, there are colored legends on the bottom which serve as color
reminders. Note these colors can be customized within Settings.


\ **Details pane**

Pressing \ **Show Details** on the top right will open a side panel with
more in-depth information. The contents of this panel will change,
depending on what the user last selected. If a single event was selected
in the Events timeline the details panel will look like below:

.. image:: media_rgp/RGP_DetailsPanel_1.png

The Details panel for a single event contains the following data:

*  The event’s API call name

*  The queue it was launched on

*  User event hierarchy (if present)

*  Start, End, and Duration timings

*  Hardware context and if it was rolled

*  List of GCN hardware stages and wavefront counts

*  Colored bar showing wavefront distribution per GCN hardware stage

*  Total wavefront count

*  Total threads

*  GCN shader timeline graphic showing active stages and duration

*  A table showing resource usage for each API shader stage:

   * The VGPR and SGPR columns refer to the vector and scalar general
     purpose registers being used, and the number of registers that have
     been allocated shown in parentheses.

   * The LDS column refers to the amount of Local Data Store that each
     shader stage is using, reported in bytes.

   * The Occupancy column refers to the Theoretical wavefront occupancy
     for the shader. This is reported 'A / B', where A is the number of
     wavefronts that can be run and 'B' is the maximum number of wavefronts
     supported by the hardware.

   * Tooltips explaining the data are available by hovering the mouse over
     the table header.

*  Block diagram of active pipeline stages

*  Primitive, vertex, control point, and pixel counts

The ‘Duration’ shows the time from the start of the first shader to the
end of the last shader, including any space between shaders where no
actual work is done (denoted by a line connecting the shader ‘blocks’).
The ‘Work duration’ only shows the time when the shaders are actually
doing work. This is the sum of all the shader blocks, ignoring the
connecting lines where no work is being done. If there is overlap
between shaders, the overlap time is only accounted for once. If all
shaders are overlapping, then the duration will be the same as the work
duration.

If the user selects a range of wavefronts in the wavefront timeline the
details panel contains a summary of all the wavefronts in the selected
region as shown below:

.. image:: media_rgp/RGP_DetailsPanel_2.png

If the user selects a barrier, the details panel will show information
relating to the barrier, such as the barrier flags and any layout
transitions associated with this barrier. It will also show the barrier
type (whether it came from the application or the driver). Note that the
barrier type is dependent on whether the video driver has support for
this feature. If not, then it will be indicated as 'N/A'. An example of
a user-inserted barrier is shown below:

.. image:: media_rgp/RGP_DetailsPanel_3.png

If the driver needed to insert a barrier, a detailed reason why this barrier
was inserted is also displayed, as shown below:

.. image:: media_rgp/RGP_DetailsPanel_5.png

If the user selects a layout transition, the details panel will show
information relating to the layout transition as shown below:

.. image:: media_rgp/RGP_DetailsPanel_4.png

The user can also right-click on any of the events in the Events
timeline view and navigate to Event timing or Pipeline state panes, as
well as Barriers, Most expensive events and Context rolls panes within
Overview tab, and view the selected event in these panes, as well as in
the side panels.

In addition, the user can zoom into an event using the “Zoom to
selection” option from this context menu.

Below is a screenshot of what the right-click context menu looks like.

.. image:: media_rgp/RGP_WavefrontOccupancy_6.png
