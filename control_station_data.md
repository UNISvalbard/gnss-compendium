(base:station:reference:data:download)=
# Downloading base station GNSS data

For post processing of the acquired dGNSS data in the field we require additional data from a base station.
At UNIS we have access to the Longyearbyen base station data ("LYRS") through Kartverket.

## Accessing LYRS base station data

This data can be downloaded through the [Kartverket's etpos website](https://etpos.kartverket.no):

```yaml
etpos.kartverket.no
```

Credentials can either be privately acquired from kartverket, or are available to UNIS students and staff (ask Peter Betlem or Sara Mollie Cohen).
The webportal provides an ftp-like interface, in which files are sorted based on the following syntax:

```yaml
/rnx3/<duration>/<rate>/<year>/<doy>/<name>
```

Herein `<duration>` specifies the data's timeframe, typically either 24h (1 large file per day) or 1h (24 smaller files per day);
`<rate>`, the sampling frequency of the data, typically either 30s (averaged over half a minute interval) or 1s (raw data at 1 Hz frequency);
`<year>`, the year of acquisition;
`<doy>`, the day of the year, starting with 001 for 1 January; and,
`<name>`, the 4-letter code of the ground station, *LYRS* for Longyearbyen.

In general, it is easiest to download the 24 hour interval with 1 second data rate to cover a full day of work.
However, if you know the exact timeframe of data acquisition, specifically targeting 1h timeframes significantly lowers the processing time.

{numref}`etpos_kartverket` shows how to download all required data for a single day, which can be adapted for 1-hour data downloads.
This will need to be done for all days/hours in which location data were acquired in the field.

```{figure} assets/etpos_kartverket.gif
:name: etpos_kartverket

Downloading all required rnx3 data for day 90 of the year 2022.
```

### The Python way of downloading data

The script below provides an alternative way of downloading the data, implementing the Python programming language.
Make sure to specify the usernane, password, data_storage_path and dates.

````{admonition} Required packages
:class: warning

The script requires some additional packages.
These can be easily downloaded through the conda package manager:

```yaml
conda install paramiko -c conda-forge
```

````

```python3
import paramiko
import datetime as dt
from pathlib import Path
import math
import sys

hostname = "etpos.kartverket.no"
username = "" # fill this out
password = "" # fill this out

start_date = "" # fill this out in YYYYMMDD format, e.g. 19th April 2022 = 20220419
end_date = "" # fill this out in YYYYMMDD format, e.g. 19th April 2022 = 20220419
station_short = "LYRS" # 4-letter station name

data_storage_path = "data" # path to where to store the data.

def convert_start_end_dates_to_year_day_of(start_date,end_date):
    start_date = dt.datetime.strptime(start_date, "%Y%m%d")
    end_date = dt.datetime.strptime(end_date, "%Y%m%d")
    return start_date.year, start_date.timetuple().tm_yday, end_date.timetuple().tm_yday

def progressbar(x, y, filename):
    ''' progressbar for the paramiko
    '''
    bar_len = 60
    filled_len = math.ceil(bar_len * x / float(y))
    percents = math.ceil(100.0 * x / float(y))
    bar = '=' * filled_len + '-' * (bar_len - filled_len)
    filesize = f'{math.ceil(y/(1024*1024)):,} MB' if y > 1024 else f'{math.ceil(y/1024):,} KB'
    sys.stdout.write(f'[{bar}] {percents}% {filesize} - {filename}\r')
    sys.stdout.flush()

year, start_day, end_day =  convert_start_end_dates_to_year_day_of(start_date,end_date)

data_storage_path = Path(data_storage_path)
data_storage_path.mkdir(parents=True, exist_ok=True)

with paramiko.Transport((hostname,22)) as transport:
    # SFTP FIXES
    transport.default_window_size=paramiko.common.MAX_WINDOW_SIZE
    transport.packetizer.REKEY_BYTES = pow(2, 40)  # 1TB max, this is a security degradation!
    transport.packetizer.REKEY_PACKETS = pow(2, 40)  # 1TB max, this is a security degradation!
    # / SFTP FIXES
    transport.connect(None,username,password)
    with paramiko.SFTPClient.from_transport(transport) as sftp:

        print("Connection successfully established ... ")
        try:
            for day in range(start_day, end_day, 1):
                sftp.chdir(f'/rnx3/24hour/1sec/{year}/{str(day).zfill(3)}')

                directory_structure = sftp.listdir_attr()
                lyrs = [attr for attr in directory_structure if "LYRS" in attr.filename]

                for attr in lyrs:
                    sftp.get(attr.filename, Path(data_storage_path,attr.filename), callback=lambda x,y: progressbar(x,y, attr.filename))
                    print(f"Downloaded {attr.filename}")
        except Exception as e:
            print("Unable to download selected dates. Check dates or contact Kartverket...")
            print(f"Error: {e}")
            pass

```
