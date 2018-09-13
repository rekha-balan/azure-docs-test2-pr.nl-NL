---
title: Enroll TPM device to Azure Device Provisioning Service using Java | Microsoft Docs
description: Azure Quickstart - Enroll TPM device to Azure IoT Hub Device Provisioning Service using Java service SDK
author: wesmc7777
ms.author: wesmc
ms.date: 12/20/2017
ms.topic: quickstart
ms.service: iot-dps
services: iot-dps
manager: timlt
ms.devlang: java
ms.custom: mvc
ms.openlocfilehash: 68f8125ddc0691346813bb31124fa3abd4976296
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857864"
---
# <a name="enroll-tpm-device-to-iot-hub-device-provisioning-service-using-java-service-sdk"></a><span data-ttu-id="7c770-103">Enroll TPM device to IoT Hub Device Provisioning Service using Java service SDK</span><span class="sxs-lookup"><span data-stu-id="7c770-103">Enroll TPM device to IoT Hub Device Provisioning Service using Java service SDK</span></span>

[!INCLUDE [iot-dps-selector-quick-enroll-device-tpm](../../includes/iot-dps-selector-quick-enroll-device-tpm.md)]


<span data-ttu-id="7c770-104">These steps show how to enroll a simulated TPM device programmatically to the Azure IoT Hub Device Provisioning Services, using the [Java Service SDK](https://azure.github.io/azure-iot-sdk-java/service/) with the help of a sample Java application.</span><span class="sxs-lookup"><span data-stu-id="7c770-104">These steps show how to enroll a simulated TPM device programmatically to the Azure IoT Hub Device Provisioning Services, using the [Java Service SDK](https://azure.github.io/azure-iot-sdk-java/service/) with the help of a sample Java application.</span></span> <span data-ttu-id="7c770-105">Although the Java Service SDK works on both Windows and Linux machines, this article uses a Windows development machine to walk through the enrollment process.</span><span class="sxs-lookup"><span data-stu-id="7c770-105">Although the Java Service SDK works on both Windows and Linux machines, this article uses a Windows development machine to walk through the enrollment process.</span></span>

<span data-ttu-id="7c770-106">Make sure to [set up IoT Hub Device Provisioning Service with the Azure portal](./quick-setup-auto-provision.md), as well as [simulate a TPM device](quick-create-simulated-device.md#simulatetpm) before you proceed.</span><span class="sxs-lookup"><span data-stu-id="7c770-106">Make sure to [set up IoT Hub Device Provisioning Service with the Azure portal](./quick-setup-auto-provision.md), as well as [simulate a TPM device](quick-create-simulated-device.md#simulatetpm) before you proceed.</span></span>

<a id="setupdevbox"></a>

## <a name="prepare-the-development-environment"></a><span data-ttu-id="7c770-107">Prepare the development environment</span><span class="sxs-lookup"><span data-stu-id="7c770-107">Prepare the development environment</span></span> 

1. <span data-ttu-id="7c770-108">Make sure you have [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) installed on your machine.</span><span class="sxs-lookup"><span data-stu-id="7c770-108">Make sure you have [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) installed on your machine.</span></span> 

2. <span data-ttu-id="7c770-109">Set up environment variables for your Java installation.</span><span class="sxs-lookup"><span data-stu-id="7c770-109">Set up environment variables for your Java installation.</span></span> <span data-ttu-id="7c770-110">The `PATH` variable should include the full path to *jdk1.8.x\bin* directory.</span><span class="sxs-lookup"><span data-stu-id="7c770-110">The `PATH` variable should include the full path to *jdk1.8.x\bin* directory.</span></span> <span data-ttu-id="7c770-111">If this is your machine's first Java installation, then create a new environment variable named `JAVA_HOME` and point it to the full path to the *jdk1.8.x* directory.</span><span class="sxs-lookup"><span data-stu-id="7c770-111">If this is your machine's first Java installation, then create a new environment variable named `JAVA_HOME` and point it to the full path to the *jdk1.8.x* directory.</span></span> <span data-ttu-id="7c770-112">On Windows machine, this directory is usually found in the *C:\\Program Files\\Java\\* folder, and you can create or edit environment variables by searching for **Edit the system environment variables** on the **Control panel** of your Windows machine.</span><span class="sxs-lookup"><span data-stu-id="7c770-112">On Windows machine, this directory is usually found in the *C:\\Program Files\\Java\\* folder, and you can create or edit environment variables by searching for **Edit the system environment variables** on the **Control panel** of your Windows machine.</span></span> 

  <span data-ttu-id="7c770-113">You may check if Java is successfully set up on your machine by running the following command on your command window:</span><span class="sxs-lookup"><span data-stu-id="7c770-113">You may check if Java is successfully set up on your machine by running the following command on your command window:</span></span>

    ```cmd\sh
    java -version
    ```

3. <span data-ttu-id="7c770-114">Download and extract [Maven 3](https://maven.apache.org/download.cgi) on your machine.</span><span class="sxs-lookup"><span data-stu-id="7c770-114">Download and extract [Maven 3](https://maven.apache.org/download.cgi) on your machine.</span></span> 

4. <span data-ttu-id="7c770-115">Edit environment variable `PATH` to point to the *apache-maven-3.x.x\\bin* folder inside the folder where Maven is extracted.</span><span class="sxs-lookup"><span data-stu-id="7c770-115">Edit environment variable `PATH` to point to the *apache-maven-3.x.x\\bin* folder inside the folder where Maven is extracted.</span></span> <span data-ttu-id="7c770-116">You may confirm that Maven is successfully installed by running this command on your command window:</span><span class="sxs-lookup"><span data-stu-id="7c770-116">You may confirm that Maven is successfully installed by running this command on your command window:</span></span>

    ```cmd\sh
    mvn --version
    ```

5. <span data-ttu-id="7c770-117">Make sure [git](https://git-scm.com/download/) is installed on your machine and is added to the environment variable `PATH`.</span><span class="sxs-lookup"><span data-stu-id="7c770-117">Make sure [git](https://git-scm.com/download/) is installed on your machine and is added to the environment variable `PATH`.</span></span> 


<a id="javasample"></a>

## <a name="download-and-modify-the-java-sample-code"></a><span data-ttu-id="7c770-118">Download and modify the Java sample code</span><span class="sxs-lookup"><span data-stu-id="7c770-118">Download and modify the Java sample code</span></span>

<span data-ttu-id="7c770-119">This section shows how to add the provisioning details of your TPM device to the sample code.</span><span class="sxs-lookup"><span data-stu-id="7c770-119">This section shows how to add the provisioning details of your TPM device to the sample code.</span></span> 

1. <span data-ttu-id="7c770-120">Open a command prompt.</span><span class="sxs-lookup"><span data-stu-id="7c770-120">Open a command prompt.</span></span> <span data-ttu-id="7c770-121">Clone the GitHub repo for device enrollment code sample using the Java Service SDK:</span><span class="sxs-lookup"><span data-stu-id="7c770-121">Clone the GitHub repo for device enrollment code sample using the Java Service SDK:</span></span>
    
    ```cmd\sh
    git clone https://github.com/Azure/azure-iot-sdk-java.git --recursive
    ```

2. <span data-ttu-id="7c770-122">In the downloaded source code, navigate to the sample folder **_azure-iot-sdk-java/provisioning/provisioning-samples/service-enrollment-sample_**.</span><span class="sxs-lookup"><span data-stu-id="7c770-122">In the downloaded source code, navigate to the sample folder **_azure-iot-sdk-java/provisioning/provisioning-samples/service-enrollment-sample_**.</span></span> <span data-ttu-id="7c770-123">Open the file **_/src/main/java/samples/com/microsoft/azure/sdk/iot/ServiceEnrollmentSample.java_** in an editor of your choice, and add the following details:</span><span class="sxs-lookup"><span data-stu-id="7c770-123">Open the file **_/src/main/java/samples/com/microsoft/azure/sdk/iot/ServiceEnrollmentSample.java_** in an editor of your choice, and add the following details:</span></span>

    1. <span data-ttu-id="7c770-124">Add the `[Provisioning Connection String]` for your provisioning service, from the portal as following:</span><span class="sxs-lookup"><span data-stu-id="7c770-124">Add the `[Provisioning Connection String]` for your provisioning service, from the portal as following:</span></span>
        1. <span data-ttu-id="7c770-125">Navigate to your provisioning service in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7c770-125">Navigate to your provisioning service in the [Azure portal](https://portal.azure.com).</span></span> 
        2. <span data-ttu-id="7c770-126">Open the **Shared access policies**, and select a policy which has the *EnrollmentWrite* permission.</span><span class="sxs-lookup"><span data-stu-id="7c770-126">Open the **Shared access policies**, and select a policy which has the *EnrollmentWrite* permission.</span></span>
        3. <span data-ttu-id="7c770-127">Copy the **Primary key connection string**.</span><span class="sxs-lookup"><span data-stu-id="7c770-127">Copy the **Primary key connection string**.</span></span> 

            ![Get the provisioning connection string from portal](./media/quick-enroll-device-tpm-java/provisioning-string.png)  

        4. <span data-ttu-id="7c770-129">In the sample code file **_ServiceEnrollmentSample.java_**, replace the `[Provisioning Connection String]` with the **Primary key connection string**.</span><span class="sxs-lookup"><span data-stu-id="7c770-129">In the sample code file **_ServiceEnrollmentSample.java_**, replace the `[Provisioning Connection String]` with the **Primary key connection string**.</span></span>
    
            ```Java
            private static final String PROVISIONING_CONNECTION_STRING = "[Provisioning Connection String]";
            ```

    2. <span data-ttu-id="7c770-130">Add the TPM device details:</span><span class="sxs-lookup"><span data-stu-id="7c770-130">Add the TPM device details:</span></span>
        1. <span data-ttu-id="7c770-131">Get the *Registration ID* and the *TPM endorsement key* for a TPM device simulation, by following the steps leading to the section [Simulate TPM device](quick-create-simulated-device.md#simulatetpm).</span><span class="sxs-lookup"><span data-stu-id="7c770-131">Get the *Registration ID* and the *TPM endorsement key* for a TPM device simulation, by following the steps leading to the section [Simulate TPM device](quick-create-simulated-device.md#simulatetpm).</span></span>
        2. <span data-ttu-id="7c770-132">Use the **_Registration ID_** and the **_Endorsement Key_** from the output of the preceding step, to replace the `[RegistrationId]` and `[TPM Endorsement Key]` in the sample code file **_ServiceEnrollmentSample.java_**:</span><span class="sxs-lookup"><span data-stu-id="7c770-132">Use the **_Registration ID_** and the **_Endorsement Key_** from the output of the preceding step, to replace the `[RegistrationId]` and `[TPM Endorsement Key]` in the sample code file **_ServiceEnrollmentSample.java_**:</span></span>
        
            ```Java
            private static final String REGISTRATION_ID = "[RegistrationId]";
            private static final String TPM_ENDORSEMENT_KEY = "[TPM Endorsement Key]";
            ```

    3. <span data-ttu-id="7c770-133">Optionally, you may configure your provisioning service through the sample code:</span><span class="sxs-lookup"><span data-stu-id="7c770-133">Optionally, you may configure your provisioning service through the sample code:</span></span>
        - <span data-ttu-id="7c770-134">To add this configuration to the sample, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="7c770-134">To add this configuration to the sample, follow these steps:</span></span>
            1. <span data-ttu-id="7c770-135">Navigate to the IoT hub linked to your provisioning service in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7c770-135">Navigate to the IoT hub linked to your provisioning service in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="7c770-136">Open the **Overview** tab for the hub, and copy the **Hostname**.</span><span class="sxs-lookup"><span data-stu-id="7c770-136">Open the **Overview** tab for the hub, and copy the **Hostname**.</span></span> <span data-ttu-id="7c770-137">Assign this **Hostname** to the *IOTHUB_HOST_NAME* parameter.</span><span class="sxs-lookup"><span data-stu-id="7c770-137">Assign this **Hostname** to the *IOTHUB_HOST_NAME* parameter.</span></span>
                ```Java
                private static final String IOTHUB_HOST_NAME = "[Host name].azure-devices.net";
                ```
            2. <span data-ttu-id="7c770-138">Assign a friendly name to the *DEVICE_ID* parameter, and keep the *PROVISIONING_STATUS* as the default *ENABLED* value.</span><span class="sxs-lookup"><span data-stu-id="7c770-138">Assign a friendly name to the *DEVICE_ID* parameter, and keep the *PROVISIONING_STATUS* as the default *ENABLED* value.</span></span> 
    
        - <span data-ttu-id="7c770-139">OR, if you choose not to configure your provisioning service, make sure to comment out or delete the following statements in the _ServiceEnrollmentSample.java_ file:</span><span class="sxs-lookup"><span data-stu-id="7c770-139">OR, if you choose not to configure your provisioning service, make sure to comment out or delete the following statements in the _ServiceEnrollmentSample.java_ file:</span></span>
            ```Java
            // The following parameters are optional. Remove it if you don't need.
            individualEnrollment.setDeviceId(DEVICE_ID);
            individualEnrollment.setIotHubHostName(IOTHUB_HOST_NAME);
            individualEnrollment.setProvisioningStatus(PROVISIONING_STATUS);
            ```

    4. <span data-ttu-id="7c770-140">Study the sample code.</span><span class="sxs-lookup"><span data-stu-id="7c770-140">Study the sample code.</span></span> <span data-ttu-id="7c770-141">It creates, updates, queries and deletes an individual TPM device enrollment.</span><span class="sxs-lookup"><span data-stu-id="7c770-141">It creates, updates, queries and deletes an individual TPM device enrollment.</span></span> <span data-ttu-id="7c770-142">To verify successful enrollment in portal, temporarily comment out the following lines of code at the end of the _ServiceEnrollmentSample.java_ file:</span><span class="sxs-lookup"><span data-stu-id="7c770-142">To verify successful enrollment in portal, temporarily comment out the following lines of code at the end of the _ServiceEnrollmentSample.java_ file:</span></span>
    
        ```Java
        // *********************************** Delete info of individualEnrollment ************************************
        System.out.println("\nDelete the individualEnrollment...");
        provisioningServiceClient.deleteIndividualEnrollment(REGISTRATION_ID);
        ```

    5. <span data-ttu-id="7c770-143">Save the file _ServiceEnrollmentSample.java_.</span><span class="sxs-lookup"><span data-stu-id="7c770-143">Save the file _ServiceEnrollmentSample.java_.</span></span>

<a id="runjavasample"></a>

## <a name="build-and-run-the-java-sample-code"></a><span data-ttu-id="7c770-144">Build and run the Java sample code</span><span class="sxs-lookup"><span data-stu-id="7c770-144">Build and run the Java sample code</span></span>

1. <span data-ttu-id="7c770-145">Open a command window, and navigate to the folder **_azure-iot-sdk-java/provisioning/provisioning-samples/service-enrollment-sample_**.</span><span class="sxs-lookup"><span data-stu-id="7c770-145">Open a command window, and navigate to the folder **_azure-iot-sdk-java/provisioning/provisioning-samples/service-enrollment-sample_**.</span></span>

2. <span data-ttu-id="7c770-146">Build the sample code by using this command:</span><span class="sxs-lookup"><span data-stu-id="7c770-146">Build the sample code by using this command:</span></span>

    ```cmd\sh
    mvn install -DskipTests
    ```

   <span data-ttu-id="7c770-147">This command downloads the Maven package [`com.microsoft.azure.sdk.iot.provisioning.service`](https://www.mvnrepository.com/artifact/com.microsoft.azure.sdk.iot.provisioning/provisioning-service-client) to your machine.</span><span class="sxs-lookup"><span data-stu-id="7c770-147">This command downloads the Maven package [`com.microsoft.azure.sdk.iot.provisioning.service`](https://www.mvnrepository.com/artifact/com.microsoft.azure.sdk.iot.provisioning/provisioning-service-client) to your machine.</span></span> <span data-ttu-id="7c770-148">This package includes the binaries for the Java service SDK, that the sample code needs to build.</span><span class="sxs-lookup"><span data-stu-id="7c770-148">This package includes the binaries for the Java service SDK, that the sample code needs to build.</span></span> 

3. <span data-ttu-id="7c770-149">Run the sample by using these commands at the command window:</span><span class="sxs-lookup"><span data-stu-id="7c770-149">Run the sample by using these commands at the command window:</span></span>

    ```cmd\sh
    cd target
    java -jar ./service-enrollment-sample-{version}-with-deps.jar
    ```

4. <span data-ttu-id="7c770-150">Observe the output window for successful enrollment.</span><span class="sxs-lookup"><span data-stu-id="7c770-150">Observe the output window for successful enrollment.</span></span> 

5. <span data-ttu-id="7c770-151">Navigate to your provisioning service in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7c770-151">Navigate to your provisioning service in the Azure portal.</span></span> <span data-ttu-id="7c770-152">Click **Manage enrollments**, and select the **Individual Enrollments** tab. Notice that the *Registration ID* of your simulated TPM device is now listed.</span><span class="sxs-lookup"><span data-stu-id="7c770-152">Click **Manage enrollments**, and select the **Individual Enrollments** tab. Notice that the *Registration ID* of your simulated TPM device is now listed.</span></span> 

    ![Verify successful TPM enrollment in portal](./media/quick-enroll-device-tpm-java/verify-tpm-enrollment.png)  

## <a name="clean-up-resources"></a><span data-ttu-id="7c770-154">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="7c770-154">Clean up resources</span></span>
<span data-ttu-id="7c770-155">If you plan to explore the Java service sample, do not clean up the resources created in this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="7c770-155">If you plan to explore the Java service sample, do not clean up the resources created in this Quickstart.</span></span> <span data-ttu-id="7c770-156">If you do not plan to continue, use the following steps to delete all resources created by this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="7c770-156">If you do not plan to continue, use the following steps to delete all resources created by this Quickstart.</span></span>

1. <span data-ttu-id="7c770-157">Close the Java sample output window on your machine.</span><span class="sxs-lookup"><span data-stu-id="7c770-157">Close the Java sample output window on your machine.</span></span>
1. <span data-ttu-id="7c770-158">Close the TPM simulator window that you may have created to simulate your TPM device.</span><span class="sxs-lookup"><span data-stu-id="7c770-158">Close the TPM simulator window that you may have created to simulate your TPM device.</span></span>
1. <span data-ttu-id="7c770-159">Navigate to your Device Provisioning service in the Azure portal, click **Manage enrollments** and then select the **Individual Enrollments** tab. Select the *Registration ID* of the device you enrolled using this Quickstart, and click the **Delete** button at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="7c770-159">Navigate to your Device Provisioning service in the Azure portal, click **Manage enrollments** and then select the **Individual Enrollments** tab. Select the *Registration ID* of the device you enrolled using this Quickstart, and click the **Delete** button at the top of the blade.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="7c770-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="7c770-160">Next steps</span></span>
<span data-ttu-id="7c770-161">In this Quickstart, you enrolled a simulated TPM device to your Device Provisioning service.</span><span class="sxs-lookup"><span data-stu-id="7c770-161">In this Quickstart, you enrolled a simulated TPM device to your Device Provisioning service.</span></span> <span data-ttu-id="7c770-162">To learn about device provisioning in depth, continue to the tutorial for the Device Provisioning Service setup in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7c770-162">To learn about device provisioning in depth, continue to the tutorial for the Device Provisioning Service setup in the Azure portal.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="7c770-163">Azure IoT Hub Device Provisioning Service tutorials</span><span class="sxs-lookup"><span data-stu-id="7c770-163">Azure IoT Hub Device Provisioning Service tutorials</span></span>](./tutorial-set-up-cloud.md)
