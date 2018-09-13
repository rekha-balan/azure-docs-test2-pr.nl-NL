---
title: How to install Azure IoT Edge on Linux | Microsoft Docs
description: Azure IoT Edge installation instructions on Linux
author: kgremban
manager: timlt
ms.reviewer: veyalla
ms.service: iot-edge
services: iot-edge
ms.topic: conceptual
ms.date: 08/27/2018
ms.author: kgremban
ms.openlocfilehash: 56223b2ed8e9d9b1a08f5313940920113a650bfe
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871593"
---
# <a name="install-the-azure-iot-edge-runtime-on-linux-x64"></a><span data-ttu-id="e0b2b-103">Install the Azure IoT Edge runtime on Linux (x64)</span><span class="sxs-lookup"><span data-stu-id="e0b2b-103">Install the Azure IoT Edge runtime on Linux (x64)</span></span>

<span data-ttu-id="e0b2b-104">The Azure IoT Edge runtime is what turns a device into an IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-104">The Azure IoT Edge runtime is what turns a device into an IoT Edge device.</span></span> <span data-ttu-id="e0b2b-105">The runtime can be deployed on devices as small as a Raspberry Pi or as large as an industrial server.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-105">The runtime can be deployed on devices as small as a Raspberry Pi or as large as an industrial server.</span></span> <span data-ttu-id="e0b2b-106">Once a device is configured with the IoT Edge runtime, you can start deploying business logic to it from the cloud.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-106">Once a device is configured with the IoT Edge runtime, you can start deploying business logic to it from the cloud.</span></span> 

<span data-ttu-id="e0b2b-107">To learn more about how the IoT Edge runtime works and what components are included, see [Understand the Azure IoT Edge runtime and its architecture](iot-edge-runtime.md).</span><span class="sxs-lookup"><span data-stu-id="e0b2b-107">To learn more about how the IoT Edge runtime works and what components are included, see [Understand the Azure IoT Edge runtime and its architecture](iot-edge-runtime.md).</span></span>

