---
title: Enroll TPM device to Azure Device Provisioning Service using Python | Microsoft Docs
description: Azure Quickstart - Enroll TPM device to Azure IoT Hub Device Provisioning Service using Python provisioning service SDK
author: wesmc7777
ms.author: wesmc
ms.date: 01/26/2018
ms.topic: quickstart
ms.service: iot-dps
services: iot-dps
manager: timlt
ms.devlang: python
ms.custom: mvc
ms.openlocfilehash: ff6200abd88144a530a243b508fd4878126fdb4b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866971"
---
# <a name="enroll-tpm-device-to-iot-hub-device-provisioning-service-using-python-provisioning-service-sdk"></a><span data-ttu-id="b4fd3-103">Enroll TPM device to IoT Hub Device Provisioning Service using Python provisioning service SDK</span><span class="sxs-lookup"><span data-stu-id="b4fd3-103">Enroll TPM device to IoT Hub Device Provisioning Service using Python provisioning service SDK</span></span>
[!INCLUDE [iot-dps-selector-quick-enroll-device-tpm](../../includes/iot-dps-selector-quick-enroll-device-tpm.md)]

<span data-ttu-id="b4fd3-104">These steps show how to programmatically create an individual enrollment for a TPM device in the Azure IoT Hub Device Provisioning Service, using the [Python Provisioning Service SDK](https://github.com/Azure/azure-iot-sdk-python/tree/master/provisioning_service_client) with the help of a sample Python application.</span><span class="sxs-lookup"><span data-stu-id="b4fd3-104">These steps show how to programmatically create an individual enrollment for a TPM device in the Azure IoT Hub Device Provisioning Service, using the [Python Provisioning Service SDK](https://github.com/Azure/azure-iot-sdk-python/tree/master/provisioning_service_client) with the help of a sample Python application.</span></span> <span data-ttu-id="b4fd3-105">Although the Python Service SDK works on both Windows and Linux machines, this article uses a Windows development machine to walk through the enrollment process.</span><span class="sxs-lookup"><span data-stu-id="b4fd3-105">Although the Python Service SDK works on both Windows and Linux machines, this article uses a Windows development machine to walk through the enrollment process.</span></span>

<span data-ttu-id="b4fd3-106">Make sure to [set up IoT Hub Device Provisioning Service with the Azure portal](./quick-setup-auto-provision.md) before you proceed.</span><span class="sxs-lookup"><span data-stu-id="b4fd3-106">Make sure to [set up IoT Hub Device Provisioning Service with the Azure portal](./quick-setup-auto-provision.md) before you proceed.</span></span>


<a id="prepareenvironment"></a>

## <a name="prepare-the-environment"></a><span data-ttu-id="b4fd3-107">Prepare the environment</span><span class="sxs-lookup"><span data-stu-id="b4fd3-107">Prepare the environment</span></span> 

1. <span data-ttu-id="b4fd3-108">Download and install [Python 2.x or 3.x](https://www.python.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="b4fd3-108">Download and install [Python 2.x or 3.x](https://www.python.org/downloads/).</span></span> <span data-ttu-id="b4fd3-109">Make sure to use the 32-bit or 64-bit installation as required by your setup.</span><span class="sxs-lookup"><span data-stu-id="b4fd3-109">Make sure to use the 32-bit or 64-bit installation as required by your setup.</span></span> <span data-ttu-id="b4fd3-110">When prompted during the installation, make sure to add Python to your platform-specific environment variables.</span><span class="sxs-lookup"><span data-stu-id="b4fd3-110">When prompted during the installation, make sure to add Python to your platform-specific environment variables.</span></span> 

1. <span data-ttu-id="b4fd3-111">Choose one of the following options:</span><span class="sxs-lookup"><span data-stu-id="b4fd3-111">Choose one of the following options:</span></span>

    - <span data-ttu-id="b4fd3-112">Build and compile the **Azure IoT Python SDK**.</span><span class="sxs-lookup"><span data-stu-id="b4fd3-112">Build and compile the **Azure IoT Python SDK**.</span></span> <span data-ttu-id="b4fd3-113">Follow [these instructions](https://github.com/Azure/azure-iot-sdk-python/blob/master/doc/python-devbox-setup.md) to build the Python packages.</span><span class="sxs-lookup"><span data-stu-id="b4fd3-113">Follow [these instructions](https://github.com/Azure/azure-iot-sdk-python/blob/master/doc/python-devbox-setup.md) to build the Python packages.</span></span> <span data-ttu-id="b4fd3-114">If you are using Windows OS, then also install [Visual C++ redistributable package](http://www.microsoft.com/download/confirmation.aspx?id=48145) to allow the use of native DLLs from Python.</span><span class="sxs-lookup"><span data-stu-id="b4fd3-114">If you are using Windows OS, then also install [Visual C++ redistributable package](http://www.microsoft.com/download/confirmation.aspx?id=48145) to allow the use of native DLLs from Python.</span></span>

    - <span data-ttu-id="b4fd3-115">[Install or upgrade *pip*, the Python package management system](https://pip.pypa.io/en/stable/installing/) and install the package via the following command:</span><span class="sxs-lookup"><span data-stu-id="b4fd3-115">[Install or upgrade *pip*, the Python package management system](https://pip.pypa.io/en/stable/installing/) and install the package via the following command:</span></span>

        ```cmd/sh
        pip install azure-iothub-provisioningserviceclient
        ```

1. <span data-ttu-id="b4fd3-116">You need the endorsement key for your device.</span><span class="sxs-lookup"><span data-stu-id="b4fd3-116">You need the endorsement key for your device.</span></span> <span data-ttu-id="b4fd3-117">If you have followed the [Create and provision a simulated device](quick-create-simulated-device.md) quickstart to create a simulated TPM device, use the key created for that device.</span><span class="sxs-lookup"><span data-stu-id="b4fd3-117">If you have followed the [Create and provision a simulated device](quick-create-simulated-device.md) quickstart to create a simulated TPM device, use the key created for that device.</span></span> <span data-ttu-id="b4fd3-118">Otherwise, you can use the following endorsement key supplied with the SDK:</span><span class="sxs-lookup"><span data-stu-id="b4fd3-118">Otherwise, you can use the following endorsement key supplied with the SDK:</span></span>

    ```
    AToAAQALAAMAsgAgg3GXZ0SEs/gakMyNRqXXJP1S124GUgtk8qHaGzMUaaoABgCAAEMAEAgAAAAAAAEAtW6MOyCu/Nih47atIIoZtlYkhLeCTiSrtRN3q6hqgOllA979No4BOcDWF90OyzJvjQknMfXS/Dx/IJIBnORgCg1YX/j4EEtO7Ase29Xd63HjvG8M94+u2XINu79rkTxeueqW7gPeRZQPnl1xYmqawYcyzJS6GKWKdoIdS+UWu6bJr58V3xwvOQI4NibXKD7htvz07jLItWTFhsWnTdZbJ7PnmfCa2vbRH/9pZIow+CcAL9mNTNNN4FdzYwapNVO+6SY/W4XU0Q+dLMCKYarqVNH5GzAWDfKT8nKzg69yQejJM8oeUWag/8odWOfbszA+iFjw3wVNrA5n8grUieRkPQ==
    ```


## <a name="modify-the-python-sample-code"></a><span data-ttu-id="b4fd3-119">Modify the Python sample code</span><span class="sxs-lookup"><span data-stu-id="b4fd3-119">Modify the Python sample code</span></span>

<span data-ttu-id="b4fd3-120">This section shows how to add the provisioning details of your TPM device to the sample code.</span><span class="sxs-lookup"><span data-stu-id="b4fd3-120">This section shows how to add the provisioning details of your TPM device to the sample code.</span></span> 

1. <span data-ttu-id="b4fd3-121">Using a text editor, create a new **TpmEnrollment.py** file.</span><span class="sxs-lookup"><span data-stu-id="b4fd3-121">Using a text editor, create a new **TpmEnrollment.py** file.</span></span>

1. <span data-ttu-id="b4fd3-122">Add the following `import` statements and variables at the start of the **TpmEnrollment.py** file.</span><span class="sxs-lookup"><span data-stu-id="b4fd3-122">Add the following `import` statements and variables at the start of the **TpmEnrollment.py** file.</span></span> <span data-ttu-id="b4fd3-123">Then replace `dpsConnectionString` with your connection string found under **Shared access policies** in your **Device Provisioning Service** on the **Azure Portal**.</span><span class="sxs-lookup"><span data-stu-id="b4fd3-123">Then replace `dpsConnectionString` with your connection string found under **Shared access policies** in your **Device Provisioning Service** on the **Azure Portal**.</span></span> <span data-ttu-id="b4fd3-124">Replace `endorsementKey` with the value noted previously in [Prepare the environment](quick-enroll-device-tpm-python.md#prepareenvironment).</span><span class="sxs-lookup"><span data-stu-id="b4fd3-124">Replace `endorsementKey` with the value noted previously in [Prepare the environment](quick-enroll-device-tpm-python.md#prepareenvironment).</span></span> <span data-ttu-id="b4fd3-125">Finally, create a unique `registrationid` and be sure that it only consists of lower-case alphanumerics and hyphens.</span><span class="sxs-lookup"><span data-stu-id="b4fd3-125">Finally, create a unique `registrationid` and be sure that it only consists of lower-case alphanumerics and hyphens.</span></span>  
   
    ```python
    from provisioningserviceclient import ProvisioningServiceClient
    from provisioningserviceclient.models import IndividualEnrollment, AttestationMechanism

    CONNECTION_STRING = "{dpsConnectionString}"

    ENDORSEMENT_KEY = "{endorsementKey}"

    REGISTRATION_ID = "{registrationid}"
    ```

1. <span data-ttu-id="b4fd3-126">Add the following function and function call to implement the group enrollment creation:</span><span class="sxs-lookup"><span data-stu-id="b4fd3-126">Add the following function and function call to implement the group enrollment creation:</span></span>
   
    ```python
    def main():
        print ( "Starting individual enrollment..." )

        psc = ProvisioningServiceClient.create_from_connection_string(CONNECTION_STRING)

        att = AttestationMechanism.create_with_tpm(ENDORSEMENT_KEY)
        ie = IndividualEnrollment.create(REGISTRATION_ID, att)

        ie = psc.create_or_update(ie)
    
        print ( "Individual enrollment successful." )
    
    if __name__ == '__main__':
        main()
    ```

1. <span data-ttu-id="b4fd3-127">Save and close the **TpmEnrollment.py** file.</span><span class="sxs-lookup"><span data-stu-id="b4fd3-127">Save and close the **TpmEnrollment.py** file.</span></span>
 

## <a name="run-the-sample-tpm-enrollment"></a><span data-ttu-id="b4fd3-128">Run the sample TPM enrollment</span><span class="sxs-lookup"><span data-stu-id="b4fd3-128">Run the sample TPM enrollment</span></span>

1. <span data-ttu-id="b4fd3-129">Open a command prompt, and run the script.</span><span class="sxs-lookup"><span data-stu-id="b4fd3-129">Open a command prompt, and run the script.</span></span>

    ```cmd/sh
    python TpmEnrollment.py
    ```

1. <span data-ttu-id="b4fd3-130">Observe the output for the successful enrollment.</span><span class="sxs-lookup"><span data-stu-id="b4fd3-130">Observe the output for the successful enrollment.</span></span>

1. <span data-ttu-id="b4fd3-131">Navigate to your provisioning service in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b4fd3-131">Navigate to your provisioning service in the Azure portal.</span></span> <span data-ttu-id="b4fd3-132">Click **Manage enrollments**.</span><span class="sxs-lookup"><span data-stu-id="b4fd3-132">Click **Manage enrollments**.</span></span> <span data-ttu-id="b4fd3-133">Notice that your TPM device appears under the **Individual Enrollments** tab, with the name `registrationid` created earlier.</span><span class="sxs-lookup"><span data-stu-id="b4fd3-133">Notice that your TPM device appears under the **Individual Enrollments** tab, with the name `registrationid` created earlier.</span></span> 

    ![Verify successful TPM enrollment in portal](./media/quick-enroll-device-tpm-python/1.png)  


## <a name="clean-up-resources"></a><span data-ttu-id="b4fd3-135">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="b4fd3-135">Clean up resources</span></span>
<span data-ttu-id="b4fd3-136">If you plan to explore the Java service sample, do not clean up the resources created in this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="b4fd3-136">If you plan to explore the Java service sample, do not clean up the resources created in this Quickstart.</span></span> <span data-ttu-id="b4fd3-137">If you do not plan to continue, use the following steps to delete all resources created by this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="b4fd3-137">If you do not plan to continue, use the following steps to delete all resources created by this Quickstart.</span></span>

1. <span data-ttu-id="b4fd3-138">Close the Python sample output window on your machine.</span><span class="sxs-lookup"><span data-stu-id="b4fd3-138">Close the Python sample output window on your machine.</span></span>
1. <span data-ttu-id="b4fd3-139">If you created a simulated TPM device, close the TPM simulator window.</span><span class="sxs-lookup"><span data-stu-id="b4fd3-139">If you created a simulated TPM device, close the TPM simulator window.</span></span>
1. <span data-ttu-id="b4fd3-140">Navigate to your Device Provisioning service in the Azure portal, click **Manage enrollments** and then select the **Individual Enrollments** tab. Select the *Registration ID* for the enrollment entry you created using this Quickstart, and click the **Delete** button at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="b4fd3-140">Navigate to your Device Provisioning service in the Azure portal, click **Manage enrollments** and then select the **Individual Enrollments** tab. Select the *Registration ID* for the enrollment entry you created using this Quickstart, and click the **Delete** button at the top of the blade.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="b4fd3-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="b4fd3-141">Next steps</span></span>
<span data-ttu-id="b4fd3-142">In this Quickstart, you’ve programmatically created an individual enrollment entry for a TPM device, and, optionally, created a TPM simulated device on your machine and provisioned it to your IoT hub using the Azure IoT Hub Device Provisioning Service.</span><span class="sxs-lookup"><span data-stu-id="b4fd3-142">In this Quickstart, you’ve programmatically created an individual enrollment entry for a TPM device, and, optionally, created a TPM simulated device on your machine and provisioned it to your IoT hub using the Azure IoT Hub Device Provisioning Service.</span></span> <span data-ttu-id="b4fd3-143">To learn about device provisioning in depth, continue to the tutorial for the Device Provisioning Service setup in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b4fd3-143">To learn about device provisioning in depth, continue to the tutorial for the Device Provisioning Service setup in the Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b4fd3-144">Azure IoT Hub Device Provisioning Service tutorials</span><span class="sxs-lookup"><span data-stu-id="b4fd3-144">Azure IoT Hub Device Provisioning Service tutorials</span></span>](./tutorial-set-up-cloud.md)
