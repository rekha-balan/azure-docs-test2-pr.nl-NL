---
title: How to use Azure IoT Hub Device Provisioning Service auto-provisioning to register the MXChip IoT DevKit with IoT Hub  | Microsoft Docs
description: How to use Azure IoT Hub Device Provisioning Service auto-provisioning to register the MXChip IoT DevKit with IoT Hub.
author: liydu
ms.author: liydu
ms.date: 04/04/2018
ms.topic: conceptual
ms.service: iot-dps
services: iot-dps
manager: jeffya
ms.openlocfilehash: d8912a5da8c4df2069d8bc53454748b5fb3d5c39
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867149"
---
# <a name="use-azure-iot-hub-device-provisioning-service-auto-provisioning-to-register-the-mxchip-iot-devkit-with-iot-hub"></a><span data-ttu-id="62771-103">Use Azure IoT Hub Device Provisioning Service auto-provisioning to register the MXChip IoT DevKit with IoT Hub</span><span class="sxs-lookup"><span data-stu-id="62771-103">Use Azure IoT Hub Device Provisioning Service auto-provisioning to register the MXChip IoT DevKit with IoT Hub</span></span>

<span data-ttu-id="62771-104">This article describes how to use Azure IoT Hub Device Provisioning Service [auto-provisioning](concepts-auto-provisioning.md), to register the MXChip IoT DevKit with Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="62771-104">This article describes how to use Azure IoT Hub Device Provisioning Service [auto-provisioning](concepts-auto-provisioning.md), to register the MXChip IoT DevKit with Azure IoT Hub.</span></span> <span data-ttu-id="62771-105">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="62771-105">In this tutorial, you learn how to:</span></span>

* <span data-ttu-id="62771-106">Configure the global endpoint of the Device Provisioning service on a device.</span><span class="sxs-lookup"><span data-stu-id="62771-106">Configure the global endpoint of the Device Provisioning service on a device.</span></span>
* <span data-ttu-id="62771-107">Use a unique device secret (UDS) to generate an X.509 certificate.</span><span class="sxs-lookup"><span data-stu-id="62771-107">Use a unique device secret (UDS) to generate an X.509 certificate.</span></span>
* <span data-ttu-id="62771-108">Enroll an individual device.</span><span class="sxs-lookup"><span data-stu-id="62771-108">Enroll an individual device.</span></span>
* <span data-ttu-id="62771-109">Verify that the device is registered.</span><span class="sxs-lookup"><span data-stu-id="62771-109">Verify that the device is registered.</span></span>

