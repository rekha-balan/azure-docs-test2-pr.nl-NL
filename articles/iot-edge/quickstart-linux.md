---
title: Quickstart Azure IoT Edge + Linux | Microsoft Docs
description: In this quickstart, learn how to deploy prebuilt code remotely to an IoT Edge device.
author: kgremban
manager: timlt
ms.author: kgremban
ms.date: 08/14/2018
ms.topic: quickstart
ms.service: iot-edge
services: iot-edge
ms.custom: mvc
ms.openlocfilehash: af291782585cf0211cf8beac54adc36fd9fe0d34
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966664"
---
# <a name="quickstart-deploy-your-first-iot-edge-module-to-a-linux-x64-device"></a><span data-ttu-id="6be2f-103">Quickstart: Deploy your first IoT Edge module to a Linux x64 device</span><span class="sxs-lookup"><span data-stu-id="6be2f-103">Quickstart: Deploy your first IoT Edge module to a Linux x64 device</span></span>

<span data-ttu-id="6be2f-104">Azure IoT Edge moves the power of the cloud to your Internet of Things devices.</span><span class="sxs-lookup"><span data-stu-id="6be2f-104">Azure IoT Edge moves the power of the cloud to your Internet of Things devices.</span></span> <span data-ttu-id="6be2f-105">In this quickstart, learn how to use the cloud interface to deploy prebuilt code remotely to an IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="6be2f-105">In this quickstart, learn how to use the cloud interface to deploy prebuilt code remotely to an IoT Edge device.</span></span>

<span data-ttu-id="6be2f-106">In this quickstart you learn how to:</span><span class="sxs-lookup"><span data-stu-id="6be2f-106">In this quickstart you learn how to:</span></span>

1. <span data-ttu-id="6be2f-107">Create an IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6be2f-107">Create an IoT Hub.</span></span>
2. <span data-ttu-id="6be2f-108">Register an IoT Edge device to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="6be2f-108">Register an IoT Edge device to your IoT hub.</span></span>
3. <span data-ttu-id="6be2f-109">Install and start the IoT Edge runtime on your device.</span><span class="sxs-lookup"><span data-stu-id="6be2f-109">Install and start the IoT Edge runtime on your device.</span></span>
4. <span data-ttu-id="6be2f-110">Remotely deploy a module to an IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="6be2f-110">Remotely deploy a module to an IoT Edge device.</span></span>

![Quickstart architecture][2]

<span data-ttu-id="6be2f-112">This quickstart turns your Linux computer or virtual machine into an IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="6be2f-112">This quickstart turns your Linux computer or virtual machine into an IoT Edge device.</span></span> <span data-ttu-id="6be2f-113">Then you can deploy a module from the Azure portal to your device.</span><span class="sxs-lookup"><span data-stu-id="6be2f-113">Then you can deploy a module from the Azure portal to your device.</span></span> <span data-ttu-id="6be2f-114">The module that you deploy in this quickstart is a simulated sensor that generates temperature, humidity, and pressure data.</span><span class="sxs-lookup"><span data-stu-id="6be2f-114">The module that you deploy in this quickstart is a simulated sensor that generates temperature, humidity, and pressure data.</span></span> <span data-ttu-id="6be2f-115">The other Azure IoT Edge tutorials build upon the work you do here by deploying modules that analyze the simulated data for business insights.</span><span class="sxs-lookup"><span data-stu-id="6be2f-115">The other Azure IoT Edge tutorials build upon the work you do here by deploying modules that analyze the simulated data for business insights.</span></span> 

<span data-ttu-id="6be2f-116">If you don't have an active Azure subscription, create a [free account][lnk-account] before you begin.</span><span class="sxs-lookup"><span data-stu-id="6be2f-116">If you don't have an active Azure subscription, create a [free account][lnk-account] before you begin.</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6be2f-117">You use the Azure CLI to complete many of the steps in this quickstart, and Azure IoT has an extension to enable additional functionality.</span><span class="sxs-lookup"><span data-stu-id="6be2f-117">You use the Azure CLI to complete many of the steps in this quickstart, and Azure IoT has an extension to enable additional functionality.</span></span> 

