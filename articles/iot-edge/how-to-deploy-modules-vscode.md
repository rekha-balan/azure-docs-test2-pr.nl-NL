---
title: Deploy Azure IoT Edge modules (VS Code) | Microsoft Docs
description: Use Visual Studio Code to deploy modules to an IoT Edge device
author: kgremban
manager: timlt
ms.author: kgremban
ms.date: 06/26/2018
ms.topic: conceptual
ms.reviewer: ''
ms.service: iot-edge
services: iot-edge
ms.openlocfilehash: d5b43f81cbb3bbebb231a8a9738f6138b62ef7f6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864634"
---
# <a name="deploy-azure-iot-edge-modules-from-visual-studio-code"></a><span data-ttu-id="5da60-103">Deploy Azure IoT Edge modules from Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="5da60-103">Deploy Azure IoT Edge modules from Visual Studio Code</span></span>

<span data-ttu-id="5da60-104">Once you create IoT Edge modules with your business logic, you want to deploy them to your devices to operate at the edge.</span><span class="sxs-lookup"><span data-stu-id="5da60-104">Once you create IoT Edge modules with your business logic, you want to deploy them to your devices to operate at the edge.</span></span> <span data-ttu-id="5da60-105">If you have multiple modules that work together to collect and process data, you can deploy them all at once and declare the routing rules that connect them.</span><span class="sxs-lookup"><span data-stu-id="5da60-105">If you have multiple modules that work together to collect and process data, you can deploy them all at once and declare the routing rules that connect them.</span></span> 

