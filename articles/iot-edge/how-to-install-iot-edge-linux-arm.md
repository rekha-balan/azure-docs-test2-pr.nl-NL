---
title: Install Azure IoT Edge on Linux ARM32 | Microsoft Docs
description: Azure IoT Edge installation instructions on Linux on ARM32 devices, like a Raspberry PI
author: kgremban
manager: timlt
ms.reviewer: veyalla
ms.service: iot-edge
services: iot-edge
ms.topic: conceptual
ms.date: 08/27/2018
ms.author: kgremban
ms.openlocfilehash: 3f4e914f12feab3c36fca604c1bb37ab1a61b66f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870607"
---
# <a name="install-azure-iot-edge-runtime-on-linux-arm32v7armhf"></a><span data-ttu-id="04664-103">Install Azure IoT Edge runtime on Linux (ARM32v7/armhf)</span><span class="sxs-lookup"><span data-stu-id="04664-103">Install Azure IoT Edge runtime on Linux (ARM32v7/armhf)</span></span>

<span data-ttu-id="04664-104">The Azure IoT Edge runtime is what turns a device into an IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="04664-104">The Azure IoT Edge runtime is what turns a device into an IoT Edge device.</span></span> <span data-ttu-id="04664-105">The runtime can be deployed on devices as small as a Raspberry Pi or as large as an industrial server.</span><span class="sxs-lookup"><span data-stu-id="04664-105">The runtime can be deployed on devices as small as a Raspberry Pi or as large as an industrial server.</span></span> <span data-ttu-id="04664-106">Once a device is configured with the IoT Edge runtime, you can start deploying business logic to it from the cloud.</span><span class="sxs-lookup"><span data-stu-id="04664-106">Once a device is configured with the IoT Edge runtime, you can start deploying business logic to it from the cloud.</span></span> 

<span data-ttu-id="04664-107">To learn more about how the IoT Edge runtime works and what components are included, see [Understand the Azure IoT Edge runtime and its architecture](iot-edge-runtime.md).</span><span class="sxs-lookup"><span data-stu-id="04664-107">To learn more about how the IoT Edge runtime works and what components are included, see [Understand the Azure IoT Edge runtime and its architecture](iot-edge-runtime.md).</span></span>

