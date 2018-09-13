---
title: Deploy Modbus on Azure IoT Edge | Microsoft Docs
description: Allow devices that use Modbus TCP to communicate with Azure IoT Hub by creating an IoT Edge gateway device
author: kgremban
manager: timlt
ms.service: iot-edge
services: iot-edge
ms.topic: conceptual
ms.date: 06/07/2018
ms.author: kgremban
ms.openlocfilehash: b5316479011a432f3822448f03b8ad6ecddd4fe1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965812"
---
# <a name="connect-modbus-tcp-devices-through-an-iot-edge-device-gateway"></a><span data-ttu-id="f11b1-103">Connect Modbus TCP devices through an IoT Edge device gateway</span><span class="sxs-lookup"><span data-stu-id="f11b1-103">Connect Modbus TCP devices through an IoT Edge device gateway</span></span>

<span data-ttu-id="f11b1-104">If you want to connect IoT devices that use Modbus TCP or RTU protocols to an Azure IoT hub, use an IoT Edge device as a gateway.</span><span class="sxs-lookup"><span data-stu-id="f11b1-104">If you want to connect IoT devices that use Modbus TCP or RTU protocols to an Azure IoT hub, use an IoT Edge device as a gateway.</span></span> <span data-ttu-id="f11b1-105">The gateway device reads data from your Modbus devices, then communicates that data to the cloud using a supported protocol.</span><span class="sxs-lookup"><span data-stu-id="f11b1-105">The gateway device reads data from your Modbus devices, then communicates that data to the cloud using a supported protocol.</span></span> 

![Modbus devices connect to IoT Hub through Edge gateway](./media/deploy-modbus-gateway/diagram.png)

<span data-ttu-id="f11b1-107">This article covers how to create your own container image for a Modbus module (or you can use a prebuilt sample) and then deploy it to the IoT Edge device that will act as your gateway.</span><span class="sxs-lookup"><span data-stu-id="f11b1-107">This article covers how to create your own container image for a Modbus module (or you can use a prebuilt sample) and then deploy it to the IoT Edge device that will act as your gateway.</span></span> 

