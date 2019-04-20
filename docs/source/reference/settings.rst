========
Settings
========

Audio Reference
~~~~~~~~~~~~~~~

Select whether your audio file is the first or the last layer in your
composition.

Move to Top
~~~~~~~~~~~

After a slice is created it gets moved to the top of the composition.

Remove first selected layers
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

After all slices are created, the layer/s that where selected before the
‚Slice‘ button was pressed, are getting deleted.

Put in sub comp
~~~~~~~~~~~~~~~

After all slices are created, all slices and the first selected layer
are getting moved to a sub composition.

Create effects layer
~~~~~~~~~~~~~~~~~~~~

A adjustment layer is created on top of all other layers in the
composition. The following list shows all effects that are applied on
the adjustment layer. The keyframes on the effects are the slice
inPoints from the sliceArray. Basically the values for each slice are
randomly choosen such as random color overlay for each slice.

-  Farbbalance (HSL)
-  Farbton, Sättigung
-  4-Farben-Verlauf
-  Punkt 1, Farbe 1, Punkt 2, Farbe 2, Punkt 3, Farbe 3, Punkt 4, Farbe
   4, Deckkraft

Set starttime to inPoint
~~~~~~~~~~~~~~~~~~~~~~~~

Sets the start time of all slices to the inpoint.

Use beat detection
~~~~~~~~~~~~~~~~~~

See ‚Markers from Beat‘.

Save Bpm Slices
~~~~~~~~~~~~~~~

If checked then the slices of the sliceArray are getting saved in a txt
file called ‚BpmSlices.txt‘ in the same folder where the after effects
project is located.

Snap In/Out Transition To Bpm
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If checked then the in and out value for the transition function are
getting updated each time the bpm or the bars value changes.