<span data-ttu-id="6be2f-118">Add the Azure IoT extension to the cloud shell instance.</span><span class="sxs-lookup"><span data-stu-id="6be2f-118">Add the Azure IoT extension to the cloud shell instance.</span></span>

   ```azurecli-interactive
   az extension add --name azure-cli-iot-ext
   ```
   
## <a name="prerequisites"></a><span data-ttu-id="6be2f-119">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6be2f-119">Prerequisites</span></span>

<span data-ttu-id="6be2f-120">Cloud resources:</span><span class="sxs-lookup"><span data-stu-id="6be2f-120">Cloud resources:</span></span> 

* <span data-ttu-id="6be2f-121">A resource group to manage all the resources you use in this quickstart.</span><span class="sxs-lookup"><span data-stu-id="6be2f-121">A resource group to manage all the resources you use in this quickstart.</span></span> 

   ```azurecli-interactive
   az group create --name IoTEdgeResources --location westus
   ```

<span data-ttu-id="6be2f-122">IoT Edge device:</span><span class="sxs-lookup"><span data-stu-id="6be2f-122">IoT Edge device:</span></span>

* <span data-ttu-id="6be2f-123">A Linux device or virtual machine to act as your IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="6be2f-123">A Linux device or virtual machine to act as your IoT Edge device.</span></span> <span data-ttu-id="6be2f-124">If you want to create a virtual machine in Azure, use the following command to get started quickly:</span><span class="sxs-lookup"><span data-stu-id="6be2f-124">If you want to create a virtual machine in Azure, use the following command to get started quickly:</span></span>

   ```azurecli-interactive
   az vm create --resource-group IoTEdgeResources --name EdgeVM --image Canonical:UbuntuServer:16.04-LTS:latest --admin-username azureuser --generate-ssh-keys --size Standard_B1ms
   ```

## <a name="create-an-iot-hub"></a><span data-ttu-id="6be2f-125">Create an IoT hub</span><span class="sxs-lookup"><span data-stu-id="6be2f-125">Create an IoT hub</span></span>

<span data-ttu-id="6be2f-126">Start the quickstart by creating your IoT hub with Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="6be2f-126">Start the quickstart by creating your IoT hub with Azure CLI.</span></span> 

![Create IoT Hub][3]

<span data-ttu-id="6be2f-128">The free level of IoT Hub works for this quickstart.</span><span class="sxs-lookup"><span data-stu-id="6be2f-128">The free level of IoT Hub works for this quickstart.</span></span> <span data-ttu-id="6be2f-129">If you've used IoT Hub in the past and already have a free hub created, you can use that IoT hub.</span><span class="sxs-lookup"><span data-stu-id="6be2f-129">If you've used IoT Hub in the past and already have a free hub created, you can use that IoT hub.</span></span> <span data-ttu-id="6be2f-130">Each subscription can only have one free IoT hub.</span><span class="sxs-lookup"><span data-stu-id="6be2f-130">Each subscription can only have one free IoT hub.</span></span> 

<span data-ttu-id="6be2f-131">The following code creates a free **F1** hub in the resource group **IoTEdgeResources**.</span><span class="sxs-lookup"><span data-stu-id="6be2f-131">The following code creates a free **F1** hub in the resource group **IoTEdgeResources**.</span></span> <span data-ttu-id="6be2f-132">Replace *{hub_name}* with a unique name for your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="6be2f-132">Replace *{hub_name}* with a unique name for your IoT hub.</span></span>

   ```azurecli-interactive
   az iot hub create --resource-group IoTEdgeResources --name {hub_name} --sku F1 
   ```

   <span data-ttu-id="6be2f-133">If you get an error because there's already one free hub in your subscription, change the SKU to **S1**.</span><span class="sxs-lookup"><span data-stu-id="6be2f-133">If you get an error because there's already one free hub in your subscription, change the SKU to **S1**.</span></span> 

## <a name="register-an-iot-edge-device"></a><span data-ttu-id="6be2f-134">Register an IoT Edge device</span><span class="sxs-lookup"><span data-stu-id="6be2f-134">Register an IoT Edge device</span></span>

<span data-ttu-id="6be2f-135">Register an IoT Edge device with your newly created IoT hub.</span><span class="sxs-lookup"><span data-stu-id="6be2f-135">Register an IoT Edge device with your newly created IoT hub.</span></span> 
<span data-ttu-id="6be2f-136">![Register a device][4]</span><span class="sxs-lookup"><span data-stu-id="6be2f-136">![Register a device][4]</span></span>

