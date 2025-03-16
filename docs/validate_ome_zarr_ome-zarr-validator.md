**Validate local and remote OME-Zarrs using the
OME-Zarr validator.**

### Validate local data

#### Terminal

Activate the conda environment `ngff_workshop`:

```bash
conda activate ngff_workshop
```

**Browse into the example data directory** 

```bash
cd /path/to/example_omezarrs
```

Validate one of the example OME-Zarrs:

```bash
ome_zarr view /path/to/example_omezarrs/6001240.zarr
```

The validator will open in a web browser and demonstrate various metadata fields
of the OME-Zarr dataset.

* Find out the metadata fields such as axes, units and scales.
* Check the array and chunk shapes and bytes per resolution level.
* Visualize a single chunk.


#### Python

Make sure the environment `ngff_workshop` is active
and you are in the `example_omezarrs` folder.

Then access Python:

```bash
python
```

Do the relevant imports and validate the dataset:
```python
from ome_zarr import utils
utils.view(input_path = "./6001240.zarr")
```


### Validate remote data

Now the aim is to validate the remotely stored version of the same dataset.

Enter the following into your browser: 

```bash
https://ome.github.io/ome-ngff-validator/?source=
```

Then paste the following dataset url after the 'equal' sign: 

```bash
https://uk1s3.embassy.ebi.ac.uk/idr/zarr/v0.4/idr0062A/6001240.zarr
```

Thus construct the following link: 

[https://ome.github.io/ome-ngff-validator/?source=https://uk1s3.embassy.ebi.ac.uk/idr/zarr/v0.4/idr0062A/6001240.zarr](https://ome.github.io/ome-ngff-validator/?source=https://uk1s3.embassy.ebi.ac.uk/idr/zarr/v0.4/idr0062A/6001240.zarr) 

Note that with the remote url it is possible to copy the link from your browser and share it with 
your colleagues.




