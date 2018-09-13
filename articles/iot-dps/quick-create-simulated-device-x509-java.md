---
title: Provision a simulated X.509 device to Azure IoT Hub using Java | Microsoft Docs
description: Azure Quickstart - Create and provision a simulated X.509 device using Java device SDK for IoT Hub Device Provisioning Service
author: wesmc7777
ms.author: wesmc
ms.date: 04/09/2018
ms.topic: quickstart
ms.service: iot-dps
services: iot-dps
manager: timlt
ms.devlang: java
ms.custom: mvc
ms.openlocfilehash: 0c5eefbd6d7758ad2a7640a1fbff3435fcd1d315
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869654"
---
# <a name="create-and-provision-a-simulated-x509-device-using-java-device-sdk-for-iot-hub-device-provisioning-service"></a><span data-ttu-id="432f1-103">Create and provision a simulated X.509 device using Java device SDK for IoT Hub Device Provisioning Service</span><span class="sxs-lookup"><span data-stu-id="432f1-103">Create and provision a simulated X.509 device using Java device SDK for IoT Hub Device Provisioning Service</span></span>
[!INCLUDE [iot-dps-selector-quick-create-simulated-device-x509](../../includes/iot-dps-selector-quick-create-simulated-device-x509.md)]

<span data-ttu-id="432f1-104">These steps show how to simulate an X.509 device on your development machine running Windows OS, and use a code sample to connect this simulated device with the Device Provisioning Service and your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="432f1-104">These steps show how to simulate an X.509 device on your development machine running Windows OS, and use a code sample to connect this simulated device with the Device Provisioning Service and your IoT hub.</span></span> 

<span data-ttu-id="432f1-105">If you're unfamiliar with the process of auto-provisioning, be sure to also review [Auto-provisioning concepts](concepts-auto-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="432f1-105">If you're unfamiliar with the process of auto-provisioning, be sure to also review [Auto-provisioning concepts](concepts-auto-provisioning.md).</span></span> <span data-ttu-id="432f1-106">Also make sure you've completed the steps in [Set up IoT Hub Device Provisioning Service with the Azure portal](./quick-setup-auto-provision.md) before continuing.</span><span class="sxs-lookup"><span data-stu-id="432f1-106">Also make sure you've completed the steps in [Set up IoT Hub Device Provisioning Service with the Azure portal](./quick-setup-auto-provision.md) before continuing.</span></span> 

## <a name="prepare-the-environment"></a><span data-ttu-id="432f1-107">Prepare the environment</span><span class="sxs-lookup"><span data-stu-id="432f1-107">Prepare the environment</span></span> 

1. <span data-ttu-id="432f1-108">Make sure you have [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) installed on your machine.</span><span class="sxs-lookup"><span data-stu-id="432f1-108">Make sure you have [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) installed on your machine.</span></span>

