============
Installation
============

Dependencies
~~~~~~~~~~~~

This script requires the 'peacock_library.jsx' which also requires three
external .jsx files (peacock_helper.jsx, peacock_aeHelper.jsx,
peacock_guiCreator.jsx) in order to run. These files have to be existing
in the following folder:

-  Win: C:\Documents and Settings\All Users\Application
   Data\Peacock\libraries\\
-  Mac: /Library/Application Support/Peacock/libraries/


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