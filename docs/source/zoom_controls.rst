.. _zoom_controls:

Zoom Controls
=============

Time based graphs in RGP provide Zoom controls for adjusting the time scale that is
viewable on screen. The following set of zoom icons are displayed above each graph that
supports zooming:

.. |ZoomSelectionRef| image:: media_rgp/rgp_zoom_to_selection.png
.. |ZoomResetRef| image:: media_rgp/rgp_zoom_reset.png
.. |ZoomInRef| image:: media_rgp/rgp_zoom_in.png
.. |ZoomOutRef| image:: media_rgp/rgp_zoom_out.png

|ZoomSelectionRef| Zoom to selection
------------------------------------
When **Zoom to selection** is clicked, the zoom level is increased to a selected
region or selected event. A selection region is set by holding down the
left mouse button while the mouse is on the graph and dragging the mouse
either left or right. A colored overlay will highlight the selected region
on the graph. For graphs that support it, an event may be selected by
clicking on it with the mouse (either the left or right button).
**Zoom to selection** can also be activated by right clicking on a selection on the
graph and choosing the **Zoom to selection** context menu option. Zooming
to a selected event can be accomplished by simply double clicking the event.
Pressing the **Z** shortcut key while holding down the **CTRL** key activates
**Zoom to selection** as well.

|ZoomResetRef| Zoom reset
-------------------------
When **Zoom reset** is clicked, the zoom level is returned to the original level
to reveal the entire time span on the graph. The zoom level can also be reset
using the **H** shortcut key.

|ZoomInRef| Zoom in
-------------------
Increases the zoom level incrementally to display a shorter time span on the
graph. The zoom level is increased each time this icon is clicked until the
maximum zoom level is reached. Alternatively, holding down the **CTRL** key
and scrolling the mouse wheel up while the mouse pointer is over the graph
will also zoom in for a more detailed view. Zooming in can be activated with
the **A** shortcut key. To zoom in quickly at a 10x rate, press the **S**
shortcut key.

|ZoomOutRef| Zoom out
---------------------
Decreases the zoom level incrementally to display a longer time span on the
graph. The zoom level is decreased each time this icon is clicked until the
minimum zoom level is reached (i.e. the full available time region).
Alternatively, holding down the **CTRL** key and scrolling the mouse wheel down
while the mouse pointer is over the graph will also zoom out for more detailed
view. Zooming out can be activated with the **Z** shortcut key. To zoom out
quickly at a 10x rate, press the **X** shortcut key.

Zoom Panning
------------

When zoomed in on a graph region, the view can be shifted left or right by using
the horizontal scroll bar. The view can also be scrolled by dragging the mouse
left or right while holding down the **spacebar** and the left mouse button.
Left and right arrow keys can be used to scroll as well.

.. _zoom_synchronization:

Synchronized Zoom
-----------------

Normally, adjusting the view of a time based graph (by zooming in and
scrolling) doesn’t affect graphs on other panes. This can be useful in
some cases when tracking more than one item. However, it is sometimes
useful to lock both the event timing and wavefront occupancy views to
the same visible time window. There is an option to control this in the
‘General’ tab of the Settings section called **Sync event time windows**.
With this enabled, any zooming and scrolling in one window will be reflected
in the other. If adjustments are made in the wavefront occupancy view, the
vertical scroll bar in the event timing view will be automatically adjusted
so that there are always events shown on screen if an event isn’t manually
selected.