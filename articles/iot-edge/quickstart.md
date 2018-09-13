---
title: Quickstart Azure IoT Edge + Windows | Microsoft Docs
description: Try out Azure IoT Edge by running analytics on a simulated edge device
author: kgremban
manager: timlt
ms.author: kgremban
ms.date: 08/02/2018
ms.topic: quickstart
ms.service: iot-edge
services: iot-edge
ms.custom: mvc
ms.openlocfilehash: 3b54a326fc648a443897a6e39c823d9c097cf1d3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869061"
---
# <a name="quickstart-deploy-your-first-iot-edge-module-from-the-azure-portal-to-a-windows-device---preview"></a><span data-ttu-id="3fbfc-103">Quickstart: Deploy your first IoT Edge module from the Azure portal to a Windows device - preview</span><span class="sxs-lookup"><span data-stu-id="3fbfc-103">Quickstart: Deploy your first IoT Edge module from the Azure portal to a Windows device - preview</span></span>

<span data-ttu-id="3fbfc-104">In this quickstart, use the Azure IoT Edge cloud interface to deploy prebuilt code remotely to an IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-104">In this quickstart, use the Azure IoT Edge cloud interface to deploy prebuilt code remotely to an IoT Edge device.</span></span> <span data-ttu-id="3fbfc-105">To accomplish this task, first use your Windows device to simulate an IoT Edge device, then you can deploy a module to it.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-105">To accomplish this task, first use your Windows device to simulate an IoT Edge device, then you can deploy a module to it.</span></span>

<span data-ttu-id="3fbfc-106">In this quickstart you learn how to:</span><span class="sxs-lookup"><span data-stu-id="3fbfc-106">In this quickstart you learn how to:</span></span>

1. <span data-ttu-id="3fbfc-107">Create an IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-107">Create an IoT Hub.</span></span>
2. <span data-ttu-id="3fbfc-108">Register an IoT Edge device to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-108">Register an IoT Edge device to your IoT hub.</span></span>
3. <span data-ttu-id="3fbfc-109">Install and start the IoT Edge runtime on your device.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-109">Install and start the IoT Edge runtime on your device.</span></span>
4. <span data-ttu-id="3fbfc-110">Remotely deploy a module to an IoT Edge device and send telemetry to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-110">Remotely deploy a module to an IoT Edge device and send telemetry to IoT Hub.</span></span>

![Tutorial architecture][2]

<span data-ttu-id="3fbfc-112">The module that you deploy in this quickstart is a simulated sensor that generates temperature, humidity, and pressure data.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-112">The module that you deploy in this quickstart is a simulated sensor that generates temperature, humidity, and pressure data.</span></span> <span data-ttu-id="3fbfc-113">The other Azure IoT Edge tutorials build upon the work you do here by deploying modules that analyze the simulated data for business insights.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-113">The other Azure IoT Edge tutorials build upon the work you do here by deploying modules that analyze the simulated data for business insights.</span></span> 

