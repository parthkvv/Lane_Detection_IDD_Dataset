pip3 install -r requirements.txt

### Test model
The trained lanenet model weights files are stored in 
[lanenet_pretrained_model](https://www.dropbox.com/sh/0b6r0ljqi76kyg9/AADedYWO3bnx4PhK1BmbJkJKa?dl=0). You can 
download the model and put them in folder model/tusimple_lanenet/

Testing a single image on the trained model as follows

```
python tools/test_lanenet.py --weights_path /PATH/TO/YOUR/CKPT_FILE_PATH 
--image_path ./data/tusimple_test_image/0.jpg
```

Evaluation on tusimple test dataset 
```
python tools/evaluate_lanenet_on_tusimple.py 
--image_dir ROOT_DIR/TUSIMPLE_DATASET/test_set/clips 
--weights_path /PATH/TO/YOUR/CKPT_FILE_PATH 
--save_dir ROOT_DIR/TUSIMPLE_DATASET/test_set/test_output
```
save_dir argument saved result in that folder 
or the result will not be saved but be 
displayed during the inference process holding on 3 seconds per image. 

### Custom model Data Preparation 
Organize your training data refer to the data/training_data_example folder structure. And you need 
to generate a train.txt and a val.txt to record the data used for training the model. 

The training samples consist of three components, a binary segmentation label file, a instance segmentation label
file and the original image. The binary segmentation uses 255 to represent the lane field and 0 for the rest. The 
instance use different pixel value to represent different lane field and 0 for the rest.

Image scaling will be done according to config file in similar manner for all images.

Generating tensorflow records file

```
python tools/make_tusimple_tfrecords.py 
```

### Train model
Check the global_configuration/config.py for details about training parameters. 
You can switch --net argument to change the base encoder stage. If you choose --net vgg then the vgg16 will be used as 
the base encoder stage and a pretrained parameters will be loaded. And you can modified the training 
script to load your own pretrained parameters or you can implement your own base encoder stage. 
Script

```
python tools/train_lanenet_tusimple.py 
```

### Generate from Tusimple
Generate the training samples from Tusimple dataset. 
Download the Tusimple dataset and unzip the  file to your local disk. Then run the following command to generate the 
training samples and the train.txt file.

```
python tools/generate_tusimple_dataset.py --src_dir path/to/your/unzipped/file
```

The script will make the train folder and the test folder. The training 
samples of origin rgb image, binary label image, instance label image will
be automatically generated in the training/gt_image, training/gt_binary_image,
training/gt_instance_image folder.


![scnnroad](https://user-images.githubusercontent.com/56112545/189868203-7cd4a737-6d6f-41cf-a75d-31f543ae75a0.jpg)
![binary_output_final](https://user-images.githubusercontent.com/56112545/189868231-304cd005-1697-447c-b311-133377fed8d1.jpg)
