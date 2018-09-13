---
title: Simulate Azure IoT Edge on Linux | Microsoft Docs
description: In this quickstart, learn how to deploy prebuilt code remotely to an IoT Edge device.
author: kgremban
manager: timlt
ms.author: kgremban
ms.date: 07/02/2018
ms.topic: tutorial
ms.service: iot-edge
services: iot-edge
ms.custom: mvc
ms.openlocfilehash: dfbe931bbe5887e9c0545558c4d2b2565718dd0a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868377"
---
# <a name="quickstart-deploy-your-first-iot-edge-module-to-a-linux-x64-device"></a><span data-ttu-id="4692f-103">Quickstart: Deploy your first IoT Edge module to a Linux x64 device</span><span class="sxs-lookup"><span data-stu-id="4692f-103">Quickstart: Deploy your first IoT Edge module to a Linux x64 device</span></span>

<span data-ttu-id="4692f-104">Azure IoT Edge enables you to perform analytics and data processing on your devices, instead of having to push all the data to the cloud.</span><span class="sxs-lookup"><span data-stu-id="4692f-104">Azure IoT Edge enables you to perform analytics and data processing on your devices, instead of having to push all the data to the cloud.</span></span> <span data-ttu-id="4692f-105">The IoT Edge tutorials demonstrate how to deploy different types of modules, but first you need a device to test.</span><span class="sxs-lookup"><span data-stu-id="4692f-105">The IoT Edge tutorials demonstrate how to deploy different types of modules, but first you need a device to test.</span></span> 

<span data-ttu-id="4692f-106">In this quickstart you learn how to:</span><span class="sxs-lookup"><span data-stu-id="4692f-106">In this quickstart you learn how to:</span></span>

1. <span data-ttu-id="4692f-107">Create an IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4692f-107">Create an IoT Hub.</span></span>
2. <span data-ttu-id="4692f-108">Register an IoT Edge device to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4692f-108">Register an IoT Edge device to your IoT hub.</span></span>
3. <span data-ttu-id="4692f-109">Start the IoT Edge runtime.</span><span class="sxs-lookup"><span data-stu-id="4692f-109">Start the IoT Edge runtime.</span></span>
4. <span data-ttu-id="4692f-110">Remotely deploy a module to an IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="4692f-110">Remotely deploy a module to an IoT Edge device.</span></span>

![Tutorial architecture][2]

<span data-ttu-id="4692f-112">This quickstart turns your Linux computer or virtual machine into an IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="4692f-112">This quickstart turns your Linux computer or virtual machine into an IoT Edge device.</span></span> <span data-ttu-id="4692f-113">Then you can deploy a module from the Azure portal to your device.</span><span class="sxs-lookup"><span data-stu-id="4692f-113">Then you can deploy a module from the Azure portal to your device.</span></span> <span data-ttu-id="4692f-114">The module that you deploy in this quickstart is a simulated sensor that generates temperature, humidity, and pressure data.</span><span class="sxs-lookup"><span data-stu-id="4692f-114">The module that you deploy in this quickstart is a simulated sensor that generates temperature, humidity, and pressure data.</span></span> <span data-ttu-id="4692f-115">The other Azure IoT Edge tutorials build upon the work you do here by deploying modules that analyze the simulated data for business insights.</span><span class="sxs-lookup"><span data-stu-id="4692f-115">The other Azure IoT Edge tutorials build upon the work you do here by deploying modules that analyze the simulated data for business insights.</span></span> 

<span data-ttu-id="4692f-116">If you don't have an active Azure subscription, create a [free account][lnk-account] before you begin.</span><span class="sxs-lookup"><span data-stu-id="4692f-116">If you don't have an active Azure subscription, create a [free account][lnk-account] before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4692f-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4692f-117">Prerequisites</span></span>