2. <span data-ttu-id="432f1-109">Download and install [Maven](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="432f1-109">Download and install [Maven](https://maven.apache.org/install.html).</span></span>

3. <span data-ttu-id="432f1-110">Make sure Git is installed on your machine and is added to the environment variables accessible to the command window.</span><span class="sxs-lookup"><span data-stu-id="432f1-110">Make sure Git is installed on your machine and is added to the environment variables accessible to the command window.</span></span> <span data-ttu-id="432f1-111">See [Software Freedom Conservancy's Git client tools](https://git-scm.com/download/) for the latest version of `git` tools to install, which includes the **Git Bash**, the command-line app that you can use to interact with your local Git repository.</span><span class="sxs-lookup"><span data-stu-id="432f1-111">See [Software Freedom Conservancy's Git client tools](https://git-scm.com/download/) for the latest version of `git` tools to install, which includes the **Git Bash**, the command-line app that you can use to interact with your local Git repository.</span></span> 

4. <span data-ttu-id="432f1-112">Open a command prompt.</span><span class="sxs-lookup"><span data-stu-id="432f1-112">Open a command prompt.</span></span> <span data-ttu-id="432f1-113">Clone the GitHub repo for device simulation code sample:</span><span class="sxs-lookup"><span data-stu-id="432f1-113">Clone the GitHub repo for device simulation code sample:</span></span>
    
    ```cmd/sh
    git clone https://github.com/Azure/azure-iot-sdk-java.git --recursive
    ```
5. <span data-ttu-id="432f1-114">Navigate to the root `azure-iot-sdk-`java\` directory and build the project to download all needed packages.</span><span class="sxs-lookup"><span data-stu-id="432f1-114">Navigate to the root `azure-iot-sdk-`java\` directory and build the project to download all needed packages.</span></span>
   
   ```cmd/sh
   cd azure-iot-sdk-java
   mvn install -DskipTests=true
   ```
6. <span data-ttu-id="432f1-115">Navigate to the certificate generator project and build the project.</span><span class="sxs-lookup"><span data-stu-id="432f1-115">Navigate to the certificate generator project and build the project.</span></span> 

    ```cmd/sh
    cd azure-iot-sdk-java/provisioning/provisioning-tools/provisioning-x509-cert-generator
    mvn clean install
    ```

## <a name="create-a-self-signed-x509-device-certificate-and-individual-enrollment-entry"></a><span data-ttu-id="432f1-116">Create a self-signed X.509 device certificate and individual enrollment entry</span><span class="sxs-lookup"><span data-stu-id="432f1-116">Create a self-signed X.509 device certificate and individual enrollment entry</span></span>

<span data-ttu-id="432f1-117">In this section you, will use a self-signed X.509 certificate, it is important to keep in mind the following:</span><span class="sxs-lookup"><span data-stu-id="432f1-117">In this section you, will use a self-signed X.509 certificate, it is important to keep in mind the following:</span></span>

* <span data-ttu-id="432f1-118">Self-signed certificates are for testing only, and should not to be used in production.</span><span class="sxs-lookup"><span data-stu-id="432f1-118">Self-signed certificates are for testing only, and should not to be used in production.</span></span>
* <span data-ttu-id="432f1-119">The default expiration date for a self-signed certificate is 1 year.</span><span class="sxs-lookup"><span data-stu-id="432f1-119">The default expiration date for a self-signed certificate is 1 year.</span></span>

<span data-ttu-id="432f1-120">You will use sample code from the [Azure IoT SDK for Java](https://github.com/Azure/azure-iot-sdk-java.git) to create the certificate to be used with the individual enrollment entry for the simulated device.</span><span class="sxs-lookup"><span data-stu-id="432f1-120">You will use sample code from the [Azure IoT SDK for Java](https://github.com/Azure/azure-iot-sdk-java.git) to create the certificate to be used with the individual enrollment entry for the simulated device.</span></span>


1. <span data-ttu-id="432f1-121">Using the command prompt from previous steps, navigate to the `target` folder, then execute the jar file created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="432f1-121">Using the command prompt from previous steps, navigate to the `target` folder, then execute the jar file created in the previous step.</span></span>

    ```cmd/sh
    cd target
    java -jar ./provisioning-x509-cert-generator-{version}-with-deps.jar
    ```

2. <span data-ttu-id="432f1-122">Enter **N** for _Do you want to input common name_.</span><span class="sxs-lookup"><span data-stu-id="432f1-122">Enter **N** for _Do you want to input common name_.</span></span> <span data-ttu-id="432f1-123">Copy to the clipboard the output of `Client Cert`, starting from *-----BEGIN CERTIFICATE-----* through *-----END CERTIFICATE-----*.</span><span class="sxs-lookup"><span data-stu-id="432f1-123">Copy to the clipboard the output of `Client Cert`, starting from *-----BEGIN CERTIFICATE-----* through *-----END CERTIFICATE-----*.</span></span>

   ![Individual certificate generator](./media/java-quick-create-simulated-device-x509/individual.png)

3. <span data-ttu-id="432f1-125">Create a file named **_X509individual.pem_** on your Windows machine, open it in an editor of your choice, and copy the clipboard contents to this file.</span><span class="sxs-lookup"><span data-stu-id="432f1-125">Create a file named **_X509individual.pem_** on your Windows machine, open it in an editor of your choice, and copy the clipboard contents to this file.</span></span> <span data-ttu-id="432f1-126">Save the file and close your editor.</span><span class="sxs-lookup"><span data-stu-id="432f1-126">Save the file and close your editor.</span></span>

4. <span data-ttu-id="432f1-127">In the command prompt, enter **N** for _Do you want to input Verification Code_ and keep the program output open for reference later in the Quickstart.</span><span class="sxs-lookup"><span data-stu-id="432f1-127">In the command prompt, enter **N** for _Do you want to input Verification Code_ and keep the program output open for reference later in the Quickstart.</span></span> <span data-ttu-id="432f1-128">Later you copy the `Client Cert` and `Client Cert Private Key` values, for use in the next section.</span><span class="sxs-lookup"><span data-stu-id="432f1-128">Later you copy the `Client Cert` and `Client Cert Private Key` values, for use in the next section.</span></span>

5. <span data-ttu-id="432f1-129">Sign in to the [Azure portal](https://portal.azure.com), click on the **All resources** button on the left-hand menu and open your Device Provisioning Service instance.</span><span class="sxs-lookup"><span data-stu-id="432f1-129">Sign in to the [Azure portal](https://portal.azure.com), click on the **All resources** button on the left-hand menu and open your Device Provisioning Service instance.</span></span>

6. <span data-ttu-id="432f1-130">On the Device Provisioning Service summary blade, select **Manage enrollments**.</span><span class="sxs-lookup"><span data-stu-id="432f1-130">On the Device Provisioning Service summary blade, select **Manage enrollments**.</span></span> <span data-ttu-id="432f1-131">Select **Individual Enrollments** tab and click the **Add** button at the top.</span><span class="sxs-lookup"><span data-stu-id="432f1-131">Select **Individual Enrollments** tab and click the **Add** button at the top.</span></span> 

7. <span data-ttu-id="432f1-132">Under the **Add enrollment** panel, enter the following information:</span><span class="sxs-lookup"><span data-stu-id="432f1-132">Under the **Add enrollment** panel, enter the following information:</span></span>
    - <span data-ttu-id="432f1-133">Select **X.509** as the identity attestation *Mechanism*.</span><span class="sxs-lookup"><span data-stu-id="432f1-133">Select **X.509** as the identity attestation *Mechanism*.</span></span>
    - <span data-ttu-id="432f1-134">Under the *Primary certificate .pem or .cer file*, click *Select a file* to select the certificate file **X509individual.pem** created in the previous steps.</span><span class="sxs-lookup"><span data-stu-id="432f1-134">Under the *Primary certificate .pem or .cer file*, click *Select a file* to select the certificate file **X509individual.pem** created in the previous steps.</span></span>  
    - <span data-ttu-id="432f1-135">Optionally, you may provide the following information:</span><span class="sxs-lookup"><span data-stu-id="432f1-135">Optionally, you may provide the following information:</span></span>
      - <span data-ttu-id="432f1-136">Select an IoT hub linked with your provisioning service.</span><span class="sxs-lookup"><span data-stu-id="432f1-136">Select an IoT hub linked with your provisioning service.</span></span>
      - <span data-ttu-id="432f1-137">Enter a unique device ID.</span><span class="sxs-lookup"><span data-stu-id="432f1-137">Enter a unique device ID.</span></span> <span data-ttu-id="432f1-138">Make sure to avoid sensitive data while naming your device.</span><span class="sxs-lookup"><span data-stu-id="432f1-138">Make sure to avoid sensitive data while naming your device.</span></span> 
      - <span data-ttu-id="432f1-139">Update the **Initial device twin state** with the desired initial configuration for the device.</span><span class="sxs-lookup"><span data-stu-id="432f1-139">Update the **Initial device twin state** with the desired initial configuration for the device.</span></span>
   - <span data-ttu-id="432f1-140">Once complete, click the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="432f1-140">Once complete, click the **Save** button.</span></span> 

    <span data-ttu-id="432f1-141">[![Add individual enrollment for X.509 attestation in the portal](./media/quick-create-simulated-device-x509-csharp/individual-enrollment.png)](./media/how-to-manage-enrollments/individual-enrollment.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="432f1-141">[![Add individual enrollment for X.509 attestation in the portal](./media/quick-create-simulated-device-x509-csharp/individual-enrollment.png)](./media/how-to-manage-enrollments/individual-enrollment.png#lightbox)</span></span>

     <span data-ttu-id="432f1-142">Upon successful enrollment, your X.509 device appears as **microsoftriotcore** under the *Registration ID* column in the *Individual Enrollments* tab.</span><span class="sxs-lookup"><span data-stu-id="432f1-142">Upon successful enrollment, your X.509 device appears as **microsoftriotcore** under the *Registration ID* column in the *Individual Enrollments* tab.</span></span> 



## <a name="simulate-the-device"></a><span data-ttu-id="432f1-143">Simulate the device</span><span class="sxs-lookup"><span data-stu-id="432f1-143">Simulate the device</span></span>

1. <span data-ttu-id="432f1-144">On the Device Provisioning Service summary blade, select **Overview** and note your _Id Scope_ and _Provisioning Service Global Endpoint_.</span><span class="sxs-lookup"><span data-stu-id="432f1-144">On the Device Provisioning Service summary blade, select **Overview** and note your _Id Scope_ and _Provisioning Service Global Endpoint_.</span></span>

    ![Service information](./media/java-quick-create-simulated-device-x509/extract-dps-endpoints.png)

2. <span data-ttu-id="432f1-146">Open a command prompt.</span><span class="sxs-lookup"><span data-stu-id="432f1-146">Open a command prompt.</span></span> <span data-ttu-id="432f1-147">Navigate to the sample project folder of the Java SDK repository.</span><span class="sxs-lookup"><span data-stu-id="432f1-147">Navigate to the sample project folder of the Java SDK repository.</span></span>

    ```cmd/sh
    cd azure-iot-sdk-java/provisioning/provisioning-samples/provisioning-X509-sample
    ```

3. <span data-ttu-id="432f1-148">Enter the provisioning service and X.509 identity information in your code.</span><span class="sxs-lookup"><span data-stu-id="432f1-148">Enter the provisioning service and X.509 identity information in your code.</span></span> <span data-ttu-id="432f1-149">This is used during auto-provisioning, for attestation of the simulated device, prior to device registration:</span><span class="sxs-lookup"><span data-stu-id="432f1-149">This is used during auto-provisioning, for attestation of the simulated device, prior to device registration:</span></span>

   - <span data-ttu-id="432f1-150">Edit the file `/src/main/java/samples/com/microsoft/azure/sdk/iot/ProvisioningX509Sample.java`, to include your _Id Scope_ and _Provisioning Service Global Endpoint_ as noted previously.</span><span class="sxs-lookup"><span data-stu-id="432f1-150">Edit the file `/src/main/java/samples/com/microsoft/azure/sdk/iot/ProvisioningX509Sample.java`, to include your _Id Scope_ and _Provisioning Service Global Endpoint_ as noted previously.</span></span> <span data-ttu-id="432f1-151">Also include _Client Cert_ and _Client Cert Private Key_ as noted in the previous section.</span><span class="sxs-lookup"><span data-stu-id="432f1-151">Also include _Client Cert_ and _Client Cert Private Key_ as noted in the previous section.</span></span>

      ```java
      private static final String idScope = "[Your ID scope here]";
      private static final String globalEndpoint = "[Your Provisioning Service Global Endpoint here]";
      private static final ProvisioningDeviceClientTransportProtocol PROVISIONING_DEVICE_CLIENT_TRANSPORT_PROTOCOL = ProvisioningDeviceClientTransportProtocol.HTTPS;
      private static final String leafPublicPem = "<Your Public PEM Certificate here>";
      private static final String leafPrivateKey = "<Your Private PEM Key here>";
      ```

   - <span data-ttu-id="432f1-152">Use the following format when copying/pasting your certificate and private key:</span><span class="sxs-lookup"><span data-stu-id="432f1-152">Use the following format when copying/pasting your certificate and private key:</span></span>
        
      ```java
      private static final String leafPublicPem = "-----BEGIN CERTIFICATE-----\n" +
        "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX\n" +
        "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX\n" +
        "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX\n" +
        "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX\n" +
        "+XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX\n" +
        "-----END CERTIFICATE-----\n";
      private static final String leafPrivateKey = "-----BEGIN PRIVATE KEY-----\n" +
            "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX\n" +
            "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX\n" +
            "XXXXXXXXXX\n" +
            "-----END PRIVATE KEY-----\n";
      ```

4. <span data-ttu-id="432f1-153">Build the sample.</span><span class="sxs-lookup"><span data-stu-id="432f1-153">Build the sample.</span></span> <span data-ttu-id="432f1-154">Navigate to the `target` folder and execute the created jar file.</span><span class="sxs-lookup"><span data-stu-id="432f1-154">Navigate to the `target` folder and execute the created jar file.</span></span>

    ```cmd/sh
    mvn clean install
    cd target
    java -jar ./provisioning-x509-sample-{version}-with-deps.jar
    ```

5. <span data-ttu-id="432f1-155">In the Azure portal, navigate to the IoT hub linked to your provisioning service and open the **Device Explorer** blade.</span><span class="sxs-lookup"><span data-stu-id="432f1-155">In the Azure portal, navigate to the IoT hub linked to your provisioning service and open the **Device Explorer** blade.</span></span> <span data-ttu-id="432f1-156">Upon successful provisioning of the simulated X.509 device to the hub, its device ID appears on the **Device Explorer** blade, with *STATUS* as **enabled**.</span><span class="sxs-lookup"><span data-stu-id="432f1-156">Upon successful provisioning of the simulated X.509 device to the hub, its device ID appears on the **Device Explorer** blade, with *STATUS* as **enabled**.</span></span>  <span data-ttu-id="432f1-157">You might need to click the **Refresh** button at the top if you already opened the blade prior to running the sample device application.</span><span class="sxs-lookup"><span data-stu-id="432f1-157">You might need to click the **Refresh** button at the top if you already opened the blade prior to running the sample device application.</span></span> 

    ![Device is registered with the IoT hub](./media/java-quick-create-simulated-device-x509/hub-registration.png) 

> [!NOTE]
> <span data-ttu-id="432f1-159">If you changed the *initial device twin state* from the default value in the enrollment entry for your device, it can pull the desired twin state from the hub and act accordingly.</span><span class="sxs-lookup"><span data-stu-id="432f1-159">If you changed the *initial device twin state* from the default value in the enrollment entry for your device, it can pull the desired twin state from the hub and act accordingly.</span></span> <span data-ttu-id="432f1-160">For more information, see [Understand and use device twins in IoT Hub](../iot-hub/iot-hub-devguide-device-twins.md).</span><span class="sxs-lookup"><span data-stu-id="432f1-160">For more information, see [Understand and use device twins in IoT Hub](../iot-hub/iot-hub-devguide-device-twins.md).</span></span>
>


## <a name="clean-up-resources"></a><span data-ttu-id="432f1-161">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="432f1-161">Clean up resources</span></span>

<span data-ttu-id="432f1-162">If you plan to continue working on and exploring the device client sample, do not clean up the resources created in this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="432f1-162">If you plan to continue working on and exploring the device client sample, do not clean up the resources created in this Quickstart.</span></span> <span data-ttu-id="432f1-163">If you do not plan to continue, use the following steps to delete all resources created by this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="432f1-163">If you do not plan to continue, use the following steps to delete all resources created by this Quickstart.</span></span>

1. <span data-ttu-id="432f1-164">Close the device client sample output window on your machine.</span><span class="sxs-lookup"><span data-stu-id="432f1-164">Close the device client sample output window on your machine.</span></span>
2. <span data-ttu-id="432f1-165">From the left-hand menu in the Azure portal, click **All resources** and then select your Device Provisioning service.</span><span class="sxs-lookup"><span data-stu-id="432f1-165">From the left-hand menu in the Azure portal, click **All resources** and then select your Device Provisioning service.</span></span> <span data-ttu-id="432f1-166">Open the **Manage Enrollments** blade for your service, and then click the **Individual Enrollments** tab. Select the *REGISTRATION ID* of the device you enrolled in this Quickstart, and click the **Delete** button at the top.</span><span class="sxs-lookup"><span data-stu-id="432f1-166">Open the **Manage Enrollments** blade for your service, and then click the **Individual Enrollments** tab. Select the *REGISTRATION ID* of the device you enrolled in this Quickstart, and click the **Delete** button at the top.</span></span> 
3. <span data-ttu-id="432f1-167">From the left-hand menu in the Azure portal, click **All resources** and then select your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="432f1-167">From the left-hand menu in the Azure portal, click **All resources** and then select your IoT hub.</span></span> <span data-ttu-id="432f1-168">Open the **IoT Devices** blade for your hub, select the *DEVICE ID* of the device you registered in this Quickstart, and then click **Delete** button at the top.</span><span class="sxs-lookup"><span data-stu-id="432f1-168">Open the **IoT Devices** blade for your hub, select the *DEVICE ID* of the device you registered in this Quickstart, and then click **Delete** button at the top.</span></span>


## <a name="next-steps"></a><span data-ttu-id="432f1-169">Next steps</span><span class="sxs-lookup"><span data-stu-id="432f1-169">Next steps</span></span>

<span data-ttu-id="432f1-170">In this Quickstart, you created a simulated X.509 device on your Windows machine.</span><span class="sxs-lookup"><span data-stu-id="432f1-170">In this Quickstart, you created a simulated X.509 device on your Windows machine.</span></span> <span data-ttu-id="432f1-171">You configured its enrollment in your Azure IoT Hub Device Provisioning Service, then auto-provisioned the device to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="432f1-171">You configured its enrollment in your Azure IoT Hub Device Provisioning Service, then auto-provisioned the device to your IoT hub.</span></span> <span data-ttu-id="432f1-172">To learn how to enroll your X.509 device programmatically, continue to the Quickstart for programmatic enrollment of X.509 devices.</span><span class="sxs-lookup"><span data-stu-id="432f1-172">To learn how to enroll your X.509 device programmatically, continue to the Quickstart for programmatic enrollment of X.509 devices.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="432f1-173">Azure Quickstart - Enroll X.509 devices to Azure IoT Hub Device Provisioning Service</span><span class="sxs-lookup"><span data-stu-id="432f1-173">Azure Quickstart - Enroll X.509 devices to Azure IoT Hub Device Provisioning Service</span></span>](quick-enroll-device-x509-java.md)
