---
title: Provision a simulated X.509 device to Azure IoT Hub using C# | Microsoft Docs
description: Azure Quickstart - Create and provision a simulated X.509 device using C# device SDK for Azure IoT Hub Device Provisioning Service
author: wesmc7777
ms.author: wesmc
ms.date: 04/09/18
ms.topic: quickstart
ms.service: iot-dps
services: iot-dps
manager: timlt
ms.devlang: csharp
ms.custom: mvc
ms.openlocfilehash: cc8db9a11aa4c942f0dcee3dce320a5bb77cf14a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865274"
---
# <a name="create-and-provision-a-simulated-x509-device-using-c-device-sdk-for-iot-hub-device-provisioning-service"></a><span data-ttu-id="37461-103">Create and provision a simulated X.509 device using C# device SDK for IoT Hub Device Provisioning Service</span><span class="sxs-lookup"><span data-stu-id="37461-103">Create and provision a simulated X.509 device using C# device SDK for IoT Hub Device Provisioning Service</span></span>
[!INCLUDE [iot-dps-selector-quick-create-simulated-device-x509](../../includes/iot-dps-selector-quick-create-simulated-device-x509.md)]

<span data-ttu-id="37461-104">These steps show you how to build the [Azure IoT Hub C# SDK](https://github.com/Azure/azure-iot-sdk-csharp) simulated X.509 device sample on a development machine running Windows OS and connect the simulated device with the Device Provisioning Service and your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="37461-104">These steps show you how to build the [Azure IoT Hub C# SDK](https://github.com/Azure/azure-iot-sdk-csharp) simulated X.509 device sample on a development machine running Windows OS and connect the simulated device with the Device Provisioning Service and your IoT hub.</span></span>

<span data-ttu-id="37461-105">If you're unfamiliar with the process of auto-provisioning, be sure to also review [Auto-provisioning concepts](concepts-auto-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="37461-105">If you're unfamiliar with the process of auto-provisioning, be sure to also review [Auto-provisioning concepts](concepts-auto-provisioning.md).</span></span> <span data-ttu-id="37461-106">Also make sure you've completed the steps in [Set up IoT Hub Device Provisioning Service with the Azure portal](./quick-setup-auto-provision.md) before continuing.</span><span class="sxs-lookup"><span data-stu-id="37461-106">Also make sure you've completed the steps in [Set up IoT Hub Device Provisioning Service with the Azure portal](./quick-setup-auto-provision.md) before continuing.</span></span> 

[!INCLUDE [IoT Device Provisioning Service basic](../../includes/iot-dps-basic.md)]

<a id="setupdevbox"></a>
## <a name="prepare-the-development-environment"></a><span data-ttu-id="37461-107">Prepare the development environment</span><span class="sxs-lookup"><span data-stu-id="37461-107">Prepare the development environment</span></span> 

1. <span data-ttu-id="37461-108">Make sure you have the [.NET core SDK](https://www.microsoft.com/net/download/windows) installed on your machine.</span><span class="sxs-lookup"><span data-stu-id="37461-108">Make sure you have the [.NET core SDK](https://www.microsoft.com/net/download/windows) installed on your machine.</span></span> 

1. <span data-ttu-id="37461-109">Make sure `git` is installed on your machine and is added to the environment variables accessible to the command window.</span><span class="sxs-lookup"><span data-stu-id="37461-109">Make sure `git` is installed on your machine and is added to the environment variables accessible to the command window.</span></span> <span data-ttu-id="37461-110">See [Software Freedom Conservancy's Git client tools](https://git-scm.com/download/) for the latest version of `git` tools to install, which includes the **Git Bash**, the command-line app that you can use to interact with your local Git repository.</span><span class="sxs-lookup"><span data-stu-id="37461-110">See [Software Freedom Conservancy's Git client tools](https://git-scm.com/download/) for the latest version of `git` tools to install, which includes the **Git Bash**, the command-line app that you can use to interact with your local Git repository.</span></span> 

4. <span data-ttu-id="37461-111">Open a command prompt or Git Bash.</span><span class="sxs-lookup"><span data-stu-id="37461-111">Open a command prompt or Git Bash.</span></span> <span data-ttu-id="37461-112">Clone the [Azure IoT SDK for C#](https://github.com/Azure/azure-iot-sdk-csharp) GitHub repo:</span><span class="sxs-lookup"><span data-stu-id="37461-112">Clone the [Azure IoT SDK for C#](https://github.com/Azure/azure-iot-sdk-csharp) GitHub repo:</span></span>
    
    ```cmd
    git clone --recursive https://github.com/Azure/azure-iot-sdk-csharp.git
    ```

## <a name="create-a-self-signed-x509-device-certificate-and-individual-enrollment-entry"></a><span data-ttu-id="37461-113">Create a self-signed X.509 device certificate and individual enrollment entry</span><span class="sxs-lookup"><span data-stu-id="37461-113">Create a self-signed X.509 device certificate and individual enrollment entry</span></span>

<span data-ttu-id="37461-114">In this section you, will use a self-signed X.509 certificate, it is important to keep in mind the following:</span><span class="sxs-lookup"><span data-stu-id="37461-114">In this section you, will use a self-signed X.509 certificate, it is important to keep in mind the following:</span></span>

* <span data-ttu-id="37461-115">Self-signed certificates are for testing only, and should not to be used in production.</span><span class="sxs-lookup"><span data-stu-id="37461-115">Self-signed certificates are for testing only, and should not to be used in production.</span></span>
* <span data-ttu-id="37461-116">The default expiration date for a self-signed certificate is 1 year.</span><span class="sxs-lookup"><span data-stu-id="37461-116">The default expiration date for a self-signed certificate is 1 year.</span></span>

<span data-ttu-id="37461-117">You will use sample code from the [Azure IoT SDK for .NET](https://github.com/Azure/azure-iot-sdk-csharp.git) to create the certificate to be used with the individual enrollment entry for the simulated device.</span><span class="sxs-lookup"><span data-stu-id="37461-117">You will use sample code from the [Azure IoT SDK for .NET](https://github.com/Azure/azure-iot-sdk-csharp.git) to create the certificate to be used with the individual enrollment entry for the simulated device.</span></span>


1. <span data-ttu-id="37461-118">In a command prompt, change directories to the project directory for the X.509 device provisioning sample.</span><span class="sxs-lookup"><span data-stu-id="37461-118">In a command prompt, change directories to the project directory for the X.509 device provisioning sample.</span></span>

    ```cmd
    cd .\azure-iot-sdk-csharp\provisioning\device\samples\ProvisioningDeviceClientX509
    ```

2. <span data-ttu-id="37461-119">The sample code is set up to use X.509 certificates stored within a password-protected PKCS12 formatted file (certificate.pfx).</span><span class="sxs-lookup"><span data-stu-id="37461-119">The sample code is set up to use X.509 certificates stored within a password-protected PKCS12 formatted file (certificate.pfx).</span></span> <span data-ttu-id="37461-120">Additionally, you need a public key certificate file (certificate.cer) to create an individual enrollment later in this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="37461-120">Additionally, you need a public key certificate file (certificate.cer) to create an individual enrollment later in this Quickstart.</span></span> <span data-ttu-id="37461-121">To generate a self-signed certificate and its associated .cer and .pfx files, run the following command:</span><span class="sxs-lookup"><span data-stu-id="37461-121">To generate a self-signed certificate and its associated .cer and .pfx files, run the following command:</span></span>

    ```cmd
    powershell .\GenerateTestCertificate.ps1
    ```

3. <span data-ttu-id="37461-122">The script prompts you for a PFX password.</span><span class="sxs-lookup"><span data-stu-id="37461-122">The script prompts you for a PFX password.</span></span> <span data-ttu-id="37461-123">Remember this password, you must use it when you run the sample.</span><span class="sxs-lookup"><span data-stu-id="37461-123">Remember this password, you must use it when you run the sample.</span></span>

    ![ <span data-ttu-id="37461-124">Enter the PFX password</span><span class="sxs-lookup"><span data-stu-id="37461-124">Enter the PFX password</span></span>](./media/quick-create-simulated-device-x509-csharp/generate-certificate.png)  


4. <span data-ttu-id="37461-125">Log in to the Azure portal, click on the **All resources** button on the left-hand menu and open your provisioning service.</span><span class="sxs-lookup"><span data-stu-id="37461-125">Log in to the Azure portal, click on the **All resources** button on the left-hand menu and open your provisioning service.</span></span>

5. <span data-ttu-id="37461-126">On the Device Provisioning Service summary blade, select **Manage enrollments**.</span><span class="sxs-lookup"><span data-stu-id="37461-126">On the Device Provisioning Service summary blade, select **Manage enrollments**.</span></span> <span data-ttu-id="37461-127">Select **Individual Enrollments** tab and click the **Add** button at the top.</span><span class="sxs-lookup"><span data-stu-id="37461-127">Select **Individual Enrollments** tab and click the **Add** button at the top.</span></span> 

6. <span data-ttu-id="37461-128">Under the **Add enrollment** panel, enter the following information:</span><span class="sxs-lookup"><span data-stu-id="37461-128">Under the **Add enrollment** panel, enter the following information:</span></span>
    - <span data-ttu-id="37461-129">Select **X.509** as the identity attestation *Mechanism*.</span><span class="sxs-lookup"><span data-stu-id="37461-129">Select **X.509** as the identity attestation *Mechanism*.</span></span>
    - <span data-ttu-id="37461-130">Under the *Primary certificate .pem or .cer file*, click *Select a file* to select the certificate file **certificate.cer** created in the previous steps.</span><span class="sxs-lookup"><span data-stu-id="37461-130">Under the *Primary certificate .pem or .cer file*, click *Select a file* to select the certificate file **certificate.cer** created in the previous steps.</span></span>
    - <span data-ttu-id="37461-131">Leave **Device ID** blank.</span><span class="sxs-lookup"><span data-stu-id="37461-131">Leave **Device ID** blank.</span></span> <span data-ttu-id="37461-132">Your device will be provisioned with its device ID set to the common name (CN) in the X.509 certificate, **iothubx509device1**.</span><span class="sxs-lookup"><span data-stu-id="37461-132">Your device will be provisioned with its device ID set to the common name (CN) in the X.509 certificate, **iothubx509device1**.</span></span> <span data-ttu-id="37461-133">This will also be the name used for the registration ID for the individual enrollment entry.</span><span class="sxs-lookup"><span data-stu-id="37461-133">This will also be the name used for the registration ID for the individual enrollment entry.</span></span> 
    - <span data-ttu-id="37461-134">Optionally, you may provide the following information:</span><span class="sxs-lookup"><span data-stu-id="37461-134">Optionally, you may provide the following information:</span></span>
        - <span data-ttu-id="37461-135">Select an IoT hub linked with your provisioning service.</span><span class="sxs-lookup"><span data-stu-id="37461-135">Select an IoT hub linked with your provisioning service.</span></span>
        - <span data-ttu-id="37461-136">Update the **Initial device twin state** with the desired initial configuration for the device.</span><span class="sxs-lookup"><span data-stu-id="37461-136">Update the **Initial device twin state** with the desired initial configuration for the device.</span></span>
    - <span data-ttu-id="37461-137">Once complete, click the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="37461-137">Once complete, click the **Save** button.</span></span> 

    <span data-ttu-id="37461-138">[![Add individual enrollment for X.509 attestation in the portal](./media/quick-create-simulated-device-x509-csharp/individual-enrollment.png)](./media/quick-create-simulated-device-x509-csharp/individual-enrollment.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="37461-138">[![Add individual enrollment for X.509 attestation in the portal](./media/quick-create-simulated-device-x509-csharp/individual-enrollment.png)](./media/quick-create-simulated-device-x509-csharp/individual-enrollment.png#lightbox)</span></span>
    
   <span data-ttu-id="37461-139">On successful enrollment, your X.509 enrollment entry appears as **iothubx509device1** under the *Registration ID* column in the *Individual Enrollments* tab.</span><span class="sxs-lookup"><span data-stu-id="37461-139">On successful enrollment, your X.509 enrollment entry appears as **iothubx509device1** under the *Registration ID* column in the *Individual Enrollments* tab.</span></span> 

## <a name="provision-the-simulated-device"></a><span data-ttu-id="37461-140">Provision the simulated device</span><span class="sxs-lookup"><span data-stu-id="37461-140">Provision the simulated device</span></span>

1. <span data-ttu-id="37461-141">From the **Overview** blade for your provisioning service, note down the **_ID Scope_** value.</span><span class="sxs-lookup"><span data-stu-id="37461-141">From the **Overview** blade for your provisioning service, note down the **_ID Scope_** value.</span></span>

    ![Extract Device Provisioning Service endpoint information from the portal blade](./media/quick-create-simulated-device-x509-csharp/copy-scope.png) 


2. <span data-ttu-id="37461-143">Type the following command to build and run the X.509 device provisioning sample.</span><span class="sxs-lookup"><span data-stu-id="37461-143">Type the following command to build and run the X.509 device provisioning sample.</span></span> <span data-ttu-id="37461-144">Replace the `<IDScope>` value with the ID Scope for your provisioning service.</span><span class="sxs-lookup"><span data-stu-id="37461-144">Replace the `<IDScope>` value with the ID Scope for your provisioning service.</span></span> 

    ```cmd
    dotnet run <IDScope>
    ```

3. <span data-ttu-id="37461-145">When prompted enter the password for the PFX file that you created previously.</span><span class="sxs-lookup"><span data-stu-id="37461-145">When prompted enter the password for the PFX file that you created previously.</span></span> <span data-ttu-id="37461-146">Notice the messages that simulate the device booting and connecting to the Device Provisioning Service to get your IoT hub information.</span><span class="sxs-lookup"><span data-stu-id="37461-146">Notice the messages that simulate the device booting and connecting to the Device Provisioning Service to get your IoT hub information.</span></span> 

    ![Sample device output](./media/quick-create-simulated-device-x509-csharp/sample-output.png) 

4. <span data-ttu-id="37461-148">Verify that the device has been provisioned.</span><span class="sxs-lookup"><span data-stu-id="37461-148">Verify that the device has been provisioned.</span></span> <span data-ttu-id="37461-149">On successful provisioning of the simulated device to the IoT hub linked with your provisioning service, the device ID appears on the hub's **Iot Devices** blade.</span><span class="sxs-lookup"><span data-stu-id="37461-149">On successful provisioning of the simulated device to the IoT hub linked with your provisioning service, the device ID appears on the hub's **Iot Devices** blade.</span></span> 

    ![Device is registered with the IoT hub](./media/quick-create-simulated-device-x509-csharp/hub-registration.png) 

    <span data-ttu-id="37461-151">If you changed the *initial device twin state* from the default value in the enrollment entry for your device, it can pull the desired twin state from the hub and act accordingly.</span><span class="sxs-lookup"><span data-stu-id="37461-151">If you changed the *initial device twin state* from the default value in the enrollment entry for your device, it can pull the desired twin state from the hub and act accordingly.</span></span> <span data-ttu-id="37461-152">For more information, see [Understand and use device twins in IoT Hub](../iot-hub/iot-hub-devguide-device-twins.md)</span><span class="sxs-lookup"><span data-stu-id="37461-152">For more information, see [Understand and use device twins in IoT Hub](../iot-hub/iot-hub-devguide-device-twins.md)</span></span>


## <a name="clean-up-resources"></a><span data-ttu-id="37461-153">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="37461-153">Clean up resources</span></span>

<span data-ttu-id="37461-154">If you plan to continue working on and exploring the device client sample, do not clean up the resources created in this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="37461-154">If you plan to continue working on and exploring the device client sample, do not clean up the resources created in this Quickstart.</span></span> <span data-ttu-id="37461-155">If you do not plan to continue, use the following steps to delete all resources created by this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="37461-155">If you do not plan to continue, use the following steps to delete all resources created by this Quickstart.</span></span>

1. <span data-ttu-id="37461-156">Close the device client sample output window on your machine.</span><span class="sxs-lookup"><span data-stu-id="37461-156">Close the device client sample output window on your machine.</span></span>
1. <span data-ttu-id="37461-157">Close the TPM simulator window on your machine.</span><span class="sxs-lookup"><span data-stu-id="37461-157">Close the TPM simulator window on your machine.</span></span>
1. <span data-ttu-id="37461-158">From the left-hand menu in the Azure portal, click **All resources** and then select your Device Provisioning service.</span><span class="sxs-lookup"><span data-stu-id="37461-158">From the left-hand menu in the Azure portal, click **All resources** and then select your Device Provisioning service.</span></span> <span data-ttu-id="37461-159">At the top of the **All resources** blade, click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="37461-159">At the top of the **All resources** blade, click **Delete**.</span></span>  
1. <span data-ttu-id="37461-160">From the left-hand menu in the Azure portal, click **All resources** and then select your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="37461-160">From the left-hand menu in the Azure portal, click **All resources** and then select your IoT hub.</span></span> <span data-ttu-id="37461-161">At the top of the **All resources** blade, click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="37461-161">At the top of the **All resources** blade, click **Delete**.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="37461-162">Next steps</span><span class="sxs-lookup"><span data-stu-id="37461-162">Next steps</span></span>

<span data-ttu-id="37461-163">In this Quickstart, you’ve created a simulated X.509 device on your Windows machine and provisioned it to your IoT hub using the Azure IoT Hub Device Provisioning Service on the portal.</span><span class="sxs-lookup"><span data-stu-id="37461-163">In this Quickstart, you’ve created a simulated X.509 device on your Windows machine and provisioned it to your IoT hub using the Azure IoT Hub Device Provisioning Service on the portal.</span></span> <span data-ttu-id="37461-164">To learn how to enroll your X.509 device programmatically, continue to the Quickstart for programmatic enrollment of X.509 devices.</span><span class="sxs-lookup"><span data-stu-id="37461-164">To learn how to enroll your X.509 device programmatically, continue to the Quickstart for programmatic enrollment of X.509 devices.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="37461-165">Azure Quickstart - Enroll X.509 devices to Azure IoT Hub Device Provisioning Service</span><span class="sxs-lookup"><span data-stu-id="37461-165">Azure Quickstart - Enroll X.509 devices to Azure IoT Hub Device Provisioning Service</span></span>](quick-enroll-device-x509-csharp.md)
