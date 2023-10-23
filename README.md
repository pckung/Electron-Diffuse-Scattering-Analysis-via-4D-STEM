# Electron-Diffuse-Scattering-Analysis-via-4D-STEM
Electron diffuse scattering analysis procedure for crystalline materials via 4D-STEM 

The ipython notebooks in this project are parts of a procedure for analysing the fluctuation and correlation of electron diffuse scattering signals obtained via Four-Dimensional Scanning Transmission Electron Microscopy (4D-STEM) technique, as described in the paper "Differentiating Diffuse Electron Scattering in Complex FCC Alloys via Fluctuation and Correlation Mapping":

(Put paper url here)

The procedure is useful for identifying diffuse scattering signals in crystalline materials that originate from nanoscale heterogeneous features, such as nanoscale planar defect and nanoscale ordered (both short-range and long-range) domains, and for solving the origins of such heterogeneous diffuse scattering signals.

## Prerequisites
1. Intall Python and necessary packages:
  - Jupyter Lab
  - numpy
  - matplotlib
  - pyqt5
  - opencv
  - scikit-image
  - hyperspy (optional, only for reading raw data)
2. Download example dataset (optional)
  - The example dataset can be downloaded at (put dataset url here)
  - The example dataset is a 4D-STEM dataset of a solution-treated (CrCoNi)<sub>93</sub>Al<sub>4</sub>Ti<sub>2</sub>Nb medium entropy alloy taken along <111> zone axis, which was analyzed and discussed in the aforementioned paper. The dataset has a dimension of (200, 200, 256, 256), where the first two dimensions are the real space coordinates of probe positions during 2D raster scan with unit of 1 nm, and the last two dimensions form the collected diffraction patterns. The details of the material, data collecting condition, and analysis results can be found in the paper mentioned above. 
