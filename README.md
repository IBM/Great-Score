# GREAT-Score

# Code_name explanation
The code is attached: the file named src/main.py contains the function to run the main experiment of the paper and get the result.

The  files in src/figures_code... etc contains the code to run and get the figures used in the paper. You can use the result get in the code to substitute x and y  to plot other plots.

The calibration file is for you to run calibration on CIFAR10 to get the corresponding temperature constants.

The request*.py file in src/face_code contains the code we use in online face API section, you can run the request file for each api and store the prediction value in npy file. For deepface API, please go to DEEPFACE(https://github.com/serengil/deepface) to get the value. For other apis , please subscribe them and get your own token and put into the file

For the GAN we used for CELEB-HQ, please use InterFACE-GAN(https://github.com/genforce/interfacegan) to control the subgroup generation. To predict the ground truth label, please use the classfier we mentioned in paper.

# Detailed Implemention for models and dataset
You should create two directory named samples and models to store the generated samples and robust models.

robustbench and autoattack modules are needed to install first

Due to the limitation of file size, we did not provide samples dataset and code for gan to generate it , you can use a package named StudioGAN(https://github.com/POSTECH-CVLab/PyTorch-StudioGAN) to generate it. By downloading the checkpoint of GAN, you can get the sampled generated by following command:

### CUDA_VISIBLE_DEVICES=1   python3 src/main.py -s -cfg PyTorch-StudioGAN/src/configs/CIFAR10/StyleGAN2-D2DCE-ADA.yaml -ckpt ckpt/ -metrics is --data_dir data/cifar10

Any other sampled dataset with npz file and  contains a x group for image features and a y group for labels can also be used in the code.

# Detailed setting for evaluate the score
We set 3 sub settings in the code that --lower_bound_eval_global,  and  which will run cw attack on 1000 images and reported average distortion , to get the true average distortion, you need to store the cw attack per image as an npy file and ignore the image that wrongly classified.

--lower_bound_eval_local will run cw attack on 50 images and report distortion for each image to compare with GREAT score.

--robust_accuracy will run autoattack on generated samples to report the autoattack accuracy.

You can modify the sample size in each subsettings to change the number of samples you want evaluate on.
