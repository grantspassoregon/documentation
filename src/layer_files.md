# Layer Files

Layer files end in the `.lyrx` extension, and contain information about layers such as the source, symbology and labeling. Sharing layer files with staff is part our strategy for ensuring the data sources in use are correct, and formatted consistently. A layer file is a snap-shot in time used only when initially adding a layer to a project, so updates to layer files do not automatically "roll out". Staff will need to drag and drop the layer file into their project all over again to take advantage of edits or changes.

## Workspace

Produce layers files from the same workspace we use to publish the corresponding service. The ArcPro projects for each service reside in the Services directory of the GIS_GENERAL folder in GISUserProjects.

The workspace contains four maps dedicated to generating layer files according to the following pattern:

- \*\_lyrx - Layer files intended for use by staff.
- \*\_agol - Layer files used to build the public-facing web viewer.
- \*\_mirror - Layer files used to mirror the agol services internally to provide redundancy.
- \*\_internal - Layer files used to build the internal web viewer.

If there are no editable layers, then the internal version is identical to the mirror version, and only the mirror map is present (e.g. _boundaries.aprx_).
The address strategic plan is only available as an editable layer for internal staff use.

## Project Dependencies

Each ArcPro project is stand-alone for the purposes of publishing the services hosted by the project. The layer file, on the other hand, may include subcategories defined in other projects. For instance, the planning category includes the sub-category for Historical and Cultural Areas, maintained in a separate project called _historical_cultural_areas_. Here is a list of project dependencies for layer files:

- boundaries
- property
  - address_strategic_plan
  - address_verification
- planning
  - historical_cultural_areas
  - agreements
  - marijuana_adult_use
  - zoning
- business
- transportation
  - parking
  - traffic
- power_gas
- water_gn
- stormwater_gn
- wastewater_gn
