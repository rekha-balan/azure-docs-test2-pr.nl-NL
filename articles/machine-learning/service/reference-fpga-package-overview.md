---
title: FPGA package for hardware acceleration for Azure Machine Learning
description: Learn about the python packages available for Azure Machine Learning users.
ms.service: machine-learning
ms.component: core
ms.topic: conceptual
ms.reviewer: jmartens
ms.author: tedway
author: tedway
ms.date: 05/07/2018
ms.openlocfilehash: 151b865498f183ba131ae68cce61a61729136149
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865850"
---
# <a name="azure-machine-learning-hardware-acceleration-package"></a><span data-ttu-id="852f9-103">Azure Machine Learning Hardware Acceleration package</span><span class="sxs-lookup"><span data-stu-id="852f9-103">Azure Machine Learning Hardware Acceleration package</span></span>

<span data-ttu-id="852f9-104">The Azure Machine Learning Hardware Acceleration package is a Python pip-installable extension for Azure Machine Learning that enables data scientists and AI developers to quickly:</span><span class="sxs-lookup"><span data-stu-id="852f9-104">The Azure Machine Learning Hardware Acceleration package is a Python pip-installable extension for Azure Machine Learning that enables data scientists and AI developers to quickly:</span></span>

+ <span data-ttu-id="852f9-105">Featurize images with a quantized version of ResNet 50</span><span class="sxs-lookup"><span data-stu-id="852f9-105">Featurize images with a quantized version of ResNet 50</span></span>

+ <span data-ttu-id="852f9-106">Train classifiers based on those features</span><span class="sxs-lookup"><span data-stu-id="852f9-106">Train classifiers based on those features</span></span>

+ <span data-ttu-id="852f9-107">Deploy models to [field programmable gate arrays (FPGA)](concept-accelerate-with-fpgas.md) on Azure for ultra-low latency inferencing</span><span class="sxs-lookup"><span data-stu-id="852f9-107">Deploy models to [field programmable gate arrays (FPGA)](concept-accelerate-with-fpgas.md) on Azure for ultra-low latency inferencing</span></span>

## <a name="prerequisites"></a><span data-ttu-id="852f9-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="852f9-108">Prerequisites</span></span>

1. <span data-ttu-id="852f9-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="852f9-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

1. <span data-ttu-id="852f9-110">You must create an Azure Machine Learning Model Management account.</span><span class="sxs-lookup"><span data-stu-id="852f9-110">You must create an Azure Machine Learning Model Management account.</span></span> <span data-ttu-id="852f9-111">For more information on creating the account, see the [Azure Machine Learning Quickstart and Workbench installation](../service/quickstart-installation.md) document.</span><span class="sxs-lookup"><span data-stu-id="852f9-111">For more information on creating the account, see the [Azure Machine Learning Quickstart and Workbench installation](../service/quickstart-installation.md) document.</span></span> 

1. <span data-ttu-id="852f9-112">The package must be installed.</span><span class="sxs-lookup"><span data-stu-id="852f9-112">The package must be installed.</span></span> 

 
## <a name="how-to-install-the-package"></a><span data-ttu-id="852f9-113">How to install the package</span><span class="sxs-lookup"><span data-stu-id="852f9-113">How to install the package</span></span>

