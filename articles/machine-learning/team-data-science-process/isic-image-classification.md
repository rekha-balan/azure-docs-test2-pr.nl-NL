---
title: Image classification with the Azure Machine Learning package for computer vision and Team Data Science Process (TDSP) | Microsoft Docs
description: Describes the use of Team Data Science Process (TDSP) and the Azure Machine Learning package for computer vision for image classification.
services: machine-learning, team-data-science-process
documentationcenter: ''
author: deguhath
ms.author: deguhath
editor: cgronlun
ms.assetid: b8fbef77-3e80-4911-8e84-23dbf42c9bee
ms.service: machine-learning
ms.component: team-data-science-process
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2018
ms.openlocfilehash: 427ea1f3f22855b2c54beacbfb89a8f7fd37cce0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967347"
---
# <a name="skin-cancer-image-classification-with-the-azure-machine-learning-package-for-computer-vision-and-team-data-science-process"></a>Skin cancer image classification with the Azure Machine Learning package for computer vision and Team Data Science Process

This article shows you how to use the [Azure Machine Learning package for computer vision](https://docs.microsoft.com/en-us/python/api/overview/azure-machine-learning/computer-vision?view=azure-ml-py-latest) to train, test, and deploy an *image classification* model. The sample uses the Team Data Science Process (TDSP) structure and templates in [Azure Machine Learning Workbench](https://docs.microsoft.com/en-us/azure/machine-learning/service/quickstart-installation). This walkthrough provides the complete sample. It uses the [Microsoft Cognitive Toolkit](https://www.microsoft.com/en-us/cognitive-toolkit/) as the deep learning framework, and training is performed on a [Data Science virtual machine](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/microsoft-ads.dsvm-deep-learning?tab=Overview) GPU machine. Deployment uses the Azure Machine Learning operationalization CLI.

Many applications in the computer vision domain can be framed as image classification problems. These include building models that answer simple questions like "Is an object present in the image?" where the object might be a dog, car, or ship. It also includes answers to more complex questions, such as "What class of eye disease severity is evinced by this patient's retinal scan?" The Azure Machine Learning package for computer vision streamlines image classification data processing and the modeling pipeline. 

## <a name="link-to-the-github-repository"></a>Link to the GitHub repository
This article is a summary document about the sample. You can find more extensive documentation on the [GitHub site](https://github.com/Azure/MachineLearningSamples-AMLVisionPackage-ISICImageClassification).

## <a name="team-data-science-process-walkthrough"></a>Team Data Science Process walkthrough

This walkthrough uses the [Team Data Science Process](https://docs.microsoft.com/en-us/azure/machine-learning/team-data-science-process/overview) lifecycle. The walkthrough covers the following lifecycle steps.

### <a name="1-data-acquisitionhttpsgithubcomazuremachinelearningsamples-amlvisionpackage-isicimageclassificationblobmastercode01dataacquisitionandunderstanding"></a>[1. Data acquisition](https://github.com/Azure/MachineLearningSamples-AMLVisionPackage-ISICImageClassification/blob/master/code/01_data_acquisition_and_understanding)
The International Skin Imaging Collaboration (ISIC) dataset is used for the image classification task. ISIC is a partnership between academia and industry to facilitate the application of digital skin imaging to study and help reduce melanoma mortality. The [ISIC archive](https://isic-archive.com/#images) contains more than 13,000 skin lesion images that are labeled as either benign or malignant. Download a sample of the images from the ISIC archive.

### <a name="2-modelinghttpsgithubcomazuremachinelearningsamples-amlvisionpackage-isicimageclassificationblobmastercode02modeling"></a>[2. Modeling](https://github.com/Azure/MachineLearningSamples-AMLVisionPackage-ISICImageClassification/blob/master/code/02_modeling)
In the modeling step, the following substeps are performed.

#### <a name="dataset-creation"></a>Dataset creation

Generate a dataset object in the Azure Machine Learning package for computer vision by providing a root directory of images on the local disk. 

#### <a name="image-visualization-and-annotation"></a>Image visualization and annotation

Visualize the images in the dataset object and correct the labels as necessary.

#### <a name="image-augmentation"></a>Image augmentation

Augment a dataset object by using the transformations that are described in the [imgaug](https://github.com/aleju/imgaug) library.

#### <a name="dnn-model-definition"></a>DNN model definition

Define the model architecture that's used in the training step. Six pre-trained deep neural network models are supported in the Azure Machine Learning package for computer vision: AlexNet, Resnet-18, Resnet-34, Resnet-50, Resnet-101, and Resnet-152.

#### <a name="classifier-training"></a>Classifier training

Train the neural networks with default or custom parameters.

#### <a name="evaluation-and-visualization"></a>Evaluation and visualization

Provide functionality to evaluate the performance of the trained model on an independent test dataset. The evaluation metrics include accuracy, precision, recall, and ROC curve.

The substeps are explained in detail in the corresponding Jupyter Notebook. The notebook also provides guidelines for turning the parameters, such as the learning rate, mini batch size, and dropout rate to further improve the model performance.

### <a name="3-deploymenthttpsgithubcomazuremachinelearningsamples-amlvisionpackage-isicimageclassificationblobmastercode03deployment"></a>[3. Deployment](https://github.com/Azure/MachineLearningSamples-AMLVisionPackage-ISICImageClassification/blob/master/code/03_deployment)

This step operationalizes the model that's produced from the modeling step. It introduces the prerequisites and the required setup. The consumption of the web service is also explained. In this tutorial, you  learn to build deep learning models with the Azure Machine Learning package for computer vision and operationalize the model in Azure.

## <a name="next-steps"></a>Next steps
- Read additional documentation about [Azure Machine Learning package for computer vision](https://docs.microsoft.com/en-us/python/api/overview/azure-machine-learning/computer-vision?view=azure-ml-py-latest).
- Read the [Team Data Science Process](https://aka.ms/tdsp) documentation to get started.


## <a name="references"></a>References

* [Azure Machine Learning package for computer vision](https://docs.microsoft.com/en-us/python/api/overview/azure-machine-learning/computer-vision?view=azure-ml-py-latest)
* [Azure Machine Learning Workbench](https://docs.microsoft.com/en-us/azure/machine-learning/service/quickstart-installation)
* [Data Science virtual machine](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/microsoft-ads.dsvm-deep-learning?tab=Overview)

