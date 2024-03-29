(gnss:data:acqusition)=
# GNSS Data acquisition with Leica Captivate

Once the hardware has been setup, it is time to power up the Leica controller with Leica Captivate software.
This software simplifies the data project management and acquisition.

```{admonition} RTK? PPK? PPP?
:class: suggestion

RTK, PPK and PPP are just some of the acronyms frequently used by the GNSS community.

RTK stands for real-time kinematics, and uses base station data to reduce the error of your measured location in real time - down to centimetre accuracies in static mode.

PPK (post-processed kinematics) uses the same base station as part of post-processing, allowing for much high accuracy and milimetre-level errors of the measurements  - down to milimetre accuracies in static mode.

PPP (precise point positioning) is relatively new, and, like RTK, allows for real-time corrections. 
Unlike RTK, PPP uses corrections from a network of global reference stations directly obtained from the GNSS networks; no need for a temporary base or fixed reference! Accuracies down to a few centimetres can be achieved. See e.g. {cite:t}`luoAssessingBenefitsGalileo2021` for more information.

This tutorial only covers RTK and PPK modes - feel free to [contribute and suggest revisions that include the PPP workflow](https://github.com/unisvalbard/gnss-compendium/edit/master/GNSS_acquisition.md).

```

## Create a new job

All measurements belonging to the same project should ideally be collected together.
Leica Captivate uses **Jobs** for this.
Switching between jobs and creating new jobs is relatively simple.
To switch between jobs, simply swipe until the right one is in the centre of the screen.
New jobs are created by clicking on **Jobs**, then proceeding to clicking **New**.
It is also in this screen that you can edit or delete jobs.

```{admonition} Available through YouTube.
:class: seealso
<iframe width=100% height=400 src="https://www.youtube.com/embed/ibuUVsF1R0c" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
```

All jobs should be provided with a **Name**, **Description**, and information on the **Creator**.
Finally, make sure to collect the correct **Coordinate system**; **WGS 1984** typically works in Svalbard, but may also be replaced with **EUREF89**.

```{admonition} No height reference model available!
:class: warning

Svalbard for the time being lacks a height reference model.
Data may, as such, be off from *reality*; e.g., shoreline data may actually be reported as significantly above or below 0 metres.
Hopefully, this will become available in the next few years.
Until then, one may use the global [Earth Gravitational Model (EGM) 2008](https://earth-info.nga.mil/index.php?dir=wgs84&action=wgs84) for corrections.
```

With the project correctly set up, you can start with the collection of data.
The next few sections help with the setup of real-time kinematics corrections, aided by control station data.
If this is of no interest, skip ahead to the section on data acquisition and post-processing kinematics.

## Real-time kinematics

Real-time kinematics (RTK) enable the live-integration of reference data to correct positional errors down to centimetres.
Typically, RTK correction data is provided by a control station within a 10-15 kilometre range.
Measurements beyond this range suffer exponentially increasing errors, reducing the effectiveness of performing differential measurements.
In Svalbard, Kartverket operates control stations in both Longyearbyen and Ny Ålesund - high-precision GNSS data acquisition elsewhere requires the use of mobile base stations and/or post-processing kinematics (PPK).

### WLAN connection

Svalbard's real-time corrections are available through Kartverket's NTRIP services.
However, the Leica Captivate controllers need internet access for this to work.
The easiest is to set up a local hotspot with your phone, then connect to the hotspot with Leica Captivate.

```{admonition} Available through YouTube.
:class: seealso
<iframe width=100% height=400 src="https://www.youtube.com/embed/shBbYNHp4K8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
```

Proceed to the **Connections (1)** screen, then select **Internet wizard (5)**.
Select **WLAN**, and search for your mobile hotspot (in the video referred to as *mobile internet*).
Sign in with the hotspot credentials, then continue with the connection test.
If all went well, you return to the **startup screen**.

### NTRIP Svalbard

