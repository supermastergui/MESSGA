Link: [https://vrc.rosscarlson.dev/docs/single_page.html](https://vrc.rosscarlson.dev/docs/single_page.html)

# Appendix F - The .sct2 Sector File Format
Starting with version 1.1, VRC supports two extensions to the standard sector file format. The two new sections are called Regions and Labels. Other than these two new sections, .sct2 files are identical to .sct files.

## Regions
Regions are used to define areas on the scope which are filled with a solid color. These filled polygons can be used to depict many different things in a sector such as special-use airspace, airways, ground maps, bodies of water, etc.

To define regions in a .sct2 sector file, create a [REGIONS] section. You can create an unlimited number of regions within the section. Each region consists of a color definition and a series of lat/lon points. A region definition ends when a new region definition begins, or when a new section begins.

Here's an example [REGIONS] section with a single region definition:

```
[REGIONS]
Grey    N042.27.51.070 W071.17.09.758
        N042.27.51.390 W071.17.14.849
        N042.28.08.310 W071.17.24.907
        N042.28.08.332 W071.17.25.163
        N042.28.09.203 W071.17.24.997
        N042.28.04.609 W071.16.38.186
        N042.28.03.796 W071.16.39.158
        N042.27.53.179 W071.16.40.814
        N042.27.55.692 W071.17.12.498
        N042.27.54.263 W071.17.12.782
        N042.27.53.896 W071.17.09.334
```

The first line of a region definition contains the color code, followed by the first point on the polygon. Each additional line must start with one or more spaces, followed by the lat/lon for the next point on the polygon.

You do not need to duplicate the start point at the end of the list of points. VRC will automatically close the polygon.

Following is another example [REGIONS] section with multiple region definitions. The third region uses a numeric color code instead of a color code specified by a #define line earlier in the sector file:

```
[REGIONS]
Grey    N042.27.51.070 W071.17.09.758
        N042.27.51.390 W071.17.14.849
        N042.28.08.310 W071.17.24.907
        N042.28.08.332 W071.17.25.163
        N042.28.09.203 W071.17.24.997
        N042.28.04.609 W071.16.38.186
        N042.28.03.796 W071.16.39.158
        N042.27.53.179 W071.16.40.814
        N042.27.55.692 W071.17.12.498
        N042.27.54.263 W071.17.12.782
        N042.27.53.896 W071.17.09.334
Orange  N042.27.48.816 W071.17.49.520
        N042.27.43.829 W071.17.54.595
        N042.27.42.910 W071.17.52.948
        N042.27.47.929 W071.17.47.903
255     N042.28.06.190 W071.17.03.084
        N042.28.05.308 W071.16.53.951
        N042.28.02.294 W071.16.54.466
        N042.28.03.155 W071.17.03.674
```

## Labels
Labels are simple static text strings drawn at a specified lat/lon on the scope. They can only be one line of text, and they're always drawn in the same font as the navaid names. These labels are useful for identifying various items in the sector such as MVAs, taxiway names, special-use airspace, etc.

To define one or more labels in your .sct2 sector file, add a [LABELS] section. You can define an unlimited number of text labels in this section. Each line creates a new label. Here's an example [LABELS] section:

```
`[LABELS]
"Bogus MOA" N042.27.47.929 W071.17.47.903 MOAColor
"This label is red" N045.00.00.000 W072.00.00.000 255
"C" N046.00.00.000 W072.00.00.000 Taxiway
```

The line starts with the actual text of the label, which must be enclosed in double quotes. This is followed by the lat/lon for the location where you want the label to be printed. The last field is the color definition for the label. Each label can be a different color.

# Appendix G - Sector File Formatting Requirements
This page documents the formatting requirements for .sct and .sct2 sector files. The rules specified here apply specifically to VRC. Other radar client programs may be more or less strict than VRC in terms of formatting.

## General Information
VRC supports two formats, known as the .sct and .sct2 formats. The .sct format existed prior to the development of VRC and is supported by other radar clients such as ASRC and ProController. The .sct2 format was introduced with VRC 1.1 and adds two new sections to the file, namely the [REGIONS] and [LABELS] sections, which are described below.

Note that if you use the new [REGIONS] and [LABELS] sections in a .sct file, VRC will reject the file with a syntax error. ASRC will most likely still load the file, but you will often get undesired results. This is because ASRC will ignore the [REGIONS] and [LABELS] section headers and treat the region and label entries as though they were a continuation of the previous section, whatever it may be. This is why you should never use [REGIONS] and [LABELS] sections in a .sct file. Use them only in .sct2 files.

### Comments
Comments are lines which are ignored by the radar client and are only meant to be a note or reminder for sector file authors and maintainers. To place a comment in a sector file, precede the comment text with a semicolon. For example, the first line of the following sector file excerpt is a comment indicating that the following lines comprise the Runway 4R/22L centerline:

```
;RUNWAY 4R/22L - Centerline
 N042.21.18.037 W071.00.35.552 N042.21.19.173 W071.00.35.002 LTGREY
 N042.21.21.797 W071.00.33.736 N042.21.22.932 W071.00.33.186 LTGREY
 N042.21.19.891 W071.00.34.657 N042.21.21.026 W071.00.34.108 LTGREY
 N042.21.23.664 W071.00.32.832 N042.21.24.800 W071.00.32.283 LTGREY
 N042.21.27.264 W071.00.31.095 N042.21.28.251 W071.00.30.612 LTGREY
 N042.21.25.209 W071.00.32.083 N042.21.26.345 W071.00.31.534 LTGREY
 N042.21.31.215 W071.00.29.178 N042.21.32.351 W071.00.28.629 LTGREY
```

Comments can also appear at the end of a line after actual data, like so:

```
[AIRPORT]
KBOS 128.800 N042.20.54.750 W071.00.21.920 C ; LOGAN INTERNATIONAL AIRPORT
KACK   0.000 N041.15.10.991 W070.03.36.652 E ; NANTUCKET MEM
KBED   0.000 N042.28.11.831 W071.17.20.512 E ; LAURENCE G HANSCOM FLD
```

### Blank Lines
Blank lines are ignored by the sector file parser, so they are acceptable.

### Coordinate Formatting
Every section uses latitude and longitude coordinate formatting. To specify a coordinate, you provide both the latitude and longitude for the point, using degrees, minutes, seconds, and decimal seconds. These values are separated by a decimal point. Latitudes must be prefixed with an N or an S, for latitudes north or south of the equator, respectively. Longitudes must be prefixed with a W or an E, for longitudes west or east of the prime meridian (zero degrees longitude,) respectively. Examples of this formatting can be found throughout this document.

Note that for some sections, a coordinate can also be specified by using a navaid identifer, such as the identifier for a VOR, NDB, FIX (intersection) or airport. In that case, the latitude and longitude for the specified navaid will be used to draw the given item. This is handy for drawing airways or procedures that use navaids as waypoints on the procedure. An example of this formatting is shown in the [LOW AIRWAY] section description below.

### Color Definitions
Sector file colors are defined by a number representing the red, green and blue components of a color. This number is a 24 bit integer where the leftmost 8 bits are the blue color, the middle 8 bits are the green color, and the rightmost 8 bits are the red color.

To convert from individual 8-bit red, green and blue values (in the range 0-255) into the 24 bit integer format, use the following formula:

```
(BLUE x 65536) + (GREEN x 256) + RED
```

The sector file format provides the ability to define named color macros for use throughout the file. This allows you to assign the same named color to a collection of line segments and be able to change their color by just changing the numeric value of the color definition, instead of having to update the color value for each line segment individually. Named color definitions can be used anywhere a color value can be used. Color definitions must appear at the top of the sector file before any section header. Each color definition must appear on a separate line. Each one must consist of the keyword "#define", followed by the color name, followed by the numeric value. Examples:

```
``#define Black 0
#define Maroon 128
#define Green 32768
#define Olive 32896
#define Navy 8388608
#define Purple 8388736
#define Teal 8421376
#define grey 8421504
#define Silver 12632256
#define Red 255
#define Lime 65280
#define Blue 16711680
#define Fuchsia 16711935
#define Aqua 16776960
#define White 16777215
```

### The [INFO] Section
Every sector file must have an [INFO] section. This section defines some basic required parameters about the airspace represented by the sector file. Here's an example:

```
[INFO]
Boston Tower v5.0_FC
BOS_TWR
KBOS
N042.20.54.750
W071.00.21.920
60
45
16
1
```

The first line defines the name of the sector file. In VRC, this is shown in the controller data at the bottom of the controller list when you click on a controller.

The second and third lines are the default callsign and the default airport for the sector. These are ignored by VRC.

The fourth and fifth lines are the latitude and longitude of the default sector center point. This is where your scope will be centered when first opening the sector file.

The sixth and seventh lines represent the number of nautical miles per degree of latitude and longitude, respectively. The first of these two should normally be 60, since lines of latitude are always parallel. The second value will decrease the further the sector is from the equator, because lines of longitude converge as you move towards the poles. These two values are used to "squeeze" the sector data display so that it appears normal on the scope.

The eighth line is the magnetic variation for the sector. This is used to rotate the display on the scope so that runways and aircraft ground tracks are aligned relative to magnetic north.

The ninth line is a sector scale value, which is ignored by VRC.

### The [VOR] Section

This section defines all the VORs in the airspace. Each VOR must be on a separate line. Each line must contain the VOR identifier, followed by the VOR frequency, followed by the latitude, followed by the longitude. These four values must be separated by at least one space. Example:

```
[VOR]
BOS 112.700 N042.21.26.852 W070.59.22.377
LWM 112.500 N042.44.25.512 W071.05.41.435
PUT 117.400 N041.57.19.652 W071.50.38.755
PVD 115.600 N041.43.27.600 W071.25.46.700
ORW 110.000 N041.33.23.045 W071.59.57.701
SEY 117.800 N041.10.02.772 W071.34.33.900
```

## The [NDB] Section

This section defines all the NDBs in the airspace. The formatting is identical to the [VOR] section.

## The [AIRPORT] Section

This section defines all the Airports in the airspace. Each airport must be on a separate line. Each line must contain the airport identifier, followed by the tower frequency, followed by the latitude, followed by the longitude, and finally the class of airspace in which the airport lies. These five values must be separated by at least one space. Example:

```
[AIRPORT]
KBED 118.500 N042.28.11.831 W071.17.20.507 D
KBOS 128.800 N042.21.86.000 W071.00.31.000 B
KBVY 125.200 N042.35.03.015 W070.54.59.465 D
KFIT 122.800 N042.33.14.839 W071.45.32.243 E
KLWM 120.000 N042.43.01.927 W071.07.24.306 D
K1B9 122.800 N042.00.00.360 W071.11.48.360 E
K3B2 122.800 N042.05.53.240 W070.40.19.480 E
K2B2 122.800 N042.47.45.330 W070.50.28.186 E
KOWD 126.000 N042.11.26.868 W071.10.23.174 D
K6B6 122.800 N042.27.37.633 W071.31.04.492 E
```

### The [RUNWAY] Section

This section defines all the runways for all airports in the airspace. Each runway definition must be on a separate line. A runway definition is comprised of the following eight space-separated fields:

Runway number with an optional L, R, or C for Left, Right or Center.
Runway number for the opposite end.
Magnetic runway heading.
Magnetic runway heading for the opposite end.
Latitude of the runway start point.
Longitude of the runway start point.
Latitude of the runway end point.
Longitude of the runway end point.
Here's an example showing the runways for three different airports. The comments indicating the airport code are not required:

```
[RUNWAY]
;KBOS
04L 22R 000 000 N042.21.28.760 W071.00.51.620 N042.22.41.850 W071.00.16.260
04R 22L 036 216 N042.21.03.813 W071.00.42.462 N042.22.36.841 W070.59.57.449
09  27  000 273 N042.21.20.718 W071.00.46.415 N042.21.36.781 W070.59.15.738
14  32  000 332 N042.21.23.750 W071.01.23.790 N042.20.54.960 W071.00.29.690 
15L 33R 000 000 N042.22.24.880 W071.00.32.860 N042.22.06.970 W071.00.08.850
15R 33L 151 331 N042.22.27.380 W071.01.04.410 N042.21.16.740 W070.59.29.710
;KBED
05  23  000 000 N042.27.48.374 W071.17.48.723 N042.28.28.585 W071.17.07.598
11  29  113 293 N042.28.18.566 W071.18.01.273 N042.28.09.979 W071.16.28.582
;KBVY
09  27  000 000 N042.34.47.779 W070.55.31.803 N042.34.59.660 W070.54.29.902
16  34  156 000 N042.35.31.005 W070.55.18.939 N042.34.55.610 W070.54.39.641
```

### The [FIXES] Section

The fixes section defines all the named VOR radial intersections or GPS waypoints in the airspace. Each fix definition must be on a separate line. Each line must contain the fix name, followed by the latitude of the fix, followed by the longitude. These fields must be separated by at least one space. Example:

```
[FIXES]
WINNI N042.07.01.710 W071.07.28.220
NABBO N042.11.42.679 W071.05.13.200
MILTT N042.16.25.455 W071.02.56.879
SWIGG N042.31.58.570 W071.14.37.409
WOBUR N042.28.39.700 W071.09.53.360
MALDY N042.25.45.879 W071.05.45.729
CELTS N042.12.47.070 W070.48.52.499
NOLEY N042.35.02.400 W070.53.45.600
WYANE N042.31.49.349 W070.55.29.210
VOCUS N042.27.07.347 W070.57.47.878
```

### The [ARTCC] Section

This section is used to define major ARTCC/FIR boundaries. Each line defines a single line segment. The line must consist of the name of the boundary that this segment is part of, followed by the latitude and longtitude of the start and end points of the line segment. These five fields must be separated by at least one space. The name is not actually used by VRC, but it must be included for backwards compatibility with older radar clients. The name cannot contain any spaces. Example:

```
[ARTCC]
KZBW    N043.38.00.000 W076.47.30.000 N044.06.15.000 W076.25.00.000
KZBW    N044.06.15.000 W076.25.00.000 N044.10.00.000 W076.20.00.000
KZBW    N044.10.00.000 W076.20.00.000 N044.12.15.000 W076.17.00.000
KZBW    N044.12.15.000 W076.17.00.000 N044.12.15.000 W076.14.00.000
KZBW    N044.12.15.000 W076.14.00.000 N044.14.00.000 W076.11.00.000
KZBW    N044.14.00.000 W076.11.00.000 N044.17.30.000 W076.08.00.000
KZBW    N044.17.30.000 W076.08.00.000 N044.19.20.000 W076.04.00.000
KZBW    N044.19.20.000 W076.04.00.000 N044.21.00.000 W076.00.00.000
KZBW    N044.21.00.000 W076.00.00.000 N044.20.50.000 W075.57.00.000
KZBW    N044.20.50.000 W075.57.00.000 N044.26.45.000 W075.49.00.000
KZBW    N044.26.45.000 W075.49.00.000 N044.30.45.000 W075.46.00.000
KZBW    N044.30.45.000 W075.46.00.000 N044.43.00.000 W075.30.00.000
KZBW    N044.43.00.000 W075.30.00.000 N044.40.00.000 W075.42.00.000
KZBW    N044.40.00.000 W075.42.00.000 N044.49.00.000 W075.45.00.000
```

### The [ARTCC HIGH] Section

This section is identical to the [ARTCC] section. It is typically used to define high-altitude ARTCC sector boundaries. It exists as a separate section so that it can be toggled on/off separately by the user.

### The [ARTCC LOW] Section

This section is identical to the [ARTCC] section. It is typically used to define low-altitude ARTCC or TRACON sector boundaries. It exists as a separate section so that it can be toggled on/off separately by the user.

### The [SID] and [STAR] Sections

These sections are used to define SID (Standard Instrument Departure) and STAR (Standard Terminal Arrival Route) diagrams, which can be toggled on/off individually by the user as needed. They are also commonly used to define IAPs (Instrument Approach Procedures) as well as vectoring diagrams, sector video maps, and even complex airport diagrams. In VRC, the items defined in these sections are collectively referred to as "Diagrams" and each one can be toggled on/off via the Diagrams Window. The Diagrams Window contains two lists, one for the diagrams defined in the [SID] section, and one for the diagrams defined in the [STAR] section. It doesn't matter what type of diagrams you place in each section.

These sections are somewhat unique in that the formatting requirements incorporate both a fixed-width field and space-delimited fields. An individual diagram consists of one or more lines in the sector file. Each line defines a single line segment in the diagram. The first line of the diagram definition contains the name of the diagram. The name field must be exactly 26 characters in length. If the name of the diagram is shorter than 26 characters, trailing spaces must be added to fill the 26 characters. After the first 26 characters, there can be one or more optional spaces, followed by the latitude and longitude of the start and end points of the line segment, followed by an optional color name or value. If no color name or value is given, the diagram will be drawn using the default SID or STAR color as defined in the radar client settings.

Subsequent lines in a diagram definition must have 26 spaces, followed by the latitude and longitude for the start and end points of the current line segment, followed by an optional color name or value. In other words, subsequent segment definitions are identical to the starting segment definition, except that only the starting segment contains the name of the diagram in the first 26 characters. VRC will continue reading lines and adding them to the current diagram definition until it encounters the start of a new diagram (signified by a name present in the first 26 characters) or the start of a new section.

In the following example, two diagrams are defined. One is the Gardner Three (GDM3) arrival into KBOS, and the other is the Woons One arrival into KBOS. These examples illustrate how navaid names can be used in place of latitude and longitude values.

```
GDM3                      JFK            JFK            ALB            ALB
                          ALB            ALB            GDM            GDM
                          GDM            GDM            BRONC          BRONC
                          BRONC          BRONC          LOBBY          LOBBY
                          LOBBY          LOBBY          REVER          REVER
WOONS 1                   ORW            ORW            N041.41.45.919 W071.49.33.180
                          N041.41.45.919 W071.49.33.180 N041.50.35.440 W071.38.31.350
                          N041.50.35.440 W071.38.31.350 N041.54.19.190 W071.33.50.390
                          N041.54.19.190 W071.33.50.390 N041.57.02.070 W071.30.25.339
```

### The [LOW AIRWAY] and [HIGH AIRWAY] Sections
These sections are used to define low altitude and high altitude airways. The formatting is identical to the [ARTCC] section. The name of the airway segment is drawn on the scope at the center point of the segment, when the associated airway is toggled on by the user. Navaid names can be used in place of latitude and longitude values. Example:

```
[HIGH AIRWAY]
J6                        PLB            PLB            N043.26.52.640 W073.42.13.780
J6-563                    N043.26.52.640 W073.42.13.780 N042.44.50.180 W073.48.11.500
J6                        N042.44.50.180 W073.48.11.500 SAX            SAX
J16-94                    BOS            BOS            N042.44.50.180 W073.48.11.500
J16-94                    N042.44.50.180 W073.48.11.500 BUF            BUF
J27-80                    BAF            BAF            SAX            SAX
J29                       YHZ            YHZ            BGR            BGR
J29-595                   BGR            BGR            PLB            PLB
J29                       PLB            PLB            SYR            SYR
J29                       SYR            SYR            JHW            JHW
```

### The [GEO] Section
This section is used to define colored line segments for any purpose. It is typically used to define geographic data such as coastlines or major bodies of water, or for other static items such as special use airspace, airport diagrams, etc. Each line in this section defines a single line segment. The line must contain the latitude and longitude of the start and end points of the segment, followed by a color name or value. Example:

```
[GEO]
N042.22.20.725 W071.00.56.951 N042.22.26.825 W071.01.05.129 Taxiway
N042.22.26.825 W071.01.05.129 N042.22.27.869 W071.01.03.707 Taxiway
N042.22.27.869 W071.01.03.707 N042.22.21.769 W071.00.55.529 Taxiway
N042.22.21.769 W071.00.55.529 N042.22.20.725 W071.00.56.951 Taxiway
N043.49.00.200 W078.00.00.000 N043.49.59.998 W076.47.48.998 Restricted
N043.37.51.999 W076.47.48.998 N043.37.51.999 W078.41.26.600 Restricted
N043.49.59.998 W076.47.48.998 N043.37.51.999 W076.47.48.998 Restricted
N036.32.58.596 W075.56.11.558 N036.32.24.803 W075.56.11.558 Coastline
N036.32.24.803 W075.56.11.558 N036.29.10.486 W075.56.11.558 Coastline
N036.29.10.486 W075.56.11.558 N036.28.45.138 W075.56.11.558 Coastline
N036.28.45.138 W075.56.11.558 N036.27.03.755 W075.56.11.558 Coastline
N036.27.03.755 W075.56.11.558 N036.26.29.962 W075.55.37.765 Coastline
N036.26.29.962 W075.55.37.765 N036.26.29.962 W075.54.55.523 Coastline
N036.26.29.962 W075.54.55.523 N036.24.23.231 W075.54.55.523 Coastline
N036.24.23.231 W075.54.55.523 N036.21.08.914 W075.54.55.523 Coastline
N036.21.08.914 W075.54.55.523 N036.15.22.522 W075.52.57.241 Coastline
N036.15.22.522 W075.52.57.241 N036.12.08.204 W075.49.34.475 Coastline
N036.12.08.204 W075.49.34.475 N036.07.46.297 W075.47.36.193 Coastline
N036.07.46.297 W075.47.36.193 N036.05.05.773 W075.47.36.193 Coastline
N036.05.05.773 W075.47.36.193 N036.07.46.297 W075.48.18.436 Coastline
```

### The [REGIONS] Section
This section is only valid in .sct2 files. For the formatting requirements and examples of the [REGIONS] section, refer to Appendix F.

### The [LABELS] Section
This section is only valid in .sct2 files. For the formatting requirements and examples of the [LABELS] section, refer to Appendix F.

