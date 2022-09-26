# Adding New Addresses

The City of Grants Pass stores addresses in an Enterprise Geodatabase Feature Class that is stored on the *OUTRIGGER* server, called *"SDEPublic.GPGIS.land_SITEADDRESSPOINT"*, referenced by planning staff, utility works, commercial utility providers (like internet companies), as well as emergency fire and medical services.  City staff access this data using the layer file is at *"O:/Layer Files/Addresses/Building Addresses.lyrx"*.  The GIS office maintains and updates the address layer using an ArcGIS Pro project stored on the O Drive at *"O:/GISUserProjects/Departments/GIS_General/Addressing/Address Editing and Mapping.aprx"*.  This project includes the following layers:

- City Limits
- Urban Growth Boundary
- Proposed Streets
- City Streets
- Building Addresses
- Service & Annexation Agreements
- Taxlot Parcels
- Aerial Imagery

The City Limits and Urban Growth Boundary layers help to orient users when finding new site locations, and the Address Notification Form has a field identifying whether new addresses fall within these boundaries.  The Proposed Streets layer is a draft layer the GIS staff use to portray new streets and extensions proposed on development site maps.  When an address request includes a new street or extension, staff create a line on this layer to represent the proposed street on the Address Notification Map.  The Proposed Streets layer is not a part of the formal creation process for the city streets map, and does not have any application outside of the addressing process, its only purpose is to help produce address notifications.

The city streets and building address layers use the official city database of streets and addresses.  When you update the address layer, saved changes update the address feature class in the Enterprise Geodatabase, becoming immediately available to city staff and emergency responders. The building footprints layer offers outlines of existing buildings, which can be useful to delineate the locations of addresses.  However, new development will often not have assigned footprints in the building footprints layer, and so will not be useful when making the Address Notification Map.  If the building footprint, city limits, urban growth boundary, or proposed streets layers are not in use, turn off the layers by unchecking their boxes in the contents pane so they do not appear in the legend of the Address Notification Map.

For developments within the Urban Growth Boundary but outside the City Limits, properties that access city water and sewer services will enter into a service and annexation agreement with the city for these services.  The Service and Annexation Agreements layer shows areas where these agreements are in place.  This layer may also be turned off when not active on the Address Notification Map.  The taxlot parcels layer shows the cadastral tax map of properties maintained by Josephine county.  Address assignment often occurs prior to final approval of taxlot subdivisions, so while addresses will be initially recorded in association to the parent taxlot, GIS staff will need to later update these points in the layer with new taxlot numbers after the county has approved the subdivision and updated the taxlot layer, assigning each lot in the subdivision a unique map taxlot number.

The 2019 aerials layer provides the most recent available orthography of the city to help orient residents and staff viewing the Address Notification Map.  As new aerial imagery becomes available, feel free to update the addressing layer to the new imagery, or to substitute the aerial imagery layer from the ESRI basemap gallery, whichever is more recent.  Even recent aerial imagery will often not show buildings at the locations of new addresses, when the location reflects new development.
