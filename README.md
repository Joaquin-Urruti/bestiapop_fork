# BestiaPop: A python script for climate data extraction and processing

Climate data is an essential input for crop models to predict crop growth and development using site-specific (point) or gridded climate data. While *point* data is currently available in MET format, gridded data is provided in NetCDF file format which is difficult to store and convert to an input file readable by [APSIM](https://www.apsim.info) or other crop models. We developed **bestiapop** (a spanish word that translates to *pop beast*), a Python script (*soon to become a package*) which allows model users to automatically download SILO's (Scientific Information for Land Owners) gridded climate data in MET file format that can then be consumed by APSIM for **crop modelling predictions**. The package offers the possibility to select a range of grids (5 km × 5 km resolution) and years producing various types of output files: csv, APSIM and soon TSV and SQLite.

Although the code downloads data from SILO (https://www.longpaddock.qld.gov.au/silo/gridded-data/), it could be applied to other climate data sources. So far, the code is producing CSV or MET files to be used by APSIM (https://www.apsim.info/), however, it also could be applied to produce input climate data for other crop models such as DSSAT and STICS.

### More information

https://www.jojeda.com/project/project-6/

## Installation

1. Clone this repo
2. Install required packages.

### Using pip

1. Change directory to the repo folder
2. `pip install -r requirements.txt`

### Using Anaconda

#### In you Base Environment

This option might take a *very* long time due to the multiple dependencies that Anaconda might have to solve on your default **base environment**. Preferably, install using the next method which creates a custom environment.

1. Open your anaconda prompt for the *base* environment (default)
2. `conda install -y -c conda-forge --file requirements.txt`

#### Create Custom Environment

1. `conda create -y --name bestiapop python==3.7`
2. `conda install --name bestiapop -y -c conda-forge --file requirements.txt`
3. `conda activate bestiapop`

## Usage

### Examples

#### Download a SILO climate file for year 2015 and the daily_rain variable

This command will **only** download the file from AWS, it won't do any further processing.

```powershell
python bestiapop.py -a download-silo-file -y 2015 -c daily_rain -o C:\some\output\folder
```

#### Process file 2015.daily_rain.nc for a range of lat/lon

```powershell
python bestiapop.py -a convert-nc4-to-csv -y 2015 -c daily_rain -lat "-41.15 -41.05" -lon "145.5 145.6" -o C:\some\folder
```

#### Generate MET output files for Radiation, Min Temperature, Max Temperature and Daily Rain for years 2015 to 2016

Note: the resulting MET files will be placed in the output directory specified by "-o"

Note: add "-ou csv" at the end of the script if a csv is required as output file. The code generates MET files by default.

```powershell
python bestiapop.py -a generate-met-file -y "2015-2016" -c "radiation max_temp min_temp daily_rain" -lat "-41.15 -41.05" -lon "145.5 145.6" -o C:\some\output\folder
```

## Main References (The following papers implemented this code and can be used as references)

1. Ojeda JJ, Eyshi Rezaei E, Remeny TA, Webb MA, Webber HA, Kamali B, Harris RMB, Brown JN, Kidd DB, Mohammed CL, Siebert S, Ewert F, Meinke H (2019) Effects of soil- and climate data aggregation on simulated potato yield and irrigation water demand. Science of the Total Environment. 710, 135589. doi:10.1016/j.scitotenv.2019.135589
2. Ojeda JJ, Perez D, Eyshi Rezaei E (2020) The BestiaPop - A Python package to automatically generate gridded climate data for crop models. APSIM Symposium, Brisbane, Australia.

## Package references

1. https://registry.opendata.aws/silo/ 
2. https://towardsdatascience.com/handling-netcdf-files-using-xarray-for-absolute-beginners-111a8ab4463f
3. http://xarray.pydata.org/en/stable/dask.html 
