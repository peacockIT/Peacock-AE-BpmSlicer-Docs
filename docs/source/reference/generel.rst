=======
Generel
=======

.. contents:: Table of Contents

?
~

Here you can find a short description for all functions of this
extension.

Bpm
~~~

Set the bpm rate of the song you want to edit your videos to. Each time
the value is changed a new sliceArray and a new markerArray is created
with slices and markers from 0 to the duration of the active
composition. If no composition is selected slices and markers will be
created from 0 to 60 seconds.

Bars
~~~~

Set bars in order to determine how many markers are created when
creating markers. Each time the value is changed a new sliceArray and a
new markerArray is created with slices and markers from 0 to the
duration of the active composition. If no composition is selected slices
and markers will be created from 0 to 60 seconds.

Select Workarea
~~~~~~~~~~~~~~~

Select the workarea to which all actions of this script are applied.

-  **Comp Workarea:** The workarea is the workarea of the active
   composition.
-  **Layer in/out:** The workareas in and out points are the in and out
   points of the selected layer. If multiple layers are selected, the
   lowest in point and the highest out point of all layers are
   considered.
-  **Comp Duration:** The workarea starts at 0 and ends with the
   duration of the active composition.

**Tools for selected Layer/s**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

move back
~~~~~~~~~

Moves the selected layer according to the bpm and bars value to the
left.

move forth
~~~~~~~~~~

Moves the selected layer according to the bpm and bars value to the
right.

Arrange Layer/s
~~~~~~~~~~~~~~~

All selected layers are getting arranged like a stairway according to
the currently set bpm and bars value.

Randomize Selection
~~~~~~~~~~~~~~~~~~~

All selected layers are getting randomly deselected.

Foist
~~~~~

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


**Markers**
~~~~~~~~~~~

Comp/Layer Dropdown
~~~~~~~~~~~~~~~~~~~

Choose whether you want to address comp markers or layer markers.

Read
~~~~

Read all markers from the selected layer or the active composition and
save them as slices to the sliceArray and as markers to the markerArray.
If you choose to click the ‚Slice‘ button right after reading markers
with this function, the selected layer is sliced at the points in the
timeline where the markers were positioned.

Add
~~~

Create layer markers on the selected layer which represent the in points
of the slices in the sliceArray.

Show
~~~~

Shows the markerArray.

Quantize
~~~~~~~~

The markers of the selected layer are getting quantized to the currently
set bpm and bars value in the region that is set by the ‚Workarea‘
dropdown list (This function doesn‘t work with composition markers yet).

Load Txt
~~~~~~~~

Load a txt file that contains midi note on and off information and
import them as slices into the sliceArray (The in points of the slices
are getting added to the markerArray which could be added as markers to
a layer or the composition by clicking the ‚Add‘ button).

Save Txt
~~~~~~~~

Save a txt file that contains all slices from the sliceArray.

**Transitions**
~~~~~~~~~~~~~~~

A (In)
~~~~~~

Attack of the envelope. If ‚Loop‘ is unchecked this is the in
transition.

D
~

Decay of the envelope.

S
~

Sustain of the envelope.

R (Out)
~~~~~~~

Release of the envelope. If ‚Loop‘ is unchecked this is the out
transition.

Loop
~~~~

If checked the adsr is applied in a loop.

Choose Transition Effect
~~~~~~~~~~~~~~~~~~~~~~~~

Choose between the following effects:

   Opacity, Blockauflösung, CC Glass Wipe, Card Wipe, CC Grid Wipe, CC
   Image Wipe, CC Jaws, CC Light Wipe, CC Line Sweep, CC Radial
   ScaleWipe, CC Scale Wipe, CC Twister, CC WarpoMatic, Gradient Wipe,
   Iris Wipe, Linear Wipe, Radial Wipe, Venetian Blinds

Presets
~~~~~~~

Choose one of the following presets for the adsr settings.

   Kick, Snare, Hihats, Bass, Piano, Pads, 1, 1/2, 1/3, 1/4, 1/6, 1/8,
   1/12, 1/16

All the instrument presets represent fixed values for the adsr.

The quantized presets (1 ... 1/16) are getting updated each time the bpm
value of the script is changed. In order to use this update function you
need to make sure the checkbox ‚Snap In Out Transition To Bpm‘ is
checked in the ‚Options‘ tab.

This is how the values are getting distributed between a, d, s and r: a
= beatRate / 3; d = beatRate / 3; r = beatRate / 3.5; The r value is
slightly smaller calculated in order to make it possible to loop the
adsr without intersections between r and the following a.

Apply Transition
~~~~~~~~~~~~~~~~

Add a transition to all selected layers.

Preview
~~~~~~~

When the script launches, the display update function is turned off.

   Option+Click (Win Alt+Click): An scheduled update function for the
   display is toggled on (or off).

If the update function is running the preview area is updated each
second with means by an scheduled task from after effects.

This only works if the script runs as a panel (If the script is launched
as a window the update function doesn‘t work).

   Option+Shift+Click (Win Alt+Shift+Click): All scheduled tasks that
   are running are getting closed.

Slice
~~~~~

Click ‚Slice‘ to slice the selected layer according to the slices in the
sliceArray.

Show slices
~~~~~~~~~~~

Show all slices of the sliceArray.





**Random**
~~~~~~~~~~

Time stretch
~~~~~~~~~~~~

The newly created slice will receive a random time stretch value. The
strenght of the randomness is set by the slider on the right.

Start point
~~~~~~~~~~~

The newly created slice will receive a random start point value. The
strenght of the randomness is set by the slider on the right.

Midiconverter (external)
------------------------

Midi converter button
~~~~~~~~~~~~~~~~~~~~~

The Midi converter interprets 12 note values in the range of C3 - B3.
Please make sure that the midinotes are placed in exactly that range,
otherwise the notes won‘t be recognized.

The chosen .mid file is converted to a .txt file with a assigned
videotrack a note-on and note-off value and a velocity value that can be
imported by the Premiere Pro extension ‚BpmSlicer‘.

e.g.

-  1 0 2.5 0.5
-  2 2.5 3.4 1.0

Bpm editor
~~~~~~~~~~

Before the midi clip is converted, a tempo event with the given ‚bpm‘
rate is added to the midi clip.

If the midi clip has a tempo event already and you want to use it
instead of a new one, set the bpm value to ‚-1‘.

If the bpm editor is empty the default bpm value of 120 is used.

Fps editor
~~~~~~~~~~

The fps value (Frames per seconds) is only needed if you want to use the
clipboard to copy keyframes directly onto one of After Effects layer
properties. With help of the fps value the time of the midi note-on
values can be transformed to frame values.

Clipboard
~~~~~~~~~

The velocity values of all midi note-on messages are mapped to the range
of 0.0 - 1.0 and copied to the systems clipboard so that you can simply
paste the values as keyframes onto a selected ‚expression slider‘
property in After Effects. A ‚expression slider‘ with those keyframes
can then be used to manipulate different properties and effects.