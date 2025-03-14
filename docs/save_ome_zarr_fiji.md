<style>
body {
    font-size: 20px !important;
}
h3 {
    font-size: 24px !important;
}
h4 {
    font-size: 22px !important;
}
</style>


First open an image on Fiji by dragging and dropping the czi image from your local path (eg., `/path/to/data/pff/xyz__multiple_images.czi`) as shown below: <br><br>
![import_czi](figures/n5-ij/save_image/import_czi.png)<br><br>
A window titled **Bioformats Import Options** will open. Then click OK without changing any options.<br><br>
Another window titled **Bioformats Series Options** will open. This shows that the czi file contains two independent
images (or "series" in bioformats terminology). Then select one of the images and click OK as shown below:<br><br>
![select_series.png](figures/n5-ij/save_image/select_series.png)<br><br>
Now open the **n5-ij's saving tool** via: 
  - `[ File > Save As > HDF5/N5/Zarr/OME-NGFF ... ]` as shown below<br><br>
![save_as_zarr](figures/n5-ij/save_image/save_as_zarr.png)<br><br>
This will open a window with saving options (which define the properties of the output OME-Zarr) as shown below:<br><br>
![configure_params_for_ngff](figures/n5-ij/save_image/configure_parameters_for_ngff.png)
