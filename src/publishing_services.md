# Publishing Services

The GIS Division uses two hosting alternatives to provide some redundancy against an outage in either host:

- The City maintains an ESRI licence for ArcGIS Enterprise, and publishes services from machines run by the IT department at <https://gisserver.grantspassoregon.gov/server/rest/services>.
- As a part of our licence, ESRI includes cloud-hosted services from ArcGIS Online (AGOL), where our service portal is at <https://services2.arcgis.com/pc4beVTMEhYHqerq/arcgis/rest/services>.

We use a dedicated project workspace for publishing each set of related services. For examples, the `property.aprx` project contains web maps for publishing the _property_ service on Enterprise and AGOL. Each user task has a dedicated web map with names evocative of their purpose, such as a _property_service_ for publishing the Enterprise and AGOL services. The Enterprise and AGOL services are intentionally mirrors, and should have the same layer ids and naming, so using the same web map for publishing to each portal helps to guarantee consistency.

## Details to Check Before Publishing

- Review Visibility Ranges:
  - [ ] In the Feature Layer ribbon for each layer.
    - Does the screen become crowded with too many features as you zoom out? If so, adjust the Minimum Scale downward to limit visibility.
  - [ ] In the Class tab of the Labeling Properties panel.
    - Are labels appearing for features that are too small to see clearly? Are labels crowding the features? If so, adjust the Minimum Scale downward to limit visibility.
    - The higher the visibility range of the feature, the more likely you will want to limit the label visibility.
- Review Symbology:
  - [ ] Field or expression correctly categorizes the layer types.
    - No missing values that will not draw because they do have a symbology assigned.
  - [ ] Categories contain an appropriate heading (e.g. Status and not Custom).
  - [ ] Categories are correctly ordered (e.g. Abandoned at the bottom, not the top).
  - [ ] Colors conform to a color-blind friendly palette.
    - Use 50% transparency as a starting default to permit overlaying of multiple layers.
- Review Labeling Properties:
  - [ ] Field or expression correctly labels the layer type.
  - [ ] Verdana 10pt is the default starting font.
  - [ ] Add a 1pt halo of light gray to provide contrast against both light and dark background.
  - [ ] Point Position should be Top of Point.
  - [ ] Lines like pipes should use River Placement on Centered Curved.
  - [ ] Do not Stack Labels for Lines.
  - [ ] If duplicate labels are an issue, consider removing all duplicates, or all within a radius.
  - Beware splitting labeling classes by symbol type, as this increases the burden of updating the labeling properties.
- [ ] The Display field is set to a useful field or a custom default.
  - Check that the selected field does not contain null values, or use an expression to define a fallback.
  - Use the Explore tool to view the results for a few observations.
    - If there is an existing Pop-Up Configuration, this may override the selected Display field, and the Configuration may need to be manually reset.
- [ ] Review Pop-Up Configuration:
  - Add attachments, custom text fields, or html.
  - Remove unwanted attachments or text fields.
  - Disable Pop-Ups if no fields provide useful information for the user.
  - Do not customize fields, save this step for later.
- Review Projection:
  - [ ] Individual layers should use OCRS Grants Pass in Meters.
  - [ ] The map projection should match the majority of layers.
- Publish layers in a flat hierarchy, no Group Layers.
- Set the map properties to automatically assign layer ids.
  - Ensure layer ids proceed sequentially from zero, correcting the sequence manually if necessary.
  - Use the compare tool when publishing to confirm layer names and ids match.
- Review Data Connection
  - Is the user schema correct for online publishing?
- Review Versioning
  - View-only layers should point to PROD.
  - Edit layers should point to DRAFT.
  - Maps titled `*_service` contain the view-only connection (e.g. _stormwater_service_).
  - Maps titled `*_editing` contain the edit connection (e.g. _stormwater_editing_).
- Review Sharing Permissions
  - Public-facing services should be shared with Everyone.
  - Editing services should be shared with the Organization.

## When Publishing

- Overwrite the existing service to preserve the item ID.
- Review the Description, Tags, and Categories associated with the layer.
- All Enterprise services should use registered data.
- All services except Utility Networks should be on a shared instance.
- For Feature Layers:
  - Enable Sync
  - Enable Export Data
  - Apply a default of zero for z-values
  - If editable, allow geometry updates without m-value
- Use the Compare tool to review map names and IDs for consistency.
- The AGOL and Enterprise services should be mirrors of each other, with no changes to the project space needed other than switching Portals.
