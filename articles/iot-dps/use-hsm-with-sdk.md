---
title: Azure How to - How to use different attestation mechanisms with the Device Provisioning Service Client SDK in Azure
description: Azure How to - How to use different attestation mechanisms with the Device Provisioning Service Client SDK in Azure
author: yzhong94
ms.author: yizhon
ms.date: 03/30/2018
ms.topic: conceptual
ms.service: iot-dps
services: iot-dps
manager: arjmands
ms.custom: mvc
ms.openlocfilehash: afd9adb05ffa919d22328fc5f484bcf5bc206422
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856502"
---
# <a name="how-to-use-different-attestation-mechanisms-with-device-provisioning-service-client-sdk-for-c"></a><span data-ttu-id="35e09-103">How to use different attestation mechanisms with Device Provisioning Service Client SDK for C</span><span class="sxs-lookup"><span data-stu-id="35e09-103">How to use different attestation mechanisms with Device Provisioning Service Client SDK for C</span></span>

<span data-ttu-id="35e09-104">This article shows you how to use different [attestation mechanisms](concepts-security.md#attestation-mechanism) with the Device Provisioning Service Client SDK for C. You can use either a physical device or a simulator.</span><span class="sxs-lookup"><span data-stu-id="35e09-104">This article shows you how to use different [attestation mechanisms](concepts-security.md#attestation-mechanism) with the Device Provisioning Service Client SDK for C. You can use either a physical device or a simulator.</span></span> <span data-ttu-id="35e09-105">The provisioning service supports authentication for two types of attestation mechanisms: X **.** 509 and Trusted Platform Module (TPM).</span><span class="sxs-lookup"><span data-stu-id="35e09-105">The provisioning service supports authentication for two types of attestation mechanisms: X **.** 509 and Trusted Platform Module (TPM).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35e09-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="35e09-106">Prerequisites</span></span>

<span data-ttu-id="35e09-107">Prepare your development environment according to the section titled "Prepare the development environment" in the [Create and provision simulated device](./quick-create-simulated-device.md) guide.</span><span class="sxs-lookup"><span data-stu-id="35e09-107">Prepare your development environment according to the section titled "Prepare the development environment" in the [Create and provision simulated device](./quick-create-simulated-device.md) guide.</span></span>

### <a name="choose-an-attestation-mechanism"></a><span data-ttu-id="35e09-108">Choose an attestation mechanism</span><span class="sxs-lookup"><span data-stu-id="35e09-108">Choose an attestation mechanism</span></span>

<span data-ttu-id="35e09-109">As a device manufacturer, you first need to choose an attestation mechanism based on one of the supported types.</span><span class="sxs-lookup"><span data-stu-id="35e09-109">As a device manufacturer, you first need to choose an attestation mechanism based on one of the supported types.</span></span> <span data-ttu-id="35e09-110">Currently, the [Device Provisioning Service client SDK for C](https://github.com/Azure/azure-iot-sdk-c/tree/master/provisioning_client) provides support for the following attestation mechanisms:</span><span class="sxs-lookup"><span data-stu-id="35e09-110">Currently, the [Device Provisioning Service client SDK for C](https://github.com/Azure/azure-iot-sdk-c/tree/master/provisioning_client) provides support for the following attestation mechanisms:</span></span> 

- <span data-ttu-id="35e09-111">[Trusted Platform Module (TPM)](https://en.wikipedia.org/wiki/Trusted_Platform_Module): TPM is an established standard for most Windows-based device platforms, as well as a few Linux/Ubuntu based devices.</span><span class="sxs-lookup"><span data-stu-id="35e09-111">[Trusted Platform Module (TPM)](https://en.wikipedia.org/wiki/Trusted_Platform_Module): TPM is an established standard for most Windows-based device platforms, as well as a few Linux/Ubuntu based devices.</span></span> <span data-ttu-id="35e09-112">As a device manufacturer, you may choose this attestation mechanism if you have either of these OSes running on your devices, and you are looking for an established standard.</span><span class="sxs-lookup"><span data-stu-id="35e09-112">As a device manufacturer, you may choose this attestation mechanism if you have either of these OSes running on your devices, and you are looking for an established standard.</span></span> <span data-ttu-id="35e09-113">With TPM chips, you can only enroll each device individually to the Device Provisioning Service.</span><span class="sxs-lookup"><span data-stu-id="35e09-113">With TPM chips, you can only enroll each device individually to the Device Provisioning Service.</span></span> <span data-ttu-id="35e09-114">For development purposes, you can use the TPM simulator on your Windows or Linux development machine.</span><span class="sxs-lookup"><span data-stu-id="35e09-114">For development purposes, you can use the TPM simulator on your Windows or Linux development machine.</span></span>

- <span data-ttu-id="35e09-115">[X.509](https://cryptography.io/en/latest/x509/): X.509 certificates can be stored in relatively newer chips called [Hardware Security Modules (HSM)](concepts-security.md#hardware-security-module).</span><span class="sxs-lookup"><span data-stu-id="35e09-115">[X.509](https://cryptography.io/en/latest/x509/): X.509 certificates can be stored in relatively newer chips called [Hardware Security Modules (HSM)](concepts-security.md#hardware-security-module).</span></span> <span data-ttu-id="35e09-116">Work is also progressing within Microsoft, on RIoT or DICE chips, which implement the X.509 certificates.</span><span class="sxs-lookup"><span data-stu-id="35e09-116">Work is also progressing within Microsoft, on RIoT or DICE chips, which implement the X.509 certificates.</span></span> <span data-ttu-id="35e09-117">With X.509 chips, you can do bulk device enrollment in the portal.</span><span class="sxs-lookup"><span data-stu-id="35e09-117">With X.509 chips, you can do bulk device enrollment in the portal.</span></span> <span data-ttu-id="35e09-118">It also supports certain non-Windows OSes like embedOS.</span><span class="sxs-lookup"><span data-stu-id="35e09-118">It also supports certain non-Windows OSes like embedOS.</span></span> <span data-ttu-id="35e09-119">For development purpose, the Device Provisioning Service client SDK supports an X.509 device simulator.</span><span class="sxs-lookup"><span data-stu-id="35e09-119">For development purpose, the Device Provisioning Service client SDK supports an X.509 device simulator.</span></span> 

<span data-ttu-id="35e09-120">For more information, see IoT Hub Device Provisioning Service [security concepts](concepts-security.md) and [auto-provisioning concepts](/azure/iot-dps/concepts-auto-provisioning).</span><span class="sxs-lookup"><span data-stu-id="35e09-120">For more information, see IoT Hub Device Provisioning Service [security concepts](concepts-security.md) and [auto-provisioning concepts](/azure/iot-dps/concepts-auto-provisioning).</span></span>

## <a name="enable-authentication-for-supported-attestation-mechanisms"></a><span data-ttu-id="35e09-121">Enable authentication for supported attestation mechanisms</span><span class="sxs-lookup"><span data-stu-id="35e09-121">Enable authentication for supported attestation mechanisms</span></span>

<span data-ttu-id="35e09-122">The SDK authentication mode (X **.** 509 or TPM) must be enabled for the physical device or simulator before they can be enrolled in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="35e09-122">The SDK authentication mode (X **.** 509 or TPM) must be enabled for the physical device or simulator before they can be enrolled in the Azure portal.</span></span> <span data-ttu-id="35e09-123">First, navigate to the root folder for azure-iot-sdk-c.</span><span class="sxs-lookup"><span data-stu-id="35e09-123">First, navigate to the root folder for azure-iot-sdk-c.</span></span> <span data-ttu-id="35e09-124">Then run the specified command, depending on the authentication mode you choose:</span><span class="sxs-lookup"><span data-stu-id="35e09-124">Then run the specified command, depending on the authentication mode you choose:</span></span>

### <a name="use-x509-with-simulator"></a><span data-ttu-id="35e09-125">Use X **.** 509 with simulator</span><span class="sxs-lookup"><span data-stu-id="35e09-125">Use X **.** 509 with simulator</span></span>

<span data-ttu-id="35e09-126">The provisioning service ships with a Device Identity Composition Engine (DICE) emulator that generates an X **.** 509 certificate for authenticating the device.</span><span class="sxs-lookup"><span data-stu-id="35e09-126">The provisioning service ships with a Device Identity Composition Engine (DICE) emulator that generates an X **.** 509 certificate for authenticating the device.</span></span> <span data-ttu-id="35e09-127">To enable X **.** 509 authentication, run the following command:</span><span class="sxs-lookup"><span data-stu-id="35e09-127">To enable X **.** 509 authentication, run the following command:</span></span> 

```
cmake -Ddps_auth_type=x509 ..
```

<span data-ttu-id="35e09-128">Information regarding hardware with DICE can be found [here](https://azure.microsoft.com/blog/azure-iot-supports-new-security-hardware-to-strengthen-iot-security/).</span><span class="sxs-lookup"><span data-stu-id="35e09-128">Information regarding hardware with DICE can be found [here](https://azure.microsoft.com/blog/azure-iot-supports-new-security-hardware-to-strengthen-iot-security/).</span></span>

### <a name="use-x509-with-hardware"></a><span data-ttu-id="35e09-129">Use X **.** 509 with hardware</span><span class="sxs-lookup"><span data-stu-id="35e09-129">Use X **.** 509 with hardware</span></span>

<span data-ttu-id="35e09-130">The provisioning service can be used with X **.** 509 on other hardware.</span><span class="sxs-lookup"><span data-stu-id="35e09-130">The provisioning service can be used with X **.** 509 on other hardware.</span></span> <span data-ttu-id="35e09-131">An interface between hardware and the SDK is needed to establish connection.</span><span class="sxs-lookup"><span data-stu-id="35e09-131">An interface between hardware and the SDK is needed to establish connection.</span></span> <span data-ttu-id="35e09-132">Talk to your HSM manufacturer for information on the interface.</span><span class="sxs-lookup"><span data-stu-id="35e09-132">Talk to your HSM manufacturer for information on the interface.</span></span>

### <a name="use-tpm"></a><span data-ttu-id="35e09-133">Use TPM</span><span class="sxs-lookup"><span data-stu-id="35e09-133">Use TPM</span></span>

<span data-ttu-id="35e09-134">The provisioning service can connect to Windows and Linux hardware TPM chips with SAS Token.</span><span class="sxs-lookup"><span data-stu-id="35e09-134">The provisioning service can connect to Windows and Linux hardware TPM chips with SAS Token.</span></span> <span data-ttu-id="35e09-135">To enable TPM authentication, run the following command:</span><span class="sxs-lookup"><span data-stu-id="35e09-135">To enable TPM authentication, run the following command:</span></span>

```
cmake -Ddps_auth_type=tpm ..
```

### <a name="use-tpm-with-simulator"></a><span data-ttu-id="35e09-136">Use TPM with simulator</span><span class="sxs-lookup"><span data-stu-id="35e09-136">Use TPM with simulator</span></span>

<span data-ttu-id="35e09-137">If you don't have a device with TPM chips, you can use a simulator for development purpose on Windows OS.</span><span class="sxs-lookup"><span data-stu-id="35e09-137">If you don't have a device with TPM chips, you can use a simulator for development purpose on Windows OS.</span></span> <span data-ttu-id="35e09-138">To enable TPM authentication and run the TPM simulator, run the following command:</span><span class="sxs-lookup"><span data-stu-id="35e09-138">To enable TPM authentication and run the TPM simulator, run the following command:</span></span>

```
cmake -Ddps_auth_type=tpm_simulator ..
```

## <a name="build-the-sdk"></a><span data-ttu-id="35e09-139">Build the SDK</span><span class="sxs-lookup"><span data-stu-id="35e09-139">Build the SDK</span></span>
<span data-ttu-id="35e09-140">Build the SDK prior to creating device enrollment.</span><span class="sxs-lookup"><span data-stu-id="35e09-140">Build the SDK prior to creating device enrollment.</span></span>

### <a name="linux"></a><span data-ttu-id="35e09-141">Linux</span><span class="sxs-lookup"><span data-stu-id="35e09-141">Linux</span></span>
- <span data-ttu-id="35e09-142">To build the SDK in Linux:</span><span class="sxs-lookup"><span data-stu-id="35e09-142">To build the SDK in Linux:</span></span>
    ```
    cd azure-iot-sdk-c
    mkdir cmake
    cd cmake
    cmake ..
    cmake --build .  # append '-- -j <n>' to run <n> jobs in parallel
    ```
- <span data-ttu-id="35e09-143">To build Debug binaries, add the corresponding CMake option to the project generation command, for example:</span><span class="sxs-lookup"><span data-stu-id="35e09-143">To build Debug binaries, add the corresponding CMake option to the project generation command, for example:</span></span>
    ```
    cmake -DCMAKE_BUILD_TYPE=Debug ..
    ```

- <span data-ttu-id="35e09-144">There are many [CMake configuration options](https://cmake.org/cmake/help/v3.6/manual/cmake.1.html) available for building the SDK.</span><span class="sxs-lookup"><span data-stu-id="35e09-144">There are many [CMake configuration options](https://cmake.org/cmake/help/v3.6/manual/cmake.1.html) available for building the SDK.</span></span> <span data-ttu-id="35e09-145">For example, you can disable one of the available protocol stacks by adding an argument to the CMake project generation command:</span><span class="sxs-lookup"><span data-stu-id="35e09-145">For example, you can disable one of the available protocol stacks by adding an argument to the CMake project generation command:</span></span>
    ```
    cmake -Duse_amqp=OFF ..
    ```
- <span data-ttu-id="35e09-146">You can also build and run unit test:</span><span class="sxs-lookup"><span data-stu-id="35e09-146">You can also build and run unit test:</span></span>
    ```
    cmake -Drun_unittests=ON ..
    cmake --build .
    ctest -C "debug" -V
    ```

### <a name="windows"></a><span data-ttu-id="35e09-147">Windows</span><span class="sxs-lookup"><span data-stu-id="35e09-147">Windows</span></span>
- <span data-ttu-id="35e09-148">To build the SDK in Windows, take the following steps to generate project files:</span><span class="sxs-lookup"><span data-stu-id="35e09-148">To build the SDK in Windows, take the following steps to generate project files:</span></span>
    - <span data-ttu-id="35e09-149">Open a "Developer Command Prompt for VS2015"</span><span class="sxs-lookup"><span data-stu-id="35e09-149">Open a "Developer Command Prompt for VS2015"</span></span>
    - <span data-ttu-id="35e09-150">Run the following CMake commands from the root of the repository:</span><span class="sxs-lookup"><span data-stu-id="35e09-150">Run the following CMake commands from the root of the repository:</span></span>
      ```
      cd azure-iot-sdk-c
      mkdir cmake
      cd cmake
      cmake -G "Visual Studio 14 2015" ..
      ```
    <span data-ttu-id="35e09-151">This command builds x86 libraries.</span><span class="sxs-lookup"><span data-stu-id="35e09-151">This command builds x86 libraries.</span></span> <span data-ttu-id="35e09-152">To build for x64, modify the cmake generator argument:</span><span class="sxs-lookup"><span data-stu-id="35e09-152">To build for x64, modify the cmake generator argument:</span></span> 
    ```
    cmake .. -G "Visual Studio 14 2015 Win64"
    ```

- <span data-ttu-id="35e09-153">If project generation completes successfully, you should see a Visual Studio solution file (.sln) under the `cmake` folder.</span><span class="sxs-lookup"><span data-stu-id="35e09-153">If project generation completes successfully, you should see a Visual Studio solution file (.sln) under the `cmake` folder.</span></span> <span data-ttu-id="35e09-154">To build the SDK:</span><span class="sxs-lookup"><span data-stu-id="35e09-154">To build the SDK:</span></span>
    - <span data-ttu-id="35e09-155">Open **cmake\azure_iot_sdks.sln** in Visual Studio and build it, **OR**</span><span class="sxs-lookup"><span data-stu-id="35e09-155">Open **cmake\azure_iot_sdks.sln** in Visual Studio and build it, **OR**</span></span>
    - <span data-ttu-id="35e09-156">Run the following command in the command prompt you used to generate the project files:</span><span class="sxs-lookup"><span data-stu-id="35e09-156">Run the following command in the command prompt you used to generate the project files:</span></span>
      ```
      cmake --build . -- /m /p:Configuration=Release
      ```
- <span data-ttu-id="35e09-157">To build Debug binaries, use the corresponding MSBuild argument:</span><span class="sxs-lookup"><span data-stu-id="35e09-157">To build Debug binaries, use the corresponding MSBuild argument:</span></span> 
    ```
    cmake --build . -- /m /p:Configuration=Debug`
    ```
- <span data-ttu-id="35e09-158">There are many CMake configuration options available for building the SDK.</span><span class="sxs-lookup"><span data-stu-id="35e09-158">There are many CMake configuration options available for building the SDK.</span></span> <span data-ttu-id="35e09-159">For example, you can disable one of the available protocol stacks by adding an argument to the CMake project generation command:</span><span class="sxs-lookup"><span data-stu-id="35e09-159">For example, you can disable one of the available protocol stacks by adding an argument to the CMake project generation command:</span></span>
    ```
    cmake -G "Visual Studio 14 2015" -Duse_amqp=OFF ..
    ```
- <span data-ttu-id="35e09-160">Also, you can build and run unit tests:</span><span class="sxs-lookup"><span data-stu-id="35e09-160">Also, you can build and run unit tests:</span></span>
    ```
    cmake -G "Visual Studio 14 2015" -Drun_unittests=ON ..
    cmake --build . -- /m /p:Configuration=Debug
    ctest -C "debug" -V
    ```
  
### <a name="libraries-to-include"></a><span data-ttu-id="35e09-161">Libraries to include</span><span class="sxs-lookup"><span data-stu-id="35e09-161">Libraries to include</span></span>
- <span data-ttu-id="35e09-162">These libraries should be included in your SDK:</span><span class="sxs-lookup"><span data-stu-id="35e09-162">These libraries should be included in your SDK:</span></span>
    - <span data-ttu-id="35e09-163">The provisioning service: dps_http_transport, dps_client, dps_security_client</span><span class="sxs-lookup"><span data-stu-id="35e09-163">The provisioning service: dps_http_transport, dps_client, dps_security_client</span></span>
    - <span data-ttu-id="35e09-164">IoTHub Security: iothub_security_client</span><span class="sxs-lookup"><span data-stu-id="35e09-164">IoTHub Security: iothub_security_client</span></span>

## <a name="create-a-device-enrollment-entry-in-device-provisioning-services"></a><span data-ttu-id="35e09-165">Create a device enrollment entry in Device Provisioning Services</span><span class="sxs-lookup"><span data-stu-id="35e09-165">Create a device enrollment entry in Device Provisioning Services</span></span>

### <a name="tpm"></a><span data-ttu-id="35e09-166">TPM</span><span class="sxs-lookup"><span data-stu-id="35e09-166">TPM</span></span>
<span data-ttu-id="35e09-167">If you are using TPM, follow instructions in ["Create and provision a simulated device using IoT Hub Device Provisioning Service"](./quick-create-simulated-device.md) to create a device enrollment entry in your Device Provisioning Service and simulate first boot.</span><span class="sxs-lookup"><span data-stu-id="35e09-167">If you are using TPM, follow instructions in ["Create and provision a simulated device using IoT Hub Device Provisioning Service"](./quick-create-simulated-device.md) to create a device enrollment entry in your Device Provisioning Service and simulate first boot.</span></span>

### <a name="x509"></a><span data-ttu-id="35e09-168">X **.** 509</span><span class="sxs-lookup"><span data-stu-id="35e09-168">X **.** 509</span></span>
1. <span data-ttu-id="35e09-169">To enroll a device in the provisioning service, you need note down the Endorsement Key and Registration ID for each device, which are displayed in the Provisioning Tool provided by Client SDK.</span><span class="sxs-lookup"><span data-stu-id="35e09-169">To enroll a device in the provisioning service, you need note down the Endorsement Key and Registration ID for each device, which are displayed in the Provisioning Tool provided by Client SDK.</span></span> <span data-ttu-id="35e09-170">Run the following command to print out the root CA certificate (for enrollment groups) and the leaf certificate (for individual enrollment):</span><span class="sxs-lookup"><span data-stu-id="35e09-170">Run the following command to print out the root CA certificate (for enrollment groups) and the leaf certificate (for individual enrollment):</span></span>
      ```
      ./azure-iot-sdk-c/dps_client/tools/x509_device_provision/x509_device_provision.exe
      ```
2. <span data-ttu-id="35e09-171">Sign in to the Azure portal, click on the **All resources** button on the left-hand menu and open your Device Provisioning service.</span><span class="sxs-lookup"><span data-stu-id="35e09-171">Sign in to the Azure portal, click on the **All resources** button on the left-hand menu and open your Device Provisioning service.</span></span>
   - <span data-ttu-id="35e09-172">X **.** 509 Individual Enrollment: On the provisioning service summary blade, select **Manage enrollments**.</span><span class="sxs-lookup"><span data-stu-id="35e09-172">X **.** 509 Individual Enrollment: On the provisioning service summary blade, select **Manage enrollments**.</span></span> <span data-ttu-id="35e09-173">Select **Individual Enrollments** tab and click the **Add** button at the top.</span><span class="sxs-lookup"><span data-stu-id="35e09-173">Select **Individual Enrollments** tab and click the **Add** button at the top.</span></span> <span data-ttu-id="35e09-174">Select **X**.**509** as the identity attestation *Mechanism*, upload the leaf certificate as required by the blade.</span><span class="sxs-lookup"><span data-stu-id="35e09-174">Select **X**.**509** as the identity attestation *Mechanism*, upload the leaf certificate as required by the blade.</span></span> <span data-ttu-id="35e09-175">Once complete, click the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="35e09-175">Once complete, click the **Save** button.</span></span> 
   - <span data-ttu-id="35e09-176">X **.** 509 Group Enrollment: On the provisioning service  summary blade, select **Manage enrollments**.</span><span class="sxs-lookup"><span data-stu-id="35e09-176">X **.** 509 Group Enrollment: On the provisioning service  summary blade, select **Manage enrollments**.</span></span> <span data-ttu-id="35e09-177">Select **Group Enrollments** tab and click the **Add** button at the top.</span><span class="sxs-lookup"><span data-stu-id="35e09-177">Select **Group Enrollments** tab and click the **Add** button at the top.</span></span> <span data-ttu-id="35e09-178">Select **X**.**509** as the identity attestation *Mechanism*, enter a group name and certification name, upload the CA/Intermediate certificate as required by the blade.</span><span class="sxs-lookup"><span data-stu-id="35e09-178">Select **X**.**509** as the identity attestation *Mechanism*, enter a group name and certification name, upload the CA/Intermediate certificate as required by the blade.</span></span> <span data-ttu-id="35e09-179">Once complete, click the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="35e09-179">Once complete, click the **Save** button.</span></span> 

## <a name="enable-authentication-for-devices-using-a-custom-attestation-mechanism-optional"></a><span data-ttu-id="35e09-180">Enable authentication for devices using a custom attestation mechanism (optional)</span><span class="sxs-lookup"><span data-stu-id="35e09-180">Enable authentication for devices using a custom attestation mechanism (optional)</span></span>

> [!NOTE]
> <span data-ttu-id="35e09-181">This section is only applicable to devices that require support for a custom platform or attestation mechanisms, not currently supported by the Device Provisioning Service Client SDK for C. Also note, the SDK frequently uses the term "HSM" as a generic substitute in place of "attestation mechanism."</span><span class="sxs-lookup"><span data-stu-id="35e09-181">This section is only applicable to devices that require support for a custom platform or attestation mechanisms, not currently supported by the Device Provisioning Service Client SDK for C. Also note, the SDK frequently uses the term "HSM" as a generic substitute in place of "attestation mechanism."</span></span>

<span data-ttu-id="35e09-182">First you need to develop a repository and library for your custom attestation mechanism:</span><span class="sxs-lookup"><span data-stu-id="35e09-182">First you need to develop a repository and library for your custom attestation mechanism:</span></span>

1. <span data-ttu-id="35e09-183">Develop a library to access your attestation mechanism.</span><span class="sxs-lookup"><span data-stu-id="35e09-183">Develop a library to access your attestation mechanism.</span></span> <span data-ttu-id="35e09-184">This project needs to produce a static library for the Device Provisioning SDK to consume.</span><span class="sxs-lookup"><span data-stu-id="35e09-184">This project needs to produce a static library for the Device Provisioning SDK to consume.</span></span>

2. <span data-ttu-id="35e09-185">Implement the functions defined in the following header file, in your library:</span><span class="sxs-lookup"><span data-stu-id="35e09-185">Implement the functions defined in the following header file, in your library:</span></span> 

    - <span data-ttu-id="35e09-186">For a custom TPM: implement the functions defined under [HSM TPM API](https://github.com/Azure/azure-iot-sdk-c/blob/master/provisioning_client/devdoc/using_custom_hsm.md#hsm-tpm-api).</span><span class="sxs-lookup"><span data-stu-id="35e09-186">For a custom TPM: implement the functions defined under [HSM TPM API](https://github.com/Azure/azure-iot-sdk-c/blob/master/provisioning_client/devdoc/using_custom_hsm.md#hsm-tpm-api).</span></span>  
    - <span data-ttu-id="35e09-187">For a custom X.509: implement the functions defined under [HSM X509 API](https://github.com/Azure/azure-iot-sdk-c/blob/master/provisioning_client/devdoc/using_custom_hsm.md#hsm-x509-api).</span><span class="sxs-lookup"><span data-stu-id="35e09-187">For a custom X.509: implement the functions defined under [HSM X509 API](https://github.com/Azure/azure-iot-sdk-c/blob/master/provisioning_client/devdoc/using_custom_hsm.md#hsm-x509-api).</span></span> 

<span data-ttu-id="35e09-188">Once your library successfully builds on its own, you need to integrate it with the Device Provisioning Service Client SDK, by linking against your library.</span><span class="sxs-lookup"><span data-stu-id="35e09-188">Once your library successfully builds on its own, you need to integrate it with the Device Provisioning Service Client SDK, by linking against your library.</span></span> <span data-ttu-id="35e09-189">:</span><span class="sxs-lookup"><span data-stu-id="35e09-189">:</span></span>

1. <span data-ttu-id="35e09-190">Supply the custom GitHub repository and the library in the following `cmake` command:</span><span class="sxs-lookup"><span data-stu-id="35e09-190">Supply the custom GitHub repository and the library in the following `cmake` command:</span></span>
    ```cmd/sh
    cmake -Duse_prov_client:BOOL=ON -Dhsm_custom_lib=<path_and_name_of_library> <PATH_TO_AZURE_IOT_SDK>
    ```
   
2. <span data-ttu-id="35e09-191">Open the Visual Studio solution file built by CMake (`\azure-iot-sdk-c\cmake\azure_iot_sdks.sln`), and build it.</span><span class="sxs-lookup"><span data-stu-id="35e09-191">Open the Visual Studio solution file built by CMake (`\azure-iot-sdk-c\cmake\azure_iot_sdks.sln`), and build it.</span></span> 

    - <span data-ttu-id="35e09-192">The build process compiles the SDK library.</span><span class="sxs-lookup"><span data-stu-id="35e09-192">The build process compiles the SDK library.</span></span>
    - <span data-ttu-id="35e09-193">The SDK attempts to link against the custom library defined in the `cmake` command.</span><span class="sxs-lookup"><span data-stu-id="35e09-193">The SDK attempts to link against the custom library defined in the `cmake` command.</span></span>

3. <span data-ttu-id="35e09-194">To verify that your custom attestation mechanism is implemented correctly, run the "prov_dev_client_ll_sample" sample app under "Provision_Samples" (under `\azure-iot-sdk-c\cmake\provisioning_client\samples\prov_dev_client_ll_sample`).</span><span class="sxs-lookup"><span data-stu-id="35e09-194">To verify that your custom attestation mechanism is implemented correctly, run the "prov_dev_client_ll_sample" sample app under "Provision_Samples" (under `\azure-iot-sdk-c\cmake\provisioning_client\samples\prov_dev_client_ll_sample`).</span></span>

## <a name="connecting-to-iot-hub-after-provisioning"></a><span data-ttu-id="35e09-195">Connecting to IoT Hub after provisioning</span><span class="sxs-lookup"><span data-stu-id="35e09-195">Connecting to IoT Hub after provisioning</span></span>

<span data-ttu-id="35e09-196">Once the device has been provisioned with the provisioning service, this API uses the specified authentication mode (X **.** 509 or TPM) to connect with IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="35e09-196">Once the device has been provisioned with the provisioning service, this API uses the specified authentication mode (X **.** 509 or TPM) to connect with IoT Hub:</span></span> 
  ```
  IOTHUB_CLIENT_LL_HANDLE handle = IoTHubClient_LL_CreateFromDeviceAuth(iothub_uri, device_id, iothub_transport);
  ```

