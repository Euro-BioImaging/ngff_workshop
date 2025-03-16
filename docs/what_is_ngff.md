

OME-Zarr is a chunked file format represented in nested directories
and supporting multiple resolution layers. 

This structure offers faster access to data that is remotely stored. It
also allows faster parallel writing to remote storage.

### What would the simplest OME-Zarr look like?

**Folder structure of a simple OME-Zarr with one chunk and 
one resolution layer:**

<div style="font-family: monospace;"> <span style="color: black;">📂 filament-single-chunk.zarr</span> <span style="color: gray;">(Zarr group with <strong>.zattrs (multiscales)</strong> metadata)</span> <br> └── <span style="color: purple;">📁 0</span> <span style="color: gray;">(Resolution level index, Zarr array with <strong>.zarray (storage)</strong> metadata)</span> <br> &nbsp;&nbsp;&nbsp;&nbsp;└── <span style="color: teal;">📁 0</span> <span style="color: gray;">(Time chunk index)</span> <br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└── <span style="color: green;">📁 0</span> <span style="color: gray;">(Channel chunk index)</span> <br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└── <span style="color: orange;">📁 0</span> <span style="color: gray;">(Z chunk index)</span> <br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└── <span style="color: blue;">📁 0</span> <span style="color: gray;">(Y chunk index)</span> <br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└── <span style="color: red;">📁 0</span> <span style="color: gray;">(X chunk index)</span> <br> </div>

**Content of the .zattrs metadata file:**
```json
{
    "multiscales": [
        {
            "name": "filament-single-chunk.zarr",
            "version": "0.4",
            "axes": [
                { "name": "t", "type": "time", "unit": "s" },
                { "name": "c", "type": "channel", "unit": "Channel" },
                { "name": "z", "type": "space", "unit": "μm" },
                { "name": "y", "type": "space", "unit": "μm" },
                { "name": "x", "type": "space", "unit": "μm" }
            ],
            "datasets": [
                {
                    "path": "0",
                    "coordinateTransformations": [
                        {
                            "type": "scale",
                            "scale": [1.0, 1, 0.23985, 0.021462, 0.021462]
                        }
                    ]
                }
            ]
        }
    ]
}
```

**Content of the .zarray metadata file:**

```json
{
    "chunks": [1, 1, 29, 253, 246],
    "shape": [1, 1, 29, 253, 246],
    "dtype": "|u1",
    "order": "C",
    "dimension_separator": "/",
    "fill_value": 0,
    "filters": null,
    "compressor": {
        "id": "blosc",
        "cname": "lz4",
        "clevel": 5,
        "shuffle": 1,
        "blocksize": 0
    },
    "zarr_format": 2
}
```

### What if it had multiple chunks?

<div style="font-family: monospace;"> <span style="color: black;">📂 filament-three-z-chunks.zarr</span><span style="color: gray;">(Zarr group with <strong>.zattrs (multiscales)</strong> metadata)</span><br> └── <span style="color: purple;">📁 0</span> <span style="color: gray;">(Resolution level index, Zarr array with <strong>.zarray (storage)</strong> metadata)</span> <br> &nbsp;&nbsp;&nbsp;&nbsp;└── <span style="color: teal;">📁 0</span> <span style="color: gray;">(Time chunk index)</span> <br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└── <span style="color: green;">📁 0</span> <span style="color: gray;">(Channel chunk index)</span> <br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├── <span style="color: orange;">📁 0</span> <span style="color: gray;">(z chunk index 0)</span> <br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;│&nbsp;&nbsp;&nbsp;&nbsp;└── <span style="color: blue;">📁 0</span> <span style="color: gray;">(y chunk index)</span> <br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;│&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└── <span style="color: red;">📁 0</span> <span style="color: gray;">(x chunk index)</span> <br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├── <span style="color: orange;">📁 1</span> <span style="color: gray;">(z chunk index 1)</span> <br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;│&nbsp;&nbsp;&nbsp;&nbsp;└── <span style="color: blue;">📁 0</span> <span style="color: gray;">(y chunk index)</span> <br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;│&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└── <span style="color: red;">📁 0</span> <span style="color: gray;">(x chunk index)</span> <br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└── <span style="color: orange;">📁 2</span> <span style="color: gray;">(z chunk index 2)</span> <br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└── <span style="color: blue;">📁 0</span> <span style="color: gray;">(y chunk index)</span> <br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└── <span style="color: red;">📁 0</span> <span style="color: gray;">(x chunk index)</span> <br> </div>

**Content of the .zattrs metadata file:**