<span data-ttu-id="6be2f-137">Create a device identity for your simulated device so that it can communicate with your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="6be2f-137">Create a device identity for your simulated device so that it can communicate with your IoT hub.</span></span> <span data-ttu-id="6be2f-138">The device identity lives in the cloud, and you use a unique device connection string to associate a physical device to a device identity.</span><span class="sxs-lookup"><span data-stu-id="6be2f-138">The device identity lives in the cloud, and you use a unique device connection string to associate a physical device to a device identity.</span></span> 

<span data-ttu-id="6be2f-139">Since IoT Edge devices behave and can be managed differently than typical IoT devices, you declare this to be an IoT Edge device from the beginning.</span><span class="sxs-lookup"><span data-stu-id="6be2f-139">Since IoT Edge devices behave and can be managed differently than typical IoT devices, you declare this to be an IoT Edge device from the beginning.</span></span> 

1. <span data-ttu-id="6be2f-140">In the Azure cloud shell, enter the following command to create a device named **myEdgeDevice** in your hub.</span><span class="sxs-lookup"><span data-stu-id="6be2f-140">In the Azure cloud shell, enter the following command to create a device named **myEdgeDevice** in your hub.</span></span>

   ```azurecli-interactive
   az iot hub device-identity create --hub-name {hub_name} --device-id myEdgeDevice --edge-enabled
   ```

1. <span data-ttu-id="6be2f-141">Retrieve the connection string for your device, which links your physical device with its identity in IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6be2f-141">Retrieve the connection string for your device, which links your physical device with its identity in IoT Hub.</span></span> 

   ```azurecli-interactive
   az iot hub device-identity show-connection-string --device-id myEdgeDevice --hub-name {hub_name}
   ```

1. <span data-ttu-id="6be2f-142">Copy the connection string and save it.</span><span class="sxs-lookup"><span data-stu-id="6be2f-142">Copy the connection string and save it.</span></span> <span data-ttu-id="6be2f-143">You'll use this value to configure the IoT Edge runtime in the next section.</span><span class="sxs-lookup"><span data-stu-id="6be2f-143">You'll use this value to configure the IoT Edge runtime in the next section.</span></span> 


## <a name="install-and-start-the-iot-edge-runtime"></a><span data-ttu-id="6be2f-144">Install and start the IoT Edge runtime</span><span class="sxs-lookup"><span data-stu-id="6be2f-144">Install and start the IoT Edge runtime</span></span>

<span data-ttu-id="6be2f-145">Install and start the Azure IoT Edge runtime on your IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="6be2f-145">Install and start the Azure IoT Edge runtime on your IoT Edge device.</span></span> 
<span data-ttu-id="6be2f-146">![Register a device][5]</span><span class="sxs-lookup"><span data-stu-id="6be2f-146">![Register a device][5]</span></span>

<span data-ttu-id="6be2f-147">The IoT Edge runtime is deployed on all IoT Edge devices.</span><span class="sxs-lookup"><span data-stu-id="6be2f-147">The IoT Edge runtime is deployed on all IoT Edge devices.</span></span> <span data-ttu-id="6be2f-148">It has three components.</span><span class="sxs-lookup"><span data-stu-id="6be2f-148">It has three components.</span></span> <span data-ttu-id="6be2f-149">The **IoT Edge security daemon** starts each time an Edge device boots and bootstraps the device by starting the IoT Edge agent.</span><span class="sxs-lookup"><span data-stu-id="6be2f-149">The **IoT Edge security daemon** starts each time an Edge device boots and bootstraps the device by starting the IoT Edge agent.</span></span> <span data-ttu-id="6be2f-150">The **IoT Edge agent** facilitates deployment and monitoring of modules on the IoT Edge device, including the IoT Edge hub.</span><span class="sxs-lookup"><span data-stu-id="6be2f-150">The **IoT Edge agent** facilitates deployment and monitoring of modules on the IoT Edge device, including the IoT Edge hub.</span></span> <span data-ttu-id="6be2f-151">The **IoT Edge hub** manages communications between modules on the IoT Edge device, and between the device and IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6be2f-151">The **IoT Edge hub** manages communications between modules on the IoT Edge device, and between the device and IoT Hub.</span></span> 