1. <span data-ttu-id="852f9-114">Download and install the latest version of [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="852f9-114">Download and install the latest version of [Git](https://git-scm.com/downloads).</span></span>

2. <span data-ttu-id="852f9-115">Install [Anaconda (Python 3.6)](https://conda.io/miniconda.html)</span><span class="sxs-lookup"><span data-stu-id="852f9-115">Install [Anaconda (Python 3.6)](https://conda.io/miniconda.html)</span></span>

   <span data-ttu-id="852f9-116">To download a pre-configured Anaconda environment, use the following command from the Git prompt:</span><span class="sxs-lookup"><span data-stu-id="852f9-116">To download a pre-configured Anaconda environment, use the following command from the Git prompt:</span></span>

    ```
    git clone https://aka.ms/aml-real-time-ai
    ```
1. <span data-ttu-id="852f9-117">To create the environment, open an **Anaconda Prompt** and use the following command:</span><span class="sxs-lookup"><span data-stu-id="852f9-117">To create the environment, open an **Anaconda Prompt** and use the following command:</span></span>

    ```
    conda env create -f aml-real-time-ai/environment.yml
    ```

1. <span data-ttu-id="852f9-118">To activate the environment, use the following command:</span><span class="sxs-lookup"><span data-stu-id="852f9-118">To activate the environment, use the following command:</span></span>

    ```
    conda activate amlrealtimeai
    ```

## <a name="sample-code"></a><span data-ttu-id="852f9-119">Sample code</span><span class="sxs-lookup"><span data-stu-id="852f9-119">Sample code</span></span>

<span data-ttu-id="852f9-120">This sample code walks you through using the SDK to deploy a model to an FPGA.</span><span class="sxs-lookup"><span data-stu-id="852f9-120">This sample code walks you through using the SDK to deploy a model to an FPGA.</span></span>

1. <span data-ttu-id="852f9-121">Import the package:</span><span class="sxs-lookup"><span data-stu-id="852f9-121">Import the package:</span></span>
   ```python
   import amlrealtimeai
   from amlrealtimeai import resnet50
   ```

1. <span data-ttu-id="852f9-122">Pre-process the image:</span><span class="sxs-lookup"><span data-stu-id="852f9-122">Pre-process the image:</span></span>
   ```python 
   from amlrealtimeai.resnet50.model import LocalQuantizedResNet50
   model_path = os.path.expanduser('~/models')
   model = LocalQuantizedResNet50(model_path)
   print(model.version)
   ```

1. <span data-ttu-id="852f9-123">Featurize the images:</span><span class="sxs-lookup"><span data-stu-id="852f9-123">Featurize the images:</span></span>
   ```python 
   from amlrealtimeai.resnet50.model import LocalQuantizedResNet50
   model_path = os.path.expanduser('~/models')
   model = LocalQuantizedResNet50(model_path)
   print(model.version)
   ```

1. <span data-ttu-id="852f9-124">Create a classifier:</span><span class="sxs-lookup"><span data-stu-id="852f9-124">Create a classifier:</span></span>
   ```python
   model.import_graph_def(include_featurizer=False)
   print(model.classifier_input)
   print(model.classifier_output)
   ```

1. <span data-ttu-id="852f9-125">Create the service definition:</span><span class="sxs-lookup"><span data-stu-id="852f9-125">Create the service definition:</span></span>
   ```python
   from amlrealtimeai.pipeline import ServiceDefinition, TensorflowStage, BrainWaveStage
   save_path = os.path.expanduser('~/models/save')
   service_def_path = os.path.join(save_path, 'service_def.zip')

   service_def = ServiceDefinition()
   service_def.pipeline.append(TensorflowStage(tf.Session(), in_images, image_tensors))
   service_def.pipeline.append(BrainWaveStage(model))
   service_def.pipeline.append(TensorflowStage(tf.Session(), model.classifier_input, model.classifier_output))
   service_def.save(service_def_path)
   print(service_def_path)
   ```
 
1. <span data-ttu-id="852f9-126">Prepare the model to run on an FPGA:</span><span class="sxs-lookup"><span data-stu-id="852f9-126">Prepare the model to run on an FPGA:</span></span>
   ```python
   from amlrealtimeai import DeploymentClient

   subscription_id = "<Your Azure Subscription ID>"
   resource_group = "<Your Azure Resource Group Name>"
   model_management_account = "<Your AzureML Model Management Account Name>"

   model_name = "resnet50-model"
   service_name = "quickstart-service"

   deployment_client = DeploymentClient(subscription_id, resource_group, model_management_account)
   ```

1. <span data-ttu-id="852f9-127">Deploy the model to run on an FPGA:</span><span class="sxs-lookup"><span data-stu-id="852f9-127">Deploy the model to run on an FPGA:</span></span>
   ```python
   service = deployment_client.get_service_by_name(service_name)
   model_id = deployment_client.register_model(model_name, service_def_path)

   if(service is None):
      service = deployment_client.create_service(service_name, model_id)    
   else:
      service = deployment_client.update_service(service.id, model_id)
   ```

1. <span data-ttu-id="852f9-128">Create the client:</span><span class="sxs-lookup"><span data-stu-id="852f9-128">Create the client:</span></span>
    ```python
   from amlrealtimeai import PredictionClient
   client = PredictionClient(service.ipAddress, service.port)  
   ```

1. <span data-ttu-id="852f9-129">Call the API:</span><span class="sxs-lookup"><span data-stu-id="852f9-129">Call the API:</span></span>
   ```python
   image_file = R'C:\path_to_file\image.jpg'
   results = client.score_image(image_file)
   ```

## <a name="reporting-issues"></a><span data-ttu-id="852f9-130">Reporting issues</span><span class="sxs-lookup"><span data-stu-id="852f9-130">Reporting issues</span></span>

<span data-ttu-id="852f9-131">Use the [forum](https://aka.ms/aml-forum) to report any issues you encounter with the package.</span><span class="sxs-lookup"><span data-stu-id="852f9-131">Use the [forum](https://aka.ms/aml-forum) to report any issues you encounter with the package.</span></span>

## <a name="next-steps"></a><span data-ttu-id="852f9-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="852f9-132">Next steps</span></span>

[<span data-ttu-id="852f9-133">Deploy a model as a web service on an FPGA</span><span class="sxs-lookup"><span data-stu-id="852f9-133">Deploy a model as a web service on an FPGA</span></span>](how-to-deploy-fpga-web-service.md)