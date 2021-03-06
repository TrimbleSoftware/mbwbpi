MBWBPI (MeteoBridge WetBulb PlugIn)

Meteobridge user defined weatherstation plugin to accurately calculate the wetbulb tempature from other Meteobridge physical weather sensors and output data on virtual sensors that are related to the calculated wetbulb temperature. The wetbulb temerature is of particular interest to snowmaking and snow percipitation forcasting.

This plugin is implemented as a rather sophisticated AWK script that uses the Newton-Raphsen iterative method to accurately calculate the wetbulb tempature from the data furnished by other Meteobridge sensors.

The method to calculate the wetbulb tempature is adapted from the javascript code in the page source from this MWS webpage:

    https://www.weather.gov/epz/wxcalc_rh

The plugin has configurable options that are stored in the Openwrt UCI style configuration file named "mbwbpi". The following settings are configurable:

    mb_cmd: The os command to extract the sensor data from Meteobridge needed to calculate the wetbulb temperature into a tab delminted list
    logfile: The location of a logfile to wite messages to
    pollsleep: The interval in seconds the sensors are polled and the sensor data is output
    writelog: This is a flag to cause messages to be written to the logfile
    snowmaking: This is a flag to cause the output of a snowmaking rank on data1 sensor

See the comments in the config file for more infomation.

This script also does an initial sleep to start its data gathering on an even polling time interval. For example if the polling interval is set to 60 seconds, the polling will start (and reoccure) on even minute intervals.

Sensor output:

        t0: The calculated wetbulb temerature is output as sensor t0 in Celcius.
        data0:  A flag as sensor data0 is also output with a value of 1 when the wetbulb temerature is low enough for snow. The flag is output as 0 if no snow is                     possible based on the wetbulb temperature.
        data1:  An configurable "optional" sensor to output a snowmaking ranking. Possible ranking value outputs are:
                    2: good (dry snow)
                    1: marginal (wet snow)
                    0: not possible
                    
                The rankings are based on this logic:
                    wetbulb temerature <= -7.0 °C outputs a value of 2 (good snowmaking)
                    wetbutb temerature > -7.0 °C AND wetbulb temp  <= -3.0 °C outputs a value of 1 (marginal snowmaking)
                    wetbulb temerature > -3.0 °C outputs a value of 0 (snowmaking not possible)

To install on your Meteobridge PRO, NANO SD, RPI3 or RPI4 Meteobridge weather server:

1) Download the code (two files: mbwbpi.plugin and mbwbpi) from this repository and place these files into the "Scripts" folder share on your Meteobridge weather server.
2) Edit the configuration file (mbwbpi) as needed. In most cases the defaults for the Primary Station should work. If you need to get the sensor data from other stations/sensors, edit the "option <b>mb_cmd</b>" line inside the "template=[th0temp-act]..." area to the approiate sensor names for you installation.
3) From the Station tab on the Meteobridge web interface, select the "Station" tab and then the "Add Weather Station" button.
4) Select the the "User-Defined" entry from the Model: pulldown list.
5) Select the "script:mbwbpi" entry from the Plug-in: pulldown list
6) Select the "no restart of logger when lacking data from this station" checkbox.
7) Click on the "Save" button. (Ignore the error message the "Error (Station #x): Download of plugin script failed: No such file or directory". This seems to a superflous error and the plugin will be added to Meteobridge anyway.)
8) Check the "System/Logging" tab to see timestamped messages written to the logfile by the plugin (if logging is enabled) or the Live "Data/Raw Sensor Data" tab to see the wetbulb tempature and snowable data flag and optional snowmaking rank.

Meteobridge forum topic: https://forum.meteohub.de/viewtopic.php?f=61&t=15468

For more information on Meteobridge weather server visit this page: https://www.meteobridge.com/wiki/index.php/Home
