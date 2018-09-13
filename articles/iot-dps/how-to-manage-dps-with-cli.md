---
title: How to use Azure CLI and the IoT extension to manage the IoT Hub Device Provisioning Service | Microsoft Docs
description: Learn how to use Azure CLI and the IoT extension to manage the IoT Hub Device Provisioning Service
author: chrissie926
ms.author: menchi
ms.date: 01/17/2018
ms.topic: conceptual
ms.service: iot-dps
services: iot-dps
manager: briz
ms.openlocfilehash: 70ce30bdc5a12aec198a2bb1b78c9bdfa8a18882
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871362"
---
# <a name="how-to-use-azure-cli-and-the-iot-extension-to-manage-the-iot-hub-device-provisioning-service"></a><span data-ttu-id="a3f89-103">How to use Azure CLI and the IoT extension to manage the IoT Hub Device Provisioning Service</span><span class="sxs-lookup"><span data-stu-id="a3f89-103">How to use Azure CLI and the IoT extension to manage the IoT Hub Device Provisioning Service</span></span>

<span data-ttu-id="a3f89-104">[Azure CLI](https://docs.microsoft.com/cli/azure?view=azure-cli-latest) is an open-source cross platform command-line tool for managing Azure resources such as IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="a3f89-104">[Azure CLI](https://docs.microsoft.com/cli/azure?view=azure-cli-latest) is an open-source cross platform command-line tool for managing Azure resources such as IoT Edge.</span></span> <span data-ttu-id="a3f89-105">Azure CLI is available on Windows, Linux, and MacOS.</span><span class="sxs-lookup"><span data-stu-id="a3f89-105">Azure CLI is available on Windows, Linux, and MacOS.</span></span> <span data-ttu-id="a3f89-106">Azure CLI enables you to manage Azure IoT Hub resources, Device Provisioning service instances, and linked-hubs out of the box.</span><span class="sxs-lookup"><span data-stu-id="a3f89-106">Azure CLI enables you to manage Azure IoT Hub resources, Device Provisioning service instances, and linked-hubs out of the box.</span></span>

<span data-ttu-id="a3f89-107">The IoT extension enriches Azure CLI with features such as device management and full IoT Edge capability.</span><span class="sxs-lookup"><span data-stu-id="a3f89-107">The IoT extension enriches Azure CLI with features such as device management and full IoT Edge capability.</span></span>

<span data-ttu-id="a3f89-108">In this tutorial, you first complete the steps to setup Azure CLI and the IoT extension.</span><span class="sxs-lookup"><span data-stu-id="a3f89-108">In this tutorial, you first complete the steps to setup Azure CLI and the IoT extension.</span></span> <span data-ttu-id="a3f89-109">Then you learn how to run CLI commands to perform basic Device Provisioning Service operations.</span><span class="sxs-lookup"><span data-stu-id="a3f89-109">Then you learn how to run CLI commands to perform basic Device Provisioning Service operations.</span></span> 

## <a name="installation"></a><span data-ttu-id="a3f89-110">Installation</span><span class="sxs-lookup"><span data-stu-id="a3f89-110">Installation</span></span> 

### <a name="step-1---install-python"></a><span data-ttu-id="a3f89-111">Step 1 - Install Python</span><span class="sxs-lookup"><span data-stu-id="a3f89-111">Step 1 - Install Python</span></span>

<span data-ttu-id="a3f89-112">[Python 2.7x or Python 3.x](https://www.python.org/downloads/) is required.</span><span class="sxs-lookup"><span data-stu-id="a3f89-112">[Python 2.7x or Python 3.x](https://www.python.org/downloads/) is required.</span></span>

### <a name="step-2---install-azure-cli"></a><span data-ttu-id="a3f89-113">Step 2 - Install Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a3f89-113">Step 2 - Install Azure CLI</span></span>

<span data-ttu-id="a3f89-114">Follow the [installation instruction](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) to setup Azure CLI in your environment.</span><span class="sxs-lookup"><span data-stu-id="a3f89-114">Follow the [installation instruction](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) to setup Azure CLI in your environment.</span></span> <span data-ttu-id="a3f89-115">At a minimum, your Azure CLI version must be 2.0.24 or above.</span><span class="sxs-lookup"><span data-stu-id="a3f89-115">At a minimum, your Azure CLI version must be 2.0.24 or above.</span></span> <span data-ttu-id="a3f89-116">Use `az –version` to validate.</span><span class="sxs-lookup"><span data-stu-id="a3f89-116">Use `az –version` to validate.</span></span> <span data-ttu-id="a3f89-117">This version supports az extension commands and introduces the Knack command framework.</span><span class="sxs-lookup"><span data-stu-id="a3f89-117">This version supports az extension commands and introduces the Knack command framework.</span></span> <span data-ttu-id="a3f89-118">One simple way to install on Windows is to download and install the [MSI](https://aka.ms/InstallAzureCliWindows).</span><span class="sxs-lookup"><span data-stu-id="a3f89-118">One simple way to install on Windows is to download and install the [MSI](https://aka.ms/InstallAzureCliWindows).</span></span>

### <a name="step-3---install-iot-extension"></a><span data-ttu-id="a3f89-119">Step 3 - Install IoT extension</span><span class="sxs-lookup"><span data-stu-id="a3f89-119">Step 3 - Install IoT extension</span></span>

<span data-ttu-id="a3f89-120">[The IoT extension readme](https://github.com/Azure/azure-iot-cli-extension) describes several ways to install the extension.</span><span class="sxs-lookup"><span data-stu-id="a3f89-120">[The IoT extension readme](https://github.com/Azure/azure-iot-cli-extension) describes several ways to install the extension.</span></span> <span data-ttu-id="a3f89-121">The simplest way is to run `az extension add --name azure-cli-iot-ext`.</span><span class="sxs-lookup"><span data-stu-id="a3f89-121">The simplest way is to run `az extension add --name azure-cli-iot-ext`.</span></span> <span data-ttu-id="a3f89-122">After installation, you can use `az extension list` to validate the currently installed extensions or `az extension show --name azure-cli-iot-ext` to see details about the IoT extension.</span><span class="sxs-lookup"><span data-stu-id="a3f89-122">After installation, you can use `az extension list` to validate the currently installed extensions or `az extension show --name azure-cli-iot-ext` to see details about the IoT extension.</span></span> <span data-ttu-id="a3f89-123">To remove the extension, you can use `az extension remove --name azure-cli-iot-ext`.</span><span class="sxs-lookup"><span data-stu-id="a3f89-123">To remove the extension, you can use `az extension remove --name azure-cli-iot-ext`.</span></span>


## <a name="basic-device-provisioning-service-operations"></a><span data-ttu-id="a3f89-124">Basic Device Provisioning Service operations</span><span class="sxs-lookup"><span data-stu-id="a3f89-124">Basic Device Provisioning Service operations</span></span>
<span data-ttu-id="a3f89-125">The example shows you how to log in to your Azure account, create an Azure Resource Group (a container that holds related resources for an Azure solution), create an IoT Hub, create a Device Provisioning service, list the existing Device Provisioning services and create a linked IoT hub with CLI commands.</span><span class="sxs-lookup"><span data-stu-id="a3f89-125">The example shows you how to log in to your Azure account, create an Azure Resource Group (a container that holds related resources for an Azure solution), create an IoT Hub, create a Device Provisioning service, list the existing Device Provisioning services and create a linked IoT hub with CLI commands.</span></span> 

<span data-ttu-id="a3f89-126">Complete the installation steps described previously before you begin.</span><span class="sxs-lookup"><span data-stu-id="a3f89-126">Complete the installation steps described previously before you begin.</span></span> <span data-ttu-id="a3f89-127">If you don't have an Azure account yet, you can [create a free account](https://azure.microsoft.com/free/?v=17.39a) today.</span><span class="sxs-lookup"><span data-stu-id="a3f89-127">If you don't have an Azure account yet, you can [create a free account](https://azure.microsoft.com/free/?v=17.39a) today.</span></span> 


### <a name="1-log-in-to-the-azure-account"></a><span data-ttu-id="a3f89-128">1. Log in to the Azure account</span><span class="sxs-lookup"><span data-stu-id="a3f89-128">1. Log in to the Azure account</span></span>
  
    az login

![login][1]

### <a name="2-create-a-resource-group-iothubblogdemo-in-eastus"></a><span data-ttu-id="a3f89-130">2. Create a resource group IoTHubBlogDemo in eastus</span><span class="sxs-lookup"><span data-stu-id="a3f89-130">2. Create a resource group IoTHubBlogDemo in eastus</span></span>

    az group create -l eastus -n IoTHubBlogDemo

![Create resource group][2]


### <a name="3-create-two-device-provisioning-services"></a><span data-ttu-id="a3f89-132">3. Create two Device Provisioning services</span><span class="sxs-lookup"><span data-stu-id="a3f89-132">3. Create two Device Provisioning services</span></span>

    az iot dps create --resource-group IoTHubBlogDemo --name demodps

![Create Device Provisioning Service][3]

    az iot dps create --resource-group IoTHubBlogDemo --name demodps2

### <a name="4-list-all-the-existing-device-provisioning-services-under-this-resource-group"></a><span data-ttu-id="a3f89-134">4. List all the existing Device Provisioning services under this resource group</span><span class="sxs-lookup"><span data-stu-id="a3f89-134">4. List all the existing Device Provisioning services under this resource group</span></span>

    az iot dps list --resource-group IoTHubBlogDemo

![List Device Provisioning Services][4]


### <a name="5-create-an-iot-hub-blogdemohub-under-the-newly-created-resource-group"></a><span data-ttu-id="a3f89-136">5. Create an IoT Hub blogDemoHub under the newly created resource group</span><span class="sxs-lookup"><span data-stu-id="a3f89-136">5. Create an IoT Hub blogDemoHub under the newly created resource group</span></span>

    az iot hub create --name blogDemoHub --resource-group IoTHubBlogDemo

![Create IoT Hub][5]

### <a name="6-link-one-existing-iot-hub-to-a-device-provisioning-service"></a><span data-ttu-id="a3f89-138">6. Link one existing IoT Hub to a Device Provisioning service</span><span class="sxs-lookup"><span data-stu-id="a3f89-138">6. Link one existing IoT Hub to a Device Provisioning service</span></span>

    az iot dps linked-hub create --resource-group IoTHubBlogDemo --dps-name demodps --connection-string <connection string> -l westus

![Link Hub][5]

<!-- Images -->
[1]: ./media/how-to-manage-dps-with-cli/login.jpg
[2]: ./media/how-to-manage-dps-with-cli/create-resource-group.jpg
[3]: ./media/how-to-manage-dps-with-cli/create-dps.jpg
[4]: ./media/how-to-manage-dps-with-cli/list-dps.jpg
[5]: ./media/how-to-manage-dps-with-cli/create-hub.jpg
[6]: ./media/how-to-manage-dps-with-cli/link-hub.jpg


## <a name="next-steps"></a><span data-ttu-id="a3f89-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="a3f89-140">Next steps</span></span>
<span data-ttu-id="a3f89-141">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="a3f89-141">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a3f89-142">Enroll the device</span><span class="sxs-lookup"><span data-stu-id="a3f89-142">Enroll the device</span></span>
> * <span data-ttu-id="a3f89-143">Start the device</span><span class="sxs-lookup"><span data-stu-id="a3f89-143">Start the device</span></span>
> * <span data-ttu-id="a3f89-144">Verify the device is registered</span><span class="sxs-lookup"><span data-stu-id="a3f89-144">Verify the device is registered</span></span>

<span data-ttu-id="a3f89-145">Advance to the next tutorial to learn how to provision multiple devices across load-balanced hubs.</span><span class="sxs-lookup"><span data-stu-id="a3f89-145">Advance to the next tutorial to learn how to provision multiple devices across load-balanced hubs.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="a3f89-146">Provision devices across load-balanced IoT hubs</span><span class="sxs-lookup"><span data-stu-id="a3f89-146">Provision devices across load-balanced IoT hubs</span></span>](./tutorial-provision-multiple-hubs.md)