<span data-ttu-id="4692f-118">This quickstart uses a Linux machine as an IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="4692f-118">This quickstart uses a Linux machine as an IoT Edge device.</span></span> <span data-ttu-id="4692f-119">If you don't have one available for testing, follow the instructions in [Create a Linux virtual machine in the Azure portal](../virtual-machines/linux/quick-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4692f-119">If you don't have one available for testing, follow the instructions in [Create a Linux virtual machine in the Azure portal](../virtual-machines/linux/quick-create-portal.md).</span></span> 
* <span data-ttu-id="4692f-120">You don't have to follow the steps to install and run the web server.</span><span class="sxs-lookup"><span data-stu-id="4692f-120">You don't have to follow the steps to install and run the web server.</span></span> <span data-ttu-id="4692f-121">Once you connect to your virtual machine, you can stop.</span><span class="sxs-lookup"><span data-stu-id="4692f-121">Once you connect to your virtual machine, you can stop.</span></span>  
* <span data-ttu-id="4692f-122">Create your virtual machine in a new resource group, that you can use when you create the rest of the Azure resources for this quickstart.</span><span class="sxs-lookup"><span data-stu-id="4692f-122">Create your virtual machine in a new resource group, that you can use when you create the rest of the Azure resources for this quickstart.</span></span> <span data-ttu-id="4692f-123">Name it something recognizable, like *IoTEdgeResources*.</span><span class="sxs-lookup"><span data-stu-id="4692f-123">Name it something recognizable, like *IoTEdgeResources*.</span></span> 
* <span data-ttu-id="4692f-124">You don't need a very large virtual machine to test IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="4692f-124">You don't need a very large virtual machine to test IoT Edge.</span></span> <span data-ttu-id="4692f-125">A size like **B1ms** is sufficient.</span><span class="sxs-lookup"><span data-stu-id="4692f-125">A size like **B1ms** is sufficient.</span></span> 

## <a name="create-an-iot-hub"></a><span data-ttu-id="4692f-126">Create an IoT hub</span><span class="sxs-lookup"><span data-stu-id="4692f-126">Create an IoT hub</span></span>

<span data-ttu-id="4692f-127">Start the quickstart by creating your IoT Hub in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4692f-127">Start the quickstart by creating your IoT Hub in the Azure portal.</span></span>
<span data-ttu-id="4692f-128">![Create IoT Hub][3]</span><span class="sxs-lookup"><span data-stu-id="4692f-128">![Create IoT Hub][3]</span></span>

[!INCLUDE [iot-hub-create-hub](../../includes/iot-hub-create-hub.md)]

## <a name="register-an-iot-edge-device"></a><span data-ttu-id="4692f-129">Register an IoT Edge device</span><span class="sxs-lookup"><span data-stu-id="4692f-129">Register an IoT Edge device</span></span>

<span data-ttu-id="4692f-130">Register an IoT Edge device with your newly created IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4692f-130">Register an IoT Edge device with your newly created IoT Hub.</span></span>
<span data-ttu-id="4692f-131">![Register a device][4]</span><span class="sxs-lookup"><span data-stu-id="4692f-131">![Register a device][4]</span></span>

[!INCLUDE [iot-edge-register-device](../../includes/iot-edge-register-device.md)]


## <a name="install-and-start-the-iot-edge-runtime"></a><span data-ttu-id="4692f-132">Install and start the IoT Edge runtime</span><span class="sxs-lookup"><span data-stu-id="4692f-132">Install and start the IoT Edge runtime</span></span>

<span data-ttu-id="4692f-133">Install and start the Azure IoT Edge runtime on your device.</span><span class="sxs-lookup"><span data-stu-id="4692f-133">Install and start the Azure IoT Edge runtime on your device.</span></span> 
<span data-ttu-id="4692f-134">![Register a device][5]</span><span class="sxs-lookup"><span data-stu-id="4692f-134">![Register a device][5]</span></span>

