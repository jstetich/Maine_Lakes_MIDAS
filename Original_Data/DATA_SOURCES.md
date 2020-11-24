# Data Sources 

## Maine Lakes and Ponds
Maine Geolibrary / Maine Office of GIS no longer provides a lakes data layer
containing the MIDAS numbers of all Maine lakes. They refer users to the
National Hydrography Dataset for all hydrologic features, but the National
Hydrography Database does not contain MIDAS numbers.

We need the MIDAS numbers to connect water quality monitoring data unambiguously
with specific Maine Lakes, because many Maine lakes have similar names.

Geospatial Data in Maine lake centroids was downloaded as a KMZ file from
Maine DEP's website by Curtis C. Bohlen on November 23, 2020, as follows:

Maine DEP's Maps and Data Links page shows "Maine Lake Information" with the
notice "Updating-Returning Soon", but data has been unavailable there for
several months. Data is still accessible as a KMZ file through
an undocumented link here:
https://www.maine.gov/dep/gis/datamaps/lawb_lakes/lakes_and_ponds.kmz

The resulting KMZ file is lakes_and_ponds.kmz

Alternatively, a similar file, `Maine_DEP_Lake_Information.kmz`, can be 
accessed through IF&W here:
https://www.maine.gov/ifw/fishing/kml/Maine_DEP_Lake_Information.kmz

The DEP and DMR links appear to provide access to similar files, but they
are not identical, differing slightly in length. Unzipping either `.kmz`
file reveals a `.kml` file, named simply `doc.kml`, containing point
features, apparently lake centroids, with MIDAS numbers and other
identifying information.

### Data Format
`KML` is a flavor of `XML` devised specifically for geospatial data.  `KML`
files are fairly easy to parse using KML and HTTP parsing tools, at least for
point features.  We use python scripts to parse the data to CSV files (details
below).

Within each KML file, each lake is represented as a Placemark, (usually) 
containing the following tags:

*  name  
*  visibility  
*  Snippet  
*  description
*  styleUrl  
*  Point 

We are interested in the  <Point> and <description> tags.

The Point tag contains geographic coordinates (in longitude and latitudes, WGS
1984). 

The <description> tag contains an HTML table with the following entries, each
in a separate row of the table:
*  Name
*  Town
*  MIDAS Number
*  Elevation
*  Notes
*  Name Change

### Extracting data
The data in the `KML` file can be extracted using a python (3) script,
`DataParserLakes.py`. Further details on data extraction and preparation
are included in the `DATA_NOTES.md` file in the `Derived_Data` folder.