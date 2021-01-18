MBWBPI (MeteoBridge WetBulb PlugIn)

Meteobridge user defined weatherstation plugin to accuratley calculate the wetbulb tempature from other Meteobridge weather sensors.

This plugin is a rather susisticated AWK script that uses the Newton-Raphsen iterative method to accuratley calculate the wetbulb tempature from the data furnished by other Meteobridge sensors. The plugin has configurable options that are stored in the OpenWrt UCI style configuration file named "mbwbpi". THe polling interval is configurable, the default is 60 seconds. The script also does and initial sleep to start its data gathering on an even polling time interval.

To install on your Meteobridge NANO SD or RPI3 or RPI4 Meteobridge weather server:

1) Download the code (two files: mbwbpi.plugin and mbwbpi) from this repository and place these files into the "Scripts" folder on your Meteobridge weather server.
2) Edit the configuration file (mbwbpi) as needed. In most cases the defaults should work. If you need to get the sensor data from other sensors, edit the mb_cmd line inside the "template=[th0temp-act]..." area to the approiate sensor names for you installation.
3) From the Station tab on the Meteobridge web interface, select the "Station" tab and then the Add Weather Station button.
4) Select the the User-Defined entry from the Model: pulldown list.
5) Select the "script:mbwbpi" entry from the Plug-in: pulldown list
6) Select the "no restart of logger when lacking data from this station" checkbox.
7) Click on the "Save" button. Ignore the error message the "Error (Station #x): Download of plugin script failed: No such file or directory". This seems to a superflous error and the plugin should be added to Meteobridge.
8) Check the System/Logging tab or the Live Data/Raw Sensor Data tab to see the wetbulb tempature.
