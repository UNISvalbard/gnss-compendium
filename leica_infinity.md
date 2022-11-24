# Leica Infinity v4.0.0

## Create a project

```{figure} assets/Leica_Infinity_New_Project.gif
:name: new-project

Create a new project
```

## Import GNSS data

First transfer the Job data from the internal memory of the controller to the SD card, using Leica Captivate (i.e., the controller software).

```{admonition} Available through YouTube.
:class: seealso
<iframe width=100% height=400 src="https://www.youtube.com/embed/boSn-jx_Trc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
```

Then connect the SD card to the computer, and drag and drop the `.m00` file into the *Navigator* panel of Leica Infinity.

```{figure} assets/Leica_Infinity_Project_Data.gif
:name: new-project

Import data
```

At the same time, download the reference data from your base station or control station (e.g., Kartverket), and drop it into the same panel.


```{figure} assets/Leica_Infinity_Reference_Data.gif
:name: new-project

Import reference data
```

The project is now set for processing.

## Processing

Proceed to the *Inspector* view, then press the *GNSS* tab within the *Inspector* panel.
You should then be able to set the *Point Role*.
Select the reference data set, go to the *Processing* tab in the main menu, then click the *GNSS* icon for more option.
Specify *Reference* for the reference data; then repeat the same for all measurements, specifying *Rover* for each.
Finally, apply post-kinematic processing by clicking *GNSS > Process*.

Before proceeding, it is important to save the processing result!
Right click the data and select *Store* to make the processing results permanent.

```{figure} assets/Leica_Infinity_Processing.gif
:name: new-project

Select rover and base data, then process the data
```

The processing report can be accessed by right clicking a data point, subsequently *Reports > Summary*.
This report has key data on the accuracy and solution type of the processed data.
Always provide the processing report along with the processed data.

```{figure} assets/Leica_Infinity_Processing_Report.gif
:name: new-project

Export the processing report
```

Data can be exported by selecting all points of interest, and then right clicking the selection.
Save the data by clicking *Save as...*, specifying the location for where the data should be stored.

```{figure} assets/Leica_Infinity_Processing_Export.gif
:name: new-project

Export the processed data points in csv format.
```

```{admonition} Using the *Export* button
:class: warning

Data may also be exported in a variety of formats by clicking on the *Export* button in the main menu (under the *Home* tab).
However, be aware that data exported in this manner does not provide all the details of the suggested approach above.
```