<span data-ttu-id="f11b1-108">This article assumes that you're using Modbus TCP protocol.</span><span class="sxs-lookup"><span data-stu-id="f11b1-108">This article assumes that you're using Modbus TCP protocol.</span></span> <span data-ttu-id="f11b1-109">For more information about how to configure the module to support Modbus RTU, refer to the [Azure IoT Edge Modbus module](https://github.com/Azure/iot-edge-modbus) project on Github.</span><span class="sxs-lookup"><span data-stu-id="f11b1-109">For more information about how to configure the module to support Modbus RTU, refer to the [Azure IoT Edge Modbus module](https://github.com/Azure/iot-edge-modbus) project on Github.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f11b1-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f11b1-110">Prerequisites</span></span>
* <span data-ttu-id="f11b1-111">An Azure IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="f11b1-111">An Azure IoT Edge device.</span></span> <span data-ttu-id="f11b1-112">For a walkthrough on how to set up one, see [Deploy Azure IoT Edge on a simulated device in Windows](quickstart.md) or [Linux](quickstart-linux.md).</span><span class="sxs-lookup"><span data-stu-id="f11b1-112">For a walkthrough on how to set up one, see [Deploy Azure IoT Edge on a simulated device in Windows](quickstart.md) or [Linux](quickstart-linux.md).</span></span> 
* <span data-ttu-id="f11b1-113">The primary key connection string for the IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="f11b1-113">The primary key connection string for the IoT Edge device.</span></span>
* <span data-ttu-id="f11b1-114">A physical or simulated Modbus device that supports Modbus TCP.</span><span class="sxs-lookup"><span data-stu-id="f11b1-114">A physical or simulated Modbus device that supports Modbus TCP.</span></span>

## <a name="prepare-a-modbus-container"></a><span data-ttu-id="f11b1-115">Prepare a Modbus container</span><span class="sxs-lookup"><span data-stu-id="f11b1-115">Prepare a Modbus container</span></span>

<span data-ttu-id="f11b1-116">If you want to test the Modbus gateway functionality, Microsoft has a sample module that you can use.</span><span class="sxs-lookup"><span data-stu-id="f11b1-116">If you want to test the Modbus gateway functionality, Microsoft has a sample module that you can use.</span></span> <span data-ttu-id="f11b1-117">To use the sample module, go to the [Run the solution](#run-the-solution) section and enter the following as the Image URI:</span><span class="sxs-lookup"><span data-stu-id="f11b1-117">To use the sample module, go to the [Run the solution](#run-the-solution) section and enter the following as the Image URI:</span></span> 

```URL
mcr.microsoft.com/azureiotedge/modbus:1.0
```

<span data-ttu-id="f11b1-118">If you want to create your own module and customize it for your environment, there is an open source [Azure IoT Edge Modbus module](https://github.com/Azure/iot-edge-modbus) project on Github.</span><span class="sxs-lookup"><span data-stu-id="f11b1-118">If you want to create your own module and customize it for your environment, there is an open source [Azure IoT Edge Modbus module](https://github.com/Azure/iot-edge-modbus) project on Github.</span></span> <span data-ttu-id="f11b1-119">Follow the guidance in that project to create your own container image.</span><span class="sxs-lookup"><span data-stu-id="f11b1-119">Follow the guidance in that project to create your own container image.</span></span> <span data-ttu-id="f11b1-120">If you create your own container image, refer to [Develop and deploy a C# IoT Edge module](tutorial-csharp-module.md) for instructions on publishing container images to a registry, and deploying a custom module to your device.</span><span class="sxs-lookup"><span data-stu-id="f11b1-120">If you create your own container image, refer to [Develop and deploy a C# IoT Edge module](tutorial-csharp-module.md) for instructions on publishing container images to a registry, and deploying a custom module to your device.</span></span> 


## <a name="run-the-solution"></a><span data-ttu-id="f11b1-121">Run the solution</span><span class="sxs-lookup"><span data-stu-id="f11b1-121">Run the solution</span></span>
1. <span data-ttu-id="f11b1-122">On the [Azure portal](https://portal.azure.com/), go to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="f11b1-122">On the [Azure portal](https://portal.azure.com/), go to your IoT hub.</span></span>
2. <span data-ttu-id="f11b1-123">Go to **IoT Edge** and click on your IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="f11b1-123">Go to **IoT Edge** and click on your IoT Edge device.</span></span>
3. <span data-ttu-id="f11b1-124">Select **Set modules**.</span><span class="sxs-lookup"><span data-stu-id="f11b1-124">Select **Set modules**.</span></span>
4. <span data-ttu-id="f11b1-125">Add the Modbus module:</span><span class="sxs-lookup"><span data-stu-id="f11b1-125">Add the Modbus module:</span></span>
   1. <span data-ttu-id="f11b1-126">Click **Add** and select **IoT Edge module**.</span><span class="sxs-lookup"><span data-stu-id="f11b1-126">Click **Add** and select **IoT Edge module**.</span></span>
   2. <span data-ttu-id="f11b1-127">In the **Name** field, enter "modbus".</span><span class="sxs-lookup"><span data-stu-id="f11b1-127">In the **Name** field, enter "modbus".</span></span>
   3. <span data-ttu-id="f11b1-128">In the **Image** field, enter the image URI of the sample container: `mcr.microsoft.com/azureiotedge/modbus:1.0`.</span><span class="sxs-lookup"><span data-stu-id="f11b1-128">In the **Image** field, enter the image URI of the sample container: `mcr.microsoft.com/azureiotedge/modbus:1.0`.</span></span>
   4. <span data-ttu-id="f11b1-129">Check the **Enable** box to update the module twin's desired properties.</span><span class="sxs-lookup"><span data-stu-id="f11b1-129">Check the **Enable** box to update the module twin's desired properties.</span></span>
   5. <span data-ttu-id="f11b1-130">Copy the following JSON into the text box.</span><span class="sxs-lookup"><span data-stu-id="f11b1-130">Copy the following JSON into the text box.</span></span> <span data-ttu-id="f11b1-131">Change the value of **SlaveConnection** to the IPv4 address of your Modbus device.</span><span class="sxs-lookup"><span data-stu-id="f11b1-131">Change the value of **SlaveConnection** to the IPv4 address of your Modbus device.</span></span>

      ```JSON
      {  
        "properties.desired":{  
          "PublishInterval":"2000",
          "SlaveConfigs":{  
            "Slave01":{  
              "SlaveConnection":"<IPV4 address>",
              "HwId":"PowerMeter-0a:01:01:01:01:01",
              "Operations":{  
                "Op01":{  
                  "PollingInterval": "1000",
                  "UnitId":"1",
                  "StartAddress":"400001",
                  "Count":"2",
                  "DisplayName":"Voltage"
                }
              }
            }
          }
        }
      }
      ```

   6. <span data-ttu-id="f11b1-132">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="f11b1-132">Select **Save**.</span></span>
5. <span data-ttu-id="f11b1-133">Back in the **Add Modules** step, select **Next**.</span><span class="sxs-lookup"><span data-stu-id="f11b1-133">Back in the **Add Modules** step, select **Next**.</span></span>
7. <span data-ttu-id="f11b1-134">In the **Specify Routes** step, copy the following JSON into the text box.</span><span class="sxs-lookup"><span data-stu-id="f11b1-134">In the **Specify Routes** step, copy the following JSON into the text box.</span></span> <span data-ttu-id="f11b1-135">This route sends all messages collected by the Modbus module to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f11b1-135">This route sends all messages collected by the Modbus module to IoT Hub.</span></span> <span data-ttu-id="f11b1-136">In this route, ''modbusOutput'' is the endpoint that Modbus module use to output data, and ''upstream'' is a special destination that tells Edge Hub to send messages to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f11b1-136">In this route, ''modbusOutput'' is the endpoint that Modbus module use to output data, and ''upstream'' is a special destination that tells Edge Hub to send messages to IoT Hub.</span></span> 
   ```JSON
   {
    "routes": {
      "modbusToIoTHub":"FROM /messages/modules/modbus/outputs/modbusOutput INTO $upstream"
    }
   }
   ```

8. <span data-ttu-id="f11b1-137">Select **Next**.</span><span class="sxs-lookup"><span data-stu-id="f11b1-137">Select **Next**.</span></span> 
9. <span data-ttu-id="f11b1-138">In the **Review Deployment** step, select **Submit**.</span><span class="sxs-lookup"><span data-stu-id="f11b1-138">In the **Review Deployment** step, select **Submit**.</span></span> 
10. <span data-ttu-id="f11b1-139">Return to the device details page and select **Refresh**.</span><span class="sxs-lookup"><span data-stu-id="f11b1-139">Return to the device details page and select **Refresh**.</span></span> <span data-ttu-id="f11b1-140">You should see the new **modbus** module running along with the IoT Edge runtime.</span><span class="sxs-lookup"><span data-stu-id="f11b1-140">You should see the new **modbus** module running along with the IoT Edge runtime.</span></span>

## <a name="view-data"></a><span data-ttu-id="f11b1-141">View data</span><span class="sxs-lookup"><span data-stu-id="f11b1-141">View data</span></span>
<span data-ttu-id="f11b1-142">View the data coming through the modbus module:</span><span class="sxs-lookup"><span data-stu-id="f11b1-142">View the data coming through the modbus module:</span></span>
```cmd/sh
docker logs -f modbus
```

<span data-ttu-id="f11b1-143">You can also view the telemetry the device is sending by using the [Azure IoT Toolkit extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-toolkit).</span><span class="sxs-lookup"><span data-stu-id="f11b1-143">You can also view the telemetry the device is sending by using the [Azure IoT Toolkit extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-toolkit).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f11b1-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="f11b1-144">Next steps</span></span>

- <span data-ttu-id="f11b1-145">To learn more about how IoT Edge devices can act as gateways, see [Create an IoT Edge device that acts as a transparent gateway][lnk-transparent-gateway-linux]</span><span class="sxs-lookup"><span data-stu-id="f11b1-145">To learn more about how IoT Edge devices can act as gateways, see [Create an IoT Edge device that acts as a transparent gateway][lnk-transparent-gateway-linux]</span></span>
- <span data-ttu-id="f11b1-146">For more information about how IoT Edge modules work, see [Understand Azure IoT Edge modules](iot-edge-modules.md)</span><span class="sxs-lookup"><span data-stu-id="f11b1-146">For more information about how IoT Edge modules work, see [Understand Azure IoT Edge modules](iot-edge-modules.md)</span></span>

<!-- Links -->
[lnk-transparent-gateway-linux]: ./how-to-create-transparent-gateway-linux.md
