---
title: Provision a simulated TPM device to Azure IoT Hub using C | Microsoft Docs
description: In this quickstart you create and provision a simulated TPM device using C device SDK for Azure IoT Hub Device Provisioning Service
author: wesmc7777
ms.author: wesmc
ms.date: 07/13/2018
ms.topic: quickstart
ms.service: iot-dps
services: iot-dps
manager: timlt
ms.custom: mvc
ms.openlocfilehash: 4e03268db32b4be6900234abe58e7a308110520a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865509"
---
# <a name="quickstart-provision-a-simulated-tpm-device-using-the-azure-iot-c-sdk"></a><span data-ttu-id="79196-103">Quickstart: Provision a simulated TPM device using the Azure IoT C SDK</span><span class="sxs-lookup"><span data-stu-id="79196-103">Quickstart: Provision a simulated TPM device using the Azure IoT C SDK</span></span>

[!INCLUDE [iot-dps-selector-quick-create-simulated-device-tpm](../../includes/iot-dps-selector-quick-create-simulated-device-tpm.md)]

<span data-ttu-id="79196-104">In this quickstart, you will learn how to create and run a Trusted Platform Module (TPM) device simulator on a Windows development machine.</span><span class="sxs-lookup"><span data-stu-id="79196-104">In this quickstart, you will learn how to create and run a Trusted Platform Module (TPM) device simulator on a Windows development machine.</span></span> <span data-ttu-id="79196-105">You will connect this simulated device to an IoT hub using a Device Provisioning Service instance.</span><span class="sxs-lookup"><span data-stu-id="79196-105">You will connect this simulated device to an IoT hub using a Device Provisioning Service instance.</span></span> <span data-ttu-id="79196-106">Sample code from the [Azure IoT C SDK](https://github.com/Azure/azure-iot-sdk-c) will be used to help enroll the device with a Device Provisioning Service instance and simulate a boot sequence for the device.</span><span class="sxs-lookup"><span data-stu-id="79196-106">Sample code from the [Azure IoT C SDK](https://github.com/Azure/azure-iot-sdk-c) will be used to help enroll the device with a Device Provisioning Service instance and simulate a boot sequence for the device.</span></span>

<span data-ttu-id="79196-107">If you're unfamiliar with the process of auto-provisioning, review [Auto-provisioning concepts](concepts-auto-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="79196-107">If you're unfamiliar with the process of auto-provisioning, review [Auto-provisioning concepts](concepts-auto-provisioning.md).</span></span> <span data-ttu-id="79196-108">Also, make sure you've completed the steps in [Set up IoT Hub Device Provisioning Service with the Azure portal](./quick-setup-auto-provision.md) before continuing with this quickstart.</span><span class="sxs-lookup"><span data-stu-id="79196-108">Also, make sure you've completed the steps in [Set up IoT Hub Device Provisioning Service with the Azure portal](./quick-setup-auto-provision.md) before continuing with this quickstart.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="79196-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="79196-109">Prerequisites</span></span>

* <span data-ttu-id="79196-110">Visual Studio 2015 or [Visual Studio 2017](https://www.visualstudio.com/vs/) with the ['Desktop development with C++'](https://www.visualstudio.com/vs/support/selecting-workloads-visual-studio-2017/) workload enabled.</span><span class="sxs-lookup"><span data-stu-id="79196-110">Visual Studio 2015 or [Visual Studio 2017](https://www.visualstudio.com/vs/) with the ['Desktop development with C++'](https://www.visualstudio.com/vs/support/selecting-workloads-visual-studio-2017/) workload enabled.</span></span>
* <span data-ttu-id="79196-111">Latest version of [Git](https://git-scm.com/download/) installed.</span><span class="sxs-lookup"><span data-stu-id="79196-111">Latest version of [Git](https://git-scm.com/download/) installed.</span></span>


<a id="setupdevbox"></a>

## <a name="prepare-a-development-environment-for-the-azure-iot-c-sdk"></a><span data-ttu-id="79196-112">Prepare a development environment for the Azure IoT C SDK</span><span class="sxs-lookup"><span data-stu-id="79196-112">Prepare a development environment for the Azure IoT C SDK</span></span>

<span data-ttu-id="79196-113">In this section, you will prepare a development environment used to build the [Azure IoT C SDK](https://github.com/Azure/azure-iot-sdk-c) and the [TPM](https://docs.microsoft.com/windows/device-security/tpm/trusted-platform-module-overview) device simulator sample.</span><span class="sxs-lookup"><span data-stu-id="79196-113">In this section, you will prepare a development environment used to build the [Azure IoT C SDK](https://github.com/Azure/azure-iot-sdk-c) and the [TPM](https://docs.microsoft.com/windows/device-security/tpm/trusted-platform-module-overview) device simulator sample.</span></span>

1. <span data-ttu-id="79196-114">Download the latest release version of the [CMake build system](https://cmake.org/download/).</span><span class="sxs-lookup"><span data-stu-id="79196-114">Download the latest release version of the [CMake build system](https://cmake.org/download/).</span></span> <span data-ttu-id="79196-115">From that same site, look up the cryptographic hash for the version of the binary distribution you chose.</span><span class="sxs-lookup"><span data-stu-id="79196-115">From that same site, look up the cryptographic hash for the version of the binary distribution you chose.</span></span> <span data-ttu-id="79196-116">Verify the downloaded binary using the corresponding cryptographic hash value.</span><span class="sxs-lookup"><span data-stu-id="79196-116">Verify the downloaded binary using the corresponding cryptographic hash value.</span></span> <span data-ttu-id="79196-117">The following example used Windows PowerShell to verify the cryptographic hash for version 3.11.4 of the x64 MSI distribution:</span><span class="sxs-lookup"><span data-stu-id="79196-117">The following example used Windows PowerShell to verify the cryptographic hash for version 3.11.4 of the x64 MSI distribution:</span></span>

    ```PowerShell
    PS C:\Users\wesmc\Downloads> $hash = get-filehash .\cmake-3.11.4-win64-x64.msi
    PS C:\Users\wesmc\Downloads> $hash.Hash -eq "56e3605b8e49cd446f3487da88fcc38cb9c3e9e99a20f5d4bd63e54b7a35f869"
    True
    ```

    <span data-ttu-id="79196-118">It is important that the Visual Studio prerequisites (Visual Studio and the 'Desktop development with C++' workload) are installed on your machine, **before** starting the `CMake` installation.</span><span class="sxs-lookup"><span data-stu-id="79196-118">It is important that the Visual Studio prerequisites (Visual Studio and the 'Desktop development with C++' workload) are installed on your machine, **before** starting the `CMake` installation.</span></span> <span data-ttu-id="79196-119">Once the prerequisites are in place, and the download is verified, install the CMake build system.</span><span class="sxs-lookup"><span data-stu-id="79196-119">Once the prerequisites are in place, and the download is verified, install the CMake build system.</span></span>

2. <span data-ttu-id="79196-120">Open a command prompt or Git Bash shell.</span><span class="sxs-lookup"><span data-stu-id="79196-120">Open a command prompt or Git Bash shell.</span></span> <span data-ttu-id="79196-121">Execute the following command to clone the [Azure IoT C SDK](https://github.com/Azure/azure-iot-sdk-c) GitHub repository:</span><span class="sxs-lookup"><span data-stu-id="79196-121">Execute the following command to clone the [Azure IoT C SDK](https://github.com/Azure/azure-iot-sdk-c) GitHub repository:</span></span>
    
    ```cmd/sh
    git clone https://github.com/Azure/azure-iot-sdk-c.git --recursive
    ```
    <span data-ttu-id="79196-122">The size of this repository is currently around 220 MB.</span><span class="sxs-lookup"><span data-stu-id="79196-122">The size of this repository is currently around 220 MB.</span></span> <span data-ttu-id="79196-123">You should expect this operation to take several minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="79196-123">You should expect this operation to take several minutes to complete.</span></span>


3. <span data-ttu-id="79196-124">Create a `cmake` subdirectory in the root directory of the git repository, and navigate to that folder.</span><span class="sxs-lookup"><span data-stu-id="79196-124">Create a `cmake` subdirectory in the root directory of the git repository, and navigate to that folder.</span></span> 

    ```cmd/sh
    cd azure-iot-sdk-c
    mkdir cmake
    cd cmake
    ```

## <a name="build-the-sdk-and-run-the-tpm-device-simulator"></a><span data-ttu-id="79196-125">Build the SDK and run the TPM device simulator</span><span class="sxs-lookup"><span data-stu-id="79196-125">Build the SDK and run the TPM device simulator</span></span>

<span data-ttu-id="79196-126">In this section, you will build the Azure IoT C SDK, which includes the TPM device simulator sample code.</span><span class="sxs-lookup"><span data-stu-id="79196-126">In this section, you will build the Azure IoT C SDK, which includes the TPM device simulator sample code.</span></span> <span data-ttu-id="79196-127">This sample provides a TPM [attestation mechanism](concepts-security.md#attestation-mechanism) via Shared Access Signature (SAS) Token authentication.</span><span class="sxs-lookup"><span data-stu-id="79196-127">This sample provides a TPM [attestation mechanism](concepts-security.md#attestation-mechanism) via Shared Access Signature (SAS) Token authentication.</span></span>

1. <span data-ttu-id="79196-128">From the `cmake` subdirectory you created in the azure-iot-sdk-c git repository, run the following command to build the sample.</span><span class="sxs-lookup"><span data-stu-id="79196-128">From the `cmake` subdirectory you created in the azure-iot-sdk-c git repository, run the following command to build the sample.</span></span> <span data-ttu-id="79196-129">A Visual Studio solution for the simulated device will also be generated by this build command.</span><span class="sxs-lookup"><span data-stu-id="79196-129">A Visual Studio solution for the simulated device will also be generated by this build command.</span></span>

    ```cmd/sh
    cmake -Duse_prov_client:BOOL=ON -Duse_tpm_simulator:BOOL=ON ..
    ```

    <span data-ttu-id="79196-130">If `cmake` does not find your C++ compiler, you might get build errors while running the above command.</span><span class="sxs-lookup"><span data-stu-id="79196-130">If `cmake` does not find your C++ compiler, you might get build errors while running the above command.</span></span> <span data-ttu-id="79196-131">If that happens, try running this command in the [Visual Studio command prompt](https://docs.microsoft.com/dotnet/framework/tools/developer-command-prompt-for-vs).</span><span class="sxs-lookup"><span data-stu-id="79196-131">If that happens, try running this command in the [Visual Studio command prompt](https://docs.microsoft.com/dotnet/framework/tools/developer-command-prompt-for-vs).</span></span> 

    <span data-ttu-id="79196-132">Once the build succeeds, the last few output lines will look similar to the following output:</span><span class="sxs-lookup"><span data-stu-id="79196-132">Once the build succeeds, the last few output lines will look similar to the following output:</span></span>

    ```cmd/sh
    $ cmake -Duse_prov_client:BOOL=ON -Duse_tpm_simulator:BOOL=ON ..
    -- Building for: Visual Studio 15 2017
    -- Selecting Windows SDK version 10.0.16299.0 to target Windows 10.0.17134.
    -- The C compiler identification is MSVC 19.12.25835.0
    -- The CXX compiler identification is MSVC 19.12.25835.0

    ...

    -- Configuring done
    -- Generating done
    -- Build files have been written to: E:/IoT Testing/azure-iot-sdk-c/cmake
    ```

2. <span data-ttu-id="79196-133">Navigate to the root folder of the git repository you cloned, and run the [TPM](https://docs.microsoft.com/windows/device-security/tpm/trusted-platform-module-overview) simulator using the path shown below.</span><span class="sxs-lookup"><span data-stu-id="79196-133">Navigate to the root folder of the git repository you cloned, and run the [TPM](https://docs.microsoft.com/windows/device-security/tpm/trusted-platform-module-overview) simulator using the path shown below.</span></span> <span data-ttu-id="79196-134">This simulator listens over a socket on ports 2321 and 2322.</span><span class="sxs-lookup"><span data-stu-id="79196-134">This simulator listens over a socket on ports 2321 and 2322.</span></span> <span data-ttu-id="79196-135">Do not close this command window; you will need to keep this simulator running until the end of this quickstart.</span><span class="sxs-lookup"><span data-stu-id="79196-135">Do not close this command window; you will need to keep this simulator running until the end of this quickstart.</span></span> 

   <span data-ttu-id="79196-136">If you are in the *cmake* folder, then run the following commands:</span><span class="sxs-lookup"><span data-stu-id="79196-136">If you are in the *cmake* folder, then run the following commands:</span></span>

    ```cmd/sh
    cd ..
    .\provisioning_client\deps\utpm\tools\tpm_simulator\Simulator.exe
    ```

    <span data-ttu-id="79196-137">You will not see any output from the simulator.</span><span class="sxs-lookup"><span data-stu-id="79196-137">You will not see any output from the simulator.</span></span> <span data-ttu-id="79196-138">Let it continue to run simulating a TPM device.</span><span class="sxs-lookup"><span data-stu-id="79196-138">Let it continue to run simulating a TPM device.</span></span>

<a id="simulatetpm"></a>

## <a name="read-cryptographic-keys-from-the-tpm-device"></a><span data-ttu-id="79196-139">Read cryptographic keys from the TPM device</span><span class="sxs-lookup"><span data-stu-id="79196-139">Read cryptographic keys from the TPM device</span></span>

<span data-ttu-id="79196-140">In this section, you will build and execute a sample that will read the endorsement key and registration ID from the TPM simulator you left running, and listening over ports 2321 and 2322.</span><span class="sxs-lookup"><span data-stu-id="79196-140">In this section, you will build and execute a sample that will read the endorsement key and registration ID from the TPM simulator you left running, and listening over ports 2321 and 2322.</span></span> <span data-ttu-id="79196-141">These values will be used for device enrollment with your Device Provisioning Service instance.</span><span class="sxs-lookup"><span data-stu-id="79196-141">These values will be used for device enrollment with your Device Provisioning Service instance.</span></span>

1. <span data-ttu-id="79196-142">Launch Visual Studio and open the new solution file named `azure_iot_sdks.sln`.</span><span class="sxs-lookup"><span data-stu-id="79196-142">Launch Visual Studio and open the new solution file named `azure_iot_sdks.sln`.</span></span> <span data-ttu-id="79196-143">This solution file is located in the `cmake` folder you previously created in the root of the azure-iot-sdk-c git repository.</span><span class="sxs-lookup"><span data-stu-id="79196-143">This solution file is located in the `cmake` folder you previously created in the root of the azure-iot-sdk-c git repository.</span></span>

2. <span data-ttu-id="79196-144">On the Visual Studio menu, select **Build** > **Build Solution** to build all projects in the solution.</span><span class="sxs-lookup"><span data-stu-id="79196-144">On the Visual Studio menu, select **Build** > **Build Solution** to build all projects in the solution.</span></span>

3. <span data-ttu-id="79196-145">In Visual Studio's *Solution Explorer* window, navigate to the **Provision\_Tools** folder.</span><span class="sxs-lookup"><span data-stu-id="79196-145">In Visual Studio's *Solution Explorer* window, navigate to the **Provision\_Tools** folder.</span></span> <span data-ttu-id="79196-146">Right-click the **tpm_device_provision** project and select **Set as Startup Project**.</span><span class="sxs-lookup"><span data-stu-id="79196-146">Right-click the **tpm_device_provision** project and select **Set as Startup Project**.</span></span> 

4. <span data-ttu-id="79196-147">On the Visual Studio menu, select **Debug** > **Start without debugging** to run the solution.</span><span class="sxs-lookup"><span data-stu-id="79196-147">On the Visual Studio menu, select **Debug** > **Start without debugging** to run the solution.</span></span> <span data-ttu-id="79196-148">The app reads and displays a **_Registration ID_** and an **_Endorsement Key_**.</span><span class="sxs-lookup"><span data-stu-id="79196-148">The app reads and displays a **_Registration ID_** and an **_Endorsement Key_**.</span></span> <span data-ttu-id="79196-149">Copy these values.</span><span class="sxs-lookup"><span data-stu-id="79196-149">Copy these values.</span></span> <span data-ttu-id="79196-150">They will be used in the next section for device enrollment.</span><span class="sxs-lookup"><span data-stu-id="79196-150">They will be used in the next section for device enrollment.</span></span> 


<a id="portalenrollment"></a>

## <a name="create-a-device-enrollment-entry-in-the-portal"></a><span data-ttu-id="79196-151">Create a device enrollment entry in the portal</span><span class="sxs-lookup"><span data-stu-id="79196-151">Create a device enrollment entry in the portal</span></span>

1. <span data-ttu-id="79196-152">Sign in to the Azure portal, click on the **All resources** button on the left-hand menu and open your Device Provisioning service.</span><span class="sxs-lookup"><span data-stu-id="79196-152">Sign in to the Azure portal, click on the **All resources** button on the left-hand menu and open your Device Provisioning service.</span></span>

2. <span data-ttu-id="79196-153">Select the **Manage enrollments** tab, and then click the **Add individual enrollment** button at the top.</span><span class="sxs-lookup"><span data-stu-id="79196-153">Select the **Manage enrollments** tab, and then click the **Add individual enrollment** button at the top.</span></span> 

3. <span data-ttu-id="79196-154">On **Add enrollment**, enter the following information, and click the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="79196-154">On **Add enrollment**, enter the following information, and click the **Save** button.</span></span>

    - <span data-ttu-id="79196-155">**Mechanism:** Select **TPM** as the identity attestation *Mechanism*.</span><span class="sxs-lookup"><span data-stu-id="79196-155">**Mechanism:** Select **TPM** as the identity attestation *Mechanism*.</span></span>
    - <span data-ttu-id="79196-156">**Endorsement key:** Enter the *Endorsement key* you generated for your TPM device by running the *tpm_device_provision* project.</span><span class="sxs-lookup"><span data-stu-id="79196-156">**Endorsement key:** Enter the *Endorsement key* you generated for your TPM device by running the *tpm_device_provision* project.</span></span>
    - <span data-ttu-id="79196-157">**Registration ID:** Enter the *Registration ID* you generated for your TPM device by running the *tpm_device_provision* project.</span><span class="sxs-lookup"><span data-stu-id="79196-157">**Registration ID:** Enter the *Registration ID* you generated for your TPM device by running the *tpm_device_provision* project.</span></span>
    - <span data-ttu-id="79196-158">**IoT Edge device:** Select **Disable**.</span><span class="sxs-lookup"><span data-stu-id="79196-158">**IoT Edge device:** Select **Disable**.</span></span>
    - <span data-ttu-id="79196-159">**IoT Hub Device ID:** Enter **test-docs-device** to give the device an ID.</span><span class="sxs-lookup"><span data-stu-id="79196-159">**IoT Hub Device ID:** Enter **test-docs-device** to give the device an ID.</span></span>

    ![Enter device enrollment information in the portal](./media/quick-create-simulated-device/enter-device-enrollment.png)  

    <span data-ttu-id="79196-161">On successful enrollment, the *Registration ID* of your device will appear in the list under the *Individual Enrollments* tab.</span><span class="sxs-lookup"><span data-stu-id="79196-161">On successful enrollment, the *Registration ID* of your device will appear in the list under the *Individual Enrollments* tab.</span></span> 


<a id="firstbootsequence"></a>

## <a name="simulate-first-boot-sequence-for-the-device"></a><span data-ttu-id="79196-162">Simulate first boot sequence for the device</span><span class="sxs-lookup"><span data-stu-id="79196-162">Simulate first boot sequence for the device</span></span>

<span data-ttu-id="79196-163">In this section, you will configure sample code to use the [Advanced Message Queuing Protocol (AMQP)](https://wikipedia.org/wiki/Advanced_Message_Queuing_Protocol) to send the device's boot sequence to your Device Provisioning Service instance.</span><span class="sxs-lookup"><span data-stu-id="79196-163">In this section, you will configure sample code to use the [Advanced Message Queuing Protocol (AMQP)](https://wikipedia.org/wiki/Advanced_Message_Queuing_Protocol) to send the device's boot sequence to your Device Provisioning Service instance.</span></span> <span data-ttu-id="79196-164">This boot sequence will cause the device to be recognized and assigned to an IoT hub linked to the Device Provisioning Service instance.</span><span class="sxs-lookup"><span data-stu-id="79196-164">This boot sequence will cause the device to be recognized and assigned to an IoT hub linked to the Device Provisioning Service instance.</span></span>

1. <span data-ttu-id="79196-165">In the Azure portal, select the **Overview** tab for your Device Provisioning service and copy the **_ID Scope_** value.</span><span class="sxs-lookup"><span data-stu-id="79196-165">In the Azure portal, select the **Overview** tab for your Device Provisioning service and copy the **_ID Scope_** value.</span></span>

    ![Extract Device Provisioning Service endpoint information from the portal](./media/quick-create-simulated-device/extract-dps-endpoints.png) 

2. <span data-ttu-id="79196-167">In Visual Studio's *Solution Explorer* window, navigate to the **Provision\_Samples** folder.</span><span class="sxs-lookup"><span data-stu-id="79196-167">In Visual Studio's *Solution Explorer* window, navigate to the **Provision\_Samples** folder.</span></span> <span data-ttu-id="79196-168">Expand the sample project named **prov\_dev\_client\_sample**.</span><span class="sxs-lookup"><span data-stu-id="79196-168">Expand the sample project named **prov\_dev\_client\_sample**.</span></span> <span data-ttu-id="79196-169">Expand **Source Files**, and open **prov\_dev\_client\_sample.c**.</span><span class="sxs-lookup"><span data-stu-id="79196-169">Expand **Source Files**, and open **prov\_dev\_client\_sample.c**.</span></span>

3. <span data-ttu-id="79196-170">Near the top of the file, find the `#define` statements for each device protocol as shown below.</span><span class="sxs-lookup"><span data-stu-id="79196-170">Near the top of the file, find the `#define` statements for each device protocol as shown below.</span></span> <span data-ttu-id="79196-171">Make sure only `SAMPLE_AMQP` is uncommented.</span><span class="sxs-lookup"><span data-stu-id="79196-171">Make sure only `SAMPLE_AMQP` is uncommented.</span></span>

    <span data-ttu-id="79196-172">Currently, the [MQTT protocol is not supported for TPM Individual Enrollment](https://github.com/Azure/azure-iot-sdk-c#provisioning-client-sdk).</span><span class="sxs-lookup"><span data-stu-id="79196-172">Currently, the [MQTT protocol is not supported for TPM Individual Enrollment](https://github.com/Azure/azure-iot-sdk-c#provisioning-client-sdk).</span></span>

    ```c
    //
    // The protocol you wish to use should be uncommented
    //
    //#define SAMPLE_MQTT
    //#define SAMPLE_MQTT_OVER_WEBSOCKETS
    #define SAMPLE_AMQP
    //#define SAMPLE_AMQP_OVER_WEBSOCKETS
    //#define SAMPLE_HTTP
    ```

4. <span data-ttu-id="79196-173">Find the `id_scope` constant, and replace the value with your **ID Scope** value that you copied earlier.</span><span class="sxs-lookup"><span data-stu-id="79196-173">Find the `id_scope` constant, and replace the value with your **ID Scope** value that you copied earlier.</span></span> 

    ```c
    static const char* id_scope = "0ne00002193";
    ```

5. <span data-ttu-id="79196-174">Find the definition for the `main()` function in the same file.</span><span class="sxs-lookup"><span data-stu-id="79196-174">Find the definition for the `main()` function in the same file.</span></span> <span data-ttu-id="79196-175">Make sure the `hsm_type` variable is set to `SECURE_DEVICE_TYPE_TPM` instead of `SECURE_DEVICE_TYPE_X509` as shown below.</span><span class="sxs-lookup"><span data-stu-id="79196-175">Make sure the `hsm_type` variable is set to `SECURE_DEVICE_TYPE_TPM` instead of `SECURE_DEVICE_TYPE_X509` as shown below.</span></span>

    ```c
    SECURE_DEVICE_TYPE hsm_type;
    hsm_type = SECURE_DEVICE_TYPE_TPM;
    //hsm_type = SECURE_DEVICE_TYPE_X509;
    ```

6. <span data-ttu-id="79196-176">Right-click the **prov\_dev\_client\_sample** project and select **Set as Startup Project**.</span><span class="sxs-lookup"><span data-stu-id="79196-176">Right-click the **prov\_dev\_client\_sample** project and select **Set as Startup Project**.</span></span> 

7. <span data-ttu-id="79196-177">On the Visual Studio menu, select **Debug** > **Start without debugging** to run the solution.</span><span class="sxs-lookup"><span data-stu-id="79196-177">On the Visual Studio menu, select **Debug** > **Start without debugging** to run the solution.</span></span> <span data-ttu-id="79196-178">In the prompt to rebuild the project, click **Yes**, to rebuild the project before running.</span><span class="sxs-lookup"><span data-stu-id="79196-178">In the prompt to rebuild the project, click **Yes**, to rebuild the project before running.</span></span>

    <span data-ttu-id="79196-179">The following output is an example of the provisioning device client sample successfully booting up, and connecting to a Device Provisioning Service instance to get IoT hub information and registering:</span><span class="sxs-lookup"><span data-stu-id="79196-179">The following output is an example of the provisioning device client sample successfully booting up, and connecting to a Device Provisioning Service instance to get IoT hub information and registering:</span></span>

    ```cmd
    Provisioning API Version: 1.2.7
    Provisioning Status: PROV_DEVICE_REG_STATUS_CONNECTED

    Registering... Press enter key to interrupt.

    Provisioning Status: PROV_DEVICE_REG_STATUS_CONNECTED
    Provisioning Status: PROV_DEVICE_REG_STATUS_ASSIGNING
    Provisioning Status: PROV_DEVICE_REG_STATUS_ASSIGNING

    Registration Information received from service:
    test-docs-hub.azure-devices.net, deviceId: test-docs-device
    ```

8. <span data-ttu-id="79196-180">Once the simulated device is provisioned to the IoT hub by your provisioning service, the device ID appears with the hub's **IoT Devices**.</span><span class="sxs-lookup"><span data-stu-id="79196-180">Once the simulated device is provisioned to the IoT hub by your provisioning service, the device ID appears with the hub's **IoT Devices**.</span></span> 

    ![Device is registered with the IoT hub](./media/quick-create-simulated-device/hub-registration.png) 


## <a name="clean-up-resources"></a><span data-ttu-id="79196-182">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="79196-182">Clean up resources</span></span>

<span data-ttu-id="79196-183">If you plan to continue working on and exploring the device client sample, do not clean up the resources created in this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="79196-183">If you plan to continue working on and exploring the device client sample, do not clean up the resources created in this Quickstart.</span></span> <span data-ttu-id="79196-184">If you do not plan to continue, use the following steps to delete all resources created by this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="79196-184">If you do not plan to continue, use the following steps to delete all resources created by this Quickstart.</span></span>

1. <span data-ttu-id="79196-185">Close the device client sample output window on your machine.</span><span class="sxs-lookup"><span data-stu-id="79196-185">Close the device client sample output window on your machine.</span></span>
2. <span data-ttu-id="79196-186">Close the TPM simulator window on your machine.</span><span class="sxs-lookup"><span data-stu-id="79196-186">Close the TPM simulator window on your machine.</span></span>
3. <span data-ttu-id="79196-187">From the left-hand menu in the Azure portal, click **All resources** and then select your Device Provisioning service.</span><span class="sxs-lookup"><span data-stu-id="79196-187">From the left-hand menu in the Azure portal, click **All resources** and then select your Device Provisioning service.</span></span> <span data-ttu-id="79196-188">Open **Manage Enrollments** for your service, and then click the **Individual Enrollments** tab. Select the *REGISTRATION ID* of the device you enrolled in this Quickstart, and click the **Delete** button at the top.</span><span class="sxs-lookup"><span data-stu-id="79196-188">Open **Manage Enrollments** for your service, and then click the **Individual Enrollments** tab. Select the *REGISTRATION ID* of the device you enrolled in this Quickstart, and click the **Delete** button at the top.</span></span> 
4. <span data-ttu-id="79196-189">From the left-hand menu in the Azure portal, click **All resources** and then select your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="79196-189">From the left-hand menu in the Azure portal, click **All resources** and then select your IoT hub.</span></span> <span data-ttu-id="79196-190">Open **IoT Devices** for your hub, select the *DEVICE ID* of the device you registered in this Quickstart, and then click **Delete** button at the top.</span><span class="sxs-lookup"><span data-stu-id="79196-190">Open **IoT Devices** for your hub, select the *DEVICE ID* of the device you registered in this Quickstart, and then click **Delete** button at the top.</span></span>

## <a name="next-steps"></a><span data-ttu-id="79196-191">Next steps</span><span class="sxs-lookup"><span data-stu-id="79196-191">Next steps</span></span>

<span data-ttu-id="79196-192">In this Quickstart, you’ve created a TPM simulated device on your machine and provisioned it to your IoT hub using the IoT Hub Device Provisioning Service.</span><span class="sxs-lookup"><span data-stu-id="79196-192">In this Quickstart, you’ve created a TPM simulated device on your machine and provisioned it to your IoT hub using the IoT Hub Device Provisioning Service.</span></span> <span data-ttu-id="79196-193">To learn how to enroll your TPM device programmatically, continue to the Quickstart for programmatic enrollment of a TPM device.</span><span class="sxs-lookup"><span data-stu-id="79196-193">To learn how to enroll your TPM device programmatically, continue to the Quickstart for programmatic enrollment of a TPM device.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="79196-194">Azure Quickstart - Enroll TPM device to Azure IoT Hub Device Provisioning Service</span><span class="sxs-lookup"><span data-stu-id="79196-194">Azure Quickstart - Enroll TPM device to Azure IoT Hub Device Provisioning Service</span></span>](quick-enroll-device-tpm-java.md)