<span data-ttu-id="e0b2b-108">This article lists the steps to install the Azure IoT Edge runtime on your Linux x64 (Intel/AMD) Edge device.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-108">This article lists the steps to install the Azure IoT Edge runtime on your Linux x64 (Intel/AMD) Edge device.</span></span> <span data-ttu-id="e0b2b-109">Refer to [Azure IoT Edge support](support.md#operating-systems) for a list of AMD64 operating systems that are currently supported.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-109">Refer to [Azure IoT Edge support](support.md#operating-systems) for a list of AMD64 operating systems that are currently supported.</span></span> 

>[!NOTE]
><span data-ttu-id="e0b2b-110">Packages in the Linux software repositories are subject to the license terms located in each package (/usr/share/doc/*package-name*).</span><span class="sxs-lookup"><span data-stu-id="e0b2b-110">Packages in the Linux software repositories are subject to the license terms located in each package (/usr/share/doc/*package-name*).</span></span> <span data-ttu-id="e0b2b-111">Read the license terms prior to using the package.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-111">Read the license terms prior to using the package.</span></span> <span data-ttu-id="e0b2b-112">Your installation and use of the package constitutes your acceptance of these terms.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-112">Your installation and use of the package constitutes your acceptance of these terms.</span></span> <span data-ttu-id="e0b2b-113">If you do not agree with the license terms, do not use the package.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-113">If you do not agree with the license terms, do not use the package.</span></span>

## <a name="register-microsoft-key-and-software-repository-feed"></a><span data-ttu-id="e0b2b-114">Register Microsoft key and software repository feed</span><span class="sxs-lookup"><span data-stu-id="e0b2b-114">Register Microsoft key and software repository feed</span></span>

<span data-ttu-id="e0b2b-115">Depending on your operating system, choose the appropriate scripts to prepare your device for the IoT Edge runtime installation.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-115">Depending on your operating system, choose the appropriate scripts to prepare your device for the IoT Edge runtime installation.</span></span> 

### <a name="ubuntu-1604"></a><span data-ttu-id="e0b2b-116">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="e0b2b-116">Ubuntu 16.04</span></span>

```bash
# Install repository configuration
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/

# Install Microsoft GPG public key
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

### <a name="ubuntu-1804"></a><span data-ttu-id="e0b2b-117">Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="e0b2b-117">Ubuntu 18.04</span></span>

```bash
# Install repository configuration
curl https://packages.microsoft.com/config/ubuntu/18.04/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/

# Install Microsoft GPG public key
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/

# Perform apt upgrade
sudo apt-get upgrade
```

## <a name="install-the-container-runtime"></a><span data-ttu-id="e0b2b-118">Install the container runtime</span><span class="sxs-lookup"><span data-stu-id="e0b2b-118">Install the container runtime</span></span> 

<span data-ttu-id="e0b2b-119">Azure IoT Edge relies on a [OCI-compatible][lnk-oci] container runtime.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-119">Azure IoT Edge relies on a [OCI-compatible][lnk-oci] container runtime.</span></span> <span data-ttu-id="e0b2b-120">For production scenarios, it is highly recommended you use the [Moby-based][lnk-moby] engine provided below.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-120">For production scenarios, it is highly recommended you use the [Moby-based][lnk-moby] engine provided below.</span></span> <span data-ttu-id="e0b2b-121">It is the only container engine officially supported with Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-121">It is the only container engine officially supported with Azure IoT Edge.</span></span> <span data-ttu-id="e0b2b-122">Docker CE/EE container images are compatible with the Moby runtime.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-122">Docker CE/EE container images are compatible with the Moby runtime.</span></span>

<span data-ttu-id="e0b2b-123">Update apt-get.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-123">Update apt-get.</span></span>

```bash
sudo apt-get update
```

<span data-ttu-id="e0b2b-124">Install the Moby engine.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-124">Install the Moby engine.</span></span> 

```bash
sudo apt-get install moby-engine
```

<span data-ttu-id="e0b2b-125">Install the Moby command-line interface (CLI).</span><span class="sxs-lookup"><span data-stu-id="e0b2b-125">Install the Moby command-line interface (CLI).</span></span> <span data-ttu-id="e0b2b-126">The CLI is useful for development but optional for production deployments.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-126">The CLI is useful for development but optional for production deployments.</span></span>

```bash
sudo apt-get install moby-cli
```

## <a name="install-the-azure-iot-edge-security-daemon"></a><span data-ttu-id="e0b2b-127">Install the Azure IoT Edge Security Daemon</span><span class="sxs-lookup"><span data-stu-id="e0b2b-127">Install the Azure IoT Edge Security Daemon</span></span>

<span data-ttu-id="e0b2b-128">The **IoT Edge security daemon** provides and maintains security standards on the Edge device.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-128">The **IoT Edge security daemon** provides and maintains security standards on the Edge device.</span></span> <span data-ttu-id="e0b2b-129">The daemon starts on every boot and bootstraps the device by starting the rest of the IoT Edge runtime.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-129">The daemon starts on every boot and bootstraps the device by starting the rest of the IoT Edge runtime.</span></span> 

<span data-ttu-id="e0b2b-130">The installation command also installs the standard version of the **iothsmlib** if not already present.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-130">The installation command also installs the standard version of the **iothsmlib** if not already present.</span></span>

<span data-ttu-id="e0b2b-131">Update apt-get.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-131">Update apt-get.</span></span>

```bash
sudo apt-get update
```

<span data-ttu-id="e0b2b-132">Install the security daemon.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-132">Install the security daemon.</span></span> <span data-ttu-id="e0b2b-133">The package is installed at `/etc/iotedge/`.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-133">The package is installed at `/etc/iotedge/`.</span></span>

```bash
sudo apt-get install iotedge
```

## <a name="configure-the-azure-iot-edge-security-daemon"></a><span data-ttu-id="e0b2b-134">Configure the Azure IoT Edge Security Daemon</span><span class="sxs-lookup"><span data-stu-id="e0b2b-134">Configure the Azure IoT Edge Security Daemon</span></span>

<span data-ttu-id="e0b2b-135">Configure the IoT Edge runtime to link your physical device with a device identity that exists in an Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-135">Configure the IoT Edge runtime to link your physical device with a device identity that exists in an Azure IoT hub.</span></span> 

<span data-ttu-id="e0b2b-136">The daemon can be configured using the configuration file at `/etc/iotedge/config.yaml`.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-136">The daemon can be configured using the configuration file at `/etc/iotedge/config.yaml`.</span></span> <span data-ttu-id="e0b2b-137">The file is write-protected by default, you might need elevated permissions to edit it.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-137">The file is write-protected by default, you might need elevated permissions to edit it.</span></span>

<span data-ttu-id="e0b2b-138">A single IoT Edge device can be provisioned manually using a device connections string provided by IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-138">A single IoT Edge device can be provisioned manually using a device connections string provided by IoT Hub.</span></span> <span data-ttu-id="e0b2b-139">Or, you can use the Device Provisioning Service to automatically provision devices, which is helpful when you have many devices to provision.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-139">Or, you can use the Device Provisioning Service to automatically provision devices, which is helpful when you have many devices to provision.</span></span> <span data-ttu-id="e0b2b-140">Depending on your provisioning choice, choose the appropriate installation script.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-140">Depending on your provisioning choice, choose the appropriate installation script.</span></span> 

### <a name="option-1-manual-provisioning"></a><span data-ttu-id="e0b2b-141">Option 1: Manual provisioning</span><span class="sxs-lookup"><span data-stu-id="e0b2b-141">Option 1: Manual provisioning</span></span>

<span data-ttu-id="e0b2b-142">To manually provision a device, you need to provide it with a [device connection string][lnk-dcs] that you can create by registering a new device in your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-142">To manually provision a device, you need to provide it with a [device connection string][lnk-dcs] that you can create by registering a new device in your IoT hub.</span></span>


<span data-ttu-id="e0b2b-143">Open the configuration file.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-143">Open the configuration file.</span></span> 

```bash
sudo nano /etc/iotedge/config.yaml
```

<span data-ttu-id="e0b2b-144">Find the provisioning section of the file and uncomment the **manual** provisioning mode.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-144">Find the provisioning section of the file and uncomment the **manual** provisioning mode.</span></span> <span data-ttu-id="e0b2b-145">Update the value of **device_connection_string** with the connection string from your IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-145">Update the value of **device_connection_string** with the connection string from your IoT Edge device.</span></span>

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

<span data-ttu-id="e0b2b-146">Save and close the file.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-146">Save and close the file.</span></span> 

   <span data-ttu-id="e0b2b-147">`CTRL + X`, `Y`, `Enter`</span><span class="sxs-lookup"><span data-stu-id="e0b2b-147">`CTRL + X`, `Y`, `Enter`</span></span>

<span data-ttu-id="e0b2b-148">After entering the provisioning information in the configuration file, restart the daemon:</span><span class="sxs-lookup"><span data-stu-id="e0b2b-148">After entering the provisioning information in the configuration file, restart the daemon:</span></span>

```bash
sudo systemctl restart iotedge
```

### <a name="option-2-automatic-provisioning"></a><span data-ttu-id="e0b2b-149">Option 2: Automatic provisioning</span><span class="sxs-lookup"><span data-stu-id="e0b2b-149">Option 2: Automatic provisioning</span></span>

<span data-ttu-id="e0b2b-150">To automatically provision a device, [set up Device Provisioning Service and retrieve your device registration ID][lnk-dps] (DPS).</span><span class="sxs-lookup"><span data-stu-id="e0b2b-150">To automatically provision a device, [set up Device Provisioning Service and retrieve your device registration ID][lnk-dps] (DPS).</span></span> <span data-ttu-id="e0b2b-151">Automatic provisioning only works with devices that have a Trusted Platform Module (TPM) chip.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-151">Automatic provisioning only works with devices that have a Trusted Platform Module (TPM) chip.</span></span> <span data-ttu-id="e0b2b-152">For example, Raspberry Pi devices do not come with TPM by default.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-152">For example, Raspberry Pi devices do not come with TPM by default.</span></span> 

<span data-ttu-id="e0b2b-153">Open the configuration file.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-153">Open the configuration file.</span></span> 

```bash
sudo nano /etc/iotedge/config.yaml
```

<span data-ttu-id="e0b2b-154">Find the provisioning section of the file and uncomment the **dps** provisioning mode.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-154">Find the provisioning section of the file and uncomment the **dps** provisioning mode.</span></span> <span data-ttu-id="e0b2b-155">Update the values of **scope_id** and **registration_id** with the values from your IoT Hub Device Provisioning Service and your IoT Edge device with TPM.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-155">Update the values of **scope_id** and **registration_id** with the values from your IoT Hub Device Provisioning Service and your IoT Edge device with TPM.</span></span> 

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

<span data-ttu-id="e0b2b-156">Save and close the file.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-156">Save and close the file.</span></span> 

   <span data-ttu-id="e0b2b-157">`CTRL + X`, `Y`, `Enter`</span><span class="sxs-lookup"><span data-stu-id="e0b2b-157">`CTRL + X`, `Y`, `Enter`</span></span>

<span data-ttu-id="e0b2b-158">After entering the provisioning information in the configuration file, restart the daemon:</span><span class="sxs-lookup"><span data-stu-id="e0b2b-158">After entering the provisioning information in the configuration file, restart the daemon:</span></span>

```bash
sudo systemctl restart iotedge
```

## <a name="verify-successful-installation"></a><span data-ttu-id="e0b2b-159">Verify successful installation</span><span class="sxs-lookup"><span data-stu-id="e0b2b-159">Verify successful installation</span></span>

<span data-ttu-id="e0b2b-160">If you used the **manual configuration** steps in the previous section, the IoT Edge runtime should be successfully provisioned and running on your device.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-160">If you used the **manual configuration** steps in the previous section, the IoT Edge runtime should be successfully provisioned and running on your device.</span></span> <span data-ttu-id="e0b2b-161">If you used the **automatic configuration** steps, then you need to complete some additional steps so that the runtime can register your device with your IoT hub on your behalf.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-161">If you used the **automatic configuration** steps, then you need to complete some additional steps so that the runtime can register your device with your IoT hub on your behalf.</span></span> <span data-ttu-id="e0b2b-162">For next steps, see [Create and provision a simulated TPM Edge device on a Linux virtual machine](how-to-auto-provision-simulated-device-linux.md#give-iot-edge-access-to-the-tpm).</span><span class="sxs-lookup"><span data-stu-id="e0b2b-162">For next steps, see [Create and provision a simulated TPM Edge device on a Linux virtual machine](how-to-auto-provision-simulated-device-linux.md#give-iot-edge-access-to-the-tpm).</span></span>

<span data-ttu-id="e0b2b-163">You can check the status of the IoT Edge Daemon using:</span><span class="sxs-lookup"><span data-stu-id="e0b2b-163">You can check the status of the IoT Edge Daemon using:</span></span>

```bash
systemctl status iotedge
```

<span data-ttu-id="e0b2b-164">Examine daemon logs using:</span><span class="sxs-lookup"><span data-stu-id="e0b2b-164">Examine daemon logs using:</span></span>

```bash
journalctl -u iotedge --no-pager --no-full
```

<span data-ttu-id="e0b2b-165">And, list running modules with:</span><span class="sxs-lookup"><span data-stu-id="e0b2b-165">And, list running modules with:</span></span>

```bash
sudo iotedge list
```

## <a name="tips-and-suggestions"></a><span data-ttu-id="e0b2b-166">Tips and suggestions</span><span class="sxs-lookup"><span data-stu-id="e0b2b-166">Tips and suggestions</span></span>

<span data-ttu-id="e0b2b-167">You need elevated privileges to run `iotedge` commands.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-167">You need elevated privileges to run `iotedge` commands.</span></span> <span data-ttu-id="e0b2b-168">After installing the runtime, sign out of your machine and sign back in to update your permissions automatically.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-168">After installing the runtime, sign out of your machine and sign back in to update your permissions automatically.</span></span> <span data-ttu-id="e0b2b-169">Until then, use **sudo** in front of any `iotedge` the commands.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-169">Until then, use **sudo** in front of any `iotedge` the commands.</span></span>

<span data-ttu-id="e0b2b-170">On resource constrained devices, it is highly recommended that you set the *OptimizeForPerformance* environment variable to *false* as per instructions in the [troubleshooting guide][lnk-trouble].</span><span class="sxs-lookup"><span data-stu-id="e0b2b-170">On resource constrained devices, it is highly recommended that you set the *OptimizeForPerformance* environment variable to *false* as per instructions in the [troubleshooting guide][lnk-trouble].</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0b2b-171">Next steps</span><span class="sxs-lookup"><span data-stu-id="e0b2b-171">Next steps</span></span>

<span data-ttu-id="e0b2b-172">If you are having problems with the Edge runtime installing properly, check out the [troubleshooting][lnk-trouble] page.</span><span class="sxs-lookup"><span data-stu-id="e0b2b-172">If you are having problems with the Edge runtime installing properly, check out the [troubleshooting][lnk-trouble] page.</span></span>

<!-- Links -->
[lnk-dcs]: how-to-register-device-portal.md
[lnk-dps]: how-to-auto-provision-simulated-device-linux.md
[lnk-oci]: https://www.opencontainers.org/
[lnk-moby]: https://mobyproject.org/
[lnk-trouble]: troubleshoot.md
