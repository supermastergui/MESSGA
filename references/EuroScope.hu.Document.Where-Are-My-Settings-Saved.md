Link: https://www.euroscope.hu/wp/where-are-my-settings-saved/

Settings Files
Those files contain several different kinds of settings. You can open them with a text editor to learn more since there are many parameters, most of them being self explanatory.

You can specify individual files for the following settings:

Symbology – Here you can find the values from the symbology settings dialog. It describes what colors, sizes, and line styles to be used for the map display.
Ground to air voice channels – You frequencies / voice channels from voice communications setup dialog.
Login profiles – The login profiles from the connect dialog. It contains the callsign, facility, range and ATIS lines.
TAG definitions – The user defined TAG families.
SIL, SEL, DEP, ARR, FP and Conflict list configuration‘ – The definition of the advanced AC lists.
Plug-in settings – any plugin specific settings.
General settings – All lines beginning with m_ are the general settings. You can change them via the Quick SET menu or one of the settings dialogs. I suppose the names here are really readable.
Screen layout – all settings related to the screen layout, which are not stored in the ASR-file.
You can also combine some of those settings into one file, for example you can create a screen layout including lists by using the same file for list configurations and screen layout.

If you have a complete settings file from 3.0 then follow the steps to use them in 3.1:

Open the Settings file setup dialog box.
Enter the file name where your settings are into EVERY group.
Press the LOAD button to load the values into memory.
Then you can save them to individual files (if you want to), or just keep all your settings in one file.
The Profile Files
The profile files are created to store all installation or workstation dependent information. They are not intending to be moved from one workstation to another as there are full paths, video card size information there too. The profile files are just plane text files (it is quite common for EuroScope) with the extension PRF. You can put them to any place in your workstation.

The good thing about saving this data to a file instead of the registry is that you may have as many configurations as you need. All profiles are completely independent from the others (except if they are referencing to the same files). The name of the profile file can also be used as a command line parameter for EuroScope. In this way you can set up as many shortcuts and desktop icons as you need and start the right configuration with a double click.

Only the name of the lastly used profile file and two flags (to indicate auto load and auto save of the last profile) are stored in the registry.

Going into details about the profile file: As the data here came from the registry, it is structured like the registry entries. First the section names after that the key itself. In the file the following information is stored:

LastSession section – It contains data about your last EuroScope session. They are one by one related to the fields in the Connection Settings. The only exception is the ATIS airport and letter that is used in ATIS Connections dialog.
atis_airport0-3 – the four airports served by voice ATIS
atis_letter0-3 – the last time used ATIS letters in your airports
atis_url0-3 – the last time used ATIS extractor URLs for your airports
atis_freq0-3 – the last time used ATIS frequencies for your airports
atis2, atis3, atis4 – the text ATIS message lines (numbered from 2for background compatibility)
callsign – the connect callsign
certificate – your VATSIM ID
connecttype – a code how you connected last time
facility – the facility of the last session
nonvatsim – indicate that last time you connected to EuroScope FSD server
password – the password entered – Important: your password is stored in this file without any encryption.
playback – the last playback file with full path name
proxyserver – the name of the proxy server computer
range – the visual range of the last session
rating – your rating
realname – your real name
scenario – the last use simulation scenario file with full path
server – the lastly connected VATSIM server
simdatapublish – how to publish the simulation data to the server
SimFolder – the folder of the last scan for FSX/P3D SimObjects
tovatsim – Indicates that last time you connected to a VATSIM server
RecentFiles section – It is a simple numbered list of your lastly used ASR files. The files here will be displayed in the SCT menu.
Settings section – In this section there are data about how your environment is set up. What configuration files do be loaded and what hardware elements do you use:
aircraft – full or relative path to the ICAO Aircraft file
airlines – full or relative path to the ICAO Airlines file
airports – full or relative path to the ICAO Airports file
airways – full or relative path to the FSNavigator database
alias – full or relative path to the alias file
AselKey – the aircraft select key code
FreqKey – the primary frequency key code
ipaddr – full or relative path to the VATSIM server descriptor file
sector – the main sector file (as it is from the last session it may be better to put to the Last Session section)
SettingsFiles – full path to the settings files (many installation independent data is stored there)
LoadedPlugIns – full or relative path to the DLL files
Sounds section – Full or relative path of the file names used for voice messages. They are not self-explanatory, just numbered.
Important note: As you see from the above list, your last session username and password are in the profile file. And they are there without any encryption. Therefore, be very careful and DO NOT give, send, share your profiles to anyone else.

ASR Files
The *.asr file contains your current Display Dialog settings. It describes what items are to be displayed from the sector file. It also contains some screen-depending settings and the use of Professional Radar Simulation]].

Once again without the complete description some notes about the lines inside:

SECTORFILE – The path of your current sector file this ASR is used for. When you open an ASR it will look to see if the sector file is loaded or not. If not, then it loads the appropriate one.
SECTORTITLE – Just quick access to the title to show in the popup list.
DisplayTypeName – The name of the screen type. The default value is ‘Standard ES radar screen‘. Others may be created by the plug-ins.
DisplayTypeNeedRadarContent – It indicates that background SCT file elements are drawn for the screen or not.
DisplayTypeGeoReferenced – It indicates if coordinates are latitude/longitude pairs or just pixels.
SHOWC – (value if 1 if checked or 0 if unchecked) “Show Squawk C aircraft” option.
SHOWSB – “Show Squawk STBY aircraft” option.
BELOW – NNNNN. The value if you choose not to display aircraft below NNNNN feet altitude (your floor level). Zero indicates no filter at all.
ABOVE – NNNNN. The value if you choose not to display aircraft above NNNNN feet altitude (your ceiling level). Zero indicates no filter at all.
LEADER – The length of the leader line. Positive values are interpreted as NM, negative as MIN.
SHOWLEADER – Indicates if the leader line should be shown as default or not.
TURNLEADER – It indicates a route following leader line.
HISTORYDOTS – The number of history trails appearing for each aircraft.
TAGFAMILY – The name of the tag family used (generally MATIAS (built in)).
WINDOWAREA – param1:param2:param3:param4 – The geographic coordinates in degrees of the bottom left corner and of the top right corner of the scope. It is important that even if you do not change any settings, just zoom in and out and pan, this value is most likely to be updated. In this way it is quite normal that you will be prompted at nearly all ASR close to decide whether to save or cancel the update of the area.
SIMULATION_MODE – The ID of the simulation mode (professional radar, easy radar and two ground modes).
individual sector file elements – Then follows the list of all your checked items in the display dialog. You cannot save the SECTORLINE and SECTOR elements as they can be switched on just for debugging purposes and not for next session’s display.
Sector Files
Sector files are the files which contain all information about the area you want to control. EuroScope can use the same sector files as ASRC or VRC. There are some places where you should or can modify them.

Runways
The first is the Runway section. It is described in the Quick Start]] page too. You should modify this to be able to display and use the runway data inside EuroScope.

Original:
[RUNWAY]
13L 31R 130 310 N047.26.43.520 E019.15.27.180 N047.25.22.620 E019.17.37.880

Modified to:
[RUNWAY]
13L 31R 130 310 N047.26.43.520 E019.15.27.180 N047.25.22.620 E019.17.37.880 LHBP Ferihegy

GEO section
There is another option for the GEO section. In a ASRC/VRC sector file, GEO lines appear like that:
N036.58.51.798 E008.51.32.509 N036.58.50.305 E008.51.32.422 white

So, in VRC, you can display GEO lines or not but always as a whole. You can display GEO lines or not, in the same manner as with VRC. But EuroScope allows us to define sub-categories in GEO lines by adding a category name at the beginning of each normal GEO line like the one below:
DTKA airport N036.58.51.798 E008.51.32.509 N036.58.50.305 E008.51.32.422 white

And when all lines have been modified the Display Dialog appears like that:


So, you can easily filter which kind of GEO lines appear on your screen, and this avoids overwhelming screen with not useful features.

NOTE: When sector files have been customized for EuroScope, they can’t be used anymore with ASRC or VRC. So, before customizing a sector file for EuroScope, don’t forget to keep an original version for ASRC/VRC users.

In fact, the name is only needed in front of the first line of each subsection. For example, the following [GEO] section works fine:
[GEO]
Red triangle N000.00.00.000 E000.00.00.000 N000.00.00.000 E000.00.00.000
N060.00.00.000 E020.00.00.000 N070.00.00.000 E030.00.00.000 redcolor
N070.00.00.000 E030.00.00.000 N060.00.00.000 E030.00.00.000 redcolor
N060.00.00.000 E030.00.00.000 N060.00.00.000 E020.00.00.000 redcolor

Yellow triangle N000.00.00.000 E000.00.00.000 N000.00.00.000 E000.00.00.000
N062.00.00.000 E024.00.00.000 N066.00.00.000 E028.00.00.000 yellowcolor
N066.00.00.000 E028.00.00.000 N062.00.00.000 E028.00.00.000 yellowcolor
N062.00.00.000 E028.00.00.000 N062.00.00.000 E024.00.00.000 yellowcolor

In EuroScope you will get the two triangles selectable in the Display Settings. This section will also work with ASRC and VRC. The ”N000.00.00.000 E000.00.00.000” coordinates in the lines where the names are would not be needed for ES but since both ASRC and VRC seem to disregard those lines completely it’s better to put coordinates in there that aren’t something you want to display.

If you pout the name in front of each line works in ES but it will not work with the other clients. But if you use the above way, then the same SCT file could be used with the other clients without any problems.

Regions
The third extension is for the SCT2 files for the very same reason. If you have regions in your SCT2 file, then they can only be switched on/off all together. If you would like to use them individually add a new line before the start of a new region:
REGIONNAME <the name of the region element>

These lines are simply ignored by VRC and can be used to name your region elements.

Sector File Extension Files
This section is here just to make this page complete. The content of the sector file extension is described in the ESE Files Description page, and there is a Tutorial about how to build an ESE file from scratch.

Runway Files
The runway files are saved along with the SCT files, with the same names and the RWY extensions. They are also TEXT files. There you can find information about the active airports and runways of your last session when the SCT file was used as main sector file.

ACTIVE_AIRPORT:LHBP:1
ACTIVE_AIRPORT:LHBP:0
ACTIVE_RUNWAY:LHBP:31R:0
ACTIVE_RUNWAY:LHBP:31L:1
ACTIVE_RUNWAY:LHBP:31L:1

There are two different kinds of lines here:

ACTIVE_AIRPORT – It describes if an airport was active in the last session. The last 0/1 digit means if it was active for departure (1) or arrival (0).
ACTIVE_RUNWAY – The same for runways. It describes if a RWY of an airport was active in the last session. Of course, here you also have the airport name, and the final number means the same.
