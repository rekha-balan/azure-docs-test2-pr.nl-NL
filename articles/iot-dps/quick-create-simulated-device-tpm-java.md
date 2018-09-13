---
title: Provision a simulated TPM device to Azure IoT Hub using Java | Microsoft Docs
description: Azure Quickstart - Create and provision a simulated TPM device using Java device SDK for Azure IoT Hub Device Provisioning Service
author: wesmc7777
ms.author: wesmc
ms.date: 04/09/2018
ms.topic: quickstart
ms.service: iot-dps
services: iot-dps
manager: timlt
ms.devlang: java
ms.custom: mvc
ms.openlocfilehash: 18342b7f3980bcd43b386c3282dda6ebf17eebba
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857210"
---
# <a name="create-and-provision-a-simulated-tpm-device-using-java-device-sdk-for-azure-iot-hub-device-provisioning-service"></a><span data-ttu-id="11077-103">Create and provision a simulated TPM device using Java device SDK for Azure IoT Hub Device Provisioning Service</span><span class="sxs-lookup"><span data-stu-id="11077-103">Create and provision a simulated TPM device using Java device SDK for Azure IoT Hub Device Provisioning Service</span></span>

[!INCLUDE [iot-dps-selector-quick-create-simulated-device-tpm](../../includes/iot-dps-selector-quick-create-simulated-device-tpm.md)]

