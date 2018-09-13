---
title: This quickstart shows you how to enroll X.509 devices to the Azure Device Provisioning Service using Node.js | Microsoft Docs
description: In this quickstart, you will enroll X.509 devices to the Azure IoT Hub Device Provisioning Service using the Node.js service SDK
author: wesmc7777
ms.author: wesmc
ms.date: 12/21/2017
ms.topic: quickstart
ms.service: iot-dps
services: iot-dps
manager: timlt
ms.devlang: nodejs
ms.custom: mvc
ms.openlocfilehash: 4c7e38f3180e8df260b29228e404a2160a17786a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869197"
---
# <a name="quickstart-enroll-x509-devices-to-the-device-provisioning-service-using-nodejs"></a><span data-ttu-id="02b9a-103">Quickstart: Enroll X.509 devices to the Device Provisioning Service using Node.js</span><span class="sxs-lookup"><span data-stu-id="02b9a-103">Quickstart: Enroll X.509 devices to the Device Provisioning Service using Node.js</span></span>

[!INCLUDE [iot-dps-selector-quick-enroll-device-x509](../../includes/iot-dps-selector-quick-enroll-device-x509.md)]

<span data-ttu-id="02b9a-104">This quickstart shows how to use Node.js to programmatically create an [Enrollment group](concepts-service.md#enrollment-group) that uses intermediate or root CA X.509 certificates.</span><span class="sxs-lookup"><span data-stu-id="02b9a-104">This quickstart shows how to use Node.js to programmatically create an [Enrollment group](concepts-service.md#enrollment-group) that uses intermediate or root CA X.509 certificates.</span></span> <span data-ttu-id="02b9a-105">The enrollment group is created using the [IoT SDK for Node.js](https://github.com/Azure/azure-iot-sdk-node) and a sample Node.js application.</span><span class="sxs-lookup"><span data-stu-id="02b9a-105">The enrollment group is created using the [IoT SDK for Node.js](https://github.com/Azure/azure-iot-sdk-node) and a sample Node.js application.</span></span> <span data-ttu-id="02b9a-106">An enrollment group controls access to the provisioning service for devices that share a common signing certificate in their certificate chain.</span><span class="sxs-lookup"><span data-stu-id="02b9a-106">An enrollment group controls access to the provisioning service for devices that share a common signing certificate in their certificate chain.</span></span> <span data-ttu-id="02b9a-107">To learn more, see [Controlling device access to the provisioning service with X.509 certificates](./concepts-security.md#controlling-device-access-to-the-provisioning-service-with-x509-certificates).</span><span class="sxs-lookup"><span data-stu-id="02b9a-107">To learn more, see [Controlling device access to the provisioning service with X.509 certificates](./concepts-security.md#controlling-device-access-to-the-provisioning-service-with-x509-certificates).</span></span> <span data-ttu-id="02b9a-108">For more information about using X.509 certificate-based Public Key Infrastructure (PKI) with Azure IoT Hub and Device Provisioning Service, see [X.509 CA certificate security overview](https://docs.microsoft.com/azure/iot-hub/iot-hub-x509ca-overview).</span><span class="sxs-lookup"><span data-stu-id="02b9a-108">For more information about using X.509 certificate-based Public Key Infrastructure (PKI) with Azure IoT Hub and Device Provisioning Service, see [X.509 CA certificate security overview](https://docs.microsoft.com/azure/iot-hub/iot-hub-x509ca-overview).</span></span> 

<span data-ttu-id="02b9a-109">This quickstart expects you have already created an IoT hub and Device Provisioning Service instance.</span><span class="sxs-lookup"><span data-stu-id="02b9a-109">This quickstart expects you have already created an IoT hub and Device Provisioning Service instance.</span></span> <span data-ttu-id="02b9a-110">If you have not already created these resources, complete the [Set up IoT Hub Device Provisioning Service with the Azure portal](./quick-setup-auto-provision.md) quickstart before proceeding with this article.</span><span class="sxs-lookup"><span data-stu-id="02b9a-110">If you have not already created these resources, complete the [Set up IoT Hub Device Provisioning Service with the Azure portal](./quick-setup-auto-provision.md) quickstart before proceeding with this article.</span></span>

<span data-ttu-id="02b9a-111">Although the steps in this article work on both Windows and Linux machines, this article is developed for a Windows development machine.</span><span class="sxs-lookup"><span data-stu-id="02b9a-111">Although the steps in this article work on both Windows and Linux machines, this article is developed for a Windows development machine.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]


