# kicadCD

kicadCD circleCI's orb, an orb to help automating the generation of production files for KiCad projects. It uses [Kiplot](https://github.com/johnbeard/kiplot) to get Gerbers and other PCB "plots" and [KiBoM](https://github.com/SchrodingersGat/KiBoM) to generate the bill of materials.

## v0.1.0 (24/10/2019)

First release of the orb. Not really intented for general use as it's pretty much WIP and will probably will change a lot in the short term. It can generate Gerbers with Kiplot and the positions file for the pick and place. It doesn't generate BoMs yet, but that will hopefully added soon.

## How to Use:

### Initial Setup:

The orb can clone the repo containing your project with the `initialSetup` job. it will be cloned in the default path (`/root/project/`). The artifact storage folder will be created in this step too (`/root/project/artifacts`).

You will also have to add an environmental variable to your project that contains the path to the KiCad project. You can choose any name you want for it, but the default if none is specified is PROJECT_PATH

### Generate Positions file:

To create a parts positions' file, use the `pickAndPlacePositions` job. It creates a tar.gz file with all the files generated. To indicate which layers to plot, use the Kiplot configuration file (a yaml file that must be named 'Kiplot_config.yaml' and must be stored in the path specified by PROJECT_PATH).

It takes four parameters:

- projectPath: an environmental variable containing the path to the Kicad project. The default value is `PROJECT_PATH`
- PCBFile: the name of the pcb file to get the parts from. It must be the name only (or a path relative to projectPath) and contain the extension (`.kicad_pcb`).
- includeVirtualComponentsFlag: a boolean flag to indicate if you want the virtual components listed in your file. It might be useful to get the positions of test pads, fiducials, mounting screws, ...
- artifactsPath: the path to store the tar.gz file with the outputs of the process. By default, they will be stored in `/root/project/artifacts/`.
