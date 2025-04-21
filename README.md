# hardware-example
Example repository for projects that include hardware (PCB) development and optionally embedded firmware \[WIP\]

## Repository structure
`|--- pcb` (contains all the KiCAD projects and related files, that are part of the project)\
`|    |--- <pcb_1_name>` (KiCAD project directory for the first PCB - auto-filled by KICAD and CI automations)\
`|    |    |--- fabrication` (a directory for auto-generated fabrication output files)\
`|    |    |    |--- <pcb_1_name>_<pcb_1_version>_gerbers.zip`\
`|    |    |    |--- <pcb_1_name>_<pcb_1_version>_positions.csv`\
`|    |    |    |--- <pcb_1_name>_<pcb_1_version>_designators.csv`\
`|    |    |    |--- <pcb_1_name>_<pcb_1_version>_bom.csv`\
`|    |    |    '--- <pcb_1_name>_<pcb_1_version>_netlist.ipc`\
`|    |    |--- pdf` (a directory for auto-generated schematic, layout, assembly & mechanical drawing PDF files)\
`|    |    |    |--- <pcb_1_name>_<pcb_1_version>_schematic.pdf`\
`|    |    |    |--- <pcb_1_name>_<pcb_1_version>_layout.pdf`\
`|    |    |    |--- <pcb_1_name>_<pcb_1_version>_assembly.pdf`\
`|    |    |    '--- <pcb_1_name>_<pcb_1_version>_mechanical.pdf`\
`|    |    |--- <pcb_1_name>_<pcb_1_version>_ibom.hmtl` (auto-generated interactive HTML BOM & Assembly guide)\
`|    |    |--- <pcb_1_name>.kicad_sch` (KiCAD root schematic page)\
`|    |    |--- ...` (other schematic pages follow)\
`|    |    |--- <pcb_1_name>.kicad_pro` (KiCAD project file)\
`|    |    |--- <pcb_1_name>.kicad_pcb` (KiCAD PCB layout file)\
`|    |    |--- <pcb_1_name>.kicad_prl` (KiCAD project status file)\
`|    |    |--- .gitignore` (standard GitIgnore file for KiCAD projects)\
`|    |    |--- VERSION.txt` (text file containing `<pcb_1_version>`)\
`|    |    |--- CHANGELOG.md` (Markdown file containing recent changes (auto-generated from commit messages))\
`|    |    '--- README.md` (README Markdown file specific to the pcb_1 KiCAD project)\
`|    |--- ...` (other related PCB projects follow as needed)\
`|    |--- _libraries` (directory containing all KiCAD part libraries related to the project, including component 3D models)\
`|    |--- _datasheets` (directory containing all component datasheets relevant to the project)\
`|    |--- _ci` (a directory containing Github/Gitlab CI pipeline configuration (e.g. PDF colors))\
`|    |--- _LEGO_default.kicad_wks` (organization default KiCAD drawing sheet file)\
`|    |--- _output.kibot.yaml` (KiBot output configuration file)\
`|    |--- _test.kibot.yaml` (KiBot ERC, DRC, LVS configuration file)\
`|    |--- _ordering.md` (Markdown file containing ordering information for each PCB: amount, options, manufacturer, price)\
`|    |--- _README.md` (README Markdown file common to all PCBs in the project)\
`|    |--- _DOCUMENTATION.md` (Hardware documentation: project structure, purpose of each PCB, interconnect & supply specification)\
`|--- firmware` (contains low-level embedded firmware projects (if applicable): IO configuration, drivers, test code)\
`|    |--- ...` (STM32Cube, MPLab, ESP-IDF, pSoC Creator, Arduino IDE, Pico-SDK, Vivado, Quartus, Yosys, etc. projects)\
`|    '--- README.md` (README Markdown file for firmware projects)\
`|--- models3D` (contains all 3D CAD models related to the project, CAD project files & 3MF exports for printing)\
`|--- README.md` (Project general README Markdown file)\
`'--- ...` (Other files related to the project)\

Different PCB projects within one complex project are developed in separate branches, all branching off of the `hw-dev` branch. The files and directories starting with underscores are common to all PCB projects within the project. Component libraries should be common to the PCB projects, and they should include schematic symbols (reasonable, usable ones (might require some editing in case of symbols downloaded from SnapMagic, SamacSys CSE, Octopart, etc.)), PCB footprints (following the newest IPC standards, in the format of official KICAD libraries), and 3D models (properly oriented and scaled, and linked to the footprints). Datasheets should be stored common between the different PCBs. The drawing sheet file, libraries and datasheets, should be linked with relative URLs into the KiCAD projects.

If applicable, low-level firmware code is developed in the `fw-dev` branch, in case of multiple programmable ICs, each gets a separate branch. This firmware contains a basic minimal-working HAL (Hardware Abstraction Layer). Higher level functionality can be included here as well, but it it typically rather developed in a separate repo. If applicable, the repo can also contain mechanical designs and 3D models.

## KiCAD automation
