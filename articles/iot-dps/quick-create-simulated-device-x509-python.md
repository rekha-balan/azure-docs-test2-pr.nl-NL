---
title: Provision a simulated X.509  device to Azure IoT Hub using Python | Microsoft Docs
description: Azure Quickstart - Create and provision a simulated X.509 device using Python device SDK for IoT Hub Device Provisioning Service
author: wesmc7777
ms.author: wesmc
ms.date: 12/21/2017
ms.topic: quickstart
ms.service: iot-dps
services: iot-dps
manager: timlt
ms.devlang: python
ms.custom: mvc
ms.openlocfilehash: 0a515a81d2d114e9a9386127b5ef4dd608984483
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868624"
---
# <a name="create-and-provision-a-simulated-x509-device-using-python-device-sdk-for-iot-hub-device-provisioning-service"></a><span data-ttu-id="cf2ca-103">Create and provision a simulated X.509 device using Python device SDK for IoT Hub Device Provisioning Service</span><span class="sxs-lookup"><span data-stu-id="cf2ca-103">Create and provision a simulated X.509 device using Python device SDK for IoT Hub Device Provisioning Service</span></span>
[!INCLUDE [iot-dps-selector-quick-create-simulated-device-x509](../../includes/iot-dps-selector-quick-create-simulated-device-x509.md)]

<span data-ttu-id="cf2ca-104">These steps show how to simulate an X.509 device on your development machine running Windows OS, and use a Python code sample to connect this simulated device with the Device Provisioning Service and your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-104">These steps show how to simulate an X.509 device on your development machine running Windows OS, and use a Python code sample to connect this simulated device with the Device Provisioning Service and your IoT hub.</span></span> 

<span data-ttu-id="cf2ca-105">If you're unfamiliar with the process of auto-provisioning, be sure to also review [Auto-provisioning concepts](concepts-auto-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="cf2ca-105">If you're unfamiliar with the process of auto-provisioning, be sure to also review [Auto-provisioning concepts](concepts-auto-provisioning.md).</span></span> <span data-ttu-id="cf2ca-106">Also make sure you've completed the steps in [Set up IoT Hub Device Provisioning Service with the Azure portal](./quick-setup-auto-provision.md) before continuing.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-106">Also make sure you've completed the steps in [Set up IoT Hub Device Provisioning Service with the Azure portal](./quick-setup-auto-provision.md) before continuing.</span></span> 

[!INCLUDE [IoT Device Provisioning Service basic](../../includes/iot-dps-basic.md)]

## <a name="prepare-the-environment"></a><span data-ttu-id="cf2ca-107">Prepare the environment</span><span class="sxs-lookup"><span data-stu-id="cf2ca-107">Prepare the environment</span></span> 

