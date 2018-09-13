---
title: Auto-provision Azure IoT Edge device with DPS - Linux | Microsoft Docs
description: Use a simulated TPM on a Linux VM to test device provisioning for Azure IoT Edge
author: kgremban
manager: timlt
ms.author: kgremban
ms.date: 06/27/2018
ms.topic: conceptual
ms.service: iot-edge
services: iot-edge
ms.openlocfilehash: 9609aab6c70bc0c2755de142023bd26e7417987a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856971"
---
# <a name="create-and-provision-an-edge-device-with-a-virtual-tpm-on-a-linux-virtual-machine"></a><span data-ttu-id="fa34f-103">Create and provision an Edge device with a virtual TPM on a Linux virtual machine</span><span class="sxs-lookup"><span data-stu-id="fa34f-103">Create and provision an Edge device with a virtual TPM on a Linux virtual machine</span></span>

<span data-ttu-id="fa34f-104">Azure IoT Edge devices can be auto-provisioned using the [Device Provisioning Service](../iot-dps/index.yml) just like devices that are not edge-enabled.</span><span class="sxs-lookup"><span data-stu-id="fa34f-104">Azure IoT Edge devices can be auto-provisioned using the [Device Provisioning Service](../iot-dps/index.yml) just like devices that are not edge-enabled.</span></span> <span data-ttu-id="fa34f-105">If you're unfamiliar with the process of auto-provisioning, review the [auto-provisioning concepts](../iot-dps/concepts-auto-provisioning.md) before continuing.</span><span class="sxs-lookup"><span data-stu-id="fa34f-105">If you're unfamiliar with the process of auto-provisioning, review the [auto-provisioning concepts](../iot-dps/concepts-auto-provisioning.md) before continuing.</span></span> 

<span data-ttu-id="fa34f-106">This article shows you how to test auto-provisioning on a simulated Edge device with the following steps:</span><span class="sxs-lookup"><span data-stu-id="fa34f-106">This article shows you how to test auto-provisioning on a simulated Edge device with the following steps:</span></span> 

* <span data-ttu-id="fa34f-107">Create a Linux virtual machine (VM) in Hyper-V with a simulated Trusted Platform Module (TPM) for hardware security.</span><span class="sxs-lookup"><span data-stu-id="fa34f-107">Create a Linux virtual machine (VM) in Hyper-V with a simulated Trusted Platform Module (TPM) for hardware security.</span></span>
* <span data-ttu-id="fa34f-108">Create an instance of IoT Hub Device Provisioning Service (DPS).</span><span class="sxs-lookup"><span data-stu-id="fa34f-108">Create an instance of IoT Hub Device Provisioning Service (DPS).</span></span>
* <span data-ttu-id="fa34f-109">Create an individual enrollment for the device</span><span class="sxs-lookup"><span data-stu-id="fa34f-109">Create an individual enrollment for the device</span></span>
* <span data-ttu-id="fa34f-110">Install the IoT Edge runtime and connect the device to IoT Hub</span><span class="sxs-lookup"><span data-stu-id="fa34f-110">Install the IoT Edge runtime and connect the device to IoT Hub</span></span>

<span data-ttu-id="fa34f-111">The steps in this article are meant for testing purposes.</span><span class="sxs-lookup"><span data-stu-id="fa34f-111">The steps in this article are meant for testing purposes.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fa34f-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="fa34f-112">Prerequisites</span></span>

* <span data-ttu-id="fa34f-113">A Windows development machine with [Hyper-V enabled](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v).</span><span class="sxs-lookup"><span data-stu-id="fa34f-113">A Windows development machine with [Hyper-V enabled](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v).</span></span> <span data-ttu-id="fa34f-114">This article uses Windows 10 running an Ubuntu Server VM.</span><span class="sxs-lookup"><span data-stu-id="fa34f-114">This article uses Windows 10 running an Ubuntu Server VM.</span></span> 
* <span data-ttu-id="fa34f-115">An active IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="fa34f-115">An active IoT Hub.</span></span> 

## <a name="create-a-linux-virtual-machine-with-a-virtual-tpm"></a><span data-ttu-id="fa34f-116">Create a Linux virtual machine with a virtual TPM</span><span class="sxs-lookup"><span data-stu-id="fa34f-116">Create a Linux virtual machine with a virtual TPM</span></span>

