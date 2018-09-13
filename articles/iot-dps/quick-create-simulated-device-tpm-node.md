---
title: Provision a simulated TPM device to Azure IoT Hub using Node.js | Microsoft Docs
description: Azure Quickstart - Create and provision a simulated TPM device using Node.js device SDK for Azure IoT Hub Device Provisioning Service
author: wesmc7777
ms.author: wesmc
ms.date: 04/09/2018
ms.topic: quickstart
ms.service: iot-dps
services: iot-dps
manager: timlt
ms.custom: mvc
ms.openlocfilehash: ef3cfb77a47face18ea5f3b75cbbf08d3e275d2e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865845"
---
# <a name="create-and-provision-a-simulated-tpm-device-using-nodejs-device-sdk-for-iot-hub-device-provisioning-service"></a><span data-ttu-id="21363-103">Create and provision a simulated TPM device using Node.js device SDK for IoT Hub Device Provisioning Service</span><span class="sxs-lookup"><span data-stu-id="21363-103">Create and provision a simulated TPM device using Node.js device SDK for IoT Hub Device Provisioning Service</span></span>

[!INCLUDE [iot-dps-selector-quick-create-simulated-device-tpm](../../includes/iot-dps-selector-quick-create-simulated-device-tpm.md)]

<span data-ttu-id="21363-104">These steps show how to create a simulated device on your development machine running Windows OS, run the Windows TPM simulator as the [Hardware Security Module (HSM)](https://azure.microsoft.com/blog/azure-iot-supports-new-security-hardware-to-strengthen-iot-security/) of the device, and use the code sample to connect this simulated device with the Device Provisioning Service and your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="21363-104">These steps show how to create a simulated device on your development machine running Windows OS, run the Windows TPM simulator as the [Hardware Security Module (HSM)](https://azure.microsoft.com/blog/azure-iot-supports-new-security-hardware-to-strengthen-iot-security/) of the device, and use the code sample to connect this simulated device with the Device Provisioning Service and your IoT hub.</span></span> 

<span data-ttu-id="21363-105">If you're unfamiliar with the process of auto-provisioning, be sure to also review [Auto-provisioning concepts](concepts-auto-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="21363-105">If you're unfamiliar with the process of auto-provisioning, be sure to also review [Auto-provisioning concepts](concepts-auto-provisioning.md).</span></span> <span data-ttu-id="21363-106">Also make sure you've completed the steps in [Set up IoT Hub Device Provisioning Service with the Azure portal](./quick-setup-auto-provision.md) before continuing.</span><span class="sxs-lookup"><span data-stu-id="21363-106">Also make sure you've completed the steps in [Set up IoT Hub Device Provisioning Service with the Azure portal](./quick-setup-auto-provision.md) before continuing.</span></span> 

[!INCLUDE [IoT Device Provisioning Service basic](../../includes/iot-dps-basic.md)]

## <a name="prepare-the-environment"></a><span data-ttu-id="21363-107">Prepare the environment</span><span class="sxs-lookup"><span data-stu-id="21363-107">Prepare the environment</span></span> 

1. <span data-ttu-id="21363-108">Make sure you have [Node.js v4.0 or above](https://nodejs.org) installed on your machine.</span><span class="sxs-lookup"><span data-stu-id="21363-108">Make sure you have [Node.js v4.0 or above](https://nodejs.org) installed on your machine.</span></span>

1. <span data-ttu-id="21363-109">Make sure `git` is installed on your machine and is added to the environment variables accessible to the command window.</span><span class="sxs-lookup"><span data-stu-id="21363-109">Make sure `git` is installed on your machine and is added to the environment variables accessible to the command window.</span></span> <span data-ttu-id="21363-110">See [Software Freedom Conservancy's Git client tools](https://git-scm.com/download/) for the latest version of `git` tools to install, which includes the **Git Bash**, the command-line app that you can use to interact with your local Git repository.</span><span class="sxs-lookup"><span data-stu-id="21363-110">See [Software Freedom Conservancy's Git client tools](https://git-scm.com/download/) for the latest version of `git` tools to install, which includes the **Git Bash**, the command-line app that you can use to interact with your local Git repository.</span></span> 


## <a name="simulate-a-tpm-device"></a><span data-ttu-id="21363-111">Simulate a TPM device</span><span class="sxs-lookup"><span data-stu-id="21363-111">Simulate a TPM device</span></span>

1. <span data-ttu-id="21363-112">Open a command prompt or Git Bash.</span><span class="sxs-lookup"><span data-stu-id="21363-112">Open a command prompt or Git Bash.</span></span> <span data-ttu-id="21363-113">Clone the `azure-utpm-c` GitHub repo:</span><span class="sxs-lookup"><span data-stu-id="21363-113">Clone the `azure-utpm-c` GitHub repo:</span></span>
    
    ```cmd/sh
    git clone https://github.com/Azure/azure-utpm-c.git
    ```

1. <span data-ttu-id="21363-114">Navigate to the GitHub root folder and run the [TPM](https://docs.microsoft.com/windows/device-security/tpm/trusted-platform-module-overview) simulator.</span><span class="sxs-lookup"><span data-stu-id="21363-114">Navigate to the GitHub root folder and run the [TPM](https://docs.microsoft.com/windows/device-security/tpm/trusted-platform-module-overview) simulator.</span></span> <span data-ttu-id="21363-115">It listens over a socket on ports 2321 and 2322.</span><span class="sxs-lookup"><span data-stu-id="21363-115">It listens over a socket on ports 2321 and 2322.</span></span> <span data-ttu-id="21363-116">Do not close this command window; you need to keep this simulator running until the end of this Quickstart guide:</span><span class="sxs-lookup"><span data-stu-id="21363-116">Do not close this command window; you need to keep this simulator running until the end of this Quickstart guide:</span></span> 

    ```cmd/sh
    .\azure-utpm-c\tools\tpm_simulator\Simulator.exe
    ```

1. <span data-ttu-id="21363-117">Create a new empty folder called **registerdevice**.</span><span class="sxs-lookup"><span data-stu-id="21363-117">Create a new empty folder called **registerdevice**.</span></span> <span data-ttu-id="21363-118">In the **registerdevice** folder, create a package.json file using the following command at your command prompt.</span><span class="sxs-lookup"><span data-stu-id="21363-118">In the **registerdevice** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="21363-119">Make sure to answer all questions asked by `npm` or accept the defaults if they suit you:</span><span class="sxs-lookup"><span data-stu-id="21363-119">Make sure to answer all questions asked by `npm` or accept the defaults if they suit you:</span></span>
   
    ```cmd/sh
    npm init
    ```

1. <span data-ttu-id="21363-120">Install the following precursor packages:</span><span class="sxs-lookup"><span data-stu-id="21363-120">Install the following precursor packages:</span></span>

    ```cmd/sh
    npm install node-gyp -g
    npm install ffi -g
    ```

    > [!NOTE]
    > <span data-ttu-id="21363-121">There are some known issues to installing the above packages.</span><span class="sxs-lookup"><span data-stu-id="21363-121">There are some known issues to installing the above packages.</span></span> <span data-ttu-id="21363-122">To resolve these issues, run `npm install --global --production windows-build-tools` using a command prompt in **Run as administrator** mode, run `SET VCTargetsPath=C:\Program Files (x86)\MSBuild\Microsoft.Cpp\v4.0\V140` after replacing the path with your installed version, and then rerun the above installation commands.</span><span class="sxs-lookup"><span data-stu-id="21363-122">To resolve these issues, run `npm install --global --production windows-build-tools` using a command prompt in **Run as administrator** mode, run `SET VCTargetsPath=C:\Program Files (x86)\MSBuild\Microsoft.Cpp\v4.0\V140` after replacing the path with your installed version, and then rerun the above installation commands.</span></span>
    >

1. <span data-ttu-id="21363-123">Install the following packages containing the components used during registration:</span><span class="sxs-lookup"><span data-stu-id="21363-123">Install the following packages containing the components used during registration:</span></span>

    - <span data-ttu-id="21363-124">a security client that works with TPM: `azure-iot-security-tpm`</span><span class="sxs-lookup"><span data-stu-id="21363-124">a security client that works with TPM: `azure-iot-security-tpm`</span></span>
    - <span data-ttu-id="21363-125">a transport for the device to connect to the Device Provisioning Service: either `azure-iot-provisioning-device-http` or `azure-iot-provisioning-device-amqp`</span><span class="sxs-lookup"><span data-stu-id="21363-125">a transport for the device to connect to the Device Provisioning Service: either `azure-iot-provisioning-device-http` or `azure-iot-provisioning-device-amqp`</span></span>
    - <span data-ttu-id="21363-126">a client to use the transport and security client: `azure-iot-provisioning-device`</span><span class="sxs-lookup"><span data-stu-id="21363-126">a client to use the transport and security client: `azure-iot-provisioning-device`</span></span>

    <span data-ttu-id="21363-127">Once the device is registered, you can use the usual IoT Hub Device Client packages to connect the device using the credentials provided during registration.</span><span class="sxs-lookup"><span data-stu-id="21363-127">Once the device is registered, you can use the usual IoT Hub Device Client packages to connect the device using the credentials provided during registration.</span></span> <span data-ttu-id="21363-128">You will need:</span><span class="sxs-lookup"><span data-stu-id="21363-128">You will need:</span></span>

    - <span data-ttu-id="21363-129">the device client: `azure-iot-device`</span><span class="sxs-lookup"><span data-stu-id="21363-129">the device client: `azure-iot-device`</span></span>
    - <span data-ttu-id="21363-130">a transport: any of `azure-iot-device-amqp`, `azure-iot-device-mqtt`, or `azure-iot-device-http`</span><span class="sxs-lookup"><span data-stu-id="21363-130">a transport: any of `azure-iot-device-amqp`, `azure-iot-device-mqtt`, or `azure-iot-device-http`</span></span>
    - <span data-ttu-id="21363-131">the security client that you already installed: `azure-iot-security-tpm`</span><span class="sxs-lookup"><span data-stu-id="21363-131">the security client that you already installed: `azure-iot-security-tpm`</span></span>

    > [!NOTE]
    > <span data-ttu-id="21363-132">The samples below use the `azure-iot-provisioning-device-http` and `azure-iot-device-mqtt` transports.</span><span class="sxs-lookup"><span data-stu-id="21363-132">The samples below use the `azure-iot-provisioning-device-http` and `azure-iot-device-mqtt` transports.</span></span>
    > 

    <span data-ttu-id="21363-133">You can install all of these packages at once by running the following command at your command prompt in the **registerdevice** folder:</span><span class="sxs-lookup"><span data-stu-id="21363-133">You can install all of these packages at once by running the following command at your command prompt in the **registerdevice** folder:</span></span>

        ```cmd/sh
        npm install --save azure-iot-device azure-iot-device-mqtt azure-iot-security-tpm azure-iot-provisioning-device-http azure-iot-provisioning-device
        ```

1. <span data-ttu-id="21363-134">Using a text editor, create a new **ExtractDevice.js** file in the **registerdevice** folder.</span><span class="sxs-lookup"><span data-stu-id="21363-134">Using a text editor, create a new **ExtractDevice.js** file in the **registerdevice** folder.</span></span>

1. <span data-ttu-id="21363-135">Add the following `require` statements at the start of the **ExtractDevice.js** file:</span><span class="sxs-lookup"><span data-stu-id="21363-135">Add the following `require` statements at the start of the **ExtractDevice.js** file:</span></span>
   
    ```
    'use strict';

    var tpmSecurity = require('azure-iot-security-tpm');
    var tssJs = require("tss.js");

    var myTpm = new tpmSecurity.TpmSecurityClient(undefined, new tssJs.Tpm(true));
    ```

1. <span data-ttu-id="21363-136">Add the following function to implement the method:</span><span class="sxs-lookup"><span data-stu-id="21363-136">Add the following function to implement the method:</span></span>
   
    ```
    myTpm.getEndorsementKey(function(err, endorsementKey) {
      if (err) {
        console.log('The error returned from get key is: ' + err);
      } else {
        console.log('the endorsement key is: ' + endorsementKey.toString('base64'));
        myTpm.getRegistrationId((getRegistrationIdError, registrationId) => {
          if (getRegistrationIdError) {
            console.log('The error returned from get registration id is: ' + getRegistrationIdError);
          } else {
            console.log('The Registration Id is: ' + registrationId);
            process.exit();
          }
        });
      }
    });
    ```

1. <span data-ttu-id="21363-137">Save and close the **ExtractDevice.js** file.</span><span class="sxs-lookup"><span data-stu-id="21363-137">Save and close the **ExtractDevice.js** file.</span></span> <span data-ttu-id="21363-138">Run the sample:</span><span class="sxs-lookup"><span data-stu-id="21363-138">Run the sample:</span></span>

    ```cmd/sh
    node ExtractDevice.js
    ```

1. <span data-ttu-id="21363-139">The output window displays the **_Endorsement Key_** and the **_Registration Id_** needed for device enrollment.</span><span class="sxs-lookup"><span data-stu-id="21363-139">The output window displays the **_Endorsement Key_** and the **_Registration Id_** needed for device enrollment.</span></span> <span data-ttu-id="21363-140">Note down these values.</span><span class="sxs-lookup"><span data-stu-id="21363-140">Note down these values.</span></span> 


## <a name="create-a-device-entry"></a><span data-ttu-id="21363-141">Create a device entry</span><span class="sxs-lookup"><span data-stu-id="21363-141">Create a device entry</span></span>

1. <span data-ttu-id="21363-142">Log in to the Azure portal, click on the **All resources** button on the left-hand menu and open your Device Provisioning service.</span><span class="sxs-lookup"><span data-stu-id="21363-142">Log in to the Azure portal, click on the **All resources** button on the left-hand menu and open your Device Provisioning service.</span></span>

1. <span data-ttu-id="21363-143">On the Device Provisioning Service summary blade, select **Manage enrollments**.</span><span class="sxs-lookup"><span data-stu-id="21363-143">On the Device Provisioning Service summary blade, select **Manage enrollments**.</span></span> <span data-ttu-id="21363-144">Select **Individual Enrollments** tab and click the **Add** button at the top.</span><span class="sxs-lookup"><span data-stu-id="21363-144">Select **Individual Enrollments** tab and click the **Add** button at the top.</span></span> 

1. <span data-ttu-id="21363-145">Under the **Add enrollment list entry**, enter the following information:</span><span class="sxs-lookup"><span data-stu-id="21363-145">Under the **Add enrollment list entry**, enter the following information:</span></span>
    - <span data-ttu-id="21363-146">Select **TPM** as the identity attestation *Mechanism*.</span><span class="sxs-lookup"><span data-stu-id="21363-146">Select **TPM** as the identity attestation *Mechanism*.</span></span>
    - <span data-ttu-id="21363-147">Enter the *Registration ID* and *Endorsement key* for your TPM device.</span><span class="sxs-lookup"><span data-stu-id="21363-147">Enter the *Registration ID* and *Endorsement key* for your TPM device.</span></span>
    - <span data-ttu-id="21363-148">Optionally, you may provide the following information:</span><span class="sxs-lookup"><span data-stu-id="21363-148">Optionally, you may provide the following information:</span></span>
        - <span data-ttu-id="21363-149">Select an IoT hub linked with your provisioning service.</span><span class="sxs-lookup"><span data-stu-id="21363-149">Select an IoT hub linked with your provisioning service.</span></span>
        - <span data-ttu-id="21363-150">Enter a unique device ID.</span><span class="sxs-lookup"><span data-stu-id="21363-150">Enter a unique device ID.</span></span> <span data-ttu-id="21363-151">Make sure to avoid sensitive data while naming your device.</span><span class="sxs-lookup"><span data-stu-id="21363-151">Make sure to avoid sensitive data while naming your device.</span></span>
        - <span data-ttu-id="21363-152">Update the **Initial device twin state** with the desired initial configuration for the device.</span><span class="sxs-lookup"><span data-stu-id="21363-152">Update the **Initial device twin state** with the desired initial configuration for the device.</span></span>
    - <span data-ttu-id="21363-153">Once complete, click the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="21363-153">Once complete, click the **Save** button.</span></span> 

    ![Enter device enrollment information in the portal blade](./media/quick-create-simulated-device/enter-device-enrollment.png)  

   <span data-ttu-id="21363-155">On successful enrollment, the *Registration ID* of your device appears in the list under the *Individual Enrollments* tab.</span><span class="sxs-lookup"><span data-stu-id="21363-155">On successful enrollment, the *Registration ID* of your device appears in the list under the *Individual Enrollments* tab.</span></span> 


## <a name="register-the-device"></a><span data-ttu-id="21363-156">Register the device</span><span class="sxs-lookup"><span data-stu-id="21363-156">Register the device</span></span>

1. <span data-ttu-id="21363-157">In the Azure portal, select the **Overview** blade for your Device Provisioning service and note down the **_Global Device Endpoint_** and **_ID Scope_** values.</span><span class="sxs-lookup"><span data-stu-id="21363-157">In the Azure portal, select the **Overview** blade for your Device Provisioning service and note down the **_Global Device Endpoint_** and **_ID Scope_** values.</span></span>

    ![Extract Device Provisioning Service endpoint information from the portal blade](./media/quick-create-simulated-device/extract-dps-endpoints.png) 

1. <span data-ttu-id="21363-159">Using a text editor, create a new **RegisterDevice.js** file in the **registerdevice** folder.</span><span class="sxs-lookup"><span data-stu-id="21363-159">Using a text editor, create a new **RegisterDevice.js** file in the **registerdevice** folder.</span></span>

1. <span data-ttu-id="21363-160">Add the following `require` statements at the start of the **RegisterDevice.js** file:</span><span class="sxs-lookup"><span data-stu-id="21363-160">Add the following `require` statements at the start of the **RegisterDevice.js** file:</span></span>
   
    ```
    'use strict';

    var ProvisioningTransport = require('azure-iot-provisioning-device-http').Http;
    var iotHubTransport = require('azure-iot-device-mqtt').Mqtt;
    var Client = require('azure-iot-device').Client;
    var Message = require('azure-iot-device').Message;
    var tpmSecurity = require('azure-iot-security-tpm');
    var ProvisioningDeviceClient = require('azure-iot-provisioning-device').ProvisioningDeviceClient;
    ```

    > [!NOTE]
    > <span data-ttu-id="21363-161">The **Azure IoT SDK for Node.js** supports additional protocols like _AMQP_, _AMQP WS_, and _MQTT WS_.</span><span class="sxs-lookup"><span data-stu-id="21363-161">The **Azure IoT SDK for Node.js** supports additional protocols like _AMQP_, _AMQP WS_, and _MQTT WS_.</span></span>  <span data-ttu-id="21363-162">For more examples, see [Device Provisioning Service SDK for Node.js samples](https://github.com/Azure/azure-iot-sdk-node/tree/master/provisioning/device/samples).</span><span class="sxs-lookup"><span data-stu-id="21363-162">For more examples, see [Device Provisioning Service SDK for Node.js samples](https://github.com/Azure/azure-iot-sdk-node/tree/master/provisioning/device/samples).</span></span>
    > 

1. <span data-ttu-id="21363-163">Add **globalDeviceEndpoint** and **idScope** variables and use them to create a **ProvisioningDeviceClient** instance.</span><span class="sxs-lookup"><span data-stu-id="21363-163">Add **globalDeviceEndpoint** and **idScope** variables and use them to create a **ProvisioningDeviceClient** instance.</span></span> <span data-ttu-id="21363-164">Replace **{globalDeviceEndpoint}** and **{idScope}** with the **_Global Device Endpoint_** and **_ID Scope_** values from **Step 1**:</span><span class="sxs-lookup"><span data-stu-id="21363-164">Replace **{globalDeviceEndpoint}** and **{idScope}** with the **_Global Device Endpoint_** and **_ID Scope_** values from **Step 1**:</span></span>
   
    ```
    var provisioningHost = '{globalDeviceEndpoint}';
    var idScope = '{idScope}';

    var tssJs = require("tss.js");
    var securityClient = new tpmSecurity.TpmSecurityClient('', new tssJs.Tpm(true));
    // if using non-simulated device, replace the above line with following:
    //var securityClient = new tpmSecurity.TpmSecurityClient();

    var provisioningClient = ProvisioningDeviceClient.create(provisioningHost, idScope, new ProvisioningTransport(), securityClient);
    ```

1. <span data-ttu-id="21363-165">Add the following function to implement the method on the device:</span><span class="sxs-lookup"><span data-stu-id="21363-165">Add the following function to implement the method on the device:</span></span>
   
    ```
    provisioningClient.register(function(err, result) {
      if (err) {
        console.log("error registering device: " + err);
      } else {
        console.log('registration succeeded');
        console.log('assigned hub=' + result.registrationState.assignedHub);
        console.log('deviceId=' + result.registrationState.deviceId);
        var tpmAuthenticationProvider = tpmSecurity.TpmAuthenticationProvider.fromTpmSecurityClient(result.registrationState.deviceId, result.registrationState.assignedHub, securityClient);
        var hubClient = Client.fromAuthenticationProvider(tpmAuthenticationProvider, iotHubTransport);

        var connectCallback = function (err) {
          if (err) {
            console.error('Could not connect: ' + err.message);
          } else {
            console.log('Client connected');
            var message = new Message('Hello world');
            hubClient.sendEvent(message, printResultFor('send'));
          }
        };

        hubClient.open(connectCallback);

        function printResultFor(op) {
          return function printResult(err, res) {
            if (err) console.log(op + ' error: ' + err.toString());
            if (res) console.log(op + ' status: ' + res.constructor.name);
            process.exit(1);
          };
        }
      }
    });
    ```

1. <span data-ttu-id="21363-166">Save and close the **RegisterDevice.js** file.</span><span class="sxs-lookup"><span data-stu-id="21363-166">Save and close the **RegisterDevice.js** file.</span></span> <span data-ttu-id="21363-167">Run the sample:</span><span class="sxs-lookup"><span data-stu-id="21363-167">Run the sample:</span></span>

    ```cmd/sh
    node RegisterDevice.js
    ```

1. <span data-ttu-id="21363-168">Notice the messages that simulate the device booting and connecting to the Device Provisioning Service to get your IoT hub information.</span><span class="sxs-lookup"><span data-stu-id="21363-168">Notice the messages that simulate the device booting and connecting to the Device Provisioning Service to get your IoT hub information.</span></span> <span data-ttu-id="21363-169">On successful provisioning of your simulated device to the IoT hub linked with your provisioning service, the device ID appears on the hub's **IoT Devices** blade.</span><span class="sxs-lookup"><span data-stu-id="21363-169">On successful provisioning of your simulated device to the IoT hub linked with your provisioning service, the device ID appears on the hub's **IoT Devices** blade.</span></span> 

    ![Device is registered with the IoT hub](./media/quick-create-simulated-device/hub-registration.png) 

    <span data-ttu-id="21363-171">If you changed the *initial device twin state* from the default value in the enrollment entry for your device, it can pull the desired twin state from the hub and act accordingly.</span><span class="sxs-lookup"><span data-stu-id="21363-171">If you changed the *initial device twin state* from the default value in the enrollment entry for your device, it can pull the desired twin state from the hub and act accordingly.</span></span> <span data-ttu-id="21363-172">For more information, see [Understand and use device twins in IoT Hub](../iot-hub/iot-hub-devguide-device-twins.md)</span><span class="sxs-lookup"><span data-stu-id="21363-172">For more information, see [Understand and use device twins in IoT Hub](../iot-hub/iot-hub-devguide-device-twins.md)</span></span>


## <a name="clean-up-resources"></a><span data-ttu-id="21363-173">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="21363-173">Clean up resources</span></span>

<span data-ttu-id="21363-174">If you plan to continue working on and exploring the device client sample, do not clean up the resources created in this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="21363-174">If you plan to continue working on and exploring the device client sample, do not clean up the resources created in this Quickstart.</span></span> <span data-ttu-id="21363-175">If you do not plan to continue, use the following steps to delete all resources created by this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="21363-175">If you do not plan to continue, use the following steps to delete all resources created by this Quickstart.</span></span>

1. <span data-ttu-id="21363-176">Close the device client sample output window on your machine.</span><span class="sxs-lookup"><span data-stu-id="21363-176">Close the device client sample output window on your machine.</span></span>
1. <span data-ttu-id="21363-177">Close the TPM simulator window on your machine.</span><span class="sxs-lookup"><span data-stu-id="21363-177">Close the TPM simulator window on your machine.</span></span>
1. <span data-ttu-id="21363-178">From the left-hand menu in the Azure portal, click **All resources** and then select your Device Provisioning service.</span><span class="sxs-lookup"><span data-stu-id="21363-178">From the left-hand menu in the Azure portal, click **All resources** and then select your Device Provisioning service.</span></span> <span data-ttu-id="21363-179">Open the **Manage Enrollments** blade for your service, and then click the **Individual Enrollments** tab. Select the *REGISTRATION ID* of the device you enrolled in this Quickstart, and click the **Delete** button at the top.</span><span class="sxs-lookup"><span data-stu-id="21363-179">Open the **Manage Enrollments** blade for your service, and then click the **Individual Enrollments** tab. Select the *REGISTRATION ID* of the device you enrolled in this Quickstart, and click the **Delete** button at the top.</span></span> 
1. <span data-ttu-id="21363-180">From the left-hand menu in the Azure portal, click **All resources** and then select your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="21363-180">From the left-hand menu in the Azure portal, click **All resources** and then select your IoT hub.</span></span> <span data-ttu-id="21363-181">Open the **IoT Devices** blade for your hub, select the *DEVICE ID* of the device you registered in this Quickstart, and then click **Delete** button at the top.</span><span class="sxs-lookup"><span data-stu-id="21363-181">Open the **IoT Devices** blade for your hub, select the *DEVICE ID* of the device you registered in this Quickstart, and then click **Delete** button at the top.</span></span>


## <a name="next-steps"></a><span data-ttu-id="21363-182">Next steps</span><span class="sxs-lookup"><span data-stu-id="21363-182">Next steps</span></span>

<span data-ttu-id="21363-183">In this Quickstart, you’ve created a TPM simulated device on your machine and provisioned it to your IoT hub using the IoT Hub Device Provisioning Service.</span><span class="sxs-lookup"><span data-stu-id="21363-183">In this Quickstart, you’ve created a TPM simulated device on your machine and provisioned it to your IoT hub using the IoT Hub Device Provisioning Service.</span></span> <span data-ttu-id="21363-184">To learn how to enroll your TPM device programmatically, continue to the Quickstart for programmatic enrollment of a TPM device.</span><span class="sxs-lookup"><span data-stu-id="21363-184">To learn how to enroll your TPM device programmatically, continue to the Quickstart for programmatic enrollment of a TPM device.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="21363-185">Azure Quickstart - Enroll TPM device to Azure IoT Hub Device Provisioning Service</span><span class="sxs-lookup"><span data-stu-id="21363-185">Azure Quickstart - Enroll TPM device to Azure IoT Hub Device Provisioning Service</span></span>](quick-enroll-device-tpm-node.md)
