BpmSlicerAE
===========

Most important References
~~~~~~~~~~~~~~~~~~~~~~~~~

-  `After Effects Scripting Guide`_

-  `The Javascript Tools Guide`_

-  `Beginning ScriptUI 2-13-f-2017`_

-  `Markup Cheatsheet for Readme.md`_

-  `Socrates view markdown`_

A manual for the After Effects Script
-------------------------------------

Description
~~~~~~~~~~~

This script is is a tool to slice footage layer in a composition into
many pieces which are synchronized to a piece of music. The script
contains a collection of features that migh help to create a music video
such as: Import a txt file that contains slice information (The external
app „Midiconverter“ converts a conventional midi clip into such a
supported txt file). This script can be used to slice a layer to the
beat of a piece of music. For this to work you need to set the Bpm rate
(Beats per minute) of your song.

1. Select a layer
2. Set the slicing rate (32 bars, 16 bars, 8, 4, 1, 1/4, 1/8, 1/16,
   1/32)
3. Check the ‚Marker‘ checkbox in case you need composition markers for
   all slices
4. Click ‚Slice‘

Dependencies
~~~~~~~~~~~~

This script requires the 'peacock_library.jsx' which also requires three
external .jsx files (peacock_helper.jsx, peacock_aeHelper.jsx,
peacock_guiCreator.jsx) in order to run. These files have to be existing
in the following folder:

-  Win: C:\Documents and Settings\All Users\Application
   Data\Peacock\libraries\\
-  Mac: /Library/Application Support/Peacock/libraries/



The Console
-----------

The console is like a command line. Three different types of input are
possible.

1. **After Effects Keyframes / Mocha Tracking Data** You can either
   paste Mocha tracking data directly from Mocha into the console or
   Keyframes from a selected layer property in After Effects. Note that
   only Position, Scale and Rotation keyframes are supported yet. If you
   press: ``Cmd+Enter`` or the ``'R' button`` the keyframes are getting
   parsed into an internal keyframe data structure.
   ``(There is no use for the parsed keyframes yet. I plan to manipulate tracking data keyframes synced to the beat)``

2. **Peacock midi note data** The external standalone program
   "Midiconverter" converts a midi file (.mid) into 'Peacock midi note
   data'. For this to work the midi notes in the midi file have to be in
   the range from C3 - C4 and you need to set the proper bpm value.
   After the midi file is converted the 'Peacock midi note data' is
   automatically copied to the clipboard and a .txt file with the same
   'Peacock midi note data' is created as a sibling of the midi file.
   The 'Peacock midi note data' can be directly pasted into the
   BpmSlicer console. By pressing ``Cmd+Enter`` or the ``'R' button``
   the slice data is getting parsed into the internal slices array which
   can then be used to slice layers in a composition.

3. **Executable javascript** You can write any javascript code you like
   and execute it directly from the console. Some useful code snippets
   are accessible through tabcompletion and shortcuts

============== ==========================================================================================================================================================================================================================================================
Shortcut       Code Snippet
============== ==========================================================================================================================================================================================================================================================
``select``     ``for(var i=0; i<comp.selectedLayers.length;i++){ var layer = comp.selectedLayers[i]; if(layer.name != "") layer.selected = true; }``
``bpm``        ``log.text = beatManager.getBpm();``
``beatRate``   ``log.text = beatManager.calculateBeatRate(beatManager.getBpm(), "1/4");``
``status``     ``log.text = markers.markers.length + " markers; ";\nlog.text += slices.slices.length + " slices";``
``rename``     ``var name = "newName"; re = /^name/; for(var i=0; i<comp.selectedLayers.length; i++){ var layer = comp.selectedLayers[i]; if(re.test(layer.name)) layer.name = name + "_" + i; }``
``createfile`` ``var text = ""; var filePath = Folder.desktop.fullName + "/_default.txt"; var file = new File(filePath); if(file === null) file = File.saveDialog("Choose a txt file","*.txt*", filePath); file.open("w"); file.writeln(text.toString()); file.close();``
============== ==========================================================================================================================================================================================================================================================