<span data-ttu-id="4692f-135">The IoT Edge runtime is deployed on all IoT Edge devices.</span><span class="sxs-lookup"><span data-stu-id="4692f-135">The IoT Edge runtime is deployed on all IoT Edge devices.</span></span> <span data-ttu-id="4692f-136">It has three components.</span><span class="sxs-lookup"><span data-stu-id="4692f-136">It has three components.</span></span> <span data-ttu-id="4692f-137">The **IoT Edge security daemon** starts each time an Edge device boots and bootstraps the device by starting the IoT Edge agent.</span><span class="sxs-lookup"><span data-stu-id="4692f-137">The **IoT Edge security daemon** starts each time an Edge device boots and bootstraps the device by starting the IoT Edge agent.</span></span> <span data-ttu-id="4692f-138">The **IoT Edge agent** facilitates deployment and monitoring of modules on the IoT Edge device, including the IoT Edge hub.</span><span class="sxs-lookup"><span data-stu-id="4692f-138">The **IoT Edge agent** facilitates deployment and monitoring of modules on the IoT Edge device, including the IoT Edge hub.</span></span> <span data-ttu-id="4692f-139">The **IoT Edge hub** manages communications between modules on the IoT Edge device, and between the device and IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4692f-139">The **IoT Edge hub** manages communications between modules on the IoT Edge device, and between the device and IoT Hub.</span></span> 

<span data-ttu-id="4692f-140">Complete the following steps in the Linux machine or VM that you prepared for this quickstart.</span><span class="sxs-lookup"><span data-stu-id="4692f-140">Complete the following steps in the Linux machine or VM that you prepared for this quickstart.</span></span> 

### <a name="register-your-device-to-use-the-software-repository"></a><span data-ttu-id="4692f-141">Register your device to use the software repository</span><span class="sxs-lookup"><span data-stu-id="4692f-141">Register your device to use the software repository</span></span>

<span data-ttu-id="4692f-142">The packages that you need to run the IoT Edge runtime are managed in a software repository.</span><span class="sxs-lookup"><span data-stu-id="4692f-142">The packages that you need to run the IoT Edge runtime are managed in a software repository.</span></span> <span data-ttu-id="4692f-143">Configure your IoT Edge device to access this repository.</span><span class="sxs-lookup"><span data-stu-id="4692f-143">Configure your IoT Edge device to access this repository.</span></span> 

<span data-ttu-id="4692f-144">The steps in this section are for devices running **Ubuntu 16.04**.</span><span class="sxs-lookup"><span data-stu-id="4692f-144">The steps in this section are for devices running **Ubuntu 16.04**.</span></span> <span data-ttu-id="4692f-145">To access the software repository on other versions of Linux, see [Install the Azure IoT Edge runtime on Linux (x64)](how-to-install-iot-edge-linux.md) or [Install Azure IoT Edge runtime on Linux (ARM32v7/armhf)](how-to-install-iot-edge-linux-arm.md).</span><span class="sxs-lookup"><span data-stu-id="4692f-145">To access the software repository on other versions of Linux, see [Install the Azure IoT Edge runtime on Linux (x64)](how-to-install-iot-edge-linux.md) or [Install Azure IoT Edge runtime on Linux (ARM32v7/armhf)](how-to-install-iot-edge-linux-arm.md).</span></span>

1. <span data-ttu-id="4692f-146">On the machine that you're using as an IoT Edge device, install the repository configuration.</span><span class="sxs-lookup"><span data-stu-id="4692f-146">On the machine that you're using as an IoT Edge device, install the repository configuration.</span></span>

   ```bash
   curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > ./microsoft-prod.list
   sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
   ```

