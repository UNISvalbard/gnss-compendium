# Instrument setup

```{admonition} Work in progress
:class: warning

This will be updated when ready :)
```

## Hardware setup

```{admonition} Work in progress
:class: warning

This will be updated when ready :)
```
### Controller startup

```{admonition} Work in progress
:class: warning

This will be updated when ready :)
```

### Sensor startup

Although similar in appearance, the GS16 and GS18 sensors have slightly different operating procedures and specifications.
This also extends to the location of the battery and (micro)SD card slot readers.
The videos below highlight where and how to insert the (micro)SD cards and batteries into the respective sensors.

`````{tab-set}
````{tab-item} GS16
```{admonition} Available through YouTube.
:class: seealso
<iframe width=100% height=400 src="https://www.youtube.com/embed/lLBGDRlqAeo" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
```
````



````{tab-item} GS18
```{admonition} Available through YouTube.
:class: seealso
<iframe width=100% height=400 src="https://www.youtube.com/embed/qvCxlDFYRT4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
```
````
`````

## Software Setup

### Connecting and configuring the GS Sensor

Once the sensor and controller have been turned on and mounted on the poles, you will need to connect the controller with the sensors, specifying the correct/absolute height of the sensor above the measuring point.

```{admonition} Available through YouTube.
:class: seealso
<iframe width=100% height=400 src="https://www.youtube.com/embed/L4yKKveGeqU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
```

After successfully connecting to the sensor, you should double-check the sensor settings, including the correct sensor height parameters, which GNSS network to use (e.g., GPS, GLONASS, BeiDou, Galileo), and more.
Finally, it is crucial to store the raw data if you want to apply post-processing.
This requires the raw data to be stored at 1.0s intervals.

```{admonition} Available through YouTube.
:class: seealso
<iframe width=100% height=400 src="https://www.youtube.com/embed/MGuMT0Gt2nM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
```

(hardware:setup:base)=
### Base station mode setup

The Leica GS sensors can be easily turned into a portable *base station*.
Simply connect to the sensor from with Leica Captivate, then proceed by clicking **Switch to base (3)**.
Within a few seconds, the base station starts recording and storing the data.

Make sure to proceed with the **Base Setup (1)**.
For most purposes, it suffices to specify data acquisition **Over any point (3)**, which then prompts for the antenna parameters and a *Point ID*.
The *Point ID* represents the name of the *base station*.
Give it a unique name that allows you to find it on the SD card.

```{admonition} Available through YouTube.
:class: seealso
<iframe width=100% height=400 src="https://www.youtube.com/embed/FLr_D48eZog" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
```

After finalising the initial setup, proceed to the **Settings (2)** menu.
Specifically, modify the **Satellite Tracking (1)** and **GNSS raw data logging (2)** parameters found within the **GS base (1)** menu.
Always enable *GNS*, *Glonass* and *Galileo* for tracking - BeiDou is not supported.
Also make sure to *Log GNSS raw data* and *Store data on* the GS sensor SD card at 1.0s intervals.
The *Leica format (MDB)* is supported by the Leica Infinity software, which can also export it in different formats.

Switching the GS sensor back to *rover* mode is easy - just click **Switch to rover (3)** when done in base mode.