<span data-ttu-id="11077-104">These steps show how to create a simulated device on your development machine running Windows OS, run the Windows TPM simulator as the [Hardware Security Module (HSM)](https://azure.microsoft.com/blog/azure-iot-supports-new-security-hardware-to-strengthen-iot-security/) of the device, and use the code sample to connect this simulated device with the Device Provisioning Service and your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="11077-104">These steps show how to create a simulated device on your development machine running Windows OS, run the Windows TPM simulator as the [Hardware Security Module (HSM)](https://azure.microsoft.com/blog/azure-iot-supports-new-security-hardware-to-strengthen-iot-security/) of the device, and use the code sample to connect this simulated device with the Device Provisioning Service and your IoT hub.</span></span> 

<span data-ttu-id="11077-105">If you're unfamiliar with the process of auto-provisioning, be sure to also review [Auto-provisioning concepts](concepts-auto-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="11077-105">If you're unfamiliar with the process of auto-provisioning, be sure to also review [Auto-provisioning concepts](concepts-auto-provisioning.md).</span></span> <span data-ttu-id="11077-106">Also make sure you've completed the steps in [Set up IoT Hub Device Provisioning Service with the Azure portal](./quick-setup-auto-provision.md) before continuing.</span><span class="sxs-lookup"><span data-stu-id="11077-106">Also make sure you've completed the steps in [Set up IoT Hub Device Provisioning Service with the Azure portal](./quick-setup-auto-provision.md) before continuing.</span></span> 

[!INCLUDE [IoT Device Provisioning Service basic](../../includes/iot-dps-basic.md)]

## <a name="prepare-the-environment"></a><span data-ttu-id="11077-107">Prepare the environment</span><span class="sxs-lookup"><span data-stu-id="11077-107">Prepare the environment</span></span> 

1. <span data-ttu-id="11077-108">Make sure you have [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) installed on your machine.</span><span class="sxs-lookup"><span data-stu-id="11077-108">Make sure you have [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) installed on your machine.</span></span>

1. <span data-ttu-id="11077-109">Download and install [Maven](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="11077-109">Download and install [Maven](https://maven.apache.org/install.html).</span></span>

1. <span data-ttu-id="11077-110">Make sure `git` is installed on your machine and is added to the environment variables accessible to the command window.</span><span class="sxs-lookup"><span data-stu-id="11077-110">Make sure `git` is installed on your machine and is added to the environment variables accessible to the command window.</span></span> <span data-ttu-id="11077-111">See [Software Freedom Conservancy's Git client tools](https://git-scm.com/download/) for the latest version of `git` tools to install, which includes the **Git Bash**, the command-line app that you can use to interact with your local Git repository.</span><span class="sxs-lookup"><span data-stu-id="11077-111">See [Software Freedom Conservancy's Git client tools](https://git-scm.com/download/) for the latest version of `git` tools to install, which includes the **Git Bash**, the command-line app that you can use to interact with your local Git repository.</span></span> 

1. <span data-ttu-id="11077-112">Open a command prompt.</span><span class="sxs-lookup"><span data-stu-id="11077-112">Open a command prompt.</span></span> <span data-ttu-id="11077-113">Clone the GitHub repo for device simulation code sample.</span><span class="sxs-lookup"><span data-stu-id="11077-113">Clone the GitHub repo for device simulation code sample.</span></span>
    
    ```cmd/sh
    git clone https://github.com/Azure/azure-iot-sdk-java.git --recursive
    ```

1. <span data-ttu-id="11077-114">Run the [TPM](https://docs.microsoft.com/windows/device-security/tpm/trusted-platform-module-overview) simulator.</span><span class="sxs-lookup"><span data-stu-id="11077-114">Run the [TPM](https://docs.microsoft.com/windows/device-security/tpm/trusted-platform-module-overview) simulator.</span></span> <span data-ttu-id="11077-115">Click **Allow access** to allow changes to _Windows Firewall_ settings.</span><span class="sxs-lookup"><span data-stu-id="11077-115">Click **Allow access** to allow changes to _Windows Firewall_ settings.</span></span> <span data-ttu-id="11077-116">It listens over a socket on ports 2321 and 2322.</span><span class="sxs-lookup"><span data-stu-id="11077-116">It listens over a socket on ports 2321 and 2322.</span></span> <span data-ttu-id="11077-117">Do not close this window; you need to keep this simulator running until the end of this Quickstart guide.</span><span class="sxs-lookup"><span data-stu-id="11077-117">Do not close this window; you need to keep this simulator running until the end of this Quickstart guide.</span></span> 

    ```cmd/sh
    .\azure-iot-sdk-java\provisioning\provisioning-tools\tpm-simulator\Simulator.exe
    ```

    ![TPM Simulator](./media/java-quick-create-simulated-device/simulator.png)

1. <span data-ttu-id="11077-119">In a separate command prompt, navigate to the root folder and build the sample dependencies.</span><span class="sxs-lookup"><span data-stu-id="11077-119">In a separate command prompt, navigate to the root folder and build the sample dependencies.</span></span>

    ```cmd/sh
    cd azure-iot-sdk-java
    mvn install -DskipTests=true
    ```

1. <span data-ttu-id="11077-120">Navigate to the sample folder.</span><span class="sxs-lookup"><span data-stu-id="11077-120">Navigate to the sample folder.</span></span>

    ```cmd/sh
    cd provisioning/provisioning-samples/provisioning-tpm-sample
    ```

1. <span data-ttu-id="11077-121">Log in to the Azure portal, click on the **All resources** button on the left-hand menu and open your Device Provisioning service.</span><span class="sxs-lookup"><span data-stu-id="11077-121">Log in to the Azure portal, click on the **All resources** button on the left-hand menu and open your Device Provisioning service.</span></span> <span data-ttu-id="11077-122">Note your _Id Scope_ and _Provisioning Service Global Endpoint_.</span><span class="sxs-lookup"><span data-stu-id="11077-122">Note your _Id Scope_ and _Provisioning Service Global Endpoint_.</span></span>

    ![Device Provisioning Service information](./media/java-quick-create-simulated-device/extract-dps-endpoints.png)

1. <span data-ttu-id="11077-124">Edit `src/main/java/samples/com/microsoft/azure/sdk/iot/ProvisioningTpmSample.java` to include your _Id Scope_ and _Provisioning Service Global Endpoint_ as noted before.</span><span class="sxs-lookup"><span data-stu-id="11077-124">Edit `src/main/java/samples/com/microsoft/azure/sdk/iot/ProvisioningTpmSample.java` to include your _Id Scope_ and _Provisioning Service Global Endpoint_ as noted before.</span></span>  

    ```java
    private static final String idScope = "[Your ID scope here]";
    private static final String globalEndpoint = "[Your Provisioning Service Global Endpoint here]";
    private static final ProvisioningDeviceClientTransportProtocol PROVISIONING_DEVICE_CLIENT_TRANSPORT_PROTOCOL = ProvisioningDeviceClientTransportProtocol.HTTPS;
    ```

1. <span data-ttu-id="11077-125">Build the project.</span><span class="sxs-lookup"><span data-stu-id="11077-125">Build the project.</span></span> <span data-ttu-id="11077-126">Navigate to the target folder and execute the created jar file.</span><span class="sxs-lookup"><span data-stu-id="11077-126">Navigate to the target folder and execute the created jar file.</span></span>

    ```cmd/sh
    mvn clean install
    cd target
    java -jar ./provisioning-tpm-sample-{version}-with-deps.jar
    ```

1. <span data-ttu-id="11077-127">The program begins running.</span><span class="sxs-lookup"><span data-stu-id="11077-127">The program begins running.</span></span> <span data-ttu-id="11077-128">Note the _Endorsement Key_ and _Registration Id_ for the next section and leave the program running.</span><span class="sxs-lookup"><span data-stu-id="11077-128">Note the _Endorsement Key_ and _Registration Id_ for the next section and leave the program running.</span></span>

    ![Java TPM device program](./media/java-quick-create-simulated-device/program.png)
    

## <a name="create-a-device-enrollment-entry"></a><span data-ttu-id="11077-130">Create a device enrollment entry</span><span class="sxs-lookup"><span data-stu-id="11077-130">Create a device enrollment entry</span></span>

1. <span data-ttu-id="11077-131">Log in to the Azure portal, click on the **All resources** button on the left-hand menu and open your Device Provisioning service.</span><span class="sxs-lookup"><span data-stu-id="11077-131">Log in to the Azure portal, click on the **All resources** button on the left-hand menu and open your Device Provisioning service.</span></span>

1. <span data-ttu-id="11077-132">On the Device Provisioning Service summary blade, select **Manage enrollments**.</span><span class="sxs-lookup"><span data-stu-id="11077-132">On the Device Provisioning Service summary blade, select **Manage enrollments**.</span></span> <span data-ttu-id="11077-133">Select **Individual Enrollments** tab and click the **Add** button at the top.</span><span class="sxs-lookup"><span data-stu-id="11077-133">Select **Individual Enrollments** tab and click the **Add** button at the top.</span></span> 

1. <span data-ttu-id="11077-134">Under the **Add enrollment list entry**, enter the following information:</span><span class="sxs-lookup"><span data-stu-id="11077-134">Under the **Add enrollment list entry**, enter the following information:</span></span>
    - <span data-ttu-id="11077-135">Select **TPM** as the identity attestation *Mechanism*.</span><span class="sxs-lookup"><span data-stu-id="11077-135">Select **TPM** as the identity attestation *Mechanism*.</span></span>
    - <span data-ttu-id="11077-136">Enter the *Registration ID* and *Endorsement key* for your TPM device as noted previously.</span><span class="sxs-lookup"><span data-stu-id="11077-136">Enter the *Registration ID* and *Endorsement key* for your TPM device as noted previously.</span></span> 
    - <span data-ttu-id="11077-137">Select an IoT hub linked with your provisioning service.</span><span class="sxs-lookup"><span data-stu-id="11077-137">Select an IoT hub linked with your provisioning service.</span></span>
    - <span data-ttu-id="11077-138">Enter a unique device ID.</span><span class="sxs-lookup"><span data-stu-id="11077-138">Enter a unique device ID.</span></span> <span data-ttu-id="11077-139">Make sure to avoid sensitive data while naming your device.</span><span class="sxs-lookup"><span data-stu-id="11077-139">Make sure to avoid sensitive data while naming your device.</span></span>
    - <span data-ttu-id="11077-140">Update the **Initial device twin state** with the desired initial configuration for the device.</span><span class="sxs-lookup"><span data-stu-id="11077-140">Update the **Initial device twin state** with the desired initial configuration for the device.</span></span>
    - <span data-ttu-id="11077-141">Once complete, click the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="11077-141">Once complete, click the **Save** button.</span></span> 

    ![Enter device enrollment information in the portal blade](./media/java-quick-create-simulated-device/enter-device-enrollment.png)  

   <span data-ttu-id="11077-143">On successful enrollment, the *Registration ID* of your device appears in the list under the *Individual Enrollments* tab.</span><span class="sxs-lookup"><span data-stu-id="11077-143">On successful enrollment, the *Registration ID* of your device appears in the list under the *Individual Enrollments* tab.</span></span> 


## <a name="simulate-the-device"></a><span data-ttu-id="11077-144">Simulate the device</span><span class="sxs-lookup"><span data-stu-id="11077-144">Simulate the device</span></span>

1. <span data-ttu-id="11077-145">On the command window running the Java sample code on your machine, click enter to continue running the application.</span><span class="sxs-lookup"><span data-stu-id="11077-145">On the command window running the Java sample code on your machine, click enter to continue running the application.</span></span> <span data-ttu-id="11077-146">Notice the messages that simulate the device booting and connecting to the Device Provisioning Service to get your IoT hub information.</span><span class="sxs-lookup"><span data-stu-id="11077-146">Notice the messages that simulate the device booting and connecting to the Device Provisioning Service to get your IoT hub information.</span></span>  

    ![Java TPM device program final](./media/java-quick-create-simulated-device/program-final.png)

1. <span data-ttu-id="11077-148">On successful provisioning of your simulated device to the IoT hub linked with your provisioning service, the device ID appears on the hub's **Device Explorer** blade.</span><span class="sxs-lookup"><span data-stu-id="11077-148">On successful provisioning of your simulated device to the IoT hub linked with your provisioning service, the device ID appears on the hub's **Device Explorer** blade.</span></span>

    ![Device is registered with the IoT hub](./media/java-quick-create-simulated-device/hub-registration.png) 

    <span data-ttu-id="11077-150">If you changed the *initial device twin state* from the default value in the enrollment entry for your device, it can pull the desired twin state from the hub and act accordingly.</span><span class="sxs-lookup"><span data-stu-id="11077-150">If you changed the *initial device twin state* from the default value in the enrollment entry for your device, it can pull the desired twin state from the hub and act accordingly.</span></span> <span data-ttu-id="11077-151">For more information, see [Understand and use device twins in IoT Hub](../iot-hub/iot-hub-devguide-device-twins.md)</span><span class="sxs-lookup"><span data-stu-id="11077-151">For more information, see [Understand and use device twins in IoT Hub](../iot-hub/iot-hub-devguide-device-twins.md)</span></span>


## <a name="clean-up-resources"></a><span data-ttu-id="11077-152">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="11077-152">Clean up resources</span></span>

<span data-ttu-id="11077-153">If you plan to continue working on and exploring the device client sample, do not clean up the resources created in this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="11077-153">If you plan to continue working on and exploring the device client sample, do not clean up the resources created in this Quickstart.</span></span> <span data-ttu-id="11077-154">If you do not plan to continue, use the following steps to delete all resources created by this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="11077-154">If you do not plan to continue, use the following steps to delete all resources created by this Quickstart.</span></span>

1. <span data-ttu-id="11077-155">Close the device client sample output window on your machine.</span><span class="sxs-lookup"><span data-stu-id="11077-155">Close the device client sample output window on your machine.</span></span>
1. <span data-ttu-id="11077-156">Close the TPM simulator window on your machine.</span><span class="sxs-lookup"><span data-stu-id="11077-156">Close the TPM simulator window on your machine.</span></span>
1. <span data-ttu-id="11077-157">From the left-hand menu in the Azure portal, click **All resources** and then select your Device Provisioning service.</span><span class="sxs-lookup"><span data-stu-id="11077-157">From the left-hand menu in the Azure portal, click **All resources** and then select your Device Provisioning service.</span></span> <span data-ttu-id="11077-158">Open the **Manage Enrollments** blade for your service, and then click the **Individual Enrollments** tab. Select the *REGISTRATION ID* of the device you enrolled in this Quickstart, and click the **Delete** button at the top.</span><span class="sxs-lookup"><span data-stu-id="11077-158">Open the **Manage Enrollments** blade for your service, and then click the **Individual Enrollments** tab. Select the *REGISTRATION ID* of the device you enrolled in this Quickstart, and click the **Delete** button at the top.</span></span> 
1. <span data-ttu-id="11077-159">From the left-hand menu in the Azure portal, click **All resources** and then select your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="11077-159">From the left-hand menu in the Azure portal, click **All resources** and then select your IoT hub.</span></span> <span data-ttu-id="11077-160">Open the **IoT Devices** blade for your hub, select the *DEVICE ID* of the device you registered in this Quickstart, and then click **Delete** button at the top.</span><span class="sxs-lookup"><span data-stu-id="11077-160">Open the **IoT Devices** blade for your hub, select the *DEVICE ID* of the device you registered in this Quickstart, and then click **Delete** button at the top.</span></span>

## <a name="next-steps"></a><span data-ttu-id="11077-161">Next steps</span><span class="sxs-lookup"><span data-stu-id="11077-161">Next steps</span></span>

<span data-ttu-id="11077-162">In this Quickstart, you’ve created a TPM simulated device on your machine and provisioned it to your IoT hub using the IoT Hub Device Provisioning Service.</span><span class="sxs-lookup"><span data-stu-id="11077-162">In this Quickstart, you’ve created a TPM simulated device on your machine and provisioned it to your IoT hub using the IoT Hub Device Provisioning Service.</span></span> <span data-ttu-id="11077-163">To learn how to enroll your TPM device programmatically, continue to the Quickstart for programmatic enrollment of a TPM device.</span><span class="sxs-lookup"><span data-stu-id="11077-163">To learn how to enroll your TPM device programmatically, continue to the Quickstart for programmatic enrollment of a TPM device.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="11077-164">Azure Quickstart - Enroll TPM device to Azure IoT Hub Device Provisioning Service</span><span class="sxs-lookup"><span data-stu-id="11077-164">Azure Quickstart - Enroll TPM device to Azure IoT Hub Device Provisioning Service</span></span>](quick-enroll-device-tpm-java.md)
