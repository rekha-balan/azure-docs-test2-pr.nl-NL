---
title: Deploy Azure IoT Edge modules (CLI) | Microsoft Docs
description: Use the IoT extension for Azure CLI 2.0 to deploy modules to an IoT Edge device
author: kgremban
manager: timlt
ms.author: kgremban
ms.date: 07/27/2018
ms.topic: conceptual
ms.reviewer: menchi
ms.service: iot-edge
services: iot-edge
ms.openlocfilehash: 29c11139a2c773db2d26bf44984ad4dc72f2d870
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856725"
---
# <a name="deploy-azure-iot-edge-modules-with-azure-cli-20"></a><span data-ttu-id="a647c-103">Deploy Azure IoT Edge modules with Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a647c-103">Deploy Azure IoT Edge modules with Azure CLI 2.0</span></span>

<span data-ttu-id="a647c-104">Once you create IoT Edge modules with your business logic, you want to deploy them to your devices to operate at the edge.</span><span class="sxs-lookup"><span data-stu-id="a647c-104">Once you create IoT Edge modules with your business logic, you want to deploy them to your devices to operate at the edge.</span></span> <span data-ttu-id="a647c-105">If you have multiple modules that work together to collect and process data, you can deploy them all at once and declare the routing rules that connect them.</span><span class="sxs-lookup"><span data-stu-id="a647c-105">If you have multiple modules that work together to collect and process data, you can deploy them all at once and declare the routing rules that connect them.</span></span> 

