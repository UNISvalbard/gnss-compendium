# Post-kinematic processing: Leica Infinity

```{admonition} Infinity Software Version
:class: suggestion

The following tutorial is based on Leica Infinity software version 4.0.0.
Minor changes may be expected when newer versions are used.
```

```{admonition} Work in progress
:class: warning

This page is still being updated.
Help is more than welcome - please edit this page (see {numref}`github_tut`).
```

## Create a project

Unless a project was previously made, Leica Infinity requires you to set up a new project.
Proceed by opening the *New Project* tab from the main side menu.
As depicted in {numref}`infinity-new-project`, fill out the project name, owner, and other metadata; then click *Create*.

```{figure} assets/Leica_Infinity_New_Project.gif
:name: infinity-new-project

Create a new project from scratch in Leica Infinity.
```

You are then ready to proceed with changing the project's coordinate reference system (crs), importing data, adding ellipsoid to orthogonal height corrections, and more.

## Transfering and importing GNSS data from Captivate into Infinity

Before accessing the measured GNSS data in Leica Infinity, the measurements need to be transferred over from the controller to the computer.
First, transfer the Job data from the internal memory of the controller to the SD card, using Leica Captivate (i.e., the controller software).

```{admonition} Available through YouTube.
:class: seealso
<iframe width=100% height=400 src="https://www.youtube.com/embed/boSn-jx_Trc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
```
The Leica CS20s have the SD card at the bottom-side of the controller unit.
Simply take off the protective slide, and take out the SD card.
A warning may pop up in case a non-Leica SD card is used.
This should not affect anything; if possible, use a lower-capacity SD card that can be formatted as FAT32 to circumvent this issue.
Then connect the SD card to the computer, and drag and drop the `.m00` file into the *Navigator* panel of Leica Infinity. 
The `.m00` file is found within the **DBX** directory on the SD card, under the job-name directory.

```{figure} assets/Leica_Infinity_Project_Data.gif
:name: raw-data-import

Importing raw GNSS rover data from the SD card.
```

Once the raw GNSS data have been imported, do the same with the reference data from the base or control station.
Permanent base station data can be obtained from e.g. Kartverket, as detailed in {ref}`base:station:reference:data:download`.
Drag and drop the data into the same panel.


```{figure} assets/Leica_Infinity_Reference_Data.gif
:name: reference-data-import

Importing GNSS reference data from a base station.
```

With both raw and reference GNSS data available, the data can now be processed.

## Processing

Proceed to the *Inspector* view, then press the *GNSS* tab within the *Inspector* panel.
You should then be able to set the *Point Role*.
Select the reference data set, go to the *Processing* tab in the main menu, then click the *GNSS* icon for more option.
Specify *Reference* for the reference data; then repeat the same for all measurements, specifying *Rover* for each.
Finally, apply post-kinematic processing by clicking *GNSS > Process*.

Before proceeding, it is important to save the processing result!
Right click the data and select *Store* to make the processing results permanent.

```{figure} assets/Leica_Infinity_Processing.gif
:name: infinity-data-processing
Select rover and base data, assign their roles, and then process the data.
```

The processing report can be accessed by right clicking a data point, subsequently *Reports > Summary*.
This report has key data on the accuracy and solution type of the processed data.
Always provide the processing report along with the processed data.

```{figure} assets/Leica_Infinity_Processing_Report.gif
:name: infinity-report-export

Exporting of processing reports should be standard procedure for any and all processing.
Only then are all the meta- and paradata correctly reported and documented.
```

Data can be exported by selecting all points of interest, and then right clicking the selection.
Save the data by clicking *Save as...*, specifying the location for where the data should be stored.

```{figure} assets/Leica_Infinity_Processing_Export.gif
:name: infinity-export-processed-data

Export the processed data points in csv format, including errors and coordinates.
```

```{admonition} Using the *Export* button
:class: warning

Data may also be exported in a variety of formats by clicking on the *Export* button in the main menu (under the *Home* tab).
However, be aware that data exported in this manner does not provide all the details of the suggested approach above.
```
