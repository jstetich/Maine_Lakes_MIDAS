# Data Notes

The file `doc.kml` was extracted from the file `lakes_and_ponds.kmz`
by changing is extension to `.zip`, and unzipping in Windows.  We
discarded the graphic file giving the point symbol for lake centroids.

The python (3) script `DataParserLakes.py` scans that `.kml` file and extracts
data on Maine lakes, including location and MIDAS number.  The script
creates the `.csv` file `lakes.csv`.  Both input and output
filenames are hard coded in the script, as are data column names.