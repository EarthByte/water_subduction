# water_subduction
A repository to calculate subducted H2O, stored H2O and slab outflux of H2O through time.

## Dependencies
The following Python libraries are required to run this workflow:

1. [gplately](https://github.com/GPlates/gplately/tree/master/gplately) and its dependencies
2. [slabdip](https://github.com/brmather/Slab-Dip/blob/main/slabdip/predictor.py)
3. moviepy
4. joblib

## Required input files
The required input files for this workflow are:

1. All files in `\utils\`
2. All files in `\loss_of_subducting_H2O_with_depth`
3. Input grids, which should follow the structure:

```text
water_subduction/
│
├── 01-Sources-of-Water.ipynb
├── 02-Subducted-Water.ipynb
├── 03-Water-Storage.ipynb
├── 04-Water-Slab-Outflux.ipynb
├── 05-Cumulative-Water-Grids.ipynb
│
├── utils/
│   └── ...
│
├── loss_of_subducting_H2O_with_depth/
│   └── ...
│
└── Grids/
    │
    └── InputGrids/
        ├── CarbonateSediment/
        ├── ContinentalMasks/
        ├── CrustalCarbon/
        ├── SeafloorAge/
        ├── SpreadingRate/
        └── TotalSediment/
```
The input grids should be prepared as follows, depending on the plate reconstruction model required:

- `CarbonateSediment` from the GitHub workflow [CarbonateSedimentThickness](https://github.com/EarthByte/CarbonateSedimentThickness)
- `ContinentalMasks`, `SeafloorAge` and `SpreadingRate` from `gplately`'s `SeafloorGrid` module, unless already available for the selected plate model elsewhere, like Zenodo or webDAV.
- `CrustalCarbon` from `\utils\`, which itself requires the `SeafloorAge` and `SpreadingRate` grids.
- `TotalSediment` from the [GitHub workflow](https://github.com/EarthByte/predicting-sediment-thickness). More details [here](https://www.earthbyte.org/predicting-sediment-thickness-on-vanished-ocean-crust-since-200-ma/).


## Workflow

1. **01-Sources-of-Water.ipynb** - Produces total water grids for each reservoir.
2. **02-Subducted-Water.ipynb** - Interpolate the grids in (1) at subduction zones to generate subducted water grids.
3. **03-Water-Storage.ipynb** - Develop water storage grids from lookup tables.
4. **04-Water-Slab-Outflux.ipynb** - Develop slab outflux as the difference between subducted water (2) and water storage (3).
5. **05-Cumulative-Water-Grids.ipynb** - Develop cumulative subducted water, water storage and water slab outflux grids.
