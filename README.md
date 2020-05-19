# SfM

# Authors
Akanksha Patel
Sri Manika Makam

# Instructions to train 

Download the given dataset where train.py code is present and run the following command. 

```
python train.py --dataset_dir=TrainingAndValData/ --checkpoint_dir=Checkpoints/Train --img_width=416 --img_height=128 --batch_size=4
```
The checkpoints and logs are stored Checkpoints/Train directory.

# Testing for depth

Download a dataset for which we know the velodyn points to 'TestSetDepth' directory. Change the 'data/kitti/test_files_eigen.txt' accordingly. Here, I have used '2011_09_26_drive_0002_sync' and it's corresponding test_files_eigen.txt is submitted. Create a 'depth_images' folder in 'predictions/' and run the following command. 

```
python test_kitti_depth.py --dataset_dir TestSetDepth/ --output_dir predictions/ --ckpt_file Checkpoints/Train/model.latest
```
The precition file is generated in 'predictions directory as 'model.latest.npy'. Depth images are saved in 'predictions/depth_images'.

For evaluation, run the following command

```
python kitti_eval/eval_depth.py --kitti_dir=TestSetDepth/ --pred_file=predictions/model.latest.npy
```

# Testing for pose 

I have used sequences 9 and 10 for which the ground truths were availble. We can generate our predictions by running the following command 

```
python test_kitti_pose.py --test_seq 09 --dataset_dir TestSetPose/ --output_dir predictions/09/ --ckpt_file Checkpoints/Train/model.latest
```
For evaluation, we can run the command

```
python kitti_eval/eval_pose.py --gtruth_dir=TestSetPose/sequences/ground_truth/09/ --pred_dir=predictions/09/
```
The same can be followed for any sequence by changing the 'test_seg' argument acoordingly. 