<span data-ttu-id="04664-108">This article lists the steps to install the Azure IoT Edge runtime on a Linux ARM32v7/armhf Edge device.</span><span class="sxs-lookup"><span data-stu-id="04664-108">This article lists the steps to install the Azure IoT Edge runtime on a Linux ARM32v7/armhf Edge device.</span></span> <span data-ttu-id="04664-109">For example, these steps would work for Raspberry Pi devices.</span><span class="sxs-lookup"><span data-stu-id="04664-109">For example, these steps would work for Raspberry Pi devices.</span></span> <span data-ttu-id="04664-110">Refer to [Azure IoT Edge support](support.md#operating-systems) for a list of ARM32 operating systems that are currently supported.</span><span class="sxs-lookup"><span data-stu-id="04664-110">Refer to [Azure IoT Edge support](support.md#operating-systems) for a list of ARM32 operating systems that are currently supported.</span></span> 

>[!NOTE]
><span data-ttu-id="04664-111">Packages in the Linux software repositories are subject to the license terms located in each package (/usr/share/doc/*package-name*).</span><span class="sxs-lookup"><span data-stu-id="04664-111">Packages in the Linux software repositories are subject to the license terms located in each package (/usr/share/doc/*package-name*).</span></span> <span data-ttu-id="04664-112">Read the license terms prior to using the package.</span><span class="sxs-lookup"><span data-stu-id="04664-112">Read the license terms prior to using the package.</span></span> <span data-ttu-id="04664-113">Your installation and use of the package constitutes your acceptance of these terms.</span><span class="sxs-lookup"><span data-stu-id="04664-113">Your installation and use of the package constitutes your acceptance of these terms.</span></span> <span data-ttu-id="04664-114">If you do not agree with the license terms, do not use the package.</span><span class="sxs-lookup"><span data-stu-id="04664-114">If you do not agree with the license terms, do not use the package.</span></span>

## <a name="install-the-container-runtime"></a><span data-ttu-id="04664-115">Install the container runtime</span><span class="sxs-lookup"><span data-stu-id="04664-115">Install the container runtime</span></span>

<span data-ttu-id="04664-116">Azure IoT Edge relies on an [OCI-compatible][lnk-oci] container runtime.</span><span class="sxs-lookup"><span data-stu-id="04664-116">Azure IoT Edge relies on an [OCI-compatible][lnk-oci] container runtime.</span></span> <span data-ttu-id="04664-117">For production scenarios, it is highly recommended you use the [Moby-based][lnk-moby] engine provided below.</span><span class="sxs-lookup"><span data-stu-id="04664-117">For production scenarios, it is highly recommended you use the [Moby-based][lnk-moby] engine provided below.</span></span> <span data-ttu-id="04664-118">It is the only container engine officially supported with Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="04664-118">It is the only container engine officially supported with Azure IoT Edge.</span></span> <span data-ttu-id="04664-119">Docker CE/EE container images are compatible with the Moby-based runtime.</span><span class="sxs-lookup"><span data-stu-id="04664-119">Docker CE/EE container images are compatible with the Moby-based runtime.</span></span>

<span data-ttu-id="04664-120">Commands below install both the Moby-based engine and command-line interface (CLI).</span><span class="sxs-lookup"><span data-stu-id="04664-120">Commands below install both the Moby-based engine and command-line interface (CLI).</span></span> <span data-ttu-id="04664-121">The CLI is useful for development but optional for production deployments.</span><span class="sxs-lookup"><span data-stu-id="04664-121">The CLI is useful for development but optional for production deployments.</span></span>

```bash

# You can copy the entire text from this code block and 
# paste in terminal. The comment lines will be ignored.

# Download and install the moby-engine
curl -L https://aka.ms/moby-engine-armhf-latest -o moby_engine.deb && sudo dpkg -i ./moby_engine.deb

# Download and install the moby-cli
curl -L https://aka.ms/moby-cli-armhf-latest -o moby_cli.deb && sudo dpkg -i ./moby_cli.deb

# Run apt-get fix
sudo apt-get install -f

```

## <a name="install-the-iot-edge-security-daemon"></a><span data-ttu-id="04664-122">Install the IoT Edge Security Daemon</span><span class="sxs-lookup"><span data-stu-id="04664-122">Install the IoT Edge Security Daemon</span></span>

<span data-ttu-id="04664-123">The **IoT Edge security daemon** provides and maintains security standards on the Edge device.</span><span class="sxs-lookup"><span data-stu-id="04664-123">The **IoT Edge security daemon** provides and maintains security standards on the Edge device.</span></span> <span data-ttu-id="04664-124">The daemon starts on every boot and bootstraps the device by starting the rest of the IoT Edge runtime.</span><span class="sxs-lookup"><span data-stu-id="04664-124">The daemon starts on every boot and bootstraps the device by starting the rest of the IoT Edge runtime.</span></span> 


```bash
# You can copy the entire text from this code block and 
# paste in terminal. The comment lines will be ignored.

# Download and install the standard libiothsm implementation
curl -L https://aka.ms/libiothsm-std-linux-armhf-latest -o libiothsm-std.deb && sudo dpkg -i ./libiothsm-std.deb

# Download and install the IoT Edge Security Daemon
curl -L https://aka.ms/iotedged-linux-armhf-latest -o iotedge.deb && sudo dpkg -i ./iotedge.deb

# Run apt-get fix
sudo apt-get install -f
```

## <a name="connect-your-device-to-an-iot-hub"></a><span data-ttu-id="04664-125">Connect your device to an IoT hub</span><span class="sxs-lookup"><span data-stu-id="04664-125">Connect your device to an IoT hub</span></span> 

<span data-ttu-id="04664-126">Configure the IoT Edge runtime to link your physical device with a device identity that exists in an Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="04664-126">Configure the IoT Edge runtime to link your physical device with a device identity that exists in an Azure IoT hub.</span></span> 

<span data-ttu-id="04664-127">The daemon can be configured using the configuration file at `/etc/iotedge/config.yaml`.</span><span class="sxs-lookup"><span data-stu-id="04664-127">The daemon can be configured using the configuration file at `/etc/iotedge/config.yaml`.</span></span> <span data-ttu-id="04664-128">The file is write-protected by default, you might need elevated permissions to edit it.</span><span class="sxs-lookup"><span data-stu-id="04664-128">The file is write-protected by default, you might need elevated permissions to edit it.</span></span>

<span data-ttu-id="04664-129">A single IoT Edge device can be provisioned manually using a device connections string provided by IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="04664-129">A single IoT Edge device can be provisioned manually using a device connections string provided by IoT Hub.</span></span> <span data-ttu-id="04664-130">Or, you can use the Device Provisioning Service to automatically provision devices, which is helpful when you have many devices to provision.</span><span class="sxs-lookup"><span data-stu-id="04664-130">Or, you can use the Device Provisioning Service to automatically provision devices, which is helpful when you have many devices to provision.</span></span> <span data-ttu-id="04664-131">Depending on your provisioning choice, choose the appropriate installation script.</span><span class="sxs-lookup"><span data-stu-id="04664-131">Depending on your provisioning choice, choose the appropriate installation script.</span></span> 

### <a name="option-1-manual-provisioning"></a><span data-ttu-id="04664-132">Option 1: Manual provisioning</span><span class="sxs-lookup"><span data-stu-id="04664-132">Option 1: Manual provisioning</span></span>

<span data-ttu-id="04664-133">To manually provision a device, you need to provide it with a [device connection string][lnk-dcs] that you can create by registering a new device in your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="04664-133">To manually provision a device, you need to provide it with a [device connection string][lnk-dcs] that you can create by registering a new device in your IoT hub.</span></span>


<span data-ttu-id="04664-134">Open the configuration file.</span><span class="sxs-lookup"><span data-stu-id="04664-134">Open the configuration file.</span></span> 

```bash
sudo nano /etc/iotedge/config.yaml
```

<span data-ttu-id="04664-135">Find the provisioning section of the file and uncomment the **manual** provisioning mode.</span><span class="sxs-lookup"><span data-stu-id="04664-135">Find the provisioning section of the file and uncomment the **manual** provisioning mode.</span></span> <span data-ttu-id="04664-136">Update the value of **device_connection_string** with the connection string from your IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="04664-136">Update the value of **device_connection_string** with the connection string from your IoT Edge device.</span></span>

   ```yaml
   provisioning:
     source: "manual"
     device_connection_string: "<ADD DEVICE CONNECTION STRING HERE>"
  
   # provisioning: 
   #   source: "dps"
   #   global_endpoint: "https://global.azure-devices-provisioning.net"
   #   scope_id: "{scope_id}"
   #   registration_id: "{registration_id}"
   ```

<span data-ttu-id="04664-137">Save and close the file.</span><span class="sxs-lookup"><span data-stu-id="04664-137">Save and close the file.</span></span> 

   <span data-ttu-id="04664-138">`CTRL + X`, `Y`, `Enter`</span><span class="sxs-lookup"><span data-stu-id="04664-138">`CTRL + X`, `Y`, `Enter`</span></span>

<span data-ttu-id="04664-139">After entering the provisioning information in the configuration file, restart the daemon:</span><span class="sxs-lookup"><span data-stu-id="04664-139">After entering the provisioning information in the configuration file, restart the daemon:</span></span>

```bash
sudo systemctl restart iotedge
```

### <a name="option-2-automatic-provisioning"></a><span data-ttu-id="04664-140">Option 2: Automatic provisioning</span><span class="sxs-lookup"><span data-stu-id="04664-140">Option 2: Automatic provisioning</span></span>

<span data-ttu-id="04664-141">To automatically provision a device, [set up Device Provisioning Service and retrieve your device registration ID][lnk-dps].</span><span class="sxs-lookup"><span data-stu-id="04664-141">To automatically provision a device, [set up Device Provisioning Service and retrieve your device registration ID][lnk-dps].</span></span> <span data-ttu-id="04664-142">Automatic provisioning only works with devices that have a Trusted Platform Module (TPM) chip.</span><span class="sxs-lookup"><span data-stu-id="04664-142">Automatic provisioning only works with devices that have a Trusted Platform Module (TPM) chip.</span></span> <span data-ttu-id="04664-143">For example, Raspberry Pi devices do not come with TPM by default.</span><span class="sxs-lookup"><span data-stu-id="04664-143">For example, Raspberry Pi devices do not come with TPM by default.</span></span> 

<span data-ttu-id="04664-144">Open the configuration file.</span><span class="sxs-lookup"><span data-stu-id="04664-144">Open the configuration file.</span></span> 

```bash
sudo nano /etc/iotedge/config.yaml
```

<span data-ttu-id="04664-145">Find the provisioning section of the file and uncomment the **dps** provisioning mode.</span><span class="sxs-lookup"><span data-stu-id="04664-145">Find the provisioning section of the file and uncomment the **dps** provisioning mode.</span></span> <span data-ttu-id="04664-146">Update the values of **scope_id** and **registration_id** with the values from your IoT Hub Device Provisioning service and your IoT Edge device with TPM.</span><span class="sxs-lookup"><span data-stu-id="04664-146">Update the values of **scope_id** and **registration_id** with the values from your IoT Hub Device Provisioning service and your IoT Edge device with TPM.</span></span> 

   ```yaml
   # provisioning:
   #   source: "manual"
   #   device_connection_string: "<ADD DEVICE CONNECTION STRING HERE>"
  
   provisioning: 
     source: "dps"
     global_endpoint: "https://global.azure-devices-provisioning.net"
     scope_id: "{scope_id}"
     registration_id: "{registration_id}"
   ```

<span data-ttu-id="04664-147">Save and close the file.</span><span class="sxs-lookup"><span data-stu-id="04664-147">Save and close the file.</span></span> 

   <span data-ttu-id="04664-148">`CTRL + X`, `Y`, `Enter`</span><span class="sxs-lookup"><span data-stu-id="04664-148">`CTRL + X`, `Y`, `Enter`</span></span>

<span data-ttu-id="04664-149">After entering the provisioning information in the configuration file, restart the daemon:</span><span class="sxs-lookup"><span data-stu-id="04664-149">After entering the provisioning information in the configuration file, restart the daemon:</span></span>

```bash
sudo systemctl restart iotedge
```


## <a name="verify-successful-installation"></a><span data-ttu-id="04664-150">Verify successful installation</span><span class="sxs-lookup"><span data-stu-id="04664-150">Verify successful installation</span></span>

<span data-ttu-id="04664-151">If you used the **manual configuration** steps in the previous section, the IoT Edge runtime should be successfully provisioned and running on your device.</span><span class="sxs-lookup"><span data-stu-id="04664-151">If you used the **manual configuration** steps in the previous section, the IoT Edge runtime should be successfully provisioned and running on your device.</span></span> <span data-ttu-id="04664-152">If you used the **automatic configuration** steps, then you need to complete some additional steps so that the runtime can register your device with your IoT hub on your behalf.</span><span class="sxs-lookup"><span data-stu-id="04664-152">If you used the **automatic configuration** steps, then you need to complete some additional steps so that the runtime can register your device with your IoT hub on your behalf.</span></span> <span data-ttu-id="04664-153">For next steps, see [Create and provision a simulated TPM Edge device on a Linux virtual machine](how-to-auto-provision-simulated-device-linux.md#give-iot-edge-access-to-the-tpm).</span><span class="sxs-lookup"><span data-stu-id="04664-153">For next steps, see [Create and provision a simulated TPM Edge device on a Linux virtual machine](how-to-auto-provision-simulated-device-linux.md#give-iot-edge-access-to-the-tpm).</span></span>

<span data-ttu-id="04664-154">You can check the status of the IoT Edge Daemon using:</span><span class="sxs-lookup"><span data-stu-id="04664-154">You can check the status of the IoT Edge Daemon using:</span></span>

```bash
systemctl status iotedge
```

<span data-ttu-id="04664-155">Examine daemon logs using:</span><span class="sxs-lookup"><span data-stu-id="04664-155">Examine daemon logs using:</span></span>

```bash
journalctl -u iotedge --no-pager --no-full
```

<span data-ttu-id="04664-156">And, list running modules with:</span><span class="sxs-lookup"><span data-stu-id="04664-156">And, list running modules with:</span></span>

```bash
sudo iotedge list
```

## <a name="tips-and-suggestions"></a><span data-ttu-id="04664-157">Tips and suggestions</span><span class="sxs-lookup"><span data-stu-id="04664-157">Tips and suggestions</span></span>

<span data-ttu-id="04664-158">You need elevated privileges to run `iotedge` commands.</span><span class="sxs-lookup"><span data-stu-id="04664-158">You need elevated privileges to run `iotedge` commands.</span></span> <span data-ttu-id="04664-159">After installing the runtime, sign out of your machine and sign back in to update your permissions automatically.</span><span class="sxs-lookup"><span data-stu-id="04664-159">After installing the runtime, sign out of your machine and sign back in to update your permissions automatically.</span></span> <span data-ttu-id="04664-160">Until then, use **sudo** in front of any `iotedge` the commands.</span><span class="sxs-lookup"><span data-stu-id="04664-160">Until then, use **sudo** in front of any `iotedge` the commands.</span></span>

<span data-ttu-id="04664-161">On resource constrained devices, it is highly recommended that you set the *OptimizeForPerformance* environment variable to *false* as per instructions in the [troubleshooting guide][lnk-trouble].</span><span class="sxs-lookup"><span data-stu-id="04664-161">On resource constrained devices, it is highly recommended that you set the *OptimizeForPerformance* environment variable to *false* as per instructions in the [troubleshooting guide][lnk-trouble].</span></span>

## <a name="next-steps"></a><span data-ttu-id="04664-162">Next steps</span><span class="sxs-lookup"><span data-stu-id="04664-162">Next steps</span></span>

<span data-ttu-id="04664-163">If you are having problems with the Edge runtime installing properly, refer to the [troubleshooting][lnk-trouble] page.</span><span class="sxs-lookup"><span data-stu-id="04664-163">If you are having problems with the Edge runtime installing properly, refer to the [troubleshooting][lnk-trouble] page.</span></span>

<!-- Links -->
[lnk-dcs]: how-to-register-device-portal.md
[lnk-dps]: how-to-auto-provision-simulated-device-linux.md
[lnk-trouble]: https://docs.microsoft.com/azure/iot-edge/troubleshoot#stability-issues-on-resource-constrained-devices
[lnk-oci]: https://www.opencontainers.org/
[lnk-moby]: https://mobyproject.org/