<span data-ttu-id="62771-110">The [MXChip IoT DevKit](https://aka.ms/iot-devkit) is an all-in-one Arduino-compatible board with rich peripherals and sensors.</span><span class="sxs-lookup"><span data-stu-id="62771-110">The [MXChip IoT DevKit](https://aka.ms/iot-devkit) is an all-in-one Arduino-compatible board with rich peripherals and sensors.</span></span> <span data-ttu-id="62771-111">You can develop for it by using the [Visual Studio Code extension for Arduino](https://aka.ms/arduino).</span><span class="sxs-lookup"><span data-stu-id="62771-111">You can develop for it by using the [Visual Studio Code extension for Arduino](https://aka.ms/arduino).</span></span> <span data-ttu-id="62771-112">The DevKit comes with a growing [projects catalog](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/) to guide your prototype Internet of Things (IoT) solutions that take advantage of Azure services.</span><span class="sxs-lookup"><span data-stu-id="62771-112">The DevKit comes with a growing [projects catalog](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/) to guide your prototype Internet of Things (IoT) solutions that take advantage of Azure services.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="62771-113">Before you begin</span><span class="sxs-lookup"><span data-stu-id="62771-113">Before you begin</span></span>

<span data-ttu-id="62771-114">To complete the steps in this tutorial, first do the following tasks:</span><span class="sxs-lookup"><span data-stu-id="62771-114">To complete the steps in this tutorial, first do the following tasks:</span></span>

* <span data-ttu-id="62771-115">Prepare your DevKit by following the steps in [Connect IoT DevKit AZ3166 to Azure IoT Hub in the cloud](/azure/iot-hub/iot-hub-arduino-iot-devkit-az3166-get-started).</span><span class="sxs-lookup"><span data-stu-id="62771-115">Prepare your DevKit by following the steps in [Connect IoT DevKit AZ3166 to Azure IoT Hub in the cloud](/azure/iot-hub/iot-hub-arduino-iot-devkit-az3166-get-started).</span></span>
* <span data-ttu-id="62771-116">Upgrade to the latest firmware (1.3.0 or later) with the [Update DevKit firmware](https://microsoft.github.io/azure-iot-developer-kit/docs/firmware-upgrading/) tutorial.</span><span class="sxs-lookup"><span data-stu-id="62771-116">Upgrade to the latest firmware (1.3.0 or later) with the [Update DevKit firmware](https://microsoft.github.io/azure-iot-developer-kit/docs/firmware-upgrading/) tutorial.</span></span>
* <span data-ttu-id="62771-117">Create and link an IoT Hub with a Device Provisioning service instance by following the steps in [Set up the IoT Hub Device Provisioning Service with the Azure portal](/azure/iot-dps/quick-setup-auto-provision).</span><span class="sxs-lookup"><span data-stu-id="62771-117">Create and link an IoT Hub with a Device Provisioning service instance by following the steps in [Set up the IoT Hub Device Provisioning Service with the Azure portal](/azure/iot-dps/quick-setup-auto-provision).</span></span>

## <a name="build-and-deploy-auto-provisioning-registration-software-to-the-device"></a><span data-ttu-id="62771-118">Build and deploy auto-provisioning registration software to the device</span><span class="sxs-lookup"><span data-stu-id="62771-118">Build and deploy auto-provisioning registration software to the device</span></span>

<span data-ttu-id="62771-119">To connect the DevKit to the Device Provisioning service instance that you created:</span><span class="sxs-lookup"><span data-stu-id="62771-119">To connect the DevKit to the Device Provisioning service instance that you created:</span></span>

1. <span data-ttu-id="62771-120">In the Azure portal, select the **Overview** pane of your Device Provisioning service and note down the **Global device endpoint** and **ID Scope** values.</span><span class="sxs-lookup"><span data-stu-id="62771-120">In the Azure portal, select the **Overview** pane of your Device Provisioning service and note down the **Global device endpoint** and **ID Scope** values.</span></span>
  <span data-ttu-id="62771-121">![Device Provisioning Service Global Endpoint and ID Scope](./media/how-to-connect-mxchip-iot-devkit/dps-global-endpoint.png)</span><span class="sxs-lookup"><span data-stu-id="62771-121">![Device Provisioning Service Global Endpoint and ID Scope](./media/how-to-connect-mxchip-iot-devkit/dps-global-endpoint.png)</span></span>

2. <span data-ttu-id="62771-122">Make sure you have `git` installed on your machine and that it's added to the environment variables accessible to the command window.</span><span class="sxs-lookup"><span data-stu-id="62771-122">Make sure you have `git` installed on your machine and that it's added to the environment variables accessible to the command window.</span></span> <span data-ttu-id="62771-123">See [Software Freedom Conservancy's Git client tools](https://git-scm.com/download/) to have the latest version installed.</span><span class="sxs-lookup"><span data-stu-id="62771-123">See [Software Freedom Conservancy's Git client tools](https://git-scm.com/download/) to have the latest version installed.</span></span>

3. <span data-ttu-id="62771-124">Open a command prompt.</span><span class="sxs-lookup"><span data-stu-id="62771-124">Open a command prompt.</span></span> <span data-ttu-id="62771-125">Clone the GitHub repo for the Device Provisioning service sample code:</span><span class="sxs-lookup"><span data-stu-id="62771-125">Clone the GitHub repo for the Device Provisioning service sample code:</span></span>
  ```bash
  git clone https://github.com/DevKitExamples/DevKitDPS.git
  ```

4. <span data-ttu-id="62771-126">Open Visual Studio Code, connect the DevKit to your computer, and then open the folder that contains the code you cloned.</span><span class="sxs-lookup"><span data-stu-id="62771-126">Open Visual Studio Code, connect the DevKit to your computer, and then open the folder that contains the code you cloned.</span></span>

5. <span data-ttu-id="62771-127">Open **DevKitDPS.ino**.</span><span class="sxs-lookup"><span data-stu-id="62771-127">Open **DevKitDPS.ino**.</span></span> <span data-ttu-id="62771-128">Find and replace `[Global Device Endpoint]` and `[ID Scope]` with the values you just noted down.</span><span class="sxs-lookup"><span data-stu-id="62771-128">Find and replace `[Global Device Endpoint]` and `[ID Scope]` with the values you just noted down.</span></span>
  <span data-ttu-id="62771-129">![Device Provisioning Service Endpoint](./media/how-to-connect-mxchip-iot-devkit/endpoint.png) You can leave the **registrationId** blank.</span><span class="sxs-lookup"><span data-stu-id="62771-129">![Device Provisioning Service Endpoint](./media/how-to-connect-mxchip-iot-devkit/endpoint.png) You can leave the **registrationId** blank.</span></span> <span data-ttu-id="62771-130">The application generates one for you based on the MAC address and firmware version.</span><span class="sxs-lookup"><span data-stu-id="62771-130">The application generates one for you based on the MAC address and firmware version.</span></span> <span data-ttu-id="62771-131">If you want to customize the Registration ID, you must use only alphanumeric, lowercase, and hyphen combinations with a maximum of 128 characters.</span><span class="sxs-lookup"><span data-stu-id="62771-131">If you want to customize the Registration ID, you must use only alphanumeric, lowercase, and hyphen combinations with a maximum of 128 characters.</span></span> <span data-ttu-id="62771-132">For more information, see [Manage device enrollments with Azure portal](https://docs.microsoft.com/azure/iot-dps/how-to-manage-enrollments).</span><span class="sxs-lookup"><span data-stu-id="62771-132">For more information, see [Manage device enrollments with Azure portal](https://docs.microsoft.com/azure/iot-dps/how-to-manage-enrollments).</span></span>

6. <span data-ttu-id="62771-133">Use Quick Open in VS Code (Windows: `Ctrl+P`, macOS: `Cmd+P`) and type *task device-upload* to build and upload the code to the DevKit.</span><span class="sxs-lookup"><span data-stu-id="62771-133">Use Quick Open in VS Code (Windows: `Ctrl+P`, macOS: `Cmd+P`) and type *task device-upload* to build and upload the code to the DevKit.</span></span>

7. <span data-ttu-id="62771-134">The output window shows whether the task was successful.</span><span class="sxs-lookup"><span data-stu-id="62771-134">The output window shows whether the task was successful.</span></span>

## <a name="save-a-unique-device-secret-on-an-stsafe-security-chip"></a><span data-ttu-id="62771-135">Save a unique device secret on an STSAFE security chip</span><span class="sxs-lookup"><span data-stu-id="62771-135">Save a unique device secret on an STSAFE security chip</span></span>

<span data-ttu-id="62771-136">Auto-provisioning can be configured on a device based on the device's [attestation mechanism](concepts-security.md#attestation-mechanism).</span><span class="sxs-lookup"><span data-stu-id="62771-136">Auto-provisioning can be configured on a device based on the device's [attestation mechanism](concepts-security.md#attestation-mechanism).</span></span> <span data-ttu-id="62771-137">The MXChip IoT DevKit uses the [Device Identity Composition Engine](https://trustedcomputinggroup.org/wp-content/uploads/Foundational-Trust-for-IOT-and-Resource-Constrained-Devices.pdf) from the [Trusted Computing Group](https://trustedcomputinggroup.org).</span><span class="sxs-lookup"><span data-stu-id="62771-137">The MXChip IoT DevKit uses the [Device Identity Composition Engine](https://trustedcomputinggroup.org/wp-content/uploads/Foundational-Trust-for-IOT-and-Resource-Constrained-Devices.pdf) from the [Trusted Computing Group](https://trustedcomputinggroup.org).</span></span> <span data-ttu-id="62771-138">A *unique device secret* (UDS) saved in an STSAFE security chip on the DevKit is used to generate the device's unique [X.509 certificate](concepts-security.md#x509-certificates).</span><span class="sxs-lookup"><span data-stu-id="62771-138">A *unique device secret* (UDS) saved in an STSAFE security chip on the DevKit is used to generate the device's unique [X.509 certificate](concepts-security.md#x509-certificates).</span></span> <span data-ttu-id="62771-139">The certificate is used later for the enrollment process in the Device Provisioning service, and during registration at runtime.</span><span class="sxs-lookup"><span data-stu-id="62771-139">The certificate is used later for the enrollment process in the Device Provisioning service, and during registration at runtime.</span></span>

<span data-ttu-id="62771-140">A typical unique device secret is a 64-character string, as seen in the following sample:</span><span class="sxs-lookup"><span data-stu-id="62771-140">A typical unique device secret is a 64-character string, as seen in the following sample:</span></span>

```
19e25a259d0c2be03a02d416c05c48ccd0cc7d1743458aae1cb488b074993eae
```

<span data-ttu-id="62771-141">The string is broken up into characters pairs that are used in the security calculation.</span><span class="sxs-lookup"><span data-stu-id="62771-141">The string is broken up into characters pairs that are used in the security calculation.</span></span> <span data-ttu-id="62771-142">The preceding sample UDS is resolved to: `0x19`, `0xe2`, `0x5a`, `0x25`, `0x9d`, `0x0c`, `0x2b`, `0xe0`, `0x3a`, `0x02`, `0xd4`, `0x16`, `0xc0`, `0x5c`, `0x48`, `0xcc`, `0xd0`, `0xcc`, `0x7d`, `0x17`, `0x43`, `0x45`, `0x8a`, `0xae`, `0x1c`, `0xb4`, `0x88`, `0xb0`, `0x74`, `0x99`, `0x3e`, `0xae`.</span><span class="sxs-lookup"><span data-stu-id="62771-142">The preceding sample UDS is resolved to: `0x19`, `0xe2`, `0x5a`, `0x25`, `0x9d`, `0x0c`, `0x2b`, `0xe0`, `0x3a`, `0x02`, `0xd4`, `0x16`, `0xc0`, `0x5c`, `0x48`, `0xcc`, `0xd0`, `0xcc`, `0x7d`, `0x17`, `0x43`, `0x45`, `0x8a`, `0xae`, `0x1c`, `0xb4`, `0x88`, `0xb0`, `0x74`, `0x99`, `0x3e`, `0xae`.</span></span>

<span data-ttu-id="62771-143">To save a unique device secret on the DevKit:</span><span class="sxs-lookup"><span data-stu-id="62771-143">To save a unique device secret on the DevKit:</span></span>

1. <span data-ttu-id="62771-144">Open the serial monitor by using a tool such as Putty.</span><span class="sxs-lookup"><span data-stu-id="62771-144">Open the serial monitor by using a tool such as Putty.</span></span> <span data-ttu-id="62771-145">See [Use configuration mode](https://microsoft.github.io/azure-iot-developer-kit/docs/use-configuration-mode/) for details.</span><span class="sxs-lookup"><span data-stu-id="62771-145">See [Use configuration mode](https://microsoft.github.io/azure-iot-developer-kit/docs/use-configuration-mode/) for details.</span></span>

2. <span data-ttu-id="62771-146">With the DevKit connected to your computer, hold down the **A** button, and then press and release the **Reset** button to enter configuration mode.</span><span class="sxs-lookup"><span data-stu-id="62771-146">With the DevKit connected to your computer, hold down the **A** button, and then press and release the **Reset** button to enter configuration mode.</span></span> <span data-ttu-id="62771-147">The screen shows the DevKit ID and Configuration.</span><span class="sxs-lookup"><span data-stu-id="62771-147">The screen shows the DevKit ID and Configuration.</span></span>

3. <span data-ttu-id="62771-148">Take the sample UDS string and change one or more characters to other values between `0` and `f` for your own UDS.</span><span class="sxs-lookup"><span data-stu-id="62771-148">Take the sample UDS string and change one or more characters to other values between `0` and `f` for your own UDS.</span></span>

4. <span data-ttu-id="62771-149">In the serial monitor window, type *set_dps_uds [your_own_uds_value]* and select Enter.</span><span class="sxs-lookup"><span data-stu-id="62771-149">In the serial monitor window, type *set_dps_uds [your_own_uds_value]* and select Enter.</span></span>
  > [!NOTE]
  > <span data-ttu-id="62771-150">For example, if you set your own UDS by changing the last two characters to `f`, you need to enter the command like this: `set_dps_uds 19e25a259d0c2be03a02d416c05c48ccd0cc7d1743458aae1cb488b074993eff`.</span><span class="sxs-lookup"><span data-stu-id="62771-150">For example, if you set your own UDS by changing the last two characters to `f`, you need to enter the command like this: `set_dps_uds 19e25a259d0c2be03a02d416c05c48ccd0cc7d1743458aae1cb488b074993eff`.</span></span>

5. <span data-ttu-id="62771-151">Without closing the serial monitor window, press the **Reset** button on the DevKit.</span><span class="sxs-lookup"><span data-stu-id="62771-151">Without closing the serial monitor window, press the **Reset** button on the DevKit.</span></span>

6. <span data-ttu-id="62771-152">Note down the **DevKit MAC Address** and **DevKit Firmware Version** values.</span><span class="sxs-lookup"><span data-stu-id="62771-152">Note down the **DevKit MAC Address** and **DevKit Firmware Version** values.</span></span>
  <span data-ttu-id="62771-153">![Firmware version](./media/how-to-connect-mxchip-iot-devkit/firmware-version.png)</span><span class="sxs-lookup"><span data-stu-id="62771-153">![Firmware version](./media/how-to-connect-mxchip-iot-devkit/firmware-version.png)</span></span>

## <a name="generate-an-x509-certificate"></a><span data-ttu-id="62771-154">Generate an X.509 certificate</span><span class="sxs-lookup"><span data-stu-id="62771-154">Generate an X.509 certificate</span></span>

<span data-ttu-id="62771-155">Now you need to generate an X.609 certificate.</span><span class="sxs-lookup"><span data-stu-id="62771-155">Now you need to generate an X.609 certificate.</span></span> 

### <a name="windows"></a><span data-ttu-id="62771-156">Windows</span><span class="sxs-lookup"><span data-stu-id="62771-156">Windows</span></span>

1. <span data-ttu-id="62771-157">Open File Explorer and go to the folder that contains the Device Provisioning Service sample code that you cloned earlier.</span><span class="sxs-lookup"><span data-stu-id="62771-157">Open File Explorer and go to the folder that contains the Device Provisioning Service sample code that you cloned earlier.</span></span> <span data-ttu-id="62771-158">In the **.build** folder, find and copy **DPS.ino.bin** and **DPS.ino.map**.</span><span class="sxs-lookup"><span data-stu-id="62771-158">In the **.build** folder, find and copy **DPS.ino.bin** and **DPS.ino.map**.</span></span>
  <span data-ttu-id="62771-159">![Generated files](./media/how-to-connect-mxchip-iot-devkit/generated-files.png)</span><span class="sxs-lookup"><span data-stu-id="62771-159">![Generated files](./media/how-to-connect-mxchip-iot-devkit/generated-files.png)</span></span>
  > [!NOTE]
  > <span data-ttu-id="62771-160">If you changed the `built.path` configuration for Arduino to another folder, you need to find those files in the folder you configured.</span><span class="sxs-lookup"><span data-stu-id="62771-160">If you changed the `built.path` configuration for Arduino to another folder, you need to find those files in the folder you configured.</span></span>

2. <span data-ttu-id="62771-161">Paste these two files into the **tools** folder on the same level with the **.build** folder.</span><span class="sxs-lookup"><span data-stu-id="62771-161">Paste these two files into the **tools** folder on the same level with the **.build** folder.</span></span>

3. <span data-ttu-id="62771-162">Run **dps_cert_gen.exe**.</span><span class="sxs-lookup"><span data-stu-id="62771-162">Run **dps_cert_gen.exe**.</span></span> <span data-ttu-id="62771-163">Follow the prompts to enter your **UDS**, the **MAC address** for the DevKit, and the **firmware version** to generate the X.509 certificate.</span><span class="sxs-lookup"><span data-stu-id="62771-163">Follow the prompts to enter your **UDS**, the **MAC address** for the DevKit, and the **firmware version** to generate the X.509 certificate.</span></span>
  <span data-ttu-id="62771-164">![Run dps-cert-gen.exe](./media/how-to-connect-mxchip-iot-devkit/dps-cert-gen.png)</span><span class="sxs-lookup"><span data-stu-id="62771-164">![Run dps-cert-gen.exe](./media/how-to-connect-mxchip-iot-devkit/dps-cert-gen.png)</span></span>

4. <span data-ttu-id="62771-165">After the X.509 certificate is generated, a **.pem** certificate is saved to the same folder.</span><span class="sxs-lookup"><span data-stu-id="62771-165">After the X.509 certificate is generated, a **.pem** certificate is saved to the same folder.</span></span>

## <a name="create-a-device-enrollment-entry-in-the-device-provisioning-service"></a><span data-ttu-id="62771-166">Create a device enrollment entry in the Device Provisioning service</span><span class="sxs-lookup"><span data-stu-id="62771-166">Create a device enrollment entry in the Device Provisioning service</span></span>

1. <span data-ttu-id="62771-167">In the Azure portal, go to your Device Provisioning service instance.</span><span class="sxs-lookup"><span data-stu-id="62771-167">In the Azure portal, go to your Device Provisioning service instance.</span></span> <span data-ttu-id="62771-168">Select **Manage enrollments**, and then select the **Individual Enrollments** tab. ![Individual enrollments](./media/how-to-connect-mxchip-iot-devkit/individual-enrollments.png)</span><span class="sxs-lookup"><span data-stu-id="62771-168">Select **Manage enrollments**, and then select the **Individual Enrollments** tab. ![Individual enrollments](./media/how-to-connect-mxchip-iot-devkit/individual-enrollments.png)</span></span>

2. <span data-ttu-id="62771-169">Select **Add**.</span><span class="sxs-lookup"><span data-stu-id="62771-169">Select **Add**.</span></span>

3. <span data-ttu-id="62771-170">On the "Add enrollment" panel:</span><span class="sxs-lookup"><span data-stu-id="62771-170">On the "Add enrollment" panel:</span></span>

   - <span data-ttu-id="62771-171">Select **X.509** under **Mechanism**.</span><span class="sxs-lookup"><span data-stu-id="62771-171">Select **X.509** under **Mechanism**.</span></span>
   - <span data-ttu-id="62771-172">Click "Select a file" under **Primary Certificate .pem or .cer file**.</span><span class="sxs-lookup"><span data-stu-id="62771-172">Click "Select a file" under **Primary Certificate .pem or .cer file**.</span></span>
   - <span data-ttu-id="62771-173">On the File Open dialog, navigate to and upload the **.pem** certificate you just generated.</span><span class="sxs-lookup"><span data-stu-id="62771-173">On the File Open dialog, navigate to and upload the **.pem** certificate you just generated.</span></span>
   - <span data-ttu-id="62771-174">Leave the rest as default and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="62771-174">Leave the rest as default and click **Save**.</span></span>

   ![Upload certificate](./media/how-to-connect-mxchip-iot-devkit/upload-cert.png)

  > [!NOTE]
  > <span data-ttu-id="62771-176">If you have an error with this message:</span><span class="sxs-lookup"><span data-stu-id="62771-176">If you have an error with this message:</span></span>
  >
  > `{"message":"BadRequest:{\r\n \"errorCode\": 400004,\r\n \"trackingId\": \"1b82d826-ccb4-4e54-91d3-0b25daee8974\",\r\n \"message\": \"The certificate is not a valid base64 string value\",\r\n \"timestampUtc\": \"2018-05-09T13:52:42.7122256Z\"\r\n}"}`
  >
  > <span data-ttu-id="62771-177">Open the certificate file **.pem** as text (open with Notepad or any text editor), and delete the lines:</span><span class="sxs-lookup"><span data-stu-id="62771-177">Open the certificate file **.pem** as text (open with Notepad or any text editor), and delete the lines:</span></span>
  >
  > <span data-ttu-id="62771-178">`"-----BEGIN CERTIFICATE-----"` and `"-----END CERTIFICATE-----"`.</span><span class="sxs-lookup"><span data-stu-id="62771-178">`"-----BEGIN CERTIFICATE-----"` and `"-----END CERTIFICATE-----"`.</span></span>
  >

## <a name="start-the-devkit"></a><span data-ttu-id="62771-179">Start the DevKit</span><span class="sxs-lookup"><span data-stu-id="62771-179">Start the DevKit</span></span>

1. <span data-ttu-id="62771-180">Open VS Code and the serial monitor.</span><span class="sxs-lookup"><span data-stu-id="62771-180">Open VS Code and the serial monitor.</span></span>

2. <span data-ttu-id="62771-181">Press the **Reset** button on your DevKit.</span><span class="sxs-lookup"><span data-stu-id="62771-181">Press the **Reset** button on your DevKit.</span></span>

<span data-ttu-id="62771-182">You see the DevKit start the registration with your Device Provisioning service.</span><span class="sxs-lookup"><span data-stu-id="62771-182">You see the DevKit start the registration with your Device Provisioning service.</span></span>

![VS Code output](./media/how-to-connect-mxchip-iot-devkit/vscode-output.png)

## <a name="verify-that-the-devkit-is-registered-with-azure-iot-hub"></a><span data-ttu-id="62771-184">Verify that the DevKit is registered with Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="62771-184">Verify that the DevKit is registered with Azure IoT Hub</span></span>

<span data-ttu-id="62771-185">After the device boots, the following actions take place:</span><span class="sxs-lookup"><span data-stu-id="62771-185">After the device boots, the following actions take place:</span></span>

1. <span data-ttu-id="62771-186">The device sends a registration request to your Device Provisioning service.</span><span class="sxs-lookup"><span data-stu-id="62771-186">The device sends a registration request to your Device Provisioning service.</span></span>
2. <span data-ttu-id="62771-187">The Device Provisioning service sends back a registration challenge to which your device responds.</span><span class="sxs-lookup"><span data-stu-id="62771-187">The Device Provisioning service sends back a registration challenge to which your device responds.</span></span>
3. <span data-ttu-id="62771-188">On successful registration, the Device Provisioning service sends the IoT Hub URI, device ID, and the encrypted key back to the device.</span><span class="sxs-lookup"><span data-stu-id="62771-188">On successful registration, the Device Provisioning service sends the IoT Hub URI, device ID, and the encrypted key back to the device.</span></span>
4. <span data-ttu-id="62771-189">The IoT Hub client application on the device connects to your hub.</span><span class="sxs-lookup"><span data-stu-id="62771-189">The IoT Hub client application on the device connects to your hub.</span></span>
5. <span data-ttu-id="62771-190">On successful connection to the hub, you see the device appear in the IoT Hub Device Explorer.</span><span class="sxs-lookup"><span data-stu-id="62771-190">On successful connection to the hub, you see the device appear in the IoT Hub Device Explorer.</span></span>
  <span data-ttu-id="62771-191">![Device registered](./media/how-to-connect-mxchip-iot-devkit/device-registered.png)</span><span class="sxs-lookup"><span data-stu-id="62771-191">![Device registered](./media/how-to-connect-mxchip-iot-devkit/device-registered.png)</span></span>

## <a name="problems-and-feedback"></a><span data-ttu-id="62771-192">Problems and feedback</span><span class="sxs-lookup"><span data-stu-id="62771-192">Problems and feedback</span></span>

<span data-ttu-id="62771-193">If you encounter problems, refer to the Iot DevKit [FAQs](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/), or reach out to the following channels for support:</span><span class="sxs-lookup"><span data-stu-id="62771-193">If you encounter problems, refer to the Iot DevKit [FAQs](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/), or reach out to the following channels for support:</span></span>

* [<span data-ttu-id="62771-194">Gitter.im</span><span class="sxs-lookup"><span data-stu-id="62771-194">Gitter.im</span></span>](http://gitter.im/Microsoft/azure-iot-developer-kit)
* [<span data-ttu-id="62771-195">Stackoverflow</span><span class="sxs-lookup"><span data-stu-id="62771-195">Stackoverflow</span></span>](https://stackoverflow.com/questions/tagged/iot-devkit)

## <a name="next-steps"></a><span data-ttu-id="62771-196">Next steps</span><span class="sxs-lookup"><span data-stu-id="62771-196">Next steps</span></span>

<span data-ttu-id="62771-197">In this tutorial, you learned to enroll a device securely to the Device Provisioning Service by using the Device Identity Composition Engine, so that the device can automatically register with Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="62771-197">In this tutorial, you learned to enroll a device securely to the Device Provisioning Service by using the Device Identity Composition Engine, so that the device can automatically register with Azure IoT Hub.</span></span> 

<span data-ttu-id="62771-198">In summary, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="62771-198">In summary, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="62771-199">Configure the global endpoint of the Device Provisioning service on a device.</span><span class="sxs-lookup"><span data-stu-id="62771-199">Configure the global endpoint of the Device Provisioning service on a device.</span></span>
> * <span data-ttu-id="62771-200">Use a unique device secret to generate an X.509 certificate.</span><span class="sxs-lookup"><span data-stu-id="62771-200">Use a unique device secret to generate an X.509 certificate.</span></span>
> * <span data-ttu-id="62771-201">Enroll an individual device.</span><span class="sxs-lookup"><span data-stu-id="62771-201">Enroll an individual device.</span></span>
> * <span data-ttu-id="62771-202">Verify that the device is registered.</span><span class="sxs-lookup"><span data-stu-id="62771-202">Verify that the device is registered.</span></span>

<span data-ttu-id="62771-203">Learn how to [Create and provision a simulated device](./quick-create-simulated-device.md).</span><span class="sxs-lookup"><span data-stu-id="62771-203">Learn how to [Create and provision a simulated device](./quick-create-simulated-device.md).</span></span>

