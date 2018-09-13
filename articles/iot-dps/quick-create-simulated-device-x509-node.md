---
title: Provision a simulated X.509 device to Azure IoT Hub using Node.js | Microsoft Docs
description: Create and provision a simulated X.509 device using Node.js device SDK for Azure IoT Hub Device Provisioning Service
author: wesmc7777
ms.author: wesmc
ms.date: 04/09/2018
ms.topic: quickstart
ms.service: iot-dps
services: iot-dps
manager: timlt
ms.devlang: nodejs
ms.custom: mvc
ms.openlocfilehash: 1a3015a458a579b0aadf51d610db512eb908352b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870768"
---
# <a name="create-and-provision-an-x509-simulated-device-using-nodejs-device-sdk-for-iot-hub-device-provisioning-service"></a><span data-ttu-id="bb920-103">Create and provision an X.509 simulated device using Node.js device SDK for IoT Hub Device Provisioning Service</span><span class="sxs-lookup"><span data-stu-id="bb920-103">Create and provision an X.509 simulated device using Node.js device SDK for IoT Hub Device Provisioning Service</span></span>
[!INCLUDE [iot-dps-selector-quick-create-simulated-device-x509](../../includes/iot-dps-selector-quick-create-simulated-device-x509.md)]

<span data-ttu-id="bb920-104">These steps show how to create an enrollment entry in the Device Provisioning Service, simulate an X.509 device on your development machine, connect the simulated device with the Device Provisioning Service, and register the device on your IoT hub using the [Azure IoT Hub Node.js Device SDK](https://github.com/Azure/azure-iot-sdk-node).</span><span class="sxs-lookup"><span data-stu-id="bb920-104">These steps show how to create an enrollment entry in the Device Provisioning Service, simulate an X.509 device on your development machine, connect the simulated device with the Device Provisioning Service, and register the device on your IoT hub using the [Azure IoT Hub Node.js Device SDK](https://github.com/Azure/azure-iot-sdk-node).</span></span>

<span data-ttu-id="bb920-105">If you're unfamiliar with the process of auto-provisioning, be sure to also review [Auto-provisioning concepts](concepts-auto-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="bb920-105">If you're unfamiliar with the process of auto-provisioning, be sure to also review [Auto-provisioning concepts](concepts-auto-provisioning.md).</span></span> <span data-ttu-id="bb920-106">Also make sure you've completed the steps in [Set up IoT Hub Device Provisioning Service with the Azure portal](./quick-setup-auto-provision.md) before continuing.</span><span class="sxs-lookup"><span data-stu-id="bb920-106">Also make sure you've completed the steps in [Set up IoT Hub Device Provisioning Service with the Azure portal](./quick-setup-auto-provision.md) before continuing.</span></span> 

[!INCLUDE [IoT Device Provisioning Service basic](../../includes/iot-dps-basic.md)]

## <a name="prepare-the-environment"></a><span data-ttu-id="bb920-107">Prepare the environment</span><span class="sxs-lookup"><span data-stu-id="bb920-107">Prepare the environment</span></span> 

1. <span data-ttu-id="bb920-108">Complete the steps in the [Setup IoT Hub Device Provisioning Service with the Azure portal](./quick-setup-auto-provision.md) before you proceed.</span><span class="sxs-lookup"><span data-stu-id="bb920-108">Complete the steps in the [Setup IoT Hub Device Provisioning Service with the Azure portal](./quick-setup-auto-provision.md) before you proceed.</span></span>

2. <span data-ttu-id="bb920-109">Make sure you have [Node.js v4.0 or above](https://nodejs.org) installed on your machine.</span><span class="sxs-lookup"><span data-stu-id="bb920-109">Make sure you have [Node.js v4.0 or above](https://nodejs.org) installed on your machine.</span></span>

3. <span data-ttu-id="bb920-110">Make sure [Git](https://git-scm.com/download/) is installed on your machine and is added to the environment variables accessible to the command window.</span><span class="sxs-lookup"><span data-stu-id="bb920-110">Make sure [Git](https://git-scm.com/download/) is installed on your machine and is added to the environment variables accessible to the command window.</span></span> 

4. <span data-ttu-id="bb920-111">Make sure [OpenSSL](https://www.openssl.org/) is installed on your machine and is added to the environment variables accessible to the command window.</span><span class="sxs-lookup"><span data-stu-id="bb920-111">Make sure [OpenSSL](https://www.openssl.org/) is installed on your machine and is added to the environment variables accessible to the command window.</span></span> <span data-ttu-id="bb920-112">This library can either be built and installed from source or downloaded and installed from a [third party](https://wiki.openssl.org/index.php/Binaries) such as [this](https://sourceforge.net/projects/openssl/).</span><span class="sxs-lookup"><span data-stu-id="bb920-112">This library can either be built and installed from source or downloaded and installed from a [third party](https://wiki.openssl.org/index.php/Binaries) such as [this](https://sourceforge.net/projects/openssl/).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="bb920-113">If you have already created your _root_, _intermediate_, and/or _leaf_ X.509 certificates, you may skip this step and all following steps regarding certificate generation.</span><span class="sxs-lookup"><span data-stu-id="bb920-113">If you have already created your _root_, _intermediate_, and/or _leaf_ X.509 certificates, you may skip this step and all following steps regarding certificate generation.</span></span>
    >

## <a name="create-a-self-signed-x509-device-certificate-and-individual-enrollment-entry"></a><span data-ttu-id="bb920-114">Create a self-signed X.509 device certificate and individual enrollment entry</span><span class="sxs-lookup"><span data-stu-id="bb920-114">Create a self-signed X.509 device certificate and individual enrollment entry</span></span>

<span data-ttu-id="bb920-115">In this section you, will use a self-signed X.509 certificate, it is important to keep in mind the following:</span><span class="sxs-lookup"><span data-stu-id="bb920-115">In this section you, will use a self-signed X.509 certificate, it is important to keep in mind the following:</span></span>

* <span data-ttu-id="bb920-116">Self-signed certificates are for testing only, and should not to be used in production.</span><span class="sxs-lookup"><span data-stu-id="bb920-116">Self-signed certificates are for testing only, and should not to be used in production.</span></span>
* <span data-ttu-id="bb920-117">The default expiration date for a self-signed certificate is 1 year.</span><span class="sxs-lookup"><span data-stu-id="bb920-117">The default expiration date for a self-signed certificate is 1 year.</span></span>

<span data-ttu-id="bb920-118">You will use sample code from the [Azure IoT SDK for Node.js](https://github.com/Azure/azure-iot-sdk-node.git) to create the certificate to be used with the individual enrollment entry for the simulated device.</span><span class="sxs-lookup"><span data-stu-id="bb920-118">You will use sample code from the [Azure IoT SDK for Node.js](https://github.com/Azure/azure-iot-sdk-node.git) to create the certificate to be used with the individual enrollment entry for the simulated device.</span></span>


1. <span data-ttu-id="bb920-119">Open a command prompt.</span><span class="sxs-lookup"><span data-stu-id="bb920-119">Open a command prompt.</span></span> <span data-ttu-id="bb920-120">Clone the GitHub repo for the code samples:</span><span class="sxs-lookup"><span data-stu-id="bb920-120">Clone the GitHub repo for the code samples:</span></span>
    
    ```cmd/sh
    git clone https://github.com/Azure/azure-iot-sdk-node.git --recursive
    ```

2. <span data-ttu-id="bb920-121">Navigate to the certificate generator script and build the project.</span><span class="sxs-lookup"><span data-stu-id="bb920-121">Navigate to the certificate generator script and build the project.</span></span> 

    ```cmd/sh
    cd azure-iot-sdk-node/provisioning/tools
    npm install
    ```

3. <span data-ttu-id="bb920-122">Create a _leaf_ X.509 certificate by running the script using your own _certificate-name_.</span><span class="sxs-lookup"><span data-stu-id="bb920-122">Create a _leaf_ X.509 certificate by running the script using your own _certificate-name_.</span></span> <span data-ttu-id="bb920-123">Note that the leaf certificate's common name becomes the [Registration ID](https://docs.microsoft.com/azure/iot-dps/concepts-device#registration-id) so be sure to only use lower-case alphanumerics and hyphens.</span><span class="sxs-lookup"><span data-stu-id="bb920-123">Note that the leaf certificate's common name becomes the [Registration ID](https://docs.microsoft.com/azure/iot-dps/concepts-device#registration-id) so be sure to only use lower-case alphanumerics and hyphens.</span></span>

    ```cmd/sh
    node create_test_cert.js device {certificate-name}
    ```

4. <span data-ttu-id="bb920-124">Sign in to the [Azure portal](https://portal.azure.com), click on the **All resources** button on the left-hand menu and open your Device Provisioning Service instance.</span><span class="sxs-lookup"><span data-stu-id="bb920-124">Sign in to the [Azure portal](https://portal.azure.com), click on the **All resources** button on the left-hand menu and open your Device Provisioning Service instance.</span></span>

5. <span data-ttu-id="bb920-125">On the Device Provisioning Service summary blade, select **Manage enrollments**.</span><span class="sxs-lookup"><span data-stu-id="bb920-125">On the Device Provisioning Service summary blade, select **Manage enrollments**.</span></span> <span data-ttu-id="bb920-126">Select **Individual Enrollments** tab and click the **Add** button at the top.</span><span class="sxs-lookup"><span data-stu-id="bb920-126">Select **Individual Enrollments** tab and click the **Add** button at the top.</span></span> 

6. <span data-ttu-id="bb920-127">Under the **Add enrollment** panel, enter the following information:</span><span class="sxs-lookup"><span data-stu-id="bb920-127">Under the **Add enrollment** panel, enter the following information:</span></span>
    - <span data-ttu-id="bb920-128">Select **X.509** as the identity attestation *Mechanism*.</span><span class="sxs-lookup"><span data-stu-id="bb920-128">Select **X.509** as the identity attestation *Mechanism*.</span></span>
    - <span data-ttu-id="bb920-129">Under the *Primary certificate .pem or .cer file*, click *Select a file* to select the certificate file **{certificate-name}_cert.pem** created in the previous steps.</span><span class="sxs-lookup"><span data-stu-id="bb920-129">Under the *Primary certificate .pem or .cer file*, click *Select a file* to select the certificate file **{certificate-name}_cert.pem** created in the previous steps.</span></span>  
    - <span data-ttu-id="bb920-130">Optionally, you may provide the following information:</span><span class="sxs-lookup"><span data-stu-id="bb920-130">Optionally, you may provide the following information:</span></span>
      - <span data-ttu-id="bb920-131">Select an IoT hub linked with your provisioning service.</span><span class="sxs-lookup"><span data-stu-id="bb920-131">Select an IoT hub linked with your provisioning service.</span></span>
      - <span data-ttu-id="bb920-132">Enter a unique device ID.</span><span class="sxs-lookup"><span data-stu-id="bb920-132">Enter a unique device ID.</span></span> <span data-ttu-id="bb920-133">Make sure to avoid sensitive data while naming your device.</span><span class="sxs-lookup"><span data-stu-id="bb920-133">Make sure to avoid sensitive data while naming your device.</span></span> 
      - <span data-ttu-id="bb920-134">Update the **Initial device twin state** with the desired initial configuration for the device.</span><span class="sxs-lookup"><span data-stu-id="bb920-134">Update the **Initial device twin state** with the desired initial configuration for the device.</span></span>
   - <span data-ttu-id="bb920-135">Once complete, click the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="bb920-135">Once complete, click the **Save** button.</span></span> 

    <span data-ttu-id="bb920-136">[![Add individual enrollment for X.509 attestation in the portal](./media/quick-create-simulated-device-x509-node/individual-enrollment.png)](./media/quick-create-simulated-device-x509-node/individual-enrollment.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="bb920-136">[![Add individual enrollment for X.509 attestation in the portal](./media/quick-create-simulated-device-x509-node/individual-enrollment.png)](./media/quick-create-simulated-device-x509-node/individual-enrollment.png#lightbox)</span></span>

    <span data-ttu-id="bb920-137">On successful enrollment, your X.509 device appears as **{certificatename}** under the *Registration ID* column in the *Individual Enrollments* tab. Note this value for later.</span><span class="sxs-lookup"><span data-stu-id="bb920-137">On successful enrollment, your X.509 device appears as **{certificatename}** under the *Registration ID* column in the *Individual Enrollments* tab. Note this value for later.</span></span>

## <a name="simulate-the-device"></a><span data-ttu-id="bb920-138">Simulate the device</span><span class="sxs-lookup"><span data-stu-id="bb920-138">Simulate the device</span></span>

<span data-ttu-id="bb920-139">The [Azure IoT Hub Node.js Device SDK](https://github.com/Azure/azure-iot-sdk-node) provides an easy way to simulate a device.</span><span class="sxs-lookup"><span data-stu-id="bb920-139">The [Azure IoT Hub Node.js Device SDK](https://github.com/Azure/azure-iot-sdk-node) provides an easy way to simulate a device.</span></span> <span data-ttu-id="bb920-140">For further reading see [Device concepts](https://docs.microsoft.com/azure/iot-dps/concepts-device).</span><span class="sxs-lookup"><span data-stu-id="bb920-140">For further reading see [Device concepts](https://docs.microsoft.com/azure/iot-dps/concepts-device).</span></span>

1. <span data-ttu-id="bb920-141">In the Azure portal, select the **Overview** blade for your Device Provisioning service and note down the **_GLobal Device Endpoint_** and **_ID Scope_** values.</span><span class="sxs-lookup"><span data-stu-id="bb920-141">In the Azure portal, select the **Overview** blade for your Device Provisioning service and note down the **_GLobal Device Endpoint_** and **_ID Scope_** values.</span></span>

    ![Extract Device Provisioning Service endpoint information from the portal blade](./media/quick-create-simulated-device-x509-node/extract-dps-endpoints.png) 

2. <span data-ttu-id="bb920-143">Copy your _certificate_ and _key_ to the sample folder.</span><span class="sxs-lookup"><span data-stu-id="bb920-143">Copy your _certificate_ and _key_ to the sample folder.</span></span>

    ```cmd/sh
    copy .\{certificate-name}_cert.pem ..\device\samples\{certificate-name}_cert.pem
    copy .\{certificate-name}_key.pem ..\device\samples\{certificate-name}_key.pem
    ```

3. <span data-ttu-id="bb920-144">Navigate to the device test script and build the project.</span><span class="sxs-lookup"><span data-stu-id="bb920-144">Navigate to the device test script and build the project.</span></span> 

    ```cmd/sh
    cd ..\device\samples
    npm install
    ```

4. <span data-ttu-id="bb920-145">Edit the **register\_x509.js** file.</span><span class="sxs-lookup"><span data-stu-id="bb920-145">Edit the **register\_x509.js** file.</span></span> <span data-ttu-id="bb920-146">Save the file after making the following changes.</span><span class="sxs-lookup"><span data-stu-id="bb920-146">Save the file after making the following changes.</span></span>
    - <span data-ttu-id="bb920-147">Replace `provisioning host` with the **_Global Device Endpoint_** noted in **Step 1** above.</span><span class="sxs-lookup"><span data-stu-id="bb920-147">Replace `provisioning host` with the **_Global Device Endpoint_** noted in **Step 1** above.</span></span>
    - <span data-ttu-id="bb920-148">Replace `id scope` with the **_Id Scope_** noted in **Step 1** above.</span><span class="sxs-lookup"><span data-stu-id="bb920-148">Replace `id scope` with the **_Id Scope_** noted in **Step 1** above.</span></span> 
    - <span data-ttu-id="bb920-149">Replace `registration id` with the **_Registration Id_** noted in the previous section.</span><span class="sxs-lookup"><span data-stu-id="bb920-149">Replace `registration id` with the **_Registration Id_** noted in the previous section.</span></span>
    - <span data-ttu-id="bb920-150">Replace `cert filename` and `key filename` with the files you copied in **Step 2** above.</span><span class="sxs-lookup"><span data-stu-id="bb920-150">Replace `cert filename` and `key filename` with the files you copied in **Step 2** above.</span></span> 

5. <span data-ttu-id="bb920-151">Execute the script and verify the device was provisioned successfully.</span><span class="sxs-lookup"><span data-stu-id="bb920-151">Execute the script and verify the device was provisioned successfully.</span></span>

    ```cmd/sh
    node register_x509.js
    ```   

6. <span data-ttu-id="bb920-152">In the portal, navigate to the IoT hub linked to your provisioning service and open the **IoT Devices** blade.</span><span class="sxs-lookup"><span data-stu-id="bb920-152">In the portal, navigate to the IoT hub linked to your provisioning service and open the **IoT Devices** blade.</span></span> <span data-ttu-id="bb920-153">On successful provisioning of the simulated X.509 device to the hub, its device ID appears on the **IoT Devices** blade, with *STATUS* as **enabled**.</span><span class="sxs-lookup"><span data-stu-id="bb920-153">On successful provisioning of the simulated X.509 device to the hub, its device ID appears on the **IoT Devices** blade, with *STATUS* as **enabled**.</span></span> <span data-ttu-id="bb920-154">You might need to click the **Refresh** button at the top if you already opened the blade prior to running the sample device application.</span><span class="sxs-lookup"><span data-stu-id="bb920-154">You might need to click the **Refresh** button at the top if you already opened the blade prior to running the sample device application.</span></span> 

    ![Device is registered with the IoT hub](./media/quick-create-simulated-device-x509-node/hub-registration.png) 

    <span data-ttu-id="bb920-156">If you changed the *initial device twin state* from the default value in the enrollment entry for your device, it can pull the desired twin state from the hub and act accordingly.</span><span class="sxs-lookup"><span data-stu-id="bb920-156">If you changed the *initial device twin state* from the default value in the enrollment entry for your device, it can pull the desired twin state from the hub and act accordingly.</span></span> <span data-ttu-id="bb920-157">For more information, see [Understand and use device twins in IoT Hub](../iot-hub/iot-hub-devguide-device-twins.md).</span><span class="sxs-lookup"><span data-stu-id="bb920-157">For more information, see [Understand and use device twins in IoT Hub](../iot-hub/iot-hub-devguide-device-twins.md).</span></span>


## <a name="clean-up-resources"></a><span data-ttu-id="bb920-158">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="bb920-158">Clean up resources</span></span>

<span data-ttu-id="bb920-159">If you plan to continue working on and exploring the device client sample, do not clean up the resources created in this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="bb920-159">If you plan to continue working on and exploring the device client sample, do not clean up the resources created in this Quickstart.</span></span> <span data-ttu-id="bb920-160">If you do not plan to continue, use the following steps to delete all resources created by this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="bb920-160">If you do not plan to continue, use the following steps to delete all resources created by this Quickstart.</span></span>

1. <span data-ttu-id="bb920-161">Close the device client sample output window on your machine.</span><span class="sxs-lookup"><span data-stu-id="bb920-161">Close the device client sample output window on your machine.</span></span>
2. <span data-ttu-id="bb920-162">From the left-hand menu in the Azure portal, click **All resources** and then select your Device Provisioning service.</span><span class="sxs-lookup"><span data-stu-id="bb920-162">From the left-hand menu in the Azure portal, click **All resources** and then select your Device Provisioning service.</span></span> <span data-ttu-id="bb920-163">Open the **Manage Enrollments** blade for your service, and then click the **Individual Enrollments** tab. Select the *REGISTRATION ID* of the device you enrolled in this Quickstart, and click the **Delete** button at the top.</span><span class="sxs-lookup"><span data-stu-id="bb920-163">Open the **Manage Enrollments** blade for your service, and then click the **Individual Enrollments** tab. Select the *REGISTRATION ID* of the device you enrolled in this Quickstart, and click the **Delete** button at the top.</span></span> 
3. <span data-ttu-id="bb920-164">From the left-hand menu in the Azure portal, click **All resources** and then select your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="bb920-164">From the left-hand menu in the Azure portal, click **All resources** and then select your IoT hub.</span></span> <span data-ttu-id="bb920-165">Open the **IoT Devices** blade for your hub, select the *DEVICE ID* of the device you registered in this Quickstart, and then click **Delete** button at the top.</span><span class="sxs-lookup"><span data-stu-id="bb920-165">Open the **IoT Devices** blade for your hub, select the *DEVICE ID* of the device you registered in this Quickstart, and then click **Delete** button at the top.</span></span>


## <a name="next-steps"></a><span data-ttu-id="bb920-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="bb920-166">Next steps</span></span>

<span data-ttu-id="bb920-167">In this Quickstart, you’ve created a simulated X.509 device and provisioned it to your IoT hub using the Azure IoT Hub Device Provisioning Service on the portal.</span><span class="sxs-lookup"><span data-stu-id="bb920-167">In this Quickstart, you’ve created a simulated X.509 device and provisioned it to your IoT hub using the Azure IoT Hub Device Provisioning Service on the portal.</span></span> <span data-ttu-id="bb920-168">To learn how to enroll your X.509 device programmatically, continue to the Quickstart for programmatic enrollment of X.509 devices.</span><span class="sxs-lookup"><span data-stu-id="bb920-168">To learn how to enroll your X.509 device programmatically, continue to the Quickstart for programmatic enrollment of X.509 devices.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="bb920-169">Azure Quickstart - Enroll X.509 devices to Azure IoT Hub Device Provisioning Service</span><span class="sxs-lookup"><span data-stu-id="bb920-169">Azure Quickstart - Enroll X.509 devices to Azure IoT Hub Device Provisioning Service</span></span>](quick-enroll-device-x509-node.md)
