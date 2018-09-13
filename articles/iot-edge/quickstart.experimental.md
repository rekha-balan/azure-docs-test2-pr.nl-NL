---
title: Simulate Azure IoT Edge on Windows | Microsoft Docs
description: Install the Azure IoT Edge runtime on a simulated device in Windows and deploy your first module
author: kgremban
manager: timlt
ms.author: kgremban
ms.reviewer: elioda
ms.date: 06/08/2018
ms.topic: tutorial
ms.service: iot-edge
services: iot-edge
ms.custom: mvc
ms.openlocfilehash: 1a45841564b0c985662e6d2db320111fa27d1e92
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871538"
---
# <a name="quickstart-deploy-your-first-iot-edge-module-from-the-azure-portal-to-a-windows-device---preview"></a><span data-ttu-id="04b88-103">Quickstart: Deploy your first IoT Edge module from the Azure portal to a Windows device - preview</span><span class="sxs-lookup"><span data-stu-id="04b88-103">Quickstart: Deploy your first IoT Edge module from the Azure portal to a Windows device - preview</span></span>

<span data-ttu-id="04b88-104">Azure IoT Edge enables you to perform analytics and data processing on your devices, instead of having to push all the data to the cloud.</span><span class="sxs-lookup"><span data-stu-id="04b88-104">Azure IoT Edge enables you to perform analytics and data processing on your devices, instead of having to push all the data to the cloud.</span></span> <span data-ttu-id="04b88-105">The IoT Edge tutorials demonstrate how to deploy different types of modules, but first you need a device to test.</span><span class="sxs-lookup"><span data-stu-id="04b88-105">The IoT Edge tutorials demonstrate how to deploy different types of modules, but first you need a device to test.</span></span> 

<span data-ttu-id="04b88-106">In this quickstart you learn how to:</span><span class="sxs-lookup"><span data-stu-id="04b88-106">In this quickstart you learn how to:</span></span>

1. <span data-ttu-id="04b88-107">Create an IoT Hub</span><span class="sxs-lookup"><span data-stu-id="04b88-107">Create an IoT Hub</span></span>
2. <span data-ttu-id="04b88-108">Register an IoT Edge device</span><span class="sxs-lookup"><span data-stu-id="04b88-108">Register an IoT Edge device</span></span>
3. <span data-ttu-id="04b88-109">Start the IoT Edge runtime</span><span class="sxs-lookup"><span data-stu-id="04b88-109">Start the IoT Edge runtime</span></span>
4. <span data-ttu-id="04b88-110">Deploy a module</span><span class="sxs-lookup"><span data-stu-id="04b88-110">Deploy a module</span></span>

![Tutorial architecture][2]

<span data-ttu-id="04b88-112">The module that you deploy in this quickstart is a simulated sensor that generates temperature, humidity, and pressure data.</span><span class="sxs-lookup"><span data-stu-id="04b88-112">The module that you deploy in this quickstart is a simulated sensor that generates temperature, humidity, and pressure data.</span></span> <span data-ttu-id="04b88-113">The other Azure IoT Edge tutorials build upon the work you do here by deploying modules that analyze the simulated data for business insights.</span><span class="sxs-lookup"><span data-stu-id="04b88-113">The other Azure IoT Edge tutorials build upon the work you do here by deploying modules that analyze the simulated data for business insights.</span></span> 

