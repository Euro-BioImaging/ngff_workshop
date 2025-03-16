**Use the ome-zarr-py library for inspecting and downloading OME-Zarrs from s3**

Remote OME-Zarr data stored in a **public** s3 bucket can be inspected and downloaded using 
the `ome-zarr-py` tool via **terminal** or **Python** code. 

Activate the conda environment `ngff_workshop`:

```bash
conda activate ngff_workshop
```

### Terminal

#### Inspect remote data

Inspect 3 different remote datasets:

```bash
ome_zarr info https://uk1s3.embassy.ebi.ac.uk/EuBI/anna_steyer0/20160112_C.elegans_std_fullhead.zarr
```

```bash
ome_zarr info https://uk1s3.embassy.ebi.ac.uk/idr/zarr/v0.4/idr0062A/6001240.zarr
```

```bash
ome_zarr info https://s3.embl.de/i2k-2020/platy-raw.ome.zarr
```

#### Download remote data

Create a directory named `downloaded_omezarrs` in your home directory, 
browse into it and download the dataset `6001240.zarr` from s3:

```bash
cd /path/to/data/downloaded_omezarrs
```

```bash
ome_zarr download https://uk1s3.embassy.ebi.ac.uk/idr/zarr/v0.4/idr0062A/6001240.zarr
```

Inspect the local dataset (**optional**):
```bash
ome_zarr info /path/to/data/downloaded_omezarrs/6001240.zarr
```

### Python

Access Python

```bash
python
```

#### Import the relevant tools

```python
from ome_zarr import utils
```

#### Inspect remote data

```python
list(utils.info("https://uk1s3.embassy.ebi.ac.uk/EuBI/anna_steyer0/20160112_C.elegans_std_fullhead.zarr"))
```

#### Download remote data

```python
utils.download(input_path = "https://uk1s3.embassy.ebi.ac.uk/idr/zarr/v0.4/idr0062A/6001240.zarr",
               output_dir = "./downloaded_omezarrs")
```