============= ================================================================================================================================
Tabcompletion Code Snippet
============= ================================================================================================================================
``for``       ``for(var i=0; i<comp.selectedLayers.length; i++) { var layer = comp.selectedLayers[i]; log.appendLog(i + " " + layer.name); }``
``fors``      ``for(var i=0; i<slices.slices.length; i++) { var slice = slices.slices[i]; log.appendLog(i + " " + slice.getInPoint()); }``
``form``      ``for(var i=0; i<markers.markers.length; i++) { var marker = markers.markers[i]; log.appendLog(i + " " + marker.getTime()); }``
``if``        ``if(markers.markers.length > 10) { log.appendLog("More than 10 markers exist"); }``
``if else``   \`if(markers
============= ================================================================================================================================



Preparations
------------

Before you can take full advantage of the functionality of the BpmSlicer
you need to prepare your footage as follows.

Song preparation
~~~~~~~~~~~~~~~~

You have to ensure that the following two conditions are met: You need
to know the exact bpm value of the song you want to work with and set
this value in the bpm input field. You need to make sure that the 1st
beat of the song sits exactly at the 0 point in time. Some songs may not
have an intro that fits the bpm rate of the actual song, then you need
to find the first beat and place it accordingly. If you have the exact
bpm rate of the song then it won‘t be too difficult to make it fit.

Preparing the midi clip
~~~~~~~~~~~~~~~~~~~~~~~

Please make sure that the midinotes in the midi file are placed in the
range between C3 - B3, otherwise the notes won‘t be recognized. Note
that the notes of C3 are placed onto videotrack 1, the notes of C#3 onto
videotrack 2 and so on.

-  C3 -> videotrack 1
-  C#3 -> videotrack 2
-  D3 -> videotrack 3
-  ... -> ...
-  B3 -> videotrack 12

Preparing your footage
~~~~~~~~~~~~~~~~~~~~~~

If there is no BpmSlicer folder structure already you can create one by
clicking the „create folders“ Button. The next step is to put all your
footage you want to be placed into the active sequence, according to the
notes in the midi file, into the „1 source“ folder and assign the
appropriate prefix for each footage item. Make sure the prefix is a
number between 1 - 12 and make sure there is a white space between the
prefix number and the footage name.

The next thing you want to make sure is that you add as much videotracks
to the active sequence as your highest assigned prefix is. In the
following example the highest assigned prefix is 4, so you need to make
sure there are at least 4 videotracks available.

::

   BpmSlicer
       1 source
           1 VideoClip2.mov
           2 LensFlare2.mov
           3 Transition_1.mov
           4 PaperTexture_9.png
           4 PaperTexture_1.mov

As you notice in the example it‘s possible to assign the same prefix to
as many footage items as you like. If you assign the same prefix to more
then one footage items, this function selects a random footage item each
time it finds a midi note for the appropriate videotrack.



Workflows
---------

Quickstart
~~~~~~~~~~

| Create a composition with some video footage in it and make sure it is
  selected. Leave all settings in the BpmSlicer as is and click the
  ‚Slice‘ button at the bottom of the script. The selected footage layer
  is getting sliced as seen in the image below:
| The reason why there are exactly 5 slices is because by default the
  sliceArray is set like this:
| That means you have to create a new sliceArray before you can slice
  the footage according to your needs.

Creating a sliceArray
~~~~~~~~~~~~~~~~~~~~~

Set Bars
~~~~~~~~

By setting a new value in the ‚Bars‘ dropdown a new sliceArray is
created which contains slices that are quantized to the selected bars
value and the bpm.

Read Composition/Layer Markers
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In the markers tab, choose whether you want to read composition markers
or layer markers (selected layer). By clicking the ‚Read‘ button in the
Markers tab, a sliceArray is created by all markers of the composition
or layer. This only works if there are at least 2 markers existing.

Read Slices from Txt File
~~~~~~~~~~~~~~~~~~~~~~~~~

By clicking the ‚midi‘ button a file chooser dialog is opened and you
get to choose a txt file with informations about all slices. Each line
of the txt file contains 4 parameter values (noteLayer, sliceIn,
sliceOut, Velocity) that represent one slice. Please refer to
„Midiconverter (external)“ auf Seite <?> on how to convert a midifile
into such a txt file.


Generel
-------

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



**Options**
~~~~~~~~~~~

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

Install Instructions
--------------------

After Effects Script Folder
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Copy the BpmSlicer script into the following folders:

-  (Windows) Programme\Adobe\Adobe After Effects \\Support
   Files\Scripts\...
-  (Windows) Programme\Adobe\Adobe After Effects \\Support
   Files\Scripts\ScriptUI Panels\...
-  (Mac OS) /Applications/Adobe After Effects /Scripts/...
-  (Mac OS) /Applications/Adobe After Effects /Scripts/ScriptUI
   Panels/...

Troubleshooting
---------------

My working environment:
-----------------------

-  macOS High Sierra Version 10.13.3
-  Modellname: MacBook Pro
-  After Effects CC
-  Version: 2017.0
-  14.0.0.207

To Do
-----

In Progress
~~~~~~~~~~~

-  Console: Paste keyframe functionality
-  Console: Parse multiline input (slices, markers, keyframes/Mocha)
-  Console: Switch with UP and DOWN key through the console history
-  Using the up and down arrow keys to change numerical data `page 99 in
   scriptui PDF`_

.. code:: javascript

   function handle_key (key, control)
   {
       var step;
       key.shiftKey ? step = 10 : step = 1;
       switch (key.keyName)
       {
           case "Up": control.text = String(Number(control.text)+step); break;
           case "Down": control.text = String(Number(control.text)-step);
       }
    } // handle_key
    e1.addEventListener ("keydown", function (k) {handle_key (k, this);});
    e2.addEventListener ("keydown", function (k) {handle_key (k, this);});

-  
-  `addEventListener() estk.aenhancers.com`_
-  `Understanding capturingPhase`_

.. code:: javascript

   controlObj.addEventListener('change', handler, capturePhase);
   controlObj.addEventListener('changing', handler, capturePhase);
   controlObj.addEventListener('focus', handler, capturePhase);
   controlObj.addEventListener('enterKey', handler, capturePhase);
   stopPropagation();
   preventDefault();

.. _page 99 in scriptui PDF: https://adobeindd.com/view/publications/a0207571-ff5b-4bbf-a540-07079bd21d75/y2c4/publication-web-resources/pdf/scriptui-2-13-f-2017.pdf#page=99
.. _addEventListener() estk.aenhancers.com: http://estk.aenhancers.com/4%20-%20User-Interface%20Tools/control-objects.html#addeventlistener
.. _Understanding capturingPhase: https://stackoverflow.com/questions/7398290/unable-to-understand-usecapture-parameter-in-addeventlistener*
-  `stopPropagation();`_
-  `preventDefault();`_
-  Example: onActivate(), onDeactivate() `page 103 in scriptui PDF`_

.. code:: javascript

   ddown.onActivate = ddown.onDeactivate = function () {buffer = "";}

-  Validating Input, edittext with red background `page 104 in scriptui
   PDF`_

.. code:: javascript

   w.input.onChanging = function () {
       w.ok.enabled = !app.activeDocument.hyperlinkTextDestinations.item
       (w.input.text).isValid;
   }
   w.input.onChanging = function () {
       var valid = /^[\d.,]+$/.test (w.input.text);
       this.graphics.backgroundColor = this.graphics.newBrush (this.graphics.BrushType.
           SOLID_COLOR, valid ? [1, 1, 1, 1] : [1, 0.5, 0.5, 1]);
       w.ok.enabled = valid;
   }

-  own display alert message with edit text `scriptui-2-13-f-2017`_

.. code:: javascript

   // create an example array
   array = [];

   for (i = 0; i < 150; i++)
       array.push ("Line " + String (i));

   alert_scroll ("Example", array);

   function alert_scroll (title, input) // string, string/array
   {
       // if input is an array, convert it to a string
       if (input instanceof Array)
           input = input.join ("\r");
       var w = new Window ("dialog", title);
       var list = w.add ("edittext", undefined, input, {multiline: true, scrolling: true});
       // the list should not be taller than the maximum possible height of the window
       list.maximumSize.height = w.maximumSize.height - 100;
       list.minimumSize.width = 150;
       w.add ("button", undefined, "Close", {name: "ok"});
       w.show ();
   }

-  edittext syntax highlighting/coloring, marker, slice
-  Add reveal preferences button to GUI

.. _stopPropagation();: http://estk.aenhancers.com/4%20-%20User-Interface%20Tools/event-handling.html#stoppropagation
.. _preventDefault();: http://estk.aenhancers.com/4%20-%20User-Interface%20Tools/event-handling.html#preventdefault
.. _page 103 in scriptui PDF: https://adobeindd.com/view/publications/a0207571-ff5b-4bbf-a540-07079bd21d75/y2c4/publication-web-resources/pdf/scriptui-2-13-f-2017.pdf#page=103
.. _page 104 in scriptui PDF: https://adobeindd.com/view/publications/a0207571-ff5b-4bbf-a540-07079bd21d75/y2c4/publication-web-resources/pdf/scriptui-2-13-f-2017.pdf#page=104
.. _scriptui-2-13-f-2017: https://adobeindd.com/view/publications/a0207571-ff5b-4bbf-a540-07079bd21d75/y2c4/publication-web-resources/pdf/scriptui-2-13-f-2017.pdf#page=16

Qued
~~~~

-  BeatManager: Include bpm edittext and rate dropdownlist directly in
   class and not in buildGUI function.
-  Console: Add expand/collapse button
-  Console: Interpret keyframes, remove all keyframes except the ones
   that are on the beat, interpolate the lasting keyframes in different
   ways. This should be fun with tracking data i think.
-  Create marker label: **1 . . . 4 . . . 8 . . . 12** and **1 . . . 1 .
   . . 1 . . . 1**
-  Check javascript compatibility ES5 and ES6, new after effects version
   `legacy-and-extend-script-engine`_
-  New class Keyframes: manage console input
-  app.beep(): Sound?
-  MouseEvent: event.altKey, ctrlKey, metaKey, shiftKey;
   event.screenX/Y, type == "mousedown"; initMouseEvent()
-  KeyboardEvent: event.getModifierState(key); key == "Alt", "Meta",
   "Control", "Shift"
-  Console functions: create multiple comps
   ``create markers [compName]`` and ``create slices [compName]`` ⋅⋅\*
   template.xml: A default template for new compositions is saved on
   disk. New compositions are created by the template data.
-  edit markers/slices in 'show' popup window. remove marker, remove
   slice
-  Quantize keyframes

Done
~~~~

-  Check AE Version, make improvements and make backward compatible

.. _legacy-and-extend-script-engine: https://helpx.adobe.com/after-effects/using/legacy-and-extend-script-engine.html

EventHandling
~~~~~~~~~~~~~

.. code:: javascript

   var newEvent = ScriptUI.events.createEvent( "UIEvent" );
   //initUIEvent(eventName, bubble, isCancelable, view, detail)
   newEvent.initUIEvent( "change", true, true, myControl, 1 );
   myControl.dispatchEvent( newEvent );

   /*
       eventNames:
       change, changing, move, moving, resize, resizing, show, enterKey, focus, blur,
       mousedown, mouseup, mousemove, mouseover, mouseout, keyup, keydown, click

       keyIdentifier:
       "Alt", "CapsLock", "Control", "Meta", "NumLock", "Scroll", "Shift"

       keyLocation:    KeyboardEvent.DOM_KEY_LOCATION_STANDARD
       DOM_KEY_LOCATION_STANDARD, DOM_KEY_LOCATION_LEFT, DOM_KEY_LOCATION_RIGHT, DOM_KEY_LOCATION_NUMPAD
       */
       var newEvent = ScriptUI.events.createEvent( "KeyboardEvent" );
   //newEvent.initKeyboardEvent (eventName, bubble, isCancelable, view, keyID, keyLocation, modifiersList:"Control Alt");
   newEvent.initKeyboardEvent ("keydown", true, true, peacockConsole.console, "Enter", 0, "");
   peacockConsole.console.dispatchEvent( newEvent );


   var newEvent = ScriptUI.events.createEvent( "MouseEvent" );
   // var newEvent = initMouseEvent( eventName, bubble, isCancelable, view, detail, screenX, screenY, clientX, clientY, ctrlKey, altKey, shiftKey, metaKey, button, relatedTarge);
   myControl.dispatchEvent( newEvent );



Errors
~~~~~~

-  ERROR: After Effects Warnung Rückgängig machen nicht
   übereinstimmender Gruppen: es wird versucht, den Fehler zu beheben. I
   create composition markers by hand, read them into markersArray, add
   markersArray to another layer, if I then move the layer the error
   happens and all markers of the moved layer will get removed.

-  Zuletzt protokollierte Meldung: <140736042881856> <BEE_WorkQueue> <5>
   BEE_Project::TimestampGetNext ZANZIBAR-3: cannot produce timestamp,
   frozen=0, open=0. Absturzprotokoll wird erstellt. Dies kann einige
   Minuten dauern. I created a slice with 'slices.createCompSlice(comp,
   new Slice(5,10));' and moved the marker by dragging it to the left.

-  If the project is saved either with autosave or with cmd+s the script
   is crashing and all the custom gui elements are disappearing.
   Actually the next day after restarting the computer and after effects
   this error doesn't happen in the beginning.

Recent Searches
~~~~~~~~~~~~~~~

-  `Progressbar estk.aenhancers`_

-  `ShortcutKey estk.aenhancers`_

-  `Event Handling estk.aenhancers`_

-  `Layer applyPreset estk.aenhancers`_

-  `AVLayer autoOrient estk.aenhancers`_

-  `AVLayer source estk.aenhancers`_

-  `AVLayer replaceSource estk.aenhancers`_

-  `AVLayer sourceRectAtTime estk.aenhancers`_

-  `NumericEditKeyboardHandler`_

-  `Addeventlistener vs OnClick attribute`_

-  `Script Console Script`_

.. _Progressbar estk.aenhancers: http://estk.aenhancers.com/4%20-%20User-Interface%20Tools/control-objects.html#progressbar
.. _ShortcutKey estk.aenhancers: http://estk.aenhancers.com/4%20-%20User-Interface%20Tools/control-objects.html#shortcutkey
.. _Event Handling estk.aenhancers: http://estk.aenhancers.com/4%20-%20User-Interface%20Tools/event-handling.html
.. _Layer applyPreset estk.aenhancers: http://docs.aenhancers.com/layers/layer/#layer-applypreset
.. _AVLayer autoOrient estk.aenhancers: http://docs.aenhancers.com/layers/avlayer/#avlayer-autoorient
.. _AVLayer source estk.aenhancers: http://docs.aenhancers.com/layers/avlayer/#avlayer-source
.. _AVLayer replaceSource estk.aenhancers: http://docs.aenhancers.com/layers/avlayer/#avlayer-replacesource
.. _AVLayer sourceRectAtTime estk.aenhancers: http://docs.aenhancers.com/layers/avlayer/#avlayer-sourcerectattime
.. _NumericEditKeyboardHandler: https://forums.adobe.com/thread/1240406
.. _Addeventlistener vs OnClick attribute: https://forums.adobe.com/thread/2591212
.. _Script Console Script: https://www.adobeexchange.com/creativecloud.details.2450.script-console.html