## <a name="prerequisites"></a><span data-ttu-id="02b9a-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="02b9a-112">Prerequisites</span></span>

- <span data-ttu-id="02b9a-113">Install [Node.js v4.0 or above](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="02b9a-113">Install [Node.js v4.0 or above](https://nodejs.org).</span></span>
- <span data-ttu-id="02b9a-114">Install [Git](https://git-scm.com/download/).</span><span class="sxs-lookup"><span data-stu-id="02b9a-114">Install [Git](https://git-scm.com/download/).</span></span>


## <a name="prepare-test-certificates"></a><span data-ttu-id="02b9a-115">Prepare test certificates</span><span class="sxs-lookup"><span data-stu-id="02b9a-115">Prepare test certificates</span></span>

<span data-ttu-id="02b9a-116">For this quickstart, you must have a .pem or a .cer file that contains the public portion of an intermediate or root CA X.509 certificate.</span><span class="sxs-lookup"><span data-stu-id="02b9a-116">For this quickstart, you must have a .pem or a .cer file that contains the public portion of an intermediate or root CA X.509 certificate.</span></span> <span data-ttu-id="02b9a-117">This certificate must be uploaded to your provisioning service, and verified by the service.</span><span class="sxs-lookup"><span data-stu-id="02b9a-117">This certificate must be uploaded to your provisioning service, and verified by the service.</span></span> 

<span data-ttu-id="02b9a-118">The [Azure IoT C SDK](https://github.com/Azure/azure-iot-sdk-c) contains test tooling that can help you create an X.509 certificate chain, upload a root or intermediate certificate from that chain, and perform proof-of-possession with the service to verify the certificate.</span><span class="sxs-lookup"><span data-stu-id="02b9a-118">The [Azure IoT C SDK](https://github.com/Azure/azure-iot-sdk-c) contains test tooling that can help you create an X.509 certificate chain, upload a root or intermediate certificate from that chain, and perform proof-of-possession with the service to verify the certificate.</span></span> <span data-ttu-id="02b9a-119">Certificates created with the SDK tooling are designed to be used for **development testing only**.</span><span class="sxs-lookup"><span data-stu-id="02b9a-119">Certificates created with the SDK tooling are designed to be used for **development testing only**.</span></span> <span data-ttu-id="02b9a-120">These certificates **must not be used in production**.</span><span class="sxs-lookup"><span data-stu-id="02b9a-120">These certificates **must not be used in production**.</span></span> <span data-ttu-id="02b9a-121">They contain hard-coded passwords ("1234") that expire after 30 days.</span><span class="sxs-lookup"><span data-stu-id="02b9a-121">They contain hard-coded passwords ("1234") that expire after 30 days.</span></span> <span data-ttu-id="02b9a-122">To learn about obtaining certificates suitable for production use, see [How to get an X.509 CA certificate](https://docs.microsoft.com/azure/iot-hub/iot-hub-x509ca-overview#how-to-get-an-x509-ca-certificate) in the Azure IoT Hub documentation.</span><span class="sxs-lookup"><span data-stu-id="02b9a-122">To learn about obtaining certificates suitable for production use, see [How to get an X.509 CA certificate](https://docs.microsoft.com/azure/iot-hub/iot-hub-x509ca-overview#how-to-get-an-x509-ca-certificate) in the Azure IoT Hub documentation.</span></span>

<span data-ttu-id="02b9a-123">To use this test tooling to generate certificates, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="02b9a-123">To use this test tooling to generate certificates, perform the following steps:</span></span> 
 
1. <span data-ttu-id="02b9a-124">Open a command prompt or Git Bash shell, and change to a working folder on your machine.</span><span class="sxs-lookup"><span data-stu-id="02b9a-124">Open a command prompt or Git Bash shell, and change to a working folder on your machine.</span></span> <span data-ttu-id="02b9a-125">Execute the following command to clone the [Azure IoT C SDK](https://github.com/Azure/azure-iot-sdk-c) GitHub repository:</span><span class="sxs-lookup"><span data-stu-id="02b9a-125">Execute the following command to clone the [Azure IoT C SDK](https://github.com/Azure/azure-iot-sdk-c) GitHub repository:</span></span>
    
  ```cmd/sh
  git clone https://github.com/Azure/azure-iot-sdk-c.git --recursive
  ```

  <span data-ttu-id="02b9a-126">The size of this repository is currently around 220 MB.</span><span class="sxs-lookup"><span data-stu-id="02b9a-126">The size of this repository is currently around 220 MB.</span></span> <span data-ttu-id="02b9a-127">You should expect this operation to take several minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="02b9a-127">You should expect this operation to take several minutes to complete.</span></span>

  <span data-ttu-id="02b9a-128">The test tooling is located in the *azure-iot-sdk-c/tools/CACertificates* of the repository you cloned.</span><span class="sxs-lookup"><span data-stu-id="02b9a-128">The test tooling is located in the *azure-iot-sdk-c/tools/CACertificates* of the repository you cloned.</span></span>    

2. <span data-ttu-id="02b9a-129">Follow the steps in [Managing test CA certificates for samples and tutorials](https://github.com/Azure/azure-iot-sdk-c/blob/master/tools/CACertificates/CACertificateOverview.md).</span><span class="sxs-lookup"><span data-stu-id="02b9a-129">Follow the steps in [Managing test CA certificates for samples and tutorials](https://github.com/Azure/azure-iot-sdk-c/blob/master/tools/CACertificates/CACertificateOverview.md).</span></span> 



## <a name="create-the-enrollment-group-sample"></a><span data-ttu-id="02b9a-130">Create the enrollment group sample</span><span class="sxs-lookup"><span data-stu-id="02b9a-130">Create the enrollment group sample</span></span> 

 
1. <span data-ttu-id="02b9a-131">From a command window in your working folder, run:</span><span class="sxs-lookup"><span data-stu-id="02b9a-131">From a command window in your working folder, run:</span></span>
  
     ```cmd\sh
     npm install azure-iot-provisioning-service
     ```  

2. <span data-ttu-id="02b9a-132">Using a text editor, create a **create_enrollment_group.js** file in your working folder.</span><span class="sxs-lookup"><span data-stu-id="02b9a-132">Using a text editor, create a **create_enrollment_group.js** file in your working folder.</span></span> <span data-ttu-id="02b9a-133">Add the following code to the file and save:</span><span class="sxs-lookup"><span data-stu-id="02b9a-133">Add the following code to the file and save:</span></span>

    ```
    'use strict';
    var fs = require('fs');

    var provisioningServiceClient = require('azure-iot-provisioning-service').ProvisioningServiceClient;

    var serviceClient = provisioningServiceClient.fromConnectionString(process.argv[2]);

    var enrollment = {
      enrollmentGroupId: 'first',
      attestation: {
        type: 'x509',
        x509: {
          signingCertificates: {
            primary: {
              certificate: fs.readFileSync(process.argv[3], 'utf-8').toString()
            }
          }
        }
      },
      provisioningStatus: 'disabled'
    };

    serviceClient.createOrUpdateEnrollmentGroup(enrollment, function(err, enrollmentResponse) {
      if (err) {
        console.log('error creating the group enrollment: ' + err);
      } else {
        console.log("enrollment record returned: " + JSON.stringify(enrollmentResponse, null, 2));
        enrollmentResponse.provisioningStatus = 'enabled';
        serviceClient.createOrUpdateEnrollmentGroup(enrollmentResponse, function(err, enrollmentResponse) {
          if (err) {
            console.log('error updating the group enrollment: ' + err);
          } else {
            console.log("updated enrollment record returned: " + JSON.stringify(enrollmentResponse, null, 2));
          }
        });
      }
    });
    ````

## <a name="run-the-enrollment-group-sample"></a><span data-ttu-id="02b9a-134">Run the enrollment group sample</span><span class="sxs-lookup"><span data-stu-id="02b9a-134">Run the enrollment group sample</span></span>
 
1. <span data-ttu-id="02b9a-135">To run the sample, you need the connection string for your provisioning service.</span><span class="sxs-lookup"><span data-stu-id="02b9a-135">To run the sample, you need the connection string for your provisioning service.</span></span> 
    1. <span data-ttu-id="02b9a-136">Sign in to the Azure portal, click on the **All resources** button on the left-hand menu and open your Device Provisioning service.</span><span class="sxs-lookup"><span data-stu-id="02b9a-136">Sign in to the Azure portal, click on the **All resources** button on the left-hand menu and open your Device Provisioning service.</span></span> 
    2. <span data-ttu-id="02b9a-137">Click **Shared access policies**, then click the access policy you want to use to open its properties.</span><span class="sxs-lookup"><span data-stu-id="02b9a-137">Click **Shared access policies**, then click the access policy you want to use to open its properties.</span></span> <span data-ttu-id="02b9a-138">In the **Access Policy** window, copy and note down the primary key connection string.</span><span class="sxs-lookup"><span data-stu-id="02b9a-138">In the **Access Policy** window, copy and note down the primary key connection string.</span></span> 

    ![Get provisioning service connection string from the portal](./media/quick-enroll-device-x509-node/get-service-connection-string.png) 


3. <span data-ttu-id="02b9a-140">As stated in [Prepare test certificates](quick-enroll-device-x509-node.md#prepare-test-certificates), you also need a .pem file that contains an X.509 intermediate or root CA certificate that has been previously uploaded and verified with your provisioning service.</span><span class="sxs-lookup"><span data-stu-id="02b9a-140">As stated in [Prepare test certificates](quick-enroll-device-x509-node.md#prepare-test-certificates), you also need a .pem file that contains an X.509 intermediate or root CA certificate that has been previously uploaded and verified with your provisioning service.</span></span> <span data-ttu-id="02b9a-141">To check that your certificate has been uploaded and verified, on the Device Provisioning Service summary page in the Azure portal, click  **Certificates**.</span><span class="sxs-lookup"><span data-stu-id="02b9a-141">To check that your certificate has been uploaded and verified, on the Device Provisioning Service summary page in the Azure portal, click  **Certificates**.</span></span> <span data-ttu-id="02b9a-142">Find the certificate that you want to use for the group enrollment and ensure that its status value is *verified*.</span><span class="sxs-lookup"><span data-stu-id="02b9a-142">Find the certificate that you want to use for the group enrollment and ensure that its status value is *verified*.</span></span>

    ![Verified certificate in the portal](./media/quick-enroll-device-x509-node/verify-certificate.png) 

1. <span data-ttu-id="02b9a-144">To create an enrollment group for your certificate, run the following command (include the quotes around the command arguments):</span><span class="sxs-lookup"><span data-stu-id="02b9a-144">To create an enrollment group for your certificate, run the following command (include the quotes around the command arguments):</span></span>
 
     ```cmd\sh
     node create_enrollment_group.js "<the connection string for your provisioning service>" "<your certificate's .pem file>"
     ```
 
3. <span data-ttu-id="02b9a-145">On successful creation, the command window displays the properties of the new enrollment group.</span><span class="sxs-lookup"><span data-stu-id="02b9a-145">On successful creation, the command window displays the properties of the new enrollment group.</span></span>

    ![Enrollment properties in the command output](./media/quick-enroll-device-x509-node/sample-output.png) 

4. <span data-ttu-id="02b9a-147">Verify that the enrollment group has been created.</span><span class="sxs-lookup"><span data-stu-id="02b9a-147">Verify that the enrollment group has been created.</span></span> <span data-ttu-id="02b9a-148">In the Azure portal, on the Device Provisioning Service summary blade, select **Manage enrollments**.</span><span class="sxs-lookup"><span data-stu-id="02b9a-148">In the Azure portal, on the Device Provisioning Service summary blade, select **Manage enrollments**.</span></span> <span data-ttu-id="02b9a-149">Select the **Enrollment Groups** tab and verify that the new enrollment entry (*first*) is present.</span><span class="sxs-lookup"><span data-stu-id="02b9a-149">Select the **Enrollment Groups** tab and verify that the new enrollment entry (*first*) is present.</span></span>

    ![Enrollment properties in the portal](./media/quick-enroll-device-x509-node/verify-enrollment-portal.png) 
 
## <a name="clean-up-resources"></a><span data-ttu-id="02b9a-151">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="02b9a-151">Clean up resources</span></span>
<span data-ttu-id="02b9a-152">If you plan to explore the Node.js service samples, do not clean up the resources created in this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="02b9a-152">If you plan to explore the Node.js service samples, do not clean up the resources created in this Quickstart.</span></span> <span data-ttu-id="02b9a-153">If you do not plan to continue, use the following steps to delete all Azure resources created by this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="02b9a-153">If you do not plan to continue, use the following steps to delete all Azure resources created by this Quickstart.</span></span>
 
1. <span data-ttu-id="02b9a-154">Close the Node.js sample output window on your machine.</span><span class="sxs-lookup"><span data-stu-id="02b9a-154">Close the Node.js sample output window on your machine.</span></span>
2. <span data-ttu-id="02b9a-155">Navigate to your Device Provisioning service in the Azure portal, click **Manage enrollments**, and then select the **Enrollment Groups** tab. Select the *Registration ID* for the enrollment entry you created using this Quickstart and click the **Delete** button at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="02b9a-155">Navigate to your Device Provisioning service in the Azure portal, click **Manage enrollments**, and then select the **Enrollment Groups** tab. Select the *Registration ID* for the enrollment entry you created using this Quickstart and click the **Delete** button at the top of the blade.</span></span>  
3. <span data-ttu-id="02b9a-156">From your Device Provisioning service in the Azure portal, click **Certificates**, click the certificate you uploaded for this Quickstart, and click the **Delete** button at the top of the **Certificate Details** window.</span><span class="sxs-lookup"><span data-stu-id="02b9a-156">From your Device Provisioning service in the Azure portal, click **Certificates**, click the certificate you uploaded for this Quickstart, and click the **Delete** button at the top of the **Certificate Details** window.</span></span>  
 
## <a name="next-steps"></a><span data-ttu-id="02b9a-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="02b9a-157">Next steps</span></span>
<span data-ttu-id="02b9a-158">In this Quickstart, you created a group enrollment for an X.509 intermediate or root CA certificate using the Azure IoT Hub Device Provisioning Service.</span><span class="sxs-lookup"><span data-stu-id="02b9a-158">In this Quickstart, you created a group enrollment for an X.509 intermediate or root CA certificate using the Azure IoT Hub Device Provisioning Service.</span></span> <span data-ttu-id="02b9a-159">To learn about device provisioning in depth, continue to the tutorial for the Device Provisioning Service setup in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="02b9a-159">To learn about device provisioning in depth, continue to the tutorial for the Device Provisioning Service setup in the Azure portal.</span></span> 
 
> [!div class="nextstepaction"]
> [<span data-ttu-id="02b9a-160">Azure IoT Hub Device Provisioning Service tutorials</span><span class="sxs-lookup"><span data-stu-id="02b9a-160">Azure IoT Hub Device Provisioning Service tutorials</span></span>](./tutorial-set-up-cloud.md)