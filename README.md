# stac-expr
Proposal for Expression Specification for Band Math across multiple STAC Feature Assets

# specification
Bands can be specified in two ways: (1) asset key with band number or (2) common name.
### asset key with band number
Bands can be specified by a combination of the unique asset key per the [item-spec](https://github.com/radiantearth/stac-spec/blob/master/item-spec/item-spec.md) and the band index number (starting with zero).  For example, `RGB[2]` refers to the **RGB** asset's 3rd band.
### common name
The Electro-Optical Extension provides a list of common names for referring to bands [here](https://github.com/radiantearth/stac-spec/tree/master/extensions/eo#common-band-names).  For example, `green` when used with Landsat 8 would refer to Lansat 8's 3rd band, which is also the first (and only) band in the B3 asset file.

# examples
### NDVI for Landsat 8 using Asset Keys with Band Number
```
(B5[0] - B4[0])/(B5[0] + B4[0])
```
Because the Landsat 8 Asset GeoTIFFs only have one band, you can remove the `[0]` and the first band will be assumed:
```
(B5 - B4)/(B5 + B4)
```

### NDVI for Landsat 8 using Common Names
```
(nir - red)/(nir + red)
```

# multi-band output
In order to output RGB tiles, you must provided 3 expressions separated by a comma.  For example, to specify a rgb output, you can enter: `red,green,blue`.  If you wanted to subsitute Near-Infrared in for Red, you could do: `nir,green,blue`

# case insensitivity
Asset variable names should not be case sensitive.  In other words,
- ```(B5 - B4)/(B5 + B4)``` is equivalent to ```(b5 - b4)/(b5 + b4)```
- ```(NIR - RED)/(NIR + RED)``` is equivalent to ```(nir - red)/(nir + red)```

# implementations
- Marblecutter Fork (partial implementation including references by `asset key[band number]`, but not common name): https://github.com/DanielJDufour/marblecutter-virtual/blob/STAC/virtual/web.py#L156

# resources
- https://github.com/developmentseed/stac-tiler

# contribute
Post an issue [here](https://github.com/GeoTIFF/stac-expr/issues) or submit a PR [here](https://github.com/GeoTIFF/stac-expr/pulls)!