>[!NOTE]
><span data-ttu-id="04b88-114">The IoT Edge runtime on Windows is in [public preview](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span><span class="sxs-lookup"><span data-stu-id="04b88-114">The IoT Edge runtime on Windows is in [public preview](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span></span>

<span data-ttu-id="04b88-115">If you don't have an active Azure subscription, create a [free account][lnk-account] before you begin.</span><span class="sxs-lookup"><span data-stu-id="04b88-115">If you don't have an active Azure subscription, create a [free account][lnk-account] before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="04b88-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="04b88-116">Prerequisites</span></span>

<span data-ttu-id="04b88-117">This quickstart assumes that you're using a computer or virtual machine running Windows to simulate an IoT device.</span><span class="sxs-lookup"><span data-stu-id="04b88-117">This quickstart assumes that you're using a computer or virtual machine running Windows to simulate an IoT device.</span></span> <span data-ttu-id="04b88-118">If you're running Windows in a virtual machine, enable [nested virtualization][lnk-nested] and allocate at least 2GB memory.</span><span class="sxs-lookup"><span data-stu-id="04b88-118">If you're running Windows in a virtual machine, enable [nested virtualization][lnk-nested] and allocate at least 2GB memory.</span></span> 

<span data-ttu-id="04b88-119">Have the following prerequisites ready on the machine that you're using for an IoT Edge device:</span><span class="sxs-lookup"><span data-stu-id="04b88-119">Have the following prerequisites ready on the machine that you're using for an IoT Edge device:</span></span>

1. <span data-ttu-id="04b88-120">Make sure you're using a supported Windows version:</span><span class="sxs-lookup"><span data-stu-id="04b88-120">Make sure you're using a supported Windows version:</span></span>
   * <span data-ttu-id="04b88-121">Windows 10 or newer</span><span class="sxs-lookup"><span data-stu-id="04b88-121">Windows 10 or newer</span></span>
   * <span data-ttu-id="04b88-122">Windows Server 2016 or newer</span><span class="sxs-lookup"><span data-stu-id="04b88-122">Windows Server 2016 or newer</span></span>
2. <span data-ttu-id="04b88-123">Install [Docker for Windows][lnk-docker] and make sure it's running.</span><span class="sxs-lookup"><span data-stu-id="04b88-123">Install [Docker for Windows][lnk-docker] and make sure it's running.</span></span>
3. <span data-ttu-id="04b88-124">Configure Docker to use [Linux containers](https://docs.docker.com/docker-for-windows/#switch-between-windows-and-linux-containers)</span><span class="sxs-lookup"><span data-stu-id="04b88-124">Configure Docker to use [Linux containers](https://docs.docker.com/docker-for-windows/#switch-between-windows-and-linux-containers)</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="04b88-125">Create an IoT hub</span><span class="sxs-lookup"><span data-stu-id="04b88-125">Create an IoT hub</span></span>

<span data-ttu-id="04b88-126">Start the quickstart by creating an IoT hub in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="04b88-126">Start the quickstart by creating an IoT hub in the Azure portal.</span></span>
<span data-ttu-id="04b88-127">![Create IoT Hub][3]</span><span class="sxs-lookup"><span data-stu-id="04b88-127">![Create IoT Hub][3]</span></span>

<span data-ttu-id="04b88-128">Create your IoT hub in a resource group that you can use to maintain and manage all the resources that you create in this quickstart.</span><span class="sxs-lookup"><span data-stu-id="04b88-128">Create your IoT hub in a resource group that you can use to maintain and manage all the resources that you create in this quickstart.</span></span> <span data-ttu-id="04b88-129">Call it something easy to remember, like **IoTEdgeResources**.</span><span class="sxs-lookup"><span data-stu-id="04b88-129">Call it something easy to remember, like **IoTEdgeResources**.</span></span> <span data-ttu-id="04b88-130">By putting all the resources for the quickstarts and tutorials in a group, you can manage them together and remove them easily when you're done testing.</span><span class="sxs-lookup"><span data-stu-id="04b88-130">By putting all the resources for the quickstarts and tutorials in a group, you can manage them together and remove them easily when you're done testing.</span></span> 

[!INCLUDE [iot-hub-create-hub](../../includes/iot-hub-create-hub.md)]

## <a name="register-an-iot-edge-device"></a><span data-ttu-id="04b88-131">Register an IoT Edge device</span><span class="sxs-lookup"><span data-stu-id="04b88-131">Register an IoT Edge device</span></span>

<span data-ttu-id="04b88-132">Register an IoT Edge device with your newly created IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="04b88-132">Register an IoT Edge device with your newly created IoT Hub.</span></span>
<span data-ttu-id="04b88-133">![Register a device][4]</span><span class="sxs-lookup"><span data-stu-id="04b88-133">![Register a device][4]</span></span>

[!INCLUDE [iot-edge-register-device](../../includes/iot-edge-register-device.md)]

## <a name="install-and-start-the-iot-edge-runtime"></a><span data-ttu-id="04b88-134">Install and start the IoT Edge runtime</span><span class="sxs-lookup"><span data-stu-id="04b88-134">Install and start the IoT Edge runtime</span></span>

<span data-ttu-id="04b88-135">Install and start the Azure IoT Edge runtime on your IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="04b88-135">Install and start the Azure IoT Edge runtime on your IoT Edge device.</span></span> 
<span data-ttu-id="04b88-136">![Register a device][5]</span><span class="sxs-lookup"><span data-stu-id="04b88-136">![Register a device][5]</span></span>

<span data-ttu-id="04b88-137">The IoT Edge runtime is deployed on all IoT Edge devices.</span><span class="sxs-lookup"><span data-stu-id="04b88-137">The IoT Edge runtime is deployed on all IoT Edge devices.</span></span> <span data-ttu-id="04b88-138">It has three components.</span><span class="sxs-lookup"><span data-stu-id="04b88-138">It has three components.</span></span> <span data-ttu-id="04b88-139">The **IoT Edge security daemon** starts each time an Edge device boots and bootstraps the device by starting the IoT Edge agent.</span><span class="sxs-lookup"><span data-stu-id="04b88-139">The **IoT Edge security daemon** starts each time an Edge device boots and bootstraps the device by starting the IoT Edge agent.</span></span> <span data-ttu-id="04b88-140">The **IoT Edge agent** facilitates deployment and monitoring of modules on the IoT Edge device, including the IoT Edge hub.</span><span class="sxs-lookup"><span data-stu-id="04b88-140">The **IoT Edge agent** facilitates deployment and monitoring of modules on the IoT Edge device, including the IoT Edge hub.</span></span> <span data-ttu-id="04b88-141">The **IoT Edge hub** manages communications between modules on the IoT Edge device, and between the device and IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="04b88-141">The **IoT Edge hub** manages communications between modules on the IoT Edge device, and between the device and IoT Hub.</span></span> 

>[!NOTE]
><span data-ttu-id="04b88-142">The installation steps in this section are manual for now while an installation script is being developed.</span><span class="sxs-lookup"><span data-stu-id="04b88-142">The installation steps in this section are manual for now while an installation script is being developed.</span></span> 

<span data-ttu-id="04b88-143">The instructions in this section configure the IoT Edge runtime with Linux containers.</span><span class="sxs-lookup"><span data-stu-id="04b88-143">The instructions in this section configure the IoT Edge runtime with Linux containers.</span></span> <span data-ttu-id="04b88-144">If you want to use Windows containers, see [Install Azure IoT Edge runtime on Windows to use with Windows containers](how-to-install-iot-edge-windows-with-windows.md).</span><span class="sxs-lookup"><span data-stu-id="04b88-144">If you want to use Windows containers, see [Install Azure IoT Edge runtime on Windows to use with Windows containers](how-to-install-iot-edge-windows-with-windows.md).</span></span>

### <a name="download-and-install-the-iot-edge-service"></a><span data-ttu-id="04b88-145">Download and install the IoT Edge service</span><span class="sxs-lookup"><span data-stu-id="04b88-145">Download and install the IoT Edge service</span></span>

1. <span data-ttu-id="04b88-146">On your IoT Edge device, run PowerShell as an administrator.</span><span class="sxs-lookup"><span data-stu-id="04b88-146">On your IoT Edge device, run PowerShell as an administrator.</span></span>

2. <span data-ttu-id="04b88-147">Download the IoT Edge service package.</span><span class="sxs-lookup"><span data-stu-id="04b88-147">Download the IoT Edge service package.</span></span>

   ```powershell
   Invoke-WebRequest https://aka.ms/iotedged-windows-latest -o .\iotedged-windows.zip
   Expand-Archive .\iotedged-windows.zip C:\ProgramData\iotedge -f
   Move-Item c:\ProgramData\iotedge\iotedged-windows\* C:\ProgramData\iotedge\ -Force
   rmdir C:\ProgramData\iotedge\iotedged-windows
   $sysenv = "HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\Environment"
   $path = (Get-ItemProperty -Path $sysenv -Name Path).Path + ";C:\ProgramData\iotedge"
   Set-ItemProperty -Path $sysenv -Name Path -Value $path
   ```

3. <span data-ttu-id="04b88-148">Install the vcruntime.</span><span class="sxs-lookup"><span data-stu-id="04b88-148">Install the vcruntime.</span></span>

  ```powershell
  Invoke-WebRequest -useb https://download.microsoft.com/download/0/6/4/064F84EA-D1DB-4EAA-9A5C-CC2F0FF6A638/vc_redist.x64.exe -o vc_redist.exe
  .\vc_redist.exe /quiet /norestart
  ```

4. <span data-ttu-id="04b88-149">Create and start the IoT Edge service.</span><span class="sxs-lookup"><span data-stu-id="04b88-149">Create and start the IoT Edge service.</span></span>

   ```powershell
   New-Service -Name "iotedge" -BinaryPathName "C:\ProgramData\iotedge\iotedged.exe -c C:\ProgramData\iotedge\config.yaml"
   Start-Service iotedge
   ```

5. <span data-ttu-id="04b88-150">Add firewall exceptions for the ports that the IoT Edge service uses.</span><span class="sxs-lookup"><span data-stu-id="04b88-150">Add firewall exceptions for the ports that the IoT Edge service uses.</span></span>

   ```powershell
   New-NetFirewallRule -DisplayName "iotedged allow inbound 15580,15581" -Direction Inbound -Action Allow -Protocol TCP -LocalPort 15580-15581 -Program "C:\programdata\iotedge\iotedged.exe" -InterfaceType Any
   ```

6. <span data-ttu-id="04b88-151">Create a new file called **iotedge.reg** and open it with a text editor.</span><span class="sxs-lookup"><span data-stu-id="04b88-151">Create a new file called **iotedge.reg** and open it with a text editor.</span></span> 

7. <span data-ttu-id="04b88-152">Add the following content and save the file.</span><span class="sxs-lookup"><span data-stu-id="04b88-152">Add the following content and save the file.</span></span> 

   ```input
   Windows Registry Editor Version 5.00
   [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\EventLog\Application\iotedged]
   "CustomSource"=dword:00000001
   "EventMessageFile"="C:\\ProgramData\\iotedge\\iotedged.exe"
   "TypesSupported"=dword:00000007
   ```

8. <span data-ttu-id="04b88-153">Navigate to your file in File Explorer and double-click it to import the changes to the Windows Registry.</span><span class="sxs-lookup"><span data-stu-id="04b88-153">Navigate to your file in File Explorer and double-click it to import the changes to the Windows Registry.</span></span> 

### <a name="configure-the-iot-edge-runtime"></a><span data-ttu-id="04b88-154">Configure the IoT Edge runtime</span><span class="sxs-lookup"><span data-stu-id="04b88-154">Configure the IoT Edge runtime</span></span> 

<span data-ttu-id="04b88-155">Configure the runtime with your IoT Edge device connection string that you copied when you registered a new device.</span><span class="sxs-lookup"><span data-stu-id="04b88-155">Configure the runtime with your IoT Edge device connection string that you copied when you registered a new device.</span></span> <span data-ttu-id="04b88-156">Then, configure the runtime network.</span><span class="sxs-lookup"><span data-stu-id="04b88-156">Then, configure the runtime network.</span></span> 

1. <span data-ttu-id="04b88-157">Open the IoT Edge configuration file, which is located at `C:\ProgramData\iotedge\config.yaml`.</span><span class="sxs-lookup"><span data-stu-id="04b88-157">Open the IoT Edge configuration file, which is located at `C:\ProgramData\iotedge\config.yaml`.</span></span> <span data-ttu-id="04b88-158">This file is protected, so run a text editor like Notepad as an administrator, then use the editor to open the file.</span><span class="sxs-lookup"><span data-stu-id="04b88-158">This file is protected, so run a text editor like Notepad as an administrator, then use the editor to open the file.</span></span> 

2. <span data-ttu-id="04b88-159">Find the **provisioning** section and update the value of **device_connection_string** with the string that you copied from your IoT Edge device details.</span><span class="sxs-lookup"><span data-stu-id="04b88-159">Find the **provisioning** section and update the value of **device_connection_string** with the string that you copied from your IoT Edge device details.</span></span> 

3. <span data-ttu-id="04b88-160">In your administrator PowerShell window, retrieve the hostname for your IoT Edge device and copy the output.</span><span class="sxs-lookup"><span data-stu-id="04b88-160">In your administrator PowerShell window, retrieve the hostname for your IoT Edge device and copy the output.</span></span> 

   ```powershell
   hostname
   ```

4. <span data-ttu-id="04b88-161">In the configuration file, find the **Edge device hostname** section.</span><span class="sxs-lookup"><span data-stu-id="04b88-161">In the configuration file, find the **Edge device hostname** section.</span></span> <span data-ttu-id="04b88-162">Update the value of **hostname** with the hostname that you copied from PowerShell.</span><span class="sxs-lookup"><span data-stu-id="04b88-162">Update the value of **hostname** with the hostname that you copied from PowerShell.</span></span>

3. <span data-ttu-id="04b88-163">In your administrator PowerShell window, retrieve the IP address for your IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="04b88-163">In your administrator PowerShell window, retrieve the IP address for your IoT Edge device.</span></span> 

   ```powershell
   ipconfig
   ```

4. <span data-ttu-id="04b88-164">Copy the value for **IPv4 Address** in the **vEthernet (DockerNAT)** section of the output.</span><span class="sxs-lookup"><span data-stu-id="04b88-164">Copy the value for **IPv4 Address** in the **vEthernet (DockerNAT)** section of the output.</span></span> 

5. <span data-ttu-id="04b88-165">Create an environment variable called **IOTEDGE_HOST**, replacing *\<ip_address\>* with the IP Address for your IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="04b88-165">Create an environment variable called **IOTEDGE_HOST**, replacing *\<ip_address\>* with the IP Address for your IoT Edge device.</span></span> 

  ```powershell
  [Environment]::SetEnvironmentVariable("IOTEDGE_HOST", "http://<ip_address>:15580")
  ```

  <span data-ttu-id="04b88-166">Persist the environment variable across reboots.</span><span class="sxs-lookup"><span data-stu-id="04b88-166">Persist the environment variable across reboots.</span></span>

  ```powershell
  SETX /M IOTEDGE_HOST "http://<ip_address>:15580"
  ```

6. <span data-ttu-id="04b88-167">In the `config.yaml` file, find the **Connect settings** section.</span><span class="sxs-lookup"><span data-stu-id="04b88-167">In the `config.yaml` file, find the **Connect settings** section.</span></span> <span data-ttu-id="04b88-168">Update the **management_uri** and **workload_uri** values with your IP address and the ports that you opened in the previous section.</span><span class="sxs-lookup"><span data-stu-id="04b88-168">Update the **management_uri** and **workload_uri** values with your IP address and the ports that you opened in the previous section.</span></span> <span data-ttu-id="04b88-169">Replace **\<GATEWAY_ADDRESS\>** with the DockerNAT IP address that you copied.</span><span class="sxs-lookup"><span data-stu-id="04b88-169">Replace **\<GATEWAY_ADDRESS\>** with the DockerNAT IP address that you copied.</span></span>

   ```yaml
   connect: 
     management_uri: "http://<GATEWAY_ADDRESS>:15580"
     workload_uri: "http://<GATEWAY_ADDRESS>:15581"
   ```

7. <span data-ttu-id="04b88-170">Find the **Listen settings** section and add the same values for **management_uri** and **workload_uri**.</span><span class="sxs-lookup"><span data-stu-id="04b88-170">Find the **Listen settings** section and add the same values for **management_uri** and **workload_uri**.</span></span> 

   ```yaml
   listen:
     management_uri: "http://<GATEWAY_ADDRESS>:15580"
     workload_uri: "http://<GATEWAY_ADDRESS>:15581"
   ```

8. <span data-ttu-id="04b88-171">Find the **Moby Container Runtime settings** section and verify that the value for **network** is uncommented and set to **azure-iot-edge**</span><span class="sxs-lookup"><span data-stu-id="04b88-171">Find the **Moby Container Runtime settings** section and verify that the value for **network** is uncommented and set to **azure-iot-edge**</span></span>

   ```yaml
   moby_runtime:
     docker_uri: "npipe://./pipe/docker_engine"
     network: "azure-iot-edge"
   ```
   
9. <span data-ttu-id="04b88-172">Save the configuration file.</span><span class="sxs-lookup"><span data-stu-id="04b88-172">Save the configuration file.</span></span> 

10. <span data-ttu-id="04b88-173">In PowerShell, restart the IoT Edge service.</span><span class="sxs-lookup"><span data-stu-id="04b88-173">In PowerShell, restart the IoT Edge service.</span></span>

   ```powershell
   Stop-Service iotedge -NoWait
   sleep 5
   Start-Service iotedge
   ```

### <a name="view-the-iot-edge-runtime-status"></a><span data-ttu-id="04b88-174">View the IoT Edge runtime status</span><span class="sxs-lookup"><span data-stu-id="04b88-174">View the IoT Edge runtime status</span></span>

<span data-ttu-id="04b88-175">Verify that the runtime was successfully installed and configured.</span><span class="sxs-lookup"><span data-stu-id="04b88-175">Verify that the runtime was successfully installed and configured.</span></span>

1. <span data-ttu-id="04b88-176">Check the status of the IoT Edge service.</span><span class="sxs-lookup"><span data-stu-id="04b88-176">Check the status of the IoT Edge service.</span></span>

   ```powershell
   Get-Service iotedge
   ```

2. <span data-ttu-id="04b88-177">If you need to troubleshoot the service, retrieve the service logs.</span><span class="sxs-lookup"><span data-stu-id="04b88-177">If you need to troubleshoot the service, retrieve the service logs.</span></span> 

   ```powershell
   # Displays logs from today, newest at the bottom.

   Get-WinEvent -ea SilentlyContinue `
    -FilterHashtable @{ProviderName= "iotedged";
      LogName = "application"; StartTime = [datetime]::Today} |
    select TimeCreated, Message |
    sort-object @{Expression="TimeCreated";Descending=$false} |
    format-table -autosize -wrap
   ```

3. <span data-ttu-id="04b88-178">View all the modules running on your IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="04b88-178">View all the modules running on your IoT Edge device.</span></span> <span data-ttu-id="04b88-179">Since the service just started for the first time, you should only see the **edgeAgent** module running.</span><span class="sxs-lookup"><span data-stu-id="04b88-179">Since the service just started for the first time, you should only see the **edgeAgent** module running.</span></span> <span data-ttu-id="04b88-180">The edgeAgent module runs by default, and helps to install and start any additional modules that you deploy to your device.</span><span class="sxs-lookup"><span data-stu-id="04b88-180">The edgeAgent module runs by default, and helps to install and start any additional modules that you deploy to your device.</span></span> 

   ```powershell
   iotedge list
   ```

   ![View one module on your device](./media/quickstart/iotedge-list-1.png)

## <a name="deploy-a-module"></a><span data-ttu-id="04b88-182">Deploy a module</span><span class="sxs-lookup"><span data-stu-id="04b88-182">Deploy a module</span></span>

<span data-ttu-id="04b88-183">Manage your Azure IoT Edge device from the cloud to deploy a module that will send telemetry data to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="04b88-183">Manage your Azure IoT Edge device from the cloud to deploy a module that will send telemetry data to IoT Hub.</span></span>
<span data-ttu-id="04b88-184">![Register a device][6]</span><span class="sxs-lookup"><span data-stu-id="04b88-184">![Register a device][6]</span></span>

[!INCLUDE [iot-edge-deploy-module](../../includes/iot-edge-deploy-module.md)]

## <a name="view-generated-data"></a><span data-ttu-id="04b88-185">View generated data</span><span class="sxs-lookup"><span data-stu-id="04b88-185">View generated data</span></span>

<span data-ttu-id="04b88-186">In this quickstart, you created a new IoT Edge device and installed the IoT Edge runtime on it.</span><span class="sxs-lookup"><span data-stu-id="04b88-186">In this quickstart, you created a new IoT Edge device and installed the IoT Edge runtime on it.</span></span> <span data-ttu-id="04b88-187">Then, you used the Azure portal to push an IoT Edge module to run on the device without having to make changes to the device itself.</span><span class="sxs-lookup"><span data-stu-id="04b88-187">Then, you used the Azure portal to push an IoT Edge module to run on the device without having to make changes to the device itself.</span></span> <span data-ttu-id="04b88-188">In this case, the module that you pushed creates environmental data that you can use for the tutorials.</span><span class="sxs-lookup"><span data-stu-id="04b88-188">In this case, the module that you pushed creates environmental data that you can use for the tutorials.</span></span> 

<span data-ttu-id="04b88-189">Confirm that the module deployed from the cloud is running on your IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="04b88-189">Confirm that the module deployed from the cloud is running on your IoT Edge device.</span></span> 

```powershell
iotedge list
```

   ![View three modules on your device](./media/quickstart/iotedge-list-2.png)

<span data-ttu-id="04b88-191">View the messages being sent from the tempSensor module to the cloud.</span><span class="sxs-lookup"><span data-stu-id="04b88-191">View the messages being sent from the tempSensor module to the cloud.</span></span> 

```powershell
iotedge logs tempSensor -f
```

  ![View the data from your module](./media/quickstart/iotedge-logs.png)

<span data-ttu-id="04b88-193">You can also view the messages that are received by your IoT hub by using the [Azure IoT Toolkit extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-toolkit).</span><span class="sxs-lookup"><span data-stu-id="04b88-193">You can also view the messages that are received by your IoT hub by using the [Azure IoT Toolkit extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-toolkit).</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="04b88-194">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="04b88-194">Clean up resources</span></span>

<span data-ttu-id="04b88-195">If you want to continue on to the IoT Edge tutorials, you can use the device that you registered and set up in this quickstart.</span><span class="sxs-lookup"><span data-stu-id="04b88-195">If you want to continue on to the IoT Edge tutorials, you can use the device that you registered and set up in this quickstart.</span></span> <span data-ttu-id="04b88-196">Otherwise, you can delete the Azure resources that you created and remove the IoT Edge runtime from your device.</span><span class="sxs-lookup"><span data-stu-id="04b88-196">Otherwise, you can delete the Azure resources that you created and remove the IoT Edge runtime from your device.</span></span> 

### <a name="delete-azure-resources"></a><span data-ttu-id="04b88-197">Delete Azure resources</span><span class="sxs-lookup"><span data-stu-id="04b88-197">Delete Azure resources</span></span>

<span data-ttu-id="04b88-198">If you created your virtual machine and IoT hub in a new resource group, you can delete that group and all the associated resources.</span><span class="sxs-lookup"><span data-stu-id="04b88-198">If you created your virtual machine and IoT hub in a new resource group, you can delete that group and all the associated resources.</span></span> <span data-ttu-id="04b88-199">If there's anything in that resource group that you want to keep, then just delete the individual resources that you want to clean up.</span><span class="sxs-lookup"><span data-stu-id="04b88-199">If there's anything in that resource group that you want to keep, then just delete the individual resources that you want to clean up.</span></span> 

<span data-ttu-id="04b88-200">To remove a resource group, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="04b88-200">To remove a resource group, follow these steps:</span></span> 

1. <span data-ttu-id="04b88-201">Sign in to the [Azure portal](https://portal.azure.com) and click **Resource groups**.</span><span class="sxs-lookup"><span data-stu-id="04b88-201">Sign in to the [Azure portal](https://portal.azure.com) and click **Resource groups**.</span></span>
2. <span data-ttu-id="04b88-202">In the **Filter by name...** textbox, type the name of the resource group containing your IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="04b88-202">In the **Filter by name...** textbox, type the name of the resource group containing your IoT Hub.</span></span> 
3. <span data-ttu-id="04b88-203">To the right of your resource group in the result list, click **...** then **Delete resource group**.</span><span class="sxs-lookup"><span data-stu-id="04b88-203">To the right of your resource group in the result list, click **...** then **Delete resource group**.</span></span>
4. <span data-ttu-id="04b88-204">You will be asked to confirm the deletion of the resource group.</span><span class="sxs-lookup"><span data-stu-id="04b88-204">You will be asked to confirm the deletion of the resource group.</span></span> <span data-ttu-id="04b88-205">Type the name of your resource group again to confirm, and then click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="04b88-205">Type the name of your resource group again to confirm, and then click **Delete**.</span></span> <span data-ttu-id="04b88-206">After a few moments, the resource group and all of its contained resources are deleted.</span><span class="sxs-lookup"><span data-stu-id="04b88-206">After a few moments, the resource group and all of its contained resources are deleted.</span></span>

### <a name="remove-the-iot-edge-runtime"></a><span data-ttu-id="04b88-207">Remove the IoT Edge runtime</span><span class="sxs-lookup"><span data-stu-id="04b88-207">Remove the IoT Edge runtime</span></span>

<span data-ttu-id="04b88-208">If you plan on using the IoT Edge device for future testing, but want to stop the tempSensor module from sending data to your IoT hub while not in use, use the following command to stop the IoT Edge service.</span><span class="sxs-lookup"><span data-stu-id="04b88-208">If you plan on using the IoT Edge device for future testing, but want to stop the tempSensor module from sending data to your IoT hub while not in use, use the following command to stop the IoT Edge service.</span></span> 

   ```powershell
   Stop-Service iotedge -NoWait
   ```

<span data-ttu-id="04b88-209">You can restart the service when you're ready to start testing again</span><span class="sxs-lookup"><span data-stu-id="04b88-209">You can restart the service when you're ready to start testing again</span></span>

   ```powershell
   Start-Service iotedge
   ```

<span data-ttu-id="04b88-210">If you want to remove the installations from your device, use the following commands.</span><span class="sxs-lookup"><span data-stu-id="04b88-210">If you want to remove the installations from your device, use the following commands.</span></span>  

<span data-ttu-id="04b88-211">Remove the IoT Edge runtime.</span><span class="sxs-lookup"><span data-stu-id="04b88-211">Remove the IoT Edge runtime.</span></span>

   ```powershell
   cmd /c sc delete iotedge
   rm -r c:\programdata\iotedge
   ```

<span data-ttu-id="04b88-212">When the IoT Edge runtime is removed, the containers that it created are stopped, but still exist on your device.</span><span class="sxs-lookup"><span data-stu-id="04b88-212">When the IoT Edge runtime is removed, the containers that it created are stopped, but still exist on your device.</span></span> <span data-ttu-id="04b88-213">View all containers.</span><span class="sxs-lookup"><span data-stu-id="04b88-213">View all containers.</span></span>

   ```powershell
   docker ps -a
   ```

<span data-ttu-id="04b88-214">Delete the containers that were created on your device by the IoT Edge runtime.</span><span class="sxs-lookup"><span data-stu-id="04b88-214">Delete the containers that were created on your device by the IoT Edge runtime.</span></span> <span data-ttu-id="04b88-215">Change the name of the tempSensor container if you called it something different.</span><span class="sxs-lookup"><span data-stu-id="04b88-215">Change the name of the tempSensor container if you called it something different.</span></span> 

   ```powershell
   docker rm -f tempSensor
   docker rm -f edgeHub
   docker rm -f edgeAgent
   ```

## <a name="next-steps"></a><span data-ttu-id="04b88-216">Next steps</span><span class="sxs-lookup"><span data-stu-id="04b88-216">Next steps</span></span>

<span data-ttu-id="04b88-217">In this quickstart, you created a new IoT Edge device and used the Azure IoT Edge cloud interface to deploy code onto the device.</span><span class="sxs-lookup"><span data-stu-id="04b88-217">In this quickstart, you created a new IoT Edge device and used the Azure IoT Edge cloud interface to deploy code onto the device.</span></span> <span data-ttu-id="04b88-218">Now, you have a test device generating raw data about its environment.</span><span class="sxs-lookup"><span data-stu-id="04b88-218">Now, you have a test device generating raw data about its environment.</span></span> 

<span data-ttu-id="04b88-219">You are ready to continue on to any of the other tutorials to learn how Azure IoT Edge can help you turn this data into business insights at the edge.</span><span class="sxs-lookup"><span data-stu-id="04b88-219">You are ready to continue on to any of the other tutorials to learn how Azure IoT Edge can help you turn this data into business insights at the edge.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="04b88-220">Filter sensor data using an Azure Function</span><span class="sxs-lookup"><span data-stu-id="04b88-220">Filter sensor data using an Azure Function</span></span>](tutorial-deploy-function.md)

<!-- Images -->
[2]: ./media/quickstart/install-edge-full.png
[3]: ./media/quickstart/create-iot-hub.png
[4]: ./media/quickstart/register-device.png
[5]: ./media/quickstart/start-runtime.png
[6]: ./media/quickstart/deploy-module.png

<!-- Links -->
[lnk-nested]: https://docs.microsoft.com/virtualization/hyper-v-on-windows/user-guide/nested-virtualization
[lnk-docker]: https://docs.docker.com/docker-for-windows/install/ 
[lnk-python]: https://www.python.org/downloads/
[lnk-docker-containers]: https://docs.microsoft.com/virtualization/windowscontainers/quick-start/quick-start-windows-10#2-switch-to-windows-containers
[lnk-install-iotcore]: how-to-install-iot-core.md
[lnk-account]: https://azure.microsoft.com/free
