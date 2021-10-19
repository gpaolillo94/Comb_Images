# Comb_Images

Comb Image Pipeline is a Python pipeline for counting uncapped cells from honey comb images.

## Installation

git clone https://github.com/gpaolillo94/Comb_Images.git

The processing pipeline has been tested using Python 3.7.6
  Package dependencies are resolved by either installing them manually:
  
  `pip install numpy pandas opencv-python staintools colorcorrect spams`
  
  or by executing the first cell of the Jupyter notebook.
  
  In our experimental setup, the following package versions have been used:
  
  ```
  numpy==1.21.1
  pandas==1.3.4
  opencv-python==4.5.3.56
  staintools==2.1.2
  colorcorrect==0.9.1
  spams==2.6.2.5
  ```

## Usage

Run the file Comb_Image_Pipeline.ipynb  

Move your comb images to the folder

    /Comb_Images/experiment/Data/photos 

where experiment is 'Circular_Crop', 'DeepBee', 'Internal_Crop'

# Set Params of Pipeline

normalization = 'ACE' 
methods available 'ACE', 'MACENKO', 'VAHADANE' 

resize = 0.1 
for experiment Crop = 0.1, for DeepBee = 0.5

thresholding = 'OTSU' 
methods available 'OTSU', 'ADAPTIVE_MEAN', 'ADAPTIVE_GAUSSIAN' 

min_Radius = 1 
set min_Radius value for circle detection

max_Radius = 27 
set max_Radius value for circle detection

blocksize = 7 
only adaptive thresholding

constant = 26 
only adaptive thresholding

# Training phase

50 images are randomly extracted from ./Comb_Images/experiment/Data/photos to generate I_{Train} and the rest to generate I_{Test}.

Function thresholding_Hough_correl(img_dict, thresholding, min_Radius, max_Radius, blocksize, constant)

Images are fed in to the function thresholding_Hough_correl along with the thresholding method and the paramaters for the Circle Hough Transform to detect and count uncapped comb cells. Function returns correlation between automated counts and manual counts obtained by experts reported in /Comb_Images/experiment/DataCorrel.csv.
'OTSU' thresholding does not need parameters contrary to 'ADAPTIVE_MEAN' and 'ADAPTIVE_GAUSSIAN' which take blocksize and constant as input.
min_Radius, max_Radius, blocksize and constant are optimized in a grid search fashion for thresholding = '' on I_{Train}.

# Testing phase
Best parameters obtained in the testing phase are fed to the function thresholding_Hough_correl to test on I_{Test}.

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## Contact
Gianluigi Paolillo - email gianluigi.paolillo@unimi.it
