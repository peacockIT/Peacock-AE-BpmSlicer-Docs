****************
Work in Progress
****************

.. contents:: Table of Contents

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
