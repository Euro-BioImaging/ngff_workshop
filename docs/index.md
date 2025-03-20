# Welcome to the NGFF Workshop!

This workshop covers several key steps for working with OME-Zarr datasets, 
including converting, inspecting, validating, opening, saving, 
and visualizing OME-Zarr data.

The sections given below are intended to guide you through working with 
OME-Zarr datasets using a variety of tools and libraries. 
Each section is designed to cover a specific task and introduces some of the
existing tools to address that particular task.

It is important to note that this workshop covers OME-Zarr version 0.4. With
transition to the version 0.5, many changes have been implemented in the 
specifications. These changes are, however, not covered or discussed here.

## Prerequisites

### Data

The workshop will use several example image datasets. 
Please download the [zip file](https://drive.google.com/drive/folders/1anU59y7pvHVqtXNV-yKBz-UdotOjNNY1?usp=sharing) 
and extract the datasets to a convenient directory.

### Installation of the tools

The easiest way to install the required tools is via mamba.

**Installing Mamba**

If you do not already have mamba, you can acquire it via Miniforge.
Follow the instructions [here](https://github.com/conda-forge/miniforge) to set 
up Miniforge on your system.

- **Unix-based systems (Linux/macOS)**: Installing Miniforge will make the mamba command available in your terminal.
- **Windows**: Miniforge installation will set up a new command prompt called Miniforge Prompt. You can find it by typing "Miniforge" in the Windows search bar. The mamba command will be available in this prompt.

**Setting Up the Workshop Environment**

Once mamba is installed, run the following commands to clean up any existing package cache and create the environment:
```bash
mamba clean --all
mamba create -n ngff_workshop -c conda-forge -c euro-bioimaging eubi-bridge napari-ome-zarr pyqt=5.*
```
**⚠️ Important: older installations of conda may be too slow to create the environment, especially
with weak internet connection. So it is strongly recommended to install miniforge.**

### Fiji Installation

Ensure that an up-to-date version of [Fiji](https://imagej.net/software/fiji/downloads) 
is installed on your system. 

## Sections

---

### [Introduction](what_is_ngff.md)

---

### [Inspecting and Validating OME-Zarr](inspection_overview.md)

---

### [Converting Data to OME-Zarr](conversion_overview.md)

---

### [Opening OME-Zarr](open_overview.md)

---

### [Saving OME-Zarr](save_overview.md)

---

