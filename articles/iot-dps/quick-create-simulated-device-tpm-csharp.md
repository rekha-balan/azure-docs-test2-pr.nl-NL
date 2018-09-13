---
title: Provision a simulated TPM device to Azure IoT Hub using C# | Microsoft Docs
description: Azure Quickstart - Create and provision a simulated TPM device using C# device SDK for Azure IoT Hub Device Provisioning Service
author: wesmc7777
ms.author: wesmc
ms.date: 04/09/2018
ms.topic: quickstart
ms.service: iot-dps
services: iot-dps
manager: timlt
ms.custom: mvc
ms.openlocfilehash: 055a1f09cf30665321d570978d800e1fbb3c0cf7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870230"
---
# <a name="create-and-provision-a-simulated-tpm-device-using-c-device-sdk-for-iot-hub-device-provisioning-service"></a><span data-ttu-id="4ecbe-103">Create and provision a simulated TPM device using C# device SDK for IoT Hub Device Provisioning Service</span><span class="sxs-lookup"><span data-stu-id="4ecbe-103">Create and provision a simulated TPM device using C# device SDK for IoT Hub Device Provisioning Service</span></span>

[!INCLUDE [iot-dps-selector-quick-create-simulated-device-tpm](../../includes/iot-dps-selector-quick-create-simulated-device-tpm.md)]

<span data-ttu-id="4ecbe-104">These steps show you how to build the Azure IoT Hub C# SDK simulated TPM device sample on a development machine running Windows OS and connect the simulated device with the Device Provisioning Service and your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-104">These steps show you how to build the Azure IoT Hub C# SDK simulated TPM device sample on a development machine running Windows OS and connect the simulated device with the Device Provisioning Service and your IoT hub.</span></span> <span data-ttu-id="4ecbe-105">The sample code uses the Windows TPM simulator as the [Hardware Security Module (HSM)](https://azure.microsoft.com/blog/azure-iot-supports-new-security-hardware-to-strengthen-iot-security/) of the device.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-105">The sample code uses the Windows TPM simulator as the [Hardware Security Module (HSM)](https://azure.microsoft.com/blog/azure-iot-supports-new-security-hardware-to-strengthen-iot-security/) of the device.</span></span> 

<span data-ttu-id="4ecbe-106">If you're unfamiliar with the process of auto-provisioning, be sure to also review [Auto-provisioning concepts](concepts-auto-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="4ecbe-106">If you're unfamiliar with the process of auto-provisioning, be sure to also review [Auto-provisioning concepts](concepts-auto-provisioning.md).</span></span> <span data-ttu-id="4ecbe-107">Also make sure you've completed the steps in [Set up IoT Hub Device Provisioning Service with the Azure portal](./quick-setup-auto-provision.md) before continuing.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-107">Also make sure you've completed the steps in [Set up IoT Hub Device Provisioning Service with the Azure portal](./quick-setup-auto-provision.md) before continuing.</span></span> 

[!INCLUDE [IoT Device Provisioning Service basic](../../includes/iot-dps-basic.md)]

<a id="setupdevbox"></a>
## <a name="prepare-the-development-environment"></a><span data-ttu-id="4ecbe-108">Prepare the development environment</span><span class="sxs-lookup"><span data-stu-id="4ecbe-108">Prepare the development environment</span></span> 

