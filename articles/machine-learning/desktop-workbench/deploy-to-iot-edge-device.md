---
title: Deploy an Azure Machine Learning model to an Azure IoT Edge device | Microsoft Docs
description: This document describes how Azure Machine Learning models can be deployed to Azure IoT Edge devices.
services: machine-learning
author: tedway
ms.author: tedway
manager: mwinkle
ms.reviewer: jmartens, jasonwhowell, mldocs
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.topic: article
ms.date: 08/24/2018
ms.openlocfilehash: 24d3cf0c4b1a1283e7a6a7f61f0bb23dae7143d5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870176"
---
# <a name="deploy-an-azure-machine-learning-model-to-an-azure-iot-edge-device"></a><span data-ttu-id="6cc52-103">Deploy an Azure Machine Learning model to an Azure IoT Edge device</span><span class="sxs-lookup"><span data-stu-id="6cc52-103">Deploy an Azure Machine Learning model to an Azure IoT Edge device</span></span>

<span data-ttu-id="6cc52-104">Azure Machine Learning models can be containerized as Docker-based web services.</span><span class="sxs-lookup"><span data-stu-id="6cc52-104">Azure Machine Learning models can be containerized as Docker-based web services.</span></span> <span data-ttu-id="6cc52-105">Azure IoT Edge enables you to deploy containers remotely onto devices.</span><span class="sxs-lookup"><span data-stu-id="6cc52-105">Azure IoT Edge enables you to deploy containers remotely onto devices.</span></span> <span data-ttu-id="6cc52-106">Use these services together to run your models at the edge for faster response times and less data transfer.</span><span class="sxs-lookup"><span data-stu-id="6cc52-106">Use these services together to run your models at the edge for faster response times and less data transfer.</span></span> 