```json
{
    "multiscales": [
        {
            "name": "filament-single-chunk.zarr",
            "version": "0.4",
            "axes": [
                { "name": "t", "type": "time", "unit": "s" },
                { "name": "c", "type": "channel", "unit": "Channel" },
                { "name": "z", "type": "space", "unit": "μm" },
                { "name": "y", "type": "space", "unit": "μm" },
                { "name": "x", "type": "space", "unit": "μm" }
            ],
            "datasets": [
                {
                    "path": "0",
                    "coordinateTransformations": [
                        {
                            "type": "scale",
                            "scale": [1.0, 1, 0.23985, 0.021462, 0.021462]
                        }
                    ]
                }
            ]
        }
    ]
}
```

**Content of the .zarray metadata file:**

```json
{
    "chunks": [1, 1, 10, 253, 246],
    "shape": [1, 1, 29, 253, 246],
    "dtype": "|u1",
    "order": "C",
    "dimension_separator": "/",
    "fill_value": 0,
    "filters": null,
    "compressor": {
        "id": "blosc",
        "cname": "lz4",
        "clevel": 5,
        "shuffle": 1,
        "blocksize": 0
    },
    "zarr_format": 2
}
```

### What if it had multiple resolution levels?

<div style="font-family: monospace;"> 
  <span style="color: black;">📂 filament-two-layers-single-chunk.zarr</span><br> 
  ├── <span style="color: blue;">📁 0</span> <span style="color: gray;">(Resolution level 0, Zarr array with  <strong>.zarray (storage)</strong> metadata))</span><br> 
  │&nbsp;&nbsp;&nbsp;&nbsp;└── <span style="color: blue;">📁 0</span> <span style="color: gray;">(Time chunk index)</span><br> 
  │&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└── <span style="color: blue;">📁 0</span> <span style="color: gray;">(Channel chunk index)</span><br> 
  │&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└── <span style="color: blue;">📁 0</span> <span style="color: gray;">(z chunk index)</span><br> 
  │&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└── <span style="color: blue;">📁 0</span> <span style="color: gray;">(y chunk index)</span><br> 
  │&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└── <span style="color: blue;">📁 0</span> <span style="color: gray;">(x chunk index)</span><br> 
  └── <span style="color: green;">📁 1</span> <span style="color: gray;">(Resolution level 1, Zarr array with  <strong>.zarray (storage)</strong> metadata))</span><br> 
  &nbsp;&nbsp;&nbsp;&nbsp;└── <span style="color: green;">📁 0</span> <span style="color: gray;">(Time chunk index)</span><br> 
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└── <span style="color: green;">📁 0</span> <span style="color: gray;">(Channel chunk index)</span><br> 
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└── <span style="color: green;">📁 0</span> <span style="color: gray;">(z chunk index)</span><br> 
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└── <span style="color: green;">📁 0</span> <span style="color: gray;">(y chunk index)</span><br> 
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└── <span style="color: green;">📁 0</span> <span style="color: gray;">(x chunk index)</span>
</div>


**Content of the .zattrs metadata file:**
```json
{
    "multiscales": [
        {
            "name": "filament.zarr",
            "version": "0.4",
            "axes": [
                { "name": "t", "type": "time", "unit": "s" },
                { "name": "c", "type": "channel", "unit": "Channel" },
                { "name": "z", "type": "space", "unit": "μm" },
                { "name": "y", "type": "space", "unit": "μm" },
                { "name": "x", "type": "space", "unit": "μm" }
            ],
            "datasets": [
                {
                    "path": "0",
                    "coordinateTransformations": [
                        { 
                            "type": "scale", 
                            "scale": [1.0, 1, 0.23985, 0.021462000487230338, 0.021462000487230338] 
                        }
                    ]
                },
                {
                    "path": "1",
                    "coordinateTransformations": [
                        { 
                            "type": "scale", 
                            "scale": [1.0, 1.0, 0.49683214285714294, 0.04309433431166092, 0.042924000974460676] 
                        }
                    ]
                }
            ]
        }
    ]
}
```

**Content of the .zarray metadata files corresponding to levels 0 and 1:**

```json
{
    "chunks": [1, 1, 29, 253, 246],
    "shape": [1, 1, 29, 253, 246],
    "dtype": "|u1",
    "order": "C",
    "dimension_separator": "/",
    "fill_value": 0,
    "filters": null,
    "compressor": {
        "id": "blosc",
        "cname": "lz4",
        "clevel": 5,
        "shuffle": 1,
        "blocksize": 0
    },
    "zarr_format": 2
}
```

```json
{
    "chunks": [1, 1, 15, 127, 123],
    "shape": [1, 1, 15, 127, 123],
    "dtype": "|u1",
    "order": "C",
    "dimension_separator": "/",
    "fill_value": 0,
    "filters": null,
    "compressor": {
        "id": "blosc",
        "cname": "lz4",
        "clevel": 5,
        "shuffle": 1,
        "blocksize": 0
    },
    "zarr_format": 2
}
```