<span data-ttu-id="fa34f-117">In this section, you create a new Linux virtual machine on Hyper-V that has a simulated TPM so that you can use it for testing how auto-provisioning works with IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="fa34f-117">In this section, you create a new Linux virtual machine on Hyper-V that has a simulated TPM so that you can use it for testing how auto-provisioning works with IoT Edge.</span></span> 

### <a name="create-a-virtual-switch"></a><span data-ttu-id="fa34f-118">Create a virtual switch</span><span class="sxs-lookup"><span data-stu-id="fa34f-118">Create a virtual switch</span></span>

<span data-ttu-id="fa34f-119">A virtual switch enables your virtual machine to connect to a physical network.</span><span class="sxs-lookup"><span data-stu-id="fa34f-119">A virtual switch enables your virtual machine to connect to a physical network.</span></span>

1. <span data-ttu-id="fa34f-120">Open Hyper-V on your windows machine.</span><span class="sxs-lookup"><span data-stu-id="fa34f-120">Open Hyper-V on your windows machine.</span></span> 

2. <span data-ttu-id="fa34f-121">In the **Actions** menu, select **Virtual Switch Manager**.</span><span class="sxs-lookup"><span data-stu-id="fa34f-121">In the **Actions** menu, select **Virtual Switch Manager**.</span></span> 

3. <span data-ttu-id="fa34f-122">Choose an **External** virtual switch, then select **Create Virtual Switch**.</span><span class="sxs-lookup"><span data-stu-id="fa34f-122">Choose an **External** virtual switch, then select **Create Virtual Switch**.</span></span> 

4. <span data-ttu-id="fa34f-123">Give your new virtual switch a name, for example **EdgeSwitch**.</span><span class="sxs-lookup"><span data-stu-id="fa34f-123">Give your new virtual switch a name, for example **EdgeSwitch**.</span></span> <span data-ttu-id="fa34f-124">Make sure that the connection type is set to **External network**, then select **Ok**.</span><span class="sxs-lookup"><span data-stu-id="fa34f-124">Make sure that the connection type is set to **External network**, then select **Ok**.</span></span>

5. <span data-ttu-id="fa34f-125">A pop-up warns you that network connectivity may be disrupted.</span><span class="sxs-lookup"><span data-stu-id="fa34f-125">A pop-up warns you that network connectivity may be disrupted.</span></span> <span data-ttu-id="fa34f-126">Select **Yes** to continue.</span><span class="sxs-lookup"><span data-stu-id="fa34f-126">Select **Yes** to continue.</span></span> 

<span data-ttu-id="fa34f-127">If you see errors while creating the new virtual switch, ensure that no other switches are using the ethernet adaptor, and that no other switches use the same name.</span><span class="sxs-lookup"><span data-stu-id="fa34f-127">If you see errors while creating the new virtual switch, ensure that no other switches are using the ethernet adaptor, and that no other switches use the same name.</span></span> 

### <a name="create-virtual-machine"></a><span data-ttu-id="fa34f-128">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="fa34f-128">Create virtual machine</span></span>