<span data-ttu-id="6cc52-107">Additional scripts and instructions can be found in the [AI Toolkit for Azure IoT Edge](http://aka.ms/AI-toolkit).</span><span class="sxs-lookup"><span data-stu-id="6cc52-107">Additional scripts and instructions can be found in the [AI Toolkit for Azure IoT Edge](http://aka.ms/AI-toolkit).</span></span>

## <a name="operationalize-the-model"></a><span data-ttu-id="6cc52-108">Operationalize the model</span><span class="sxs-lookup"><span data-stu-id="6cc52-108">Operationalize the model</span></span>

<span data-ttu-id="6cc52-109">Azure IoT Edge modules are based on container images.</span><span class="sxs-lookup"><span data-stu-id="6cc52-109">Azure IoT Edge modules are based on container images.</span></span> <span data-ttu-id="6cc52-110">To deploy your Machine Learning model to an IoT Edge device, you need to create a Docker image.</span><span class="sxs-lookup"><span data-stu-id="6cc52-110">To deploy your Machine Learning model to an IoT Edge device, you need to create a Docker image.</span></span>

<span data-ttu-id="6cc52-111">Operationalize your model by following the instructions in [Azure Machine Learning Model Management Web Service Deployment](model-management-service-deploy.md) to create a Docker image with your model.</span><span class="sxs-lookup"><span data-stu-id="6cc52-111">Operationalize your model by following the instructions in [Azure Machine Learning Model Management Web Service Deployment](model-management-service-deploy.md) to create a Docker image with your model.</span></span>

## <a name="deploy-to-azure-iot-edge"></a><span data-ttu-id="6cc52-112">Deploy to Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="6cc52-112">Deploy to Azure IoT Edge</span></span>

<span data-ttu-id="6cc52-113">Once you have the image of your model, you can deploy it to any Azure IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="6cc52-113">Once you have the image of your model, you can deploy it to any Azure IoT Edge device.</span></span> <span data-ttu-id="6cc52-114">All Machine Learning models can run on IoT Edge devices.</span><span class="sxs-lookup"><span data-stu-id="6cc52-114">All Machine Learning models can run on IoT Edge devices.</span></span> 

### <a name="set-up-an-iot-edge-device"></a><span data-ttu-id="6cc52-115">Set up an IoT Edge device</span><span class="sxs-lookup"><span data-stu-id="6cc52-115">Set up an IoT Edge device</span></span>

<span data-ttu-id="6cc52-116">Use the Azure IoT Edge documentation to prepare a device.</span><span class="sxs-lookup"><span data-stu-id="6cc52-116">Use the Azure IoT Edge documentation to prepare a device.</span></span> 

1. <span data-ttu-id="6cc52-117">[Register a device with Azure IoT Hub](../../iot-edge/how-to-register-device-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6cc52-117">[Register a device with Azure IoT Hub](../../iot-edge/how-to-register-device-portal.md).</span></span> <span data-ttu-id="6cc52-118">The output of this processes is a connection string that you can use to configure your physical device.</span><span class="sxs-lookup"><span data-stu-id="6cc52-118">The output of this processes is a connection string that you can use to configure your physical device.</span></span> 
2. <span data-ttu-id="6cc52-119">Install the IoT Edge runtime on your physical device, and configure it with a connection string.</span><span class="sxs-lookup"><span data-stu-id="6cc52-119">Install the IoT Edge runtime on your physical device, and configure it with a connection string.</span></span> <span data-ttu-id="6cc52-120">You can install the runtime on [Windows](../../iot-edge/how-to-install-iot-edge-windows-with-windows.md) or [Linux](../../iot-edge/how-to-install-iot-edge-linux.md) devices.</span><span class="sxs-lookup"><span data-stu-id="6cc52-120">You can install the runtime on [Windows](../../iot-edge/how-to-install-iot-edge-windows-with-windows.md) or [Linux](../../iot-edge/how-to-install-iot-edge-linux.md) devices.</span></span>  


### <a name="find-the-machine-learning-container-image-location"></a><span data-ttu-id="6cc52-121">Find the Machine Learning container image location</span><span class="sxs-lookup"><span data-stu-id="6cc52-121">Find the Machine Learning container image location</span></span>
<span data-ttu-id="6cc52-122">You need the location of your Machine Learning container image.</span><span class="sxs-lookup"><span data-stu-id="6cc52-122">You need the location of your Machine Learning container image.</span></span> <span data-ttu-id="6cc52-123">To find the container image location:</span><span class="sxs-lookup"><span data-stu-id="6cc52-123">To find the container image location:</span></span>

1. <span data-ttu-id="6cc52-124">Log into the [Azure portal](http://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="6cc52-124">Log into the [Azure portal](http://portal.azure.com/).</span></span>
2. <span data-ttu-id="6cc52-125">In the **Azure Container Registry**, select the registry you wish to inspect.</span><span class="sxs-lookup"><span data-stu-id="6cc52-125">In the **Azure Container Registry**, select the registry you wish to inspect.</span></span>
3. <span data-ttu-id="6cc52-126">In the registry, click **Repositories** to see a list of all the repositories and their images.</span><span class="sxs-lookup"><span data-stu-id="6cc52-126">In the registry, click **Repositories** to see a list of all the repositories and their images.</span></span>

<span data-ttu-id="6cc52-127">While you're looking at your container registry in the Azure portal, retrieve the container registry credentials.</span><span class="sxs-lookup"><span data-stu-id="6cc52-127">While you're looking at your container registry in the Azure portal, retrieve the container registry credentials.</span></span> <span data-ttu-id="6cc52-128">These credentials need to be given to the IoT Edge device so that it can pull the image from your private registry.</span><span class="sxs-lookup"><span data-stu-id="6cc52-128">These credentials need to be given to the IoT Edge device so that it can pull the image from your private registry.</span></span> 

1. <span data-ttu-id="6cc52-129">In the container registry, click **Access keys**.</span><span class="sxs-lookup"><span data-stu-id="6cc52-129">In the container registry, click **Access keys**.</span></span> 
2. <span data-ttu-id="6cc52-130">**Enable** the admin user, if it isn't already.</span><span class="sxs-lookup"><span data-stu-id="6cc52-130">**Enable** the admin user, if it isn't already.</span></span> 
3. <span data-ttu-id="6cc52-131">Save the values for **Login server**, **Username**, and **password**.</span><span class="sxs-lookup"><span data-stu-id="6cc52-131">Save the values for **Login server**, **Username**, and **password**.</span></span> 

### <a name="deploy-the-container-image-to-your-device"></a><span data-ttu-id="6cc52-132">Deploy the container image to your device</span><span class="sxs-lookup"><span data-stu-id="6cc52-132">Deploy the container image to your device</span></span>

<span data-ttu-id="6cc52-133">With the container image and the container registry credentials, you're ready to deploy the machine learning model to your IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="6cc52-133">With the container image and the container registry credentials, you're ready to deploy the machine learning model to your IoT Edge device.</span></span> 

<span data-ttu-id="6cc52-134">Follow the instructions in [Deploy IoT Edge modules from the Azure portal](../../iot-edge/how-to-deploy-modules-portal.md) to launch your model on your IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="6cc52-134">Follow the instructions in [Deploy IoT Edge modules from the Azure portal](../../iot-edge/how-to-deploy-modules-portal.md) to launch your model on your IoT Edge device.</span></span> 











