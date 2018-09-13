---
title: This quickstart shows you how to enroll X.509 devices to the Azure Device Provisioning Service using Java | Microsoft Docs
description: In this quickstart, you will enroll X.509 devices to the Azure IoT Hub Device Provisioning Service using Java
author: wesmc7777
ms.author: wesmc
ms.date: 12/20/2017
ms.topic: quickstart
ms.service: iot-dps
services: iot-dps
manager: timlt
ms.devlang: java
ms.custom: mvc
ms.openlocfilehash: 505aee35c839a0224ca158d918fc5e54dc6e0f28
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856505"
---
# <a name="quickstart-enroll-x509-devices-to-the-device-provisioning-service-using-java"></a><span data-ttu-id="0e480-103">Quickstart: Enroll X.509 devices to the Device Provisioning Service using Java</span><span class="sxs-lookup"><span data-stu-id="0e480-103">Quickstart: Enroll X.509 devices to the Device Provisioning Service using Java</span></span>

[!INCLUDE [iot-dps-selector-quick-enroll-device-x509](../../includes/iot-dps-selector-quick-enroll-device-x509.md)]

<span data-ttu-id="0e480-104">This quickstart shows how to use Java to programmatically enroll a group of X.509 simulated devices to the Azure IoT Hub Device Provisioning Service.</span><span class="sxs-lookup"><span data-stu-id="0e480-104">This quickstart shows how to use Java to programmatically enroll a group of X.509 simulated devices to the Azure IoT Hub Device Provisioning Service.</span></span> <span data-ttu-id="0e480-105">Devices are enrolled to a provisioning service instance by creating an [Enrollment group](concepts-service.md#enrollment-group), or an [Individual enrollment](concepts-service.md#individual-enrollment).</span><span class="sxs-lookup"><span data-stu-id="0e480-105">Devices are enrolled to a provisioning service instance by creating an [Enrollment group](concepts-service.md#enrollment-group), or an [Individual enrollment](concepts-service.md#individual-enrollment).</span></span> <span data-ttu-id="0e480-106">This quickstart shows how to create both types of enrollments.</span><span class="sxs-lookup"><span data-stu-id="0e480-106">This quickstart shows how to create both types of enrollments.</span></span> <span data-ttu-id="0e480-107">The enrollments are created using the [Java Service SDK](https://azure.github.io/azure-iot-sdk-java/service/) with the help of a sample Java application.</span><span class="sxs-lookup"><span data-stu-id="0e480-107">The enrollments are created using the [Java Service SDK](https://azure.github.io/azure-iot-sdk-java/service/) with the help of a sample Java application.</span></span> 

<span data-ttu-id="0e480-108">This quickstart expects you have already created an IoT hub and Device Provisioning Service instance.</span><span class="sxs-lookup"><span data-stu-id="0e480-108">This quickstart expects you have already created an IoT hub and Device Provisioning Service instance.</span></span> <span data-ttu-id="0e480-109">If you have not already created these resources, complete the [Set up IoT Hub Device Provisioning Service with the Azure portal](./quick-setup-auto-provision.md) quickstart before proceeding with this article.</span><span class="sxs-lookup"><span data-stu-id="0e480-109">If you have not already created these resources, complete the [Set up IoT Hub Device Provisioning Service with the Azure portal](./quick-setup-auto-provision.md) quickstart before proceeding with this article.</span></span>

<span data-ttu-id="0e480-110">Although the Java Service SDK works on both Windows and Linux machines, this article uses a Windows development machine to walk through the enrollment process.</span><span class="sxs-lookup"><span data-stu-id="0e480-110">Although the Java Service SDK works on both Windows and Linux machines, this article uses a Windows development machine to walk through the enrollment process.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="0e480-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0e480-111">Prerequisites</span></span>

* <span data-ttu-id="0e480-112">Install [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="0e480-112">Install [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="0e480-113">Install [Maven 3](https://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="0e480-113">Install [Maven 3](https://maven.apache.org/download.cgi).</span></span> <span data-ttu-id="0e480-114">You can verify your current Maven version by running:</span><span class="sxs-lookup"><span data-stu-id="0e480-114">You can verify your current Maven version by running:</span></span>

    ```cmd/sh
    mvn --version
    ```

* <span data-ttu-id="0e480-115">Install [Git](https://git-scm.com/download/).</span><span class="sxs-lookup"><span data-stu-id="0e480-115">Install [Git](https://git-scm.com/download/).</span></span>


<a id="javasample"></a>

## <a name="download-and-modify-the-java-sample-code"></a><span data-ttu-id="0e480-116">Download and modify the Java sample code</span><span class="sxs-lookup"><span data-stu-id="0e480-116">Download and modify the Java sample code</span></span>

<span data-ttu-id="0e480-117">This section uses a self-signed X.509 certificate, it is important to keep in mind the following points:</span><span class="sxs-lookup"><span data-stu-id="0e480-117">This section uses a self-signed X.509 certificate, it is important to keep in mind the following points:</span></span>

* <span data-ttu-id="0e480-118">Self-signed certificates are for testing only, and should not be used in production.</span><span class="sxs-lookup"><span data-stu-id="0e480-118">Self-signed certificates are for testing only, and should not be used in production.</span></span>
* <span data-ttu-id="0e480-119">The default expiration date for a self-signed certificate is one year.</span><span class="sxs-lookup"><span data-stu-id="0e480-119">The default expiration date for a self-signed certificate is one year.</span></span>

<span data-ttu-id="0e480-120">The following steps show how to add the provisioning details of your X.509 device to the sample code.</span><span class="sxs-lookup"><span data-stu-id="0e480-120">The following steps show how to add the provisioning details of your X.509 device to the sample code.</span></span> 

1. <span data-ttu-id="0e480-121">Open a command prompt.</span><span class="sxs-lookup"><span data-stu-id="0e480-121">Open a command prompt.</span></span> <span data-ttu-id="0e480-122">Clone the GitHub repo for device enrollment code sample using the Java Service SDK:</span><span class="sxs-lookup"><span data-stu-id="0e480-122">Clone the GitHub repo for device enrollment code sample using the Java Service SDK:</span></span>
    
    ```cmd\sh
    git clone https://github.com/Azure/azure-iot-sdk-java.git --recursive
    ```

2. <span data-ttu-id="0e480-123">In the downloaded source code, navigate to the sample folder **_azure-iot-sdk-java/provisioning/provisioning-samples/service-enrollment-group-sample_**.</span><span class="sxs-lookup"><span data-stu-id="0e480-123">In the downloaded source code, navigate to the sample folder **_azure-iot-sdk-java/provisioning/provisioning-samples/service-enrollment-group-sample_**.</span></span> <span data-ttu-id="0e480-124">Open the file **_/src/main/java/samples/com/microsoft/azure/sdk/iot/ServiceEnrollmentGroupSample.java_** in an editor of your choice, and add the following details:</span><span class="sxs-lookup"><span data-stu-id="0e480-124">Open the file **_/src/main/java/samples/com/microsoft/azure/sdk/iot/ServiceEnrollmentGroupSample.java_** in an editor of your choice, and add the following details:</span></span>

    1. <span data-ttu-id="0e480-125">Add the `[Provisioning Connection String]` for your provisioning service, from the portal as following:</span><span class="sxs-lookup"><span data-stu-id="0e480-125">Add the `[Provisioning Connection String]` for your provisioning service, from the portal as following:</span></span>
        1. <span data-ttu-id="0e480-126">Navigate to your provisioning service in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0e480-126">Navigate to your provisioning service in the [Azure portal](https://portal.azure.com).</span></span> 
        2. <span data-ttu-id="0e480-127">Open the **Shared access policies**, and select a policy, which has the *EnrollmentWrite* permission.</span><span class="sxs-lookup"><span data-stu-id="0e480-127">Open the **Shared access policies**, and select a policy, which has the *EnrollmentWrite* permission.</span></span>
        3. <span data-ttu-id="0e480-128">Copy the **Primary key connection string**.</span><span class="sxs-lookup"><span data-stu-id="0e480-128">Copy the **Primary key connection string**.</span></span> 

            ![Get the provisioning connection string from portal](./media/quick-enroll-device-x509-java/provisioning-string.png)  

        4. <span data-ttu-id="0e480-130">In the sample code file **_ServiceEnrollmentGroupSample.java_**, replace the `[Provisioning Connection String]` with the **Primary key connection string**.</span><span class="sxs-lookup"><span data-stu-id="0e480-130">In the sample code file **_ServiceEnrollmentGroupSample.java_**, replace the `[Provisioning Connection String]` with the **Primary key connection string**.</span></span>

            ```Java
            private static final String PROVISIONING_CONNECTION_STRING = "[Provisioning Connection String]";
            ```

    2. <span data-ttu-id="0e480-131">Add the root certificate for the group of devices.</span><span class="sxs-lookup"><span data-stu-id="0e480-131">Add the root certificate for the group of devices.</span></span> <span data-ttu-id="0e480-132">If you need a sample root certificate, use the _X.509 certificate generator_ tool as follows:</span><span class="sxs-lookup"><span data-stu-id="0e480-132">If you need a sample root certificate, use the _X.509 certificate generator_ tool as follows:</span></span>
        1. <span data-ttu-id="0e480-133">In a command window, navigate to the folder **_azure-iot-sdk-java/provisioning/provisioning-tools/provisioning-x509-cert-generator_**.</span><span class="sxs-lookup"><span data-stu-id="0e480-133">In a command window, navigate to the folder **_azure-iot-sdk-java/provisioning/provisioning-tools/provisioning-x509-cert-generator_**.</span></span>
        2. <span data-ttu-id="0e480-134">Build the tool by running the following command:</span><span class="sxs-lookup"><span data-stu-id="0e480-134">Build the tool by running the following command:</span></span>

                ```cmd\sh
                mvn clean install
                ```

        4. <span data-ttu-id="0e480-135">Run the tool using the following commands:</span><span class="sxs-lookup"><span data-stu-id="0e480-135">Run the tool using the following commands:</span></span>

                ```cmd\sh
                cd target
                java -jar ./provisioning-x509-cert-generator-{version}-with-deps.jar
                ```

        5. <span data-ttu-id="0e480-136">When prompted, you may optionally enter a _Common Name_ for your certificates.</span><span class="sxs-lookup"><span data-stu-id="0e480-136">When prompted, you may optionally enter a _Common Name_ for your certificates.</span></span>
        6. <span data-ttu-id="0e480-137">The tool locally generates a **Client Cert**, the **Client Cert Private Key**, and the **Root Cert**.</span><span class="sxs-lookup"><span data-stu-id="0e480-137">The tool locally generates a **Client Cert**, the **Client Cert Private Key**, and the **Root Cert**.</span></span>
        7. <span data-ttu-id="0e480-138">Copy the **Root Cert**, including the lines **_-----BEGIN CERTIFICATE-----_** and **_-----END CERTIFICATE-----_**.</span><span class="sxs-lookup"><span data-stu-id="0e480-138">Copy the **Root Cert**, including the lines **_-----BEGIN CERTIFICATE-----_** and **_-----END CERTIFICATE-----_**.</span></span> 
        8. <span data-ttu-id="0e480-139">Assign the value of the **Root Cert** to the parameter **PUBLIC_KEY_CERTIFICATE_STRING** as shown below:</span><span class="sxs-lookup"><span data-stu-id="0e480-139">Assign the value of the **Root Cert** to the parameter **PUBLIC_KEY_CERTIFICATE_STRING** as shown below:</span></span>

                ```Java
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

        9. <span data-ttu-id="0e480-140">Close the command window, or enter **n** when prompted for *Verification Code*.</span><span class="sxs-lookup"><span data-stu-id="0e480-140">Close the command window, or enter **n** when prompted for *Verification Code*.</span></span> 
 
    3. <span data-ttu-id="0e480-141">Optionally, you may configure your provisioning service through the sample code:</span><span class="sxs-lookup"><span data-stu-id="0e480-141">Optionally, you may configure your provisioning service through the sample code:</span></span>
        - <span data-ttu-id="0e480-142">To add this configuration to the sample, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="0e480-142">To add this configuration to the sample, follow these steps:</span></span>
            1. <span data-ttu-id="0e480-143">Navigate to the IoT hub linked to your provisioning service in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0e480-143">Navigate to the IoT hub linked to your provisioning service in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="0e480-144">Open the **Overview** tab for the hub, and copy the **Hostname**.</span><span class="sxs-lookup"><span data-stu-id="0e480-144">Open the **Overview** tab for the hub, and copy the **Hostname**.</span></span> <span data-ttu-id="0e480-145">Assign this **Hostname** to the *IOTHUB_HOST_NAME* parameter.</span><span class="sxs-lookup"><span data-stu-id="0e480-145">Assign this **Hostname** to the *IOTHUB_HOST_NAME* parameter.</span></span>

                ```Java
                private static final String IOTHUB_HOST_NAME = "[Host name].azure-devices.net";
                ```
            2. <span data-ttu-id="0e480-146">Assign a friendly name to the *DEVICE_ID* parameter, and keep the *PROVISIONING_STATUS* as the default *ENABLED* value.</span><span class="sxs-lookup"><span data-stu-id="0e480-146">Assign a friendly name to the *DEVICE_ID* parameter, and keep the *PROVISIONING_STATUS* as the default *ENABLED* value.</span></span> 

        - <span data-ttu-id="0e480-147">OR, if you choose not to configure your provisioning service, make sure to comment out or delete the following statements in the _ServiceEnrollmentGroupSample.java_ file:</span><span class="sxs-lookup"><span data-stu-id="0e480-147">OR, if you choose not to configure your provisioning service, make sure to comment out or delete the following statements in the _ServiceEnrollmentGroupSample.java_ file:</span></span>

            ```Java
            enrollmentGroup.setIotHubHostName(IOTHUB_HOST_NAME);                // Optional parameter.
            enrollmentGroup.setProvisioningStatus(ProvisioningStatus.ENABLED);  // Optional parameter.
            ```

    4. <span data-ttu-id="0e480-148">Study the sample code.</span><span class="sxs-lookup"><span data-stu-id="0e480-148">Study the sample code.</span></span> <span data-ttu-id="0e480-149">It creates, updates, queries, and deletes a group enrollment for X.509 devices.</span><span class="sxs-lookup"><span data-stu-id="0e480-149">It creates, updates, queries, and deletes a group enrollment for X.509 devices.</span></span> <span data-ttu-id="0e480-150">To verify successful enrollment in portal, temporarily comment out the following lines of code at the end of the _ServiceEnrollmentGroupSample.java_ file:</span><span class="sxs-lookup"><span data-stu-id="0e480-150">To verify successful enrollment in portal, temporarily comment out the following lines of code at the end of the _ServiceEnrollmentGroupSample.java_ file:</span></span>

        ```Java
        // ************************************** Delete info of enrollmentGroup ***************************************
        System.out.println("\nDelete the enrollmentGroup...");
        provisioningServiceClient.deleteEnrollmentGroup(enrollmentGroupId);
        ```

    5. <span data-ttu-id="0e480-151">Save the file _ServiceEnrollmentGroupSample.java_.</span><span class="sxs-lookup"><span data-stu-id="0e480-151">Save the file _ServiceEnrollmentGroupSample.java_.</span></span> 
 

<a id="runjavasample"></a>

## <a name="build-and-run-sample-group-enrollment"></a><span data-ttu-id="0e480-152">Build and run sample group enrollment</span><span class="sxs-lookup"><span data-stu-id="0e480-152">Build and run sample group enrollment</span></span>

1. <span data-ttu-id="0e480-153">Open a command window, and navigate to the folder **_azure-iot-sdk-java/provisioning/provisioning-samples/service-enrollment-group-sample_**.</span><span class="sxs-lookup"><span data-stu-id="0e480-153">Open a command window, and navigate to the folder **_azure-iot-sdk-java/provisioning/provisioning-samples/service-enrollment-group-sample_**.</span></span>

2. <span data-ttu-id="0e480-154">Build the sample code by using this command:</span><span class="sxs-lookup"><span data-stu-id="0e480-154">Build the sample code by using this command:</span></span>

    ```cmd\sh
    mvn install -DskipTests
    ```

   <span data-ttu-id="0e480-155">This command downloads the Maven package [`com.microsoft.azure.sdk.iot.provisioning.service`](https://www.mvnrepository.com/artifact/com.microsoft.azure.sdk.iot.provisioning/provisioning-service-client) to your machine.</span><span class="sxs-lookup"><span data-stu-id="0e480-155">This command downloads the Maven package [`com.microsoft.azure.sdk.iot.provisioning.service`](https://www.mvnrepository.com/artifact/com.microsoft.azure.sdk.iot.provisioning/provisioning-service-client) to your machine.</span></span> <span data-ttu-id="0e480-156">This package includes the binaries for the Java service SDK, that the sample code needs to build.</span><span class="sxs-lookup"><span data-stu-id="0e480-156">This package includes the binaries for the Java service SDK, that the sample code needs to build.</span></span> <span data-ttu-id="0e480-157">If you ran the _X.509 certificate generator_ tool in the preceding section, this package will be already downloaded on your machine.</span><span class="sxs-lookup"><span data-stu-id="0e480-157">If you ran the _X.509 certificate generator_ tool in the preceding section, this package will be already downloaded on your machine.</span></span> 

3. <span data-ttu-id="0e480-158">Run the sample by using these commands at the command window:</span><span class="sxs-lookup"><span data-stu-id="0e480-158">Run the sample by using these commands at the command window:</span></span>

    ```cmd\sh
    cd target
    java -jar ./service-enrollment-group-sample-{version}-with-deps.jar
    ```

4. <span data-ttu-id="0e480-159">Observe the output window for successful enrollment.</span><span class="sxs-lookup"><span data-stu-id="0e480-159">Observe the output window for successful enrollment.</span></span>

5. <span data-ttu-id="0e480-160">Navigate to your provisioning service in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0e480-160">Navigate to your provisioning service in the Azure portal.</span></span> <span data-ttu-id="0e480-161">Click **Manage enrollments**.</span><span class="sxs-lookup"><span data-stu-id="0e480-161">Click **Manage enrollments**.</span></span> <span data-ttu-id="0e480-162">Notice that your group of X.509 devices appears under the **Enrollment Groups** tab, with an auto-generated *GROUP NAME*.</span><span class="sxs-lookup"><span data-stu-id="0e480-162">Notice that your group of X.509 devices appears under the **Enrollment Groups** tab, with an auto-generated *GROUP NAME*.</span></span> 

    ![Verify successful X.509 enrollment in portal](./media/quick-enroll-device-x509-java/verify-x509-enrollment.png)  

## <a name="modifications-to-enroll-a-single-x509-device"></a><span data-ttu-id="0e480-164">Modifications to enroll a single X.509 device</span><span class="sxs-lookup"><span data-stu-id="0e480-164">Modifications to enroll a single X.509 device</span></span>

<span data-ttu-id="0e480-165">To enroll a single X.509 device, modify the *individual enrollment* sample code used in [Enroll TPM device to IoT Hub Device Provisioning Service using Java service SDK](quick-enroll-device-tpm-java.md#javasample) as follows:</span><span class="sxs-lookup"><span data-stu-id="0e480-165">To enroll a single X.509 device, modify the *individual enrollment* sample code used in [Enroll TPM device to IoT Hub Device Provisioning Service using Java service SDK](quick-enroll-device-tpm-java.md#javasample) as follows:</span></span>

1. <span data-ttu-id="0e480-166">Copy the *Common Name* of your X.509 client certificate to the clipboard.</span><span class="sxs-lookup"><span data-stu-id="0e480-166">Copy the *Common Name* of your X.509 client certificate to the clipboard.</span></span> <span data-ttu-id="0e480-167">If you wish to use the _X.509 certificate generator_ tool as shown in the [preceding sample code section](#javasample), either enter a _Common Name_ for your certificate, or use the default **microsoftriotcore**.</span><span class="sxs-lookup"><span data-stu-id="0e480-167">If you wish to use the _X.509 certificate generator_ tool as shown in the [preceding sample code section](#javasample), either enter a _Common Name_ for your certificate, or use the default **microsoftriotcore**.</span></span> <span data-ttu-id="0e480-168">Use this **Common Name** as the value for the *REGISTRATION_ID* variable.</span><span class="sxs-lookup"><span data-stu-id="0e480-168">Use this **Common Name** as the value for the *REGISTRATION_ID* variable.</span></span> 

    ```Java
    // Use common name of your X.509 client certificate
    private static final String REGISTRATION_ID = "[RegistrationId]";
    ```

2. <span data-ttu-id="0e480-169">Rename the variable *TPM_ENDORSEMENT_KEY* as *PUBLIC_KEY_CERTIFICATE_STRING*.</span><span class="sxs-lookup"><span data-stu-id="0e480-169">Rename the variable *TPM_ENDORSEMENT_KEY* as *PUBLIC_KEY_CERTIFICATE_STRING*.</span></span> <span data-ttu-id="0e480-170">Copy your client certificate or the **Client Cert** from the output of the _X.509 certificate generator_ tool, as the value for the *PUBLIC_KEY_CERTIFICATE_STRING* variable.</span><span class="sxs-lookup"><span data-stu-id="0e480-170">Copy your client certificate or the **Client Cert** from the output of the _X.509 certificate generator_ tool, as the value for the *PUBLIC_KEY_CERTIFICATE_STRING* variable.</span></span> 

    ```Java
    // Rename the variable *TPM_ENDORSEMENT_KEY* as *PUBLIC_KEY_CERTIFICATE_STRING*
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
3. <span data-ttu-id="0e480-171">In the **main** function, replace the line `Attestation attestation = new TpmAttestation(TPM_ENDORSEMENT_KEY);` with the following to use the X.509 client certificate:</span><span class="sxs-lookup"><span data-stu-id="0e480-171">In the **main** function, replace the line `Attestation attestation = new TpmAttestation(TPM_ENDORSEMENT_KEY);` with the following to use the X.509 client certificate:</span></span>
    ```Java
    Attestation attestation = X509Attestation.createFromClientCertificates(PUBLIC_KEY_CERTIFICATE_STRING);
    ```

4. <span data-ttu-id="0e480-172">Save, build, and run the *individual enrollment* sample file, using the steps in the section [Build and run the sample code for individual enrollment](quick-enroll-device-tpm-java.md#runjavasample).</span><span class="sxs-lookup"><span data-stu-id="0e480-172">Save, build, and run the *individual enrollment* sample file, using the steps in the section [Build and run the sample code for individual enrollment](quick-enroll-device-tpm-java.md#runjavasample).</span></span>


## <a name="clean-up-resources"></a><span data-ttu-id="0e480-173">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="0e480-173">Clean up resources</span></span>
<span data-ttu-id="0e480-174">If you plan to explore the Java service sample, do not clean up the resources created in this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="0e480-174">If you plan to explore the Java service sample, do not clean up the resources created in this Quickstart.</span></span> <span data-ttu-id="0e480-175">If you do not plan to continue, use the following steps to delete all resources created by this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="0e480-175">If you do not plan to continue, use the following steps to delete all resources created by this Quickstart.</span></span>

1. <span data-ttu-id="0e480-176">Close the Java sample output window on your machine.</span><span class="sxs-lookup"><span data-stu-id="0e480-176">Close the Java sample output window on your machine.</span></span>
1. <span data-ttu-id="0e480-177">Close the _X509 Cert Generator_ window on your machine.</span><span class="sxs-lookup"><span data-stu-id="0e480-177">Close the _X509 Cert Generator_ window on your machine.</span></span>
1. <span data-ttu-id="0e480-178">Navigate to your Device Provisioning service in the Azure portal, click **Manage enrollments**, and then select the **Enrollment Groups** tab. Select the *GROUP NAME* for the X.509 devices you enrolled using this Quickstart, and click the **Delete** button at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="0e480-178">Navigate to your Device Provisioning service in the Azure portal, click **Manage enrollments**, and then select the **Enrollment Groups** tab. Select the *GROUP NAME* for the X.509 devices you enrolled using this Quickstart, and click the **Delete** button at the top of the blade.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="0e480-179">Next steps</span><span class="sxs-lookup"><span data-stu-id="0e480-179">Next steps</span></span>
<span data-ttu-id="0e480-180">In this Quickstart, you enrolled a simulated group of X.509 devices to your Device Provisioning service.</span><span class="sxs-lookup"><span data-stu-id="0e480-180">In this Quickstart, you enrolled a simulated group of X.509 devices to your Device Provisioning service.</span></span> <span data-ttu-id="0e480-181">To learn about device provisioning in depth, continue to the tutorial for the Device Provisioning Service setup in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0e480-181">To learn about device provisioning in depth, continue to the tutorial for the Device Provisioning Service setup in the Azure portal.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="0e480-182">Azure IoT Hub Device Provisioning Service tutorials</span><span class="sxs-lookup"><span data-stu-id="0e480-182">Azure IoT Hub Device Provisioning Service tutorials</span></span>](./tutorial-set-up-cloud.md)
