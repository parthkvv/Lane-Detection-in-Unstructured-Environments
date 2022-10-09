### Dataset Preparation
	set the path till "dataset\train_set" in config.py file

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

### CULane format data (Optional) 

```
CULane
├── driver_100_30frame
├── driver_161_90frame
├── driver_182_30frame
├── driver_193_90frame
├── driver_23_30frame
├── driver_37_30frame
├── laneseg_label_w16
├── laneseg_label_w16_test
└── list
```

 Note: Enter absolute path.

### Tusimple format data (Optional) 

```
Tusimple
├── clips
├── label_data_0313.json
├── label_data_0531.json
├── label_data_0601.json
└── test_label.json
```


### Trained Model 

Model trained on CULane Dataset can be converted from [official implementation](https://github.com/XingangPan/SCNN#Testing)， which can be downloaded [here](https://drive.google.com/open?id=1Wv3r3dCYNBwJdKl_WPEfrEOt-XGaROKu). Please put the `vgg_SCNN_DULR_w9.t7` file into `experiments/vgg_SCNN_DULR_w9`.

  ```bash
  python experiments/vgg_SCNN_DULR_w9/t7_to_pt.py
  ```

Model will be cached into `experiments/vgg_SCNN_DULR_w9/vgg_SCNN_DULR_w9.pth`. 


For single image demo test:

```shell
python demo_test.py   -i demo/demo.jpg 
                      -w experiments/vgg_SCNN_DULR_w9/vgg_SCNN_DULR_w9.pth 
                      [--visualize / -v]
```

### Train 

1. Specify an experiment directory, e.g. `experiments/exp0`. 

2. Modify the hyperparameters in `experiments/exp0/cfg.json`.

	saved models
	- \experiments\exp0\

	Number of epochs 
	- \experiments\exp0\cfg.json
	"MAX_EPOCHES": 60

3. Start training:

   ```shell
	- tools/train.py --exp_dir ./experiments/exp0 [--resume/-r]
   ```

4. Monitor on tensorboard:

   ```bash
   tensorboard --logdir='experiments/exp0'
   ```

### Test

  ``` shell
  python demo_test.py -i E:\Abhishek\Lane_Detection\CULane\parth\SCNN\SCNN_Pytorch-master\demo\demo.jpg -w E:\Abhishek\Lane_Detection\CULane\parth\SCNN\SCNN_Pytorch-master\experiments\exp0\exp0_best.pth
  ```

  - EVALUATE ON CUSTOM TEST DATASET :
	test_tusimple.py --exp_dir ./experiments/exp0 (keep one category of test data at a time)

  (Optional) For Tusimple 

  ```Shell
  python test_tusimple.py --exp_dir ./experiments/exp0
  ```

### Evaluation

  ``` shell
  - \dataset\Evaluate\
		- Generate csv files with results
  ```
  
  
  
### Demo
![lane_final](https://user-images.githubusercontent.com/56112545/190910553-29415c2e-218e-40fe-a40d-132df58852a5.gif)

