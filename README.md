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
  - The example dataset can be downloaded [here](https://uofi.box.com/s/lx24fd3m6m46n184jjwnt22tg0ozom2j)
  - The example dataset is a 4D-STEM dataset of a solution-treated (CrCoNi)<sub>93</sub>Al<sub>4</sub>Ti<sub>2</sub>Nb medium entropy alloy taken along <111> zone axis, which was analyzed and discussed in the aforementioned paper. The dataset has a dimension of (200, 200, 256, 256), where the first two dimensions are the real space coordinates of probe positions during 2D raster scan with unit of 1 nm, and the last two dimensions form the collected diffraction patterns. The details of the material, data collecting condition, and analysis results can be found in the paper mentioned above.

## 1. Data Preprocessing and Local Background Removal
The notebook [1_Data_preprocessing_locbkg_removal](1_Data_preprocessing_locbkg_removal.ipynb) reads the raw data and apply the preprocessing steps to remove detector hot pixels and reduce file size by binning and cropping the diffraction patterns and changing datatype to uint16. The notebook then perform the local background removal step on the preprocessed dataset to remove most of the Bragg diffraction and leave mainly the diffuse scattering signals. The details of the preprocessing and local background removal steps can be found in the Method section in the aforementioned paper.

### Notes
- The notebook will output the preprocessed dataset and the local background removed diffuse scattering dataset (I_diff) as numpy (.npy) files at the same folder as the raw data.
- The notebook uses the [Hyperspy](https://hyperspy.org/index.html) package to read the example file (.emi file). Users can alter the code to read their own raw data file using other method, as long as the raw data is assign to a numpy array "data" with dimensions (x,y,kx,ky) before running the preprocessing steps.
- The notebook does not utilize the lazy-load function of Hyperspy and the memory map function of Numpy, thus it can be memory intensive when dealing with the raw data. If the user's PC does not have the required memroy for their own datasets, they can either change the code to utilize the memory-saving features of Hyperspy and Numpy, or work on the preprocessing steps in this notebook on a workstation with larger memory. The actual analysis will be done in the next notebook which only reads the preprocessed dataset and the diffuse scattering dataset, both have much smaller file size than the raw data.

## 2. Diffuse Scattering Analysis
The notebook [2_Diffuse_scattering_analysis](2_Diffuse_scattering_analysis.ipynb) read the preprocessed dataset and the diffuse scattering dataset and analyize the fluctuation and correlation behaviors of the diffuse scattering signals. The diffuse scattering analysis procedure includes four main steps:
1. Visualize the fluctuation of diffuse scattering signals via normalized variance map
2. Identify the correlation between heterogeneous diffuse scattering peaks via correlation coefficient map
3. Visualize the heterogeneous domains and their nanobeam diffraction pattern via virtual dark-field image and domain map
4. Isolate homogeneous diffuse scattering signals from the heterogeneous ones
The details of each step in the analysis process can be from in the Method section of the aforementioned paper.

### Notes
-Many parameters used in this notebook, such as the location of the virtual aperture, were selected for the example dataset. Users should change these parameters to values appropriate for their own dataset. 

## Limitation
This diffuse scattering analysis procedure is designed to be a rudimentary analysis that can be apply to any 4D-STEM dataset as a first step towards understanding the diffuse scattering behaviors in materials. While it works well for its intended purpose, the users should be aware of its limitations:
1. For many materials, the diffuse scattering signals are weak enough to be overwhelmed by the inelastic scattering background. Therefore, the procedure might not work properly when the 4D-STEM dataset is not collected with energy filter.
2. The analysis is qualitative not quantitative. Thus it lacks the ability to resolve some finer details of the studied features, such as chemical composition.
3. This method is not sensitive to diffuse scattering signals that are streakings stem from the Bragg diffraction. Because this kind of streakings are too close to the Bragg peaks, they can be altered during the local background removal process when the diffraction condition (such as bending) changes within the mapping area. 

