***************
Troubleshooting
***************

.. contents:: Table of Contents

My working environment:
-----------------------

-  macOS High Sierra Version 10.13.3
-  Modellname: MacBook Pro
-  After Effects CC
-  Version: 2017.0
-  14.0.0.207


Errors
~~~~~~
.. Error::
    **Error:**
    ERROR: After Effects Warnung Rückgängig machen nicht übereinstimmender Gruppen: es wird versucht, den Fehler zu beheben.

    **Description:**
    I create composition markers by hand, read them into markersArray, add markersArray to another layer, if I then move the layer the error happens and all markers of the moved layer will get removed.

.. Error::
    **Error:**
    Zuletzt protokollierte Meldung: <140736042881856> <BEE_WorkQueue> <5> BEE_Project::TimestampGetNext ZANZIBAR-3: cannot produce timestamp, frozen=0, open=0. Absturzprotokoll wird erstellt. Dies kann einige Minuten dauern.

    **Description:**
    I created a slice with 'slices.createCompSlice(comp, new Slice(5,10));' and moved the marker by dragging it to the left.

.. Error::
    **Error:**
    If the project is saved either with autosave or with cmd+s the script is crashing and all the custom gui elements are disappearing.

    **Description:**
    Actually the next day after restarting the computer and after effects this error doesn't happen in the beginning.