*******
Generel
*******

.. contents:: Table of Contents


Bpm
---

Set the bpm rate of the song you want to edit your videos to. Each time
the value is changed a new sliceArray and a new markerArray is created
with slices and markers from 0 to the duration of the active
composition. If no composition is selected slices and markers will be
created from 0 to 60 seconds.

Bars
----

Set bars in order to determine how many markers are created when
creating markers. Each time the value is changed a new sliceArray and a
new markerArray is created with slices and markers from 0 to the
duration of the active composition. If no composition is selected slices
and markers will be created from 0 to 60 seconds.

Select Workarea
---------------

Select the workarea to which all actions of this script are applied.

-  **Comp Workarea:** The workarea is the workarea of the active
   composition.
-  **Layer in/out:** The workareas in and out points are the in and out
   points of the selected layer. If multiple layers are selected, the
   lowest in point and the highest out point of all layers are
   considered.
-  **Comp Duration:** The workarea starts at 0 and ends with the
   duration of the active composition.

Tools for selected Layer/s
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

move back
---------

Moves the selected layer according to the bpm and bars value to the
left.

move forth
---------

Moves the selected layer according to the bpm and bars value to the
right.

Arrange Layer/s
---------------

All selected layers are getting arranged like a stairway according to
the currently set bpm and bars value.

Randomize Selection
-------------------

All selected layers are getting randomly deselected.

Foist
-----

For all selected layers:

1. The function tries to find a new randomly choosen starttime for the
   layer
   ⋅⋅⋅\ ``layer.startTime += (Math.random() < 0.5) ? Math.random() * 100 : Math.random() * -100;``\ ⋅⋅
2. The function tries to find a new randomly choosen stretch value for
   the layer
   ⋅⋅⋅\ ``layer.stretch = 200 * Math.random() or layer.stretch = 200 * Math.random() * (-1)``

If the original in- and out-point of the layer have changed by setting
the randomly choosen values
``(origInPoint != layer.inPoint && origOutPoint != layer.outPoint)``,
the function tries to find another starttime/stretch value for the layer
and loops through this process as long as the condition is not true.



Load Txt
--------

Load a txt file that contains midi note on and off information and
import them as slices into the sliceArray (The in points of the slices
are getting added to the markerArray which could be added as markers to
a layer or the composition by clicking the ‚Add‘ button).

Save Txt
--------

Save a txt file that contains all slices from the sliceArray.



Preview
-------

When the script launches, the display update function is turned off.

   Option+Click (Win Alt+Click): An scheduled update function for the
   display is toggled on (or off).

If the update function is running the preview area is updated each
second with means by an scheduled task from after effects.

This only works if the script runs as a panel (If the script is launched
as a window the update function doesn‘t work).

   Option+Shift+Click (Win Alt+Shift+Click): All scheduled tasks that
   are running are getting closed.


