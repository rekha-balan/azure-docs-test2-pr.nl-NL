---
title: Provision a simulated TPM device to Azure IoT Hub using Python | Microsoft Docs
description: Azure Quickstart - Create and provision a simulated TPM device using Java device SDK for IoT Hub Device Provisioning Service
author: wesmc7777
ms.author: wesmc
ms.date: 05/21/2018
ms.topic: quickstart
ms.service: iot-dps
services: iot-dps
manager: timlt
ms.devlang: python
ms.custom: mvc
ms.openlocfilehash: 46c25e19fbf8882779e7334da69f74ef0fa79272
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965532"
---
# <a name="create-and-provision-a-simulated-tpm-device-using-python-device-sdk-for-iot-hub-device-provisioning-service"></a><span data-ttu-id="20db2-103">Create and provision a simulated TPM device using Python device SDK for IoT Hub Device Provisioning Service</span><span class="sxs-lookup"><span data-stu-id="20db2-103">Create and provision a simulated TPM device using Python device SDK for IoT Hub Device Provisioning Service</span></span>

[!INCLUDE [iot-dps-selector-quick-create-simulated-device-tpm](../../includes/iot-dps-selector-quick-create-simulated-device-tpm.md)]

<span data-ttu-id="20db2-104">These steps show how to create a simulated device on your development machine running Windows OS, run the Windows TPM simulator as the [Hardware Security Module (HSM)](https://azure.microsoft.com/blog/azure-iot-supports-new-security-hardware-to-strengthen-iot-security/) of the device, and use the Python code sample to connect this simulated device with the Device Provisioning Service and your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="20db2-104">These steps show how to create a simulated device on your development machine running Windows OS, run the Windows TPM simulator as the [Hardware Security Module (HSM)](https://azure.microsoft.com/blog/azure-iot-supports-new-security-hardware-to-strengthen-iot-security/) of the device, and use the Python code sample to connect this simulated device with the Device Provisioning Service and your IoT hub.</span></span> 

<span data-ttu-id="20db2-105">If you're unfamiliar with the process of auto-provisioning, be sure to also review [Auto-provisioning concepts](concepts-auto-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="20db2-105">If you're unfamiliar with the process of auto-provisioning, be sure to also review [Auto-provisioning concepts](concepts-auto-provisioning.md).</span></span> <span data-ttu-id="20db2-106">Also make sure you've completed the steps in [Set up IoT Hub Device Provisioning Service with the Azure portal](./quick-setup-auto-provision.md) before continuing.</span><span class="sxs-lookup"><span data-stu-id="20db2-106">Also make sure you've completed the steps in [Set up IoT Hub Device Provisioning Service with the Azure portal](./quick-setup-auto-provision.md) before continuing.</span></span> 

[!INCLUDE [IoT Device Provisioning Service basic](../../includes/iot-dps-basic.md)]

## <a name="prepare-the-environment"></a><span data-ttu-id="20db2-107">Prepare the environment</span><span class="sxs-lookup"><span data-stu-id="20db2-107">Prepare the environment</span></span> 

1. <span data-ttu-id="20db2-108">Make sure you have either [Visual Studio 2015](https://www.visualstudio.com/vs/older-downloads/) or [Visual Studio 2017](https://www.visualstudio.com/vs/) installed on your machine.</span><span class="sxs-lookup"><span data-stu-id="20db2-108">Make sure you have either [Visual Studio 2015](https://www.visualstudio.com/vs/older-downloads/) or [Visual Studio 2017](https://www.visualstudio.com/vs/) installed on your machine.</span></span> <span data-ttu-id="20db2-109">You must have 'Desktop development with C++' workload enabled for your Visual Studio installation.</span><span class="sxs-lookup"><span data-stu-id="20db2-109">You must have 'Desktop development with C++' workload enabled for your Visual Studio installation.</span></span>

1. <span data-ttu-id="20db2-110">Download and install the [CMake build system](https://cmake.org/download/).</span><span class="sxs-lookup"><span data-stu-id="20db2-110">Download and install the [CMake build system](https://cmake.org/download/).</span></span>

1. <span data-ttu-id="20db2-111">Make sure `git` is installed on your machine and is added to the environment variables accessible to the command window.</span><span class="sxs-lookup"><span data-stu-id="20db2-111">Make sure `git` is installed on your machine and is added to the environment variables accessible to the command window.</span></span> <span data-ttu-id="20db2-112">See [Software Freedom Conservancy's Git client tools](https://git-scm.com/download/) for the latest version of `git` tools to install, which includes the **Git Bash**, the command-line app that you can use to interact with your local Git repository.</span><span class="sxs-lookup"><span data-stu-id="20db2-112">See [Software Freedom Conservancy's Git client tools](https://git-scm.com/download/) for the latest version of `git` tools to install, which includes the **Git Bash**, the command-line app that you can use to interact with your local Git repository.</span></span> 

1. <span data-ttu-id="20db2-113">Open a command prompt or Git Bash.</span><span class="sxs-lookup"><span data-stu-id="20db2-113">Open a command prompt or Git Bash.</span></span> <span data-ttu-id="20db2-114">Clone the GitHub repo for device simulation code sample:</span><span class="sxs-lookup"><span data-stu-id="20db2-114">Clone the GitHub repo for device simulation code sample:</span></span>
    
    ```cmd/sh
    git clone https://github.com/Azure/azure-iot-sdk-python.git --recursive
    ```

1. <span data-ttu-id="20db2-115">Create a folder in your local copy of this GitHub repo for CMake build process.</span><span class="sxs-lookup"><span data-stu-id="20db2-115">Create a folder in your local copy of this GitHub repo for CMake build process.</span></span> 

    ```cmd/sh
    cd azure-iot-sdk-python/c
    mkdir cmake
    cd cmake
    ```

1. <span data-ttu-id="20db2-116">The code sample uses a Windows TPM simulator.</span><span class="sxs-lookup"><span data-stu-id="20db2-116">The code sample uses a Windows TPM simulator.</span></span> <span data-ttu-id="20db2-117">Run the following command to enable the SAS token authentication.</span><span class="sxs-lookup"><span data-stu-id="20db2-117">Run the following command to enable the SAS token authentication.</span></span> <span data-ttu-id="20db2-118">It also generates a Visual Studio solution for the simulated device.</span><span class="sxs-lookup"><span data-stu-id="20db2-118">It also generates a Visual Studio solution for the simulated device.</span></span>

    ```cmd/sh
    cmake -Duse_prov_client:BOOL=ON -Duse_tpm_simulator:BOOL=ON ..
    ```

1. <span data-ttu-id="20db2-119">In a separate command prompt, navigate to the TPM simulator folder and run the [TPM](https://docs.microsoft.com/windows/device-security/tpm/trusted-platform-module-overview) simulator.</span><span class="sxs-lookup"><span data-stu-id="20db2-119">In a separate command prompt, navigate to the TPM simulator folder and run the [TPM](https://docs.microsoft.com/windows/device-security/tpm/trusted-platform-module-overview) simulator.</span></span> <span data-ttu-id="20db2-120">Click **Allow Access**.</span><span class="sxs-lookup"><span data-stu-id="20db2-120">Click **Allow Access**.</span></span> <span data-ttu-id="20db2-121">It listens over a socket on ports 2321 and 2322.</span><span class="sxs-lookup"><span data-stu-id="20db2-121">It listens over a socket on ports 2321 and 2322.</span></span> <span data-ttu-id="20db2-122">Do not close this command window; you will need to keep this simulator running until the end of this Quickstart guide.</span><span class="sxs-lookup"><span data-stu-id="20db2-122">Do not close this command window; you will need to keep this simulator running until the end of this Quickstart guide.</span></span> 

    ```cmd/sh
    .\azure-iot-sdk-python\c\provisioning_client\deps\utpm\tools\tpm_simulator\Simulator.exe
    ```

    ![TPM Simulator](./media/python-quick-create-simulated-device/tpm-simulator.png)


## <a name="create-a-device-enrollment-entry"></a><span data-ttu-id="20db2-124">Create a device enrollment entry</span><span class="sxs-lookup"><span data-stu-id="20db2-124">Create a device enrollment entry</span></span>

1. <span data-ttu-id="20db2-125">Open the solution generated in the *cmake* folder named `azure_iot_sdks.sln`, and build it in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="20db2-125">Open the solution generated in the *cmake* folder named `azure_iot_sdks.sln`, and build it in Visual Studio.</span></span>

1. <span data-ttu-id="20db2-126">Right-click the **tpm_device_provision** project and select **Set as Startup Project**.</span><span class="sxs-lookup"><span data-stu-id="20db2-126">Right-click the **tpm_device_provision** project and select **Set as Startup Project**.</span></span> <span data-ttu-id="20db2-127">Run the solution.</span><span class="sxs-lookup"><span data-stu-id="20db2-127">Run the solution.</span></span> <span data-ttu-id="20db2-128">The output window displays the **_Endorsement Key_** and the **_Registration ID_** needed for device enrollment.</span><span class="sxs-lookup"><span data-stu-id="20db2-128">The output window displays the **_Endorsement Key_** and the **_Registration ID_** needed for device enrollment.</span></span> <span data-ttu-id="20db2-129">Note down these values.</span><span class="sxs-lookup"><span data-stu-id="20db2-129">Note down these values.</span></span> 

    ![TPM setup](./media/python-quick-create-simulated-device/tpm-setup.png)

1. <span data-ttu-id="20db2-131">Log in to the Azure portal, click on the **All resources** button on the left-hand menu and open your Device Provisioning service.</span><span class="sxs-lookup"><span data-stu-id="20db2-131">Log in to the Azure portal, click on the **All resources** button on the left-hand menu and open your Device Provisioning service.</span></span>

1. <span data-ttu-id="20db2-132">On the Device Provisioning Service summary blade, select **Manage enrollments**.</span><span class="sxs-lookup"><span data-stu-id="20db2-132">On the Device Provisioning Service summary blade, select **Manage enrollments**.</span></span> <span data-ttu-id="20db2-133">Select **Individual Enrollments** tab and click the **Add** button at the top.</span><span class="sxs-lookup"><span data-stu-id="20db2-133">Select **Individual Enrollments** tab and click the **Add** button at the top.</span></span> 

1. <span data-ttu-id="20db2-134">Under the **Add enrollment list entry**, enter the following information:</span><span class="sxs-lookup"><span data-stu-id="20db2-134">Under the **Add enrollment list entry**, enter the following information:</span></span>
    - <span data-ttu-id="20db2-135">Select **TPM** as the identity attestation *Mechanism*.</span><span class="sxs-lookup"><span data-stu-id="20db2-135">Select **TPM** as the identity attestation *Mechanism*.</span></span>
    - <span data-ttu-id="20db2-136">Enter the *Registration ID* and *Endorsement key* for your TPM device.</span><span class="sxs-lookup"><span data-stu-id="20db2-136">Enter the *Registration ID* and *Endorsement key* for your TPM device.</span></span> 
    - <span data-ttu-id="20db2-137">Select an IoT hub linked with your provisioning service.</span><span class="sxs-lookup"><span data-stu-id="20db2-137">Select an IoT hub linked with your provisioning service.</span></span>
    - <span data-ttu-id="20db2-138">Enter a unique device ID.</span><span class="sxs-lookup"><span data-stu-id="20db2-138">Enter a unique device ID.</span></span> <span data-ttu-id="20db2-139">Make sure to avoid sensitive data while naming your device.</span><span class="sxs-lookup"><span data-stu-id="20db2-139">Make sure to avoid sensitive data while naming your device.</span></span>
    - <span data-ttu-id="20db2-140">Update the **Initial device twin state** with the desired initial configuration for the device.</span><span class="sxs-lookup"><span data-stu-id="20db2-140">Update the **Initial device twin state** with the desired initial configuration for the device.</span></span>
    - <span data-ttu-id="20db2-141">Once complete, click the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="20db2-141">Once complete, click the **Save** button.</span></span> 

    ![Enter device enrollment information in the portal blade](./media/python-quick-create-simulated-device/enter-device-enrollment.png)  

   <span data-ttu-id="20db2-143">On successful enrollment, the *Registration ID* of your device will appear in the list under the *Individual Enrollments* tab.</span><span class="sxs-lookup"><span data-stu-id="20db2-143">On successful enrollment, the *Registration ID* of your device will appear in the list under the *Individual Enrollments* tab.</span></span> 


## <a name="simulate-the-device"></a><span data-ttu-id="20db2-144">Simulate the device</span><span class="sxs-lookup"><span data-stu-id="20db2-144">Simulate the device</span></span>

1. <span data-ttu-id="20db2-145">Download and install [Python 2.x or 3.x](https://www.python.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="20db2-145">Download and install [Python 2.x or 3.x](https://www.python.org/downloads/).</span></span> <span data-ttu-id="20db2-146">Make sure to use the 32-bit or 64-bit installation as required by your setup.</span><span class="sxs-lookup"><span data-stu-id="20db2-146">Make sure to use the 32-bit or 64-bit installation as required by your setup.</span></span> <span data-ttu-id="20db2-147">When prompted during the installation, make sure to add Python to your platform-specific environment variables.</span><span class="sxs-lookup"><span data-stu-id="20db2-147">When prompted during the installation, make sure to add Python to your platform-specific environment variables.</span></span>
    - <span data-ttu-id="20db2-148">If you are using Windows OS, then [Visual C++ redistributable package](http://www.microsoft.com/download/confirmation.aspx?id=48145) to allow the use of native DLLs from Python.</span><span class="sxs-lookup"><span data-stu-id="20db2-148">If you are using Windows OS, then [Visual C++ redistributable package](http://www.microsoft.com/download/confirmation.aspx?id=48145) to allow the use of native DLLs from Python.</span></span>

1. <span data-ttu-id="20db2-149">Follow [these instructions](https://github.com/Azure/azure-iot-sdk-python/blob/master/doc/python-devbox-setup.md) to build the Python packages.</span><span class="sxs-lookup"><span data-stu-id="20db2-149">Follow [these instructions](https://github.com/Azure/azure-iot-sdk-python/blob/master/doc/python-devbox-setup.md) to build the Python packages.</span></span>

    > [!NOTE]
        > <span data-ttu-id="20db2-150">If running the `build_client.cmd` make sure to use the `--use-tpm-simulator` flag.</span><span class="sxs-lookup"><span data-stu-id="20db2-150">If running the `build_client.cmd` make sure to use the `--use-tpm-simulator` flag.</span></span>

    > [!NOTE]
        > <span data-ttu-id="20db2-151">If using `pip` make sure to also install the `azure-iot-provisioning-device-client` package.</span><span class="sxs-lookup"><span data-stu-id="20db2-151">If using `pip` make sure to also install the `azure-iot-provisioning-device-client` package.</span></span> <span data-ttu-id="20db2-152">Note that the released PIP packages are using the real TPM, not the simulator.</span><span class="sxs-lookup"><span data-stu-id="20db2-152">Note that the released PIP packages are using the real TPM, not the simulator.</span></span> <span data-ttu-id="20db2-153">To use the simulator you need to compile from the source using the `--use-tpm-simulator` flag.</span><span class="sxs-lookup"><span data-stu-id="20db2-153">To use the simulator you need to compile from the source using the `--use-tpm-simulator` flag.</span></span>

1. <span data-ttu-id="20db2-154">Navigate to the samples folder.</span><span class="sxs-lookup"><span data-stu-id="20db2-154">Navigate to the samples folder.</span></span>

    ```cmd/sh
    cd azure-iot-sdk-python/provisioning_device_client/samples
    ```

1. <span data-ttu-id="20db2-155">Using your Python IDE, edit the python script named **provisioning\_device\_client\_sample.py**.</span><span class="sxs-lookup"><span data-stu-id="20db2-155">Using your Python IDE, edit the python script named **provisioning\_device\_client\_sample.py**.</span></span> <span data-ttu-id="20db2-156">Modify the *GLOBAL\_PROV\_URI* and  *ID\_SCOPE* variables to the values noted previously.</span><span class="sxs-lookup"><span data-stu-id="20db2-156">Modify the *GLOBAL\_PROV\_URI* and  *ID\_SCOPE* variables to the values noted previously.</span></span> <span data-ttu-id="20db2-157">Also make sure *SECURITY\_DEVICE\_TYPE* is set to `ProvisioningSecurityDeviceType.TPM`</span><span class="sxs-lookup"><span data-stu-id="20db2-157">Also make sure *SECURITY\_DEVICE\_TYPE* is set to `ProvisioningSecurityDeviceType.TPM`</span></span>

    ```python
    GLOBAL_PROV_URI = "{globalServiceEndpoint}"
    ID_SCOPE = "{idScope}"
    SECURITY_DEVICE_TYPE = ProvisioningSecurityDeviceType.TPM
    PROTOCOL = ProvisioningTransportProvider.HTTP
    ```

    ![Service information](./media/python-quick-create-simulated-device/extract-dps-endpoints.png)

1. <span data-ttu-id="20db2-159">Run the sample.</span><span class="sxs-lookup"><span data-stu-id="20db2-159">Run the sample.</span></span> 

    ```cmd/sh
    python provisioning_device_client_sample.py
    ```

1. <span data-ttu-id="20db2-160">Notice the messages that simulate the device booting and connecting to the Device Provisioning Service to get your IoT hub information.</span><span class="sxs-lookup"><span data-stu-id="20db2-160">Notice the messages that simulate the device booting and connecting to the Device Provisioning Service to get your IoT hub information.</span></span> 

    ![Successful registration](./media/python-quick-create-simulated-device/registration-success.png)

1. <span data-ttu-id="20db2-162">On successful provisioning of your simulated device to the IoT hub linked with your provisioning service, the device ID appears on the hub's **Device Explorer** blade.</span><span class="sxs-lookup"><span data-stu-id="20db2-162">On successful provisioning of your simulated device to the IoT hub linked with your provisioning service, the device ID appears on the hub's **Device Explorer** blade.</span></span>

    ![Device is registered with the IoT hub](./media/python-quick-create-simulated-device/hub-registration.png) 

    <span data-ttu-id="20db2-164">If you changed the *initial device twin state* from the default value in the enrollment entry for your device, it can pull the desired twin state from the hub and act accordingly.</span><span class="sxs-lookup"><span data-stu-id="20db2-164">If you changed the *initial device twin state* from the default value in the enrollment entry for your device, it can pull the desired twin state from the hub and act accordingly.</span></span> <span data-ttu-id="20db2-165">For more information, see [Understand and use device twins in IoT Hub](../iot-hub/iot-hub-devguide-device-twins.md)</span><span class="sxs-lookup"><span data-stu-id="20db2-165">For more information, see [Understand and use device twins in IoT Hub](../iot-hub/iot-hub-devguide-device-twins.md)</span></span>


## <a name="clean-up-resources"></a><span data-ttu-id="20db2-166">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="20db2-166">Clean up resources</span></span>

<span data-ttu-id="20db2-167">If you plan to continue working on and exploring the device client sample, do not clean up the resources created in this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="20db2-167">If you plan to continue working on and exploring the device client sample, do not clean up the resources created in this Quickstart.</span></span> <span data-ttu-id="20db2-168">If you do not plan to continue, use the following steps to delete all resources created by this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="20db2-168">If you do not plan to continue, use the following steps to delete all resources created by this Quickstart.</span></span>

1. <span data-ttu-id="20db2-169">Close the device client sample output window on your machine.</span><span class="sxs-lookup"><span data-stu-id="20db2-169">Close the device client sample output window on your machine.</span></span>
1. <span data-ttu-id="20db2-170">Close the TPM simulator window on your machine.</span><span class="sxs-lookup"><span data-stu-id="20db2-170">Close the TPM simulator window on your machine.</span></span>
1. <span data-ttu-id="20db2-171">From the left-hand menu in the Azure portal, click **All resources** and then select your Device Provisioning service.</span><span class="sxs-lookup"><span data-stu-id="20db2-171">From the left-hand menu in the Azure portal, click **All resources** and then select your Device Provisioning service.</span></span> <span data-ttu-id="20db2-172">Open the **Manage Enrollments** blade for your service, and then click the **Individual Enrollments** tab. Select the *REGISTRATION ID* of the device you enrolled in this Quickstart, and click the **Delete** button at the top.</span><span class="sxs-lookup"><span data-stu-id="20db2-172">Open the **Manage Enrollments** blade for your service, and then click the **Individual Enrollments** tab. Select the *REGISTRATION ID* of the device you enrolled in this Quickstart, and click the **Delete** button at the top.</span></span> 
1. <span data-ttu-id="20db2-173">From the left-hand menu in the Azure portal, click **All resources** and then select your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="20db2-173">From the left-hand menu in the Azure portal, click **All resources** and then select your IoT hub.</span></span> <span data-ttu-id="20db2-174">Open the **IoT Devices** blade for your hub, select the *DEVICE ID* of the device you registered in this Quickstart, and then click **Delete** button at the top.</span><span class="sxs-lookup"><span data-stu-id="20db2-174">Open the **IoT Devices** blade for your hub, select the *DEVICE ID* of the device you registered in this Quickstart, and then click **Delete** button at the top.</span></span>

## <a name="next-steps"></a><span data-ttu-id="20db2-175">Next steps</span><span class="sxs-lookup"><span data-stu-id="20db2-175">Next steps</span></span>

<span data-ttu-id="20db2-176">In this Quickstart, you’ve created a TPM simulated device on your machine and provisioned it to your IoT hub using the IoT Hub Device Provisioning Service.</span><span class="sxs-lookup"><span data-stu-id="20db2-176">In this Quickstart, you’ve created a TPM simulated device on your machine and provisioned it to your IoT hub using the IoT Hub Device Provisioning Service.</span></span> <span data-ttu-id="20db2-177">To learn how to enroll your TPM device programmatically, continue to the Quickstart for programmatic enrollment of a TPM device.</span><span class="sxs-lookup"><span data-stu-id="20db2-177">To learn how to enroll your TPM device programmatically, continue to the Quickstart for programmatic enrollment of a TPM device.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="20db2-178">Azure Quickstart - Enroll TPM device to Azure IoT Hub Device Provisioning Service</span><span class="sxs-lookup"><span data-stu-id="20db2-178">Azure Quickstart - Enroll TPM device to Azure IoT Hub Device Provisioning Service</span></span>](quick-enroll-device-tpm-python.md)
