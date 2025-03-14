**Perform parallelised conversion of image data collections to OME-Zarr using EuBI-Bridge**

First cd into the directory with the example datasets: 

`cd /path/to/data`

### Unary Conversion  

Given a dataset structured as follows:  

<div style="font-family: monospace;"> <span style="color: black;">📂 multichannel_timeseries</span><br> ├── <span style="color: blue;">📄 Channel1-T0001.tif</span><br> ├── <span style="color: blue;">📄 Channel1-T0002.tif</span><br> ├── <span style="color: blue;">📄 Channel1-T0003.tif</span><br> ├── <span style="color: blue;">📄 Channel1-T0004.tif</span><br> ├── <span style="color: red;">📄 Channel2-T0001.tif</span><br> ├── <span style="color: red;">📄 Channel2-T0002.tif</span><br> ├── <span style="color: red;">📄 Channel2-T0003.tif</span><br> └── <span style="color: red;">📄 Channel2-T0004.tif</span><br> </div>

To convert each TIFF into a separate OME-Zarr container (unary conversion):  

```shell
eubi to_zarr multichannel_timeseries multichannel_timeseries_zarr
```  

This produces:  

<div style="font-family: monospace;"> <span style="color: black;">📂 multichannel_timeseries_zarr</span><br> ├── <span style="color: blue;">📄 Channel1-T0001.zarr</span><br> ├── <span style="color: blue;">📄 Channel1-T0002.zarr</span><br> ├── <span style="color: blue;">📄 Channel1-T0003.zarr</span><br> ├── <span style="color: blue;">📄 Channel1-T0004.zarr</span><br> ├── <span style="color: red;">📄 Channel2-T0001.zarr</span><br> ├── <span style="color: red;">📄 Channel2-T0002.zarr</span><br> ├── <span style="color: red;">📄 Channel2-T0003.zarr</span><br> └── <span style="color: red;">📄 Channel2-T0004.zarr</span><br> </div>

### Aggregative Conversion (Concatenation Along Dimensions)  

To concatenate images along specific dimensions, EuBI-Bridge needs to be informed
of file patterns that specify image dimensions. For this example,
the file pattern for the channel dimension is `Channel`, which is followed by the channel index,
and the file pattern for the time dimension is `T`, which is followed by the time index.

For concatenation along the time dimension:

```shell
eubi to_zarr multichannel_timeseries multichannel_timeseries_concat-t_zarr --channel_tag Channel --time_tag T --concatenation_axes t
```  
Output:  

<div style="font-family: monospace;"> <span style="color: black;">📂 multichannel_timeseries_time_concat-t_zarr</span><br> ├── <span style="color: blue;">📄 Channel1-T_tset.zarr</span><br> └── <span style="color: red;">📄 Channel2-T_tset.zarr</span><br> </div>

**Important note:** if the `--channel_tag` were not provided, the tool would not be aware
of the multiple channels in the image and try to concatenate all images into a single one-channeled OME-Zarr. Therefore, 
when an aggregative conversion is performed, all dimensions existing in the input files must be specified via their respective tags. 

For multidimensional concatenation (channel + time):

```shell
eubi to_zarr multichannel_timeseries multichannel_timeseries_concat-ct_zarr --channel_tag Channel --time_tag T --concatenation_axes ct
```  

Note that both axes are specified with the argument `--concatenation_axes ct`.

Output:  

<div style="font-family: monospace;"> <span style="color: black;">📂 multichannel_timeseries_concat-ct_zarr</span><br> └── <span style="color: purple;">📄 Channel_cset-T_tset.zarr</span><br> </div>

### Handling Nested Directories  

For datasets stored in nested directories such as:  

