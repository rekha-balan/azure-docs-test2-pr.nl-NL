---
title: This quickstart shows you how to enroll X.509 devices to the Azure Device Provisioning Service using Python | Microsoft Docs
description: In this quickstart, you will enroll X.509 devices to the Azure IoT Hub Device Provisioning Service using using Python
author: wesmc7777
ms.author: wesmc
ms.date: 01/25/2018
ms.topic: quickstart
ms.service: iot-dps
services: iot-dps
manager: timlt
ms.devlang: python
ms.custom: mvc
ms.openlocfilehash: f6c6c4abf80a67c654b17771787ae530461ca3b4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857453"
---
# <a name="quickstart-enroll-x509-devices-to-the-device-provisioning-service-using-python"></a><span data-ttu-id="59b73-103">Quickstart: Enroll X.509 devices to the Device Provisioning Service using Python</span><span class="sxs-lookup"><span data-stu-id="59b73-103">Quickstart: Enroll X.509 devices to the Device Provisioning Service using Python</span></span>

[!INCLUDE [iot-dps-selector-quick-enroll-device-x509](../../includes/iot-dps-selector-quick-enroll-device-x509.md)]

<span data-ttu-id="59b73-104">Devices are enrolled to a provisioning service instance by creating an [Enrollment group](concepts-service.md#enrollment-group), or an [Individual enrollment](concepts-service.md#individual-enrollment).</span><span class="sxs-lookup"><span data-stu-id="59b73-104">Devices are enrolled to a provisioning service instance by creating an [Enrollment group](concepts-service.md#enrollment-group), or an [Individual enrollment](concepts-service.md#individual-enrollment).</span></span> <span data-ttu-id="59b73-105">This quickstart shows how to use Python to programmatically create an [Enrollment group](concepts-service.md#enrollment-group) that uses intermediate or root CA X.509 certificates.</span><span class="sxs-lookup"><span data-stu-id="59b73-105">This quickstart shows how to use Python to programmatically create an [Enrollment group](concepts-service.md#enrollment-group) that uses intermediate or root CA X.509 certificates.</span></span> <span data-ttu-id="59b73-106">An enrollment group controls access to the provisioning service for devices that share a common signing certificate in their certificate chain.</span><span class="sxs-lookup"><span data-stu-id="59b73-106">An enrollment group controls access to the provisioning service for devices that share a common signing certificate in their certificate chain.</span></span> <span data-ttu-id="59b73-107">The enrollment group is created using the [Python Provisioning Service SDK](https://github.com/Azure/azure-iot-sdk-python/tree/master/provisioning_service_client) and a sample Python application.</span><span class="sxs-lookup"><span data-stu-id="59b73-107">The enrollment group is created using the [Python Provisioning Service SDK](https://github.com/Azure/azure-iot-sdk-python/tree/master/provisioning_service_client) and a sample Python application.</span></span> <span data-ttu-id="59b73-108">Creating Individual enrollments using the *Python Provisioning Service SDK* is still a work in progress.</span><span class="sxs-lookup"><span data-stu-id="59b73-108">Creating Individual enrollments using the *Python Provisioning Service SDK* is still a work in progress.</span></span> <span data-ttu-id="59b73-109">To learn more, see [Controlling device access to the provisioning service with X.509 certificates](./concepts-security.md#controlling-device-access-to-the-provisioning-service-with-x509-certificates).</span><span class="sxs-lookup"><span data-stu-id="59b73-109">To learn more, see [Controlling device access to the provisioning service with X.509 certificates](./concepts-security.md#controlling-device-access-to-the-provisioning-service-with-x509-certificates).</span></span> <span data-ttu-id="59b73-110">For more information about using X.509 certificate-based Public Key Infrastructure (PKI) with Azure IoT Hub and Device Provisioning Service, see [X.509 CA certificate security overview](https://docs.microsoft.com/azure/iot-hub/iot-hub-x509ca-overview).</span><span class="sxs-lookup"><span data-stu-id="59b73-110">For more information about using X.509 certificate-based Public Key Infrastructure (PKI) with Azure IoT Hub and Device Provisioning Service, see [X.509 CA certificate security overview](https://docs.microsoft.com/azure/iot-hub/iot-hub-x509ca-overview).</span></span> 

<span data-ttu-id="59b73-111">This quickstart expects you have already created an IoT hub and Device Provisioning Service instance.</span><span class="sxs-lookup"><span data-stu-id="59b73-111">This quickstart expects you have already created an IoT hub and Device Provisioning Service instance.</span></span> <span data-ttu-id="59b73-112">If you have not already created these resources, complete the [Set up IoT Hub Device Provisioning Service with the Azure portal](./quick-setup-auto-provision.md) quickstart before proceeding with this article.</span><span class="sxs-lookup"><span data-stu-id="59b73-112">If you have not already created these resources, complete the [Set up IoT Hub Device Provisioning Service with the Azure portal](./quick-setup-auto-provision.md) quickstart before proceeding with this article.</span></span>

<span data-ttu-id="59b73-113">Although the steps in this article work on both Windows and Linux machines, this article is developed for a Windows development machine.</span><span class="sxs-lookup"><span data-stu-id="59b73-113">Although the steps in this article work on both Windows and Linux machines, this article is developed for a Windows development machine.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]


