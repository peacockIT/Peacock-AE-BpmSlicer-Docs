***********
The Console
***********

.. contents:: Table of Contents

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

============== ================================================================================================================
Shortcut       Code Snippet
============== ================================================================================================================
``select``     ``for(var i=0; i<comp.selectedLayers.length;i++){ var layer = comp.selectedLayers[i]; if(layer.name != "") layer.selected = true; }``
``bpm``        ``log.text = beatManager.getBpm();``
``beatRate``   ``log.text = beatManager.calculateBeatRate(beatManager.getBpm(), "1/4");``
``status``     ``log.text = markers.markers.length + " markers; ";\nlog.text += slices.slices.length + " slices";``
``rename``     ``var name = "newName"; re = /^name/; for(var i=0; i<comp.selectedLayers.length; i++){ var layer = comp.selectedLayers[i]; if(re.test(layer.name)) layer.name = name + "_" + i; }``
``createfile`` ``var text = ""; var filePath = Folder.desktop.fullName + "/_default.txt"; var file = new File(filePath); if(file === null) file = File.saveDialog("Choose a txt file","*.txt*", filePath); file.open("w"); file.writeln(text.toString()); file.close();``
============== ================================================================================================================

============= ================================================================================================================================
Tabcompletion Code Snippet
============= ================================================================================================================================
``for``       ``for(var i=0; i<comp.selectedLayers.length; i++) { var layer = comp.selectedLayers[i]; log.appendLog(i + " " + layer.name); }``
``fors``      ``for(var i=0; i<slices.slices.length; i++) { var slice = slices.slices[i]; log.appendLog(i + " " + slice.getInPoint()); }``
``form``      ``for(var i=0; i<markers.markers.length; i++) { var marker = markers.markers[i]; log.appendLog(i + " " + marker.getTime()); }``
``if``        ``if(markers.markers.length > 10) { log.appendLog("More than 10 markers exist"); }``
``if else``   ``if(markers.markers.length > 10) { log.appendLog("More than 10 markers exist"); }else { log.appendLog("Less than 10 (or equal) markers exist"); }``
============= ================================================================================================================================


Field list
~~~~~~~~~

Shortcuts
---------

:select: for(var i=0; i<comp.selectedLayers.length;i++){
             var layer = comp.selectedLayers[i]; if(layer.name != "")
             layer.selected = true;
         }
:bpm: log.text = beatManager.calculateBeatRate(beatManager.getBpm(), "1/4");
:beatRate: log.text = beatManager.calculateBeatRate(beatManager.getBpm(), "1/4");
:status: log.text = markers.markers.length + " markers; ";\nlog.text += slices.slices.length + " slices";
:rename: var name = "newName"; re = /^name/;
         for(var i=0; i<comp.selectedLayers.length; i++){
            var layer = comp.selectedLayers[i];
            if(re.test(layer.name))
               layer.name = name + "_" + i;
         }
:createfile: var text = "";
             var filePath = Folder.desktop.fullName + "/_default.txt";
             var file = new File(filePath);
             if(file === null)
               file = File.saveDialog("Choose a txt file","*.txt*", filePath);
             file.open("w");
             file.writeln(text.toString());
             file.close();


Tabcompletion
-------------
:for: for(var i=0; i<comp.selectedLayers.length; i++){
         var layer = comp.selectedLayers[i];
         log.appendLog(i + " " + layer.name);
      }
:fors: for(var i=0; i<slices.slices.length; i++) {
         var slice = slices.slices[i];
         log.appendLog(i + " " + slice.getInPoint());
       }
:form: for(var i=0; i<markers.markers.length; i++) {
         var marker = markers.markers[i];
         log.appendLog(i + " " + marker.getTime());
       }
:if: if(markers.markers.length > 10) {
       log.appendLog("More than 10 markers exist");
     }
:if else: if(markers.markers.length > 10) {
              log.appendLog("More than 10 markers exist");
          }else {
              log.appendLog("Less than 10 (or equal) markers exist");
          }



Option Lists
~~~~~~~~~~~~

Shortcuts
---------

-select
              for(var i=0; i<comp.selectedLayers.length;i++){
                 var layer = comp.selectedLayers[i]; if(layer.name != "")
                 layer.selected = true;
              }
-bpm          log.text = beatManager.calculateBeatRate(beatManager.getBpm(), "1/4");
beatRate      log.text = beatManager.calculateBeatRate(beatManager.getBpm(), "1/4");
status        log.text = markers.markers.length + " markers; ";\nlog.text += slices.slices.length + " slices";
rename        var name = "newName"; re = /^name/;
              for(var i=0; i<comp.selectedLayers.length; i++){
                 var layer = comp.selectedLayers[i];
                 if(re.test(layer.name))
                 layer.name = name + "_" + i;
              }
