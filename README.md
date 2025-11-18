# DEM Slope and Aspect Analysis Tool

A Python-based tool for analyzing Digital Elevation Models (DEMs) using weighted linear combination of slope and aspect parameters.

## 📋 Overview

This tool processes DEM (Digital Elevation Model) data to calculate and normalize slope and aspect values, applying user-defined weights to create a weighted linear combination analysis. It's particularly useful for terrain analysis, site suitability studies, and geospatial applications.

## 🚀 Features

- **DEM Processing**: Automatically extracts slope and aspect from DEM files
- **Normalization**: Normalizes terrain parameters to 0-1 range
- **Weighted Analysis**: Applies custom weights to slope and aspect layers
- **Multi-layer Support**: Processes multiple DEM inputs and combines results
- **GDAL Integration**: Uses GDAL for robust geospatial data handling

## 📦 Requirements

```bash
pip install pillow numpy gdal matplotlib
```

### Dependencies
- `PIL` (Pillow) - Image processing
- `numpy` - Numerical computations
- `gdal` (OSGEO) - Geospatial data processing
- `matplotlib` - Visualization (optional)

## 🗂️ File Structure

```
project/
│
├── WLC.ipynb          # Main Jupyter notebook
├── dem.tif                  # Input DEM file
└── README.md                # This file
```

## 💻 Usage

### 1. Prepare Your Data
Place your DEM file (`.tif` format):
```
dem.tif
```

### 2. Run the Notebook
Open `WLC.ipynb` in Jupyter Notebook or JupyterLab.

### 3. Input Weights
When prompted, enter weights for slope and aspect (must sum to 1):
```
Slop Weight: 0.6
aspect Weight: 0.4
```

The tool will validate that weights sum to 1 before proceeding.

### 4. Processing Steps

The notebook performs the following operations:

1. **Load DEM**: Reads the DEM file using GDAL
2. **Extract Slope**: Calculates slope values in degrees
3. **Extract Aspect**: Calculates aspect (direction) values
4. **Normalize**: Scales values to 0-1 range
5. **Apply Weights**: Multiplies normalized values by user weights
6. **Combine Layers**: Aggregates multiple weighted layers

## 📊 Output

The tool generates:
- Normalized slope arrays weighted by W1
- Normalized aspect arrays weighted by W2
- Final combined arrays for both parameters

Example output:
```
Normal Slop Array * W = [0.103, 0.253, 0.236, ...]
Normal aspect Array * W = [0.037, 0.073, 0.072, ...]
```

## 🔧 Functions

### `normalize(arr, t_min, t_max)`
Normalizes an array to a specified range.

**Parameters:**
- `arr`: Input numpy array
- `t_min`: Minimum value of target range
- `t_max`: Maximum value of target range

**Returns:**
- List of normalized values

## 📈 Methodology

The Weighted Linear Combination (WLC) approach:

1. **Normalization**: Transforms input data to common scale (0-1)
   ```
   normalized = (value - min) / (max - min)
   ```

2. **Weight Application**: Multiplies normalized values by importance weights
   ```
   weighted_value = normalized_value × weight
   ```

3. **Combination**: Sums weighted layers
   ```
   final = Σ(weighted_layers)
   ```

## ⚙️ Configuration

Modify these parameters in the code:

- **DEM File Path**: `fn1 = r'dem.tif'`
- **Array Dimensions**: `range(2925)` and `range(2793)` based on your DEM size
- **Normalization Range**: `range_to_normalize = (0, 1)`

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📝 Notes

- Ensure your DEM is in GeoTIFF format
- The tool uses `computeEdges = True` for edge handling in slope/aspect calculation
- Array dimensions (2925 × 2793) should match your DEM size
- The code processes three DEM layers - modify as needed for your analysis

## ⚠️ Common Issues

**Issue**: "jame adad vrad shed bayad 1 bashad" error
- **Solution**: Ensure weights sum to exactly 1.0

**Issue**: File not found error
- **Solution**: Check DEM file path and ensure file exists

**Issue**: Memory error with large DEMs
- **Solution**: Process smaller tiles or increase available RAM


## 🙏 Acknowledgments

- GDAL/OGR contributors for geospatial processing tools
- NumPy community for numerical computation support

---

**Note**: This tool is designed for geospatial analysis and terrain evaluation. Ensure proper understanding of WLC methodology before applying to critical decision-making processes.
