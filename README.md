# Simultaneous Prediction of Optical and Tactile Sensation

This repository contains the code and resources for the T-RO 2023 paper: **Combining Vision and Touch for Physical Robot Interaction**.

**Author**: Willow Mandil, Amir Ghalamzan E

We examine the benefits of incorporating tactile sensation into video prediction models for physical robot interactions. By proposing three multi-modal integration approaches and comparing the performance of these tactile-enhanced video prediction models, we demonstrate the potential of using both visual and tactile feedback for improved scene prediction accuracy and a better understanding of cause-effect relationships during robot interactions. We also introduce two new datasets of robot pushing using a magnetic-based tactile sensor for unsupervised learning.

<p align="center">
<img src="https://github.com/imanlab/WM-4-PRI/blob/master/assets/SPOTS_abstract_5_.jpg" width="500">
<p/>

## Datasets

Two datasets and their descriptions can be found at:

  - [Marked Friction Dataset](https://github.com/imanlab/object_pushing_MarkedFrictionDataset)
  - [Household Objects Dataset](https://github.com/imanlab/)

<p align="center">
<img src="https://github.com/imanlab/WM-4-PRI/blob/master/assets/data_collection_household.jpg" width="500">
<p/>

<p align="center">
  <img src="https://github.com/imanlab/WM-4-PRI/blob/master/assets/DatasetExampleLarge_.jpeg" width="500">
</p>

## Requirements

- GPU access is recommended for faster training (we used two Nvidia RTX A6000 GPUs)
- Python 3.8
- PyTorch, torchvision
- SciPy
- NumPy
- Matplotlib
- OpenCV
- tqdm

To install dependencies, use:
```bash
pip install -r requirements.txt
```

### Dataset formatting:
Download the dataset you wish from the section above using:
```bash
git clone https://github.com/imanlab/object_pushing_MarkedFrictionDataset.git
```

The dataset requires formatting for use in the training and testing scripts.

To format the data, apply [format_data.py](https://github.com/imanlab/SPOTS_IML/data_formatting/format_data.py). The function requires several user inputs, for example, the length of the context window, the length of the prediction horizon, where to save the data, whether to convert the tactile data to tactile images and finally, desired image height and width.

```bash
python3 format_data.py
```

### Training and Testing:
We have simplified the training and testing procedure of the models presented in this paper. 

To train the model run:  
```bash
python3 model_trainer.py
```

To test the model run:  
```bash
python3 model_trainer.py
```

There are a variety of input arguments that can be adjusted to suit your needs. The extensive list below explains each argument for the two programs. An example of the use of these input arguments is shown below: 

```bash
python3 model_trainer.py --model_name="SPOTS_SVG_ACTP" --batch_size=32 --epochs=100 --device="cuda:0" --model_save_path= "/home/.../SPOTS_SVG_ACTP/" --train_data_dir="/home/.../test_dataset/" --scaler_dir="/home/.../scalar_dataset/" 
```

### Input functions to train script:
- model_name = Set name for prediction model, SVG, SVTG_SE, SPOTS_SVG_ACTP, SVG_TC, SVG_MMFM
- batch_size = Batch size for training.
- lr = learning rate
- beta1 = Beta gain
- optimizer = what optimiser to use - only adam available currently
- seed = value for the torch seed
- image_width = Size of scene image data
- dataset = name of the dataset
- n_past = context sequence length
- n_future = time horizon sequence length
- n_eval = sum of context and time horizon
- prior_rnn_layers = number of LSTMs in the prior model
- posterior_rnn_layers = number of LSTMs in the posterior model
- predictor_rnn_layers = number of LSTMs in the frame predictor model
- state_action_size = size of action conditioning data
- z_dim = number of latent variables to estimate
- beta = beta gain
- epochs = number of epochs to run for 
- train_percentage = how much of the data to train with
- validation_percentage = how much of the data to use for validation
- criterion = loss function to use for training (L1/L2)
- tactile_size = size of tacitle frame - 48, if no tacitle data set to 0
- g_dim = size of encoded data for input to prior
- rnn_size = size of encoded data for input to frame predictor (g_dim = rnn-size)
- channels = input channels
- out_channels = output channels
- training_stages = define the training stages - if none leave blank - available: 3part
- training_stages_epochs = define the end point of each training stage
- num_workers = number of workers used by the data loader
- model_save_path = where should the script save the trained model.
- train_data_dir = where is training the data saved 
- scaler_dir = where is the datas scaler directory 
- model_name_save_appendix = What to add to the save file to identify the model as a specific subset (_1c= 1 conditional frame, GTT=groundtruth tactile data)
- tactile_encoder_hidden_size = Size of hidden layer in tactile encoder, 200
- tactile_encoder_output_size = size of output layer from tactile encoder, 100
- occlusion_test = if you would like to train for occlusion
- occlusion_gain_per_epoch = increasing size of the occlusion block per epoch 0.1=(0.1 x MAX) each epoch
- occlusion_start_epoch = size of output layer from tactile encoder, 100
- occlusion_max_size = max size of the window as a % of total size (0.5 = 50% of frame (32x32 squares in ))
- using_depth_data = is the model using depth video data
- using_tactile_images = does the model use tacitle images or tactile vectors
- early_stop_clock = should the early stop clock be engaged
- device = what device to run the model on
- save_intervals = how often to save a model of the data 
- tactile_random = if you want to provide random tactile data to the model instead of real tactile data
- image_random  = if you want to provide random scene data to the model instead of real scene data

### input functions to test script:
- model_name =Set name for prediction model, SVG, SVTG_SE, SVG_TC, SVG_TC_TE, SPOTS_SVG_ACTP
- model_stage =what stage of model should you test? BEST, stage1 etc.
- tactile_random =if you want to provide random tactile data to the model instead of real tactile data
- tactile_zero =if you want to provide neutral tactile data to the model instead of real tactile data
- image_random =if you want to provide random scene data to the model instead of real scene data
- model_folder_name =Folder name where the model is stored
- quant_analysis =Perform quantitative analysis on the test data
- qual_analysis =Perform qualitative analysis on the test data
- qual_tactile_analysis =Perform qualitative tactile analysis on the test tactile data
- quant_tactile_analysis =Perform quantitative tactile analysis on the test tactile data
- test_sample_time_step =which time steps in prediciton sequence to calculate performance metrics for.
- model_name_save_appendix = What to add to the save file to identify the model as a specific subset, _1c
- test_data_dir = where is the test data directory in the drive?
- scaler_dir = should the output be scaled?
- using_tactile_images = does the model use tactile images or vecotrs?
- using_depth_data = does the model use the depth data as well?
- seen = is the test data seen or unseen
- device = Which device to use?

### Maintainers
Willow Mandil - 18710370@students.lincoln.ac.uk

### Copyright
Copyright © 2023 Willow Mandil, Amir Ghalamzan E. All rights reserved.

### License
This project is licensed under the MIT License.

###  Acknowledgments
Please cite our paper if you find this code or the datasets useful in your research:

Mandil, W., & Ghalamzan E, A. (2023). Combining Vision and Touch for Physical Robot Interaction. T-RO, 2023.