<span data-ttu-id="5da60-106">This article shows how to create a JSON deployment manifest, then use that file to push the deployment to an IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="5da60-106">This article shows how to create a JSON deployment manifest, then use that file to push the deployment to an IoT Edge device.</span></span> <span data-ttu-id="5da60-107">For information about creating a deployment that targets multiple devices based on their shared tags, see [Deploy and monitor IoT Edge modules at scale](how-to-deploy-monitor.md)</span><span class="sxs-lookup"><span data-stu-id="5da60-107">For information about creating a deployment that targets multiple devices based on their shared tags, see [Deploy and monitor IoT Edge modules at scale](how-to-deploy-monitor.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5da60-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5da60-108">Prerequisites</span></span>

* <span data-ttu-id="5da60-109">An [IoT hub](../iot-hub/iot-hub-create-through-portal.md) in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="5da60-109">An [IoT hub](../iot-hub/iot-hub-create-through-portal.md) in your Azure subscription.</span></span> 
* <span data-ttu-id="5da60-110">An [IoT Edge device](how-to-register-device-portal.md) with the IoT Edge runtime installed.</span><span class="sxs-lookup"><span data-stu-id="5da60-110">An [IoT Edge device](how-to-register-device-portal.md) with the IoT Edge runtime installed.</span></span> 
* <span data-ttu-id="5da60-111">[Visual Studio Code](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="5da60-111">[Visual Studio Code](https://code.visualstudio.com/).</span></span>
* <span data-ttu-id="5da60-112">[Azure IoT Edge extension](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-edge) for Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="5da60-112">[Azure IoT Edge extension](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-edge) for Visual Studio Code.</span></span> 

## <a name="configure-a-deployment-manifest"></a><span data-ttu-id="5da60-113">Configure a deployment manifest</span><span class="sxs-lookup"><span data-stu-id="5da60-113">Configure a deployment manifest</span></span>

<span data-ttu-id="5da60-114">A deployment manifest is a JSON document that describes which modules to deploy, how data flows between the modules, and desired properties of the module twins.</span><span class="sxs-lookup"><span data-stu-id="5da60-114">A deployment manifest is a JSON document that describes which modules to deploy, how data flows between the modules, and desired properties of the module twins.</span></span> <span data-ttu-id="5da60-115">For more information about how deployment manifests work and how to create them, see [Understand how IoT Edge modules can be used, configured, and reused](module-composition.md).</span><span class="sxs-lookup"><span data-stu-id="5da60-115">For more information about how deployment manifests work and how to create them, see [Understand how IoT Edge modules can be used, configured, and reused](module-composition.md).</span></span>

<span data-ttu-id="5da60-116">To deploy modules using Visual Studio Code, save the deployment manifest locally as a .JSON file.</span><span class="sxs-lookup"><span data-stu-id="5da60-116">To deploy modules using Visual Studio Code, save the deployment manifest locally as a .JSON file.</span></span> <span data-ttu-id="5da60-117">You will use the file path in the next section when you run the command to apply the configuration to your device.</span><span class="sxs-lookup"><span data-stu-id="5da60-117">You will use the file path in the next section when you run the command to apply the configuration to your device.</span></span>

<span data-ttu-id="5da60-118">Here's a basic deployment manifest with one module as an example:</span><span class="sxs-lookup"><span data-stu-id="5da60-118">Here's a basic deployment manifest with one module as an example:</span></span>

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
   
## <a name="sign-in-to-access-your-iot-hub"></a><span data-ttu-id="5da60-119">Sign in to access your IoT hub</span><span class="sxs-lookup"><span data-stu-id="5da60-119">Sign in to access your IoT hub</span></span>

<span data-ttu-id="5da60-120">You can use the Azure IoT extensions for Visual Studio Code to perform operations with your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="5da60-120">You can use the Azure IoT extensions for Visual Studio Code to perform operations with your IoT hub.</span></span> <span data-ttu-id="5da60-121">For these operations to work, you need to sign in to your Azure account and select the IoT hub that you are working on.</span><span class="sxs-lookup"><span data-stu-id="5da60-121">For these operations to work, you need to sign in to your Azure account and select the IoT hub that you are working on.</span></span>

1. <span data-ttu-id="5da60-122">In Visual Studio Code, open the **Explorer** view.</span><span class="sxs-lookup"><span data-stu-id="5da60-122">In Visual Studio Code, open the **Explorer** view.</span></span>

2. <span data-ttu-id="5da60-123">At the bottom of the Explorer, expand the **Azure IoT Hub Devices** section.</span><span class="sxs-lookup"><span data-stu-id="5da60-123">At the bottom of the Explorer, expand the **Azure IoT Hub Devices** section.</span></span> 

   ![Expand Azure IoT Hub Devices](./media/how-to-deploy-modules-vscode/azure-iot-hub-devices.png)

3. <span data-ttu-id="5da60-125">Click on the **...** in the **Azure IoT Hub Devices** section header.</span><span class="sxs-lookup"><span data-stu-id="5da60-125">Click on the **...** in the **Azure IoT Hub Devices** section header.</span></span> <span data-ttu-id="5da60-126">If you don't see the ellipsis, hover over the header.</span><span class="sxs-lookup"><span data-stu-id="5da60-126">If you don't see the ellipsis, hover over the header.</span></span> 

4. <span data-ttu-id="5da60-127">Choose **Select IoT Hub**.</span><span class="sxs-lookup"><span data-stu-id="5da60-127">Choose **Select IoT Hub**.</span></span>

5. <span data-ttu-id="5da60-128">If you are not signed in to your Azure account, follow the prompts to do so.</span><span class="sxs-lookup"><span data-stu-id="5da60-128">If you are not signed in to your Azure account, follow the prompts to do so.</span></span> 

6. <span data-ttu-id="5da60-129">Select your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="5da60-129">Select your Azure subscription.</span></span> 

7. <span data-ttu-id="5da60-130">Select your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="5da60-130">Select your IoT hub.</span></span> 


## <a name="deploy-to-your-device"></a><span data-ttu-id="5da60-131">Deploy to your device</span><span class="sxs-lookup"><span data-stu-id="5da60-131">Deploy to your device</span></span>

<span data-ttu-id="5da60-132">You deploy modules to your device by applying the deployment manifest that you configured with the module information.</span><span class="sxs-lookup"><span data-stu-id="5da60-132">You deploy modules to your device by applying the deployment manifest that you configured with the module information.</span></span> 

1. <span data-ttu-id="5da60-133">In the Visual Studio Code explorer view, expand the **Azure IoT Hub Devices** section.</span><span class="sxs-lookup"><span data-stu-id="5da60-133">In the Visual Studio Code explorer view, expand the **Azure IoT Hub Devices** section.</span></span> 

2. <span data-ttu-id="5da60-134">Right-click on the device that you want to configure with the deployment manifest.</span><span class="sxs-lookup"><span data-stu-id="5da60-134">Right-click on the device that you want to configure with the deployment manifest.</span></span> 

3. <span data-ttu-id="5da60-135">Select **Create Deployment for Single Device**.</span><span class="sxs-lookup"><span data-stu-id="5da60-135">Select **Create Deployment for Single Device**.</span></span> 

4. <span data-ttu-id="5da60-136">Navigate to the deployment manifest JSON file that you want to use, and click **Select Edge Deployment Manifest**.</span><span class="sxs-lookup"><span data-stu-id="5da60-136">Navigate to the deployment manifest JSON file that you want to use, and click **Select Edge Deployment Manifest**.</span></span> 

   ![Select Edge Deployment Manifest](./media/how-to-deploy-modules-vscode/select-deployment-manifest.png)


<span data-ttu-id="5da60-138">The results of your deployment are printed in the VS Code output.</span><span class="sxs-lookup"><span data-stu-id="5da60-138">The results of your deployment are printed in the VS Code output.</span></span> <span data-ttu-id="5da60-139">Successful deployments are applied within a few minutes if the target device is running and connected to the internet.</span><span class="sxs-lookup"><span data-stu-id="5da60-139">Successful deployments are applied within a few minutes if the target device is running and connected to the internet.</span></span> 

## <a name="view-modules-on-your-device"></a><span data-ttu-id="5da60-140">View modules on your device</span><span class="sxs-lookup"><span data-stu-id="5da60-140">View modules on your device</span></span>

<span data-ttu-id="5da60-141">Once you've deployed modules to your device, you can view all of them in the **Azure IoT Hub Devices** section.</span><span class="sxs-lookup"><span data-stu-id="5da60-141">Once you've deployed modules to your device, you can view all of them in the **Azure IoT Hub Devices** section.</span></span> <span data-ttu-id="5da60-142">Select the arrow next to your IoT Edge device to expand it.</span><span class="sxs-lookup"><span data-stu-id="5da60-142">Select the arrow next to your IoT Edge device to expand it.</span></span> <span data-ttu-id="5da60-143">All the currently running modules are displayed.</span><span class="sxs-lookup"><span data-stu-id="5da60-143">All the currently running modules are displayed.</span></span> 

<span data-ttu-id="5da60-144">If you recently deployed new modules to a device, hover over the **Azure IoT Hub Devices** section header and select the refresh icon to update the view.</span><span class="sxs-lookup"><span data-stu-id="5da60-144">If you recently deployed new modules to a device, hover over the **Azure IoT Hub Devices** section header and select the refresh icon to update the view.</span></span> 

<span data-ttu-id="5da60-145">Right-click the name of a module to view and edit the module twin.</span><span class="sxs-lookup"><span data-stu-id="5da60-145">Right-click the name of a module to view and edit the module twin.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5da60-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="5da60-146">Next steps</span></span>

<span data-ttu-id="5da60-147">Learn how to [Deploy and monitor IoT Edge modules at scale](how-to-deploy-monitor.md)</span><span class="sxs-lookup"><span data-stu-id="5da60-147">Learn how to [Deploy and monitor IoT Edge modules at scale](how-to-deploy-monitor.md)</span></span>
