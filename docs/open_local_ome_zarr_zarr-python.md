**First cd into the data directory and then access Python:** 

```bash
cd /path/to/data
python
```

### Import the relevant tools
```python
import zarr, os, pprint
import numpy as np
```

### Read remote local and remote OME-Zarrs

```python
# path = "https://uk1s3.embassy.ebi.ac.uk/idr/zarr/v0.4/idr0062A/6001240.zarr"
path = "./6001240.zarr"
dataset = zarr.open_group(path, mode = 'r')
```

### Inspect the group-level metadata

**Print the data type**
```python
print(f"Type of the dataset: {type(dataset)}")
```

**Summarize group-level metadata:**
```python
dataset.info
```
Note the store type, the number of arrays and groups. \
Note also the group named 'labels'.

**Print the full metadata:**
```python
pprint.pprint(dict(dataset.attrs))
```

**Get multiscales metadata:**
```python
meta = dict(dataset.attrs['multiscales'][0])
```

**Print the axis ordering and the units**
```python
pprint.pprint(meta['axes'])
axis_order = ''.join(item['name'] for item in meta['axes'])
print(f"Axis order is {axis_order}")
```
**Print the voxel scaling for each resolution level**
```python
for idx, transform in enumerate(meta['datasets']):
    print(f"\033[1mVoxel transform for the level {idx}:\033[0m")
    pprint.pprint(transform)
```

### Inspect individual resolution layers

**Get the top resolution array:**
```python
zarr_array0 = dataset[0]
print(f"Array type: {type(zarr_array0)}")
print(f"Shape of the top-level array: {zarr_array0.shape}")
```
**Get a downscaled array:**
```python
zarr_array1 = dataset[1]
print(f"Array type: {type(zarr_array1)}")
print(f"Shape of the first-level downscaled array: {zarr_array1.shape}")
```
**Summarize array-level metadata:**
```python
zarr_array0.info
zarr_array1.info
```
**Print chunk size for the top layer:**
```python
print(f"Chunk size: {zarr_array0.chunks}")
```

**Convert the zarr array to a numpy array:**
```python
numpy_array0 = zarr_array0[:]
print(f"Array type: {type(numpy_array0)}")
# or use numpy directly
numpy_array0 = np.array(zarr_array0)
print(f"Array type: {type(numpy_array0)}")
```
