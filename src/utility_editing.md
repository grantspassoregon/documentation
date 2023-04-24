# Editing the Utility Network

## Install Utility Editing Plugins to ArcMap

- Install Attribute Assistant and Water Utility Network Tools
  - Specify location on O: drive or link to download source on web
  - Make sure the Attribute Assistant is turned on [button is green, not red]

## Add Features and Specify Fields

- Create desired Features
  - Select "List by Source" in the Contents pane and ensure the layers you wish to edit are on the DRAFT version of the data.
  - Add the Editing toolbar to the toolbar menu.
    - Select "Start Editing" and click on the layer you wish to edit.
    - The "Create Features" pane should open, or you can also select this tool from the Editor toolbar.
      - Select the feature to create from the "Create Features" pane.
      - Choose an appropriate option from the Construction Tools in the "Create Features" pane.
  - Specify Data Source
    - zFieldWorker if location is specified by field worker
    - Aerial Photography if using aerial imagery to determine asset placement
    - Street View Imagery if using street imagery to determine asset placement
    - Assumed Logic if the asset location is not directly verified, but implied by connected assets
  - Insert a tap fitting where water service lines, or stormwater or sewer laterals connect to a main
  - Turn snapping on to ensure created features attach to existing features.

## Connect Features to Network

- Select newly-created features.
- Use the "Connect Geometric Network Features" tool from the Water Utility Network Editor toolbar to connect the new features to the network.
- Use the "Connection Checker" tool from the Water Utility Network Editor toolbar to verify the new features have been connected to the network.
  - If some features have failed to connect, zoom in and ensure that they are placed correctly, touching the features of the network to which they should connect.
- Select "Save Edits" from the "Editor" tool on the Editor toolbar.
- Select "Stop Editing" from the "Editor" tool on the Editor toolbar when you are finished.