<span data-ttu-id="6be2f-152">During the runtime configuration, you provide a device connection string.</span><span class="sxs-lookup"><span data-stu-id="6be2f-152">During the runtime configuration, you provide a device connection string.</span></span> <span data-ttu-id="6be2f-153">Use the string that you retrieved from the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="6be2f-153">Use the string that you retrieved from the Azure CLI.</span></span> <span data-ttu-id="6be2f-154">This string associates your physical device with the IoT Edge device identity in Azure.</span><span class="sxs-lookup"><span data-stu-id="6be2f-154">This string associates your physical device with the IoT Edge device identity in Azure.</span></span> 

<span data-ttu-id="6be2f-155">Complete the following steps in the Linux machine or VM that you prepared to function as an IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="6be2f-155">Complete the following steps in the Linux machine or VM that you prepared to function as an IoT Edge device.</span></span> 

### <a name="register-your-device-to-use-the-software-repository"></a><span data-ttu-id="6be2f-156">Register your device to use the software repository</span><span class="sxs-lookup"><span data-stu-id="6be2f-156">Register your device to use the software repository</span></span>

<span data-ttu-id="6be2f-157">The packages that you need to run the IoT Edge runtime are managed in a software repository.</span><span class="sxs-lookup"><span data-stu-id="6be2f-157">The packages that you need to run the IoT Edge runtime are managed in a software repository.</span></span> <span data-ttu-id="6be2f-158">Configure your IoT Edge device to access this repository.</span><span class="sxs-lookup"><span data-stu-id="6be2f-158">Configure your IoT Edge device to access this repository.</span></span> 

<span data-ttu-id="6be2f-159">The steps in this section are for devices running **Ubuntu 16.04**.</span><span class="sxs-lookup"><span data-stu-id="6be2f-159">The steps in this section are for devices running **Ubuntu 16.04**.</span></span> <span data-ttu-id="6be2f-160">To access the software repository on other versions of Linux, see [Install the Azure IoT Edge runtime on Linux (x64)](how-to-install-iot-edge-linux.md) or [Install Azure IoT Edge runtime on Linux (ARM32v7/armhf)](how-to-install-iot-edge-linux-arm.md).</span><span class="sxs-lookup"><span data-stu-id="6be2f-160">To access the software repository on other versions of Linux, see [Install the Azure IoT Edge runtime on Linux (x64)](how-to-install-iot-edge-linux.md) or [Install Azure IoT Edge runtime on Linux (ARM32v7/armhf)](how-to-install-iot-edge-linux-arm.md).</span></span>

1. <span data-ttu-id="6be2f-161">On the machine that you're using as an IoT Edge device, install the repository configuration.</span><span class="sxs-lookup"><span data-stu-id="6be2f-161">On the machine that you're using as an IoT Edge device, install the repository configuration.</span></span>

   ```bash
   curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > ./microsoft-prod.list
   sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
   ```

