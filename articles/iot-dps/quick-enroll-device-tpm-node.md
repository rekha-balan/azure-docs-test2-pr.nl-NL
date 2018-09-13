---
title: Enroll TPM device to Azure Device Provisioning Service using Node.js | Microsoft Docs
description: Azure Quickstart - Enroll TPM device to Azure IoT Hub Device Provisioning Service using Node.js service SDK
author: wesmc7777
ms.author: wesmc
ms.date: 12/21/2017
ms.topic: quickstart
ms.service: iot-dps
services: iot-dps
manager: timlt
ms.devlang: nodejs
ms.custom: mvc
ms.openlocfilehash: feec3083ae924cbc87b34912d6aa0ceaa0555a18
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864584"
---
# <a name="enroll-tpm-device-to-iot-hub-device-provisioning-service-using-nodejs-service-sdk"></a><span data-ttu-id="80f13-103">Enroll TPM device to IoT Hub Device Provisioning Service using Node.js service SDK</span><span class="sxs-lookup"><span data-stu-id="80f13-103">Enroll TPM device to IoT Hub Device Provisioning Service using Node.js service SDK</span></span>

[!INCLUDE [iot-dps-selector-quick-enroll-device-tpm](../../includes/iot-dps-selector-quick-enroll-device-tpm.md)]