<div style="font-family: monospace;">
  <span style="color: black;">📂 multichannel_timeseries_nested</span><br>
  ├── <span style="color: blue;">📁 Channel1</span><br>
  │&nbsp;&nbsp;&nbsp;&nbsp;├── <span style="color: blue;">📄 T0001.tif</span><br>
  │&nbsp;&nbsp;&nbsp;&nbsp;├── <span style="color: blue;">📄 T0002.tif</span><br>
  │&nbsp;&nbsp;&nbsp;&nbsp;├── <span style="color: blue;">📄 T0003.tif</span><br>
  │&nbsp;&nbsp;&nbsp;&nbsp;├── <span style="color: blue;">📄 T0004.tif</span><br>
  ├── <span style="color: red;">📁 Channel2</span><br>
  │&nbsp;&nbsp;&nbsp;&nbsp;├── <span style="color: red;">📄 T0001.tif</span><br>
  │&nbsp;&nbsp;&nbsp;&nbsp;├── <span style="color: red;">📄 T0002.tif</span><br>
  │&nbsp;&nbsp;&nbsp;&nbsp;├── <span style="color: red;">📄 T0003.tif</span><br>
  │&nbsp;&nbsp;&nbsp;&nbsp;├── <span style="color: red;">📄 T0004.tif</span><br>
</div>


EuBI-Bridge automatically detects the nested structure. For multidimensional concatenation:  

```shell
eubi to_zarr multichannel_timeseries_nested multichannel_timeseries_nested_concat-ct_zarr --channel_tag Channel --time_tag T --concatenation_axes ct
```  

Output:  

```shell
multichannel_timeseries_nested_concat-ct_zarr
└── Channel_cset-T_tset.zarr
```  


### Selective Data Conversion Using Wildcards  

To process only specific files, wildcards can be used. 
For example, to concatenate only **timepoint 3** along the channel dimension:  

```shell
eubi to_zarr "multichannel_timeseries_nested/**/*T0003*" multichannel_timeseries_nested_concat-wildcards_zarr --channel_tag Channel --time_tag T --concatenation_axes c
```  

Output:  

<div style="font-family: monospace;"> <span style="color: black;">📂 multichannel_timeseries_nested_concat-wildcards_zarr</span><br> └── <span style="color: purple;">📄 Channel_cset-T0003.zarr</span><br> </div>

**Note:** When using wildcards, the input directory path must be enclosed in quotes as shown in the example above.  

### Handling Categorical Dimension Patterns  

For datasets where channel names are categorical such as in:

<div style="font-family: monospace;">
  <span style="color: black;">📂 blueredchannels_timeseries_nested</span><br>
  ├── <span style="color: blue;">📁 Blue</span><br>
  │&nbsp;&nbsp;&nbsp;&nbsp;├── <span style="color: blue;">📄 T0001.tif</span><br>
  │&nbsp;&nbsp;&nbsp;&nbsp;├── <span style="color: blue;">📄 T0002.tif</span><br>
  │&nbsp;&nbsp;&nbsp;&nbsp;├── <span style="color: blue;">📄 T0003.tif</span><br>
  │&nbsp;&nbsp;&nbsp;&nbsp;└── <span style="color: blue;">📄 T0004.tif</span><br>
  └── <span style="color: red;">📁 Red</span><br>
  &nbsp;&nbsp;&nbsp;&nbsp;├── <span style="color: red;">📄 T0001.tif</span><br>
  &nbsp;&nbsp;&nbsp;&nbsp;├── <span style="color: red;">📄 T0002.tif</span><br>
  &nbsp;&nbsp;&nbsp;&nbsp;├── <span style="color: red;">📄 T0003.tif</span><br>
  &nbsp;&nbsp;&nbsp;&nbsp;└── <span style="color: red;">📄 T0004.tif</span><br>
</div>


One can run the exact same command:

```shell
eubi to_zarr blueredchannels_timeseries_nested blueredchannels_timeseries_nested_concat-ct_zarr --channel_tag Blue,Red --time_tag T --concatenation_axes ct
```  

Output:  

<div style="font-family: monospace;"> <span style="color: black;">📂 blueredchannels_timeseries_nested_concat-ct_zarr</span><br> └── <span style="color: purple;">📄 BlueRed_cset-T_tset.zarr</span><br> </div>

### Extraction of Single Series from a Multi-series Dataset

```shell
eubi to_zarr pff/17_03_18.lif lif_series_31 --series 31 --no_distributed True
```