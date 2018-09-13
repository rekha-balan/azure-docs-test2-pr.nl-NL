---
title: Build and deploy an image classification model using Azure Machine Learning Package for Computer Vision.
description: Learn how to build, train, test and deploy a computer vision image classification model using the Azure Machine Learning Package for Computer Vision.
services: machine-learning
ms.service: machine-learning
ms.component: core
ms.topic: conceptual
ms.reviewer: jmartens
ms.author: netahw
author: nhaiby
ms.date: 04/23/2018
ms.openlocfilehash: f5d83e2924461d463741fc545339d9d7d3216c98
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966048"
---
# <a name="build-and-deploy-image-classification-models-with-azure-machine-learning"></a><span data-ttu-id="bdd9a-103">Build and deploy image classification models with Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="bdd9a-103">Build and deploy image classification models with Azure Machine Learning</span></span>

<span data-ttu-id="bdd9a-104">In this article, learn how to use **Azure Machine Learning Package for Computer Vision** (AMLPCV) to train, test, and deploy an image classification model.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-104">In this article, learn how to use **Azure Machine Learning Package for Computer Vision** (AMLPCV) to train, test, and deploy an image classification model.</span></span> 

<span data-ttu-id="bdd9a-105">A large number of problems in the computer vision domain can be solved using image classification.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-105">A large number of problems in the computer vision domain can be solved using image classification.</span></span> <span data-ttu-id="bdd9a-106">These problems include building models that answer questions such as:</span><span class="sxs-lookup"><span data-stu-id="bdd9a-106">These problems include building models that answer questions such as:</span></span>
+ <span data-ttu-id="bdd9a-107">_Is an OBJECT present in the image? For example, "dog", "car", "ship", and so on_</span><span class="sxs-lookup"><span data-stu-id="bdd9a-107">_Is an OBJECT present in the image? For example, "dog", "car", "ship", and so on_</span></span>
+ <span data-ttu-id="bdd9a-108">_What class of eye disease severity is evinced by this patient's retinal scan?_</span><span class="sxs-lookup"><span data-stu-id="bdd9a-108">_What class of eye disease severity is evinced by this patient's retinal scan?_</span></span>

<span data-ttu-id="bdd9a-109">When building and deploying this model with AMLPCV, you go through the following steps:</span><span class="sxs-lookup"><span data-stu-id="bdd9a-109">When building and deploying this model with AMLPCV, you go through the following steps:</span></span>
1. <span data-ttu-id="bdd9a-110">Dataset Creation</span><span class="sxs-lookup"><span data-stu-id="bdd9a-110">Dataset Creation</span></span>
2. <span data-ttu-id="bdd9a-111">Image Visualization and annotation</span><span class="sxs-lookup"><span data-stu-id="bdd9a-111">Image Visualization and annotation</span></span>
3. <span data-ttu-id="bdd9a-112">Image Augmentation</span><span class="sxs-lookup"><span data-stu-id="bdd9a-112">Image Augmentation</span></span>
4. <span data-ttu-id="bdd9a-113">Deep Neural Network (DNN) Model Definition</span><span class="sxs-lookup"><span data-stu-id="bdd9a-113">Deep Neural Network (DNN) Model Definition</span></span>
5. <span data-ttu-id="bdd9a-114">Classifier Training</span><span class="sxs-lookup"><span data-stu-id="bdd9a-114">Classifier Training</span></span>
6. <span data-ttu-id="bdd9a-115">Evaluation and Visualization</span><span class="sxs-lookup"><span data-stu-id="bdd9a-115">Evaluation and Visualization</span></span>
7. <span data-ttu-id="bdd9a-116">Web service Deployment</span><span class="sxs-lookup"><span data-stu-id="bdd9a-116">Web service Deployment</span></span>
8. <span data-ttu-id="bdd9a-117">Web service Load Testing</span><span class="sxs-lookup"><span data-stu-id="bdd9a-117">Web service Load Testing</span></span>

