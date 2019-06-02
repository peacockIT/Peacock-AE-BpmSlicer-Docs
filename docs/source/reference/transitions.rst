~~~~~~~~~~~
Transitions
~~~~~~~~~~~

A (In)
------

Attack of the envelope.
If ``Loop`` is unchecked this is the in transition.

D
---

Decay of the envelope.

S
---

Sustain of the envelope.

R (Out)
-------

Release of the envelope.
If ``Loop`` is unchecked this is the out transition.

Loop
----

If checked the adsr is applied in a loop.

Choose Transition Effect
------------------------

Choose between the following effects:

  - Opacity
  - Blockauflösung
  - CC Glass Wipe
  - Card Wipe
  - CC Grid Wipe
  - CC Image Wipe
  - CC Jaws
  - CC Light Wipe
  - CC Line Sweep
  - CC Radial ScaleWipe
  - CC Scale Wipe
  - CC Twister
  - CC WarpoMatic
  - Gradient Wipe
  - Iris Wipe
  - Linear Wipe
  - Radial Wipe
  - Venetian Blinds

Presets
-------

Choose one of the following presets for the adsr settings.

  - Kick
  - Snare
  - Hihats
  - Bass
  - Piano
  - Pads
  - 1
  - 1/2
  - 1/3
  - 1/4
  - 1/6
  - 1/8
  - 1/12
  - 1/16

All the instrument presets represent fixed values for the adsr.

The quantized presets (1 ... 1/16) are getting updated each time the bpm
value of the script is changed. In order to use this update function you
need to make sure the checkbox ``Snap In Out Transition To Bpm`` is
checked in the ``Options`` tab.

This is how the values are getting distributed between a, d, s and r:
  .. code-block:: javascript

    a = beatRate / 3; d = beatRate / 3; r = beatRate / 3.5;

The r value is slightly smaller calculated in order to make it possible
to loop the adsr without intersections between r and the following a.


Apply Transition
----------------

Add a transition to all selected layers.

