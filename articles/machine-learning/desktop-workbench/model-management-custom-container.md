---
title: Customize the Container Image Used for Deploying Azure ML Models | Microsoft Docs
description: This article describes how to customize a container image for Azure Machine Learning models
services: machine-learning
author: tedway
ms.author: tedway
manager: mwinkle
ms.reviewer: mldocs, raymondl
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.topic: article
ms.date: 3/26/2018
ms.openlocfilehash: 7879cf1891e071da1a0ad3ddfc30f90fc7be8ca5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857203"
---
# <a name="customize-the-container-image-used-for-azure-ml-models"></a><span data-ttu-id="2b0d8-103">Customize the container image used for Azure ML Models</span><span class="sxs-lookup"><span data-stu-id="2b0d8-103">Customize the container image used for Azure ML Models</span></span>

<span data-ttu-id="2b0d8-104">This article describes how to customize a container image for Azure Machine Learning models.</span><span class="sxs-lookup"><span data-stu-id="2b0d8-104">This article describes how to customize a container image for Azure Machine Learning models.</span></span>  <span data-ttu-id="2b0d8-105">Azure ML Workbench uses containers for deploying machine learning models.</span><span class="sxs-lookup"><span data-stu-id="2b0d8-105">Azure ML Workbench uses containers for deploying machine learning models.</span></span> <span data-ttu-id="2b0d8-106">The models are deployed along with their dependencies, and Azure ML builds an image from the model, the dependencies, and associated files.</span><span class="sxs-lookup"><span data-stu-id="2b0d8-106">The models are deployed along with their dependencies, and Azure ML builds an image from the model, the dependencies, and associated files.</span></span>

## <a name="how-to-customize-the-docker-image"></a><span data-ttu-id="2b0d8-107">How to customize the Docker image</span><span class="sxs-lookup"><span data-stu-id="2b0d8-107">How to customize the Docker image</span></span>
<span data-ttu-id="2b0d8-108">Customize the Docker image that Azure ML deploys using:</span><span class="sxs-lookup"><span data-stu-id="2b0d8-108">Customize the Docker image that Azure ML deploys using:</span></span>

1. <span data-ttu-id="2b0d8-109">A `dependencies.yml` file: to manage dependencies that are installable from [PyPi]( https://pypi.python.org/pypi), you can use the `conda_dependencies.yml` file from the Workbench project, or create your own.</span><span class="sxs-lookup"><span data-stu-id="2b0d8-109">A `dependencies.yml` file: to manage dependencies that are installable from [PyPi]( https://pypi.python.org/pypi), you can use the `conda_dependencies.yml` file from the Workbench project, or create your own.</span></span> <span data-ttu-id="2b0d8-110">This is the recommend approach for installing Python dependencies that are pip-installable.</span><span class="sxs-lookup"><span data-stu-id="2b0d8-110">This is the recommend approach for installing Python dependencies that are pip-installable.</span></span>

   <span data-ttu-id="2b0d8-111">Example CLI command:</span><span class="sxs-lookup"><span data-stu-id="2b0d8-111">Example CLI command:</span></span>
   ```azurecli
   az ml image create -n <my Image Name> --manifest-id <my Manifest ID> -c amlconfig\conda_dependencies.yml
   ```

   <span data-ttu-id="2b0d8-112">Example conda_dependencies file:</span><span class="sxs-lookup"><span data-stu-id="2b0d8-112">Example conda_dependencies file:</span></span> 
   ```yaml
   name: project_environment
   dependencies:
      - python=3.5.2
      - scikit-learn
      - ipykernel=4.6.1
      
      - pip:
        - azure-ml-api-sdk==0.1.0a11
        - matplotlib
   ```
        
2. <span data-ttu-id="2b0d8-113">A Docker steps file: using this option, you customize the deployed image by installing dependencies that cannot be installed from PyPi.</span><span class="sxs-lookup"><span data-stu-id="2b0d8-113">A Docker steps file: using this option, you customize the deployed image by installing dependencies that cannot be installed from PyPi.</span></span> 

   <span data-ttu-id="2b0d8-114">The file should include Docker installation steps like a DockerFile.</span><span class="sxs-lookup"><span data-stu-id="2b0d8-114">The file should include Docker installation steps like a DockerFile.</span></span> <span data-ttu-id="2b0d8-115">The following commands are allowed in the file:</span><span class="sxs-lookup"><span data-stu-id="2b0d8-115">The following commands are allowed in the file:</span></span> 

    <span data-ttu-id="2b0d8-116">RUN, ENV, ARG, LABEL, EXPOSE</span><span class="sxs-lookup"><span data-stu-id="2b0d8-116">RUN, ENV, ARG, LABEL, EXPOSE</span></span>

   <span data-ttu-id="2b0d8-117">Example CLI command:</span><span class="sxs-lookup"><span data-stu-id="2b0d8-117">Example CLI command:</span></span>
   ```azurecli
   az ml image create -n <my Image Name> --manifest-id <my Manifest ID> --docker-file <myDockerStepsFileName> 
   ```

   <span data-ttu-id="2b0d8-118">Image, Manifest, and Service commands accept the docker-file flag.</span><span class="sxs-lookup"><span data-stu-id="2b0d8-118">Image, Manifest, and Service commands accept the docker-file flag.</span></span>

   <span data-ttu-id="2b0d8-119">Example Docker steps file:</span><span class="sxs-lookup"><span data-stu-id="2b0d8-119">Example Docker steps file:</span></span>
   ```docker
   # Install tools required to build the project
   RUN apt-get update && apt-get install -y git libxml2-dev
   # Install library dependencies
   RUN dep ensure -vendor-only
   ```

> [!NOTE]
> <span data-ttu-id="2b0d8-120">The base image for Azure ML containers is Ubuntu and can't be changed.</span><span class="sxs-lookup"><span data-stu-id="2b0d8-120">The base image for Azure ML containers is Ubuntu and can't be changed.</span></span> <span data-ttu-id="2b0d8-121">If you specify a different base image, it will be ignored.</span><span class="sxs-lookup"><span data-stu-id="2b0d8-121">If you specify a different base image, it will be ignored.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b0d8-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="2b0d8-122">Next steps</span></span>
<span data-ttu-id="2b0d8-123">Now that you've customized your container image, you can deploy it to a cluster for large-scale use.</span><span class="sxs-lookup"><span data-stu-id="2b0d8-123">Now that you've customized your container image, you can deploy it to a cluster for large-scale use.</span></span>  <span data-ttu-id="2b0d8-124">For details on setting up a cluster for web service deployment, see [Model Management Configuration](deployment-setup-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="2b0d8-124">For details on setting up a cluster for web service deployment, see [Model Management Configuration](deployment-setup-configuration.md).</span></span> 
