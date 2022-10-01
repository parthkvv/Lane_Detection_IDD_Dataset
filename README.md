### Data Preparation 

The training samples consist of three components, a binary segmentation label file, a instance segmentation label
file and the original image. The binary segmentation uses 255 to represent the lane field and 0 for the rest. The 
instance use different pixel value to represent different lane field and 0 for the rest.

Image scaling will be done according to config file in similar manner for all images.

Generating tensorflow records file

```
python tools/make_tusimple_tfrecords.py 
```

	Set the path till "dataset\train_set" in config.py file

	"dataset\train_set" directory should consist of following files:
		"train_img" - Folder containing all the ground truth images
		"train_seg_img" - Folder containing all the binary label images

		"val_img" - Folder containing all the ground truth images
		"val_seg_img" - Folder containing all the binary label images
	
	txt_file_gen_SCNN.py
		- generate txt files from image dataset, saved in dataset/train_set/seg_label/list
		  "train_gt.txt"
		  "val_gt.txt"
		  "test_gt.txt"	
      
### Train 

- tools/train.py --exp_dir ./experiments/exp0 
 
saved models
	- \experiments\exp0\

	Number of epochs 
	- \experiments\exp0\cfg.json
	"MAX_EPOCHES": 60


```
python tools/train_lanenet_tusimple.py 
```

### Test


	- \tools\demo_test.py -i E:\Abhishek\Lane_Detection\CULane\parth\SCNN\SCNN_Pytorch-master\demo\demo.jpg -w E:\Abhishek\Lane_Detection\CULane\parth\SCNN\SCNN_Pytorch-master\experiments\exp0\exp0_best.pth


	- EVALUATE ON CUSTOM TEST DATASET :
		test_tusimple.py --exp_dir ./experiments/exp0 (keep one category of test data at a time)
    
### Evaluation

	- \dataset\Evaluate\
		- Generate csv files with results

![scnnroad](https://user-images.githubusercontent.com/56112545/189868203-7cd4a737-6d6f-41cf-a75d-31f543ae75a0.jpg)
![binary_output_final](https://user-images.githubusercontent.com/56112545/189868231-304cd005-1697-447c-b311-133377fed8d1.jpg)
