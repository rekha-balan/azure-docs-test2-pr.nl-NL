---
title: This quickstart shows how to provision a simulated X.509 device to Azure IoT Hub using C | Microsoft Docs
description: In this quickstart you create and provision a simulated X.509 device using C device SDK for Azure IoT Hub Device Provisioning Service
author: wesmc7777
ms.author: wesmc
ms.date: 07/16/2018
ms.topic: quickstart
ms.service: iot-dps
services: iot-dps
manager: timlt
ms.custom: mvc
ms.openlocfilehash: 40d6d149d07f55784e8428eb0faa943814195a47
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865028"
---
# <a name="quickstart-provision-an-x509-simulated-device-using-the-azure-iot-c-sdk"></a><span data-ttu-id="7a2a6-103">Quickstart: Provision an X.509 simulated device using the Azure IoT C SDK</span><span class="sxs-lookup"><span data-stu-id="7a2a6-103">Quickstart: Provision an X.509 simulated device using the Azure IoT C SDK</span></span>

[!INCLUDE [iot-dps-selector-quick-create-simulated-device-x509](../../includes/iot-dps-selector-quick-create-simulated-device-x509.md)]

<span data-ttu-id="7a2a6-104">In this quickstart, you will learn how to create and run a X.509 device simulator on a Windows development machine.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-104">In this quickstart, you will learn how to create and run a X.509 device simulator on a Windows development machine.</span></span> <span data-ttu-id="7a2a6-105">You will configure this simulated device to be assigned to an IoT hub using an enrollment with a Device Provisioning Service instance.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-105">You will configure this simulated device to be assigned to an IoT hub using an enrollment with a Device Provisioning Service instance.</span></span> <span data-ttu-id="7a2a6-106">Sample code from the [Azure IoT C SDK](https://github.com/Azure/azure-iot-sdk-c) will be used to simulate a boot sequence for the device.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-106">Sample code from the [Azure IoT C SDK](https://github.com/Azure/azure-iot-sdk-c) will be used to simulate a boot sequence for the device.</span></span> <span data-ttu-id="7a2a6-107">The device will be recognized based on the enrollment with the provisioning service and assigned to the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-107">The device will be recognized based on the enrollment with the provisioning service and assigned to the IoT hub.</span></span>

<span data-ttu-id="7a2a6-108">If you're unfamiliar with the process of auto-provisioning, review [Auto-provisioning concepts](concepts-auto-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="7a2a6-108">If you're unfamiliar with the process of auto-provisioning, review [Auto-provisioning concepts](concepts-auto-provisioning.md).</span></span> <span data-ttu-id="7a2a6-109">Also, make sure you've completed the steps in [Set up IoT Hub Device Provisioning Service with the Azure portal](./quick-setup-auto-provision.md) before continuing with this quickstart.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-109">Also, make sure you've completed the steps in [Set up IoT Hub Device Provisioning Service with the Azure portal](./quick-setup-auto-provision.md) before continuing with this quickstart.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]


## <a name="prerequisites"></a><span data-ttu-id="7a2a6-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7a2a6-110">Prerequisites</span></span>

