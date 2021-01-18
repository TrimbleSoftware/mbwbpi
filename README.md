MBWBPI (MeteoBridge WetBulb PlugIn)

Meteobridge user defined weatherstation plugin to accuratley calculate the wetbulb tempature from other Meteobridge weather sensors.

This plugin is implemented as a rather sophisticated AWK script that uses the Newton-Raphsen iterative method to accuratley calculate the wetbulb tempature from the data furnished by other Meteobridge sensors.

The method to calculate the wetbulb tempature is adapted from the javascript code in the page source from this MWS webpage:

    https://www.weather.gov/epz/wxcalc_rh

The plugin has configurable options that are stored in the OpenWrt UCI style configuration file named "mbwbpi". For example, the polling interval is configurable, the default is 60 seconds. The script also does an initial sleep to start its data gathering on an even polling time interval.

The calculated webbulb temerature is output as sensor t0 in Celcius. A flag as sensor data0 is also output with a value of 1 when the wetbulb temature is low enough for snow. The flag is output as 0 if no snow is possible based on the wetbulb temperature.

To install on your Meteobridge PRO, NANO SD, RPI3 or RPI4 Meteobridge weather server:

1) Download the code (two files: mbwbpi.plugin and mbwbpi) from this repository and place these files into the "Scripts" folder on your Meteobridge weather server.
2) Edit the configuration file (mbwbpi) as needed. In most cases the defaults should work. If you need to get the sensor data from other sensors, edit the "option mb_cmd" line inside the "template=[th0temp-act]..." area to the approiate sensor names for you installation.
3) From the Station tab on the Meteobridge web interface, select the "Station" tab and then the "Add Weather Station" button.
4) Select the the "User-Defined" entry from the Model: pulldown list.
5) Select the "script:mbwbpi" entry from the Plug-in: pulldown list
6) Select the "no restart of logger when lacking data from this station" checkbox.
7) Click on the "Save" button. (Ignore the error message the "Error (Station #x): Download of plugin script failed: No such file or directory". This seems to a superflous error and the plugin should be added to Meteobridge.)
8) Check the "System/Logging" tab to see message written to the log by the plugin or the Live "Data/Raw Sensor Data" tab to see the wetbulb tempature and snowable data flag.

For more information on Meteobridge weather server visit this page: https://www.meteobridge.com/wiki/index.php/Home