After successfully connecting Leica Captivate to the internet, you can configure the NTRIP service.
Below is an overview of the key parameters, though an up to date list is available at [https://www.kartverket.no/til-lands/posisjon/brukerveiledning-posisjonstjenester](https://www.kartverket.no/til-lands/posisjon/brukerveiledning-posisjonstjenester).

**IP address:**
```
159.162.103.14
```

**Port:**
```
2101
```

**Mountpoint:**
```
SVALBARD
```

**GNSS-system:**
```
GPS+GLO
```

```{admonition} Available through YouTube.
:class: seealso
<iframe width=100% height="400" src="https://www.youtube.com/embed/FKqjSqGYeYY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
```

Once again proceed to **Connections (1)**, then head over to **RTK rover wizard (3)** to configure the RTK services.
Either **Create a new profile**, or select **Edit an existing profile** to update the existing configuration.
The pre-configured *Kartverket* RTK profile used the parameters above and successfully connects to the Svalbard NTRIP service.
Make sure to specify **WLAN** as the RTK device connection; this is after all what is used to connect to the internet.
Double check the **Network name**, making sure this is the same name as previously specified for the mobile hotspot.
Then specify the RTK server IP address, the mountpoint, tick the checkbox to **Receive RTK corrections from RTK network**, using the *Nearest* **Network type**.

```{admonition} Login prompted?
:class: tip
The username and password for Kartverket's NTRIP service in Svalbard are the same as those used for the Kartverket data download services.
Ask the UNIS Arctic Geology GIS admin for the credentials.
```

RTK corrections are transmitted in the *RTCM v3* format, and use an automated coordinate system.
Finally, test the connection; hopefully all checkboxes are successfully checked.

```{admonition} Available through YouTube.
:class: seealso
<iframe width=100% height="400" src="https://www.youtube.com/embed/3CebRc33RUQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
```

Leica Captivate should now be running in RTK mode.
The enabled configuration can be easily checked by using the *RTK Data Link*; i.e., simply click the smartphone icon.
The **RTK Data Link menu** also allows you to enable and disable the connection, and provides an overview of successfull corrections in the past minute.

## Data Acquisition in rover mode

Prior to pressing *Measure*, fill out the target ID and double check the antenna height.
The target ID should be unique for each measurement.

Both RTK and *raw* data acquisition (for PPK) follow roughly the same procedures for conducting measurements.
The main difference is that RTK data comprises both correction data and raw data; reflected in the measurement screen where the RTK positions count is shown.
When measuring raw data over a target, make sure to collect at least 30 seconds worth of data - with longer measurements generally resulting in better results.
A handy timer shows how long the instrument has been recording for the current measurement.

`````{tab-set}
````{tab-item} RTK Measurement
```{admonition} Available through YouTube.
:class: seealso
<iframe width=100% height="400" src="https://www.youtube.com/embed/oNelh531vFg" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

The quality warning may be ignored if you wish to use the data for PPK.
```
````

````{tab-item} Raw Measurement
```{admonition} Work in progress
:class: warning

This will be updated when ready :)

For now, please follow the RTK Measurement video on the other tab.
```
````
`````

```{admonition} Double checking parameters & saving.
:class: warning

Make sure to double check the antenna height for each measurement.
This is impossible to double check after the field campaign!

Also make sure that each point is saved before moving on to the next point.
You may have to press *Store* when not explicitly asked to store the data.
```

(software:setup:base)=
## Data acquisition in base station mode

Data acquisition in base station mode is detailed in section {ref}`hardware:setup:base`.
{ref}`hardware:setup:base` also shows how to set up the base station through the Captivate software.

When relying on a temproary base, it is important to have the base station running for at least an hour before and after the first, respectively last rover measurement.
Also make sure to store the Raw GNSS base station measurements on the base station SD card, and plug in the external battery while running it over longer amounts of time.

Base station data are written to the **DBX** folder on the SD card.
The file name consists of the *Point ID* specified in base setup and a datetime stamp, in the .M00 format.
These files should be imported to Leica Infinity (see {ref}`software:importing:infinity`) and marked as reference data when applying PPK.

## Post-processed kinematics

Post-processing kinematics (PPK) involves applying corrections after measuring of the GNSS data.
This typically involves downloading the control station data as reference data (*base*) for the correction of raw data acquired from the *rover*.
Not much can be done in the field for this, except for collecting the raw data at 1 Hz frequencies.

```{admonition} Did you know?
:class: suggestion

One of the Leica GS sensors can be set to *base* station mode while using the other to record *rover* data.
The *base* station data recorded in this way can be used as a substitute for Kartverket data, especially when recording data 10-15 km away from the nearest station.
See {ref}`hardware:setup:base` and {ref}`software:setup:base` on how to set things up.
```