## <a name="prerequisites"></a><span data-ttu-id="59b73-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="59b73-114">Prerequisites</span></span>

- <span data-ttu-id="59b73-115">Install [Python 2.x or 3.x](https://www.python.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="59b73-115">Install [Python 2.x or 3.x](https://www.python.org/downloads/).</span></span> <span data-ttu-id="59b73-116">Make sure to use the 32-bit or 64-bit installation as required by your setup.</span><span class="sxs-lookup"><span data-stu-id="59b73-116">Make sure to use the 32-bit or 64-bit installation as required by your setup.</span></span> <span data-ttu-id="59b73-117">When prompted during the installation, make sure to add Python to your platform-specific environment variables.</span><span class="sxs-lookup"><span data-stu-id="59b73-117">When prompted during the installation, make sure to add Python to your platform-specific environment variables.</span></span>
- <span data-ttu-id="59b73-118">[Install or upgrade *pip*, the Python package management system](https://pip.pypa.io/en/stable/installing/).</span><span class="sxs-lookup"><span data-stu-id="59b73-118">[Install or upgrade *pip*, the Python package management system](https://pip.pypa.io/en/stable/installing/).</span></span>
- <span data-ttu-id="59b73-119">Install [Git](https://git-scm.com/download/).</span><span class="sxs-lookup"><span data-stu-id="59b73-119">Install [Git](https://git-scm.com/download/).</span></span>



## <a name="prepare-test-certificates"></a><span data-ttu-id="59b73-120">Prepare test certificates</span><span class="sxs-lookup"><span data-stu-id="59b73-120">Prepare test certificates</span></span>

<span data-ttu-id="59b73-121">For this quickstart, you must have a .pem or a .cer file that contains the public portion of an intermediate or root CA X.509 certificate.</span><span class="sxs-lookup"><span data-stu-id="59b73-121">For this quickstart, you must have a .pem or a .cer file that contains the public portion of an intermediate or root CA X.509 certificate.</span></span> <span data-ttu-id="59b73-122">This certificate must be uploaded to your provisioning service, and verified by the service.</span><span class="sxs-lookup"><span data-stu-id="59b73-122">This certificate must be uploaded to your provisioning service, and verified by the service.</span></span> 

<span data-ttu-id="59b73-123">The [Azure IoT C SDK](https://github.com/Azure/azure-iot-sdk-c) contains test tooling that can help you create an X.509 certificate chain, upload a root or intermediate certificate from that chain, and perform proof-of-possession with the service to verify the certificate.</span><span class="sxs-lookup"><span data-stu-id="59b73-123">The [Azure IoT C SDK](https://github.com/Azure/azure-iot-sdk-c) contains test tooling that can help you create an X.509 certificate chain, upload a root or intermediate certificate from that chain, and perform proof-of-possession with the service to verify the certificate.</span></span> <span data-ttu-id="59b73-124">Certificates created with the SDK tooling are designed to be used for **development testing only**.</span><span class="sxs-lookup"><span data-stu-id="59b73-124">Certificates created with the SDK tooling are designed to be used for **development testing only**.</span></span> <span data-ttu-id="59b73-125">These certificates **must not be used in production**.</span><span class="sxs-lookup"><span data-stu-id="59b73-125">These certificates **must not be used in production**.</span></span> <span data-ttu-id="59b73-126">They contain hard-coded passwords ("1234") that expire after 30 days.</span><span class="sxs-lookup"><span data-stu-id="59b73-126">They contain hard-coded passwords ("1234") that expire after 30 days.</span></span> <span data-ttu-id="59b73-127">To learn about obtaining certificates suitable for production use, see [How to get an X.509 CA certificate](https://docs.microsoft.com/azure/iot-hub/iot-hub-x509ca-overview#how-to-get-an-x509-ca-certificate) in the Azure IoT Hub documentation.</span><span class="sxs-lookup"><span data-stu-id="59b73-127">To learn about obtaining certificates suitable for production use, see [How to get an X.509 CA certificate](https://docs.microsoft.com/azure/iot-hub/iot-hub-x509ca-overview#how-to-get-an-x509-ca-certificate) in the Azure IoT Hub documentation.</span></span>

<span data-ttu-id="59b73-128">To use this test tooling to generate certificates, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="59b73-128">To use this test tooling to generate certificates, perform the following steps:</span></span> 
 
1. <span data-ttu-id="59b73-129">Open a command prompt or Git Bash shell, and change to a working folder on your machine.</span><span class="sxs-lookup"><span data-stu-id="59b73-129">Open a command prompt or Git Bash shell, and change to a working folder on your machine.</span></span> <span data-ttu-id="59b73-130">Execute the following command to clone the [Azure IoT C SDK](https://github.com/Azure/azure-iot-sdk-c) GitHub repository:</span><span class="sxs-lookup"><span data-stu-id="59b73-130">Execute the following command to clone the [Azure IoT C SDK](https://github.com/Azure/azure-iot-sdk-c) GitHub repository:</span></span>
    
  ```cmd/sh
  git clone https://github.com/Azure/azure-iot-sdk-c.git --recursive
  ```

  <span data-ttu-id="59b73-131">The size of this repository is currently around 220 MB.</span><span class="sxs-lookup"><span data-stu-id="59b73-131">The size of this repository is currently around 220 MB.</span></span> <span data-ttu-id="59b73-132">You should expect this operation to take several minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="59b73-132">You should expect this operation to take several minutes to complete.</span></span>

  <span data-ttu-id="59b73-133">The test tooling is located in the *azure-iot-sdk-c/tools/CACertificates* of the repository you cloned.</span><span class="sxs-lookup"><span data-stu-id="59b73-133">The test tooling is located in the *azure-iot-sdk-c/tools/CACertificates* of the repository you cloned.</span></span>    

2. <span data-ttu-id="59b73-134">Follow the steps in [Managing test CA certificates for samples and tutorials](https://github.com/Azure/azure-iot-sdk-c/blob/master/tools/CACertificates/CACertificateOverview.md).</span><span class="sxs-lookup"><span data-stu-id="59b73-134">Follow the steps in [Managing test CA certificates for samples and tutorials](https://github.com/Azure/azure-iot-sdk-c/blob/master/tools/CACertificates/CACertificateOverview.md).</span></span> 


## <a name="modify-the-python-sample-code"></a><span data-ttu-id="59b73-135">Modify the Python sample code</span><span class="sxs-lookup"><span data-stu-id="59b73-135">Modify the Python sample code</span></span>

<span data-ttu-id="59b73-136">This section shows how to add the provisioning details of your X.509 device to the sample code.</span><span class="sxs-lookup"><span data-stu-id="59b73-136">This section shows how to add the provisioning details of your X.509 device to the sample code.</span></span> 

1. <span data-ttu-id="59b73-137">Using a text editor, create a new **EnrollmentGroup.py** file.</span><span class="sxs-lookup"><span data-stu-id="59b73-137">Using a text editor, create a new **EnrollmentGroup.py** file.</span></span>

1. <span data-ttu-id="59b73-138">Add the following `import` statements and variables at the start of the **EnrollmentGroup.py** file.</span><span class="sxs-lookup"><span data-stu-id="59b73-138">Add the following `import` statements and variables at the start of the **EnrollmentGroup.py** file.</span></span> <span data-ttu-id="59b73-139">Then replace `dpsConnectionString` with your connection string found under **Shared access policies** in your **Device Provisioning Service** on the **Azure Portal**.</span><span class="sxs-lookup"><span data-stu-id="59b73-139">Then replace `dpsConnectionString` with your connection string found under **Shared access policies** in your **Device Provisioning Service** on the **Azure Portal**.</span></span> <span data-ttu-id="59b73-140">Replace the certificate placeholder with the certificate created previously in [Prepare test certificates](quick-enroll-device-x509-python.md#prepare-test-certificates).</span><span class="sxs-lookup"><span data-stu-id="59b73-140">Replace the certificate placeholder with the certificate created previously in [Prepare test certificates](quick-enroll-device-x509-python.md#prepare-test-certificates).</span></span> <span data-ttu-id="59b73-141">Finally, create a unique `registrationid` and be sure that it only consists of lower-case alphanumerics and hyphens.</span><span class="sxs-lookup"><span data-stu-id="59b73-141">Finally, create a unique `registrationid` and be sure that it only consists of lower-case alphanumerics and hyphens.</span></span>  
   
    ```python
    from provisioningserviceclient import ProvisioningServiceClient
    from provisioningserviceclient.models import EnrollmentGroup, AttestationMechanism

    CONNECTION_STRING = "{dpsConnectionString}"

    SIGNING_CERT = """-----BEGIN CERTIFICATE-----
    XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    -----END CERTIFICATE-----"""

    GROUP_ID = "{registrationid}"
    ```

1. <span data-ttu-id="59b73-142">Add the following function and function call to implement the group enrollment creation:</span><span class="sxs-lookup"><span data-stu-id="59b73-142">Add the following function and function call to implement the group enrollment creation:</span></span>
   
    ```python
    def main():
        print ( "Initiating enrollment group creation..." )

        psc = ProvisioningServiceClient.create_from_connection_string(CONNECTION_STRING)
        att = AttestationMechanism.create_with_x509_signing_certs(SIGNING_CERT)
        eg = EnrollmentGroup.create(GROUP_ID, att)

        eg = psc.create_or_update(eg)
    
        print ( "Enrollment group created." )

    if __name__ == '__main__':
        main()
    ```

1. <span data-ttu-id="59b73-143">Save and close the **EnrollmentGroup.py** file.</span><span class="sxs-lookup"><span data-stu-id="59b73-143">Save and close the **EnrollmentGroup.py** file.</span></span>
 

## <a name="run-the-sample-group-enrollment"></a><span data-ttu-id="59b73-144">Run the sample group enrollment</span><span class="sxs-lookup"><span data-stu-id="59b73-144">Run the sample group enrollment</span></span>

1. <span data-ttu-id="59b73-145">Open a command prompt, and run the following command to install the [azure-iot-provisioning-device-client](https://pypi.org/project/azure-iot-provisioning-device-client).</span><span class="sxs-lookup"><span data-stu-id="59b73-145">Open a command prompt, and run the following command to install the [azure-iot-provisioning-device-client](https://pypi.org/project/azure-iot-provisioning-device-client).</span></span>

    ```cmd/sh
    pip install azure-iothub-provisioningserviceclient    
    ```

2. <span data-ttu-id="59b73-146">In the command prompt, and run the script.</span><span class="sxs-lookup"><span data-stu-id="59b73-146">In the command prompt, and run the script.</span></span>

    ```cmd/sh
    python EnrollmentGroup.py
    ```

3. <span data-ttu-id="59b73-147">Observe the output for the successful enrollment.</span><span class="sxs-lookup"><span data-stu-id="59b73-147">Observe the output for the successful enrollment.</span></span>

4. <span data-ttu-id="59b73-148">Navigate to your provisioning service in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="59b73-148">Navigate to your provisioning service in the Azure portal.</span></span> <span data-ttu-id="59b73-149">Click **Manage enrollments**.</span><span class="sxs-lookup"><span data-stu-id="59b73-149">Click **Manage enrollments**.</span></span> <span data-ttu-id="59b73-150">Notice that your group of X.509 devices appears under the **Enrollment Groups** tab, with the name `registrationid` created earlier.</span><span class="sxs-lookup"><span data-stu-id="59b73-150">Notice that your group of X.509 devices appears under the **Enrollment Groups** tab, with the name `registrationid` created earlier.</span></span> 

    ![Verify successful X.509 enrollment in portal](./media/quick-enroll-device-x509-python/1.png)  


## <a name="clean-up-resources"></a><span data-ttu-id="59b73-152">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="59b73-152">Clean up resources</span></span>
<span data-ttu-id="59b73-153">If you plan to explore the Java service sample, do not clean up the resources created in this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="59b73-153">If you plan to explore the Java service sample, do not clean up the resources created in this Quickstart.</span></span> <span data-ttu-id="59b73-154">If you do not plan to continue, use the following steps to delete all resources created by this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="59b73-154">If you do not plan to continue, use the following steps to delete all resources created by this Quickstart.</span></span>

1. <span data-ttu-id="59b73-155">Close the Java sample output window on your machine.</span><span class="sxs-lookup"><span data-stu-id="59b73-155">Close the Java sample output window on your machine.</span></span>
1. <span data-ttu-id="59b73-156">Close the _X509 Cert Generator_ window on your machine.</span><span class="sxs-lookup"><span data-stu-id="59b73-156">Close the _X509 Cert Generator_ window on your machine.</span></span>
1. <span data-ttu-id="59b73-157">Navigate to your Device Provisioning service in the Azure portal, click **Manage enrollments**, and then select the **Enrollment Groups** tab. Select the *GROUP NAME* for the X.509 devices you enrolled using this Quickstart, and click the **Delete** button at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="59b73-157">Navigate to your Device Provisioning service in the Azure portal, click **Manage enrollments**, and then select the **Enrollment Groups** tab. Select the *GROUP NAME* for the X.509 devices you enrolled using this Quickstart, and click the **Delete** button at the top of the blade.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="59b73-158">Next steps</span><span class="sxs-lookup"><span data-stu-id="59b73-158">Next steps</span></span>
<span data-ttu-id="59b73-159">In this Quickstart, you enrolled a simulated group of X.509 devices to your Device Provisioning service.</span><span class="sxs-lookup"><span data-stu-id="59b73-159">In this Quickstart, you enrolled a simulated group of X.509 devices to your Device Provisioning service.</span></span> <span data-ttu-id="59b73-160">To learn about device provisioning in depth, continue to the tutorial for the Device Provisioning Service setup in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="59b73-160">To learn about device provisioning in depth, continue to the tutorial for the Device Provisioning Service setup in the Azure portal.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="59b73-161">Azure IoT Hub Device Provisioning Service tutorials</span><span class="sxs-lookup"><span data-stu-id="59b73-161">Azure IoT Hub Device Provisioning Service tutorials</span></span>](./tutorial-set-up-cloud.md)
