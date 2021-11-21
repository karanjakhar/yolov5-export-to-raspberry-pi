# Yolov5 export to Raspberry Pi

![img](images/busyolov5_output.jpg)

It is a two step process:

1. Convert model weights to tflite
2. Run the inference on Raspberry Pi



### Convert Model Weights to tflite



**If you don't want to install anything on your system then use this [Google Colab](https://colab.research.google.com/drive/1oZN9azdFyrlbzeVcGaqdddJ_YVatVTJJ?usp=sharing) (*Recommended*).**  [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1oZN9azdFyrlbzeVcGaqdddJ_YVatVTJJ?usp=sharing)



##### And if you want to perform the conversion on your system then follow bellow instructions:

I recommend create a new conda environment for this as we need python==3.7.0 for this: 

```
conda create -n yolov5_env python==3.7.0
conda activate yolov5_env
```

Then run below commands and replace **yolov5s.pt** with your own model path and also change **yolov5s.yaml** accordingly. 

```bash
git clone https://github.com/ultralytics/yolov5.git
cd yolov5
pip3 install tensorflow==2.3.1
pip install -r requirements.txt
python3 export.py --weights yolov5s.pt --img 418 --batch 1 --include onnx tflite
```



### Run the inference on Raspberry Pi

Just clone this repository and we are good to go:

```bash
git clone https://github.com/karanjakhar/yolov5-export-to-raspberry-pi.git
cd yolov5-export-to-raspberry-pi
chmod +x setup.sh
./setup.sh
python3 yolov5_tflite_folder_of_images_inference.py --weights yolov5s-fp16.tflite --folder_path images/ 
```

Move your own model tflite file to raspberry pi and use that with above command. 



**yolov5_tflite_inference.py**   this file contains main inference code which you can use with your own project. 

Other files show examples how to use it. I have placed a tflite file and some sample images to run a quick test. 





**To Run Examples:** 

For webcam:

`python3 yolov5_tflite_webcam_inference.py -w yolov5s-fp16.tflite  `

For image:

`python3 yolov5_tflite_image_inference.py -w yolov5s-fp16.tflite -i images/bus.jpg`

For video:

`python3 yolov5_tflite_video_inference.py -w yolov5s-fp16.tflite -v <your video path>`

For folder of images:

`python3 yolov5_tflite_folder_of_images_inference.py -w yolov5s-fp16.tflite -f images/`