<span data-ttu-id="80f13-104">These steps show how to programmatically create an individual enrollment for a TPM device in the Azure IoT Hub Device Provisioning Service using the [Node.js Service SDK](https://github.com/Azure/azure-iot-sdk-node) and a sample Node.js application.</span><span class="sxs-lookup"><span data-stu-id="80f13-104">These steps show how to programmatically create an individual enrollment for a TPM device in the Azure IoT Hub Device Provisioning Service using the [Node.js Service SDK](https://github.com/Azure/azure-iot-sdk-node) and a sample Node.js application.</span></span> <span data-ttu-id="80f13-105">You can optionally enroll a simulated TPM device to the provisioning service using this individual enrollment entry.</span><span class="sxs-lookup"><span data-stu-id="80f13-105">You can optionally enroll a simulated TPM device to the provisioning service using this individual enrollment entry.</span></span> <span data-ttu-id="80f13-106">Although these steps will work on both Windows and Linux machines, we will use a Windows development machine for the purpose of this article.</span><span class="sxs-lookup"><span data-stu-id="80f13-106">Although these steps will work on both Windows and Linux machines, we will use a Windows development machine for the purpose of this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80f13-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="80f13-107">Prerequisites</span></span>

- <span data-ttu-id="80f13-108">Make sure to complete the steps in [Set up the IoT Hub Device Provisioning Service with the Azure portal](./quick-setup-auto-provision.md) before you proceed.</span><span class="sxs-lookup"><span data-stu-id="80f13-108">Make sure to complete the steps in [Set up the IoT Hub Device Provisioning Service with the Azure portal](./quick-setup-auto-provision.md) before you proceed.</span></span> 
-  <span data-ttu-id="80f13-109">Make sure you have [Node.js v4.0 or above](https://nodejs.org) installed on your machine.</span><span class="sxs-lookup"><span data-stu-id="80f13-109">Make sure you have [Node.js v4.0 or above](https://nodejs.org) installed on your machine.</span></span>
- <span data-ttu-id="80f13-110">If you want to enroll a simulated device at the end of this Quickstart, follow the steps in [Create and provision a simulated device](quick-create-simulated-device.md) up until the step where you get an endorsement key for the device.</span><span class="sxs-lookup"><span data-stu-id="80f13-110">If you want to enroll a simulated device at the end of this Quickstart, follow the steps in [Create and provision a simulated device](quick-create-simulated-device.md) up until the step where you get an endorsement key for the device.</span></span> <span data-ttu-id="80f13-111">Note down the endorsement key, you will use it later in this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="80f13-111">Note down the endorsement key, you will use it later in this Quickstart.</span></span> <span data-ttu-id="80f13-112">**Do not follow the steps to create an individual enrollment using the Azure portal.**</span><span class="sxs-lookup"><span data-stu-id="80f13-112">**Do not follow the steps to create an individual enrollment using the Azure portal.**</span></span>
 
## <a name="create-the-individual-enrollment-sample"></a><span data-ttu-id="80f13-113">Create the individual enrollment sample</span><span class="sxs-lookup"><span data-stu-id="80f13-113">Create the individual enrollment sample</span></span> 

 
1. <span data-ttu-id="80f13-114">From a command window in your working folder, run:</span><span class="sxs-lookup"><span data-stu-id="80f13-114">From a command window in your working folder, run:</span></span>
  
    ```cmd\sh
    npm install azure-iot-provisioning-service
    ```  

2. <span data-ttu-id="80f13-115">Using a text editor, create a **create_individual_enrollment.js** file in your working folder.</span><span class="sxs-lookup"><span data-stu-id="80f13-115">Using a text editor, create a **create_individual_enrollment.js** file in your working folder.</span></span> <span data-ttu-id="80f13-116">Add the following code to the file and save:</span><span class="sxs-lookup"><span data-stu-id="80f13-116">Add the following code to the file and save:</span></span>

    ```
    'use strict';

    var provisioningServiceClient = require('azure-iot-provisioning-service').ProvisioningServiceClient;

    var serviceClient = provisioningServiceClient.fromConnectionString(process.argv[2]);
    var endorsementKey = process.argv[3];

    var enrollment = {
      registrationId: 'first',
      attestation: {
        type: 'tpm',
        tpm: {
          endorsementKey: endorsementKey
        }
      }
    };

    serviceClient.createOrUpdateIndividualEnrollment(enrollment, function(err, enrollmentResponse) {
      if (err) {
        console.log('error creating the individual enrollment: ' + err);
      } else {
        console.log("enrollment record returned: " + JSON.stringify(enrollmentResponse, null, 2));
      }
    });
    ````

## <a name="run-the-individual-enrollment-sample"></a><span data-ttu-id="80f13-117">Run the individual enrollment sample</span><span class="sxs-lookup"><span data-stu-id="80f13-117">Run the individual enrollment sample</span></span>
  
1. <span data-ttu-id="80f13-118">To run the sample, you need the connection string for your provisioning service.</span><span class="sxs-lookup"><span data-stu-id="80f13-118">To run the sample, you need the connection string for your provisioning service.</span></span> 
    1. <span data-ttu-id="80f13-119">Log in to the Azure portal, click on the **All resources** button on the left-hand menu and open your Device Provisioning service.</span><span class="sxs-lookup"><span data-stu-id="80f13-119">Log in to the Azure portal, click on the **All resources** button on the left-hand menu and open your Device Provisioning service.</span></span> 
    2. <span data-ttu-id="80f13-120">Click **Shared access policies**, then click the access policy you want to use to open its properties.</span><span class="sxs-lookup"><span data-stu-id="80f13-120">Click **Shared access policies**, then click the access policy you want to use to open its properties.</span></span> <span data-ttu-id="80f13-121">In the **Access Policy** window, copy and note down the primary key connection string.</span><span class="sxs-lookup"><span data-stu-id="80f13-121">In the **Access Policy** window, copy and note down the primary key connection string.</span></span> 

    ![Get provisioning service connection string from the portal](./media/quick-enroll-device-tpm-node/get-service-connection-string.png) 


2. <span data-ttu-id="80f13-123">You also need the endorsement key for your device.</span><span class="sxs-lookup"><span data-stu-id="80f13-123">You also need the endorsement key for your device.</span></span> <span data-ttu-id="80f13-124">If you have followed the [Create and provision a simulated device](quick-create-simulated-device.md) quickstart to create a simulated TPM device, use the key created for that device.</span><span class="sxs-lookup"><span data-stu-id="80f13-124">If you have followed the [Create and provision a simulated device](quick-create-simulated-device.md) quickstart to create a simulated TPM device, use the key created for that device.</span></span> <span data-ttu-id="80f13-125">Otherwise, to create a sample individual enrollment, you can use the following endorsement key supplied with the SDK:</span><span class="sxs-lookup"><span data-stu-id="80f13-125">Otherwise, to create a sample individual enrollment, you can use the following endorsement key supplied with the SDK:</span></span>

    ```
    AToAAQALAAMAsgAgg3GXZ0SEs/gakMyNRqXXJP1S124GUgtk8qHaGzMUaaoABgCAAEMAEAgAAAAAAAEAxsj2gUScTk1UjuioeTlfGYZrrimExB+bScH75adUMRIi2UOMxG1kw4y+9RW/IVoMl4e620VxZad0ARX2gUqVjYO7KPVt3dyKhZS3dkcvfBisBhP1XH9B33VqHG9SHnbnQXdBUaCgKAfxome8UmBKfe+naTsE5fkvjb/do3/dD6l4sGBwFCnKRdln4XpM03zLpoHFao8zOwt8l/uP3qUIxmCYv9A7m69Ms+5/pCkTu/rK4mRDsfhZ0QLfbzVI6zQFOKF/rwsfBtFeWlWtcuJMKlXdD8TXWElTzgh7JS4qhFzreL0c1mI0GCj+Aws0usZh7dLIVPnlgZcBhgy1SSDQMQ==
    ```

3. <span data-ttu-id="80f13-126">To create an individual enrollment for your TPM device, run the following command (include the quotes around the command arguments):</span><span class="sxs-lookup"><span data-stu-id="80f13-126">To create an individual enrollment for your TPM device, run the following command (include the quotes around the command arguments):</span></span>
 
     ```cmd\sh
     node create_individual_enrollment.js "<the connection string for your provisioning service>" "<endorsement key>"
     ```
 
3. <span data-ttu-id="80f13-127">On successful creation, the command window displays the properties of the new individual enrollment.</span><span class="sxs-lookup"><span data-stu-id="80f13-127">On successful creation, the command window displays the properties of the new individual enrollment.</span></span>

    ![Enrollment properties in the command output](./media/quick-enroll-device-tpm-node/output.png) 

4. <span data-ttu-id="80f13-129">Verify that an individual enrollment has been created.</span><span class="sxs-lookup"><span data-stu-id="80f13-129">Verify that an individual enrollment has been created.</span></span> <span data-ttu-id="80f13-130">In the Azure portal, on the Device Provisioning Service summary blade, select **Manage enrollments**.</span><span class="sxs-lookup"><span data-stu-id="80f13-130">In the Azure portal, on the Device Provisioning Service summary blade, select **Manage enrollments**.</span></span> <span data-ttu-id="80f13-131">Select the **Individual Enrollments** tab and click the new enrollment entry (*first*) to verify the endorsement key and other properties for the entry.</span><span class="sxs-lookup"><span data-stu-id="80f13-131">Select the **Individual Enrollments** tab and click the new enrollment entry (*first*) to verify the endorsement key and other properties for the entry.</span></span>

    ![Enrollment properties in the portal](./media/quick-enroll-device-tpm-node/verify-enrollment-portal.png) 
 
<span data-ttu-id="80f13-133">Now that you've created an individual enrollment for a TPM device, if you want to enroll a simulated device, you can continue with the remaining steps in [Create and provision a simulated device](quick-create-simulated-device.md).</span><span class="sxs-lookup"><span data-stu-id="80f13-133">Now that you've created an individual enrollment for a TPM device, if you want to enroll a simulated device, you can continue with the remaining steps in [Create and provision a simulated device](quick-create-simulated-device.md).</span></span> <span data-ttu-id="80f13-134">Be sure to skip the steps to create an individual enrollment using the Azure portal in that Quickstart.</span><span class="sxs-lookup"><span data-stu-id="80f13-134">Be sure to skip the steps to create an individual enrollment using the Azure portal in that Quickstart.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="80f13-135">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="80f13-135">Clean up resources</span></span>
<span data-ttu-id="80f13-136">If you plan to explore the Node.js service samples, do not clean up the resources created in this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="80f13-136">If you plan to explore the Node.js service samples, do not clean up the resources created in this Quickstart.</span></span> <span data-ttu-id="80f13-137">If you do not plan to continue, use the following steps to delete all resources created by this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="80f13-137">If you do not plan to continue, use the following steps to delete all resources created by this Quickstart.</span></span>

1. <span data-ttu-id="80f13-138">Close the Node.js sample output window on your machine.</span><span class="sxs-lookup"><span data-stu-id="80f13-138">Close the Node.js sample output window on your machine.</span></span>
1. <span data-ttu-id="80f13-139">If you created a simulated TPM device, close the TPM simulator window.</span><span class="sxs-lookup"><span data-stu-id="80f13-139">If you created a simulated TPM device, close the TPM simulator window.</span></span>
2. <span data-ttu-id="80f13-140">Navigate to your Device Provisioning service in the Azure portal, click **Manage enrollments** and then select the **Individual Enrollments** tab. Select the *Registration ID* for the enrollment entry you created using this Quickstart, and click the **Delete** button at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="80f13-140">Navigate to your Device Provisioning service in the Azure portal, click **Manage enrollments** and then select the **Individual Enrollments** tab. Select the *Registration ID* for the enrollment entry you created using this Quickstart, and click the **Delete** button at the top of the blade.</span></span> 
 
## <a name="next-steps"></a><span data-ttu-id="80f13-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="80f13-141">Next steps</span></span>
<span data-ttu-id="80f13-142">In this Quickstart, you’ve programmatically created an individual enrollment entry for a TPM device, and, optionally, created a TPM simulated device on your machine and provisioned it to your IoT hub using the Azure IoT Hub Device Provisioning Service.</span><span class="sxs-lookup"><span data-stu-id="80f13-142">In this Quickstart, you’ve programmatically created an individual enrollment entry for a TPM device, and, optionally, created a TPM simulated device on your machine and provisioned it to your IoT hub using the Azure IoT Hub Device Provisioning Service.</span></span> <span data-ttu-id="80f13-143">To learn about device provisioning in depth, continue to the tutorial for the Device Provisioning Service setup in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="80f13-143">To learn about device provisioning in depth, continue to the tutorial for the Device Provisioning Service setup in the Azure portal.</span></span> 
 
> [!div class="nextstepaction"]
> [<span data-ttu-id="80f13-144">Azure IoT Hub Device Provisioning Service tutorials</span><span class="sxs-lookup"><span data-stu-id="80f13-144">Azure IoT Hub Device Provisioning Service tutorials</span></span>](./tutorial-set-up-cloud.md)