# Recyclable Object Classifier

 This project is meant to help the world. It can classify different items as recyclable, and what type of material it is. By being able to classify these objects, it enables others to utlize its features to become more eco friendly. Less items that can be reused for better will end up in a landfill. By using this code, it creates a healthier Earth.

![Recyclable Plastic Water Bottle]    image link - [Imgur](https://imgur.com/YFmlLII)

## The Algorithm

 The first thing you need to do for this project is to download a dataset used in this project. This downloads images of recyclable materials. You then run an unzip command to provide access to all of the images in the dataset. In this project, it is necessary to have a jetson-inference library. From this folder, run the docker command to run the container. For the most accurate results of classifying materials, it is important to retrain the model. This allows it to have a greater chance of classifying images, as it is more trained. To retrain the model, you must be in the docker container. When retraining, the directory must be jetson-inference/python/training/classification, as this is where the data and plastics folder is located. It is recommended to set epochs to at least 15, as it will provide more accurate conclusions. While continuing to be in the docker container, export the model. Once the model is exported, set NET=models/plastics and DATASET=data/plastics. Once these are set, it is time to run the model. The command used will output the class the model thinks the image is and how confident it is, using a percentage.
 -The model uses the resnet-18 network.

## Running this project

1. Download dataset
2. Unzip file
3. Download jetson-inference library
4. Run docker container in jetson-inference directory: ./docker/run.sh
5. Retrain model in classification folder(cd jetson-inference/python/training/classification):  python3 train.py --model-dir=models/plastics --epochs=(recommended at least 15) --workers=1 --batch-size=4 data/plastics
6. Export model: python3 onnx_export.py --model-dir=models/plastics
7. Exit docker (ctrl + d)
8. Stay in classification folder
9. Run: NET=models/plastics
10. Run: DATASET=data/plastics
11. Run model: imagenet.py --model=$NET/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=$DATASET/labels.txt $DATASET/test/(Chosen Material)/(Image Name).

Video link for demonstration - https://youtu.be/_J-M2iX0w2w
