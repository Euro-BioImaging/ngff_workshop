**Here we cover different ways to open remote and local OME-Zarrs in Napari**

### Drag and drop

Open napari via terminal:
```bash
napari
```

Now drag and drop one of the local OME-Zarrs (e.g., `6001240.zarr`) into `napari`.<br><br>

You will be prompted to choose a plugin. Choose `napari-ome-zarr` 
and click `OK`.

This is a convenient way to open local OME-Zarrs.

### Use command line

This method can be used to open both local and remotely stored OME-Zarrs.
For instance, use the following command to open an OME-Zarr from EBI's s3 bucket.

``` bash
napari --plugin napari-ome-zarr https://uk1s3.embassy.ebi.ac.uk/idr/zarr/v0.4/idr0062A/6001240.zarr
```

### Use Python code

Similarly to the command line option, local and remote OME-Zarrs can also
be read directly via Python code.

Approach 1: Open the full OME-Zarr from the top level url:
```python
import napari
 
v = napari.Viewer()
v.open("https://uk1s3.embassy.ebi.ac.uk/idr/zarr/v0.4/idr0062A/6001240.zarr",
       plugin = 'napari-ome-zarr'
       )
napari.run()
```
Note that this approach automates a lot of tasks for the user,
discovering look-up tables, pixel scalings and units from the OME-Zarr metadata.

Approach 2: Read arrays and open them individually:
```python
import napari
import zarr, dask.array as da

url = "https://uk1s3.embassy.ebi.ac.uk/idr/zarr/v0.4/idr0062A/6001240.zarr"
gr = zarr.open_group(url, mode = 'r')
# Get the resolution layer 2 from the raw data as dask array.
array2 = da.from_zarr(gr[2]) 
# Get the resolution layer 2 from the label data as dask array.
label_array2 = da.from_zarr(gr.labels['0'][2]) 
# Open the viewer and add the dask arrays.
v = napari.Viewer()
v.add_image(array2, contrast_limits = (0, 2000), colormap = 'red')
v.add_labels(label_array2)
napari.run()
```

Note that approach 2 does not read any metadata. You have to
specify the metadata manually in the viewer's api.