2. <span data-ttu-id="4692f-147">Install a public key to access the repository.</span><span class="sxs-lookup"><span data-stu-id="4692f-147">Install a public key to access the repository.</span></span>

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
   sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
   ```

### <a name="install-a-container-runtime"></a><span data-ttu-id="4692f-148">Install a container runtime</span><span class="sxs-lookup"><span data-stu-id="4692f-148">Install a container runtime</span></span>

<span data-ttu-id="4692f-149">The IoT Edge runtime is a set of containers, and the logic that you deploy to your IoT Edge device is packaged as containers.</span><span class="sxs-lookup"><span data-stu-id="4692f-149">The IoT Edge runtime is a set of containers, and the logic that you deploy to your IoT Edge device is packaged as containers.</span></span> <span data-ttu-id="4692f-150">Prepare your device for these components by installing a container runtime.</span><span class="sxs-lookup"><span data-stu-id="4692f-150">Prepare your device for these components by installing a container runtime.</span></span>

<span data-ttu-id="4692f-151">Update **apt-get**.</span><span class="sxs-lookup"><span data-stu-id="4692f-151">Update **apt-get**.</span></span>

   ```bash
   sudo apt-get update
   ```

<span data-ttu-id="4692f-152">Install **Moby**, a container runtime.</span><span class="sxs-lookup"><span data-stu-id="4692f-152">Install **Moby**, a container runtime.</span></span>

   ```bash
   sudo apt-get install moby-engine
   ```

<span data-ttu-id="4692f-153">Install the CLI commands for Moby.</span><span class="sxs-lookup"><span data-stu-id="4692f-153">Install the CLI commands for Moby.</span></span> 

   ```bash
   sudo apt-get install moby-cli
   ```

### <a name="install-and-configure-the-iot-edge-security-daemon"></a><span data-ttu-id="4692f-154">Install and configure the IoT Edge security daemon</span><span class="sxs-lookup"><span data-stu-id="4692f-154">Install and configure the IoT Edge security daemon</span></span>

<span data-ttu-id="4692f-155">The security daemon installs as a system service so that the IoT Edge runtime starts every time your device boots.</span><span class="sxs-lookup"><span data-stu-id="4692f-155">The security daemon installs as a system service so that the IoT Edge runtime starts every time your device boots.</span></span> <span data-ttu-id="4692f-156">The installation also includes a version of **hsmlib** that allows the security daemon to interact with the device's hardware security.</span><span class="sxs-lookup"><span data-stu-id="4692f-156">The installation also includes a version of **hsmlib** that allows the security daemon to interact with the device's hardware security.</span></span> 

1. <span data-ttu-id="4692f-157">Download and install the IoT Edge Security Daemon.</span><span class="sxs-lookup"><span data-stu-id="4692f-157">Download and install the IoT Edge Security Daemon.</span></span> 

   ```bash
   sudo apt-get update
   sudo apt-get install iotedge
   ```

2. <span data-ttu-id="4692f-158">Open the IoT Edge configuration file.</span><span class="sxs-lookup"><span data-stu-id="4692f-158">Open the IoT Edge configuration file.</span></span> <span data-ttu-id="4692f-159">It is a protected file so you may have to use elevated privileges to access it.</span><span class="sxs-lookup"><span data-stu-id="4692f-159">It is a protected file so you may have to use elevated privileges to access it.</span></span>
   
   ```bash
   sudo nano /etc/iotedge/config.yaml
   ```

3. <span data-ttu-id="4692f-160">Add the IoT Edge device connection string.</span><span class="sxs-lookup"><span data-stu-id="4692f-160">Add the IoT Edge device connection string.</span></span> <span data-ttu-id="4692f-161">Find the variable **device_connection_string** and update its value with the string that you copied after registering your device.</span><span class="sxs-lookup"><span data-stu-id="4692f-161">Find the variable **device_connection_string** and update its value with the string that you copied after registering your device.</span></span>

4. <span data-ttu-id="4692f-162">Save and close the file.</span><span class="sxs-lookup"><span data-stu-id="4692f-162">Save and close the file.</span></span> 

   <span data-ttu-id="4692f-163">`CTRL + X`, `Y`, `Enter`</span><span class="sxs-lookup"><span data-stu-id="4692f-163">`CTRL + X`, `Y`, `Enter`</span></span>

4. <span data-ttu-id="4692f-164">Restart the IoT Edge security daemon.</span><span class="sxs-lookup"><span data-stu-id="4692f-164">Restart the IoT Edge security daemon.</span></span>

   ```bash
   sudo systemctl restart iotedge
   ```

5. <span data-ttu-id="4692f-165">Check to see that the Edge Security Daemon is running as a system service.</span><span class="sxs-lookup"><span data-stu-id="4692f-165">Check to see that the Edge Security Daemon is running as a system service.</span></span>

   ```bash
   sudo systemctl status iotedge
   ```

   ![See the Edge Daemon running as a system service](./media/quickstart-linux/iotedged-running.png)

   <span data-ttu-id="4692f-167">You can also see logs from the Edge Security Daemon by running the following command:</span><span class="sxs-lookup"><span data-stu-id="4692f-167">You can also see logs from the Edge Security Daemon by running the following command:</span></span>

   ```bash
   journalctl -u iotedge
   ```

6. <span data-ttu-id="4692f-168">View the modules running on your device.</span><span class="sxs-lookup"><span data-stu-id="4692f-168">View the modules running on your device.</span></span> 

   >[!TIP]
   ><span data-ttu-id="4692f-169">You need to use *sudo* to run `iotedge` commands at first.</span><span class="sxs-lookup"><span data-stu-id="4692f-169">You need to use *sudo* to run `iotedge` commands at first.</span></span> <span data-ttu-id="4692f-170">Sign out of your machine and sign back in to update permissions, then you can run `iotedge` commands without elevated privileges.</span><span class="sxs-lookup"><span data-stu-id="4692f-170">Sign out of your machine and sign back in to update permissions, then you can run `iotedge` commands without elevated privileges.</span></span> 

   ```bash
   sudo iotedge list
   ```

   ![View one module on your device](./media/quickstart-linux/iotedge-list-1.png)

## <a name="deploy-a-module"></a><span data-ttu-id="4692f-172">Deploy a module</span><span class="sxs-lookup"><span data-stu-id="4692f-172">Deploy a module</span></span>

<span data-ttu-id="4692f-173">Manage your Azure IoT Edge device from the cloud to deploy a module that will send telemetry data to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4692f-173">Manage your Azure IoT Edge device from the cloud to deploy a module that will send telemetry data to IoT Hub.</span></span>
<span data-ttu-id="4692f-174">![Register a device][6]</span><span class="sxs-lookup"><span data-stu-id="4692f-174">![Register a device][6]</span></span>

[!INCLUDE [iot-edge-deploy-module](../../includes/iot-edge-deploy-module.md)]


## <a name="view-generated-data"></a><span data-ttu-id="4692f-175">View generated data</span><span class="sxs-lookup"><span data-stu-id="4692f-175">View generated data</span></span>

<span data-ttu-id="4692f-176">In this quickstart, you created a new IoT Edge device and installed the IoT Edge runtime on it.</span><span class="sxs-lookup"><span data-stu-id="4692f-176">In this quickstart, you created a new IoT Edge device and installed the IoT Edge runtime on it.</span></span> <span data-ttu-id="4692f-177">Then, you used the Azure portal to push an IoT Edge module to run on the device without having to make changes to the device itself.</span><span class="sxs-lookup"><span data-stu-id="4692f-177">Then, you used the Azure portal to push an IoT Edge module to run on the device without having to make changes to the device itself.</span></span> <span data-ttu-id="4692f-178">In this case, the module that you pushed creates environmental data that you can use for the tutorials.</span><span class="sxs-lookup"><span data-stu-id="4692f-178">In this case, the module that you pushed creates environmental data that you can use for the tutorials.</span></span> 

<span data-ttu-id="4692f-179">Open the command prompt on the computer running your simulated device again.</span><span class="sxs-lookup"><span data-stu-id="4692f-179">Open the command prompt on the computer running your simulated device again.</span></span> <span data-ttu-id="4692f-180">Confirm that the module deployed from the cloud is running on your IoT Edge device:</span><span class="sxs-lookup"><span data-stu-id="4692f-180">Confirm that the module deployed from the cloud is running on your IoT Edge device:</span></span>

   ```bash
   sudo iotedge list
   ```

   ![View three modules on your device](./media/quickstart-linux/iotedge-list-2.png)

<span data-ttu-id="4692f-182">View the messages being sent from the tempSensor module:</span><span class="sxs-lookup"><span data-stu-id="4692f-182">View the messages being sent from the tempSensor module:</span></span>

  ```bash
   sudo iotedge logs tempSensor -f 
   ```

<span data-ttu-id="4692f-183">After a logoff and login, *sudo* is not required for the above command.</span><span class="sxs-lookup"><span data-stu-id="4692f-183">After a logoff and login, *sudo* is not required for the above command.</span></span>

![View the data from your module](./media/quickstart-linux/iotedge-logs.png)

<span data-ttu-id="4692f-185">The temperature sensor module may be waiting to connect to Edge Hub if the last line you see in the log is `Using transport Mqtt_Tcp_Only`.</span><span class="sxs-lookup"><span data-stu-id="4692f-185">The temperature sensor module may be waiting to connect to Edge Hub if the last line you see in the log is `Using transport Mqtt_Tcp_Only`.</span></span> <span data-ttu-id="4692f-186">Try killing the module and letting the Edge Agent restart it.</span><span class="sxs-lookup"><span data-stu-id="4692f-186">Try killing the module and letting the Edge Agent restart it.</span></span> <span data-ttu-id="4692f-187">You can kill it with the command `sudo docker stop tempSensor`.</span><span class="sxs-lookup"><span data-stu-id="4692f-187">You can kill it with the command `sudo docker stop tempSensor`.</span></span>

<span data-ttu-id="4692f-188">You can also view the telemetry the device is sending by using the [Azure IoT Toolkit extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-toolkit).</span><span class="sxs-lookup"><span data-stu-id="4692f-188">You can also view the telemetry the device is sending by using the [Azure IoT Toolkit extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-toolkit).</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="4692f-189">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="4692f-189">Clean up resources</span></span>

<span data-ttu-id="4692f-190">If you want to continue on to the IoT Edge tutorials, you can use the device that you registered and set up in this quickstart.</span><span class="sxs-lookup"><span data-stu-id="4692f-190">If you want to continue on to the IoT Edge tutorials, you can use the device that you registered and set up in this quickstart.</span></span> <span data-ttu-id="4692f-191">Otherwise, you can delete the Azure resources that you created and remove the IoT Edge runtime from your device.</span><span class="sxs-lookup"><span data-stu-id="4692f-191">Otherwise, you can delete the Azure resources that you created and remove the IoT Edge runtime from your device.</span></span> 

### <a name="delete-azure-resources"></a><span data-ttu-id="4692f-192">Delete Azure resources</span><span class="sxs-lookup"><span data-stu-id="4692f-192">Delete Azure resources</span></span>

<span data-ttu-id="4692f-193">If you created your virtual machine and IoT hub in a new resource group, you can delete that group and all the associated resources.</span><span class="sxs-lookup"><span data-stu-id="4692f-193">If you created your virtual machine and IoT hub in a new resource group, you can delete that group and all the associated resources.</span></span> <span data-ttu-id="4692f-194">If there's anything in that resource group that you want to keep, then just delete the individual resources that you want to clean up.</span><span class="sxs-lookup"><span data-stu-id="4692f-194">If there's anything in that resource group that you want to keep, then just delete the individual resources that you want to clean up.</span></span> 

<span data-ttu-id="4692f-195">To remove a resource group, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="4692f-195">To remove a resource group, follow these steps:</span></span> 

1. <span data-ttu-id="4692f-196">Sign in to the [Azure portal](https://portal.azure.com) and click **Resource groups**.</span><span class="sxs-lookup"><span data-stu-id="4692f-196">Sign in to the [Azure portal](https://portal.azure.com) and click **Resource groups**.</span></span>
2. <span data-ttu-id="4692f-197">In the **Filter by name...** textbox, type the name of the resource group containing your IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4692f-197">In the **Filter by name...** textbox, type the name of the resource group containing your IoT Hub.</span></span> 
3. <span data-ttu-id="4692f-198">To the right of your resource group in the result list, click **...** then **Delete resource group**.</span><span class="sxs-lookup"><span data-stu-id="4692f-198">To the right of your resource group in the result list, click **...** then **Delete resource group**.</span></span>
4. <span data-ttu-id="4692f-199">You will be asked to confirm the deletion of the resource group.</span><span class="sxs-lookup"><span data-stu-id="4692f-199">You will be asked to confirm the deletion of the resource group.</span></span> <span data-ttu-id="4692f-200">Type the name of your resource group again to confirm, and then click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="4692f-200">Type the name of your resource group again to confirm, and then click **Delete**.</span></span> <span data-ttu-id="4692f-201">After a few moments, the resource group and all of its contained resources are deleted.</span><span class="sxs-lookup"><span data-stu-id="4692f-201">After a few moments, the resource group and all of its contained resources are deleted.</span></span>

### <a name="remove-the-iot-edge-runtime"></a><span data-ttu-id="4692f-202">Remove the IoT Edge runtime</span><span class="sxs-lookup"><span data-stu-id="4692f-202">Remove the IoT Edge runtime</span></span>

<span data-ttu-id="4692f-203">If you want to remove the installations from your device, use the following commands.</span><span class="sxs-lookup"><span data-stu-id="4692f-203">If you want to remove the installations from your device, use the following commands.</span></span>  

<span data-ttu-id="4692f-204">Remove the IoT Edge runtime.</span><span class="sxs-lookup"><span data-stu-id="4692f-204">Remove the IoT Edge runtime.</span></span>

   ```bash
   sudo apt-get remove --purge iotedge
   ```

<span data-ttu-id="4692f-205">When the IoT Edge runtime is removed, the containers that it created are stopped, but still exist on your device.</span><span class="sxs-lookup"><span data-stu-id="4692f-205">When the IoT Edge runtime is removed, the containers that it created are stopped, but still exist on your device.</span></span> <span data-ttu-id="4692f-206">View all containers.</span><span class="sxs-lookup"><span data-stu-id="4692f-206">View all containers.</span></span>

   ```bash
   sudo docker ps -a
   ```

<span data-ttu-id="4692f-207">Delete the containers that were created on your device by the IoT Edge runtime.</span><span class="sxs-lookup"><span data-stu-id="4692f-207">Delete the containers that were created on your device by the IoT Edge runtime.</span></span> <span data-ttu-id="4692f-208">Change the name of the tempSensor container if you called it something different.</span><span class="sxs-lookup"><span data-stu-id="4692f-208">Change the name of the tempSensor container if you called it something different.</span></span> 

   ```bash
   sudo docker rm -f tempSensor
   sudo docker rm -f edgeHub
   sudo docker rm -f edgeAgent
   ```

<span data-ttu-id="4692f-209">Remove the container runtime.</span><span class="sxs-lookup"><span data-stu-id="4692f-209">Remove the container runtime.</span></span>

   ```bash
   sudo apt-get remove --purge moby
   ```

## <a name="next-steps"></a><span data-ttu-id="4692f-210">Next steps</span><span class="sxs-lookup"><span data-stu-id="4692f-210">Next steps</span></span>

<span data-ttu-id="4692f-211">In this quickstart, you created a new IoT Edge device and used the Azure IoT Edge cloud interface to deploy code onto the device.</span><span class="sxs-lookup"><span data-stu-id="4692f-211">In this quickstart, you created a new IoT Edge device and used the Azure IoT Edge cloud interface to deploy code onto the device.</span></span> <span data-ttu-id="4692f-212">Now, you have a simulated device generating raw data about its environment.</span><span class="sxs-lookup"><span data-stu-id="4692f-212">Now, you have a simulated device generating raw data about its environment.</span></span> 

<span data-ttu-id="4692f-213">This quickstart is the prerequisite for all of the IoT Edge tutorials.</span><span class="sxs-lookup"><span data-stu-id="4692f-213">This quickstart is the prerequisite for all of the IoT Edge tutorials.</span></span> <span data-ttu-id="4692f-214">You can continue on to any of the tutorials to learn how Azure IoT Edge can help you turn this data into business insights at the edge.</span><span class="sxs-lookup"><span data-stu-id="4692f-214">You can continue on to any of the tutorials to learn how Azure IoT Edge can help you turn this data into business insights at the edge.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4692f-215">Filter sensor data using an Azure Function</span><span class="sxs-lookup"><span data-stu-id="4692f-215">Filter sensor data using an Azure Function</span></span>](tutorial-deploy-function.md)


<!-- Images -->
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
[lnk-account]: https://azure.microsoft.com/free
[lnk-docker-ubuntu]: https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/ 