* <span data-ttu-id="7a2a6-111">Visual Studio 2015 or [Visual Studio 2017](https://www.visualstudio.com/vs/) with the ['Desktop development with C++'](https://www.visualstudio.com/vs/support/selecting-workloads-visual-studio-2017/) workload enabled.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-111">Visual Studio 2015 or [Visual Studio 2017](https://www.visualstudio.com/vs/) with the ['Desktop development with C++'](https://www.visualstudio.com/vs/support/selecting-workloads-visual-studio-2017/) workload enabled.</span></span>
* <span data-ttu-id="7a2a6-112">Latest version of [Git](https://git-scm.com/download/) installed.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-112">Latest version of [Git](https://git-scm.com/download/) installed.</span></span>


<a id="setupdevbox"></a>

## <a name="prepare-a-development-environment-for-the-azure-iot-c-sdk"></a><span data-ttu-id="7a2a6-113">Prepare a development environment for the Azure IoT C SDK</span><span class="sxs-lookup"><span data-stu-id="7a2a6-113">Prepare a development environment for the Azure IoT C SDK</span></span>

<span data-ttu-id="7a2a6-114">In this section, you will prepare a development environment used to build the [Azure IoT C SDK](https://github.com/Azure/azure-iot-sdk-c) which include the sample code for the X.509 boot sequence.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-114">In this section, you will prepare a development environment used to build the [Azure IoT C SDK](https://github.com/Azure/azure-iot-sdk-c) which include the sample code for the X.509 boot sequence.</span></span>

1. <span data-ttu-id="7a2a6-115">Download the latest release version of the [CMake build system](https://cmake.org/download/).</span><span class="sxs-lookup"><span data-stu-id="7a2a6-115">Download the latest release version of the [CMake build system](https://cmake.org/download/).</span></span> <span data-ttu-id="7a2a6-116">From that same site, look up the cryptographic hash for the version of the binary distribution you chose.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-116">From that same site, look up the cryptographic hash for the version of the binary distribution you chose.</span></span> <span data-ttu-id="7a2a6-117">Verify the downloaded binary using the corresponding cryptographic hash value.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-117">Verify the downloaded binary using the corresponding cryptographic hash value.</span></span> <span data-ttu-id="7a2a6-118">The following example used Windows PowerShell to verify the cryptographic hash for version 3.11.4 of the x64 MSI distribution:</span><span class="sxs-lookup"><span data-stu-id="7a2a6-118">The following example used Windows PowerShell to verify the cryptographic hash for version 3.11.4 of the x64 MSI distribution:</span></span>

    ```PowerShell
    PS C:\Users\wesmc\Downloads> $hash = get-filehash .\cmake-3.11.4-win64-x64.msi
    PS C:\Users\wesmc\Downloads> $hash.Hash -eq "56e3605b8e49cd446f3487da88fcc38cb9c3e9e99a20f5d4bd63e54b7a35f869"
    True
    ```

    <span data-ttu-id="7a2a6-119">It is important that the Visual Studio prerequisites (Visual Studio and the 'Desktop development with C++' workload) are installed on your machine, **before** starting the `CMake` installation.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-119">It is important that the Visual Studio prerequisites (Visual Studio and the 'Desktop development with C++' workload) are installed on your machine, **before** starting the `CMake` installation.</span></span> <span data-ttu-id="7a2a6-120">Once the prerequisites are in place, and the download is verified, install the CMake build system.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-120">Once the prerequisites are in place, and the download is verified, install the CMake build system.</span></span>

2. <span data-ttu-id="7a2a6-121">Open a command prompt or Git Bash shell.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-121">Open a command prompt or Git Bash shell.</span></span> <span data-ttu-id="7a2a6-122">Execute the following command to clone the [Azure IoT C SDK](https://github.com/Azure/azure-iot-sdk-c) GitHub repository:</span><span class="sxs-lookup"><span data-stu-id="7a2a6-122">Execute the following command to clone the [Azure IoT C SDK](https://github.com/Azure/azure-iot-sdk-c) GitHub repository:</span></span>
    
    ```cmd/sh
    git clone https://github.com/Azure/azure-iot-sdk-c.git --recursive
    ```
    <span data-ttu-id="7a2a6-123">The size of this repository is currently around 220 MB.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-123">The size of this repository is currently around 220 MB.</span></span> <span data-ttu-id="7a2a6-124">You should expect this operation to take several minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-124">You should expect this operation to take several minutes to complete.</span></span>


3. <span data-ttu-id="7a2a6-125">Create a `cmake` subdirectory in the root directory of the git repository, and navigate to that folder.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-125">Create a `cmake` subdirectory in the root directory of the git repository, and navigate to that folder.</span></span> 

    ```cmd/sh
    cd azure-iot-sdk-c
    mkdir cmake
    cd cmake
    ```

4. <span data-ttu-id="7a2a6-126">The code sample uses an X.509 certificate to provide attestation via X.509 authentication.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-126">The code sample uses an X.509 certificate to provide attestation via X.509 authentication.</span></span> <span data-ttu-id="7a2a6-127">Run the following command which builds a version of the SDK specific to your development client platform.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-127">Run the following command which builds a version of the SDK specific to your development client platform.</span></span> <span data-ttu-id="7a2a6-128">A Visual Studio solution for the simulated device will be generated in the `cmake` directory.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-128">A Visual Studio solution for the simulated device will be generated in the `cmake` directory.</span></span> 

    ```cmd
    cmake -Duse_prov_client:BOOL=ON ..
    ```
    
    <span data-ttu-id="7a2a6-129">If `cmake` does not find your C++ compiler, you might get build errors while running the above command.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-129">If `cmake` does not find your C++ compiler, you might get build errors while running the above command.</span></span> <span data-ttu-id="7a2a6-130">If that happens, try running this command in the [Visual Studio command prompt](https://docs.microsoft.com/dotnet/framework/tools/developer-command-prompt-for-vs).</span><span class="sxs-lookup"><span data-stu-id="7a2a6-130">If that happens, try running this command in the [Visual Studio command prompt](https://docs.microsoft.com/dotnet/framework/tools/developer-command-prompt-for-vs).</span></span> 

    <span data-ttu-id="7a2a6-131">Once the build succeeds, the last few output lines will look similar to the following output:</span><span class="sxs-lookup"><span data-stu-id="7a2a6-131">Once the build succeeds, the last few output lines will look similar to the following output:</span></span>

    ```cmd/sh
    $ cmake -Duse_prov_client:BOOL=ON ..
    -- Building for: Visual Studio 15 2017
    -- Selecting Windows SDK version 10.0.16299.0 to target Windows 10.0.17134.
    -- The C compiler identification is MSVC 19.12.25835.0
    -- The CXX compiler identification is MSVC 19.12.25835.0

    ...

    -- Configuring done
    -- Generating done
    -- Build files have been written to: E:/IoT Testing/azure-iot-sdk-c/cmake
    ```



<a id="portalenroll"></a>

## <a name="create-a-self-signed-x509-device-certificate"></a><span data-ttu-id="7a2a6-132">Create a self-signed X.509 device certificate</span><span class="sxs-lookup"><span data-stu-id="7a2a6-132">Create a self-signed X.509 device certificate</span></span>

<span data-ttu-id="7a2a6-133">In this section you, will use a self-signed X.509 certificate, it is important to keep in mind the following:</span><span class="sxs-lookup"><span data-stu-id="7a2a6-133">In this section you, will use a self-signed X.509 certificate, it is important to keep in mind the following:</span></span>

* <span data-ttu-id="7a2a6-134">Self-signed certificates are for testing only, and should not to be used in production.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-134">Self-signed certificates are for testing only, and should not to be used in production.</span></span>
* <span data-ttu-id="7a2a6-135">The default expiration date for a self-signed certificate is 1 year.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-135">The default expiration date for a self-signed certificate is 1 year.</span></span>

<span data-ttu-id="7a2a6-136">You will use sample code from the Azure IoT C SDK to create the certificate to be used with the individual enrollment entry for the simulated device.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-136">You will use sample code from the Azure IoT C SDK to create the certificate to be used with the individual enrollment entry for the simulated device.</span></span>

1. <span data-ttu-id="7a2a6-137">Launch Visual Studio and open the new solution file named `azure_iot_sdks.sln`.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-137">Launch Visual Studio and open the new solution file named `azure_iot_sdks.sln`.</span></span> <span data-ttu-id="7a2a6-138">This solution file is located in the `cmake` folder you previously created in the root of the azure-iot-sdk-c git repository.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-138">This solution file is located in the `cmake` folder you previously created in the root of the azure-iot-sdk-c git repository.</span></span>

2. <span data-ttu-id="7a2a6-139">On the Visual Studio menu, select **Build** > **Build Solution** to build all projects in the solution.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-139">On the Visual Studio menu, select **Build** > **Build Solution** to build all projects in the solution.</span></span>

3. <span data-ttu-id="7a2a6-140">In Visual Studio's *Solution Explorer* window, navigate to the **Provision\_Tools** folder.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-140">In Visual Studio's *Solution Explorer* window, navigate to the **Provision\_Tools** folder.</span></span> <span data-ttu-id="7a2a6-141">Right-click the **dice\_device\_enrollment** project and select **Set as Startup Project**.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-141">Right-click the **dice\_device\_enrollment** project and select **Set as Startup Project**.</span></span> 

4. <span data-ttu-id="7a2a6-142">On the Visual Studio menu, select **Debug** > **Start without debugging** to run the solution.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-142">On the Visual Studio menu, select **Debug** > **Start without debugging** to run the solution.</span></span> <span data-ttu-id="7a2a6-143">In the output window, enter **i** for individual enrollment when prompted.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-143">In the output window, enter **i** for individual enrollment when prompted.</span></span> 

    <span data-ttu-id="7a2a6-144">The output window displays a locally generated self-signed X.509 certificate for your simulated device.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-144">The output window displays a locally generated self-signed X.509 certificate for your simulated device.</span></span> <span data-ttu-id="7a2a6-145">Copy the output to clipboard, starting from **-----BEGIN CERTIFICATE-----** and ending with the first **-----END CERTIFICATE-----**, making sure to include both of these lines as well.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-145">Copy the output to clipboard, starting from **-----BEGIN CERTIFICATE-----** and ending with the first **-----END CERTIFICATE-----**, making sure to include both of these lines as well.</span></span> <span data-ttu-id="7a2a6-146">Note that you need only the first certificate from the output window.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-146">Note that you need only the first certificate from the output window.</span></span>
 
5. <span data-ttu-id="7a2a6-147">Using a text editor, save the certifiate to a new file named **_X509testcert.pem_**.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-147">Using a text editor, save the certifiate to a new file named **_X509testcert.pem_**.</span></span> 


## <a name="create-a-device-enrollment-entry-in-the-portal"></a><span data-ttu-id="7a2a6-148">Create a device enrollment entry in the portal</span><span class="sxs-lookup"><span data-stu-id="7a2a6-148">Create a device enrollment entry in the portal</span></span>

1. <span data-ttu-id="7a2a6-149">Sign in to the Azure portal, click on the **All resources** button on the left-hand menu and open your Device Provisioning service.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-149">Sign in to the Azure portal, click on the **All resources** button on the left-hand menu and open your Device Provisioning service.</span></span>

2. <span data-ttu-id="7a2a6-150">Select the **Manage enrollments** tab, and then click the **Add individual enrollment** button at the top.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-150">Select the **Manage enrollments** tab, and then click the **Add individual enrollment** button at the top.</span></span> 

3. <span data-ttu-id="7a2a6-151">On **Add enrollment**, enter the following information, and click the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-151">On **Add enrollment**, enter the following information, and click the **Save** button.</span></span>

    - <span data-ttu-id="7a2a6-152">**Mechanism:** Select **X.509** as the identity attestation *Mechanism*.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-152">**Mechanism:** Select **X.509** as the identity attestation *Mechanism*.</span></span>
    - <span data-ttu-id="7a2a6-153">**Primary certificate .pem or .cer file:** Click **Select a file** to select the certificate file, X509testcert.pem, you created earlier.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-153">**Primary certificate .pem or .cer file:** Click **Select a file** to select the certificate file, X509testcert.pem, you created earlier.</span></span>
    - <span data-ttu-id="7a2a6-154">**IoT Hub Device ID:** Enter **test-docs-cert-device** to give the device an ID.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-154">**IoT Hub Device ID:** Enter **test-docs-cert-device** to give the device an ID.</span></span>

    <span data-ttu-id="7a2a6-155">[![Add individual enrollment for X.509 attestation in the portal](./media/quick-create-simulated-device-x509/individual-enrollment.png)](./media/quick-create-simulated-device-x509/individual-enrollment.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="7a2a6-155">[![Add individual enrollment for X.509 attestation in the portal](./media/quick-create-simulated-device-x509/individual-enrollment.png)](./media/quick-create-simulated-device-x509/individual-enrollment.png#lightbox)</span></span>

    <span data-ttu-id="7a2a6-156">On successful enrollment, your X.509 device appears as **riot-device-cert** under the *Registration ID* column in the *Individual Enrollments* tab.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-156">On successful enrollment, your X.509 device appears as **riot-device-cert** under the *Registration ID* column in the *Individual Enrollments* tab.</span></span> 



<a id="firstbootsequence"></a>

## <a name="simulate-first-boot-sequence-for-the-device"></a><span data-ttu-id="7a2a6-157">Simulate first boot sequence for the device</span><span class="sxs-lookup"><span data-stu-id="7a2a6-157">Simulate first boot sequence for the device</span></span>

<span data-ttu-id="7a2a6-158">In this section, update the sample code to send the device's boot sequence to your Device Provisioning Service instance.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-158">In this section, update the sample code to send the device's boot sequence to your Device Provisioning Service instance.</span></span> <span data-ttu-id="7a2a6-159">This boot sequence will cause the device to be recognized and assigned to an IoT hub linked to the Device Provisioning Service instance.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-159">This boot sequence will cause the device to be recognized and assigned to an IoT hub linked to the Device Provisioning Service instance.</span></span>



1. <span data-ttu-id="7a2a6-160">In the Azure portal, select the **Overview** tab for your Device Provisioning service and note down the **_ID Scope_** value.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-160">In the Azure portal, select the **Overview** tab for your Device Provisioning service and note down the **_ID Scope_** value.</span></span>

    ![Extract Device Provisioning Service endpoint information from the portal blade](./media/quick-create-simulated-device-x509/extract-dps-endpoints.png) 

2. <span data-ttu-id="7a2a6-162">In Visual Studio's *Solution Explorer* window, navigate to the **Provision\_Samples** folder.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-162">In Visual Studio's *Solution Explorer* window, navigate to the **Provision\_Samples** folder.</span></span> <span data-ttu-id="7a2a6-163">Expand the sample project named **prov\_dev\_client\_sample**.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-163">Expand the sample project named **prov\_dev\_client\_sample**.</span></span> <span data-ttu-id="7a2a6-164">Expand **Source Files**, and open **prov\_dev\_client\_sample.c**.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-164">Expand **Source Files**, and open **prov\_dev\_client\_sample.c**.</span></span>

3. <span data-ttu-id="7a2a6-165">Find the `id_scope` constant, and replace the value with your **ID Scope** value that you copied earlier.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-165">Find the `id_scope` constant, and replace the value with your **ID Scope** value that you copied earlier.</span></span> 

    ```c
    static const char* id_scope = "0ne00002193";
    ```

4. <span data-ttu-id="7a2a6-166">Find the definition for the `main()` function in the same file.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-166">Find the definition for the `main()` function in the same file.</span></span> <span data-ttu-id="7a2a6-167">Make sure the `hsm_type` variable is set to `SECURE_DEVICE_TYPE_X509` instead of `SECURE_DEVICE_TYPE_TPM` as shown below.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-167">Make sure the `hsm_type` variable is set to `SECURE_DEVICE_TYPE_X509` instead of `SECURE_DEVICE_TYPE_TPM` as shown below.</span></span>

    ```c
    SECURE_DEVICE_TYPE hsm_type;
    //hsm_type = SECURE_DEVICE_TYPE_TPM;
    hsm_type = SECURE_DEVICE_TYPE_X509;
    ```

5. <span data-ttu-id="7a2a6-168">Right-click the **prov\_dev\_client\_sample** project and select **Set as Startup Project**.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-168">Right-click the **prov\_dev\_client\_sample** project and select **Set as Startup Project**.</span></span> 

6. <span data-ttu-id="7a2a6-169">On the Visual Studio menu, select **Debug** > **Start without debugging** to run the solution.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-169">On the Visual Studio menu, select **Debug** > **Start without debugging** to run the solution.</span></span> <span data-ttu-id="7a2a6-170">In the prompt to rebuild the project, click **Yes**, to rebuild the project before running.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-170">In the prompt to rebuild the project, click **Yes**, to rebuild the project before running.</span></span>

    <span data-ttu-id="7a2a6-171">The following output is an example of the provisioning device client sample successfully booting up, and connecting to the provisioning Service instance to get IoT hub information and registering:</span><span class="sxs-lookup"><span data-stu-id="7a2a6-171">The following output is an example of the provisioning device client sample successfully booting up, and connecting to the provisioning Service instance to get IoT hub information and registering:</span></span>

    ```cmd
    Provisioning API Version: 1.2.7

    Registering... Press enter key to interrupt.

    Provisioning Status: PROV_DEVICE_REG_STATUS_CONNECTED
    Provisioning Status: PROV_DEVICE_REG_STATUS_ASSIGNING
    Provisioning Status: PROV_DEVICE_REG_STATUS_ASSIGNING

    Registration Information received from service: 
    test-docs-hub.azure-devices.net, deviceId: test-docs-cert-device    
    ```

7. <span data-ttu-id="7a2a6-172">In the portal, navigate to the IoT hub linked to your provisioning service and click the **IoT Devices** tab. On successful provisioning of the simulated X.509 device to the hub, its device ID appears on the **IoT Devices** blade, with *STATUS* as **enabled**.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-172">In the portal, navigate to the IoT hub linked to your provisioning service and click the **IoT Devices** tab. On successful provisioning of the simulated X.509 device to the hub, its device ID appears on the **IoT Devices** blade, with *STATUS* as **enabled**.</span></span> <span data-ttu-id="7a2a6-173">Note that you might need to click the **Refresh** button at the top.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-173">Note that you might need to click the **Refresh** button at the top.</span></span> 

    ![Device is registered with the IoT hub](./media/quick-create-simulated-device/hub-registration.png) 


## <a name="clean-up-resources"></a><span data-ttu-id="7a2a6-175">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="7a2a6-175">Clean up resources</span></span>

<span data-ttu-id="7a2a6-176">If you plan to continue working on and exploring the device client sample, do not clean up the resources created in this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-176">If you plan to continue working on and exploring the device client sample, do not clean up the resources created in this Quickstart.</span></span> <span data-ttu-id="7a2a6-177">If you do not plan to continue, use the following steps to delete all resources created by this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-177">If you do not plan to continue, use the following steps to delete all resources created by this Quickstart.</span></span>

1. <span data-ttu-id="7a2a6-178">Close the device client sample output window on your machine.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-178">Close the device client sample output window on your machine.</span></span>
1. <span data-ttu-id="7a2a6-179">From the left-hand menu in the Azure portal, click **All resources** and then select your Device Provisioning service.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-179">From the left-hand menu in the Azure portal, click **All resources** and then select your Device Provisioning service.</span></span> <span data-ttu-id="7a2a6-180">Open **Manage Enrollments** for your service, and then click the **Individual Enrollments** tab. Select the *REGISTRATION ID* of the device you enrolled in this Quickstart, and click the **Delete** button at the top.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-180">Open **Manage Enrollments** for your service, and then click the **Individual Enrollments** tab. Select the *REGISTRATION ID* of the device you enrolled in this Quickstart, and click the **Delete** button at the top.</span></span> 
1. <span data-ttu-id="7a2a6-181">From the left-hand menu in the Azure portal, click **All resources** and then select your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-181">From the left-hand menu in the Azure portal, click **All resources** and then select your IoT hub.</span></span> <span data-ttu-id="7a2a6-182">Open **IoT Devices** for your hub, select the *DEVICE ID* of the device you registered in this Quickstart, and then click **Delete** button at the top.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-182">Open **IoT Devices** for your hub, select the *DEVICE ID* of the device you registered in this Quickstart, and then click **Delete** button at the top.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a2a6-183">Next steps</span><span class="sxs-lookup"><span data-stu-id="7a2a6-183">Next steps</span></span>

<span data-ttu-id="7a2a6-184">In this Quickstart, you’ve created a simulated X.509 device on your Windows machine and provisioned it to your IoT hub using the Azure IoT Hub Device Provisioning Service on the portal.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-184">In this Quickstart, you’ve created a simulated X.509 device on your Windows machine and provisioned it to your IoT hub using the Azure IoT Hub Device Provisioning Service on the portal.</span></span> <span data-ttu-id="7a2a6-185">To learn how to enroll your X.509 device programmatically, continue to the Quickstart for programmatic enrollment of X.509 devices.</span><span class="sxs-lookup"><span data-stu-id="7a2a6-185">To learn how to enroll your X.509 device programmatically, continue to the Quickstart for programmatic enrollment of X.509 devices.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="7a2a6-186">Azure Quickstart - Enroll X.509 devices to Azure IoT Hub Device Provisioning Service</span><span class="sxs-lookup"><span data-stu-id="7a2a6-186">Azure Quickstart - Enroll X.509 devices to Azure IoT Hub Device Provisioning Service</span></span>](quick-enroll-device-x509-java.md)
