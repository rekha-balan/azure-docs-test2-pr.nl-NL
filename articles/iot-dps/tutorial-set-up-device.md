---
title: Set up device for the Azure IoT Hub Device Provisioning Service
description: Set up device to provision via the IoT Hub Device Provisioning Service during the device manufacturing process
author: wesmc7777
ms.author: wesmc
ms.date: 04/02/2018
ms.topic: tutorial
ms.service: iot-dps
services: iot-dps
manager: timlt
ms.custom: mvc
ms.openlocfilehash: 998bc7cb7e3289a85a9ffc315f7c1f5e568a75cb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865447"
---
# <a name="set-up-a-device-to-provision-using-the-azure-iot-hub-device-provisioning-service"></a><span data-ttu-id="7c913-103">Set up a device to provision using the Azure IoT Hub Device Provisioning Service</span><span class="sxs-lookup"><span data-stu-id="7c913-103">Set up a device to provision using the Azure IoT Hub Device Provisioning Service</span></span>

<span data-ttu-id="7c913-104">In the previous tutorial, you learned how to set up the Azure IoT Hub Device Provisioning Service to automatically provision your devices to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="7c913-104">In the previous tutorial, you learned how to set up the Azure IoT Hub Device Provisioning Service to automatically provision your devices to your IoT hub.</span></span> <span data-ttu-id="7c913-105">This tutorial shows you how to set up your device during the manufacturing process, enabling it to be auto-provisioned with IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="7c913-105">This tutorial shows you how to set up your device during the manufacturing process, enabling it to be auto-provisioned with IoT Hub.</span></span> <span data-ttu-id="7c913-106">Your device is provisioned based on its [Attestation mechanism](concepts-device.md#attestation-mechanism), upon first boot and connection to the provisioning service.</span><span class="sxs-lookup"><span data-stu-id="7c913-106">Your device is provisioned based on its [Attestation mechanism](concepts-device.md#attestation-mechanism), upon first boot and connection to the provisioning service.</span></span> <span data-ttu-id="7c913-107">This tutorial covers the following tasks:</span><span class="sxs-lookup"><span data-stu-id="7c913-107">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7c913-108">Build platform-specific Device Provisioning Services Client SDK</span><span class="sxs-lookup"><span data-stu-id="7c913-108">Build platform-specific Device Provisioning Services Client SDK</span></span>
> * <span data-ttu-id="7c913-109">Extract the security artifacts</span><span class="sxs-lookup"><span data-stu-id="7c913-109">Extract the security artifacts</span></span>
> * <span data-ttu-id="7c913-110">Create the device registration software</span><span class="sxs-lookup"><span data-stu-id="7c913-110">Create the device registration software</span></span>

<span data-ttu-id="7c913-111">This tutorial expects that you have already created your Device Provisioning Service instance and an IoT hub, using the instructions in the previous [Set up cloud resources](tutorial-set-up-cloud.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="7c913-111">This tutorial expects that you have already created your Device Provisioning Service instance and an IoT hub, using the instructions in the previous [Set up cloud resources](tutorial-set-up-cloud.md) tutorial.</span></span>

<span data-ttu-id="7c913-112">This tutorial uses the [Azure IoT SDKs and libraries for C repository](https://github.com/Azure/azure-iot-sdk-c), which contains the Device Provisioning Service Client SDK for C. The SDK currently provides TPM and X.509 support for devices running on Windows or Ubuntu implementations.</span><span class="sxs-lookup"><span data-stu-id="7c913-112">This tutorial uses the [Azure IoT SDKs and libraries for C repository](https://github.com/Azure/azure-iot-sdk-c), which contains the Device Provisioning Service Client SDK for C. The SDK currently provides TPM and X.509 support for devices running on Windows or Ubuntu implementations.</span></span> <span data-ttu-id="7c913-113">This tutorial is based on use of a Windows development client, which also assumes basic proficiency with Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="7c913-113">This tutorial is based on use of a Windows development client, which also assumes basic proficiency with Visual Studio 2017.</span></span> 

<span data-ttu-id="7c913-114">If you're unfamiliar with the process of auto-provisioning, be sure to review [Auto-provisioning concepts](concepts-auto-provisioning.md) before continuing.</span><span class="sxs-lookup"><span data-stu-id="7c913-114">If you're unfamiliar with the process of auto-provisioning, be sure to review [Auto-provisioning concepts](concepts-auto-provisioning.md) before continuing.</span></span> 


[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="7c913-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7c913-115">Prerequisites</span></span>

* <span data-ttu-id="7c913-116">Visual Studio 2015 or [Visual Studio 2017](https://www.visualstudio.com/vs/) with the ['Desktop development with C++'](https://www.visualstudio.com/vs/support/selecting-workloads-visual-studio-2017/) workload enabled.</span><span class="sxs-lookup"><span data-stu-id="7c913-116">Visual Studio 2015 or [Visual Studio 2017](https://www.visualstudio.com/vs/) with the ['Desktop development with C++'](https://www.visualstudio.com/vs/support/selecting-workloads-visual-studio-2017/) workload enabled.</span></span>
* <span data-ttu-id="7c913-117">Latest version of [Git](https://git-scm.com/download/) installed.</span><span class="sxs-lookup"><span data-stu-id="7c913-117">Latest version of [Git](https://git-scm.com/download/) installed.</span></span>



## <a name="build-a-platform-specific-version-of-the-sdk"></a><span data-ttu-id="7c913-118">Build a platform-specific version of the SDK</span><span class="sxs-lookup"><span data-stu-id="7c913-118">Build a platform-specific version of the SDK</span></span>

<span data-ttu-id="7c913-119">The Device Provisioning Service Client SDK helps you implement your device registration software.</span><span class="sxs-lookup"><span data-stu-id="7c913-119">The Device Provisioning Service Client SDK helps you implement your device registration software.</span></span> <span data-ttu-id="7c913-120">But before you can use it, you need to build a version of the SDK specific to your development client platform and attestation mechanism.</span><span class="sxs-lookup"><span data-stu-id="7c913-120">But before you can use it, you need to build a version of the SDK specific to your development client platform and attestation mechanism.</span></span> <span data-ttu-id="7c913-121">In this tutorial, you build an SDK that uses Visual Studio 2017 on a Windows development platform, for a supported type of attestation:</span><span class="sxs-lookup"><span data-stu-id="7c913-121">In this tutorial, you build an SDK that uses Visual Studio 2017 on a Windows development platform, for a supported type of attestation:</span></span>

1. <span data-ttu-id="7c913-122">Download the latest release version of the [CMake build system](https://cmake.org/download/).</span><span class="sxs-lookup"><span data-stu-id="7c913-122">Download the latest release version of the [CMake build system](https://cmake.org/download/).</span></span> <span data-ttu-id="7c913-123">From that same site, look up the cryptographic hash for the version of the binary distribution you chose.</span><span class="sxs-lookup"><span data-stu-id="7c913-123">From that same site, look up the cryptographic hash for the version of the binary distribution you chose.</span></span> <span data-ttu-id="7c913-124">Verify the downloaded binary using the corresponding cryptographic hash value.</span><span class="sxs-lookup"><span data-stu-id="7c913-124">Verify the downloaded binary using the corresponding cryptographic hash value.</span></span> <span data-ttu-id="7c913-125">The following example used Windows PowerShell to verify the cryptographic hash for version 3.11.4 of the x64 MSI distribution:</span><span class="sxs-lookup"><span data-stu-id="7c913-125">The following example used Windows PowerShell to verify the cryptographic hash for version 3.11.4 of the x64 MSI distribution:</span></span>

    ```PowerShell
    PS C:\Users\wesmc\Downloads> $hash = get-filehash .\cmake-3.11.4-win64-x64.msi
    PS C:\Users\wesmc\Downloads> $hash.Hash -eq "56e3605b8e49cd446f3487da88fcc38cb9c3e9e99a20f5d4bd63e54b7a35f869"
    True
    ```

    <span data-ttu-id="7c913-126">It is important that the Visual Studio prerequisites (Visual Studio and the 'Desktop development with C++' workload) are installed on your machine, **before** starting the `CMake` installation.</span><span class="sxs-lookup"><span data-stu-id="7c913-126">It is important that the Visual Studio prerequisites (Visual Studio and the 'Desktop development with C++' workload) are installed on your machine, **before** starting the `CMake` installation.</span></span> <span data-ttu-id="7c913-127">Once the prerequisites are in place, and the download is verified, install the CMake build system.</span><span class="sxs-lookup"><span data-stu-id="7c913-127">Once the prerequisites are in place, and the download is verified, install the CMake build system.</span></span>

1. <span data-ttu-id="7c913-128">Open a command prompt or Git Bash shell.</span><span class="sxs-lookup"><span data-stu-id="7c913-128">Open a command prompt or Git Bash shell.</span></span> <span data-ttu-id="7c913-129">Execute the following command to clone the [Azure IoT C SDK](https://github.com/Azure/azure-iot-sdk-c) GitHub repository:</span><span class="sxs-lookup"><span data-stu-id="7c913-129">Execute the following command to clone the [Azure IoT C SDK](https://github.com/Azure/azure-iot-sdk-c) GitHub repository:</span></span>
    
    ```cmd/sh
    git clone https://github.com/Azure/azure-iot-sdk-c.git --recursive
    ```
    <span data-ttu-id="7c913-130">The size of this repository is currently around 220 MB.</span><span class="sxs-lookup"><span data-stu-id="7c913-130">The size of this repository is currently around 220 MB.</span></span> <span data-ttu-id="7c913-131">You should expect this operation to take several minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="7c913-131">You should expect this operation to take several minutes to complete.</span></span>


1. <span data-ttu-id="7c913-132">Create a `cmake` subdirectory in the root directory of the git repository, and navigate to that folder.</span><span class="sxs-lookup"><span data-stu-id="7c913-132">Create a `cmake` subdirectory in the root directory of the git repository, and navigate to that folder.</span></span> 

    ```cmd/sh
    cd azure-iot-sdk-c
    mkdir cmake
    cd cmake
    ```

1. <span data-ttu-id="7c913-133">Build the SDK for your development platform based on the attestation mechanisms you will be using.</span><span class="sxs-lookup"><span data-stu-id="7c913-133">Build the SDK for your development platform based on the attestation mechanisms you will be using.</span></span> <span data-ttu-id="7c913-134">Use one of the following commands (also note the two trailing period characters for each command).</span><span class="sxs-lookup"><span data-stu-id="7c913-134">Use one of the following commands (also note the two trailing period characters for each command).</span></span> <span data-ttu-id="7c913-135">Upon completion, CMake builds out the `/cmake` subdirectory with content specific to your device:</span><span class="sxs-lookup"><span data-stu-id="7c913-135">Upon completion, CMake builds out the `/cmake` subdirectory with content specific to your device:</span></span>
 
    - <span data-ttu-id="7c913-136">For devices that use the TPM simulator for attestation:</span><span class="sxs-lookup"><span data-stu-id="7c913-136">For devices that use the TPM simulator for attestation:</span></span>

        ```cmd/sh
        cmake -Duse_prov_client:BOOL=ON -Duse_tpm_simulator:BOOL=ON ..
        ```

    - <span data-ttu-id="7c913-137">For any other device (physical TPM/HSM/X.509, or a simulated X.509 certificate):</span><span class="sxs-lookup"><span data-stu-id="7c913-137">For any other device (physical TPM/HSM/X.509, or a simulated X.509 certificate):</span></span>

        ```cmd/sh
        cmake -Duse_prov_client:BOOL=ON ..
        ```


<span data-ttu-id="7c913-138">Now you're ready to use the SDK to build your device registration code.</span><span class="sxs-lookup"><span data-stu-id="7c913-138">Now you're ready to use the SDK to build your device registration code.</span></span> 
 
<a id="extractsecurity"></a> 

## <a name="extract-the-security-artifacts"></a><span data-ttu-id="7c913-139">Extract the security artifacts</span><span class="sxs-lookup"><span data-stu-id="7c913-139">Extract the security artifacts</span></span> 

<span data-ttu-id="7c913-140">The next step is to extract the security artifacts for the attestation mechanism used by your device.</span><span class="sxs-lookup"><span data-stu-id="7c913-140">The next step is to extract the security artifacts for the attestation mechanism used by your device.</span></span> 

### <a name="physical-devices"></a><span data-ttu-id="7c913-141">Physical devices</span><span class="sxs-lookup"><span data-stu-id="7c913-141">Physical devices</span></span> 

<span data-ttu-id="7c913-142">Depending on whether you built the SDK to use attestation for a physical TPM/HSM or using X.509 certificates, gathering the security artifacts is as follows:</span><span class="sxs-lookup"><span data-stu-id="7c913-142">Depending on whether you built the SDK to use attestation for a physical TPM/HSM or using X.509 certificates, gathering the security artifacts is as follows:</span></span>

- <span data-ttu-id="7c913-143">For a TPM device, you need to determine the **Endorsement Key** associated with it from the TPM chip manufacturer.</span><span class="sxs-lookup"><span data-stu-id="7c913-143">For a TPM device, you need to determine the **Endorsement Key** associated with it from the TPM chip manufacturer.</span></span> <span data-ttu-id="7c913-144">You can derive a unique **Registration ID** for your TPM device by hashing the endorsement key.</span><span class="sxs-lookup"><span data-stu-id="7c913-144">You can derive a unique **Registration ID** for your TPM device by hashing the endorsement key.</span></span>  

- <span data-ttu-id="7c913-145">For an X.509 device, you need to obtain the certificates issued to your device(s).</span><span class="sxs-lookup"><span data-stu-id="7c913-145">For an X.509 device, you need to obtain the certificates issued to your device(s).</span></span> <span data-ttu-id="7c913-146">The provisioning service exposes two types of enrollment entries that control access for devices using the X.509 attestation mechanism.</span><span class="sxs-lookup"><span data-stu-id="7c913-146">The provisioning service exposes two types of enrollment entries that control access for devices using the X.509 attestation mechanism.</span></span> <span data-ttu-id="7c913-147">The certificates needed depend on the enrollment types you will be using.</span><span class="sxs-lookup"><span data-stu-id="7c913-147">The certificates needed depend on the enrollment types you will be using.</span></span>

    1. <span data-ttu-id="7c913-148">Individual enrollments: Enrollment for a specific single device.</span><span class="sxs-lookup"><span data-stu-id="7c913-148">Individual enrollments: Enrollment for a specific single device.</span></span> <span data-ttu-id="7c913-149">This type of enrollment entry requires [end-entity, "leaf", certificates](concepts-security.md#end-entity-leaf-certificate).</span><span class="sxs-lookup"><span data-stu-id="7c913-149">This type of enrollment entry requires [end-entity, "leaf", certificates](concepts-security.md#end-entity-leaf-certificate).</span></span>
    1. <span data-ttu-id="7c913-150">Enrollment groups: This type of enrollment entry requires intermediate or root certificates.</span><span class="sxs-lookup"><span data-stu-id="7c913-150">Enrollment groups: This type of enrollment entry requires intermediate or root certificates.</span></span> <span data-ttu-id="7c913-151">For more information, see [Controlling device access to the provisioning service with X.509 certificates](concepts-security.md#controlling-device-access-to-the-provisioning-service-with-x509-certificates).</span><span class="sxs-lookup"><span data-stu-id="7c913-151">For more information, see [Controlling device access to the provisioning service with X.509 certificates](concepts-security.md#controlling-device-access-to-the-provisioning-service-with-x509-certificates).</span></span>

### <a name="simulated-devices"></a><span data-ttu-id="7c913-152">Simulated devices</span><span class="sxs-lookup"><span data-stu-id="7c913-152">Simulated devices</span></span>

<span data-ttu-id="7c913-153">Depending on whether you built the SDK to use attestation for a simulated device using TPM or X.509 certificates, gathering the security artifacts is as follows:</span><span class="sxs-lookup"><span data-stu-id="7c913-153">Depending on whether you built the SDK to use attestation for a simulated device using TPM or X.509 certificates, gathering the security artifacts is as follows:</span></span>

- <span data-ttu-id="7c913-154">For a simulated TPM device:</span><span class="sxs-lookup"><span data-stu-id="7c913-154">For a simulated TPM device:</span></span>

   1. <span data-ttu-id="7c913-155">Open a Windows Command Prompt, navigate to the `azure-iot-sdk-c` subdirectory, and run the TPM simulator.</span><span class="sxs-lookup"><span data-stu-id="7c913-155">Open a Windows Command Prompt, navigate to the `azure-iot-sdk-c` subdirectory, and run the TPM simulator.</span></span> <span data-ttu-id="7c913-156">It listens over a socket on ports 2321 and 2322.</span><span class="sxs-lookup"><span data-stu-id="7c913-156">It listens over a socket on ports 2321 and 2322.</span></span> <span data-ttu-id="7c913-157">Do not close this command window; you will need to keep this simulator running until the end of the following Quickstart.</span><span class="sxs-lookup"><span data-stu-id="7c913-157">Do not close this command window; you will need to keep this simulator running until the end of the following Quickstart.</span></span> 

      <span data-ttu-id="7c913-158">From the `azure-iot-sdk-c` subdirectory, run the following command to start the simulator:</span><span class="sxs-lookup"><span data-stu-id="7c913-158">From the `azure-iot-sdk-c` subdirectory, run the following command to start the simulator:</span></span>

      ```cmd/sh
      .\provisioning_client\deps\utpm\tools\tpm_simulator\Simulator.exe
      ```

      > [!NOTE]
      > <span data-ttu-id="7c913-159">If you use the Git Bash command prompt for this step, you'll need to change the backslashes to forward slashes, for example: `./provisioning_client/deps/utpm/tools/tpm_simulator/Simulator.exe`.</span><span class="sxs-lookup"><span data-stu-id="7c913-159">If you use the Git Bash command prompt for this step, you'll need to change the backslashes to forward slashes, for example: `./provisioning_client/deps/utpm/tools/tpm_simulator/Simulator.exe`.</span></span>

   1. <span data-ttu-id="7c913-160">Using Visual Studio, open the solution generated in the *cmake* folder named `azure_iot_sdks.sln`, and build it using the "Build solution" command on the "Build" menu.</span><span class="sxs-lookup"><span data-stu-id="7c913-160">Using Visual Studio, open the solution generated in the *cmake* folder named `azure_iot_sdks.sln`, and build it using the "Build solution" command on the "Build" menu.</span></span>

   1. <span data-ttu-id="7c913-161">In the *Solution Explorer* pane in Visual Studio, navigate to the folder **Provision\_Tools**.</span><span class="sxs-lookup"><span data-stu-id="7c913-161">In the *Solution Explorer* pane in Visual Studio, navigate to the folder **Provision\_Tools**.</span></span> <span data-ttu-id="7c913-162">Right-click the **tpm_device_provision** project and select **Set as Startup Project**.</span><span class="sxs-lookup"><span data-stu-id="7c913-162">Right-click the **tpm_device_provision** project and select **Set as Startup Project**.</span></span> 

   1. <span data-ttu-id="7c913-163">Run the solution using either of the "Start" commands on the "Debug" menu.</span><span class="sxs-lookup"><span data-stu-id="7c913-163">Run the solution using either of the "Start" commands on the "Debug" menu.</span></span> <span data-ttu-id="7c913-164">The output window displays the TPM simulator's **_Registration ID_** and the **_Endorsement Key_**, needed for device enrollment and registration.</span><span class="sxs-lookup"><span data-stu-id="7c913-164">The output window displays the TPM simulator's **_Registration ID_** and the **_Endorsement Key_**, needed for device enrollment and registration.</span></span> <span data-ttu-id="7c913-165">Copy these values for use later.</span><span class="sxs-lookup"><span data-stu-id="7c913-165">Copy these values for use later.</span></span> <span data-ttu-id="7c913-166">You can close this window (with Registration ID and Endorsement Key), but leave the TPM simulator window running that you started in step #1.</span><span class="sxs-lookup"><span data-stu-id="7c913-166">You can close this window (with Registration ID and Endorsement Key), but leave the TPM simulator window running that you started in step #1.</span></span>

- <span data-ttu-id="7c913-167">For a simulated X.509 device:</span><span class="sxs-lookup"><span data-stu-id="7c913-167">For a simulated X.509 device:</span></span>

  1. <span data-ttu-id="7c913-168">Using Visual Studio, open the solution generated in the *cmake* folder named `azure_iot_sdks.sln`, and build it using the "Build solution" command on the "Build" menu.</span><span class="sxs-lookup"><span data-stu-id="7c913-168">Using Visual Studio, open the solution generated in the *cmake* folder named `azure_iot_sdks.sln`, and build it using the "Build solution" command on the "Build" menu.</span></span>

  1. <span data-ttu-id="7c913-169">In the *Solution Explorer* pane in Visual Studio, navigate to the folder **Provision\_Tools**.</span><span class="sxs-lookup"><span data-stu-id="7c913-169">In the *Solution Explorer* pane in Visual Studio, navigate to the folder **Provision\_Tools**.</span></span> <span data-ttu-id="7c913-170">Right-click the **dice\_device\_enrollment** project and select **Set as Startup Project**.</span><span class="sxs-lookup"><span data-stu-id="7c913-170">Right-click the **dice\_device\_enrollment** project and select **Set as Startup Project**.</span></span> 
  
  1. <span data-ttu-id="7c913-171">Run the solution using either of the "Start" commands on the "Debug" menu.</span><span class="sxs-lookup"><span data-stu-id="7c913-171">Run the solution using either of the "Start" commands on the "Debug" menu.</span></span> <span data-ttu-id="7c913-172">In the output window, enter **i** for individual enrollment when prompted.</span><span class="sxs-lookup"><span data-stu-id="7c913-172">In the output window, enter **i** for individual enrollment when prompted.</span></span> <span data-ttu-id="7c913-173">The output window displays a locally generated X.509 certificate for your simulated device.</span><span class="sxs-lookup"><span data-stu-id="7c913-173">The output window displays a locally generated X.509 certificate for your simulated device.</span></span> <span data-ttu-id="7c913-174">Copy to clipboard the output starting from *-----BEGIN CERTIFICATE-----* and ending at the first *-----END CERTIFICATE-----*, making sure to include both of these lines as well.</span><span class="sxs-lookup"><span data-stu-id="7c913-174">Copy to clipboard the output starting from *-----BEGIN CERTIFICATE-----* and ending at the first *-----END CERTIFICATE-----*, making sure to include both of these lines as well.</span></span> <span data-ttu-id="7c913-175">You only need the first certificate from the output window.</span><span class="sxs-lookup"><span data-stu-id="7c913-175">You only need the first certificate from the output window.</span></span>
 
  1. <span data-ttu-id="7c913-176">Create a file named **_X509testcert.pem_**, open it in a text editor of your choice, and copy the clipboard contents to this file.</span><span class="sxs-lookup"><span data-stu-id="7c913-176">Create a file named **_X509testcert.pem_**, open it in a text editor of your choice, and copy the clipboard contents to this file.</span></span> <span data-ttu-id="7c913-177">Save the file as you will use it later for device enrollment.</span><span class="sxs-lookup"><span data-stu-id="7c913-177">Save the file as you will use it later for device enrollment.</span></span> <span data-ttu-id="7c913-178">When your registration software runs, it uses the same certificate during auto-provisioning.</span><span class="sxs-lookup"><span data-stu-id="7c913-178">When your registration software runs, it uses the same certificate during auto-provisioning.</span></span>    

<span data-ttu-id="7c913-179">These security artifacts are required during enrollment your device to the Device Provisioning Service.</span><span class="sxs-lookup"><span data-stu-id="7c913-179">These security artifacts are required during enrollment your device to the Device Provisioning Service.</span></span> <span data-ttu-id="7c913-180">The provisioning service waits for the device to boot and connect with it at any later point in time.</span><span class="sxs-lookup"><span data-stu-id="7c913-180">The provisioning service waits for the device to boot and connect with it at any later point in time.</span></span> <span data-ttu-id="7c913-181">When your device boots for the first time, the client SDK logic interacts with your chip (or simulator) to extract the security artifacts from the device, and verifies registration with your Device Provisioning service.</span><span class="sxs-lookup"><span data-stu-id="7c913-181">When your device boots for the first time, the client SDK logic interacts with your chip (or simulator) to extract the security artifacts from the device, and verifies registration with your Device Provisioning service.</span></span> 

## <a name="create-the-device-registration-software"></a><span data-ttu-id="7c913-182">Create the device registration software</span><span class="sxs-lookup"><span data-stu-id="7c913-182">Create the device registration software</span></span>

<span data-ttu-id="7c913-183">The last step is to write a registration application that uses the Device Provisioning Service client SDK to register the device with the IoT Hub service.</span><span class="sxs-lookup"><span data-stu-id="7c913-183">The last step is to write a registration application that uses the Device Provisioning Service client SDK to register the device with the IoT Hub service.</span></span> 

> [!NOTE]
> <span data-ttu-id="7c913-184">For this step we will assume the use of a simulated device, accomplished by running an SDK sample registration application from your workstation.</span><span class="sxs-lookup"><span data-stu-id="7c913-184">For this step we will assume the use of a simulated device, accomplished by running an SDK sample registration application from your workstation.</span></span> <span data-ttu-id="7c913-185">However, the same concepts apply if you are building a registration application for deployment to a physical device.</span><span class="sxs-lookup"><span data-stu-id="7c913-185">However, the same concepts apply if you are building a registration application for deployment to a physical device.</span></span> 

1. <span data-ttu-id="7c913-186">In the Azure portal, select the **Overview** blade for your Device Provisioning service and copy the **_ID Scope_** value.</span><span class="sxs-lookup"><span data-stu-id="7c913-186">In the Azure portal, select the **Overview** blade for your Device Provisioning service and copy the **_ID Scope_** value.</span></span> <span data-ttu-id="7c913-187">The *ID Scope* is generated by the service and guarantees uniqueness.</span><span class="sxs-lookup"><span data-stu-id="7c913-187">The *ID Scope* is generated by the service and guarantees uniqueness.</span></span> <span data-ttu-id="7c913-188">It is immutable and used to uniquely identify the registration IDs.</span><span class="sxs-lookup"><span data-stu-id="7c913-188">It is immutable and used to uniquely identify the registration IDs.</span></span>

    ![Extract Device Provisioning Service endpoint information from the portal blade](./media/tutorial-set-up-device/extract-dps-endpoints.png) 

1. <span data-ttu-id="7c913-190">In the Visual Studio *Solution Explorer* on your machine, navigate to the folder **Provision\_Samples**.</span><span class="sxs-lookup"><span data-stu-id="7c913-190">In the Visual Studio *Solution Explorer* on your machine, navigate to the folder **Provision\_Samples**.</span></span> <span data-ttu-id="7c913-191">Select the sample project named **prov\_dev\_client\_sample** and open the source file **prov\_dev\_client\_sample.c**.</span><span class="sxs-lookup"><span data-stu-id="7c913-191">Select the sample project named **prov\_dev\_client\_sample** and open the source file **prov\_dev\_client\_sample.c**.</span></span>

1. <span data-ttu-id="7c913-192">Assign the _ID Scope_ value obtained in step #1, to the `id_scope` variable (removing the left/`[` and right/`]` brackets):</span><span class="sxs-lookup"><span data-stu-id="7c913-192">Assign the _ID Scope_ value obtained in step #1, to the `id_scope` variable (removing the left/`[` and right/`]` brackets):</span></span> 

    ```c
    static const char* global_prov_uri = "global.azure-devices-provisioning.net";
    static const char* id_scope = "[ID Scope]";
    ```

    <span data-ttu-id="7c913-193">For reference, the `global_prov_uri` variable, which allows the IoT Hub client registration API `IoTHubClient_LL_CreateFromDeviceAuth` to connect with the designated Device Provisioning Service instance.</span><span class="sxs-lookup"><span data-stu-id="7c913-193">For reference, the `global_prov_uri` variable, which allows the IoT Hub client registration API `IoTHubClient_LL_CreateFromDeviceAuth` to connect with the designated Device Provisioning Service instance.</span></span>

1. <span data-ttu-id="7c913-194">In the **main()** function in the same file, comment/uncomment the `hsm_type` variable that matches the attestation mechanism being used by your device's registration software (TPM or X.509):</span><span class="sxs-lookup"><span data-stu-id="7c913-194">In the **main()** function in the same file, comment/uncomment the `hsm_type` variable that matches the attestation mechanism being used by your device's registration software (TPM or X.509):</span></span> 

    ```c
    hsm_type = SECURE_DEVICE_TYPE_TPM;
    //hsm_type = SECURE_DEVICE_TYPE_X509;
    ```

1. <span data-ttu-id="7c913-195">Save your changes and rebuild the **prov\_dev\_client\_sample** sample by selecting "Build solution" from the "Build" menu.</span><span class="sxs-lookup"><span data-stu-id="7c913-195">Save your changes and rebuild the **prov\_dev\_client\_sample** sample by selecting "Build solution" from the "Build" menu.</span></span> 

1. <span data-ttu-id="7c913-196">Right-click the **prov\_dev\_client\_sample** project under the **Provision\_Samples** folder, and select **Set as Startup Project**.</span><span class="sxs-lookup"><span data-stu-id="7c913-196">Right-click the **prov\_dev\_client\_sample** project under the **Provision\_Samples** folder, and select **Set as Startup Project**.</span></span> <span data-ttu-id="7c913-197">DO NOT run the sample application yet.</span><span class="sxs-lookup"><span data-stu-id="7c913-197">DO NOT run the sample application yet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7c913-198">Do not run/start the device yet!</span><span class="sxs-lookup"><span data-stu-id="7c913-198">Do not run/start the device yet!</span></span> <span data-ttu-id="7c913-199">You need to finish the process by enrolling the device with the Device Provisioning Service first, before starting the device.</span><span class="sxs-lookup"><span data-stu-id="7c913-199">You need to finish the process by enrolling the device with the Device Provisioning Service first, before starting the device.</span></span> <span data-ttu-id="7c913-200">The Next steps section below will guide you to the next article.</span><span class="sxs-lookup"><span data-stu-id="7c913-200">The Next steps section below will guide you to the next article.</span></span>

### <a name="sdk-apis-used-during-registration-for-reference-only"></a><span data-ttu-id="7c913-201">SDK APIs used during registration (for reference only)</span><span class="sxs-lookup"><span data-stu-id="7c913-201">SDK APIs used during registration (for reference only)</span></span>

<span data-ttu-id="7c913-202">For reference, the SDK provides the following APIs for your application to use during registration.</span><span class="sxs-lookup"><span data-stu-id="7c913-202">For reference, the SDK provides the following APIs for your application to use during registration.</span></span> <span data-ttu-id="7c913-203">These APIs help your device connect and register with the Device Provisioning Service when it boots up.</span><span class="sxs-lookup"><span data-stu-id="7c913-203">These APIs help your device connect and register with the Device Provisioning Service when it boots up.</span></span> <span data-ttu-id="7c913-204">In return, your device receives the information required to establish a connection to your IoT Hub instance:</span><span class="sxs-lookup"><span data-stu-id="7c913-204">In return, your device receives the information required to establish a connection to your IoT Hub instance:</span></span>

```C
// Creates a Provisioning Client for communications with the Device Provisioning Client Service.  
PROV_DEVICE_LL_HANDLE Prov_Device_LL_Create(const char* uri, const char* scope_id, PROV_DEVICE_TRANSPORT_PROVIDER_FUNCTION protocol)

// Disposes of resources allocated by the provisioning Client.
void Prov_Device_LL_Destroy(PROV_DEVICE_LL_HANDLE handle)

// Asynchronous call initiates the registration of a device.
PROV_DEVICE_RESULT Prov_Device_LL_Register_Device(PROV_DEVICE_LL_HANDLE handle, PROV_DEVICE_CLIENT_REGISTER_DEVICE_CALLBACK register_callback, void* user_context, PROV_DEVICE_CLIENT_REGISTER_STATUS_CALLBACK reg_status_cb, void* status_user_ctext)

// Api to be called by user when work (registering device) can be done
void Prov_Device_LL_DoWork(PROV_DEVICE_LL_HANDLE handle)

// API sets a runtime option identified by parameter optionName to a value pointed to by value
PROV_DEVICE_RESULT Prov_Device_LL_SetOption(PROV_DEVICE_LL_HANDLE handle, const char* optionName, const void* value)
```

<span data-ttu-id="7c913-205">You may also find that you need to refine your Device Provisioning Service client registration application, using a simulated device at first, and a test service setup.</span><span class="sxs-lookup"><span data-stu-id="7c913-205">You may also find that you need to refine your Device Provisioning Service client registration application, using a simulated device at first, and a test service setup.</span></span> <span data-ttu-id="7c913-206">Once your application is working in the test environment, you can build it for your specific device and copy the executable to your device image.</span><span class="sxs-lookup"><span data-stu-id="7c913-206">Once your application is working in the test environment, you can build it for your specific device and copy the executable to your device image.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="7c913-207">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="7c913-207">Clean up resources</span></span>

<span data-ttu-id="7c913-208">At this point, you might have the Device Provisioning and IoT Hub services running in the portal.</span><span class="sxs-lookup"><span data-stu-id="7c913-208">At this point, you might have the Device Provisioning and IoT Hub services running in the portal.</span></span> <span data-ttu-id="7c913-209">If you wish to abandon the device provisioning setup, and/or delay completion of this tutorial series, we recommend shutting them down to avoid incurring unnecessary costs.</span><span class="sxs-lookup"><span data-stu-id="7c913-209">If you wish to abandon the device provisioning setup, and/or delay completion of this tutorial series, we recommend shutting them down to avoid incurring unnecessary costs.</span></span>

1. <span data-ttu-id="7c913-210">From the left-hand menu in the Azure portal, click **All resources** and then select your Device Provisioning service.</span><span class="sxs-lookup"><span data-stu-id="7c913-210">From the left-hand menu in the Azure portal, click **All resources** and then select your Device Provisioning service.</span></span> <span data-ttu-id="7c913-211">At the top of the **All resources** blade, click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="7c913-211">At the top of the **All resources** blade, click **Delete**.</span></span>  
1. <span data-ttu-id="7c913-212">From the left-hand menu in the Azure portal, click **All resources** and then select your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="7c913-212">From the left-hand menu in the Azure portal, click **All resources** and then select your IoT hub.</span></span> <span data-ttu-id="7c913-213">At the top of the **All resources** blade, click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="7c913-213">At the top of the **All resources** blade, click **Delete**.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="7c913-214">Next steps</span><span class="sxs-lookup"><span data-stu-id="7c913-214">Next steps</span></span>
<span data-ttu-id="7c913-215">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="7c913-215">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7c913-216">Build platform-specific Device Provisioning Service Client SDK</span><span class="sxs-lookup"><span data-stu-id="7c913-216">Build platform-specific Device Provisioning Service Client SDK</span></span>
> * <span data-ttu-id="7c913-217">Extract the security artifacts</span><span class="sxs-lookup"><span data-stu-id="7c913-217">Extract the security artifacts</span></span>
> * <span data-ttu-id="7c913-218">Create the device registration software</span><span class="sxs-lookup"><span data-stu-id="7c913-218">Create the device registration software</span></span>

<span data-ttu-id="7c913-219">Advance to the next tutorial to learn how to provision the device to your IoT hub by enrolling it to the Azure IoT Hub Device Provisioning Service for auto-provisioning.</span><span class="sxs-lookup"><span data-stu-id="7c913-219">Advance to the next tutorial to learn how to provision the device to your IoT hub by enrolling it to the Azure IoT Hub Device Provisioning Service for auto-provisioning.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7c913-220">Provision the device to your IoT hub</span><span class="sxs-lookup"><span data-stu-id="7c913-220">Provision the device to your IoT hub</span></span>](tutorial-provision-device-to-hub.md)