<span data-ttu-id="bdd9a-118">[CNTK](https://www.microsoft.com/en-us/cognitive-toolkit/) is used as the deep learning framework, training is performed locally on a GPU powered machine such as the ([Deep learning Data Science VM](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft-ads.dsvm-deep-learning?tab=Overview)), and deployment uses the Azure ML Operationalization CLI.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-118">[CNTK](https://www.microsoft.com/en-us/cognitive-toolkit/) is used as the deep learning framework, training is performed locally on a GPU powered machine such as the ([Deep learning Data Science VM](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft-ads.dsvm-deep-learning?tab=Overview)), and deployment uses the Azure ML Operationalization CLI.</span></span>

<span data-ttu-id="bdd9a-119">Consult the [package reference documentation](https://aka.ms/aml-packages/vision) for the detailed reference for each module and class.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-119">Consult the [package reference documentation](https://aka.ms/aml-packages/vision) for the detailed reference for each module and class.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bdd9a-120">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bdd9a-120">Prerequisites</span></span>

1. <span data-ttu-id="bdd9a-121">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-121">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

1. <span data-ttu-id="bdd9a-122">The following accounts and application must be set up and installed:</span><span class="sxs-lookup"><span data-stu-id="bdd9a-122">The following accounts and application must be set up and installed:</span></span>
   - <span data-ttu-id="bdd9a-123">An Azure Machine Learning Experimentation account</span><span class="sxs-lookup"><span data-stu-id="bdd9a-123">An Azure Machine Learning Experimentation account</span></span> 
   - <span data-ttu-id="bdd9a-124">An Azure Machine Learning Model Management account</span><span class="sxs-lookup"><span data-stu-id="bdd9a-124">An Azure Machine Learning Model Management account</span></span>
   - <span data-ttu-id="bdd9a-125">Azure Machine Learning Workbench installed</span><span class="sxs-lookup"><span data-stu-id="bdd9a-125">Azure Machine Learning Workbench installed</span></span>

   <span data-ttu-id="bdd9a-126">If these three are not yet created or installed, follow the [Azure Machine Learning Quickstart and Workbench installation](../service/quickstart-installation.md) article.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-126">If these three are not yet created or installed, follow the [Azure Machine Learning Quickstart and Workbench installation](../service/quickstart-installation.md) article.</span></span> 

1. <span data-ttu-id="bdd9a-127">The Azure Machine Learning Package for Computer Vision must be installed.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-127">The Azure Machine Learning Package for Computer Vision must be installed.</span></span> <span data-ttu-id="bdd9a-128">Learn how to [install this package here](https://aka.ms/aml-packages/vision).</span><span class="sxs-lookup"><span data-stu-id="bdd9a-128">Learn how to [install this package here](https://aka.ms/aml-packages/vision).</span></span>

## <a name="sample-data-and-notebook"></a><span data-ttu-id="bdd9a-129">Sample data and notebook</span><span class="sxs-lookup"><span data-stu-id="bdd9a-129">Sample data and notebook</span></span>

### <a name="get-the-jupyter-notebook"></a><span data-ttu-id="bdd9a-130">Get the Jupyter notebook</span><span class="sxs-lookup"><span data-stu-id="bdd9a-130">Get the Jupyter notebook</span></span>

<span data-ttu-id="bdd9a-131">Download the notebook to run the sample described here yourself.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-131">Download the notebook to run the sample described here yourself.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bdd9a-132">Get the Jupyter notebook</span><span class="sxs-lookup"><span data-stu-id="bdd9a-132">Get the Jupyter notebook</span></span>](https://aka.ms/aml-packages/vision/notebooks/image_classification)

### <a name="load-the-sample-data"></a><span data-ttu-id="bdd9a-133">Load the sample data</span><span class="sxs-lookup"><span data-stu-id="bdd9a-133">Load the sample data</span></span>

<span data-ttu-id="bdd9a-134">The following example uses a dataset consisting of 63 tableware images.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-134">The following example uses a dataset consisting of 63 tableware images.</span></span> <span data-ttu-id="bdd9a-135">Each image is labeled as belonging to one of four different classes (bowl, cup, cutlery, plate).</span><span class="sxs-lookup"><span data-stu-id="bdd9a-135">Each image is labeled as belonging to one of four different classes (bowl, cup, cutlery, plate).</span></span> <span data-ttu-id="bdd9a-136">The number of images in this example is small so that this sample can be executed quickly.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-136">The number of images in this example is small so that this sample can be executed quickly.</span></span> <span data-ttu-id="bdd9a-137">In practice at least 100 images per class should be provided.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-137">In practice at least 100 images per class should be provided.</span></span> <span data-ttu-id="bdd9a-138">All images are located at *"../sample_data/imgs_recycling/"*, in subdirectories called "bowl", "cup", "cutlery", and "plate".</span><span class="sxs-lookup"><span data-stu-id="bdd9a-138">All images are located at *"../sample_data/imgs_recycling/"*, in subdirectories called "bowl", "cup", "cutlery", and "plate".</span></span>

![Azure Machine Learning dataset](media/how-to-build-deploy-image-classification-models/recycling_examples.jpg)


```python
import warnings
warnings.filterwarnings("ignore")
import json, numpy as np, os, timeit 
from azureml.logging import get_azureml_logger
from imgaug import augmenters
from IPython.display import display
from sklearn import svm
from cvtk import ClassificationDataset, CNTKTLModel, Context, Splitter, StorageContext
from cvtk.augmentation import augment_dataset
from cvtk.core.classifier import ScikitClassifier
from cvtk.evaluation import ClassificationEvaluation, graph_roc_curve, graph_pr_curve, graph_confusion_matrix
import matplotlib.pyplot as plt

from classification.notebook.ui_utils.ui_annotation import AnnotationUI
from classification.notebook.ui_utils.ui_results_viewer import ResultsUI
from classification.notebook.ui_utils.ui_precision_recall import PrecisionRecallUI

%matplotlib inline

# Disable printing of logging messages
from azuremltkbase.logging import ToolkitLogger
ToolkitLogger.getInstance().setEnabled(False)
```



## <a name="create-a-dataset"></a><span data-ttu-id="bdd9a-140">Create a dataset</span><span class="sxs-lookup"><span data-stu-id="bdd9a-140">Create a dataset</span></span>

<span data-ttu-id="bdd9a-141">Once you have imported the dependencies and set the storage context, you can create the dataset object.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-141">Once you have imported the dependencies and set the storage context, you can create the dataset object.</span></span>

<span data-ttu-id="bdd9a-142">To create that object with Azure Machine Learning Package for Computer Vision, provide the root directory of the images on the local disk.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-142">To create that object with Azure Machine Learning Package for Computer Vision, provide the root directory of the images on the local disk.</span></span> <span data-ttu-id="bdd9a-143">This directory must follow the same general structure as the tableware dataset, that is, contain subdirectories with the actual images:</span><span class="sxs-lookup"><span data-stu-id="bdd9a-143">This directory must follow the same general structure as the tableware dataset, that is, contain subdirectories with the actual images:</span></span>
- <span data-ttu-id="bdd9a-144">root</span><span class="sxs-lookup"><span data-stu-id="bdd9a-144">root</span></span>
    - <span data-ttu-id="bdd9a-145">label 1</span><span class="sxs-lookup"><span data-stu-id="bdd9a-145">label 1</span></span>
    - <span data-ttu-id="bdd9a-146">label 2</span><span class="sxs-lookup"><span data-stu-id="bdd9a-146">label 2</span></span>
    - <span data-ttu-id="bdd9a-147">...</span><span class="sxs-lookup"><span data-stu-id="bdd9a-147">...</span></span>
    - <span data-ttu-id="bdd9a-148">label n</span><span class="sxs-lookup"><span data-stu-id="bdd9a-148">label n</span></span>
  
<span data-ttu-id="bdd9a-149">Training an image classification model for a different dataset is as easy as changing the root path `dataset_location` in the following code to point at different images.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-149">Training an image classification model for a different dataset is as easy as changing the root path `dataset_location` in the following code to point at different images.</span></span>


```python
# Root image directory
dataset_location = os.path.abspath("classification/sample_data/imgs_recycling")

dataset_name = 'recycling'
dataset = ClassificationDataset.create_from_dir(dataset_name, dataset_location)
print("Dataset consists of {} images with {} labels.".format(len(dataset.images), len(dataset.labels)))
print("Select information for image 2: name={}, label={}, unique id={}.".format(
    dataset.images[2].name, dataset.images[2]._labels[0].name, dataset.images[2]._storage_id))
```

    F1 2018-04-23 17:12:57,593 INFO azureml.vision:machine info {"is_dsvm": true, "os_type": "Windows"} 
    F1 2018-04-23 17:12:57,599 INFO azureml.vision:dataset creating dataset for scenario=classification 
    Dataset consists of 63 images with 4 labels.
    Select information for image 2: name=msft-plastic-bowl20170725152154282.jpg, label=bowl, unique id=3.

<span data-ttu-id="bdd9a-150">The dataset object provides functionality to download images using the [Bing Image Search API](https://azure.microsoft.com/services/cognitive-services/bing-image-search-api/).</span><span class="sxs-lookup"><span data-stu-id="bdd9a-150">The dataset object provides functionality to download images using the [Bing Image Search API](https://azure.microsoft.com/services/cognitive-services/bing-image-search-api/).</span></span> 

<span data-ttu-id="bdd9a-151">Two types of search queries are supported:</span><span class="sxs-lookup"><span data-stu-id="bdd9a-151">Two types of search queries are supported:</span></span> 
+ <span data-ttu-id="bdd9a-152">Regular text queries</span><span class="sxs-lookup"><span data-stu-id="bdd9a-152">Regular text queries</span></span>
+ <span data-ttu-id="bdd9a-153">Image URL queries</span><span class="sxs-lookup"><span data-stu-id="bdd9a-153">Image URL queries</span></span>

<span data-ttu-id="bdd9a-154">These queries along with the class label must be provided inside a JSON-encoded text file.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-154">These queries along with the class label must be provided inside a JSON-encoded text file.</span></span> <span data-ttu-id="bdd9a-155">For example:</span><span class="sxs-lookup"><span data-stu-id="bdd9a-155">For example:</span></span>

```json
{
    "bowl": [
                    "plastic bowl",
                    "../imgs_recycling/bowl"
    ],
    "cup": [
                    "plastic cup",
                    "../imgs_recycling/cup",
                    "http://cdnimg2.webstaurantstore.com/images/products/main/123662/268841/dart-solo-ultra-clear-conex-tp12-12-oz-pet-plastic-cold-cup-1000-case.jpg"
    ],
    "cutlery": [
                    "plastic cutlery",
                    "../imgs_recycling/cutlery",
                    "http://img4.foodservicewarehouse.com/Prd/1900SQ/Fineline_2514-BO.jpg"
    ],
    "plate": [
                    "plastic plate",
                    "../imgs_recycling/plate"
    ]
}
```

<span data-ttu-id="bdd9a-156">Furthermore, you must explicitly create a Context object to contain the Bing Image Search API key.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-156">Furthermore, you must explicitly create a Context object to contain the Bing Image Search API key.</span></span> <span data-ttu-id="bdd9a-157">This requires a Bing Image Search API subscription.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-157">This requires a Bing Image Search API subscription.</span></span>

## <a name="visualize-and-annotate-images"></a><span data-ttu-id="bdd9a-158">Visualize and annotate images</span><span class="sxs-lookup"><span data-stu-id="bdd9a-158">Visualize and annotate images</span></span>

<span data-ttu-id="bdd9a-159">You can visualize the images and correct labels in the dataset object using the following widget.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-159">You can visualize the images and correct labels in the dataset object using the following widget.</span></span> 

<span data-ttu-id="bdd9a-160">If you encounter the "Widget Javascript not detected" error, run this command to solve it:</span><span class="sxs-lookup"><span data-stu-id="bdd9a-160">If you encounter the "Widget Javascript not detected" error, run this command to solve it:</span></span>
<br>`jupyter nbextension enable --py --sys-prefix widgetsnbextension`


```python
annotation_ui = AnnotationUI(dataset, Context.get_global_context())
display(annotation_ui.ui)
```

![Azure Machine Learning dataset](media/how-to-build-deploy-image-classification-models/image_annotation.png)

## <a name="augment-images"></a><span data-ttu-id="bdd9a-162">Augment images</span><span class="sxs-lookup"><span data-stu-id="bdd9a-162">Augment images</span></span>

<span data-ttu-id="bdd9a-163">The [`augmentation` module](https://docs.microsoft.com/en-us/python/api/cvtk.augmentation) provides functionality to augment a dataset object using all the transformations described in the [imgaug](https://github.com/aleju/imgaug) library.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-163">The [`augmentation` module](https://docs.microsoft.com/en-us/python/api/cvtk.augmentation) provides functionality to augment a dataset object using all the transformations described in the [imgaug](https://github.com/aleju/imgaug) library.</span></span> <span data-ttu-id="bdd9a-164">Image transformations can be grouped in a single pipeline, in which case all transformations in the pipeline are applied simultaneously each image.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-164">Image transformations can be grouped in a single pipeline, in which case all transformations in the pipeline are applied simultaneously each image.</span></span> 

<span data-ttu-id="bdd9a-165">If you would like to apply different augmentation steps separately, or in any different manner, you can define multiple pipelines and pass them to the *augment_dataset* function.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-165">If you would like to apply different augmentation steps separately, or in any different manner, you can define multiple pipelines and pass them to the *augment_dataset* function.</span></span> <span data-ttu-id="bdd9a-166">For more information and examples of image augmentation, see the [imgaug documentation](https://github.com/aleju/imgaug).</span><span class="sxs-lookup"><span data-stu-id="bdd9a-166">For more information and examples of image augmentation, see the [imgaug documentation](https://github.com/aleju/imgaug).</span></span>

<span data-ttu-id="bdd9a-167">Adding augmented images to the training set is especially beneficial for small datasets.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-167">Adding augmented images to the training set is especially beneficial for small datasets.</span></span> <span data-ttu-id="bdd9a-168">Since the DNN training process is slower due to the increased number of training images, we recommend you start experimentation without augmentation.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-168">Since the DNN training process is slower due to the increased number of training images, we recommend you start experimentation without augmentation.</span></span>


```python
# Split the dataset into train and test  
train_set_orig, test_set = dataset.split(train_size = 0.66, stratify = "label")
print("Number of training images = {}, test images = {}.".format(train_set_orig.size(), test_set.size()))
```

    F1 2018-04-23 17:13:01,780 INFO azureml.vision:splitter splitting a dataset 
    F1 2018-04-23 17:13:01,805 INFO azureml.vision:dataset creating dataset for scenario=classification 
    F1 2018-04-23 17:13:01,809 INFO azureml.vision:dataset creating dataset for scenario=classification 
    Number of training images = 41, test images = 22.
    


```python
augment_train_set = False

if augment_train_set:
    aug_sequence = augmenters.Sequential([
            augmenters.Fliplr(0.5),             # horizontally flip 50% of all images
            augmenters.Crop(percent=(0, 0.1)),  # crop images by 0-10% of their height/width
        ])
    train_set = augment_dataset(train_set_orig, [aug_sequence])
    print("Number of original training images = {}, with augmented images included = {}.".format(train_set_orig.size(), train_set.size()))
else:
    train_set = train_set_orig  
```

## <a name="define-dnn-models"></a><span data-ttu-id="bdd9a-169">Define DNN models</span><span class="sxs-lookup"><span data-stu-id="bdd9a-169">Define DNN models</span></span>

<span data-ttu-id="bdd9a-170">The following pretrained Deep Neural Network models are supported with this package:</span><span class="sxs-lookup"><span data-stu-id="bdd9a-170">The following pretrained Deep Neural Network models are supported with this package:</span></span> 
+ <span data-ttu-id="bdd9a-171">Resnet-18</span><span class="sxs-lookup"><span data-stu-id="bdd9a-171">Resnet-18</span></span>
+ <span data-ttu-id="bdd9a-172">Resnet-34</span><span class="sxs-lookup"><span data-stu-id="bdd9a-172">Resnet-34</span></span>
+ <span data-ttu-id="bdd9a-173">Resnet-50</span><span class="sxs-lookup"><span data-stu-id="bdd9a-173">Resnet-50</span></span>
+ <span data-ttu-id="bdd9a-174">Resnet-101</span><span class="sxs-lookup"><span data-stu-id="bdd9a-174">Resnet-101</span></span>
+ <span data-ttu-id="bdd9a-175">Resnet-152</span><span class="sxs-lookup"><span data-stu-id="bdd9a-175">Resnet-152</span></span>

<span data-ttu-id="bdd9a-176">These DNNs can be used either as classifier, or as featurizer.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-176">These DNNs can be used either as classifier, or as featurizer.</span></span> 

<span data-ttu-id="bdd9a-177">More information about the networks can be found [here](https://github.com/Microsoft/CNTK/blob/master/PretrainedModels/Image.md), and a basic introduction to Transfer Learning is [here](https://blog.slavv.com/a-gentle-intro-to-transfer-learning-2c0b674375a0).</span><span class="sxs-lookup"><span data-stu-id="bdd9a-177">More information about the networks can be found [here](https://github.com/Microsoft/CNTK/blob/master/PretrainedModels/Image.md), and a basic introduction to Transfer Learning is [here](https://blog.slavv.com/a-gentle-intro-to-transfer-learning-2c0b674375a0).</span></span>

<span data-ttu-id="bdd9a-178">The default image classification parameters for this package are 224x224 pixel resolution and a Resnet-18 DNN.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-178">The default image classification parameters for this package are 224x224 pixel resolution and a Resnet-18 DNN.</span></span> <span data-ttu-id="bdd9a-179">These parameters were selected to work well on a wide variety of tasks.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-179">These parameters were selected to work well on a wide variety of tasks.</span></span> <span data-ttu-id="bdd9a-180">Accuracy can often be improved, for example, by increasing the image resolution to 500x500 pixels, and/or selecting a deeper model (Resnet-50).</span><span class="sxs-lookup"><span data-stu-id="bdd9a-180">Accuracy can often be improved, for example, by increasing the image resolution to 500x500 pixels, and/or selecting a deeper model (Resnet-50).</span></span> <span data-ttu-id="bdd9a-181">However, changing the parameters can come at a significant increase in training time.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-181">However, changing the parameters can come at a significant increase in training time.</span></span> <span data-ttu-id="bdd9a-182">See the article on [How to improve accuracy](https://docs.microsoft.com/azure/machine-learning/service/how-to-improve-accuracy-for-computer-vision-models).</span><span class="sxs-lookup"><span data-stu-id="bdd9a-182">See the article on [How to improve accuracy](https://docs.microsoft.com/azure/machine-learning/service/how-to-improve-accuracy-for-computer-vision-models).</span></span>


```python
# Default parameters (224 x 224 pixels resolution, Resnet-18)
lr_per_mb = [0.05]*7 + [0.005]*7 +  [0.0005]
mb_size = 32
input_resoluton = 224
base_model_name = "ResNet18_ImageNet_CNTK"

# Suggested parameters for 500 x 500 pixels resolution, Resnet-50
# (see in the Appendix "How to improve accuracy", last row in table)
# lr_per_mb   = [0.01] * 7 + [0.001] * 7 + [0.0001]
# mb_size    = 8
# input_resoluton = 500
# base_model_name = "ResNet50_ImageNet_CNTK"

# Initialize model
dnn_model = CNTKTLModel(train_set.labels,
                       base_model_name=base_model_name,
                       image_dims = (3, input_resoluton, input_resoluton))
```

    Successfully downloaded ResNet18_ImageNet_CNTK
    

## <a name="train-the-classifier"></a><span data-ttu-id="bdd9a-183">Train the classifier</span><span class="sxs-lookup"><span data-stu-id="bdd9a-183">Train the classifier</span></span>

<span data-ttu-id="bdd9a-184">You can choose one of the following methods for the pre-trained DNN.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-184">You can choose one of the following methods for the pre-trained DNN.</span></span>

  - <span data-ttu-id="bdd9a-185">**DNN refinement**, which trains the DNN to perform the classification directly.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-185">**DNN refinement**, which trains the DNN to perform the classification directly.</span></span> <span data-ttu-id="bdd9a-186">While DNN training is slow, it typically leads to the best results since all network weights can be improved during training to give best accuracy.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-186">While DNN training is slow, it typically leads to the best results since all network weights can be improved during training to give best accuracy.</span></span>

  - <span data-ttu-id="bdd9a-187">**DNN featurization**, which runs the DNN as-is to obtain a lower-dimensional representation of an image (512, 2048, or 4096 floats).</span><span class="sxs-lookup"><span data-stu-id="bdd9a-187">**DNN featurization**, which runs the DNN as-is to obtain a lower-dimensional representation of an image (512, 2048, or 4096 floats).</span></span> <span data-ttu-id="bdd9a-188">That representation is then used as input to train a separate classifier.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-188">That representation is then used as input to train a separate classifier.</span></span> <span data-ttu-id="bdd9a-189">Since the DNN is kept unchanged, this approach is much faster compared to DNN refinement, however accuracy is not as good.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-189">Since the DNN is kept unchanged, this approach is much faster compared to DNN refinement, however accuracy is not as good.</span></span> <span data-ttu-id="bdd9a-190">Nevertheless, training an external classifier such as a linear SVM (as shown in the following code) can provide a strong baseline, and help with understanding the feasibility of a problem.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-190">Nevertheless, training an external classifier such as a linear SVM (as shown in the following code) can provide a strong baseline, and help with understanding the feasibility of a problem.</span></span>
  
<span data-ttu-id="bdd9a-191">TensorBoard can be used to visualize the training progress.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-191">TensorBoard can be used to visualize the training progress.</span></span> <span data-ttu-id="bdd9a-192">To activate TensorBoard:</span><span class="sxs-lookup"><span data-stu-id="bdd9a-192">To activate TensorBoard:</span></span>
1. <span data-ttu-id="bdd9a-193">Add the parameter `tensorboard_logdir=PATH` as shown in the following code</span><span class="sxs-lookup"><span data-stu-id="bdd9a-193">Add the parameter `tensorboard_logdir=PATH` as shown in the following code</span></span>
1. <span data-ttu-id="bdd9a-194">Start the TensorBoard client using the command `tensorboard --logdir=PATH` in a new console.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-194">Start the TensorBoard client using the command `tensorboard --logdir=PATH` in a new console.</span></span>
1. <span data-ttu-id="bdd9a-195">Open a web browser as instructed by TensorBoard, which by default is localhost:6006.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-195">Open a web browser as instructed by TensorBoard, which by default is localhost:6006.</span></span> 


```python
# Train either the DNN or a SVM as classifier 
classifier_name = "dnn"

if classifier_name.lower() == "dnn":  
    dnn_model.train(train_set, lr_per_mb = lr_per_mb, mb_size = mb_size, eval_dataset=test_set) #, tensorboard_logdir=r"tensorboard"
    classifier = dnn_model
elif classifier_name.lower() == "svm":
    learner = svm.LinearSVC(C=1.0, class_weight='balanced', verbose=0)
    classifier = ScikitClassifier(dnn_model, learner = learner)
    classifier.train(train_set)
else:
    raise Exception("Classifier unknown: " + classifier)   
```

    F1 2018-04-23 17:13:28,238 INFO azureml.vision:Fit starting in experiment  1541466320 
    F1 2018-04-23 17:13:28,239 INFO azureml.vision:model starting training for scenario=classification 
    <class 'int'>
    1 worker
    Training transfer learning model for 15 epochs (epoch_size = 41).
    non-distributed mode
    Training 15741700 parameters in 53 parameter tensors.
    Training 15741700 parameters in 53 parameter tensors.
    Learning rate per minibatch: 0.05
    Momentum per minibatch: 0.9
    PROGRESS: 0.00%
    Finished Epoch[1 of 15]: [Training] loss = 2.820586 * 41, metric = 68.29% * 41 5.738s (  7.1 samples/s);
    Evaluation Set Error :: 29.27%
    Finished Epoch[2 of 15]: [Training] loss = 0.286728 * 41, metric = 9.76% * 41 0.752s ( 54.5 samples/s);
    Evaluation Set Error :: 34.15%
    Finished Epoch[3 of 15]: [Training] loss = 0.206938 * 41, metric = 4.88% * 41 0.688s ( 59.6 samples/s);
    Evaluation Set Error :: 41.46%
    Finished Epoch[4 of 15]: [Training] loss = 0.098931 * 41, metric = 2.44% * 41 0.785s ( 52.2 samples/s);
    Evaluation Set Error :: 48.78%
    Finished Epoch[5 of 15]: [Training] loss = 0.046547 * 41, metric = 0.00% * 41 0.724s ( 56.6 samples/s);
    Evaluation Set Error :: 43.90%
    Finished Epoch[6 of 15]: [Training] loss = 0.059709 * 41, metric = 4.88% * 41 0.636s ( 64.5 samples/s);
    Evaluation Set Error :: 34.15%
    Finished Epoch[7 of 15]: [Training] loss = 0.005817 * 41, metric = 0.00% * 41 0.710s ( 57.7 samples/s);
    Evaluation Set Error :: 14.63%
    Learning rate per minibatch: 0.005
    Finished Epoch[8 of 15]: [Training] loss = 0.014917 * 41, metric = 0.00% * 41 0.649s ( 63.2 samples/s);
    Evaluation Set Error :: 9.76%
    Finished Epoch[9 of 15]: [Training] loss = 0.040539 * 41, metric = 2.44% * 41 0.777s ( 52.8 samples/s);
    Evaluation Set Error :: 9.76%
    Finished Epoch[10 of 15]: [Training] loss = 0.024606 * 41, metric = 0.00% * 41 0.626s ( 65.5 samples/s);
    Evaluation Set Error :: 7.32%
    PROGRESS: 0.00%
    Finished Epoch[11 of 15]: [Training] loss = 0.004225 * 41, metric = 0.00% * 41 0.656s ( 62.5 samples/s);
    Evaluation Set Error :: 4.88%
    Finished Epoch[12 of 15]: [Training] loss = 0.004364 * 41, metric = 0.00% * 41 0.702s ( 58.4 samples/s);
    Evaluation Set Error :: 4.88%
    Finished Epoch[13 of 15]: [Training] loss = 0.007974 * 41, metric = 0.00% * 41 0.721s ( 56.9 samples/s);
    Evaluation Set Error :: 4.88%
    Finished Epoch[14 of 15]: [Training] loss = 0.000655 * 41, metric = 0.00% * 41 0.711s ( 57.7 samples/s);
    Evaluation Set Error :: 4.88%
    Learning rate per minibatch: 0.0005
    Finished Epoch[15 of 15]: [Training] loss = 0.024865 * 41, metric = 0.00% * 41 0.688s ( 59.6 samples/s);
    Evaluation Set Error :: 4.88%
    Stored trained model at ../../../cvtk_output\model_trained\ImageClassification.model
    F1 2018-04-23 17:13:45,097 INFO azureml.vision:Fit finished in experiment  1541466320 
    


```python
# Plot how the training and test accuracy increases during gradient descent. 
if classifier_name == "dnn":
    [train_accs, test_accs, epoch_numbers] = classifier.train_eval_accs
    plt.xlabel("Number of training epochs") 
    plt.ylabel("Classification accuracy") 
    train_plot = plt.plot(epoch_numbers, train_accs, 'r-', label = "Training accuracy")
    test_plot = plt.plot(epoch_numbers, test_accs, 'b-.', label = "Test accuracy")
    plt.legend()
```

![png](media/how-to-build-deploy-image-classification-models/output_17_0.png)


## <a name="evaluate-and-visualize-model-performance"></a><span data-ttu-id="bdd9a-197">Evaluate and visualize model performance</span><span class="sxs-lookup"><span data-stu-id="bdd9a-197">Evaluate and visualize model performance</span></span>

<span data-ttu-id="bdd9a-198">You can evaluate the performance of the trained model on an independent test dataset using the evaluation module.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-198">You can evaluate the performance of the trained model on an independent test dataset using the evaluation module.</span></span> <span data-ttu-id="bdd9a-199">Some of the evaluation metrics it computes include:</span><span class="sxs-lookup"><span data-stu-id="bdd9a-199">Some of the evaluation metrics it computes include:</span></span>
 
+ <span data-ttu-id="bdd9a-200">Accuracy (by default class-averaged)</span><span class="sxs-lookup"><span data-stu-id="bdd9a-200">Accuracy (by default class-averaged)</span></span>
+ <span data-ttu-id="bdd9a-201">PR curve</span><span class="sxs-lookup"><span data-stu-id="bdd9a-201">PR curve</span></span>
+ <span data-ttu-id="bdd9a-202">ROC curve</span><span class="sxs-lookup"><span data-stu-id="bdd9a-202">ROC curve</span></span>
+ <span data-ttu-id="bdd9a-203">Area-under-curve</span><span class="sxs-lookup"><span data-stu-id="bdd9a-203">Area-under-curve</span></span>
+ <span data-ttu-id="bdd9a-204">Confusion matrix</span><span class="sxs-lookup"><span data-stu-id="bdd9a-204">Confusion matrix</span></span>


```python
# Run the classifier on all test set images
ce = ClassificationEvaluation(classifier, test_set, minibatch_size = mb_size)

# Compute Accuracy and the confusion matrix
acc = ce.compute_accuracy()
print("Accuracy = {:2.2f}%".format(100*acc))
cm  = ce.compute_confusion_matrix()
print("Confusion matrix = \n{}".format(cm))

# Show PR curve, ROC curve, and confusion matrix
fig, ((ax1, ax2, ax3)) = plt.subplots(1,3)
fig.set_size_inches(18, 4)
graph_roc_curve(ce, ax=ax1)
graph_pr_curve(ce, ax=ax2)
graph_confusion_matrix(ce, ax=ax3)
plt.show()
```

    F1 2018-04-23 17:14:37,449 INFO azureml.vision:evaluation doing evaluation for scenario=classification 
    F1 2018-04-23 17:14:37,450 INFO azureml.vision:model scoring dataset for scenario=classification 
    Accuracy = 95.45%
    Confusion matrix = 
    [[ 0  1  0  1]
     [ 0  7  0  0]
     [ 0  0  2  0]
     [ 0  0  0 11]]
    


![png](media/how-to-build-deploy-image-classification-models/output_20_1.png)



```python
# Results viewer UI
labels = [l.name for l in dataset.labels] 
pred_scores = ce.scores #classification scores for all images and all classes
pred_labels = [labels[i] for i in np.argmax(pred_scores, axis=1)]

results_ui = ResultsUI(test_set, Context.get_global_context(), pred_scores, pred_labels)
display(results_ui.ui)
```

![Azure Machine Learning dataset](media/how-to-build-deploy-image-classification-models/Image_Classification_Results.png)


```python
# Precision / recall curve UI
precisions, recalls, thresholds = ce.compute_precision_recall_curve() 
thresholds = list(thresholds)
thresholds.append(thresholds[-1])
pr_ui = PrecisionRecallUI(100*precisions[::-1], 100*recalls[::-1], thresholds[::-1])
display(pr_ui.ui) 
```

![Azure Machine Learning dataset](media/how-to-build-deploy-image-classification-models/image_precision_curve.png)

## <a name="operationalization-deploy-and-consume"></a><span data-ttu-id="bdd9a-208">Operationalization: deploy and consume</span><span class="sxs-lookup"><span data-stu-id="bdd9a-208">Operationalization: deploy and consume</span></span>

<span data-ttu-id="bdd9a-209">Operationalization is the process of publishing models and code as web services and the consumption of these services to produce business results.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-209">Operationalization is the process of publishing models and code as web services and the consumption of these services to produce business results.</span></span> 

<span data-ttu-id="bdd9a-210">Once your model is trained, you can deploy that model as a web service for consumption using [Azure Machine Learning CLI](https://docs.microsoft.com/azure/machine-learning/desktop-workbench/cli-for-azure-machine-learning).</span><span class="sxs-lookup"><span data-stu-id="bdd9a-210">Once your model is trained, you can deploy that model as a web service for consumption using [Azure Machine Learning CLI](https://docs.microsoft.com/azure/machine-learning/desktop-workbench/cli-for-azure-machine-learning).</span></span> <span data-ttu-id="bdd9a-211">Your models can be deployed to your local machine or Azure Container Service (ACS) cluster.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-211">Your models can be deployed to your local machine or Azure Container Service (ACS) cluster.</span></span> <span data-ttu-id="bdd9a-212">Using ACS, you can scale your web service manually or use the autoscaling functionality.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-212">Using ACS, you can scale your web service manually or use the autoscaling functionality.</span></span>

<span data-ttu-id="bdd9a-213">**Sign in with Azure CLI**</span><span class="sxs-lookup"><span data-stu-id="bdd9a-213">**Sign in with Azure CLI**</span></span>

<span data-ttu-id="bdd9a-214">Using an [Azure](https://azure.microsoft.com/) account with a valid subscription, log in using the following CLI command:</span><span class="sxs-lookup"><span data-stu-id="bdd9a-214">Using an [Azure](https://azure.microsoft.com/) account with a valid subscription, log in using the following CLI command:</span></span>
<br>`az login`

+ <span data-ttu-id="bdd9a-215">To switch to another Azure subscription, use the command:</span><span class="sxs-lookup"><span data-stu-id="bdd9a-215">To switch to another Azure subscription, use the command:</span></span>
<br>`az account set --subscription [your subscription name]`

+ <span data-ttu-id="bdd9a-216">To see the current model management account, use the command:</span><span class="sxs-lookup"><span data-stu-id="bdd9a-216">To see the current model management account, use the command:</span></span>
  <br>`az ml account modelmanagement show`

<span data-ttu-id="bdd9a-217">**Create and set your cluster deployment environment**</span><span class="sxs-lookup"><span data-stu-id="bdd9a-217">**Create and set your cluster deployment environment**</span></span>

<span data-ttu-id="bdd9a-218">You only need to set your deployment environment once.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-218">You only need to set your deployment environment once.</span></span> <span data-ttu-id="bdd9a-219">If you don't have one yet, set up your deployment environment now using [these instructions](https://docs.microsoft.com/azure/machine-learning/desktop-workbench/deployment-setup-configuration#environment-setup).</span><span class="sxs-lookup"><span data-stu-id="bdd9a-219">If you don't have one yet, set up your deployment environment now using [these instructions](https://docs.microsoft.com/azure/machine-learning/desktop-workbench/deployment-setup-configuration#environment-setup).</span></span> 

<span data-ttu-id="bdd9a-220">To see your active deployment environment, use the following CLI command:</span><span class="sxs-lookup"><span data-stu-id="bdd9a-220">To see your active deployment environment, use the following CLI command:</span></span>
<br>`az ml env show`
   
<span data-ttu-id="bdd9a-221">Sample Azure CLI command to create and set deployment environment</span><span class="sxs-lookup"><span data-stu-id="bdd9a-221">Sample Azure CLI command to create and set deployment environment</span></span>

```CLI
az provider register -n Microsoft.MachineLearningCompute
az provider register -n Microsoft.ContainerRegistry
az provider register -n Microsoft.ContainerService
az ml env setup --cluster -n [your environment name] -l [Azure region e.g. westcentralus] [-g [resource group]]
az ml env set -n [environment name] -g [resource group]
az ml env cluster
```
    
### <a name="manage-web-services-and-deployments"></a><span data-ttu-id="bdd9a-222">Manage web services and deployments</span><span class="sxs-lookup"><span data-stu-id="bdd9a-222">Manage web services and deployments</span></span>

<span data-ttu-id="bdd9a-223">The following APIs can be used to deploy models as web services, manage those web services, and manage deployments.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-223">The following APIs can be used to deploy models as web services, manage those web services, and manage deployments.</span></span>

|<span data-ttu-id="bdd9a-224">Task</span><span class="sxs-lookup"><span data-stu-id="bdd9a-224">Task</span></span>|<span data-ttu-id="bdd9a-225">API</span><span class="sxs-lookup"><span data-stu-id="bdd9a-225">API</span></span>|
|----|----|
|<span data-ttu-id="bdd9a-226">Create deployment object</span><span class="sxs-lookup"><span data-stu-id="bdd9a-226">Create deployment object</span></span>|`deploy_obj = AMLDeployment(deployment_name=deployment_name, associated_DNNModel=dnn_model, aml_env="cluster")`
|<span data-ttu-id="bdd9a-227">Deploy web service</span><span class="sxs-lookup"><span data-stu-id="bdd9a-227">Deploy web service</span></span>|`deploy_obj.deploy()`|
|<span data-ttu-id="bdd9a-228">Score image</span><span class="sxs-lookup"><span data-stu-id="bdd9a-228">Score image</span></span>|`deploy_obj.score_image(local_image_path_or_image_url)`|
|<span data-ttu-id="bdd9a-229">Delete web service</span><span class="sxs-lookup"><span data-stu-id="bdd9a-229">Delete web service</span></span>|`deploy_obj.delete()`|
|<span data-ttu-id="bdd9a-230">Build docker image without web service</span><span class="sxs-lookup"><span data-stu-id="bdd9a-230">Build docker image without web service</span></span>|`deploy_obj.build_docker_image()`|
|<span data-ttu-id="bdd9a-231">List existing deployment</span><span class="sxs-lookup"><span data-stu-id="bdd9a-231">List existing deployment</span></span>|`AMLDeployment.list_deployment()`|
|<span data-ttu-id="bdd9a-232">Delete if the service exists with the deployment name</span><span class="sxs-lookup"><span data-stu-id="bdd9a-232">Delete if the service exists with the deployment name</span></span>|`AMLDeployment.delete_if_service_exist(deployment_name)`|

<span data-ttu-id="bdd9a-233">**API documentation:** Consult the [package reference documentation](https://aka.ms/aml-packages/vision) for the detailed reference for each module and class.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-233">**API documentation:** Consult the [package reference documentation](https://aka.ms/aml-packages/vision) for the detailed reference for each module and class.</span></span>

<span data-ttu-id="bdd9a-234">**CLI reference:** For more advanced operations related to deployment, refer to the [model management CLI reference](https://docs.microsoft.com/azure/machine-learning/desktop-workbench/model-management-cli-reference).</span><span class="sxs-lookup"><span data-stu-id="bdd9a-234">**CLI reference:** For more advanced operations related to deployment, refer to the [model management CLI reference](https://docs.microsoft.com/azure/machine-learning/desktop-workbench/model-management-cli-reference).</span></span>

<span data-ttu-id="bdd9a-235">**Deployment management in Azure portal**: You can track and manage your deployments in the [Azure portal](https://ms.portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="bdd9a-235">**Deployment management in Azure portal**: You can track and manage your deployments in the [Azure portal](https://ms.portal.azure.com/).</span></span> <span data-ttu-id="bdd9a-236">From the Azure portal, find your Machine Learning Model Management account page using its name.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-236">From the Azure portal, find your Machine Learning Model Management account page using its name.</span></span> <span data-ttu-id="bdd9a-237">Then go to the Model Management account page > Model Management > Services.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-237">Then go to the Model Management account page > Model Management > Services.</span></span>


```python
# ##### OPTIONAL###### 
# Interactive CLI setup helper, including model management account and deployment environment.
# If you haven't setup you CLI before or if you want to change you CLI settings, you can use this block to help you interactively.
#
# UNCOMMENT THE FOLLOWING LINES IF YOU HAVE NOT CREATED OR SET THE MODEL MANAGEMENT ACCOUNT AND DEPLOYMENT ENVIRONMENT
#
# from azuremltkbase.deployment import CliSetup
# CliSetup().run()
```


```python
# # Optional. Persist your model on disk and reuse it later for deployment. 
# from cvtk import TFFasterRCNN, Context
# import os
# save_model_path = os.path.join(Context.get_global_context().storage.persistent_path, "saved_classifier.model")
# # Save model to disk
# dnn_model.serialize(save_model_path)
# # Load model from disk
# dnn_model = CNTKTLModel.deserialize(save_model_path)
```


```python
from cvtk.operationalization import AMLDeployment

# set deployment name
deployment_name = "wsdeployment"

# Optional Azure Machine Learning deployment cluster name (environment name) and resource group name
# If you don't provide here. It will use the current deployment environment (you can check with CLI command "az ml env show").
azureml_rscgroup = "<resource group>"
cluster_name = "<cluster name>"

# If you provide the cluster information, it will use the provided cluster to deploy. 
# Example: deploy_obj = AMLDeployment(deployment_name=deployment_name, associated_DNNModel=dnn_model,
#                            aml_env="cluster", cluster_name=cluster_name, resource_group=azureml_rscgroup, replicas=1)

# Create deployment object
deploy_obj = AMLDeployment(deployment_name=deployment_name, aml_env="cluster", associated_DNNModel=dnn_model, replicas=1)

# Check if the deployment name exists, if yes remove it first.
if deploy_obj.is_existing_service():
    AMLDeployment.delete_if_service_exist(deployment_name)
    
# Create the web service
print("Deploying to Azure cluster...")
deploy_obj.deploy()
print("Deployment DONE")
```

### <a name="consume-the-web-service"></a><span data-ttu-id="bdd9a-238">Consume the web service</span><span class="sxs-lookup"><span data-stu-id="bdd9a-238">Consume the web service</span></span> 

<span data-ttu-id="bdd9a-239">Once you deploy the model as a web service, you can score images with the web service using one of these methods:</span><span class="sxs-lookup"><span data-stu-id="bdd9a-239">Once you deploy the model as a web service, you can score images with the web service using one of these methods:</span></span>

- <span data-ttu-id="bdd9a-240">Score the web service directly with the deployment object using `deploy_obj.score_image(image_path_or_url)`</span><span class="sxs-lookup"><span data-stu-id="bdd9a-240">Score the web service directly with the deployment object using `deploy_obj.score_image(image_path_or_url)`</span></span>

- <span data-ttu-id="bdd9a-241">Use the Service endpoint URL and Service key (None for local deployment) with: `AMLDeployment.score_existing_service_with_image(image_path_or_url, service_endpoint_url, service_key=None)`</span><span class="sxs-lookup"><span data-stu-id="bdd9a-241">Use the Service endpoint URL and Service key (None for local deployment) with: `AMLDeployment.score_existing_service_with_image(image_path_or_url, service_endpoint_url, service_key=None)`</span></span>

- <span data-ttu-id="bdd9a-242">Form your HTTP requests directly to score the web service endpoint.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-242">Form your HTTP requests directly to score the web service endpoint.</span></span> <span data-ttu-id="bdd9a-243">This option is for advanced users.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-243">This option is for advanced users.</span></span>

### <a name="score-with-existing-deployment-object"></a><span data-ttu-id="bdd9a-244">Score with existing deployment object</span><span class="sxs-lookup"><span data-stu-id="bdd9a-244">Score with existing deployment object</span></span>

```
deploy_obj.score_image(image_path_or_url)
```


```python
# Score with existing deployment object

# Score local image with file path
print("Score local image with file path")
image_path_or_url = test_set.images[0].storage_path
print("Image source:",image_path_or_url)
serialized_result_in_json = deploy_obj.score_image(image_path_or_url, image_resize_dims=[224,224])
print("serialized_result_in_json:", serialized_result_in_json)

# Score image url and remove image resizing
print("Score image url")
image_path_or_url = "https://cvtkdata.blob.core.windows.net/publicimages/microsoft_logo.jpg"
print("Image source:",image_path_or_url)
serialized_result_in_json = deploy_obj.score_image(image_path_or_url)
print("serialized_result_in_json:", serialized_result_in_json)

# Score image url with added paramters. Add softmax to score.
print("Score image url with added paramters. Add softmax to score")
from cvtk.utils.constants import ClassificationRESTApiParamters
image_path_or_url = "https://cvtkdata.blob.core.windows.net/publicimages/microsoft_logo.jpg"
print("Image source:",image_path_or_url)
serialized_result_in_json = deploy_obj.score_image(image_path_or_url, image_resize_dims=[224,224], parameters={ClassificationRESTApiParamters.ADD_SOFTMAX:True})
print("serialized_result_in_json:", serialized_result_in_json)
```


```python
# Time image scoring
import timeit

for img_index, img_obj in enumerate(test_set.images[:10]):
    print("Calling API for image {} of {}: {}...".format(img_index, len(test_set.images), img_obj.name))
    tic = timeit.default_timer()
    return_json = deploy_obj.score_image(img_obj.storage_path, image_resize_dims=[224,224])
    print("   Time for API call: {:.2f} seconds".format(timeit.default_timer() - tic))
    print(return_json)
```

### <a name="score-with-service-endpoint-url-and-service-key"></a><span data-ttu-id="bdd9a-245">Score with service endpoint url and service key</span><span class="sxs-lookup"><span data-stu-id="bdd9a-245">Score with service endpoint url and service key</span></span>

`AMLDeployment.score_existing_service_with_image(image_path_or_url, service_endpoint_url, service_key=None)`

```python
# Import related classes and functions
from cvtk.operationalization import AMLDeployment

service_endpoint_url = "" # please replace with your own service url
service_key = "" # please replace with your own service key
# score local image with file path
image_path_or_url = test_set.images[0].storage_path
print("Image source:",image_path_or_url)
serialized_result_in_json = AMLDeployment.score_existing_service_with_image(image_path_or_url,service_endpoint_url, service_key = service_key)
print("serialized_result_in_json:", serialized_result_in_json)

# score image url
image_path_or_url = "https://cvtkdata.blob.core.windows.net/publicimages/microsoft_logo.jpg"
print("Image source:",image_path_or_url)
serialized_result_in_json = AMLDeployment.score_existing_service_with_image(image_path_or_url,service_endpoint_url, service_key = service_key, image_resize_dims=[224,224])
print("serialized_result_in_json:", serialized_result_in_json)
```

### <a name="score-endpoint-with-http-request-directly"></a><span data-ttu-id="bdd9a-246">Score endpoint with http request directly</span><span class="sxs-lookup"><span data-stu-id="bdd9a-246">Score endpoint with http request directly</span></span>

<span data-ttu-id="bdd9a-247">The following example code forms the HTTP request directly in Python.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-247">The following example code forms the HTTP request directly in Python.</span></span> <span data-ttu-id="bdd9a-248">However, you can do it in other programming languages.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-248">However, you can do it in other programming languages.</span></span>


```python
def score_image_list_with_http(images, service_endpoint_url, service_key=None, parameters={}):
    """Score image list with http request

    Args:
        images(list): list of (input image file path, base64 image string, url or buffer)
        service_endpoint_url(str): endpoint url
        service_key(str): service key, None for local deployment.
        parameters(dict): service additional paramters in dictionary


    Returns:
        result (list): list of serialized result 
    """
    import requests
    from io import BytesIO
    import base64
    routing_id = ""

    if service_key is None:
        headers = {'Content-Type': 'application/json',
                   'X-Marathon-App-Id': routing_id}
    else:
        headers = {'Content-Type': 'application/json',
                   "Authorization": ('Bearer ' + service_key), 'X-Marathon-App-Id': routing_id}
    payload = []
    for image in images:
        encoded = None
        # read image
        with open(image,'rb') as f:
            image_buffer = BytesIO(f.read()) ## Getting an image file represented as a BytesIO object
        # convert your image to base64 string
        encoded = base64.b64encode(image_buffer.getvalue())
        image_request = {"image_in_base64": "{0}".format(encoded), "parameters": parameters}
        payload.append(image_request)
    body = json.dumps(payload)
    r = requests.post(service_endpoint_url, data=body, headers=headers)
    try:
        result = json.loads(r.text)
    except:
        raise ValueError("Incorrect output format. Result cant not be parsed: " + r.text)
    return result

# Test with images
images = [test_set.images[0].storage_path, test_set.images[1].storage_path] # A list of local image files
score_image_list_with_http(images, service_endpoint_url, service_key)
```

### <a name="parse-serialized-result-from-web-service"></a><span data-ttu-id="bdd9a-249">Parse serialized result from web service</span><span class="sxs-lookup"><span data-stu-id="bdd9a-249">Parse serialized result from web service</span></span>

<span data-ttu-id="bdd9a-250">The output from the web service is a JSON string.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-250">The output from the web service is a JSON string.</span></span> <span data-ttu-id="bdd9a-251">You can parse this JSON string with different DNN model classes.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-251">You can parse this JSON string with different DNN model classes.</span></span>


```python
image_path_or_url = test_set.images[0].storage_path
print("Image source:",image_path_or_url)
serialized_result_in_json = deploy_obj.score_image(image_path_or_url, image_resize_dims=[224,224])
print("serialized_result_in_json:", serialized_result_in_json)
```


```python
# Parse result from json string
import numpy as np
parsed_result = CNTKTLModel.parse_serialized_result(serialized_result_in_json)
print("Parsed result:", parsed_result)
# Map result to image class
class_index = np.argmax(np.array(parsed_result))
print("Class index:", class_index)
dnn_model.class_map
print("Class label:", dnn_model.class_map[class_index])
```


## <a name="next-steps"></a><span data-ttu-id="bdd9a-252">Next steps</span><span class="sxs-lookup"><span data-stu-id="bdd9a-252">Next steps</span></span>

<span data-ttu-id="bdd9a-253">Learn more about Azure Machine Learning Package for Computer Vision in these articles:</span><span class="sxs-lookup"><span data-stu-id="bdd9a-253">Learn more about Azure Machine Learning Package for Computer Vision in these articles:</span></span>

+ <span data-ttu-id="bdd9a-254">Learn how to [improve the accuracy of this model](how-to-improve-accuracy-for-computer-vision-models.md).</span><span class="sxs-lookup"><span data-stu-id="bdd9a-254">Learn how to [improve the accuracy of this model](how-to-improve-accuracy-for-computer-vision-models.md).</span></span>

+ <span data-ttu-id="bdd9a-255">Read the [package overview and learn how to install it](https://aka.ms/aml-packages/vision).</span><span class="sxs-lookup"><span data-stu-id="bdd9a-255">Read the [package overview and learn how to install it](https://aka.ms/aml-packages/vision).</span></span>

+ <span data-ttu-id="bdd9a-256">Explore the [reference documentation](https://docs.microsoft.com/python/api/overview/azure-machine-learning/computer-vision) for this package.</span><span class="sxs-lookup"><span data-stu-id="bdd9a-256">Explore the [reference documentation](https://docs.microsoft.com/python/api/overview/azure-machine-learning/computer-vision) for this package.</span></span>

+ <span data-ttu-id="bdd9a-257">Learn about [other Python packages for Azure Machine Learning](reference-python-package-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bdd9a-257">Learn about [other Python packages for Azure Machine Learning](reference-python-package-overview.md).</span></span>