1. <span data-ttu-id="fa34f-129">Download a disk image file to use for your virtual machine and save it locally.</span><span class="sxs-lookup"><span data-stu-id="fa34f-129">Download a disk image file to use for your virtual machine and save it locally.</span></span> <span data-ttu-id="fa34f-130">For example, [Ubuntu server](https://www.ubuntu.com/download/server).</span><span class="sxs-lookup"><span data-stu-id="fa34f-130">For example, [Ubuntu server](https://www.ubuntu.com/download/server).</span></span> 

2. <span data-ttu-id="fa34f-131">Open Hyper-V again.</span><span class="sxs-lookup"><span data-stu-id="fa34f-131">Open Hyper-V again.</span></span> <span data-ttu-id="fa34f-132">In the **Actions** menu, select **New** > **Virtual Machine**.</span><span class="sxs-lookup"><span data-stu-id="fa34f-132">In the **Actions** menu, select **New** > **Virtual Machine**.</span></span>

3. <span data-ttu-id="fa34f-133">Complete the **New Virtual Machine Wizard** with the following specific configurations:</span><span class="sxs-lookup"><span data-stu-id="fa34f-133">Complete the **New Virtual Machine Wizard** with the following specific configurations:</span></span>

   1. <span data-ttu-id="fa34f-134">**Specify Generation**: Select **Generation 2**.</span><span class="sxs-lookup"><span data-stu-id="fa34f-134">**Specify Generation**: Select **Generation 2**.</span></span>
   2. <span data-ttu-id="fa34f-135">**Configure Networking**: Set the value of **Connection** to the virtual switch that you created in the previous section.</span><span class="sxs-lookup"><span data-stu-id="fa34f-135">**Configure Networking**: Set the value of **Connection** to the virtual switch that you created in the previous section.</span></span> 
   3. <span data-ttu-id="fa34f-136">**Installation Oprtions**: Select **Install an operating system from a bootable image file** and browse to the disk image file that you saved locally.</span><span class="sxs-lookup"><span data-stu-id="fa34f-136">**Installation Oprtions**: Select **Install an operating system from a bootable image file** and browse to the disk image file that you saved locally.</span></span>

<span data-ttu-id="fa34f-137">It may take a view minutes to create the new VM.</span><span class="sxs-lookup"><span data-stu-id="fa34f-137">It may take a view minutes to create the new VM.</span></span> 

### <a name="enable-virtual-tpm"></a><span data-ttu-id="fa34f-138">Enable virtual TPM</span><span class="sxs-lookup"><span data-stu-id="fa34f-138">Enable virtual TPM</span></span>

1. <span data-ttu-id="fa34f-139">Once your VM is created, open its settings.</span><span class="sxs-lookup"><span data-stu-id="fa34f-139">Once your VM is created, open its settings.</span></span> 
2. <span data-ttu-id="fa34f-140">Navigate to **Security**.</span><span class="sxs-lookup"><span data-stu-id="fa34f-140">Navigate to **Security**.</span></span> 
3. <span data-ttu-id="fa34f-141">Uncheck **Enable Secure Boot**.</span><span class="sxs-lookup"><span data-stu-id="fa34f-141">Uncheck **Enable Secure Boot**.</span></span>
4. <span data-ttu-id="fa34f-142">Check **Enable Trusted Platform Module**.</span><span class="sxs-lookup"><span data-stu-id="fa34f-142">Check **Enable Trusted Platform Module**.</span></span> 
5. <span data-ttu-id="fa34f-143">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="fa34f-143">Click **OK**.</span></span>  

### <a name="start-the-virtual-machine-and-collect-tpm-data"></a><span data-ttu-id="fa34f-144">Start the virtual machine and collect TPM data</span><span class="sxs-lookup"><span data-stu-id="fa34f-144">Start the virtual machine and collect TPM data</span></span>

<span data-ttu-id="fa34f-145">In the virtual machine, build a C SDK tool that you can use to retrieve the device's **Registration ID** and **Endorsement Key**.</span><span class="sxs-lookup"><span data-stu-id="fa34f-145">In the virtual machine, build a C SDK tool that you can use to retrieve the device's **Registration ID** and **Endorsement Key**.</span></span> 

1. <span data-ttu-id="fa34f-146">Start your VM and connect to it to finish the installation process.</span><span class="sxs-lookup"><span data-stu-id="fa34f-146">Start your VM and connect to it to finish the installation process.</span></span> 

2. <span data-ttu-id="fa34f-147">In your VM, follow the steps in [Set up a Linux development environment](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md#linux) to install and build the Azure IoT device SDK for C.</span><span class="sxs-lookup"><span data-stu-id="fa34f-147">In your VM, follow the steps in [Set up a Linux development environment](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md#linux) to install and build the Azure IoT device SDK for C.</span></span> 

3. <span data-ttu-id="fa34f-148">Run the following commands to build an C SDK tool that retrieves your device provisioning information.</span><span class="sxs-lookup"><span data-stu-id="fa34f-148">Run the following commands to build an C SDK tool that retrieves your device provisioning information.</span></span> 

   ```bash
   cd azure-iot-sdk-c/cmake
   cmake -Duse_prov_client:BOOL=ON ..
   cd provisioning_client/tools/tpm_device_provision
   make
   sudo ./tpm_device_provision
   ```

3. <span data-ttu-id="fa34f-149">Copy the values for **Registration ID** and **Endorsement Key**.</span><span class="sxs-lookup"><span data-stu-id="fa34f-149">Copy the values for **Registration ID** and **Endorsement Key**.</span></span> <span data-ttu-id="fa34f-150">You use these values to create an individual enrollment for your device in DPS.</span><span class="sxs-lookup"><span data-stu-id="fa34f-150">You use these values to create an individual enrollment for your device in DPS.</span></span> 

## <a name="set-up-the-iot-hub-device-provisioning-service"></a><span data-ttu-id="fa34f-151">Set up the IoT Hub Device Provisioning Service</span><span class="sxs-lookup"><span data-stu-id="fa34f-151">Set up the IoT Hub Device Provisioning Service</span></span>

<span data-ttu-id="fa34f-152">Create a new instance of the IoT Hub Device Provisioning Service in Azure, and link it to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="fa34f-152">Create a new instance of the IoT Hub Device Provisioning Service in Azure, and link it to your IoT hub.</span></span> <span data-ttu-id="fa34f-153">You can follow the instructions in [Set up the IoT Hub DPS](../iot-dps/quick-setup-auto-provision.md).</span><span class="sxs-lookup"><span data-stu-id="fa34f-153">You can follow the instructions in [Set up the IoT Hub DPS](../iot-dps/quick-setup-auto-provision.md).</span></span>

<span data-ttu-id="fa34f-154">After you have the Device Provisioning Service running, copy the value of **ID Scope** from the overview page.</span><span class="sxs-lookup"><span data-stu-id="fa34f-154">After you have the Device Provisioning Service running, copy the value of **ID Scope** from the overview page.</span></span> <span data-ttu-id="fa34f-155">You use this value when you configure the IoT Edge runtime.</span><span class="sxs-lookup"><span data-stu-id="fa34f-155">You use this value when you configure the IoT Edge runtime.</span></span> 

## <a name="create-a-dps-enrollment"></a><span data-ttu-id="fa34f-156">Create a DPS enrollment</span><span class="sxs-lookup"><span data-stu-id="fa34f-156">Create a DPS enrollment</span></span>

<span data-ttu-id="fa34f-157">Retrieve the provisioning information from your virtual machine, and use that to create an individual enrollment in Device Provisioning Service.</span><span class="sxs-lookup"><span data-stu-id="fa34f-157">Retrieve the provisioning information from your virtual machine, and use that to create an individual enrollment in Device Provisioning Service.</span></span> 

<span data-ttu-id="fa34f-158">When you create an enrollment in DPS, you have the opportunity to declare an **Initial Device Twin State**.</span><span class="sxs-lookup"><span data-stu-id="fa34f-158">When you create an enrollment in DPS, you have the opportunity to declare an **Initial Device Twin State**.</span></span> <span data-ttu-id="fa34f-159">In the device twin you can set tags to group devices by any metric you need in your solution, like region, environment, location, or device type.</span><span class="sxs-lookup"><span data-stu-id="fa34f-159">In the device twin you can set tags to group devices by any metric you need in your solution, like region, environment, location, or device type.</span></span> <span data-ttu-id="fa34f-160">These tags are used to create [automatic deployments](how-to-deploy-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="fa34f-160">These tags are used to create [automatic deployments](how-to-deploy-monitor.md).</span></span> 


1. <span data-ttu-id="fa34f-161">In the [Azure portal](https://portal.azure.com), and navigate to your instance of IoT Hub Device Provisioning Service.</span><span class="sxs-lookup"><span data-stu-id="fa34f-161">In the [Azure portal](https://portal.azure.com), and navigate to your instance of IoT Hub Device Provisioning Service.</span></span> 

2. <span data-ttu-id="fa34f-162">Under **Settings**, select **Manage enrollments**.</span><span class="sxs-lookup"><span data-stu-id="fa34f-162">Under **Settings**, select **Manage enrollments**.</span></span> 

3. <span data-ttu-id="fa34f-163">Select **Add individual enrollment** then complete the following steps to configure the enrollment:</span><span class="sxs-lookup"><span data-stu-id="fa34f-163">Select **Add individual enrollment** then complete the following steps to configure the enrollment:</span></span>  

   1. <span data-ttu-id="fa34f-164">For **Mechanism**, select **TPM**.</span><span class="sxs-lookup"><span data-stu-id="fa34f-164">For **Mechanism**, select **TPM**.</span></span> 
   2. <span data-ttu-id="fa34f-165">Insert the **Endorsement key** and **Registration ID** that you copied from your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="fa34f-165">Insert the **Endorsement key** and **Registration ID** that you copied from your virtual machine.</span></span>
   3. <span data-ttu-id="fa34f-166">Select **Enable** to declare that this virtual machine is an IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="fa34f-166">Select **Enable** to declare that this virtual machine is an IoT Edge device.</span></span> 
   4. <span data-ttu-id="fa34f-167">Choose the linked **IoT Hub** that you want to connect your device to.</span><span class="sxs-lookup"><span data-stu-id="fa34f-167">Choose the linked **IoT Hub** that you want to connect your device to.</span></span> 
   5. <span data-ttu-id="fa34f-168">Provide an ID for your device if you'd like.</span><span class="sxs-lookup"><span data-stu-id="fa34f-168">Provide an ID for your device if you'd like.</span></span> <span data-ttu-id="fa34f-169">You can use device IDs to target an individual device for module deployment.</span><span class="sxs-lookup"><span data-stu-id="fa34f-169">You can use device IDs to target an individual device for module deployment.</span></span> 
   6. <span data-ttu-id="fa34f-170">Add a tag value to the **Initial Device Twin State** if you'd like.</span><span class="sxs-lookup"><span data-stu-id="fa34f-170">Add a tag value to the **Initial Device Twin State** if you'd like.</span></span> <span data-ttu-id="fa34f-171">You can use tags to target groups of devices for module deployment.</span><span class="sxs-lookup"><span data-stu-id="fa34f-171">You can use tags to target groups of devices for module deployment.</span></span> 
   7. <span data-ttu-id="fa34f-172">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="fa34f-172">Select **Save**.</span></span> 


## <a name="install-the-iot-edge-runtime"></a><span data-ttu-id="fa34f-173">Install the IoT Edge runtime</span><span class="sxs-lookup"><span data-stu-id="fa34f-173">Install the IoT Edge runtime</span></span>

<span data-ttu-id="fa34f-174">The IoT Edge runtime is deployed on all IoT Edge devices.</span><span class="sxs-lookup"><span data-stu-id="fa34f-174">The IoT Edge runtime is deployed on all IoT Edge devices.</span></span> <span data-ttu-id="fa34f-175">Its components run in containers, and allow you to deploy additional containers to the device so that you can run code at the edge.</span><span class="sxs-lookup"><span data-stu-id="fa34f-175">Its components run in containers, and allow you to deploy additional containers to the device so that you can run code at the edge.</span></span> <span data-ttu-id="fa34f-176">Install the IoT Edge runtime on your virtual m achine.</span><span class="sxs-lookup"><span data-stu-id="fa34f-176">Install the IoT Edge runtime on your virtual m achine.</span></span> 

<span data-ttu-id="fa34f-177">Know your DPS **ID Scope** and device **Registration ID** before beginning the article that matches your device type.</span><span class="sxs-lookup"><span data-stu-id="fa34f-177">Know your DPS **ID Scope** and device **Registration ID** before beginning the article that matches your device type.</span></span> <span data-ttu-id="fa34f-178">If you installed the example Ubuntu server, use the **x64** instructions.</span><span class="sxs-lookup"><span data-stu-id="fa34f-178">If you installed the example Ubuntu server, use the **x64** instructions.</span></span> <span data-ttu-id="fa34f-179">Make sure to configure the IoT Edge runtime for automatic, not manual, provisioning.</span><span class="sxs-lookup"><span data-stu-id="fa34f-179">Make sure to configure the IoT Edge runtime for automatic, not manual, provisioning.</span></span> 

* [<span data-ttu-id="fa34f-180">Linux (x64)</span><span class="sxs-lookup"><span data-stu-id="fa34f-180">Linux (x64)</span></span>](how-to-install-iot-edge-linux.md)
* [<span data-ttu-id="fa34f-181">Linux (ARM32v7/armhf)</span><span class="sxs-lookup"><span data-stu-id="fa34f-181">Linux (ARM32v7/armhf)</span></span>](how-to-install-iot-edge-linux-arm.md)

## <a name="give-iot-edge-access-to-the-tpm"></a><span data-ttu-id="fa34f-182">Give IoT Edge access to the TPM</span><span class="sxs-lookup"><span data-stu-id="fa34f-182">Give IoT Edge access to the TPM</span></span>

<span data-ttu-id="fa34f-183">In order for the IoT Edge runtime to automatically provision your device, it needs access to the TPM.</span><span class="sxs-lookup"><span data-stu-id="fa34f-183">In order for the IoT Edge runtime to automatically provision your device, it needs access to the TPM.</span></span> 

<span data-ttu-id="fa34f-184">Use the following steps to give TPM access.</span><span class="sxs-lookup"><span data-stu-id="fa34f-184">Use the following steps to give TPM access.</span></span> <span data-ttu-id="fa34f-185">Alternatively, you can accomplish the same thing by overriding the systemd settings so that the *iotedge* service can run as root.</span><span class="sxs-lookup"><span data-stu-id="fa34f-185">Alternatively, you can accomplish the same thing by overriding the systemd settings so that the *iotedge* service can run as root.</span></span> 

1. <span data-ttu-id="fa34f-186">Find the file path to the TPM hardware module on your device and save it as a local variable.</span><span class="sxs-lookup"><span data-stu-id="fa34f-186">Find the file path to the TPM hardware module on your device and save it as a local variable.</span></span> 

   ```bash
   tpm=$(sudo find /sys -name dev -print | fgrep tpm | sed 's/.\{4\}$//')
   ```

2. <span data-ttu-id="fa34f-187">Create a new rule that will give the IoT Edge runtime access to tpm0.</span><span class="sxs-lookup"><span data-stu-id="fa34f-187">Create a new rule that will give the IoT Edge runtime access to tpm0.</span></span> 

   ```bash
   sudo touch /etc/udev/rules.d/tpmaccess.rules
   ```

3. <span data-ttu-id="fa34f-188">Open the rules file.</span><span class="sxs-lookup"><span data-stu-id="fa34f-188">Open the rules file.</span></span> 

   ```bash
   sudo nano /etc/udev/rules.d/tpmaccess.rules
   ```

4. <span data-ttu-id="fa34f-189">Copy the following access information into the rules file.</span><span class="sxs-lookup"><span data-stu-id="fa34f-189">Copy the following access information into the rules file.</span></span> 

   ```input 
   # allow iotedge access to tpm0
   KERNEL=="tpm0", SUBSYSTEM=="tpm", GROUP="iotedge", MODE="0660"
   ```

5. <span data-ttu-id="fa34f-190">Save and exit the file.</span><span class="sxs-lookup"><span data-stu-id="fa34f-190">Save and exit the file.</span></span> 

6. <span data-ttu-id="fa34f-191">Trigger the udev system to evaluate the new rule.</span><span class="sxs-lookup"><span data-stu-id="fa34f-191">Trigger the udev system to evaluate the new rule.</span></span> 

   ```bash
   /bin/udevadm trigger $tpm
   ```

7. <span data-ttu-id="fa34f-192">Verify that the rule was successfully applied.</span><span class="sxs-lookup"><span data-stu-id="fa34f-192">Verify that the rule was successfully applied.</span></span>

   ```bash
   ls -l /dev/tpm0
   ```

   <span data-ttu-id="fa34f-193">Successful output looks like the following:</span><span class="sxs-lookup"><span data-stu-id="fa34f-193">Successful output looks like the following:</span></span>

   ```output
   crw------- 1 root root 10, 224 Jun 28 22:34 /dev/tpm0
   ```

8. <span data-ttu-id="fa34f-194">Open the IoT Edge runtime overrides file.</span><span class="sxs-lookup"><span data-stu-id="fa34f-194">Open the IoT Edge runtime overrides file.</span></span> 

   ```bash
   sudo systemctl edit iotedge.service
   ```

9. <span data-ttu-id="fa34f-195">Add the following code to establish a TPM environment variable.</span><span class="sxs-lookup"><span data-stu-id="fa34f-195">Add the following code to establish a TPM environment variable.</span></span>

   ```input
   [Service]
   Environment=IOTEDGE_USE_TPM_DEVICE=ON
   ```

9. <span data-ttu-id="fa34f-196">Verify that the override was successful.</span><span class="sxs-lookup"><span data-stu-id="fa34f-196">Verify that the override was successful.</span></span>

   ```bash
   sudo systemctl cat iotedge.service
   ```

   <span data-ttu-id="fa34f-197">Successful output displays the **iotedge** default service variables, and then shows the environment variable that you set in **override.conf**.</span><span class="sxs-lookup"><span data-stu-id="fa34f-197">Successful output displays the **iotedge** default service variables, and then shows the environment variable that you set in **override.conf**.</span></span> 

12. <span data-ttu-id="fa34f-198">Reload the settings.</span><span class="sxs-lookup"><span data-stu-id="fa34f-198">Reload the settings.</span></span>

   ```bash
   sudo systemctl daemon-reload
   ```

## <a name="restart-the-iot-edge-runtime"></a><span data-ttu-id="fa34f-199">Restart the IoT Edge runtime</span><span class="sxs-lookup"><span data-stu-id="fa34f-199">Restart the IoT Edge runtime</span></span>

<span data-ttu-id="fa34f-200">Restart the IoT Edge runtime so that it picks up all the configuration changes that you made on the device.</span><span class="sxs-lookup"><span data-stu-id="fa34f-200">Restart the IoT Edge runtime so that it picks up all the configuration changes that you made on the device.</span></span> 

   ```bash
   sudo systemctl restart iotedge
   ```

<span data-ttu-id="fa34f-201">Check to see that the IoT Edge runtime is running.</span><span class="sxs-lookup"><span data-stu-id="fa34f-201">Check to see that the IoT Edge runtime is running.</span></span> 

   ```bash
   sudo systemctl status iotedge
   ```

<span data-ttu-id="fa34f-202">If you see provisioning errors, it may be that the configuration changes haven't taken effect yet.</span><span class="sxs-lookup"><span data-stu-id="fa34f-202">If you see provisioning errors, it may be that the configuration changes haven't taken effect yet.</span></span> <span data-ttu-id="fa34f-203">Try restarting the IoT Edge daemon gain.</span><span class="sxs-lookup"><span data-stu-id="fa34f-203">Try restarting the IoT Edge daemon gain.</span></span> 

   ```bash
   sudo systemctl daemon-reload
   ```
   
<span data-ttu-id="fa34f-204">Or, try restarting your virtual machine to see if the changes take effect on a fresh start.</span><span class="sxs-lookup"><span data-stu-id="fa34f-204">Or, try restarting your virtual machine to see if the changes take effect on a fresh start.</span></span> 

## <a name="verify-successful-installation"></a><span data-ttu-id="fa34f-205">Verify successful installation</span><span class="sxs-lookup"><span data-stu-id="fa34f-205">Verify successful installation</span></span>

<span data-ttu-id="fa34f-206">If the runtime started successfully, you can go into your IoT Hub and see that your new device was automatically provisioned and is ready to run IoT Edge modules.</span><span class="sxs-lookup"><span data-stu-id="fa34f-206">If the runtime started successfully, you can go into your IoT Hub and see that your new device was automatically provisioned and is ready to run IoT Edge modules.</span></span> 

<span data-ttu-id="fa34f-207">Check the status of the IoT Edge Daemon.</span><span class="sxs-lookup"><span data-stu-id="fa34f-207">Check the status of the IoT Edge Daemon.</span></span>

```cmd/sh
systemctl status iotedge
```

<span data-ttu-id="fa34f-208">Examine daemon logs.</span><span class="sxs-lookup"><span data-stu-id="fa34f-208">Examine daemon logs.</span></span>

```cmd/sh
journalctl -u iotedge --no-pager --no-full
```

<span data-ttu-id="fa34f-209">List running modules.</span><span class="sxs-lookup"><span data-stu-id="fa34f-209">List running modules.</span></span>

```cmd/sh
iotedge list
```


## <a name="next-steps"></a><span data-ttu-id="fa34f-210">Next steps</span><span class="sxs-lookup"><span data-stu-id="fa34f-210">Next steps</span></span>

<span data-ttu-id="fa34f-211">The Device Provisioning Service enrollment process lets you set the device ID and device twin tags at the same time as you provision the new device.</span><span class="sxs-lookup"><span data-stu-id="fa34f-211">The Device Provisioning Service enrollment process lets you set the device ID and device twin tags at the same time as you provision the new device.</span></span> <span data-ttu-id="fa34f-212">You can use those values to target individual devices or groups of devices using automatic device management.</span><span class="sxs-lookup"><span data-stu-id="fa34f-212">You can use those values to target individual devices or groups of devices using automatic device management.</span></span> <span data-ttu-id="fa34f-213">Learn how to [Deploy and monitor IoT Edge modules at scale using the Azure portal](how-to-deploy-monitor.md) or [using Azure CLI](how-to-deploy-monitor-cli.md)</span><span class="sxs-lookup"><span data-stu-id="fa34f-213">Learn how to [Deploy and monitor IoT Edge modules at scale using the Azure portal](how-to-deploy-monitor.md) or [using Azure CLI](how-to-deploy-monitor-cli.md)</span></span>
