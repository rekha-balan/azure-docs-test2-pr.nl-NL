---
title: Provision a simulated X.509 device to Azure IoT Hub using Java and enrollment groups | Microsoft Docs
description: Azure Tutorial - Create and provision a simulated X.509 device using Java device and service SDK and enrollment groups for IoT Hub Device Provisioning Service
author: wesmc7777
ms.author: wesmc
ms.date: 01/04/2018
ms.topic: tutorial
ms.service: iot-dps
services: iot-dps
manager: timlt
ms.devlang: java
ms.custom: mvc
ms.openlocfilehash: 7f51ac0e1137bf09c220c892e2c21b154f2f2433
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868670"
---
# <a name="create-and-provision-a-simulated-x509-device-using-java-device-and-service-sdk-and-group-enrollments-for-iot-hub-device-provisioning-service"></a><span data-ttu-id="190e4-103">Create and provision a simulated X.509 device using Java device and service SDK and group enrollments for IoT Hub Device Provisioning Service</span><span class="sxs-lookup"><span data-stu-id="190e4-103">Create and provision a simulated X.509 device using Java device and service SDK and group enrollments for IoT Hub Device Provisioning Service</span></span>

<span data-ttu-id="190e4-104">These steps show how to simulate an X.509 device on your development machine running Windows OS, and use a code sample to connect this simulated device with the Device Provisioning Service and your IoT hub using enrollment groups.</span><span class="sxs-lookup"><span data-stu-id="190e4-104">These steps show how to simulate an X.509 device on your development machine running Windows OS, and use a code sample to connect this simulated device with the Device Provisioning Service and your IoT hub using enrollment groups.</span></span> 

<span data-ttu-id="190e4-105">Make sure to complete the steps in the [Setup IoT Hub Device Provisioning Service with the Azure portal](./quick-setup-auto-provision.md) before you proceed.</span><span class="sxs-lookup"><span data-stu-id="190e4-105">Make sure to complete the steps in the [Setup IoT Hub Device Provisioning Service with the Azure portal](./quick-setup-auto-provision.md) before you proceed.</span></span>


## <a name="prepare-the-environment"></a><span data-ttu-id="190e4-106">Prepare the environment</span><span class="sxs-lookup"><span data-stu-id="190e4-106">Prepare the environment</span></span> 

1. <span data-ttu-id="190e4-107">Make sure you have [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) installed on your machine.</span><span class="sxs-lookup"><span data-stu-id="190e4-107">Make sure you have [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) installed on your machine.</span></span>

