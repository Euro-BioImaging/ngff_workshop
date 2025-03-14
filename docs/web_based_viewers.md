### Vizarr (2D + Channels)

Create a link by pasting the address of the dataset after the `=`
in the following link:<br>

```bash
https://hms-dbmi.github.io/vizarr/?source=
```

For example, paste the following address:
```bash
https://uk1s3.embassy.ebi.ac.uk/bia-integrator-data/S-BSST410/IM2/IM2.zarr/0
```

Thus construct the following link:<br>
[https://hms-dbmi.github.io/vizarr/?source=https://uk1s3.embassy.ebi.ac.uk/bia-integrator-data/S-BSST410/IM2/IM2.zarr/0](https://hms-dbmi.github.io/vizarr/?source=https://uk1s3.embassy.ebi.ac.uk/bia-integrator-data/S-BSST410/IM2/IM2.zarr/0)

Click on it or paste it in the browser to open the viewer.

### itk-vtk-viewer (3D + channels)

Create a link by pasting the address of the dataset after the `=`
```bash
https://kitware.github.io/itk-vtk-viewer/app/?fileToLoad=
```

For example, paste the following address:
```bash
https://uk1s3.embassy.ebi.ac.uk/bia-integrator-data/S-BSST410/IM2/IM2.zarr/0
```

Thus construct the following link:<br>
[https://kitware.github.io/itk-vtk-viewer/app/?fileToLoad=https://uk1s3.embassy.ebi.ac.uk/bia-integrator-data/S-BSST410/IM2/IM2.zarr/0](https://kitware.github.io/itk-vtk-viewer/app/?fileToLoad=https://uk1s3.embassy.ebi.ac.uk/bia-integrator-data/S-BSST410/IM2/IM2.zarr/0)

Click on it or paste it in the browser to open the viewer.

### Allen 3D Volume Viewer (4D + channels)

Create a link by pasting the address of the dataset after the `=`<br>
```bash
https://volumeviewer.allencell.org/viewer?url=
```

For example, paste the following address:
```bash
https://uk1s3.embassy.ebi.ac.uk/bia-integrator-data/S-BSST410/IM2/IM2.zarr/0
```

Thus create the following link:<br>
[https://volumeviewer.allencell.org/viewer?url=https://uk1s3.embassy.ebi.ac.uk/bia-integrator-data/S-BSST410/IM2/IM2.zarr/0](https://volumeviewer.allencell.org/viewer?url=https://uk1s3.embassy.ebi.ac.uk/bia-integrator-data/S-BSST410/IM2/IM2.zarr/0)

Click on it or paste it in the browser to open the viewer.

### Neuroglancer (2D + channels, volume rendering experimental)

- Go to [https://neuroglancer-demo.appspot.com/](https://neuroglancer-demo.appspot.com/)<br>
- On to top right in `Source`, paste the following: 
```bash 
zarr://https://s3.embl.de/i2k-2020/platy-raw.ome.zarr
```
- Press Enter (multiple times). <br>
- Navigate around in the sample <br>
- Zoom in/out: `ctrl + mouse scroll`<br>
- Neuroglancer enables sharing of views. The URL in your browser adapts
to your current view. Simply copy and paste the URL to share a view with a collaborator

### BioImage Archive

The BioImage Archive also provides visualisations for the datasets they store, using the tools discussed above. 
Click on the link below to see an example.<br>
[https://uk1s3.embassy.ebi.ac.uk/bia-integrator-data/pages/S-BSST410/IM2.html](https://uk1s3.embassy.ebi.ac.uk/bia-integrator-data/pages/S-BSST410/IM2.html)<br>
An advantage of the BioImage Archive is that they also provide a range of image metadata along with the visualisation.