>[!NOTE]
><span data-ttu-id="3fbfc-114">The IoT Edge runtime on Windows is in [public preview](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span><span class="sxs-lookup"><span data-stu-id="3fbfc-114">The IoT Edge runtime on Windows is in [public preview](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span></span>

<span data-ttu-id="3fbfc-115">If you don't have an active Azure subscription, create a [free account][lnk-account] before you begin.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-115">If you don't have an active Azure subscription, create a [free account][lnk-account] before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="3fbfc-116">You use the Azure CLI to complete many of the steps in this quickstart, and Azure IoT has an extension to enable additional functionality.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-116">You use the Azure CLI to complete many of the steps in this quickstart, and Azure IoT has an extension to enable additional functionality.</span></span> 

<span data-ttu-id="3fbfc-117">Add the Azure IoT extension to the cloud shell instance.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-117">Add the Azure IoT extension to the cloud shell instance.</span></span>

   ```azurecli-interactive
   az extension add --name azure-cli-iot-ext
   ```

## <a name="prerequisites"></a><span data-ttu-id="3fbfc-118">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3fbfc-118">Prerequisites</span></span>

<span data-ttu-id="3fbfc-119">Cloud resources:</span><span class="sxs-lookup"><span data-stu-id="3fbfc-119">Cloud resources:</span></span> 

* <span data-ttu-id="3fbfc-120">A resource group to manage all the resources you use in this quickstart.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-120">A resource group to manage all the resources you use in this quickstart.</span></span> 

   ```azurecli-interactive
   az group create --name IoTEdgeResources --location westus
   ```

<span data-ttu-id="3fbfc-121">IoT Edge device:</span><span class="sxs-lookup"><span data-stu-id="3fbfc-121">IoT Edge device:</span></span> 

* <span data-ttu-id="3fbfc-122">A Windows computer or virtual machine to act as your IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-122">A Windows computer or virtual machine to act as your IoT Edge device.</span></span> <span data-ttu-id="3fbfc-123">Use a supported Windows version:</span><span class="sxs-lookup"><span data-stu-id="3fbfc-123">Use a supported Windows version:</span></span>
   * <span data-ttu-id="3fbfc-124">Windows 10 or newer</span><span class="sxs-lookup"><span data-stu-id="3fbfc-124">Windows 10 or newer</span></span>
   * <span data-ttu-id="3fbfc-125">Windows Server 2016 or newer</span><span class="sxs-lookup"><span data-stu-id="3fbfc-125">Windows Server 2016 or newer</span></span>
* <span data-ttu-id="3fbfc-126">If it's a virtual machine, enable [nested virtualization][lnk-nested] and allocate at least 2GB memory.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-126">If it's a virtual machine, enable [nested virtualization][lnk-nested] and allocate at least 2GB memory.</span></span> 
* <span data-ttu-id="3fbfc-127">Install [Docker for Windows][lnk-docker] and make sure it's running.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-127">Install [Docker for Windows][lnk-docker] and make sure it's running.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="3fbfc-128">Create an IoT hub</span><span class="sxs-lookup"><span data-stu-id="3fbfc-128">Create an IoT hub</span></span>

<span data-ttu-id="3fbfc-129">Start the quickstart by creating your IoT hub with Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-129">Start the quickstart by creating your IoT hub with Azure CLI.</span></span> 

![Create IoT Hub][3]

<span data-ttu-id="3fbfc-131">The free level of IoT Hub works for this quickstart.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-131">The free level of IoT Hub works for this quickstart.</span></span> <span data-ttu-id="3fbfc-132">If you've used IoT Hub in the past and already have a free hub created, you can use that IoT hub.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-132">If you've used IoT Hub in the past and already have a free hub created, you can use that IoT hub.</span></span> <span data-ttu-id="3fbfc-133">Each subscription can only have one free IoT hub.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-133">Each subscription can only have one free IoT hub.</span></span> 

<span data-ttu-id="3fbfc-134">The following code creates a free **F1** hub in the resource group **IoTEdgeResources**.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-134">The following code creates a free **F1** hub in the resource group **IoTEdgeResources**.</span></span> <span data-ttu-id="3fbfc-135">Replace *{hub_name}* with a unique name for your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-135">Replace *{hub_name}* with a unique name for your IoT hub.</span></span>

   ```azurecli-interactive
   az iot hub create --resource-group IoTEdgeResources --name {hub_name} --sku F1 
   ```

   <span data-ttu-id="3fbfc-136">If you get an error because there's already one free hub in your subscription, change the SKU to **S1**.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-136">If you get an error because there's already one free hub in your subscription, change the SKU to **S1**.</span></span> 

## <a name="register-an-iot-edge-device"></a><span data-ttu-id="3fbfc-137">Register an IoT Edge device</span><span class="sxs-lookup"><span data-stu-id="3fbfc-137">Register an IoT Edge device</span></span>

<span data-ttu-id="3fbfc-138">Register an IoT Edge device with your newly created IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-138">Register an IoT Edge device with your newly created IoT Hub.</span></span>
<span data-ttu-id="3fbfc-139">![Register a device][4]</span><span class="sxs-lookup"><span data-stu-id="3fbfc-139">![Register a device][4]</span></span>

<span data-ttu-id="3fbfc-140">Create a device identity for your simulated device so that it can communicate with your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-140">Create a device identity for your simulated device so that it can communicate with your IoT hub.</span></span> <span data-ttu-id="3fbfc-141">The device identity lives in the cloud, and you use a unique device connection string to associate a physical device to a device identity.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-141">The device identity lives in the cloud, and you use a unique device connection string to associate a physical device to a device identity.</span></span> 

<span data-ttu-id="3fbfc-142">Since IoT Edge devices behave and can be managed differently than typical IoT devices, you declare this to be an IoT Edge device from the beginning.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-142">Since IoT Edge devices behave and can be managed differently than typical IoT devices, you declare this to be an IoT Edge device from the beginning.</span></span> 

1. <span data-ttu-id="3fbfc-143">In the Azure cloud shell, enter the following command to create a device named **myEdgeDevice** in your hub.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-143">In the Azure cloud shell, enter the following command to create a device named **myEdgeDevice** in your hub.</span></span>

   ```azurecli-interactive
   az iot hub device-identity create --device-id myEdgeDevice --hub-name {hub_name} --edge-enabled
   ```

1. <span data-ttu-id="3fbfc-144">Retrieve the connection string for your device, which links your physical device with its identity in IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-144">Retrieve the connection string for your device, which links your physical device with its identity in IoT Hub.</span></span> 

   ```azurecli-interactive
   az iot hub device-identity show-connection-string --device-id myEdgeDevice --hub-name {hub_name}
   ```

1. <span data-ttu-id="3fbfc-145">Copy the connection string and save it.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-145">Copy the connection string and save it.</span></span> <span data-ttu-id="3fbfc-146">You'll use this value to configure the IoT Edge runtime in the next section.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-146">You'll use this value to configure the IoT Edge runtime in the next section.</span></span> 

## <a name="install-and-start-the-iot-edge-runtime"></a><span data-ttu-id="3fbfc-147">Install and start the IoT Edge runtime</span><span class="sxs-lookup"><span data-stu-id="3fbfc-147">Install and start the IoT Edge runtime</span></span>

<span data-ttu-id="3fbfc-148">Install the Azure IoT Edge runtime on your IoT Edge device and configure it with a device connection string.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-148">Install the Azure IoT Edge runtime on your IoT Edge device and configure it with a device connection string.</span></span> 
<span data-ttu-id="3fbfc-149">![Register a device][5]</span><span class="sxs-lookup"><span data-stu-id="3fbfc-149">![Register a device][5]</span></span>

<span data-ttu-id="3fbfc-150">The IoT Edge runtime is deployed on all IoT Edge devices.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-150">The IoT Edge runtime is deployed on all IoT Edge devices.</span></span> <span data-ttu-id="3fbfc-151">It has three components.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-151">It has three components.</span></span> <span data-ttu-id="3fbfc-152">The **IoT Edge security daemon** starts each time an Edge device boots and bootstraps the device by starting the IoT Edge agent.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-152">The **IoT Edge security daemon** starts each time an Edge device boots and bootstraps the device by starting the IoT Edge agent.</span></span> <span data-ttu-id="3fbfc-153">The **IoT Edge agent** facilitates deployment and monitoring of modules on the IoT Edge device, including the IoT Edge hub.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-153">The **IoT Edge agent** facilitates deployment and monitoring of modules on the IoT Edge device, including the IoT Edge hub.</span></span> <span data-ttu-id="3fbfc-154">The **IoT Edge hub** manages communications between modules on the IoT Edge device, and between the device and IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-154">The **IoT Edge hub** manages communications between modules on the IoT Edge device, and between the device and IoT Hub.</span></span> 

<span data-ttu-id="3fbfc-155">During the runtime installation, you're asked for a device connection string.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-155">During the runtime installation, you're asked for a device connection string.</span></span> <span data-ttu-id="3fbfc-156">Use the string that you retrieved from the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-156">Use the string that you retrieved from the Azure CLI.</span></span> <span data-ttu-id="3fbfc-157">This string associates your physical device with the IoT Edge device identity in Azure.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-157">This string associates your physical device with the IoT Edge device identity in Azure.</span></span> 

<span data-ttu-id="3fbfc-158">The instructions in this section configure the IoT Edge runtime with Linux containers.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-158">The instructions in this section configure the IoT Edge runtime with Linux containers.</span></span> <span data-ttu-id="3fbfc-159">If you want to use Windows containers, see [Install Azure IoT Edge runtime on Windows to use with Windows containers](how-to-install-iot-edge-windows-with-windows.md).</span><span class="sxs-lookup"><span data-stu-id="3fbfc-159">If you want to use Windows containers, see [Install Azure IoT Edge runtime on Windows to use with Windows containers](how-to-install-iot-edge-windows-with-windows.md).</span></span>

<span data-ttu-id="3fbfc-160">Complete the following steps in the Windows machine or VM that you prepared to function as an IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-160">Complete the following steps in the Windows machine or VM that you prepared to function as an IoT Edge device.</span></span> 

### <a name="download-and-install-the-iot-edge-service"></a><span data-ttu-id="3fbfc-161">Download and install the IoT Edge service</span><span class="sxs-lookup"><span data-stu-id="3fbfc-161">Download and install the IoT Edge service</span></span>

<span data-ttu-id="3fbfc-162">Use PowerShell to download and install the IoT Edge runtime.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-162">Use PowerShell to download and install the IoT Edge runtime.</span></span> <span data-ttu-id="3fbfc-163">Use the device connection string that you retrieved from IoT Hub to configure your device.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-163">Use the device connection string that you retrieved from IoT Hub to configure your device.</span></span> 

1. <span data-ttu-id="3fbfc-164">On your IoT Edge device, run PowerShell as an administrator.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-164">On your IoT Edge device, run PowerShell as an administrator.</span></span>

2. <span data-ttu-id="3fbfc-165">Download and install the IoT Edge service on your device.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-165">Download and install the IoT Edge service on your device.</span></span> 

   ```powershell
   . {Invoke-WebRequest -useb aka.ms/iotedge-win} | Invoke-Expression; `
   Install-SecurityDaemon -Manual -ContainerOs Linux
   ```

3. <span data-ttu-id="3fbfc-166">When prompted for a **DeviceConnectionString**, provide the string that you copied in the previous section.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-166">When prompted for a **DeviceConnectionString**, provide the string that you copied in the previous section.</span></span> <span data-ttu-id="3fbfc-167">Don't include quotes around the connection string.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-167">Don't include quotes around the connection string.</span></span> 

### <a name="view-the-iot-edge-runtime-status"></a><span data-ttu-id="3fbfc-168">View the IoT Edge runtime status</span><span class="sxs-lookup"><span data-stu-id="3fbfc-168">View the IoT Edge runtime status</span></span>

<span data-ttu-id="3fbfc-169">Verify that the runtime was successfully installed and configured.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-169">Verify that the runtime was successfully installed and configured.</span></span>

1. <span data-ttu-id="3fbfc-170">Check the status of the IoT Edge service.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-170">Check the status of the IoT Edge service.</span></span>

   ```powershell
   Get-Service iotedge
   ```

2. <span data-ttu-id="3fbfc-171">If you need to troubleshoot the service, retrieve the service logs.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-171">If you need to troubleshoot the service, retrieve the service logs.</span></span> 

   ```powershell
   # Displays logs from today, newest at the bottom.

   Get-WinEvent -ea SilentlyContinue `
    -FilterHashtable @{ProviderName= "iotedged";
      LogName = "application"; StartTime = [datetime]::Today} |
    select TimeCreated, Message |
    sort-object @{Expression="TimeCreated";Descending=$false} |
    format-table -autosize -wrap
   ```

3. <span data-ttu-id="3fbfc-172">View all the modules running on your IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-172">View all the modules running on your IoT Edge device.</span></span> <span data-ttu-id="3fbfc-173">Since the service just started for the first time, you should only see the **edgeAgent** module running.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-173">Since the service just started for the first time, you should only see the **edgeAgent** module running.</span></span> <span data-ttu-id="3fbfc-174">The edgeAgent module runs by default, and helps to install and start any additional modules that you deploy to your device.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-174">The edgeAgent module runs by default, and helps to install and start any additional modules that you deploy to your device.</span></span> 

   ```powershell
   iotedge list
   ```

   ![View one module on your device](./media/quickstart/iotedge-list-1.png)

<span data-ttu-id="3fbfc-176">Your IoT Edge device is now configured.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-176">Your IoT Edge device is now configured.</span></span> <span data-ttu-id="3fbfc-177">It's ready to run cloud-deployed modules.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-177">It's ready to run cloud-deployed modules.</span></span> 

## <a name="deploy-a-module"></a><span data-ttu-id="3fbfc-178">Deploy a module</span><span class="sxs-lookup"><span data-stu-id="3fbfc-178">Deploy a module</span></span>

<span data-ttu-id="3fbfc-179">Manage your Azure IoT Edge device from the cloud to deploy a module that will send telemetry data to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-179">Manage your Azure IoT Edge device from the cloud to deploy a module that will send telemetry data to IoT Hub.</span></span>
<span data-ttu-id="3fbfc-180">![Register a device][6]</span><span class="sxs-lookup"><span data-stu-id="3fbfc-180">![Register a device][6]</span></span>

[!INCLUDE [iot-edge-deploy-module](../../includes/iot-edge-deploy-module.md)]

## <a name="view-generated-data"></a><span data-ttu-id="3fbfc-181">View generated data</span><span class="sxs-lookup"><span data-stu-id="3fbfc-181">View generated data</span></span>

<span data-ttu-id="3fbfc-182">In this quickstart, you created a new IoT Edge device and installed the IoT Edge runtime on it.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-182">In this quickstart, you created a new IoT Edge device and installed the IoT Edge runtime on it.</span></span> <span data-ttu-id="3fbfc-183">Then, you used the Azure portal to push an IoT Edge module to run on the device without having to make changes to the device itself.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-183">Then, you used the Azure portal to push an IoT Edge module to run on the device without having to make changes to the device itself.</span></span> <span data-ttu-id="3fbfc-184">In this case, the module that you pushed creates environmental data that you can use for the tutorials.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-184">In this case, the module that you pushed creates environmental data that you can use for the tutorials.</span></span> 

<span data-ttu-id="3fbfc-185">Confirm that the module deployed from the cloud is running on your IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-185">Confirm that the module deployed from the cloud is running on your IoT Edge device.</span></span> 

```powershell
iotedge list
```

   ![View three modules on your device](./media/quickstart/iotedge-list-2.png)

<span data-ttu-id="3fbfc-187">View the messages being sent from the tempSensor module to the cloud.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-187">View the messages being sent from the tempSensor module to the cloud.</span></span> 

```powershell
iotedge logs tempSensor -f
```

  ![View the data from your module](./media/quickstart/iotedge-logs.png)

<span data-ttu-id="3fbfc-189">You can also view the messages that are received by your IoT hub by using the [Azure IoT Toolkit extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-toolkit).</span><span class="sxs-lookup"><span data-stu-id="3fbfc-189">You can also view the messages that are received by your IoT hub by using the [Azure IoT Toolkit extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-toolkit).</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="3fbfc-190">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="3fbfc-190">Clean up resources</span></span>

<span data-ttu-id="3fbfc-191">If you want to continue on to the IoT Edge tutorials, you can use the device that you registered and set up in this quickstart.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-191">If you want to continue on to the IoT Edge tutorials, you can use the device that you registered and set up in this quickstart.</span></span> <span data-ttu-id="3fbfc-192">Otherwise, you can delete the Azure resources that you created and remove the IoT Edge runtime from your device.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-192">Otherwise, you can delete the Azure resources that you created and remove the IoT Edge runtime from your device.</span></span> 

### <a name="delete-azure-resources"></a><span data-ttu-id="3fbfc-193">Delete Azure resources</span><span class="sxs-lookup"><span data-stu-id="3fbfc-193">Delete Azure resources</span></span>

<span data-ttu-id="3fbfc-194">If you created your virtual machine and IoT hub in a new resource group, you can delete that group and all the associated resources.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-194">If you created your virtual machine and IoT hub in a new resource group, you can delete that group and all the associated resources.</span></span> <span data-ttu-id="3fbfc-195">If there's anything in that resource group that you want to keep, then just delete the individual resources that you want to clean up.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-195">If there's anything in that resource group that you want to keep, then just delete the individual resources that you want to clean up.</span></span> 

<span data-ttu-id="3fbfc-196">Remove the **IoTEdgeResources** group.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-196">Remove the **IoTEdgeResources** group.</span></span> 

   ```azurecli-interactive
   az group delete --name IoTEdgeResources 
   ```

### <a name="remove-the-iot-edge-runtime"></a><span data-ttu-id="3fbfc-197">Remove the IoT Edge runtime</span><span class="sxs-lookup"><span data-stu-id="3fbfc-197">Remove the IoT Edge runtime</span></span>

<span data-ttu-id="3fbfc-198">If you plan on using the IoT Edge device for future testing, but want to stop the tempSensor module from sending data to your IoT hub while not in use, use the following command to stop the IoT Edge service.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-198">If you plan on using the IoT Edge device for future testing, but want to stop the tempSensor module from sending data to your IoT hub while not in use, use the following command to stop the IoT Edge service.</span></span> 

   ```powershell
   Stop-Service iotedge -NoWait
   ```

<span data-ttu-id="3fbfc-199">You can restart the service when you're ready to start testing again</span><span class="sxs-lookup"><span data-stu-id="3fbfc-199">You can restart the service when you're ready to start testing again</span></span>

   ```powershell
   Start-Service iotedge
   ```

<span data-ttu-id="3fbfc-200">If you want to remove the installations from your device, use the following commands.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-200">If you want to remove the installations from your device, use the following commands.</span></span>  

<span data-ttu-id="3fbfc-201">Remove the IoT Edge runtime.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-201">Remove the IoT Edge runtime.</span></span>

   ```powershell
   . {Invoke-WebRequest -useb aka.ms/iotedge-win} | Invoke-Expression; `
   Uninstall-SecurityDaemon
   ```

<span data-ttu-id="3fbfc-202">When the IoT Edge runtime is removed, the containers that it created are stopped, but still exist on your device.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-202">When the IoT Edge runtime is removed, the containers that it created are stopped, but still exist on your device.</span></span> <span data-ttu-id="3fbfc-203">View all containers.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-203">View all containers.</span></span>

   ```powershell
   docker ps -a
   ```

<span data-ttu-id="3fbfc-204">Delete the containers that were created on your device by the IoT Edge runtime.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-204">Delete the containers that were created on your device by the IoT Edge runtime.</span></span> <span data-ttu-id="3fbfc-205">Change the name of the tempSensor container if you called it something different.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-205">Change the name of the tempSensor container if you called it something different.</span></span> 

   ```powershell
   docker rm -f tempSensor
   docker rm -f edgeHub
   docker rm -f edgeAgent
   ```
   
## <a name="next-steps"></a><span data-ttu-id="3fbfc-206">Next steps</span><span class="sxs-lookup"><span data-stu-id="3fbfc-206">Next steps</span></span>

<span data-ttu-id="3fbfc-207">In this quickstart, you created a new IoT Edge device and used the Azure IoT Edge cloud interface to deploy code onto the device.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-207">In this quickstart, you created a new IoT Edge device and used the Azure IoT Edge cloud interface to deploy code onto the device.</span></span> <span data-ttu-id="3fbfc-208">Now, you have a test device generating raw data about its environment.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-208">Now, you have a test device generating raw data about its environment.</span></span> 

<span data-ttu-id="3fbfc-209">You are ready to continue on to any of the other tutorials to learn how Azure IoT Edge can help you turn this data into business insights at the edge.</span><span class="sxs-lookup"><span data-stu-id="3fbfc-209">You are ready to continue on to any of the other tutorials to learn how Azure IoT Edge can help you turn this data into business insights at the edge.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3fbfc-210">Filter sensor data using an Azure Function</span><span class="sxs-lookup"><span data-stu-id="3fbfc-210">Filter sensor data using an Azure Function</span></span>](tutorial-deploy-function.md)


<!-- Images -->
[1]: ./media/quickstart/cloud-shell.png
[2]: ./media/quickstart/install-edge-full.png
[3]: ./media/quickstart/create-iot-hub.png
[4]: ./media/quickstart/register-device.png
[5]: ./media/quickstart/start-runtime.png
[6]: ./media/quickstart/deploy-module.png


<!-- Links -->
[lnk-docker]: https://docs.docker.com/docker-for-windows/install/ 
[lnk-account]: https://azure.microsoft.com/free
[lnk-portal]: https://portal.azure.com
[lnk-nested]: https://docs.microsoft.com/virtualization/hyper-v-on-windows/user-guide/nested-virtualization
[lnk-delete]: https://docs.microsoft.com/cli/azure/iot/hub?view=azure-cli-latest#az-iot-hub-delete