1. <span data-ttu-id="4ecbe-109">Make sure you have the [.Net Core SDK](https://www.microsoft.com/net/download/windows) installed on your machine.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-109">Make sure you have the [.Net Core SDK](https://www.microsoft.com/net/download/windows) installed on your machine.</span></span> 

1. <span data-ttu-id="4ecbe-110">Make sure `git` is installed on your machine and is added to the environment variables accessible to the command window.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-110">Make sure `git` is installed on your machine and is added to the environment variables accessible to the command window.</span></span> <span data-ttu-id="4ecbe-111">See [Software Freedom Conservancy's Git client tools](https://git-scm.com/download/) for the latest version of `git` tools to install, which includes the **Git Bash**, the command-line app that you can use to interact with your local Git repository.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-111">See [Software Freedom Conservancy's Git client tools](https://git-scm.com/download/) for the latest version of `git` tools to install, which includes the **Git Bash**, the command-line app that you can use to interact with your local Git repository.</span></span> 

4. <span data-ttu-id="4ecbe-112">Open a command prompt or Git Bash.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-112">Open a command prompt or Git Bash.</span></span> <span data-ttu-id="4ecbe-113">Clone the Azure IoT SDK for C# GitHub repo:</span><span class="sxs-lookup"><span data-stu-id="4ecbe-113">Clone the Azure IoT SDK for C# GitHub repo:</span></span>
    
    ```cmd
    git clone --recursive https://github.com/Azure/azure-iot-sdk-csharp.git
    ```

## <a name="provision-the-simulated-device"></a><span data-ttu-id="4ecbe-114">Provision the simulated device</span><span class="sxs-lookup"><span data-stu-id="4ecbe-114">Provision the simulated device</span></span>


1. <span data-ttu-id="4ecbe-115">Log in to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-115">Log in to the Azure portal.</span></span> <span data-ttu-id="4ecbe-116">Click the **All resources** button on the left-hand menu and open your Device Provisioning service.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-116">Click the **All resources** button on the left-hand menu and open your Device Provisioning service.</span></span> <span data-ttu-id="4ecbe-117">From the **Overview** blade.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-117">From the **Overview** blade.</span></span> <span data-ttu-id="4ecbe-118">note down the **_ID Scope_** value.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-118">note down the **_ID Scope_** value.</span></span>

    ![Copy provisioning service Scope ID from the portal blade](./media/quick-create-simulated-device-tpm-csharp/copy-scope.png) 


2. <span data-ttu-id="4ecbe-120">In a command prompt, change directories to the project directory for the TPM device provisioning sample.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-120">In a command prompt, change directories to the project directory for the TPM device provisioning sample.</span></span>

    ```cmd
    cd .\azure-iot-sdk-csharp\provisioning\device\samples\ProvisioningDeviceClientTpm
    ```

2. <span data-ttu-id="4ecbe-121">Type the following command to build and run the TPM device provisioning sample.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-121">Type the following command to build and run the TPM device provisioning sample.</span></span> <span data-ttu-id="4ecbe-122">Replace the `<IDScope>` value with the ID Scope for your provisioning service.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-122">Replace the `<IDScope>` value with the ID Scope for your provisioning service.</span></span> 

    ```cmd
    dotnet run <IDScope>
    ```

1. <span data-ttu-id="4ecbe-123">The command window displays the **_Endorsement Key_**,  the **_Registration ID_**, and a suggested **_Device ID_** needed for device enrollment.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-123">The command window displays the **_Endorsement Key_**,  the **_Registration ID_**, and a suggested **_Device ID_** needed for device enrollment.</span></span> <span data-ttu-id="4ecbe-124">Note down these values.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-124">Note down these values.</span></span> 
   > [!NOTE]
   > <span data-ttu-id="4ecbe-125">Do not confuse the window that contains command output with the window that contains output from the TPM simulator.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-125">Do not confuse the window that contains command output with the window that contains output from the TPM simulator.</span></span> <span data-ttu-id="4ecbe-126">You may have to click the command window to bring it to the foreground.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-126">You may have to click the command window to bring it to the foreground.</span></span>

    ![Command window output](./media/quick-create-simulated-device-tpm-csharp/output1.png) 


4. <span data-ttu-id="4ecbe-128">In the Azure portal, on the Device Provisioning Service summary blade, select **Manage enrollments**.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-128">In the Azure portal, on the Device Provisioning Service summary blade, select **Manage enrollments**.</span></span> <span data-ttu-id="4ecbe-129">Select the **Individual Enrollments** tab and click the **Add** button at the top.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-129">Select the **Individual Enrollments** tab and click the **Add** button at the top.</span></span> 

5. <span data-ttu-id="4ecbe-130">Under **Add enrollment list entry**, enter the following information:</span><span class="sxs-lookup"><span data-stu-id="4ecbe-130">Under **Add enrollment list entry**, enter the following information:</span></span>
    - <span data-ttu-id="4ecbe-131">Select **TPM** as the identity attestation *Mechanism*.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-131">Select **TPM** as the identity attestation *Mechanism*.</span></span>
    - <span data-ttu-id="4ecbe-132">Enter the *Registration ID* and *Endorsement key* for your TPM device.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-132">Enter the *Registration ID* and *Endorsement key* for your TPM device.</span></span> 
    - <span data-ttu-id="4ecbe-133">Optionally select an IoT hub linked with your provisioning service.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-133">Optionally select an IoT hub linked with your provisioning service.</span></span>
    - <span data-ttu-id="4ecbe-134">Enter a unique device ID.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-134">Enter a unique device ID.</span></span> <span data-ttu-id="4ecbe-135">You can enter the device ID suggested in the sample output or enter your own.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-135">You can enter the device ID suggested in the sample output or enter your own.</span></span> <span data-ttu-id="4ecbe-136">If you use your own, make sure to avoid sensitive data when naming your device.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-136">If you use your own, make sure to avoid sensitive data when naming your device.</span></span> 
    - <span data-ttu-id="4ecbe-137">Update the **Initial device twin state** with the desired initial configuration for the device.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-137">Update the **Initial device twin state** with the desired initial configuration for the device.</span></span>
    - <span data-ttu-id="4ecbe-138">Once complete, click the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-138">Once complete, click the **Save** button.</span></span> 

    ![Enter device enrollment information in the portal blade](./media/quick-create-simulated-device-tpm-csharp/enter-device-enrollment.png)  

   <span data-ttu-id="4ecbe-140">On successful enrollment, the *Registration ID* of your device will appear in the list under the *Individual Enrollments* tab.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-140">On successful enrollment, the *Registration ID* of your device will appear in the list under the *Individual Enrollments* tab.</span></span> 

6. <span data-ttu-id="4ecbe-141">Press Enter in the command window (that displayed the **_Endorsement Key_**,  the **_Registration ID_**, and a suggested **_Device ID_**)  to enroll the simulated device.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-141">Press Enter in the command window (that displayed the **_Endorsement Key_**,  the **_Registration ID_**, and a suggested **_Device ID_**)  to enroll the simulated device.</span></span> <span data-ttu-id="4ecbe-142">Notice the messages that simulate the device booting and connecting to the Device Provisioning Service to get your IoT hub information.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-142">Notice the messages that simulate the device booting and connecting to the Device Provisioning Service to get your IoT hub information.</span></span> 

1. <span data-ttu-id="4ecbe-143">Verify that the device has been provisioned.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-143">Verify that the device has been provisioned.</span></span> <span data-ttu-id="4ecbe-144">On successful provisioning of the simulated device to the IoT hub linked with your provisioning service, the device ID appears on the hub's **IoT Devices** blade.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-144">On successful provisioning of the simulated device to the IoT hub linked with your provisioning service, the device ID appears on the hub's **IoT Devices** blade.</span></span> 

    ![Device is registered with the IoT hub](./media/quick-create-simulated-device-tpm-csharp/hub-registration.png) 

    <span data-ttu-id="4ecbe-146">If you changed the *initial device twin state* from the default value in the enrollment entry for your device, it can pull the desired twin state from the hub and act accordingly.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-146">If you changed the *initial device twin state* from the default value in the enrollment entry for your device, it can pull the desired twin state from the hub and act accordingly.</span></span> <span data-ttu-id="4ecbe-147">For more information, see [Understand and use device twins in IoT Hub](../iot-hub/iot-hub-devguide-device-twins.md)</span><span class="sxs-lookup"><span data-stu-id="4ecbe-147">For more information, see [Understand and use device twins in IoT Hub](../iot-hub/iot-hub-devguide-device-twins.md)</span></span>


## <a name="clean-up-resources"></a><span data-ttu-id="4ecbe-148">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="4ecbe-148">Clean up resources</span></span>

<span data-ttu-id="4ecbe-149">If you plan to continue working on and exploring the device client sample, do not clean up the resources created in this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-149">If you plan to continue working on and exploring the device client sample, do not clean up the resources created in this Quickstart.</span></span> <span data-ttu-id="4ecbe-150">If you do not plan to continue, use the following steps to delete all resources created by this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-150">If you do not plan to continue, use the following steps to delete all resources created by this Quickstart.</span></span>

1. <span data-ttu-id="4ecbe-151">Close the device client sample output window on your machine.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-151">Close the device client sample output window on your machine.</span></span>
1. <span data-ttu-id="4ecbe-152">Close the TPM simulator window on your machine.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-152">Close the TPM simulator window on your machine.</span></span>
1. <span data-ttu-id="4ecbe-153">From the left-hand menu in the Azure portal, click **All resources** and then select your Device Provisioning service.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-153">From the left-hand menu in the Azure portal, click **All resources** and then select your Device Provisioning service.</span></span> <span data-ttu-id="4ecbe-154">At the top of the **All resources** blade, click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-154">At the top of the **All resources** blade, click **Delete**.</span></span>  
1. <span data-ttu-id="4ecbe-155">From the left-hand menu in the Azure portal, click **All resources** and then select your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-155">From the left-hand menu in the Azure portal, click **All resources** and then select your IoT hub.</span></span> <span data-ttu-id="4ecbe-156">At the top of the **All resources** blade, click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-156">At the top of the **All resources** blade, click **Delete**.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="4ecbe-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="4ecbe-157">Next steps</span></span>

<span data-ttu-id="4ecbe-158">In this Quickstart, you’ve created a TPM simulated device on your machine and provisioned it to your IoT hub using the IoT Hub Device Provisioning Service.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-158">In this Quickstart, you’ve created a TPM simulated device on your machine and provisioned it to your IoT hub using the IoT Hub Device Provisioning Service.</span></span> <span data-ttu-id="4ecbe-159">To learn how to enroll your TPM device programmatically, continue to the Quickstart for programmatic enrollment of a TPM device.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-159">To learn how to enroll your TPM device programmatically, continue to the Quickstart for programmatic enrollment of a TPM device.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="4ecbe-160">Azure Quickstart - Enroll TPM device to Azure IoT Hub Device Provisioning Service</span><span class="sxs-lookup"><span data-stu-id="4ecbe-160">Azure Quickstart - Enroll TPM device to Azure IoT Hub Device Provisioning Service</span></span>](quick-enroll-device-tpm-csharp.md)
