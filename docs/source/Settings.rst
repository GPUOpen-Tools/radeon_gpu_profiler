General
-------
**Units:** This tells the profiler whether to work in clocks, nanoseconds, microseconds,
or milliseconds. Refer to the keyboard binding in the secion below to quickly
toggle between these time units.

**State buckets:** Specify how the profiler should generate its own state buckets.
This can be based off a combination of shader base address, depth buffer address,
render target address and API PSO hash.

**Sync event time windows:** Keep the Wavefront Occupancy and Event Timing
panes in sync while browsing through different time ranges.

**Processor boundness:** Specific to the Frame Summary and Profile Summary, this value will tell
RGP at which point to consider an application as being GPU bound or CPU bound.

**Wavefront occupancy detail:** Increase the visual quality of wavefronts in
the Wavefront Occupancy pane. This allows users to see a more accurate
representation of GPU occupancy at the expense of some profiler performance.


Themes and colors
-----------------
The profiler makes heavy use of coloring to display its information.
This pane allows users to thoroughly customize those colors.

.. image:: media_rgp/RGP_ThemesAndColors_Settings.png

Keyboard shortcuts
------------------

Here users will find the **Keyboard shortcuts** pane:

.. image:: media_rgp/RGP_KeyboardShortcuts_Settings.png

The **System activity, Wavefront occupancy and Event timing** shortcuts
are specific to zooming and panning operations that can be performed
within the Frame Summary and Events subtabs.  See the section entitled
:ref:`Zoom Controls <zoom_controls>` for more information.

.. image:: media_rgp/RGP_Tabs_1.png

.. image:: media_rgp/RGP_Tabs_2.png

The **Event timeline** section refers to panning and event selection
operations for the bottom graph within the Wavefront occupancy view.

The **Instruction timing** section refers to keystrokes to change
API PSO and event selection, toggle line numbers, and jump
to a specific instruction

The **Global navigation** section refers to keystrokes that aid user
navigation, and are always detected regardless of which pane is visible.

The **Global hotkeys** section refers to any hotkeys available anywhere
in the product. Pressing *CTRL* + *T* allows the user to quickly cycle
through the different time units (cycles, milliseconds, microseconds
or nanoseconds) from any pane, rather than having to go to the settings.
The user can also open or close a profile from any pane using the
Global hotkeys.

We encourage all users to adopt these keystrokes while using RGP.

UI Navigation
-------------

In an effort to improve workflow, RGP supports keyboard shortcuts and
back and forward history to quickly navigate throughout the UI.

Back and forward navigation
~~~~~~~~~~~~~~~~~~~~~~~~~~~

RGP tracks navigation history, which allows users to navigate back and
forward between all of RGP’s panes. This is achieved using global
navigation **hotkeys** shown above, or the back and forward **buttons**
shown below:

.. image:: media_rgp/RGP_Navigation.png

Currently, back and forward navigation is restricted to pane switches
and moving between events within a pane, but further releases may
support navigation history of more detailed user actions within panes.