1. <span data-ttu-id="cf2ca-108">Make sure you have either [Visual Studio 2015](https://www.visualstudio.com/vs/older-downloads/) or [Visual Studio 2017](https://www.visualstudio.com/vs/) installed on your machine.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-108">Make sure you have either [Visual Studio 2015](https://www.visualstudio.com/vs/older-downloads/) or [Visual Studio 2017](https://www.visualstudio.com/vs/) installed on your machine.</span></span> <span data-ttu-id="cf2ca-109">You must have 'Desktop development with C++' workload enabled for your Visual Studio installation.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-109">You must have 'Desktop development with C++' workload enabled for your Visual Studio installation.</span></span>

2. <span data-ttu-id="cf2ca-110">Download and install the [CMake build system](https://cmake.org/download/).</span><span class="sxs-lookup"><span data-stu-id="cf2ca-110">Download and install the [CMake build system](https://cmake.org/download/).</span></span>

3. <span data-ttu-id="cf2ca-111">Make sure `git` is installed on your machine and is added to the environment variables accessible to the command window.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-111">Make sure `git` is installed on your machine and is added to the environment variables accessible to the command window.</span></span> <span data-ttu-id="cf2ca-112">See [Software Freedom Conservancy's Git client tools](https://git-scm.com/download/) for the latest version of `git` tools to install, which includes the **Git Bash**, the command-line app that you can use to interact with your local Git repository.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-112">See [Software Freedom Conservancy's Git client tools](https://git-scm.com/download/) for the latest version of `git` tools to install, which includes the **Git Bash**, the command-line app that you can use to interact with your local Git repository.</span></span> 

4. <span data-ttu-id="cf2ca-113">Open a command prompt or Git Bash.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-113">Open a command prompt or Git Bash.</span></span> <span data-ttu-id="cf2ca-114">Clone the GitHub repo for device simulation code sample.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-114">Clone the GitHub repo for device simulation code sample.</span></span>
    
    ```cmd/sh
    git clone https://github.com/Azure/azure-iot-sdk-python.git --recursive
    ```

5. <span data-ttu-id="cf2ca-115">Create a folder in your local copy of this GitHub repo for CMake build process.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-115">Create a folder in your local copy of this GitHub repo for CMake build process.</span></span> 

    ```cmd/sh
    cd azure-iot-sdk-python/c
    mkdir cmake
    cd cmake
    ```

6. <span data-ttu-id="cf2ca-116">Run the following command to create the Visual Studio solution for the provisioning client.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-116">Run the following command to create the Visual Studio solution for the provisioning client.</span></span>

    ```cmd/sh
    cmake -Duse_prov_client:BOOL=ON ..
    ```


## <a name="create-a-self-signed-x509-device-certificate-and-individual-enrollment-entry"></a><span data-ttu-id="cf2ca-117">Create a self-signed X.509 device certificate and individual enrollment entry</span><span class="sxs-lookup"><span data-stu-id="cf2ca-117">Create a self-signed X.509 device certificate and individual enrollment entry</span></span>

<span data-ttu-id="cf2ca-118">In this section you, will use a self-signed X.509 certificate.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-118">In this section you, will use a self-signed X.509 certificate.</span></span> <span data-ttu-id="cf2ca-119">It is important to keep in mind the following points:</span><span class="sxs-lookup"><span data-stu-id="cf2ca-119">It is important to keep in mind the following points:</span></span>

* <span data-ttu-id="cf2ca-120">Self-signed certificates are for testing only, and should not be used in production.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-120">Self-signed certificates are for testing only, and should not be used in production.</span></span>
* <span data-ttu-id="cf2ca-121">The default expiration date for a self-signed certificate is one year.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-121">The default expiration date for a self-signed certificate is one year.</span></span>

<span data-ttu-id="cf2ca-122">You will use sample code from the Azure IoT C SDK to create the certificate to be used with the individual enrollment entry for the simulated device.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-122">You will use sample code from the Azure IoT C SDK to create the certificate to be used with the individual enrollment entry for the simulated device.</span></span>

1. <span data-ttu-id="cf2ca-123">Open the solution generated in the *cmake* folder named `azure_iot_sdks.sln`, and build it in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-123">Open the solution generated in the *cmake* folder named `azure_iot_sdks.sln`, and build it in Visual Studio.</span></span>

2. <span data-ttu-id="cf2ca-124">Right-click the **dice\_device\_enrollment** project under the **Provision\_Tools** folder, and select **Set as Startup Project**.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-124">Right-click the **dice\_device\_enrollment** project under the **Provision\_Tools** folder, and select **Set as Startup Project**.</span></span> <span data-ttu-id="cf2ca-125">Run the solution.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-125">Run the solution.</span></span> 

3. <span data-ttu-id="cf2ca-126">In the output window, enter `i` for individual enrollment when prompted.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-126">In the output window, enter `i` for individual enrollment when prompted.</span></span> <span data-ttu-id="cf2ca-127">The output window displays a locally generated X.509 certificate for your simulated device.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-127">The output window displays a locally generated X.509 certificate for your simulated device.</span></span> 
    
    <span data-ttu-id="cf2ca-128">Copy the first certificate to clipboard.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-128">Copy the first certificate to clipboard.</span></span> <span data-ttu-id="cf2ca-129">Begin with the first occurrence of:</span><span class="sxs-lookup"><span data-stu-id="cf2ca-129">Begin with the first occurrence of:</span></span>
    
        -----BEGIN CERTIFICATE----- 
        
    <span data-ttu-id="cf2ca-130">End you copying after the first occurrence of:</span><span class="sxs-lookup"><span data-stu-id="cf2ca-130">End you copying after the first occurrence of:</span></span>
    
        -----END CERTIFICATE-----
        
    <span data-ttu-id="cf2ca-131">Make sure to include both of those lines as well.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-131">Make sure to include both of those lines as well.</span></span> 

    ![Dice device enrollment application](./media/python-quick-create-simulated-device-x509/dice-device-enrollment.png)
 
4. <span data-ttu-id="cf2ca-133">Create a file named **_X509testcertificate.pem_** on your Windows machine, open it in an editor of your choice, and copy the clipboard contents to this file.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-133">Create a file named **_X509testcertificate.pem_** on your Windows machine, open it in an editor of your choice, and copy the clipboard contents to this file.</span></span> <span data-ttu-id="cf2ca-134">Save the file.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-134">Save the file.</span></span> 

5. <span data-ttu-id="cf2ca-135">Sign in to the Azure portal, click on the **All resources** button on the left-hand menu and open your provisioning service.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-135">Sign in to the Azure portal, click on the **All resources** button on the left-hand menu and open your provisioning service.</span></span>

6. <span data-ttu-id="cf2ca-136">On the Device Provisioning Service summary blade, select **Manage enrollments**.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-136">On the Device Provisioning Service summary blade, select **Manage enrollments**.</span></span> <span data-ttu-id="cf2ca-137">Select **Individual Enrollments** tab and click the **Add** button at the top.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-137">Select **Individual Enrollments** tab and click the **Add** button at the top.</span></span> 

7. <span data-ttu-id="cf2ca-138">Under the **Add enrollment** panel, enter the following information:</span><span class="sxs-lookup"><span data-stu-id="cf2ca-138">Under the **Add enrollment** panel, enter the following information:</span></span>
    - <span data-ttu-id="cf2ca-139">Select **X.509** as the identity attestation *Mechanism*.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-139">Select **X.509** as the identity attestation *Mechanism*.</span></span>
    - <span data-ttu-id="cf2ca-140">Under the *Primary certificate .pem or .cer file*, click *Select a file* to select the certificate file **X509testcertificate.pem** created in the previous steps.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-140">Under the *Primary certificate .pem or .cer file*, click *Select a file* to select the certificate file **X509testcertificate.pem** created in the previous steps.</span></span>
    - <span data-ttu-id="cf2ca-141">Optionally, you may provide the following information:</span><span class="sxs-lookup"><span data-stu-id="cf2ca-141">Optionally, you may provide the following information:</span></span>
      - <span data-ttu-id="cf2ca-142">Select an IoT hub linked with your provisioning service.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-142">Select an IoT hub linked with your provisioning service.</span></span>
      - <span data-ttu-id="cf2ca-143">Enter a unique device ID.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-143">Enter a unique device ID.</span></span> <span data-ttu-id="cf2ca-144">Make sure to avoid sensitive data while naming your device.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-144">Make sure to avoid sensitive data while naming your device.</span></span> 
      - <span data-ttu-id="cf2ca-145">Update the **Initial device twin state** with the desired initial configuration for the device.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-145">Update the **Initial device twin state** with the desired initial configuration for the device.</span></span>
    - <span data-ttu-id="cf2ca-146">Once complete, click the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-146">Once complete, click the **Save** button.</span></span> 

    <span data-ttu-id="cf2ca-147">[![Add individual enrollment for X.509 attestation in the portal](./media/python-quick-create-simulated-device-x509/individual-enrollment.png)](./media/python-quick-create-simulated-device-x509/individual-enrollment.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="cf2ca-147">[![Add individual enrollment for X.509 attestation in the portal](./media/python-quick-create-simulated-device-x509/individual-enrollment.png)](./media/python-quick-create-simulated-device-x509/individual-enrollment.png#lightbox)</span></span>

   <span data-ttu-id="cf2ca-148">Upon successful enrollment, your X.509 device appears as **riot-device-cert** under the *Registration ID* column in the *Individual Enrollments* tab.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-148">Upon successful enrollment, your X.509 device appears as **riot-device-cert** under the *Registration ID* column in the *Individual Enrollments* tab.</span></span> 

## <a name="simulate-the-device"></a><span data-ttu-id="cf2ca-149">Simulate the device</span><span class="sxs-lookup"><span data-stu-id="cf2ca-149">Simulate the device</span></span>

1. <span data-ttu-id="cf2ca-150">On the Device Provisioning Service summary blade, select **Overview**.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-150">On the Device Provisioning Service summary blade, select **Overview**.</span></span> <span data-ttu-id="cf2ca-151">Note your _ID Scope_ and _Global Service Endpoint_.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-151">Note your _ID Scope_ and _Global Service Endpoint_.</span></span>

    ![Service information](./media/python-quick-create-simulated-device-x509/extract-dps-endpoints.png)

2. <span data-ttu-id="cf2ca-153">Download and install [Python 2.x or 3.x](https://www.python.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="cf2ca-153">Download and install [Python 2.x or 3.x](https://www.python.org/downloads/).</span></span> <span data-ttu-id="cf2ca-154">Make sure to use the 32-bit or 64-bit installation as required by your setup.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-154">Make sure to use the 32-bit or 64-bit installation as required by your setup.</span></span> <span data-ttu-id="cf2ca-155">When prompted during the installation, make sure to add Python to your platform-specific environment variables.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-155">When prompted during the installation, make sure to add Python to your platform-specific environment variables.</span></span> <span data-ttu-id="cf2ca-156">If you are using Python 2.x, you may need to [install or upgrade *pip*, the Python package management system](https://pip.pypa.io/en/stable/installing/).</span><span class="sxs-lookup"><span data-stu-id="cf2ca-156">If you are using Python 2.x, you may need to [install or upgrade *pip*, the Python package management system](https://pip.pypa.io/en/stable/installing/).</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="cf2ca-157">If you are using Windows, also install the [Visual C++ Redistributable for Visual Studio 2015](http://www.microsoft.com/download/confirmation.aspx?id=48145).</span><span class="sxs-lookup"><span data-stu-id="cf2ca-157">If you are using Windows, also install the [Visual C++ Redistributable for Visual Studio 2015](http://www.microsoft.com/download/confirmation.aspx?id=48145).</span></span> <span data-ttu-id="cf2ca-158">The pip packages require the redistributable in order to load/execute the C DLLs.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-158">The pip packages require the redistributable in order to load/execute the C DLLs.</span></span>

3. <span data-ttu-id="cf2ca-159">Follow [these instructions](https://github.com/Azure/azure-iot-sdk-python/blob/master/doc/python-devbox-setup.md) to build the Python packages.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-159">Follow [these instructions](https://github.com/Azure/azure-iot-sdk-python/blob/master/doc/python-devbox-setup.md) to build the Python packages.</span></span>

    > [!NOTE]
        > <span data-ttu-id="cf2ca-160">If using `pip` make sure to also install the `azure-iot-provisioning-device-client` package.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-160">If using `pip` make sure to also install the `azure-iot-provisioning-device-client` package.</span></span>

4. <span data-ttu-id="cf2ca-161">Navigate to the samples folder.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-161">Navigate to the samples folder.</span></span>

    ```cmd/sh
    cd azure-iot-sdk-python/provisioning_device_client/samples
    ```

5. <span data-ttu-id="cf2ca-162">Using your Python IDE, edit the python script named **provisioning\_device\_client\_sample.py**.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-162">Using your Python IDE, edit the python script named **provisioning\_device\_client\_sample.py**.</span></span> <span data-ttu-id="cf2ca-163">Modify the _GLOBAL\_PROV\_URI_ and _ID\_SCOPE_ variables to the values noted previously.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-163">Modify the _GLOBAL\_PROV\_URI_ and _ID\_SCOPE_ variables to the values noted previously.</span></span>

    ```python
    GLOBAL_PROV_URI = "{globalServiceEndpoint}"
    ID_SCOPE = "{idScope}"
    SECURITY_DEVICE_TYPE = ProvisioningSecurityDeviceType.X509
    PROTOCOL = ProvisioningTransportProvider.HTTP
    ```

6. <span data-ttu-id="cf2ca-164">Run the sample.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-164">Run the sample.</span></span> 

    ```cmd/sh
    python provisioning_device_client_sample.py
    ```

7. <span data-ttu-id="cf2ca-165">The application will connect, enroll the device, and display a successful enrollment message.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-165">The application will connect, enroll the device, and display a successful enrollment message.</span></span>

    ![successful enrollment](./media/python-quick-create-simulated-device-x509/enrollment-success.png)

8. <span data-ttu-id="cf2ca-167">In the portal, navigate to the IoT hub linked to your provisioning service and open the **Device Explorer** blade.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-167">In the portal, navigate to the IoT hub linked to your provisioning service and open the **Device Explorer** blade.</span></span> <span data-ttu-id="cf2ca-168">On successful provisioning of the simulated X.509 device to the hub, its device ID appears on the **Device Explorer** blade, with *STATUS* as **enabled**.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-168">On successful provisioning of the simulated X.509 device to the hub, its device ID appears on the **Device Explorer** blade, with *STATUS* as **enabled**.</span></span> <span data-ttu-id="cf2ca-169">You might need to click the **Refresh** button at the top if you already opened the blade prior to running the sample device application.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-169">You might need to click the **Refresh** button at the top if you already opened the blade prior to running the sample device application.</span></span> 

    ![Device is registered with the IoT hub](./media/python-quick-create-simulated-device-x509/hub-registration.png) 

> [!NOTE]
> <span data-ttu-id="cf2ca-171">If you changed the *initial device twin state* from the default value in the enrollment entry for your device, it can pull the desired twin state from the hub and act accordingly.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-171">If you changed the *initial device twin state* from the default value in the enrollment entry for your device, it can pull the desired twin state from the hub and act accordingly.</span></span> <span data-ttu-id="cf2ca-172">For more information, see [Understand and use device twins in IoT Hub](../iot-hub/iot-hub-devguide-device-twins.md).</span><span class="sxs-lookup"><span data-stu-id="cf2ca-172">For more information, see [Understand and use device twins in IoT Hub](../iot-hub/iot-hub-devguide-device-twins.md).</span></span>
>

## <a name="clean-up-resources"></a><span data-ttu-id="cf2ca-173">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="cf2ca-173">Clean up resources</span></span>

<span data-ttu-id="cf2ca-174">If you plan to continue working on and exploring the device client sample, do not clean up the resources created in this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-174">If you plan to continue working on and exploring the device client sample, do not clean up the resources created in this Quickstart.</span></span> <span data-ttu-id="cf2ca-175">If you do not plan to continue, use the following steps to delete all resources created by this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-175">If you do not plan to continue, use the following steps to delete all resources created by this Quickstart.</span></span>

1. <span data-ttu-id="cf2ca-176">Close the device client sample output window on your machine.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-176">Close the device client sample output window on your machine.</span></span>
2. <span data-ttu-id="cf2ca-177">From the left-hand menu in the Azure portal, click **All resources** and then select your Device Provisioning service.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-177">From the left-hand menu in the Azure portal, click **All resources** and then select your Device Provisioning service.</span></span> <span data-ttu-id="cf2ca-178">Open the **Manage Enrollments** blade for your service, and then click the **Individual Enrollments** tab. Select the *REGISTRATION ID* of the device you enrolled in this Quickstart, and click the **Delete** button at the top.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-178">Open the **Manage Enrollments** blade for your service, and then click the **Individual Enrollments** tab. Select the *REGISTRATION ID* of the device you enrolled in this Quickstart, and click the **Delete** button at the top.</span></span> 
3. <span data-ttu-id="cf2ca-179">From the left-hand menu in the Azure portal, click **All resources** and then select your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-179">From the left-hand menu in the Azure portal, click **All resources** and then select your IoT hub.</span></span> <span data-ttu-id="cf2ca-180">Open the **IoT Devices** blade for your hub, select the *DEVICE ID* of the device you registered in this Quickstart, and then click **Delete** button at the top.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-180">Open the **IoT Devices** blade for your hub, select the *DEVICE ID* of the device you registered in this Quickstart, and then click **Delete** button at the top.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf2ca-181">Next steps</span><span class="sxs-lookup"><span data-stu-id="cf2ca-181">Next steps</span></span>

<span data-ttu-id="cf2ca-182">In this Quickstart, you’ve created a simulated X.509 device on your Windows machine and provisioned it to your IoT hub using the Azure IoT Hub Device Provisioning Service on the portal.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-182">In this Quickstart, you’ve created a simulated X.509 device on your Windows machine and provisioned it to your IoT hub using the Azure IoT Hub Device Provisioning Service on the portal.</span></span> <span data-ttu-id="cf2ca-183">To learn how to enroll your X.509 device programmatically, continue to the Quickstart for programmatic enrollment of X.509 devices.</span><span class="sxs-lookup"><span data-stu-id="cf2ca-183">To learn how to enroll your X.509 device programmatically, continue to the Quickstart for programmatic enrollment of X.509 devices.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="cf2ca-184">Azure Quickstart - Enroll X.509 devices to Azure IoT Hub Device Provisioning Service</span><span class="sxs-lookup"><span data-stu-id="cf2ca-184">Azure Quickstart - Enroll X.509 devices to Azure IoT Hub Device Provisioning Service</span></span>](quick-enroll-device-x509-python.md)
