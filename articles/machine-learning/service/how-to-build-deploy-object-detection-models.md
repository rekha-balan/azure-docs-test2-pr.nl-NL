---
title: Build and deploy an object detection model using Azure Machine Learning Package for Computer Vision.
description: Learn how to build, train, test and deploy a computer vision object detection model using the Azure Machine Learning Package for Computer Vision.
services: machine-learning
ms.service: machine-learning
ms.component: core
ms.topic: conceptual
ms.reviewer: jmartens
ms.author: netahw
author: nhaiby
ms.date: 06/01/2018
ms.openlocfilehash: 44059de5a0ef0667b4268d9cdc2997162bab474a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864456"
---
# <a name="build-and-deploy-object-detection-models-with-azure-machine-learning"></a><span data-ttu-id="97b53-103">Build and deploy object detection models with Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="97b53-103">Build and deploy object detection models with Azure Machine Learning</span></span>

<span data-ttu-id="97b53-104">In this article, learn how to use **Azure Machine Learning Package for Computer Vision** to train, test, and deploy a [Faster R-CNN](https://arxiv.org/abs/1506.01497) object detection model.</span><span class="sxs-lookup"><span data-stu-id="97b53-104">In this article, learn how to use **Azure Machine Learning Package for Computer Vision** to train, test, and deploy a [Faster R-CNN](https://arxiv.org/abs/1506.01497) object detection model.</span></span> 

<span data-ttu-id="97b53-105">A large number of problems in the computer vision domain can be solved using object detection.</span><span class="sxs-lookup"><span data-stu-id="97b53-105">A large number of problems in the computer vision domain can be solved using object detection.</span></span> <span data-ttu-id="97b53-106">These problems include building models that find a variable number of objects on an image.</span><span class="sxs-lookup"><span data-stu-id="97b53-106">These problems include building models that find a variable number of objects on an image.</span></span> 

<span data-ttu-id="97b53-107">When building and deploying this model with this package, you go through the following steps:</span><span class="sxs-lookup"><span data-stu-id="97b53-107">When building and deploying this model with this package, you go through the following steps:</span></span>
1.  <span data-ttu-id="97b53-108">Dataset Creation</span><span class="sxs-lookup"><span data-stu-id="97b53-108">Dataset Creation</span></span>
2.  <span data-ttu-id="97b53-109">Deep Neural Network (DNN) Model Definition</span><span class="sxs-lookup"><span data-stu-id="97b53-109">Deep Neural Network (DNN) Model Definition</span></span>
3.  <span data-ttu-id="97b53-110">Model Training</span><span class="sxs-lookup"><span data-stu-id="97b53-110">Model Training</span></span>
4.  <span data-ttu-id="97b53-111">Evaluation and Visualization</span><span class="sxs-lookup"><span data-stu-id="97b53-111">Evaluation and Visualization</span></span>
5.  <span data-ttu-id="97b53-112">Web service Deployment</span><span class="sxs-lookup"><span data-stu-id="97b53-112">Web service Deployment</span></span>
6.  <span data-ttu-id="97b53-113">Web service Load Testing</span><span class="sxs-lookup"><span data-stu-id="97b53-113">Web service Load Testing</span></span>

<span data-ttu-id="97b53-114">In this example, TensorFlow is used as the deep learning framework, training is performed locally on a GPU powered machine such as the [Deep learning Data Science VM](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft-ads.dsvm-deep-learning?tab=Overview), and deployment uses the Azure ML Operationalization CLI.</span><span class="sxs-lookup"><span data-stu-id="97b53-114">In this example, TensorFlow is used as the deep learning framework, training is performed locally on a GPU powered machine such as the [Deep learning Data Science VM](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft-ads.dsvm-deep-learning?tab=Overview), and deployment uses the Azure ML Operationalization CLI.</span></span>

<span data-ttu-id="97b53-115">Consult the [package reference documentation](https://aka.ms/aml-packages/vision) for the detailed reference for each module and class.</span><span class="sxs-lookup"><span data-stu-id="97b53-115">Consult the [package reference documentation](https://aka.ms/aml-packages/vision) for the detailed reference for each module and class.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="97b53-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="97b53-116">Prerequisites</span></span>

1. <span data-ttu-id="97b53-117">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="97b53-117">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

1. <span data-ttu-id="97b53-118">The following accounts and application must be set up and installed:</span><span class="sxs-lookup"><span data-stu-id="97b53-118">The following accounts and application must be set up and installed:</span></span>
   - <span data-ttu-id="97b53-119">An Azure Machine Learning Experimentation account</span><span class="sxs-lookup"><span data-stu-id="97b53-119">An Azure Machine Learning Experimentation account</span></span> 
   - <span data-ttu-id="97b53-120">An Azure Machine Learning Model Management account</span><span class="sxs-lookup"><span data-stu-id="97b53-120">An Azure Machine Learning Model Management account</span></span>
   - <span data-ttu-id="97b53-121">Azure Machine Learning Workbench installed</span><span class="sxs-lookup"><span data-stu-id="97b53-121">Azure Machine Learning Workbench installed</span></span>

   <span data-ttu-id="97b53-122">If these three are not yet created or installed, follow the [Azure Machine Learning Quickstart and Workbench installation](../service/quickstart-installation.md) article.</span><span class="sxs-lookup"><span data-stu-id="97b53-122">If these three are not yet created or installed, follow the [Azure Machine Learning Quickstart and Workbench installation](../service/quickstart-installation.md) article.</span></span> 

1. <span data-ttu-id="97b53-123">The Azure Machine Learning Package for Computer Vision must be installed.</span><span class="sxs-lookup"><span data-stu-id="97b53-123">The Azure Machine Learning Package for Computer Vision must be installed.</span></span> <span data-ttu-id="97b53-124">Learn how to [install this package here](https://aka.ms/aml-packages/vision).</span><span class="sxs-lookup"><span data-stu-id="97b53-124">Learn how to [install this package here](https://aka.ms/aml-packages/vision).</span></span>

## <a name="sample-data-and-notebook"></a><span data-ttu-id="97b53-125">Sample data and notebook</span><span class="sxs-lookup"><span data-stu-id="97b53-125">Sample data and notebook</span></span>

### <a name="get-the-jupyter-notebook"></a><span data-ttu-id="97b53-126">Get the Jupyter notebook</span><span class="sxs-lookup"><span data-stu-id="97b53-126">Get the Jupyter notebook</span></span>

<span data-ttu-id="97b53-127">Download the notebook to run the sample described here yourself.</span><span class="sxs-lookup"><span data-stu-id="97b53-127">Download the notebook to run the sample described here yourself.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="97b53-128">Get the Jupyter notebook</span><span class="sxs-lookup"><span data-stu-id="97b53-128">Get the Jupyter notebook</span></span>](https://aka.ms/aml-packages/vision/notebooks/object_detection)

### <a name="load-the-sample-data"></a><span data-ttu-id="97b53-129">Load the sample data</span><span class="sxs-lookup"><span data-stu-id="97b53-129">Load the sample data</span></span>

<span data-ttu-id="97b53-130">For this demo, a dataset of grocery items inside refrigerators is provided, consisting of 30 images and 8 classes (eggBox, joghurt, ketchup, mushroom, mustard, orange, squash, and water).</span><span class="sxs-lookup"><span data-stu-id="97b53-130">For this demo, a dataset of grocery items inside refrigerators is provided, consisting of 30 images and 8 classes (eggBox, joghurt, ketchup, mushroom, mustard, orange, squash, and water).</span></span> <span data-ttu-id="97b53-131">For each jpg image, there's an annotation xml-file with similar name.</span><span class="sxs-lookup"><span data-stu-id="97b53-131">For each jpg image, there's an annotation xml-file with similar name.</span></span> 

<span data-ttu-id="97b53-132">The following figure shows the recommended folder structure.</span><span class="sxs-lookup"><span data-stu-id="97b53-132">The following figure shows the recommended folder structure.</span></span> 

![folder structure](media/how-to-build-deploy-object-detection-models/data_directory.JPG)

## <a name="image-annotation"></a><span data-ttu-id="97b53-134">Image Annotation</span><span class="sxs-lookup"><span data-stu-id="97b53-134">Image Annotation</span></span>

<span data-ttu-id="97b53-135">Annotated object locations are required to train and evaluate an object detector.</span><span class="sxs-lookup"><span data-stu-id="97b53-135">Annotated object locations are required to train and evaluate an object detector.</span></span> <span data-ttu-id="97b53-136">[LabelImg](https://tzutalin.github.io/labelImg) is an open source annotation tool that can be used to annotate images.</span><span class="sxs-lookup"><span data-stu-id="97b53-136">[LabelImg](https://tzutalin.github.io/labelImg) is an open source annotation tool that can be used to annotate images.</span></span> <span data-ttu-id="97b53-137">LabelImg writes an xml-file per image in Pascal-VOC format, which can be read by this package.</span><span class="sxs-lookup"><span data-stu-id="97b53-137">LabelImg writes an xml-file per image in Pascal-VOC format, which can be read by this package.</span></span> 


```python
import warnings
warnings.filterwarnings("ignore")
import os, time
from cvtk.core import Context, ObjectDetectionDataset, TFFasterRCNN
from cvtk.evaluation import DetectionEvaluation
from cvtk.evaluation.evaluation_utils import graph_error_counts
from cvtk.utils import detection_utils

# Disable printing of logging messages
from azuremltkbase.logging import ToolkitLogger
ToolkitLogger.getInstance().setEnabled(False)

from matplotlib import pyplot as plt
# Display the images
%matplotlib inline
```

## <a name="create-a-dataset"></a><span data-ttu-id="97b53-138">Create a dataset</span><span class="sxs-lookup"><span data-stu-id="97b53-138">Create a dataset</span></span>

<span data-ttu-id="97b53-139">Create a CVTK dataset that consists of a set of images, with their respective bounding box annotations.</span><span class="sxs-lookup"><span data-stu-id="97b53-139">Create a CVTK dataset that consists of a set of images, with their respective bounding box annotations.</span></span> <span data-ttu-id="97b53-140">In this example, the refrigerator images that are provided in the "../sample_data/foods/training" folder are used.</span><span class="sxs-lookup"><span data-stu-id="97b53-140">In this example, the refrigerator images that are provided in the "../sample_data/foods/training" folder are used.</span></span> <span data-ttu-id="97b53-141">Only JPEG images are supported.</span><span class="sxs-lookup"><span data-stu-id="97b53-141">Only JPEG images are supported.</span></span>


```python
image_folder = "detection/sample_data/foods/train"
data_train = ObjectDetectionDataset.create_from_dir(dataset_name='training_dataset', data_dir=image_folder,
                                                    annotations_dir="Annotations", image_subdirectory='JPEGImages')

# Show some statistics of the training image, and also give one example of the ground truth rectangle annotations
data_train.print_info()
_ = data_train.images[2].visualize_bounding_boxes(image_size = (10,10))
```

    F1 2018-05-25 23:12:21,727 INFO azureml.vision:machine info {"is_dsvm": true, "os_type": "Windows"} 
    F1 2018-05-25 23:12:21,733 INFO azureml.vision:dataset creating dataset for scenario=detection 
    Dataset name: training_dataset
    Total classes: 8, total images: 25
    Label-wise object counts:
        Label eggBox: 20 objects
        Label joghurt: 20 objects
        Label ketchup: 20 objects
        Label mushroom: 20 objects
        Label mustard: 20 objects
        Label orange: 20 objects
        Label squash: 40 objects
        Label water: 20 objects
    Bounding box width and height distribution:
        Bounding box widths  0/5/25/50/75/95/100-percentile: 54/61/79/117/133/165/311 pixels
        Bounding box heights 0/5/25/50/75/95/100-percentile: 48/58/75/124/142/170/212 pixels
    


![png](media/how-to-build-deploy-object-detection-models/output_6_1.JPG)


## <a name="define-a-model"></a><span data-ttu-id="97b53-143">Define a model</span><span class="sxs-lookup"><span data-stu-id="97b53-143">Define a model</span></span>

<span data-ttu-id="97b53-144">In this example, the Faster R-CNN model is used.</span><span class="sxs-lookup"><span data-stu-id="97b53-144">In this example, the Faster R-CNN model is used.</span></span> <span data-ttu-id="97b53-145">Various parameters can be provided when defining this model.</span><span class="sxs-lookup"><span data-stu-id="97b53-145">Various parameters can be provided when defining this model.</span></span> <span data-ttu-id="97b53-146">The meaning of these parameters, as well as the parameters used for training (see next section) can be found in either CVTK's API docs, or on the [Tensorflow object detection website](https://github.com/tensorflow/models/tree/master/research/object_detection).</span><span class="sxs-lookup"><span data-stu-id="97b53-146">The meaning of these parameters, as well as the parameters used for training (see next section) can be found in either CVTK's API docs, or on the [Tensorflow object detection website](https://github.com/tensorflow/models/tree/master/research/object_detection).</span></span> <span data-ttu-id="97b53-147">More information about Faster R-CNN model can be found at [this link](https://docs.microsoft.com/en-us/cognitive-toolkit/Object-Detection-using-Faster-R-CNN#technical-details).</span><span class="sxs-lookup"><span data-stu-id="97b53-147">More information about Faster R-CNN model can be found at [this link](https://docs.microsoft.com/en-us/cognitive-toolkit/Object-Detection-using-Faster-R-CNN#technical-details).</span></span> <span data-ttu-id="97b53-148">This model is based on Fast R-CNN and more information about it can be found [here](https://docs.microsoft.com/en-us/cognitive-toolkit/Object-Detection-using-Fast-R-CNN#algorithm-details).</span><span class="sxs-lookup"><span data-stu-id="97b53-148">This model is based on Fast R-CNN and more information about it can be found [here](https://docs.microsoft.com/en-us/cognitive-toolkit/Object-Detection-using-Fast-R-CNN#algorithm-details).</span></span>


```python
score_threshold = 0.0       # Threshold on the detection score, use to discard lower-confidence detections.
max_total_detections = 300  # Maximum number of detections. A high value slows down training but might increase accuracy.
my_detector = TFFasterRCNN(labels=data_train.labels, 
                           score_threshold=score_threshold, 
                           max_total_detections=max_total_detections)
```

## <a name="train-the-model"></a><span data-ttu-id="97b53-149">Train the model</span><span class="sxs-lookup"><span data-stu-id="97b53-149">Train the model</span></span>

<span data-ttu-id="97b53-150">The COCO-trained Faster R-CNN model with ResNet50 is used as the starting point for training.</span><span class="sxs-lookup"><span data-stu-id="97b53-150">The COCO-trained Faster R-CNN model with ResNet50 is used as the starting point for training.</span></span> 

<span data-ttu-id="97b53-151">To train the detector, the number of training steps in the code is set to 350, so that training runs more quickly (~5 minutes with GPU).</span><span class="sxs-lookup"><span data-stu-id="97b53-151">To train the detector, the number of training steps in the code is set to 350, so that training runs more quickly (~5 minutes with GPU).</span></span> <span data-ttu-id="97b53-152">In practice, set it to at least 10 times the number of images in the training set.</span><span class="sxs-lookup"><span data-stu-id="97b53-152">In practice, set it to at least 10 times the number of images in the training set.</span></span>

<span data-ttu-id="97b53-153">In this example, the number of detector training steps is set to 350 for speedy training.</span><span class="sxs-lookup"><span data-stu-id="97b53-153">In this example, the number of detector training steps is set to 350 for speedy training.</span></span> <span data-ttu-id="97b53-154">However, in practice, a good rule of thumb is to set the steps to 10 or more times the number of images in the training set.</span><span class="sxs-lookup"><span data-stu-id="97b53-154">However, in practice, a good rule of thumb is to set the steps to 10 or more times the number of images in the training set.</span></span>

<span data-ttu-id="97b53-155">Two key parameters for training are:</span><span class="sxs-lookup"><span data-stu-id="97b53-155">Two key parameters for training are:</span></span>
- <span data-ttu-id="97b53-156">Number of steps to train the model, represented by the num_seps argument.</span><span class="sxs-lookup"><span data-stu-id="97b53-156">Number of steps to train the model, represented by the num_seps argument.</span></span> <span data-ttu-id="97b53-157">Each step trains the model with a minibatch of batch size one.</span><span class="sxs-lookup"><span data-stu-id="97b53-157">Each step trains the model with a minibatch of batch size one.</span></span>
- <span data-ttu-id="97b53-158">Learning rate(s), which can be set by initial_learning_rate</span><span class="sxs-lookup"><span data-stu-id="97b53-158">Learning rate(s), which can be set by initial_learning_rate</span></span>

```python
print("tensorboard --logdir={}".format(my_detector.train_dir))

# to get good results, use a larger value for num_steps, e.g., 5000.
num_steps = 350
learning_rate = 0.001 # learning rate

start_train = time.time()
my_detector.train(dataset=data_train, num_steps=num_steps, 
                  initial_learning_rate=learning_rate)
end_train = time.time()
print(end_train-start_train)
```

    tensorboard --logdir=C:\Users\lixun\Desktop\AutoDL\CVTK\Src\API\cvtk_output\temp_faster_rcnn_resnet50\models\train
    F1 2018-05-25 23:12:22,764 INFO azureml.vision:Fit starting in experiment  1125722225 
    F1 2018-05-25 23:12:22,767 INFO azureml.vision:model starting trainging for scenario=detection 
    Using existing checkpoint file that's saved at 'C:\Users\lixun\Desktop\AutoDL\CVTK\Src\API\cvtk_output\models\detection\faster_rcnn_resnet50_coco_2018_01_28\model.ckpt.index'.
    TFRecords creation started.
    F1 2018-05-25 23:12:22,773 INFO On image 0 of 25
    TFRecords creation completed.
    Training started.
    Training progressing: step 0 ...
    Training progressing: step 100 ...
    Training progressing: step 200 ...
    Training progressing: step 300 ...
    F1 2018-05-25 23:18:02,730 INFO Graph Rewriter optimizations enabled
    Converted 275 variables to const ops.
    F1 2018-05-25 23:18:10,722 INFO 2953 ops in the final graph.
    F1 2018-05-25 23:18:24,244 INFO azureml.vision:Fit finished in experiment  1125722225 
    Training completed.
    361.604615688324
    

<span data-ttu-id="97b53-159">TensorBoard can be used to visualize the training progress.</span><span class="sxs-lookup"><span data-stu-id="97b53-159">TensorBoard can be used to visualize the training progress.</span></span> <span data-ttu-id="97b53-160">TensorBoard events are located in the folder specified by the model object's train_dir attribute.</span><span class="sxs-lookup"><span data-stu-id="97b53-160">TensorBoard events are located in the folder specified by the model object's train_dir attribute.</span></span> <span data-ttu-id="97b53-161">To view TensorBoard, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="97b53-161">To view TensorBoard, follow these steps:</span></span>
1. <span data-ttu-id="97b53-162">Copy the printout that starts with 'tensorboard --logdir' to a command line and run it.</span><span class="sxs-lookup"><span data-stu-id="97b53-162">Copy the printout that starts with 'tensorboard --logdir' to a command line and run it.</span></span> 
2. <span data-ttu-id="97b53-163">Copy the returned URL from the command line to a web browser to view the TensorBoard.</span><span class="sxs-lookup"><span data-stu-id="97b53-163">Copy the returned URL from the command line to a web browser to view the TensorBoard.</span></span> 

<span data-ttu-id="97b53-164">The TensorBoard should look like the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="97b53-164">The TensorBoard should look like the following screenshot.</span></span> <span data-ttu-id="97b53-165">It takes a few moments for the training folder to be populated.</span><span class="sxs-lookup"><span data-stu-id="97b53-165">It takes a few moments for the training folder to be populated.</span></span> <span data-ttu-id="97b53-166">So if TensorBoard does not show up correctly the first time try repeating steps 1-2.</span><span class="sxs-lookup"><span data-stu-id="97b53-166">So if TensorBoard does not show up correctly the first time try repeating steps 1-2.</span></span>  

![tensorboard](media/how-to-build-deploy-object-detection-models/tensorboard.JPG)

## <a name="evaluate-the-model"></a><span data-ttu-id="97b53-168">Evaluate the model</span><span class="sxs-lookup"><span data-stu-id="97b53-168">Evaluate the model</span></span>

<span data-ttu-id="97b53-169">The 'evaluate' method is used to evaluate the model.</span><span class="sxs-lookup"><span data-stu-id="97b53-169">The 'evaluate' method is used to evaluate the model.</span></span> <span data-ttu-id="97b53-170">This function requires an ObjectDetectionDataset object as an input.</span><span class="sxs-lookup"><span data-stu-id="97b53-170">This function requires an ObjectDetectionDataset object as an input.</span></span> <span data-ttu-id="97b53-171">The evaluation dataset can be created using the same function as the one used for the training dataset.</span><span class="sxs-lookup"><span data-stu-id="97b53-171">The evaluation dataset can be created using the same function as the one used for the training dataset.</span></span> <span data-ttu-id="97b53-172">The supported metric is Average Precision as defined for the [PASCAL VOC Challenge](http://host.robots.ox.ac.uk/pascal/VOC/pubs/everingham10.pdf).</span><span class="sxs-lookup"><span data-stu-id="97b53-172">The supported metric is Average Precision as defined for the [PASCAL VOC Challenge](http://host.robots.ox.ac.uk/pascal/VOC/pubs/everingham10.pdf).</span></span>  


```python
image_folder = "detection/sample_data/foods/test"
data_val = ObjectDetectionDataset.create_from_dir(dataset_name='val_dataset', data_dir=image_folder)
eval_result = my_detector.evaluate(dataset=data_val)
```

    F1 2018-05-25 23:18:24,253 INFO azureml.vision:dataset creating dataset for scenario=detection 
    F1 2018-05-25 23:18:24,286 INFO On image 0 of 5
    F1 2018-05-25 23:18:29,300 INFO Starting evaluation at 2018-05-26-03:18:29
    F1 2018-05-25 23:18:32,403 INFO Creating detection visualizations.
    F1 2018-05-25 23:18:33,158 INFO Detection visualizations written to summary with tag image-0.
    F1 2018-05-25 23:18:33,518 INFO Creating detection visualizations.
    F1 2018-05-25 23:18:34,342 INFO Detection visualizations written to summary with tag image-1.
    F1 2018-05-25 23:18:34,714 INFO Creating detection visualizations.
    F1 2018-05-25 23:18:35,470 INFO Detection visualizations written to summary with tag image-2.
    F1 2018-05-25 23:18:35,835 INFO Creating detection visualizations.
    F1 2018-05-25 23:18:36,654 INFO Detection visualizations written to summary with tag image-3.
    F1 2018-05-25 23:18:37,010 INFO Creating detection visualizations.
    F1 2018-05-25 23:18:37,798 INFO Detection visualizations written to summary with tag image-4.
    F1 2018-05-25 23:18:37,804 INFO Running eval batches done.
    F1 2018-05-25 23:18:37,805 INFO # success: 5
    F1 2018-05-25 23:18:37,806 INFO # skipped: 0
    F1 2018-05-25 23:18:38,119 INFO Writing metrics to tf summary.
    F1 2018-05-25 23:18:38,121 INFO PASCAL/PerformanceByCategory/AP@0.5IOU/eggBox: 1.000000
    F1 2018-05-25 23:18:38,205 INFO PASCAL/PerformanceByCategory/AP@0.5IOU/joghurt: 0.942857
    F1 2018-05-25 23:18:38,206 INFO PASCAL/PerformanceByCategory/AP@0.5IOU/ketchup: 1.000000
    F1 2018-05-25 23:18:38,207 INFO PASCAL/PerformanceByCategory/AP@0.5IOU/mushroom: 1.000000
    F1 2018-05-25 23:18:38,208 INFO PASCAL/PerformanceByCategory/AP@0.5IOU/mustard: 1.000000
    F1 2018-05-25 23:18:38,209 INFO PASCAL/PerformanceByCategory/AP@0.5IOU/orange: 1.000000
    F1 2018-05-25 23:18:38,210 INFO PASCAL/PerformanceByCategory/AP@0.5IOU/squash: 1.000000
    F1 2018-05-25 23:18:38,211 INFO PASCAL/PerformanceByCategory/AP@0.5IOU/water: 1.000000
    F1 2018-05-25 23:18:38,211 INFO PASCAL/Precision/mAP@0.5IOU: 0.992857
    F1 2018-05-25 23:18:38,253 INFO Metrics written to tf summary.
    F1 2018-05-25 23:18:38,254 INFO Finished evaluation!
    

<span data-ttu-id="97b53-173">The evaluation results can be printed out in a clean format.</span><span class="sxs-lookup"><span data-stu-id="97b53-173">The evaluation results can be printed out in a clean format.</span></span>


```python
# print out the performance metric values
for label_obj in data_train.labels:
    label = label_obj.name
    key = 'PASCAL/PerformanceByCategory/AP@0.5IOU/' + label
    print('{0: <15}: {1: <3}'.format(label, round(eval_result[key], 2)))
print('{0: <15}: {1: <3}'.format("overall:", round(eval_result['PASCAL/Precision/mAP@0.5IOU'], 2))) 
```

    joghurt        : 0.94
    squash         : 1.0
    mushroom       : 1.0
    eggBox         : 1.0
    ketchup        : 1.0
    mustard        : 1.0
    water          : 1.0
    orange         : 1.0
    overall:       : 0.99
    

<span data-ttu-id="97b53-174">Similarly, you can compute the accuracy of the model on the training set.</span><span class="sxs-lookup"><span data-stu-id="97b53-174">Similarly, you can compute the accuracy of the model on the training set.</span></span> <span data-ttu-id="97b53-175">Doing this helps make sure training converged to a good solution.</span><span class="sxs-lookup"><span data-stu-id="97b53-175">Doing this helps make sure training converged to a good solution.</span></span> <span data-ttu-id="97b53-176">The accuracy on the training set after successful training is often close to 100%.</span><span class="sxs-lookup"><span data-stu-id="97b53-176">The accuracy on the training set after successful training is often close to 100%.</span></span>

<span data-ttu-id="97b53-177">Evaluation results can also be viewed from TensorBoard, including mAP values and images with predicted bounding boxes.</span><span class="sxs-lookup"><span data-stu-id="97b53-177">Evaluation results can also be viewed from TensorBoard, including mAP values and images with predicted bounding boxes.</span></span> <span data-ttu-id="97b53-178">Copy the printout from the following code into a command line window to start the TensorBoard client.</span><span class="sxs-lookup"><span data-stu-id="97b53-178">Copy the printout from the following code into a command line window to start the TensorBoard client.</span></span> <span data-ttu-id="97b53-179">Here a port value 8008 is used to avoid conflict with the default value of 6006, which was using for viewing training status.</span><span class="sxs-lookup"><span data-stu-id="97b53-179">Here a port value 8008 is used to avoid conflict with the default value of 6006, which was using for viewing training status.</span></span>


```python
print("tensorboard --logdir={} --port=8008".format(my_detector.eval_dir))
```

    tensorboard --logdir=C:\Users\lixun\Desktop\AutoDL\CVTK\Src\API\cvtk_output\temp_faster_rcnn_resnet50\models\eval --port=8008
    

## <a name="score-an-image"></a><span data-ttu-id="97b53-180">Score an image</span><span class="sxs-lookup"><span data-stu-id="97b53-180">Score an image</span></span>

<span data-ttu-id="97b53-181">Once you're satisfied with the performance of the trained model, the model object's 'score' function can be used to score new images.</span><span class="sxs-lookup"><span data-stu-id="97b53-181">Once you're satisfied with the performance of the trained model, the model object's 'score' function can be used to score new images.</span></span> <span data-ttu-id="97b53-182">The returned scores can be visualized with the 'visualize' function .</span><span class="sxs-lookup"><span data-stu-id="97b53-182">The returned scores can be visualized with the 'visualize' function .</span></span> 


```python
image_path = data_val.images[1].storage_path
detections_dict = my_detector.score(image_path)
path_save = "./scored_images/scored_image_preloaded.jpg"
ax = detection_utils.visualize(image_path, detections_dict, image_size=(8, 12))
path_save_dir = os.path.dirname(os.path.abspath(path_save))
os.makedirs(path_save_dir, exist_ok=True)
ax.get_figure().savefig(path_save)
```

![png](media/how-to-build-deploy-object-detection-models/output_20_0.JPG)

##  <a name="save-the-model"></a><span data-ttu-id="97b53-184">Save the model</span><span class="sxs-lookup"><span data-stu-id="97b53-184">Save the model</span></span>

<span data-ttu-id="97b53-185">The trained model can be saved to disk, and loaded back into memory, as shown in the following code examples.</span><span class="sxs-lookup"><span data-stu-id="97b53-185">The trained model can be saved to disk, and loaded back into memory, as shown in the following code examples.</span></span>


```python
save_model_path = "./frozen_model/faster_rcnn.model"
my_detector.save(save_model_path)
```

    F1 2018-05-25 23:18:55,166 INFO Graph Rewriter optimizations enabled
    Converted 275 variables to const ops.
    F1 2018-05-25 23:19:03,867 INFO 2953 ops in the final graph.
    

## <a name="load-the-saved-model-for-scoring"></a><span data-ttu-id="97b53-186">Load the saved model for scoring</span><span class="sxs-lookup"><span data-stu-id="97b53-186">Load the saved model for scoring</span></span>

<span data-ttu-id="97b53-187">To use the saved model, load the model into memory with the 'load' function.</span><span class="sxs-lookup"><span data-stu-id="97b53-187">To use the saved model, load the model into memory with the 'load' function.</span></span> <span data-ttu-id="97b53-188">You only need to load once.</span><span class="sxs-lookup"><span data-stu-id="97b53-188">You only need to load once.</span></span> 

```python
my_detector_loaded = TFFasterRCNN.load(save_model_path)
```

<span data-ttu-id="97b53-189">After the model is loaded, it can be used to score an image or a list of images.</span><span class="sxs-lookup"><span data-stu-id="97b53-189">After the model is loaded, it can be used to score an image or a list of images.</span></span> <span data-ttu-id="97b53-190">For a single image, a dictionary is returned with keys such as 'detection_boxes', 'detection_scores', and 'num_detections'.</span><span class="sxs-lookup"><span data-stu-id="97b53-190">For a single image, a dictionary is returned with keys such as 'detection_boxes', 'detection_scores', and 'num_detections'.</span></span> <span data-ttu-id="97b53-191">If the input is a list of images, a list of dictionary is returned, with one dictionary corresponding to one image.</span><span class="sxs-lookup"><span data-stu-id="97b53-191">If the input is a list of images, a list of dictionary is returned, with one dictionary corresponding to one image.</span></span> 


```python
detections_dict = my_detector_loaded.score(image_path)
```

<span data-ttu-id="97b53-192">The detected objects with scores above 0.5, including labels, scores, and coordinates can be printed out.</span><span class="sxs-lookup"><span data-stu-id="97b53-192">The detected objects with scores above 0.5, including labels, scores, and coordinates can be printed out.</span></span>


```python
look_up = dict((v,k) for k,v in my_detector.class_map.items())
n_obj = 0
for i in range(detections_dict['num_detections']):
    if detections_dict['detection_scores'][i] > 0.5:
        n_obj += 1
        print("Object {}: label={:11}, score={:.2f}, location=(top: {:.2f}, left: {:.2f}, bottom: {:.2f}, right: {:.2f})".format(
            i, look_up[detections_dict['detection_classes'][i]], 
            detections_dict['detection_scores'][i], 
            detections_dict['detection_boxes'][i][0],
            detections_dict['detection_boxes'][i][1], 
            detections_dict['detection_boxes'][i][2],
            detections_dict['detection_boxes'][i][3]))    
        
print("\nFound {} objects in image {}.".format(n_obj, image_path))           
```

    Object 0: label=squash     , score=0.99, location=(top: 0.74, left: 0.30, bottom: 0.84, right: 0.42)
    Object 1: label=squash     , score=0.98, location=(top: 0.27, left: 0.21, bottom: 0.37, right: 0.33)
    Object 2: label=orange     , score=0.98, location=(top: 0.31, left: 0.39, bottom: 0.37, right: 0.48)
    Object 3: label=joghurt    , score=0.98, location=(top: 0.57, left: 0.29, bottom: 0.67, right: 0.39)
    Object 4: label=eggBox     , score=0.97, location=(top: 0.41, left: 0.53, bottom: 0.49, right: 0.69)
    Object 5: label=water      , score=0.95, location=(top: 0.23, left: 0.51, bottom: 0.37, right: 0.57)
    Object 6: label=mustard    , score=0.88, location=(top: 0.61, left: 0.47, bottom: 0.66, right: 0.57)
    Object 7: label=ketchup    , score=0.80, location=(top: 0.62, left: 0.62, bottom: 0.68, right: 0.72)
    
    Found 8 objects in image ../sample_data/foods/test\JPEGImages\10.jpg.
    

<span data-ttu-id="97b53-193">Visualize the scores just like before.</span><span class="sxs-lookup"><span data-stu-id="97b53-193">Visualize the scores just like before.</span></span>


```python
path_save = "./scored_images/scored_image_frozen_graph.jpg"
ax = detection_utils.visualize(image_path, detections_dict, path_save=path_save, image_size=(8, 12))
# ax.get_figure() # use this code extract the returned image
```

![png](media/how-to-build-deploy-object-detection-models/output_30_0.JPG)

## <a name="operationalization-deploy-and-consume"></a><span data-ttu-id="97b53-195">Operationalization: deploy and consume</span><span class="sxs-lookup"><span data-stu-id="97b53-195">Operationalization: deploy and consume</span></span>

<span data-ttu-id="97b53-196">Operationalization is the process of publishing models and code as web services and the consumption of these services to produce business results.</span><span class="sxs-lookup"><span data-stu-id="97b53-196">Operationalization is the process of publishing models and code as web services and the consumption of these services to produce business results.</span></span> 

<span data-ttu-id="97b53-197">Once your model is trained, you can deploy that model as a web service for consumption using [Azure Machine Learning CLI](https://docs.microsoft.com/azure/machine-learning/desktop-workbench/cli-for-azure-machine-learning).</span><span class="sxs-lookup"><span data-stu-id="97b53-197">Once your model is trained, you can deploy that model as a web service for consumption using [Azure Machine Learning CLI](https://docs.microsoft.com/azure/machine-learning/desktop-workbench/cli-for-azure-machine-learning).</span></span> <span data-ttu-id="97b53-198">Your models can be deployed to your local machine or Azure Container Service (ACS) cluster.</span><span class="sxs-lookup"><span data-stu-id="97b53-198">Your models can be deployed to your local machine or Azure Container Service (ACS) cluster.</span></span> <span data-ttu-id="97b53-199">Using ACS, you can scale your web service manually or use the autoscaling functionality.</span><span class="sxs-lookup"><span data-stu-id="97b53-199">Using ACS, you can scale your web service manually or use the autoscaling functionality.</span></span>

<span data-ttu-id="97b53-200">**Sign in with Azure CLI**</span><span class="sxs-lookup"><span data-stu-id="97b53-200">**Sign in with Azure CLI**</span></span>

<span data-ttu-id="97b53-201">Using an [Azure](https://azure.microsoft.com/) account with a valid subscription, log in using the following CLI command:</span><span class="sxs-lookup"><span data-stu-id="97b53-201">Using an [Azure](https://azure.microsoft.com/) account with a valid subscription, log in using the following CLI command:</span></span>
<br>`az login`

+ <span data-ttu-id="97b53-202">To switch to another Azure subscription, use the command:</span><span class="sxs-lookup"><span data-stu-id="97b53-202">To switch to another Azure subscription, use the command:</span></span>
<br>`az account set --subscription [your subscription name]`

+ <span data-ttu-id="97b53-203">To see the current model management account, use the command:</span><span class="sxs-lookup"><span data-stu-id="97b53-203">To see the current model management account, use the command:</span></span>
  <br>`az ml account modelmanagement show`

<span data-ttu-id="97b53-204">**Create and set your cluster deployment environment**</span><span class="sxs-lookup"><span data-stu-id="97b53-204">**Create and set your cluster deployment environment**</span></span>

<span data-ttu-id="97b53-205">You only need to set your deployment environment once.</span><span class="sxs-lookup"><span data-stu-id="97b53-205">You only need to set your deployment environment once.</span></span> <span data-ttu-id="97b53-206">If you don't have one yet, set up your deployment environment now using [these instructions](https://docs.microsoft.com/azure/machine-learning/desktop-workbench/deployment-setup-configuration#environment-setup).</span><span class="sxs-lookup"><span data-stu-id="97b53-206">If you don't have one yet, set up your deployment environment now using [these instructions](https://docs.microsoft.com/azure/machine-learning/desktop-workbench/deployment-setup-configuration#environment-setup).</span></span> 

<span data-ttu-id="97b53-207">To see your active deployment environment, use the following CLI command:</span><span class="sxs-lookup"><span data-stu-id="97b53-207">To see your active deployment environment, use the following CLI command:</span></span>
<br>`az ml env show`
   
<span data-ttu-id="97b53-208">Sample Azure CLI command to create and set deployment environment</span><span class="sxs-lookup"><span data-stu-id="97b53-208">Sample Azure CLI command to create and set deployment environment</span></span>

```CLI
az provider register -n Microsoft.MachineLearningCompute
az provider register -n Microsoft.ContainerRegistry
az provider register -n Microsoft.ContainerService
az ml env setup --cluster -n [your environment name] -l [Azure region e.g. westcentralus] [-g [resource group]]
az ml env set -n [environment name] -g [resource group]
az ml env cluster
```
    
### <a name="manage-web-services-and-deployments"></a><span data-ttu-id="97b53-209">Manage web services and deployments</span><span class="sxs-lookup"><span data-stu-id="97b53-209">Manage web services and deployments</span></span>

<span data-ttu-id="97b53-210">The following APIs can be used to deploy models as web services, manage those web services, and manage deployments.</span><span class="sxs-lookup"><span data-stu-id="97b53-210">The following APIs can be used to deploy models as web services, manage those web services, and manage deployments.</span></span>

|<span data-ttu-id="97b53-211">Task</span><span class="sxs-lookup"><span data-stu-id="97b53-211">Task</span></span>|<span data-ttu-id="97b53-212">API</span><span class="sxs-lookup"><span data-stu-id="97b53-212">API</span></span>|
|----|----|
|<span data-ttu-id="97b53-213">Create deployment object</span><span class="sxs-lookup"><span data-stu-id="97b53-213">Create deployment object</span></span>|`deploy_obj = AMLDeployment(deployment_name=deployment_name, associated_DNNModel=dnn_model, aml_env="cluster")`
|<span data-ttu-id="97b53-214">Deploy web service</span><span class="sxs-lookup"><span data-stu-id="97b53-214">Deploy web service</span></span>|`deploy_obj.deploy()`|
|<span data-ttu-id="97b53-215">Score image</span><span class="sxs-lookup"><span data-stu-id="97b53-215">Score image</span></span>|`deploy_obj.score_image(local_image_path_or_image_url)`|
|<span data-ttu-id="97b53-216">Delete web service</span><span class="sxs-lookup"><span data-stu-id="97b53-216">Delete web service</span></span>|`deploy_obj.delete()`|
|<span data-ttu-id="97b53-217">Build docker image without web service</span><span class="sxs-lookup"><span data-stu-id="97b53-217">Build docker image without web service</span></span>|`deploy_obj.build_docker_image()`|
|<span data-ttu-id="97b53-218">List existing deployment</span><span class="sxs-lookup"><span data-stu-id="97b53-218">List existing deployment</span></span>|`AMLDeployment.list_deployment()`|
|<span data-ttu-id="97b53-219">Delete if the service exists with the deployment name</span><span class="sxs-lookup"><span data-stu-id="97b53-219">Delete if the service exists with the deployment name</span></span>|`AMLDeployment.delete_if_service_exist(deployment_name)`|

<span data-ttu-id="97b53-220">**API documentation:** Consult the [package reference documentation](https://aka.ms/aml-packages/vision) for the detailed reference for each module and class.</span><span class="sxs-lookup"><span data-stu-id="97b53-220">**API documentation:** Consult the [package reference documentation](https://aka.ms/aml-packages/vision) for the detailed reference for each module and class.</span></span>

<span data-ttu-id="97b53-221">**CLI reference:** For more advanced operations related to deployment, refer to the [model management CLI reference](https://docs.microsoft.com/azure/machine-learning/desktop-workbench/model-management-cli-reference).</span><span class="sxs-lookup"><span data-stu-id="97b53-221">**CLI reference:** For more advanced operations related to deployment, refer to the [model management CLI reference](https://docs.microsoft.com/azure/machine-learning/desktop-workbench/model-management-cli-reference).</span></span>

<span data-ttu-id="97b53-222">**Deployment management in Azure portal**: You can track and manage your deployments in the [Azure portal](https://ms.portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="97b53-222">**Deployment management in Azure portal**: You can track and manage your deployments in the [Azure portal](https://ms.portal.azure.com/).</span></span> <span data-ttu-id="97b53-223">From the Azure portal, find your Machine Learning Model Management account page using its name.</span><span class="sxs-lookup"><span data-stu-id="97b53-223">From the Azure portal, find your Machine Learning Model Management account page using its name.</span></span> <span data-ttu-id="97b53-224">Then go to the Model Management account page > Model Management > Services.</span><span class="sxs-lookup"><span data-stu-id="97b53-224">Then go to the Model Management account page > Model Management > Services.</span></span>

```python
# ##### OPTIONAL - Interactive CLI setup helper ###### 
# # Interactive CLI setup helper, including model management account and deployment environment.
# # If you haven't setup you CLI before or if you want to change you CLI settings, you can use this block to help you interactively.
# # UNCOMMENT THE FOLLOWING LINES IF YOU HAVE NOT CREATED OR SET THE MODEL MANAGEMENT ACCOUNT AND DEPLOYMENT ENVIRONMENT

# from azuremltkbase.deployment import CliSetup
# CliSetup().run()
```


```python
from cvtk.operationalization import AMLDeployment

# set deployment name
deployment_name = "wsdeployment"

# Create deployment object
# It will use the current deployment environment (you can check it with CLI command "az ml env show").
deploy_obj = AMLDeployment(deployment_name=deployment_name, aml_env="cluster", associated_DNNModel=my_detector, replicas=1)

# Alternatively, you can provide azure machine learning deployment cluster name (environment name) and resource group name
# to deploy your model. It will use the provided cluster to deploy. To do that, please uncomment the following lines to create 
# the deployment object.

# azureml_rscgroup = "<resource group>"
# cluster_name = "<cluster name>"
# deploy_obj = AMLDeployment(deployment_name=deployment_name, associated_DNNModel=my_detector,
#                            aml_env="cluster", cluster_name=cluster_name, resource_group=azureml_rscgroup, replicas=1)

# Check if the deployment name exists, if yes remove it first.
if deploy_obj.is_existing_service():
    AMLDeployment.delete_if_service_exist(deployment_name)
    
# create the webservice
print("Deploying to Azure cluster...")
deploy_obj.deploy()
print("Deployment DONE")
```

### <a name="consume-the-web-service"></a><span data-ttu-id="97b53-225">Consume the web service</span><span class="sxs-lookup"><span data-stu-id="97b53-225">Consume the web service</span></span>

<span data-ttu-id="97b53-226">Once you created the webservice, you can score images with the deployed webservice.</span><span class="sxs-lookup"><span data-stu-id="97b53-226">Once you created the webservice, you can score images with the deployed webservice.</span></span> <span data-ttu-id="97b53-227">You have several options:</span><span class="sxs-lookup"><span data-stu-id="97b53-227">You have several options:</span></span>

   - <span data-ttu-id="97b53-228">You can directly score the webservice with the deployment object with: deploy_obj.score_image(image_path_or_url)</span><span class="sxs-lookup"><span data-stu-id="97b53-228">You can directly score the webservice with the deployment object with: deploy_obj.score_image(image_path_or_url)</span></span> 
   - <span data-ttu-id="97b53-229">Or, you can use the Service endpoint url and Service key (None for local deployment) with: AMLDeployment.score_existing_service_with_image(image_path_or_url, service_endpoint_url, service_key=None)</span><span class="sxs-lookup"><span data-stu-id="97b53-229">Or, you can use the Service endpoint url and Service key (None for local deployment) with: AMLDeployment.score_existing_service_with_image(image_path_or_url, service_endpoint_url, service_key=None)</span></span>
   - <span data-ttu-id="97b53-230">Form your http requests directly to score the webservice endpoint (For advanced users).</span><span class="sxs-lookup"><span data-stu-id="97b53-230">Form your http requests directly to score the webservice endpoint (For advanced users).</span></span>

### <a name="score-with-existing-deployment-object"></a><span data-ttu-id="97b53-231">Score with existing deployment object</span><span class="sxs-lookup"><span data-stu-id="97b53-231">Score with existing deployment object</span></span>
```
deploy_obj.score_image(image_path_or_url)
```


```python
# Score with existing deployment object

# Score local image with file path
print("Score local image with file path")
image_path_or_url = data_train.images[0].storage_path
print("Image source:",image_path_or_url)
serialized_result_in_json = deploy_obj.score_image(image_path_or_url, image_resize_dims=[224,224])
print("serialized_result_in_json:", serialized_result_in_json[:50])

# Score image url and remove image resizing
print("Score image url")
image_path_or_url = "https://cvtkdata.blob.core.windows.net/publicimages/microsoft_logo.jpg"
print("Image source:",image_path_or_url)
serialized_result_in_json = deploy_obj.score_image(image_path_or_url)
print("serialized_result_in_json:", serialized_result_in_json[:50])

```


```python
# Time image scoring
import timeit

num_images = 3
for img_index, img_obj in enumerate(data_train.images[:num_images]):
    print("Calling API for image {} of {}: {}...".format(img_index, num_images, img_obj.name))
    tic = timeit.default_timer()
    return_json = deploy_obj.score_image(img_obj.storage_path, image_resize_dims=[224,224])
    print("   Time for API call: {:.2f} seconds".format(timeit.default_timer() - tic))
```

### <a name="score-with-service-endpoint-url-and-service-key"></a><span data-ttu-id="97b53-232">Score with service endpoint url and service key</span><span class="sxs-lookup"><span data-stu-id="97b53-232">Score with service endpoint url and service key</span></span>
```
    AMLDeployment.score_existing_service_with_image(image_path_or_url, service_endpoint_url, service_key=None)
```


```python
# Import related classes and functions
from cvtk.operationalization import AMLDeployment

service_endpoint_url = "http://xxx" # please replace with your own service url
service_key = "xxx" # please replace with your own service key

# score image url
image_path_or_url = "https://cvtkdata.blob.core.windows.net/publicimages/microsoft_logo.jpg"
print("Image source:",image_path_or_url)
serialized_result_in_json = AMLDeployment.score_existing_service_with_image(image_path_or_url,service_endpoint_url, service_key = service_key, image_resize_dims=[224,224])
print("serialized_result_in_json:", serialized_result_in_json[:50])
```

### <a name="score-endpoint-with-http-request-directly"></a><span data-ttu-id="97b53-233">Score endpoint with http request directly</span><span class="sxs-lookup"><span data-stu-id="97b53-233">Score endpoint with http request directly</span></span>
<span data-ttu-id="97b53-234">Following is some example code to form the http request directly in Python.</span><span class="sxs-lookup"><span data-stu-id="97b53-234">Following is some example code to form the http request directly in Python.</span></span> <span data-ttu-id="97b53-235">You can do it in other programming languages.</span><span class="sxs-lookup"><span data-stu-id="97b53-235">You can do it in other programming languages.</span></span>


```python
def score_image_with_http(image, service_endpoint_url, service_key=None, parameters={}):
    """Score local image with http request

    Args:
        image (str): Image file path
        service_endpoint_url(str): web service endpoint url
        service_key(str): Service key. None for local deployment.
        parameters (dict): Additional request paramters in dictionary. Default is {}.


    Returns:
        str: serialized result 
    """
    import requests
    from io import BytesIO
    import base64
    import json

    if service_key is None:
        headers = {'Content-Type': 'application/json'}
    else:
        headers = {'Content-Type': 'application/json',
                   "Authorization": ('Bearer ' + service_key)}
    payload = []
    encoded = None
    
    # Read image
    with open(image,'rb') as f:
        image_buffer = BytesIO(f.read()) ## Getting an image file represented as a BytesIO object
        
    # Convert your image to base64 string
    # image_in_base64 : "b'{base64}'"
    encoded = base64.b64encode(image_buffer.getvalue())
    image_request = {"image_in_base64": "{0}".format(encoded), "parameters": parameters}
    payload.append(image_request)
    body = json.dumps(payload)
    r = requests.post(service_endpoint_url, data=body, headers=headers)
    try:
        result = json.loads(r.text)
        json.loads(result[0])
    except:
        raise ValueError("Incorrect output format. Result cant not be parsed: " + r.text)
    return result[0]

```

### <a name="parse-serialized-result-from-webservice"></a><span data-ttu-id="97b53-236">Parse serialized result from webservice</span><span class="sxs-lookup"><span data-stu-id="97b53-236">Parse serialized result from webservice</span></span>
<span data-ttu-id="97b53-237">The result from the web service is in json string that can be parsed.</span><span class="sxs-lookup"><span data-stu-id="97b53-237">The result from the web service is in json string that can be parsed.</span></span>


```python
image_path_or_url = image_path
print("Image source:",image_path_or_url)
serialized_result_in_json = deploy_obj.score_image(image_path_or_url)
print("serialized_result_in_json:", serialized_result_in_json[:50])
```


```python
# Parse result from json string
import numpy as np
parsed_result = TFFasterRCNN.parse_serialized_result(serialized_result_in_json)
print("Parsed result:", parsed_result)
```


```python
ax = detection_utils.visualize(image_path, parsed_result)
path_save = "./scored_images/scored_image_web.jpg"
path_save_dir = os.path.dirname(os.path.abspath(path_save))
os.makedirs(path_save_dir, exist_ok=True)
ax.get_figure().savefig(path_save)
```

## <a name="next-steps"></a><span data-ttu-id="97b53-238">Next steps</span><span class="sxs-lookup"><span data-stu-id="97b53-238">Next steps</span></span>

<span data-ttu-id="97b53-239">Learn more about Azure Machine Learning Package for Computer Vision in these articles:</span><span class="sxs-lookup"><span data-stu-id="97b53-239">Learn more about Azure Machine Learning Package for Computer Vision in these articles:</span></span>

+ <span data-ttu-id="97b53-240">Read the [package overview and learn how to install it](https://aka.ms/aml-packages/vision).</span><span class="sxs-lookup"><span data-stu-id="97b53-240">Read the [package overview and learn how to install it](https://aka.ms/aml-packages/vision).</span></span>

+ <span data-ttu-id="97b53-241">Explore the [reference documentation](https://docs.microsoft.com/python/api/overview/azure-machine-learning/computer-vision) for this package.</span><span class="sxs-lookup"><span data-stu-id="97b53-241">Explore the [reference documentation](https://docs.microsoft.com/python/api/overview/azure-machine-learning/computer-vision) for this package.</span></span>

+ <span data-ttu-id="97b53-242">Learn about [other Python packages for Azure Machine Learning](reference-python-package-overview.md).</span><span class="sxs-lookup"><span data-stu-id="97b53-242">Learn about [other Python packages for Azure Machine Learning](reference-python-package-overview.md).</span></span>
