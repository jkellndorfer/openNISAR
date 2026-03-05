# openNISAR
open NISAR Tools by Earth Big Data

These are tools to use with NISAR and some other sensors

## seppo_earthaccess_credentials

Use this program to set your earthaccess credentials environment variables when on an ec2 instance in us-west-2

Run 
```
eval $(seppo_earthaccess_credentials.py -s)
```

## seppo_nisar_earthaccess_search

Use this program to run a search for NISAR products available through earthaccess

Example to get the complete collection of GCOV data as a geojson file:
```
seppo_nisar_earthaccess_search.py --product GCOV --format geojson --output gcov.geojson
```

## Requirements

You need the `earthaccess` package from conda-forge

PIP:
```
pip install earthaccess
```

Mamba or Conda:
```
mamba install -c conda-forge earthaccess
#OR
conda install -c conda-forge earthaccess
```

## DISPLAY NISAR Data directly from s3 urls in QGIS

Here is a quick tip on how NISAR data can be directly displayed in QGIS

You need:
1. a running AWS ec2 instance in `us-west-2`
2. an installation of QGIS on the instance and  the `earthaccess` package installed
3. using the `seppo_earthaccess_credentials.py` program 
4. the s3 url (either obtained from Vertex search or via the `seppo_nisar_earthaccess_search.py` tool

 
### 1. Launching an ec2 instance

We suggest to launch a instance with a good amount of RAM (32 GB)
If you are a SEPPO user, just launch with

```
seppo_setregion us-west-2
sacc r8i.xlarge --autoLogin
```

### 2. Install QGIS on the instance

PIP:
```
pip install qgis earthaccess
```

Mamba (create a new environent)
```
mamba env create -c conda-forge -n qgis qgis earthaccess
```

### 3. Set the earthaccess credentials and launch QGIS

```
conda activate qgis
eval $(seppo_earthaccess_credentials.py -s)
```

### 4.  Open s3 url

in QGIS add a raster file by using this pattern

`NETCDF:/vsis3/<s3url without the s3:// prefix>`

This will open a dialog to pick the h5 variables to load. Note that frequency A takes a while, whereas frequency B HHHH or HVHV for example display rather quickly.