createfile    var text = "";
              var filePath = Folder.desktop.fullName + "/_default.txt";
              var file = new File(filePath);
              if(file === null)
                 file = File.saveDialog("Choose a txt file","*.txt*", filePath);
              file.open("w");
              file.writeln(text.toString());
              file.close();

Tabcompletion
-------------
for   for(var i=0; i<comp.selectedLayers.length; i++){
         var layer = comp.selectedLayers[i];
         log.appendLog(i + " " + layer.name);
      }
-fors  for(var i=0; i<slices.slices.length; i++) {
         var slice = slices.slices[i];
         log.appendLog(i + " " + slice.getInPoint());
       }
form   for(var i=0; i<markers.markers.length; i++) {
         var marker = markers.markers[i];
         log.appendLog(i + " " + marker.getTime());
       }
if   if(markers.markers.length > 10) {
       log.appendLog("More than 10 markers exist");
     }
if else   if(markers.markers.length > 10) {
              log.appendLog("More than 10 markers exist");
          }else {
              log.appendLog("Less than 10 (or equal) markers exist");
          }




Second list level
~~~~~~~~~~~~~~~~

Tabcompletion
-------------
- here is a list in a second-level section.
  - here is an inner bullet ``oh``
    - one more ``with an inline literally``. `yahoo <http://www.yahoo.com>`_

      heh heh. child. try to beat this embed:

      .. code-block:: javascript
         :caption: for
         for(var i=0; i<comp.selectedLayers.length; i++){
           var layer = comp.selectedLayers[i];
           log.appendLog(i + " " + layer.name);
         }
      .. code-block:: javascript
         :caption: fors
         for(var i=0; i<slices.slices.length; i++) {
           var slice = slices.slices[i];
           log.appendLog(i + " " + slice.getInPoint());
         }
      .. code-block:: javascript
         :caption: form
         for(var i=0; i<markers.markers.length; i++) {
           var marker = markers.markers[i];
           log.appendLog(i + " " + marker.getTime());
         }
      .. code-block:: javascript
         :caption: if
         if(markers.markers.length > 10) {
           log.appendLog("More than 10 markers exist");
         }
      .. code-block:: javascript
         :caption: if else
         if(markers.markers.length > 10) {
           log.appendLog("More than 10 markers exist");
         }else {
           log.appendLog("Less than 10 (or equal) markers exist");
         }




Tabcompletion List
~~~~~~~~~~~~~~~~~~

Shortcuts
---------

.. code-block:: javascript
  :caption: select

  for(var i=0; i<comp.selectedLayers.length;i++){
    var layer = comp.selectedLayers[i]; if(layer.name != "")
    layer.selected = true;
  }

.. code-block:: javascript
  :caption: bpm
  log.text = beatManager.calculateBeatRate(beatManager.getBpm(), "1/4");

.. code-block:: javascript
  :caption: beatRate
  log.text = beatManager.calculateBeatRate(beatManager.getBpm(), "1/4");

.. code-block:: javascript
  :caption: status
  log.text = markers.markers.length + " markers; ";\nlog.text += slices.slices.length + " slices";

.. code-block:: javascript
  :caption: rename
  var name = "newName"; re = /^name/;
  for(var i=0; i<comp.selectedLayers.length; i++){
    var layer = comp.selectedLayers[i];
    if(re.test(layer.name))
    layer.name = name + "_" + i;
  }

.. code-block:: javascript
  :caption: createfile
  var text = "";
  var filePath = Folder.desktop.fullName + "/_default.txt";
  var file = new File(filePath);
  if(file === null)
    file = File.saveDialog("Choose a txt file","*.txt*", filePath);
  file.open("w");
  file.writeln(text.toString());
  file.close();




Tabcompletion
-------------
.. code-block:: javascript
  :caption: for
  for(var i=0; i<comp.selectedLayers.length; i++){
    var layer = comp.selectedLayers[i];
    log.appendLog(i + " " + layer.name);
  }
.. code-block:: javascript
  :caption: fors
  for(var i=0; i<slices.slices.length; i++) {
    var slice = slices.slices[i];
    log.appendLog(i + " " + slice.getInPoint());
  }

.. code-block:: javascript
  :caption: form
  for(var i=0; i<markers.markers.length; i++) {
    var marker = markers.markers[i];
    log.appendLog(i + " " + marker.getTime());
  }
.. code-block:: javascript
  :caption: if
  if(markers.markers.length > 10) {
    log.appendLog("More than 10 markers exist");
  }
.. code-block:: javascript
  :caption: if else
  if(markers.markers.length > 10) {
    log.appendLog("More than 10 markers exist");
  }else {
    log.appendLog("Less than 10 (or equal) markers exist");
  }