2. <span data-ttu-id="6be2f-162">Install a public key to access the repository.</span><span class="sxs-lookup"><span data-stu-id="6be2f-162">Install a public key to access the repository.</span></span>

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
   sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
   ```

### <a name="install-a-container-runtime"></a><span data-ttu-id="6be2f-163">Install a container runtime</span><span class="sxs-lookup"><span data-stu-id="6be2f-163">Install a container runtime</span></span>

<span data-ttu-id="6be2f-164">The IoT Edge runtime is a set of containers, and the logic that you deploy to your IoT Edge device is packaged as containers.</span><span class="sxs-lookup"><span data-stu-id="6be2f-164">The IoT Edge runtime is a set of containers, and the logic that you deploy to your IoT Edge device is packaged as containers.</span></span> <span data-ttu-id="6be2f-165">Prepare your device for these components by installing a container runtime.</span><span class="sxs-lookup"><span data-stu-id="6be2f-165">Prepare your device for these components by installing a container runtime.</span></span>

1. <span data-ttu-id="6be2f-166">Update **apt-get**.</span><span class="sxs-lookup"><span data-stu-id="6be2f-166">Update **apt-get**.</span></span>

   ```bash
   sudo apt-get update
   ```

2. <span data-ttu-id="6be2f-167">Install **Moby**, a container runtime.</span><span class="sxs-lookup"><span data-stu-id="6be2f-167">Install **Moby**, a container runtime.</span></span>

   ```bash
   sudo apt-get install moby-engine
   ```

3. <span data-ttu-id="6be2f-168">Install the CLI commands for Moby.</span><span class="sxs-lookup"><span data-stu-id="6be2f-168">Install the CLI commands for Moby.</span></span> 

   ```bash
   sudo apt-get install moby-cli
   ```

### <a name="install-and-configure-the-iot-edge-security-daemon"></a><span data-ttu-id="6be2f-169">Install and configure the IoT Edge security daemon</span><span class="sxs-lookup"><span data-stu-id="6be2f-169">Install and configure the IoT Edge security daemon</span></span>

<span data-ttu-id="6be2f-170">The security daemon installs as a system service so that the IoT Edge runtime starts every time your device boots.</span><span class="sxs-lookup"><span data-stu-id="6be2f-170">The security daemon installs as a system service so that the IoT Edge runtime starts every time your device boots.</span></span> <span data-ttu-id="6be2f-171">The installation also includes a version of **hsmlib** that allows the security daemon to interact with the device's hardware security.</span><span class="sxs-lookup"><span data-stu-id="6be2f-171">The installation also includes a version of **hsmlib** that allows the security daemon to interact with the device's hardware security.</span></span> 

1. <span data-ttu-id="6be2f-172">Download and install the IoT Edge Security Daemon.</span><span class="sxs-lookup"><span data-stu-id="6be2f-172">Download and install the IoT Edge Security Daemon.</span></span> 

   ```bash
   sudo apt-get update
   sudo apt-get install iotedge
   ```

2. <span data-ttu-id="6be2f-173">Open the IoT Edge configuration file.</span><span class="sxs-lookup"><span data-stu-id="6be2f-173">Open the IoT Edge configuration file.</span></span> <span data-ttu-id="6be2f-174">It is a protected file so you may have to use elevated privileges to access it.</span><span class="sxs-lookup"><span data-stu-id="6be2f-174">It is a protected file so you may have to use elevated privileges to access it.</span></span>
   
   ```bash
   sudo nano /etc/iotedge/config.yaml
   ```

3. <span data-ttu-id="6be2f-175">Add the IoT Edge device connection string.</span><span class="sxs-lookup"><span data-stu-id="6be2f-175">Add the IoT Edge device connection string.</span></span> <span data-ttu-id="6be2f-176">Find the variable **device_connection_string** and update its value with the string that you copied after registering your device.</span><span class="sxs-lookup"><span data-stu-id="6be2f-176">Find the variable **device_connection_string** and update its value with the string that you copied after registering your device.</span></span> <span data-ttu-id="6be2f-177">This connection string associates your physical device with the device identity that you created in Azure.</span><span class="sxs-lookup"><span data-stu-id="6be2f-177">This connection string associates your physical device with the device identity that you created in Azure.</span></span>

4. <span data-ttu-id="6be2f-178">Save and close the file.</span><span class="sxs-lookup"><span data-stu-id="6be2f-178">Save and close the file.</span></span> 

   <span data-ttu-id="6be2f-179">`CTRL + X`, `Y`, `Enter`</span><span class="sxs-lookup"><span data-stu-id="6be2f-179">`CTRL + X`, `Y`, `Enter`</span></span>

5. <span data-ttu-id="6be2f-180">Restart the IoT Edge security daemon to apply your changes.</span><span class="sxs-lookup"><span data-stu-id="6be2f-180">Restart the IoT Edge security daemon to apply your changes.</span></span>

   ```bash
   sudo systemctl restart iotedge
   ```

>[!TIP]
><span data-ttu-id="6be2f-181">You need elevated privileges to run `iotedge` commands.</span><span class="sxs-lookup"><span data-stu-id="6be2f-181">You need elevated privileges to run `iotedge` commands.</span></span> <span data-ttu-id="6be2f-182">Once you sign out of your machine and sign back in the first time after installing the IoT Edge runtime, your permissions are automatically updated.</span><span class="sxs-lookup"><span data-stu-id="6be2f-182">Once you sign out of your machine and sign back in the first time after installing the IoT Edge runtime, your permissions are automatically updated.</span></span> <span data-ttu-id="6be2f-183">Until then, use **sudo** in front of the commands.</span><span class="sxs-lookup"><span data-stu-id="6be2f-183">Until then, use **sudo** in front of the commands.</span></span> 

### <a name="view-the-iot-edge-runtime-status"></a><span data-ttu-id="6be2f-184">View the IoT Edge runtime status</span><span class="sxs-lookup"><span data-stu-id="6be2f-184">View the IoT Edge runtime status</span></span>

<span data-ttu-id="6be2f-185">Verify that the runtime was successfully installed and configured.</span><span class="sxs-lookup"><span data-stu-id="6be2f-185">Verify that the runtime was successfully installed and configured.</span></span>

1. <span data-ttu-id="6be2f-186">Check to see that the Edge Security Daemon is running as a system service.</span><span class="sxs-lookup"><span data-stu-id="6be2f-186">Check to see that the Edge Security Daemon is running as a system service.</span></span>

   ```bash
   sudo systemctl status iotedge
   ```

   ![See the Edge Daemon running as a system service](./media/quickstart-linux/iotedged-running.png)

2. <span data-ttu-id="6be2f-188">If you need to troubleshoot the service, retrieve the service logs.</span><span class="sxs-lookup"><span data-stu-id="6be2f-188">If you need to troubleshoot the service, retrieve the service logs.</span></span> 

   ```bash
   journalctl -u iotedge
   ```

3. <span data-ttu-id="6be2f-189">View the modules running on your device.</span><span class="sxs-lookup"><span data-stu-id="6be2f-189">View the modules running on your device.</span></span> 

   ```bash
   sudo iotedge list
   ```

   ![View one module on your device](./media/quickstart-linux/iotedge-list-1.png)

<span data-ttu-id="6be2f-191">Your IoT Edge device is now configured.</span><span class="sxs-lookup"><span data-stu-id="6be2f-191">Your IoT Edge device is now configured.</span></span> <span data-ttu-id="6be2f-192">It's ready to run cloud-deployed modules.</span><span class="sxs-lookup"><span data-stu-id="6be2f-192">It's ready to run cloud-deployed modules.</span></span> 

## <a name="deploy-a-module"></a><span data-ttu-id="6be2f-193">Deploy a module</span><span class="sxs-lookup"><span data-stu-id="6be2f-193">Deploy a module</span></span>

<span data-ttu-id="6be2f-194">Manage your Azure IoT Edge device from the cloud to deploy a module that will send telemetry data to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6be2f-194">Manage your Azure IoT Edge device from the cloud to deploy a module that will send telemetry data to IoT Hub.</span></span>
<span data-ttu-id="6be2f-195">![Register a device][6]</span><span class="sxs-lookup"><span data-stu-id="6be2f-195">![Register a device][6]</span></span>

[!INCLUDE [iot-edge-deploy-module](../../includes/iot-edge-deploy-module.md)]

## <a name="view-generated-data"></a><span data-ttu-id="6be2f-196">View generated data</span><span class="sxs-lookup"><span data-stu-id="6be2f-196">View generated data</span></span>

<span data-ttu-id="6be2f-197">In this quickstart, you created a new IoT Edge device and installed the IoT Edge runtime on it.</span><span class="sxs-lookup"><span data-stu-id="6be2f-197">In this quickstart, you created a new IoT Edge device and installed the IoT Edge runtime on it.</span></span> <span data-ttu-id="6be2f-198">Then, you used the Azure portal to push an IoT Edge module to run on the device without having to make changes to the device itself.</span><span class="sxs-lookup"><span data-stu-id="6be2f-198">Then, you used the Azure portal to push an IoT Edge module to run on the device without having to make changes to the device itself.</span></span> <span data-ttu-id="6be2f-199">In this case, the module that you pushed creates environmental data that you can use for the tutorials.</span><span class="sxs-lookup"><span data-stu-id="6be2f-199">In this case, the module that you pushed creates environmental data that you can use for the tutorials.</span></span> 

<span data-ttu-id="6be2f-200">Open the command prompt on your IoT Edge device again.</span><span class="sxs-lookup"><span data-stu-id="6be2f-200">Open the command prompt on your IoT Edge device again.</span></span> <span data-ttu-id="6be2f-201">Confirm that the module deployed from the cloud is running on your IoT Edge device:</span><span class="sxs-lookup"><span data-stu-id="6be2f-201">Confirm that the module deployed from the cloud is running on your IoT Edge device:</span></span>

   ```bash
   sudo iotedge list
   ```

   ![View three modules on your device](./media/quickstart-linux/iotedge-list-2.png)

<span data-ttu-id="6be2f-203">View the messages being sent from the tempSensor module:</span><span class="sxs-lookup"><span data-stu-id="6be2f-203">View the messages being sent from the tempSensor module:</span></span>

   ```bash
   sudo iotedge logs tempSensor -f 
   ```
<span data-ttu-id="6be2f-204">After a logoff and login, *sudo* is not required for the above command.</span><span class="sxs-lookup"><span data-stu-id="6be2f-204">After a logoff and login, *sudo* is not required for the above command.</span></span>

![View the data from your module](./media/quickstart-linux/iotedge-logs.png)

<span data-ttu-id="6be2f-206">The temperature sensor module may be waiting to connect to Edge Hub if the last line you see in the log is `Using transport Mqtt_Tcp_Only`.</span><span class="sxs-lookup"><span data-stu-id="6be2f-206">The temperature sensor module may be waiting to connect to Edge Hub if the last line you see in the log is `Using transport Mqtt_Tcp_Only`.</span></span> <span data-ttu-id="6be2f-207">Try killing the module and letting the Edge Agent restart it.</span><span class="sxs-lookup"><span data-stu-id="6be2f-207">Try killing the module and letting the Edge Agent restart it.</span></span> <span data-ttu-id="6be2f-208">You can kill it with the command `sudo docker stop tempSensor`.</span><span class="sxs-lookup"><span data-stu-id="6be2f-208">You can kill it with the command `sudo docker stop tempSensor`.</span></span>

<span data-ttu-id="6be2f-209">You can also view the telemetry as it arrives at your IoT hub by using the [Azure IoT Toolkit extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-toolkit).</span><span class="sxs-lookup"><span data-stu-id="6be2f-209">You can also view the telemetry as it arrives at your IoT hub by using the [Azure IoT Toolkit extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-toolkit).</span></span> 


## <a name="clean-up-resources"></a><span data-ttu-id="6be2f-210">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="6be2f-210">Clean up resources</span></span>

<span data-ttu-id="6be2f-211">If you want to continue on to the IoT Edge tutorials, you can use the device that you registered and set up in this quickstart.</span><span class="sxs-lookup"><span data-stu-id="6be2f-211">If you want to continue on to the IoT Edge tutorials, you can use the device that you registered and set up in this quickstart.</span></span> <span data-ttu-id="6be2f-212">Otherwise, you can delete the Azure resources that you created and remove the IoT Edge runtime from your device.</span><span class="sxs-lookup"><span data-stu-id="6be2f-212">Otherwise, you can delete the Azure resources that you created and remove the IoT Edge runtime from your device.</span></span> 

### <a name="delete-azure-resources"></a><span data-ttu-id="6be2f-213">Delete Azure resources</span><span class="sxs-lookup"><span data-stu-id="6be2f-213">Delete Azure resources</span></span>

<span data-ttu-id="6be2f-214">If you created your virtual machine and IoT hub in a new resource group, you can delete that group and all the associated resources.</span><span class="sxs-lookup"><span data-stu-id="6be2f-214">If you created your virtual machine and IoT hub in a new resource group, you can delete that group and all the associated resources.</span></span> <span data-ttu-id="6be2f-215">If there's anything in that resource group that you want to keep, then just delete the individual resources that you want to clean up.</span><span class="sxs-lookup"><span data-stu-id="6be2f-215">If there's anything in that resource group that you want to keep, then just delete the individual resources that you want to clean up.</span></span> 

<span data-ttu-id="6be2f-216">Remove the **IoTEdgeResources** group.</span><span class="sxs-lookup"><span data-stu-id="6be2f-216">Remove the **IoTEdgeResources** group.</span></span> 

   ```azurecli-interactive
   az group delete --name IoTEdgeResources 
   ```

### <a name="remove-the-iot-edge-runtime"></a><span data-ttu-id="6be2f-217">Remove the IoT Edge runtime</span><span class="sxs-lookup"><span data-stu-id="6be2f-217">Remove the IoT Edge runtime</span></span>

<span data-ttu-id="6be2f-218">If you want to remove the installations from your device, use the following commands.</span><span class="sxs-lookup"><span data-stu-id="6be2f-218">If you want to remove the installations from your device, use the following commands.</span></span>  

<span data-ttu-id="6be2f-219">Remove the IoT Edge runtime.</span><span class="sxs-lookup"><span data-stu-id="6be2f-219">Remove the IoT Edge runtime.</span></span>

   ```bash
   sudo apt-get remove --purge iotedge
   ```

<span data-ttu-id="6be2f-220">When the IoT Edge runtime is removed, the containers that it created are stopped, but still exist on your device.</span><span class="sxs-lookup"><span data-stu-id="6be2f-220">When the IoT Edge runtime is removed, the containers that it created are stopped, but still exist on your device.</span></span> <span data-ttu-id="6be2f-221">View all containers.</span><span class="sxs-lookup"><span data-stu-id="6be2f-221">View all containers.</span></span>

   ```bash
   sudo docker ps -a
   ```

<span data-ttu-id="6be2f-222">Delete the containers that were created on your device by the IoT Edge runtime.</span><span class="sxs-lookup"><span data-stu-id="6be2f-222">Delete the containers that were created on your device by the IoT Edge runtime.</span></span> <span data-ttu-id="6be2f-223">Change the name of the tempSensor container if you called it something different.</span><span class="sxs-lookup"><span data-stu-id="6be2f-223">Change the name of the tempSensor container if you called it something different.</span></span> 

   ```bash
   sudo docker rm -f tempSensor
   sudo docker rm -f edgeHub
   sudo docker rm -f edgeAgent
   ```

<span data-ttu-id="6be2f-224">Remove the container runtime.</span><span class="sxs-lookup"><span data-stu-id="6be2f-224">Remove the container runtime.</span></span>

   ```bash
   sudo apt-get remove --purge moby-cli
   sudo apt-get remove --purge moby-engine
   ```

## <a name="next-steps"></a><span data-ttu-id="6be2f-225">Next steps</span><span class="sxs-lookup"><span data-stu-id="6be2f-225">Next steps</span></span>

<span data-ttu-id="6be2f-226">This quickstart is the prerequisite for all of the IoT Edge tutorials.</span><span class="sxs-lookup"><span data-stu-id="6be2f-226">This quickstart is the prerequisite for all of the IoT Edge tutorials.</span></span> <span data-ttu-id="6be2f-227">You can continue on to any of the other tutorials to learn how Azure IoT Edge can help you turn this data into business insights at the edge.</span><span class="sxs-lookup"><span data-stu-id="6be2f-227">You can continue on to any of the other tutorials to learn how Azure IoT Edge can help you turn this data into business insights at the edge.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6be2f-228">Filter sensor data using an Azure Function</span><span class="sxs-lookup"><span data-stu-id="6be2f-228">Filter sensor data using an Azure Function</span></span>](tutorial-deploy-function.md)



<!-- Images -->
[0]: ./media/quickstart-linux/cloud-shell.png
[1]: ./media/quickstart-linux/view-module.png
[2]: ./media/quickstart-linux/install-edge-full.png
[3]: ./media/quickstart-linux/create-iot-hub.png
[4]: ./media/quickstart-linux/register-device.png
[5]: ./media/quickstart-linux/start-runtime.png
[6]: ./media/quickstart-linux/deploy-module.png
[7]: ./media/quickstart-linux/iotedged-running.png
[8]: ./media/tutorial-simulate-device-linux/running-modules.png
[9]: ./media/tutorial-simulate-device-linux/sensor-data.png


<!-- Links -->
[lnk-docker-ubuntu]: https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/ 
[lnk-account]: https://azure.microsoft.com/free
[lnk-portal]: https://portal.azure.com
[lnk-delete]: https://docs.microsoft.com/cli/azure/iot/hub?view=azure-cli-latest#az-iot-hub-delete

<!-- Anchor links -->
[anchor-register]: #register-an-iot-edge-device
