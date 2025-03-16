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

Download the [zip file](https://drive.google.com/file/d/13hO32fLmyLrxcaTr14lk5NFx7hZjvfO-/view?usp=drive_link) to a convenient local directory.
Extract the datasets to a folder. This folder contains
all the image data to be used in the sections.

Verify that the conda environment `ngff_workshop` is 
available by running:
```bash
conda env list
```
If you do not see `ngff_workshop`, run the command 
below to create the environment:
```bash
conda create -n ngff_workshop -c conda-forge -c euro-bioimaging eubi-bridge napari-ome-zarr
```
Also make sure an update version of Fiji is installed on
your system.

## Sections

---

### [Introduction](what_is_ngff.md)

---

### [Inspecting and Validating OME-Zarr](inspection_overview.md)

---

### [Opening OME-Zarr](open_overview.md)

---

### [Saving OME-Zarr](save_overview.md)

---

### [Converting Data to OME-Zarr](conversion_overview.md)

---