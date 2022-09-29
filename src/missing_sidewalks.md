# Missing Sidewalks

According to the City of Grants Pass development code, new street should have sidewalk adjacent on either side, except for the following cases.  Only one sidewalk is necessary if:
    - the street is on a hillslope, or
    - the street serves four units or fewer.

Currently a number of city streets lack the required number of sidewalks.  Older developments that predate the language in the development code may have omitted the construction of sidewalks.  Developers also have the option of omitting sidewalk construction using the Fee in Lieu Option, paying the cost of construction to the city instead of building the sidewalks directly.  The purpose of the Missing Sidewalks Map is to show areas of the city where sidewalks are currently required but not built.

To produce the Missing Sidewalks Map, first clone the *scripts* repository from the GIS Github account:

``````{shell}
git clone git@github.com:grantspassoregon/scripts
``````

Whereas repositories normally host working packages, such as the [webmap](https://github.com/grantspassoregon/webmap) package for producing web city web maps, or the content for a static web site, such as the [documentation](https://github.com/grantspassoregon/documentation) repo, the *scripts* repository hosts stand-alone scripts designed to handle specific projects in the City of Grants Pass GIS Office.  In the case of the script for this project, *missing_sidewalks.py*, the code uses the *arcpy* module, which only works during a running session of ArcGIS.  Since the *arcpy* module is not available outside of ArcGIS, consolidating the code within the script into a full Python package does not make sense.

To use the *missing_sidewalks.py* script, the first step is to open an empty project in ArcGIS Pro.  With the mouse, select the **View** tab and open the Python window by clicking the **Python Window** button in the *Windows* menu.  The Python window will open in a pane docked to the bottom of the application.  The upper portion of the pane shows output from the Python interpreter, while the blank line with the cursor on the bottom of the pane is where you enter Python code.

The script *missing_sidewalks.py* will create a file geodatabase on your machine, a log file, and a csv of summary statistics.  Before running the script on your machine, you will likely want to customize the name and location of these files by adjusting the file path names in the script.  Open the *missing_sidewalks.py* in the file editor of your choice, and note that the file path variables appear at the top of the file, immediately below the import statements:

```Python
# Customize these variables to paths on your system
PROJECT_DIR = "C:/Users/erose/projects"
GDB_NAME = "missing_sidewalks.gdb"
WORKSPACE = "C:/Users/erose/projects/missing_sidewalks.gdb"
ARCGIS_PROJECT = "P:/projects/sidewalks/sidewalks3.aprx"
LOG_FILE = "P:/missing_sidewalks.log"
CSV_FILE = "P:/missing_sidewalks_report.csv"
```
The variable names are in SCREAMING_SNAKE_CASE, and the values are strings indicating the file path names that the script uses for the project.  Edit these file path names as suitable for your device (for instance, your username is probably not *erose*).  A short description of each file path variable:

 - PROJECT_DIR - The project directory where ArcGIS will create a new file geodatabase.
 - GDB_NAME - The desired name of the new geodatabase.  The script may fail if the geodatabase already exists!
 - WORKSPACE - The full path name of the new geodatabase.  This should be the project directory followed by the new geodatabase name, separated by a space.  Since we create and use a new geodatabase, this step is a little redundant.
 - ARCGIS_PROJECT - The name of the empty ArcGIS project that should be open in ArcGIS Pro.  One of the *arcpy* commands run by the script (SelectByAttribute), requires an open session of ArcGIS to work, which is why we open first open an empty project in ArcGIS Pro.  There is no need to use a pre-existing project because the script will load and create the necessary layers when run.
 - LOG_FILE - The file path name at which to create a log file.  This script uses the *logging* package to record progress, but ArcGIS does not permit logging to the console, so the script saves logging messages in a log file.  If an error occurs while running the script, you can open the log file in the text editor of your choice to view the output and diagnose where the problem occurred.
 - CSV_FILE - The file path name of the table of summary statistics on the length of streets missing sidewalks.

Once you have editing the file path variable names in *missing_sidewalks.py*, you can save the changes in a copy on your local machine.  In a traditional Python package, we might store the values of these variables in a `.env` file, but ArcGIS does not currently support the *dotenv* package, so we are stuck with the values hard-coded into the script for now.  This should be the only part of the script that you need to alter, and now we can run it on your machine.

In the Python window in your open session of ArcGIS Pro, paste the following line of code:

```Python
exec(open('/path-to-my-script/missing_sidewalks.py').read())
```

You can also change the working directory to your project folder, using the *os* package:

```Python
import os
os.chdir('/project/directory/path')
exec(open('missing_sidewalks.py').read())
```

Important note:  Do not set the location of the file geodatabase on a virtual drive.  Use the primary (C:) drive on your machine.  The IT department discourages employees from storing information on the local (C:) drive, and consequently employees are in the habit of storing personal files on the P: drive, and GIS project files on the O: drive.  However, this script performs many heavy computations in ArcGIS.  If you store the geodatabase in a remote drive (P: or O:), this will substantially decrease the speed of operations by requiring ArcGIS to transmit the information over the network to the remote drive.  This may also cause internal congestion on the city network.  Once the script has finished running, you can move the resulting geodatabase to a permanent storage location on the O: drive, but while the script is generating the geodatabase you want the work to occur on your local (C:) drive.  This will improve processing time as ArcGIS will be limited by the speed on your processor (CPU-bound) and not by the speed of the network (I/O-bound).
