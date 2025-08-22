# Survey Points

Import instructions from the TSC3 handheld:

- Open the UTILITIES project on the TSC3
- Select Export Data
- Export Fixed Format (CSV)
- Overwrite existing file
- Select All Points
- Overwrite UTILITIES.csv in the project folder _project_tracker_
  - O:/GISUserProjects/Users/ErikRose/project_tracker/
- Add UTILITIES.csv to the project (replace the existing file)
- Create XY table from points
  - X is field 3
  - Y is field 2
  - Z is field 4
  - rename output feature to today's date
  - Use OCRS Grants Pass (meters) projection
- Open Data Design > Fields and rename the fields to match the target schema
  - gnss_id: GNSS ID
  - latitude: Latitude
  - longitude: Longitude
  - elevation: Elevation
  - notes: Notes
- Open the Attribute Table and highlight the samples that need import (just the ones you took, at the end of the dataset)
- Run the Append operation
  - Target Survey Points
  - Input your utilities
    - Make sure only the highlighted samples are active
  - Use the field map to reconcile differences
- Open the Survey Points attribute table
  - Highlight the newly appended fields
  - Right-click on the date column
  - Calculate field using the Now() function in Arcade
- Attach photos to each point
  - Select the point and the Attributes button on the ribbon.
  - Click on the Attachments tab and select "Add".