<span data-ttu-id="a647c-106">[Azure CLI 2.0](https://docs.microsoft.com/cli/azure?view=azure-cli-latest) is an open-source cross platform command-line tool for managing Azure resources such as IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="a647c-106">[Azure CLI 2.0](https://docs.microsoft.com/cli/azure?view=azure-cli-latest) is an open-source cross platform command-line tool for managing Azure resources such as IoT Edge.</span></span> <span data-ttu-id="a647c-107">It enables you to manage Azure IoT Hub resources, device provisioning service instances, and linked-hubs out of the box.</span><span class="sxs-lookup"><span data-stu-id="a647c-107">It enables you to manage Azure IoT Hub resources, device provisioning service instances, and linked-hubs out of the box.</span></span> <span data-ttu-id="a647c-108">The new IoT extension enriches Azure CLI 2.0 with features such as device management and full IoT Edge capability.</span><span class="sxs-lookup"><span data-stu-id="a647c-108">The new IoT extension enriches Azure CLI 2.0 with features such as device management and full IoT Edge capability.</span></span>

<span data-ttu-id="a647c-109">This article shows how to create a JSON deployment manifest, then use that file to push the deployment to an IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="a647c-109">This article shows how to create a JSON deployment manifest, then use that file to push the deployment to an IoT Edge device.</span></span> <span data-ttu-id="a647c-110">For information about creating a deployment that targets multiple devices based on their shared tags, see [Deploy and monitor IoT Edge modules at scale](how-to-deploy-monitor-cli.md)</span><span class="sxs-lookup"><span data-stu-id="a647c-110">For information about creating a deployment that targets multiple devices based on their shared tags, see [Deploy and monitor IoT Edge modules at scale](how-to-deploy-monitor-cli.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a647c-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a647c-111">Prerequisites</span></span>

* <span data-ttu-id="a647c-112">An [IoT hub](../iot-hub/iot-hub-create-using-cli.md) in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="a647c-112">An [IoT hub](../iot-hub/iot-hub-create-using-cli.md) in your Azure subscription.</span></span> 
* <span data-ttu-id="a647c-113">An [IoT Edge device](how-to-register-device-cli.md) with the IoT Edge runtime installed.</span><span class="sxs-lookup"><span data-stu-id="a647c-113">An [IoT Edge device](how-to-register-device-cli.md) with the IoT Edge runtime installed.</span></span>
* <span data-ttu-id="a647c-114">[Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) in your environment.</span><span class="sxs-lookup"><span data-stu-id="a647c-114">[Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) in your environment.</span></span> <span data-ttu-id="a647c-115">At a minimum, your Azure CLI 2.0 version must be 2.0.24 or above.</span><span class="sxs-lookup"><span data-stu-id="a647c-115">At a minimum, your Azure CLI 2.0 version must be 2.0.24 or above.</span></span> <span data-ttu-id="a647c-116">Use `az –-version` to validate.</span><span class="sxs-lookup"><span data-stu-id="a647c-116">Use `az –-version` to validate.</span></span> <span data-ttu-id="a647c-117">This version supports az extension commands and introduces the Knack command framework.</span><span class="sxs-lookup"><span data-stu-id="a647c-117">This version supports az extension commands and introduces the Knack command framework.</span></span> 
* <span data-ttu-id="a647c-118">The [IoT extension for Azure CLI 2.0](https://github.com/Azure/azure-iot-cli-extension).</span><span class="sxs-lookup"><span data-stu-id="a647c-118">The [IoT extension for Azure CLI 2.0](https://github.com/Azure/azure-iot-cli-extension).</span></span>

## <a name="configure-a-deployment-manifest"></a><span data-ttu-id="a647c-119">Configure a deployment manifest</span><span class="sxs-lookup"><span data-stu-id="a647c-119">Configure a deployment manifest</span></span>

<span data-ttu-id="a647c-120">A deployment manifest is a JSON document that describes which modules to deploy, how data flows between the modules, and desired properties of the module twins.</span><span class="sxs-lookup"><span data-stu-id="a647c-120">A deployment manifest is a JSON document that describes which modules to deploy, how data flows between the modules, and desired properties of the module twins.</span></span> <span data-ttu-id="a647c-121">For more information about how deployment manifests work and how to create them, see [Understand how IoT Edge modules can be used, configured, and reused](module-composition.md).</span><span class="sxs-lookup"><span data-stu-id="a647c-121">For more information about how deployment manifests work and how to create them, see [Understand how IoT Edge modules can be used, configured, and reused](module-composition.md).</span></span>

<span data-ttu-id="a647c-122">To deploy modules using Azure CLI 2.0, save the deployment manifest locally as a .json file.</span><span class="sxs-lookup"><span data-stu-id="a647c-122">To deploy modules using Azure CLI 2.0, save the deployment manifest locally as a .json file.</span></span> <span data-ttu-id="a647c-123">You will use the file path in the next section when you run the command to apply the configuration to your device.</span><span class="sxs-lookup"><span data-stu-id="a647c-123">You will use the file path in the next section when you run the command to apply the configuration to your device.</span></span> 

<span data-ttu-id="a647c-124">Here's a basic deployment manifest with one module as an example:</span><span class="sxs-lookup"><span data-stu-id="a647c-124">Here's a basic deployment manifest with one module as an example:</span></span>

   ```json
   {
     "modulesContent": {
       "$edgeAgent": {
         "properties.desired": {
           "schemaVersion": "1.0",
           "runtime": {
             "type": "docker",
             "settings": {
               "minDockerVersion": "v1.25",
               "loggingOptions": "",
               "registryCredentials": {}
             }
           },
           "systemModules": {
             "edgeAgent": {
               "type": "docker",
               "settings": {
                 "image": "mcr.microsoft.com/azureiotedge-agent:1.0",
                 "createOptions": "{}"
               }
             },
             "edgeHub": {
               "type": "docker",
               "status": "running",
               "restartPolicy": "always",
               "settings": {
                 "image": "mcr.microsoft.com/azureiotedge-hub:1.0",
                 "createOptions": "{}"
               }
             }
           },
           "modules": {
             "tempSensor": {
               "version": "1.0",
               "type": "docker",
               "status": "running",
               "restartPolicy": "always",
               "settings": {
                 "image": "mcr.microsoft.com/azureiotedge-simulated-temperature-sensor:1.0",
                 "createOptions": "{}"
               }
             }
           }
         }
       },
       "$edgeHub": {
         "properties.desired": {
           "schemaVersion": "1.0",
           "routes": {
               "route": "FROM /* INTO $upstream"
           },
           "storeAndForwardConfiguration": {
             "timeToLiveSecs": 7200
           }
         }
       },
       "tempSensor": {
         "properties.desired": {}
       }
     }
   }
   ```

## <a name="deploy-to-your-device"></a><span data-ttu-id="a647c-125">Deploy to your device</span><span class="sxs-lookup"><span data-stu-id="a647c-125">Deploy to your device</span></span>

<span data-ttu-id="a647c-126">You deploy modules to your device by applying the deployment manifest that you configured with the module information.</span><span class="sxs-lookup"><span data-stu-id="a647c-126">You deploy modules to your device by applying the deployment manifest that you configured with the module information.</span></span> 

<span data-ttu-id="a647c-127">Change directories into the folder where your deployment manifest is saved.</span><span class="sxs-lookup"><span data-stu-id="a647c-127">Change directories into the folder where your deployment manifest is saved.</span></span> <span data-ttu-id="a647c-128">If you used one of the VS Code IoT Edge templates, use the `deployment.json` file in the **config** folder of your solution directory.</span><span class="sxs-lookup"><span data-stu-id="a647c-128">If you used one of the VS Code IoT Edge templates, use the `deployment.json` file in the **config** folder of your solution directory.</span></span> <span data-ttu-id="a647c-129">Don't use the `deployment.template.json` file.</span><span class="sxs-lookup"><span data-stu-id="a647c-129">Don't use the `deployment.template.json` file.</span></span> 

<span data-ttu-id="a647c-130">Use the following command to apply the configuration to an IoT Edge device:</span><span class="sxs-lookup"><span data-stu-id="a647c-130">Use the following command to apply the configuration to an IoT Edge device:</span></span>

   ```cli
   az iot hub apply-configuration --device-id [device id] --hub-name [hub name] --content [file path]
   ```

<span data-ttu-id="a647c-131">The device id parameter is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="a647c-131">The device id parameter is case-sensitive.</span></span> <span data-ttu-id="a647c-132">The content parameter points to the deployment manifest file that you saved.</span><span class="sxs-lookup"><span data-stu-id="a647c-132">The content parameter points to the deployment manifest file that you saved.</span></span> 

   ![Set modules](./media/how-to-deploy-cli/set-modules.png)

## <a name="view-modules-on-your-device"></a><span data-ttu-id="a647c-134">View modules on your device</span><span class="sxs-lookup"><span data-stu-id="a647c-134">View modules on your device</span></span>

<span data-ttu-id="a647c-135">Once you've deployed modules to your device, you can view all of them with the following command:</span><span class="sxs-lookup"><span data-stu-id="a647c-135">Once you've deployed modules to your device, you can view all of them with the following command:</span></span> 

<span data-ttu-id="a647c-136">View the modules on your IoT Edge device:</span><span class="sxs-lookup"><span data-stu-id="a647c-136">View the modules on your IoT Edge device:</span></span>
    
   ```cli
   az iot hub module-identity list --device-id [device id] --hub-name [hub name]
   ```

<span data-ttu-id="a647c-137">The device id parameter is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="a647c-137">The device id parameter is case-sensitive.</span></span>

   ![List modules](./media/how-to-deploy-cli/list-modules.png)

## <a name="next-steps"></a><span data-ttu-id="a647c-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="a647c-139">Next steps</span></span>

<span data-ttu-id="a647c-140">Learn how to [Deploy and monitor IoT Edge modules at scale](how-to-deploy-monitor.md)</span><span class="sxs-lookup"><span data-stu-id="a647c-140">Learn how to [Deploy and monitor IoT Edge modules at scale](how-to-deploy-monitor.md)</span></span>