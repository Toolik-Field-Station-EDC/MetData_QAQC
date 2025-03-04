# Toolik Meteorological Data QA/QC
Code for quality control and assessment of the Toolik Field Station Meteorological data from main met station (68.628311°N 149.595967°W). Raw files can be made available upon request. As can flagged data files.

The following QA/QC steps are taken:
- Pulls raw data from https://edc.tfs.alaska.edu/metdata/
- Reformats the headers, filters missing or duplicate timestamps
- Filters data for the designated time frame for web upload

The following is a list of QAQC parameters for each sensor. More information can be found embedded in the notebook. 
- Temperature sensors: checked that sensors are within the range of -9 and 37. Otherwise changed to NaN
- Precipitation sensors: vales < 0 are changed to NaN, tipping bucket (rain2_mm_Tot) is changed to 0 for the winter months when there is only snow precipitaiton or and on negative degree days.
- Relative humidity: values of 100-105, changed to 100. If > 105, values are changed to NaN. Values < 0, are changed to 0
- Barometric pressure:  Values < 850 are changed to NaN, graphed to spot outliers
- Windspeed: wind speeds should be within a range of 0-30 m/s. Graphed to spot outliers. std and dir are filtered where the wind rows are removed for erronous data. Removed flatlines in sonics (WS_5m_sonic_Max, WS_5m_sonic_Avg, mean_wing_speed_5m_sonic, mean_wing_direction_5m_sonic, std_wind_dir_sonic
- Lake Temperature: values of all are checked to be within range of -40 to 30
- Lake Level Sensor: values are checked to be within a range of 250 to 400
- Lake PAR: sensor is seasonally removed and values are changed to NaN. Values < 0 are replaced with 0, values > 400 are replaed with NaN
- Evaporation Pan: seasonally removed values are changed to NaN
- UVA and UVB:  sensor is seasonally removed and values are changed to NaN. UVB's range is 0-2. Values < 0 are changed to 0; values > 2 are changed to NaN. UVA's range is 0-50, values < 0 are changed to 0; valeus > 50 are changed to NaN.
- BF5: sensor is seasonally removed and are changed to NaN. Values < 0 are replaced with 0
- SolarkW_Avg/Total solar radiation: values < 0 are replaced with 0. Values > 880 are changed to NaN
- Noramal PAR: Checked within the range of 0 to 1700. Values < 0 are changed to 0
- CNR4/Shortwave or longwave pyranometers looking up and down: All CNR4s have a range of 0 to 900. If < 0, values are replaced with 0. If > 900, values are replaced with NaN.
- Rnet/Net radiation from CNR4 sensors:  Range is -250 to 750. This is graphed to spot outliers.
- Albedo form CNR4 sensors: The range is 0-1. Values < 0 and > 1 are replaced with NaNs.
- VWC Soil:  Range 0-1; Values are removed when Tsoil1 is < 0C
- shf_Avg: graph all the SHF varaibles, they can vary widley. They should all look similar. Spot outliers
- Temperature soil average: Within a range of -10 to 30, replace with NaN if outside.
- Snow Depth:  Values are calibrated up or down based on lowest June value or a field calibration of snow.

Data is exported from this code and uploaded to the Toolik Field Station website here: https://www.uaf.edu/toolik/edc/monitoring/abiotic/met-data-query.php