1. <span data-ttu-id="190e4-108">Download and install [Maven](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="190e4-108">Download and install [Maven](https://maven.apache.org/install.html).</span></span>

1. <span data-ttu-id="190e4-109">Make sure `git` is installed on your machine and is added to the environment variables accessible to the command window.</span><span class="sxs-lookup"><span data-stu-id="190e4-109">Make sure `git` is installed on your machine and is added to the environment variables accessible to the command window.</span></span> <span data-ttu-id="190e4-110">See [Software Freedom Conservancy's Git client tools](https://git-scm.com/download/) for the latest version of `git` tools to install, which includes the **Git Bash**, the command-line app that you can use to interact with your local Git repository.</span><span class="sxs-lookup"><span data-stu-id="190e4-110">See [Software Freedom Conservancy's Git client tools](https://git-scm.com/download/) for the latest version of `git` tools to install, which includes the **Git Bash**, the command-line app that you can use to interact with your local Git repository.</span></span> 

1. <span data-ttu-id="190e4-111">Use the following [Certifcate Overview](https://github.com/Azure/azure-iot-sdk-c/blob/master/tools/CACertificates/CACertificateOverview.md) to create your test certificates.</span><span class="sxs-lookup"><span data-stu-id="190e4-111">Use the following [Certifcate Overview](https://github.com/Azure/azure-iot-sdk-c/blob/master/tools/CACertificates/CACertificateOverview.md) to create your test certificates.</span></span>

    > [!NOTE]
    > <span data-ttu-id="190e4-112">This step requires [OpenSSL](https://www.openssl.org/), which can either be built and installed from source or downloaded and installed from a [3rd party](https://wiki.openssl.org/index.php/Binaries) such as [this](https://sourceforge.net/projects/openssl/).</span><span class="sxs-lookup"><span data-stu-id="190e4-112">This step requires [OpenSSL](https://www.openssl.org/), which can either be built and installed from source or downloaded and installed from a [3rd party](https://wiki.openssl.org/index.php/Binaries) such as [this](https://sourceforge.net/projects/openssl/).</span></span> <span data-ttu-id="190e4-113">If you have already created your _root_, _intermediate_ and _device_ certificates you may skip this step.</span><span class="sxs-lookup"><span data-stu-id="190e4-113">If you have already created your _root_, _intermediate_ and _device_ certificates you may skip this step.</span></span>
    >

    1. <span data-ttu-id="190e4-114">Run through the first two steps to create your _root_ and _intermediate_ certificates.</span><span class="sxs-lookup"><span data-stu-id="190e4-114">Run through the first two steps to create your _root_ and _intermediate_ certificates.</span></span>

    1. <span data-ttu-id="190e4-115">Log in to the Azure portal, click on the **All resources** button on the left-hand menu and open your provisioning service.</span><span class="sxs-lookup"><span data-stu-id="190e4-115">Log in to the Azure portal, click on the **All resources** button on the left-hand menu and open your provisioning service.</span></span>

        1. <span data-ttu-id="190e4-116">On the Device Provisioning Service summary blade, select **Certificates** and click the **Add** button at the top.</span><span class="sxs-lookup"><span data-stu-id="190e4-116">On the Device Provisioning Service summary blade, select **Certificates** and click the **Add** button at the top.</span></span>

        1. <span data-ttu-id="190e4-117">Under the **Add Certificate**, enter the following information:</span><span class="sxs-lookup"><span data-stu-id="190e4-117">Under the **Add Certificate**, enter the following information:</span></span>
            - <span data-ttu-id="190e4-118">Enter a unique certificate name.</span><span class="sxs-lookup"><span data-stu-id="190e4-118">Enter a unique certificate name.</span></span>
            - <span data-ttu-id="190e4-119">Select the **_RootCA.pem_** file you just created.</span><span class="sxs-lookup"><span data-stu-id="190e4-119">Select the **_RootCA.pem_** file you just created.</span></span>
            - <span data-ttu-id="190e4-120">Once complete, click the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="190e4-120">Once complete, click the **Save** button.</span></span>

        ![Add certificate](./media/tutorial-group-enrollments/add-certificate.png)

        1. <span data-ttu-id="190e4-122">Select the newly created certificate:</span><span class="sxs-lookup"><span data-stu-id="190e4-122">Select the newly created certificate:</span></span>
            - <span data-ttu-id="190e4-123">Click **Generate Verification Code**.</span><span class="sxs-lookup"><span data-stu-id="190e4-123">Click **Generate Verification Code**.</span></span> <span data-ttu-id="190e4-124">Copy the code generated.</span><span class="sxs-lookup"><span data-stu-id="190e4-124">Copy the code generated.</span></span>
            - <span data-ttu-id="190e4-125">Run the verification step.</span><span class="sxs-lookup"><span data-stu-id="190e4-125">Run the verification step.</span></span> <span data-ttu-id="190e4-126">Enter the _verification code_ or right-click to paste in your running PowerShell window.</span><span class="sxs-lookup"><span data-stu-id="190e4-126">Enter the _verification code_ or right-click to paste in your running PowerShell window.</span></span>  <span data-ttu-id="190e4-127">Press **Enter**.</span><span class="sxs-lookup"><span data-stu-id="190e4-127">Press **Enter**.</span></span>
            - <span data-ttu-id="190e4-128">Select the newly created **_verifyCert4.pem_** file in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="190e4-128">Select the newly created **_verifyCert4.pem_** file in the Azure portal.</span></span> <span data-ttu-id="190e4-129">Click **Verify**.</span><span class="sxs-lookup"><span data-stu-id="190e4-129">Click **Verify**.</span></span>

            ![Validate certificate](./media/tutorial-group-enrollments/validate-certificate.png)

    1. <span data-ttu-id="190e4-131">Finish by running the steps to create your device certificates and clean-up resources.</span><span class="sxs-lookup"><span data-stu-id="190e4-131">Finish by running the steps to create your device certificates and clean-up resources.</span></span>

    > [!NOTE]
    > <span data-ttu-id="190e4-132">When creating device certificates be sure to use only lower-case alphanumerics and hyphens in your device name.</span><span class="sxs-lookup"><span data-stu-id="190e4-132">When creating device certificates be sure to use only lower-case alphanumerics and hyphens in your device name.</span></span>
    >


## <a name="create-a-device-enrollment-entry"></a><span data-ttu-id="190e4-133">Create a device enrollment entry</span><span class="sxs-lookup"><span data-stu-id="190e4-133">Create a device enrollment entry</span></span>

1. <span data-ttu-id="190e4-134">Open a command prompt.</span><span class="sxs-lookup"><span data-stu-id="190e4-134">Open a command prompt.</span></span> <span data-ttu-id="190e4-135">Clone the GitHub repo for Java SDK code samples:</span><span class="sxs-lookup"><span data-stu-id="190e4-135">Clone the GitHub repo for Java SDK code samples:</span></span>
    
    ```cmd/sh
    git clone https://github.com/Azure/azure-iot-sdk-java.git --recursive
    ```

1. <span data-ttu-id="190e4-136">In the downloaded source code, navigate to the sample folder **_azure-iot-sdk-java/provisioning/provisioning-samples/service-enrollment-group-sample_**.</span><span class="sxs-lookup"><span data-stu-id="190e4-136">In the downloaded source code, navigate to the sample folder **_azure-iot-sdk-java/provisioning/provisioning-samples/service-enrollment-group-sample_**.</span></span> <span data-ttu-id="190e4-137">Open the file **_/src/main/java/samples/com/microsoft/azure/sdk/iot/ServiceEnrollmentGroupSample.java_** in an editor of your choice, and add the following details:</span><span class="sxs-lookup"><span data-stu-id="190e4-137">Open the file **_/src/main/java/samples/com/microsoft/azure/sdk/iot/ServiceEnrollmentGroupSample.java_** in an editor of your choice, and add the following details:</span></span>

    1. <span data-ttu-id="190e4-138">Add the `[Provisioning Connection String]` for your provisioning service, from the portal as following:</span><span class="sxs-lookup"><span data-stu-id="190e4-138">Add the `[Provisioning Connection String]` for your provisioning service, from the portal as following:</span></span>

        1. <span data-ttu-id="190e4-139">Navigate to your provisioning service in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="190e4-139">Navigate to your provisioning service in the [Azure portal](https://portal.azure.com).</span></span> 

        1. <span data-ttu-id="190e4-140">Open the **Shared access policies**, and select a policy which has the *EnrollmentWrite* permission.</span><span class="sxs-lookup"><span data-stu-id="190e4-140">Open the **Shared access policies**, and select a policy which has the *EnrollmentWrite* permission.</span></span>
    
        1. <span data-ttu-id="190e4-141">Copy the **Primary key connection string**.</span><span class="sxs-lookup"><span data-stu-id="190e4-141">Copy the **Primary key connection string**.</span></span> 

            ![Get the provisioning connection string from portal](./media/tutorial-group-enrollments/provisioning-string.png)  

        1. <span data-ttu-id="190e4-143">In the sample code file **_ServiceEnrollmentGroupSample.java_**, replace the `[Provisioning Connection String]` with the **Primary key connection string**.</span><span class="sxs-lookup"><span data-stu-id="190e4-143">In the sample code file **_ServiceEnrollmentGroupSample.java_**, replace the `[Provisioning Connection String]` with the **Primary key connection string**.</span></span>

            ```java
            private static final String PROVISIONING_CONNECTION_STRING = "[Provisioning Connection String]";
            ```

    1. <span data-ttu-id="190e4-144">Open the **_RootCA.pem_** file in a text editor.</span><span class="sxs-lookup"><span data-stu-id="190e4-144">Open the **_RootCA.pem_** file in a text editor.</span></span> <span data-ttu-id="190e4-145">Assign the value of the **Root Cert** to the parameter **PUBLIC_KEY_CERTIFICATE_STRING** as shown below:</span><span class="sxs-lookup"><span data-stu-id="190e4-145">Assign the value of the **Root Cert** to the parameter **PUBLIC_KEY_CERTIFICATE_STRING** as shown below:</span></span>

        ```java
        private static final String PUBLIC_KEY_CERTIFICATE_STRING =
                "-----BEGIN CERTIFICATE-----\n" +
                "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX\n" +
                "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX\n" +
                "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX\n" +
                "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX\n" +
                "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX\n" +
                "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX\n" +
                "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX\n" +
                "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX\n" +
                "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX\n" +
                "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX\n" +
                "-----END CERTIFICATE-----\n";
        ```
 
    1. <span data-ttu-id="190e4-146">Navigate to the IoT hub linked to your provisioning service in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="190e4-146">Navigate to the IoT hub linked to your provisioning service in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="190e4-147">Open the **Overview** tab for the hub, and copy the **Hostname**.</span><span class="sxs-lookup"><span data-stu-id="190e4-147">Open the **Overview** tab for the hub, and copy the **Hostname**.</span></span> <span data-ttu-id="190e4-148">Assign this **Hostname** to the *IOTHUB_HOST_NAME* parameter.</span><span class="sxs-lookup"><span data-stu-id="190e4-148">Assign this **Hostname** to the *IOTHUB_HOST_NAME* parameter.</span></span>

        ```java
        private static final String IOTHUB_HOST_NAME = "[Host name].azure-devices.net";
        ```

    1. <span data-ttu-id="190e4-149">Study the sample code.</span><span class="sxs-lookup"><span data-stu-id="190e4-149">Study the sample code.</span></span> <span data-ttu-id="190e4-150">It creates, updates, queries and deletes a group enrollment for X.509 devices.</span><span class="sxs-lookup"><span data-stu-id="190e4-150">It creates, updates, queries and deletes a group enrollment for X.509 devices.</span></span> <span data-ttu-id="190e4-151">To verify successful enrollment in portal, temporarily comment out the following lines of code at the end of the _ServiceEnrollmentGroupSample.java_ file:</span><span class="sxs-lookup"><span data-stu-id="190e4-151">To verify successful enrollment in portal, temporarily comment out the following lines of code at the end of the _ServiceEnrollmentGroupSample.java_ file:</span></span>

        ```java
        // ************************************** Delete info of enrollmentGroup ***************************************
        System.out.println("\nDelete the enrollmentGroup...");
        provisioningServiceClient.deleteEnrollmentGroup(enrollmentGroupId);
        ```

    1. <span data-ttu-id="190e4-152">Save the file _ServiceEnrollmentGroupSample.java_.</span><span class="sxs-lookup"><span data-stu-id="190e4-152">Save the file _ServiceEnrollmentGroupSample.java_.</span></span> 

1. <span data-ttu-id="190e4-153">Open a command window, and navigate to the folder **_azure-iot-sdk-java/provisioning/provisioning-samples/service-enrollment-group-sample_**.</span><span class="sxs-lookup"><span data-stu-id="190e4-153">Open a command window, and navigate to the folder **_azure-iot-sdk-java/provisioning/provisioning-samples/service-enrollment-group-sample_**.</span></span>

1. <span data-ttu-id="190e4-154">Build the sample code by using this command:</span><span class="sxs-lookup"><span data-stu-id="190e4-154">Build the sample code by using this command:</span></span>

    ```cmd\sh
    mvn install -DskipTests
    ```

1. <span data-ttu-id="190e4-155">Run the sample by using these commands at the command window:</span><span class="sxs-lookup"><span data-stu-id="190e4-155">Run the sample by using these commands at the command window:</span></span>

    ```cmd\sh
    cd target
    java -jar ./service-enrollment-group-sample-{version}-with-deps.jar
    ```

1. <span data-ttu-id="190e4-156">Observe the output window for successful enrollment.</span><span class="sxs-lookup"><span data-stu-id="190e4-156">Observe the output window for successful enrollment.</span></span>

    ![Successful enrollment](./media/tutorial-group-enrollments/enrollment.png) 

1. <span data-ttu-id="190e4-158">Navigate to your provisioning service in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="190e4-158">Navigate to your provisioning service in the Azure portal.</span></span> <span data-ttu-id="190e4-159">Click **Manage enrollments**.</span><span class="sxs-lookup"><span data-stu-id="190e4-159">Click **Manage enrollments**.</span></span> <span data-ttu-id="190e4-160">Notice that your group of X.509 devices appears under the **Enrollment Groups** tab, with an auto-generated *GROUP NAME*.</span><span class="sxs-lookup"><span data-stu-id="190e4-160">Notice that your group of X.509 devices appears under the **Enrollment Groups** tab, with an auto-generated *GROUP NAME*.</span></span> 


## <a name="simulate-the-device"></a><span data-ttu-id="190e4-161">Simulate the device</span><span class="sxs-lookup"><span data-stu-id="190e4-161">Simulate the device</span></span>

1. <span data-ttu-id="190e4-162">On the Device Provisioning Service summary blade, select **Overview** and note your _Id Scope_ and _Provisioning Service Global Endpoint_.</span><span class="sxs-lookup"><span data-stu-id="190e4-162">On the Device Provisioning Service summary blade, select **Overview** and note your _Id Scope_ and _Provisioning Service Global Endpoint_.</span></span>

    ![Service information](./media/tutorial-group-enrollments/extract-dps-endpoints.png)

1. <span data-ttu-id="190e4-164">Open a command prompt.</span><span class="sxs-lookup"><span data-stu-id="190e4-164">Open a command prompt.</span></span> <span data-ttu-id="190e4-165">Navigate to the sample project folder.</span><span class="sxs-lookup"><span data-stu-id="190e4-165">Navigate to the sample project folder.</span></span>

    ```cmd/sh
    cd azure-iot-sdk-java/provisioning/provisioning-samples/provisioning-X509-sample
    ```

1. <span data-ttu-id="190e4-166">Enter the enrollment group information in the following way:</span><span class="sxs-lookup"><span data-stu-id="190e4-166">Enter the enrollment group information in the following way:</span></span>

    - <span data-ttu-id="190e4-167">Edit `/src/main/java/samples/com/microsoft/azure/sdk/iot/ProvisioningX509Sample.java` to include your _Id Scope_ and _Provisioning Service Global Endpoint_ as noted before.</span><span class="sxs-lookup"><span data-stu-id="190e4-167">Edit `/src/main/java/samples/com/microsoft/azure/sdk/iot/ProvisioningX509Sample.java` to include your _Id Scope_ and _Provisioning Service Global Endpoint_ as noted before.</span></span> <span data-ttu-id="190e4-168">Open your **_{deviceName}-public.pem_** file and include this value as your _Client Cert_. Open your **_{deviceName}-all.pem_** file and copy the text from _-----BEGIN PRIVATE KEY-----_ to _-----END PRIVATE KEY-----_.</span><span class="sxs-lookup"><span data-stu-id="190e4-168">Open your **_{deviceName}-public.pem_** file and include this value as your _Client Cert_. Open your **_{deviceName}-all.pem_** file and copy the text from _-----BEGIN PRIVATE KEY-----_ to _-----END PRIVATE KEY-----_.</span></span>  <span data-ttu-id="190e4-169">Use this as your _Client Cert Private Key_.</span><span class="sxs-lookup"><span data-stu-id="190e4-169">Use this as your _Client Cert Private Key_.</span></span>

        ```java
        private static final String idScope = "[Your ID scope here]";
        private static final String globalEndpoint = "[Your Provisioning Service Global Endpoint here]";
        private static final ProvisioningDeviceClientTransportProtocol PROVISIONING_DEVICE_CLIENT_TRANSPORT_PROTOCOL = ProvisioningDeviceClientTransportProtocol.HTTPS;
        private static final String leafPublicPem = "<Your Public PEM Certificate here>";
        private static final String leafPrivateKey = "<Your Private PEM Key here>";
        ```

        - <span data-ttu-id="190e4-170">Use the following format for including your certificate and key:</span><span class="sxs-lookup"><span data-stu-id="190e4-170">Use the following format for including your certificate and key:</span></span>
            
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

1. <span data-ttu-id="190e4-171">Build the sample.</span><span class="sxs-lookup"><span data-stu-id="190e4-171">Build the sample.</span></span> <span data-ttu-id="190e4-172">Navigate to the target folder and execute the created jar file.</span><span class="sxs-lookup"><span data-stu-id="190e4-172">Navigate to the target folder and execute the created jar file.</span></span>

    ```cmd/sh
    mvn clean install
    cd target
    java -jar ./provisioning-x509-sample-{version}-with-deps.jar
    ```

    ![Successful registration](./media/tutorial-group-enrollments/registration.png)

1. <span data-ttu-id="190e4-174">In the portal, navigate to the IoT hub linked to your provisioning service and open the **Device Explorer** blade.</span><span class="sxs-lookup"><span data-stu-id="190e4-174">In the portal, navigate to the IoT hub linked to your provisioning service and open the **Device Explorer** blade.</span></span> <span data-ttu-id="190e4-175">On successful provisioning of the simulated X.509 device to the hub, its device ID appears on the **Device Explorer** blade, with *STATUS* as **enabled**.</span><span class="sxs-lookup"><span data-stu-id="190e4-175">On successful provisioning of the simulated X.509 device to the hub, its device ID appears on the **Device Explorer** blade, with *STATUS* as **enabled**.</span></span> <span data-ttu-id="190e4-176">Note that you might need to click the **Refresh** button at the top if you already opened the blade prior to running the sample device application.</span><span class="sxs-lookup"><span data-stu-id="190e4-176">Note that you might need to click the **Refresh** button at the top if you already opened the blade prior to running the sample device application.</span></span> 

    ![Device is registered with the IoT hub](./media/tutorial-group-enrollments/hub-registration.png) 


## <a name="clean-up-resources"></a><span data-ttu-id="190e4-178">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="190e4-178">Clean up resources</span></span>

<span data-ttu-id="190e4-179">If you plan to continue working on and exploring the device client sample, do not clean up the resources created in this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="190e4-179">If you plan to continue working on and exploring the device client sample, do not clean up the resources created in this Quickstart.</span></span> <span data-ttu-id="190e4-180">If you do not plan to continue, use the following steps to delete all resources created by this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="190e4-180">If you do not plan to continue, use the following steps to delete all resources created by this Quickstart.</span></span>

1. <span data-ttu-id="190e4-181">Close the device client sample output window on your machine.</span><span class="sxs-lookup"><span data-stu-id="190e4-181">Close the device client sample output window on your machine.</span></span>
1. <span data-ttu-id="190e4-182">From the left-hand menu in the Azure portal, click **All resources** and then select your Device Provisioning service.</span><span class="sxs-lookup"><span data-stu-id="190e4-182">From the left-hand menu in the Azure portal, click **All resources** and then select your Device Provisioning service.</span></span> <span data-ttu-id="190e4-183">Open the **Manage Enrollments** blade for your service, and then click the **Individual Enrollments** tab. Select the *REGISTRATION ID* of the device you enrolled in this Quickstart, and click the **Delete** button at the top.</span><span class="sxs-lookup"><span data-stu-id="190e4-183">Open the **Manage Enrollments** blade for your service, and then click the **Individual Enrollments** tab. Select the *REGISTRATION ID* of the device you enrolled in this Quickstart, and click the **Delete** button at the top.</span></span> 
1. <span data-ttu-id="190e4-184">From the left-hand menu in the Azure portal, click **All resources** and then select your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="190e4-184">From the left-hand menu in the Azure portal, click **All resources** and then select your IoT hub.</span></span> <span data-ttu-id="190e4-185">Open the **IoT Devices** blade for your hub, select the *DEVICE ID* of the device you registered in this Quickstart, and then click **Delete** button at the top.</span><span class="sxs-lookup"><span data-stu-id="190e4-185">Open the **IoT Devices** blade for your hub, select the *DEVICE ID* of the device you registered in this Quickstart, and then click **Delete** button at the top.</span></span>


## <a name="next-steps"></a><span data-ttu-id="190e4-186">Next steps</span><span class="sxs-lookup"><span data-stu-id="190e4-186">Next steps</span></span>

<span data-ttu-id="190e4-187">In this tutorial, you’ve created a simulated X.509 device on your Windows machine and provisioned it to your IoT hub using the Azure IoT Hub Device Provisioning Service and enrollment groups.</span><span class="sxs-lookup"><span data-stu-id="190e4-187">In this tutorial, you’ve created a simulated X.509 device on your Windows machine and provisioned it to your IoT hub using the Azure IoT Hub Device Provisioning Service and enrollment groups.</span></span> <span data-ttu-id="190e4-188">To learn more about your X.509 device, continue to device concepts.</span><span class="sxs-lookup"><span data-stu-id="190e4-188">To learn more about your X.509 device, continue to device concepts.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="190e4-189">IoT Hub Device Provisioning Service device concepts</span><span class="sxs-lookup"><span data-stu-id="190e4-189">IoT Hub Device Provisioning Service device concepts</span></span>](concepts-device.md)
