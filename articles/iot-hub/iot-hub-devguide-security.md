---
title: Understand Azure IoT Hub security | Microsoft Docs
description: Developer guide - how to control access to IoT Hub for device apps and back-end apps. Includes information about security tokens and support for X.509 certificates.
author: dominicbetts
manager: timlt
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.date: 07/18/2018
ms.author: dobett
ms.openlocfilehash: 227723ecea1401247f0df87bccfe058fb2273647
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44780980"
---
# <a name="control-access-to-iot-hub"></a><span data-ttu-id="2b581-104">Control access to IoT Hub</span><span class="sxs-lookup"><span data-stu-id="2b581-104">Control access to IoT Hub</span></span>

<span data-ttu-id="2b581-105">This article describes the options for securing your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="2b581-105">This article describes the options for securing your IoT hub.</span></span> <span data-ttu-id="2b581-106">IoT Hub uses *permissions* to grant access to each IoT hub endpoint.</span><span class="sxs-lookup"><span data-stu-id="2b581-106">IoT Hub uses *permissions* to grant access to each IoT hub endpoint.</span></span> <span data-ttu-id="2b581-107">Permissions limit the access to an IoT hub based on functionality.</span><span class="sxs-lookup"><span data-stu-id="2b581-107">Permissions limit the access to an IoT hub based on functionality.</span></span>

<span data-ttu-id="2b581-108">This article introduces:</span><span class="sxs-lookup"><span data-stu-id="2b581-108">This article introduces:</span></span>

* <span data-ttu-id="2b581-109">The different permissions that you can grant to a device or back-end app to access your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="2b581-109">The different permissions that you can grant to a device or back-end app to access your IoT hub.</span></span>
* <span data-ttu-id="2b581-110">The authentication process and the tokens it uses to verify permissions.</span><span class="sxs-lookup"><span data-stu-id="2b581-110">The authentication process and the tokens it uses to verify permissions.</span></span>
* <span data-ttu-id="2b581-111">How to scope credentials to limit access to specific resources.</span><span class="sxs-lookup"><span data-stu-id="2b581-111">How to scope credentials to limit access to specific resources.</span></span>
* <span data-ttu-id="2b581-112">IoT Hub support for X.509 certificates.</span><span class="sxs-lookup"><span data-stu-id="2b581-112">IoT Hub support for X.509 certificates.</span></span>
* <span data-ttu-id="2b581-113">Custom device authentication mechanisms that use existing device identity registries or authentication schemes.</span><span class="sxs-lookup"><span data-stu-id="2b581-113">Custom device authentication mechanisms that use existing device identity registries or authentication schemes.</span></span>

[!INCLUDE [iot-hub-basic](../../includes/iot-hub-basic-partial.md)]

<span data-ttu-id="2b581-114">You must have appropriate permissions to access any of the IoT Hub endpoints.</span><span class="sxs-lookup"><span data-stu-id="2b581-114">You must have appropriate permissions to access any of the IoT Hub endpoints.</span></span> <span data-ttu-id="2b581-115">For example, a device must include a token containing security credentials along with every message it sends to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2b581-115">For example, a device must include a token containing security credentials along with every message it sends to IoT Hub.</span></span>

## <a name="access-control-and-permissions"></a><span data-ttu-id="2b581-116">Access control and permissions</span><span class="sxs-lookup"><span data-stu-id="2b581-116">Access control and permissions</span></span>

<span data-ttu-id="2b581-117">You can grant [permissions](#iot-hub-permissions) in the following ways:</span><span class="sxs-lookup"><span data-stu-id="2b581-117">You can grant [permissions](#iot-hub-permissions) in the following ways:</span></span>

* <span data-ttu-id="2b581-118">**IoT hub-level shared access policies**.</span><span class="sxs-lookup"><span data-stu-id="2b581-118">**IoT hub-level shared access policies**.</span></span> <span data-ttu-id="2b581-119">Shared access policies can grant any combination of [permissions](#iot-hub-permissions).</span><span class="sxs-lookup"><span data-stu-id="2b581-119">Shared access policies can grant any combination of [permissions](#iot-hub-permissions).</span></span> <span data-ttu-id="2b581-120">You can define policies in the [Azure portal][lnk-management-portal], programmatically by using the [IoT Hub Resource REST APIs][lnk-resource-provider-apis], or using the [az iot hub policy](https://docs.microsoft.com/cli/azure/iot/hub/policy?view=azure-cli-latest) CLI.</span><span class="sxs-lookup"><span data-stu-id="2b581-120">You can define policies in the [Azure portal][lnk-management-portal], programmatically by using the [IoT Hub Resource REST APIs][lnk-resource-provider-apis], or using the [az iot hub policy](https://docs.microsoft.com/cli/azure/iot/hub/policy?view=azure-cli-latest) CLI.</span></span> <span data-ttu-id="2b581-121">A newly created IoT hub has the following default policies:</span><span class="sxs-lookup"><span data-stu-id="2b581-121">A newly created IoT hub has the following default policies:</span></span>
  
  | <span data-ttu-id="2b581-122">Shared Access Policy</span><span class="sxs-lookup"><span data-stu-id="2b581-122">Shared Access Policy</span></span> | <span data-ttu-id="2b581-123">Permissions</span><span class="sxs-lookup"><span data-stu-id="2b581-123">Permissions</span></span> |
  | -------------------- | ----------- |
  | <span data-ttu-id="2b581-124">iothubowner</span><span class="sxs-lookup"><span data-stu-id="2b581-124">iothubowner</span></span> | <span data-ttu-id="2b581-125">All permission</span><span class="sxs-lookup"><span data-stu-id="2b581-125">All permission</span></span> |
  | <span data-ttu-id="2b581-126">service</span><span class="sxs-lookup"><span data-stu-id="2b581-126">service</span></span> | <span data-ttu-id="2b581-127">**ServiceConnect** permissions</span><span class="sxs-lookup"><span data-stu-id="2b581-127">**ServiceConnect** permissions</span></span> |
  | <span data-ttu-id="2b581-128">device</span><span class="sxs-lookup"><span data-stu-id="2b581-128">device</span></span> | <span data-ttu-id="2b581-129">**DeviceConnect** permissions</span><span class="sxs-lookup"><span data-stu-id="2b581-129">**DeviceConnect** permissions</span></span> |
  | <span data-ttu-id="2b581-130">registryRead</span><span class="sxs-lookup"><span data-stu-id="2b581-130">registryRead</span></span> | <span data-ttu-id="2b581-131">**RegistryRead** permissions</span><span class="sxs-lookup"><span data-stu-id="2b581-131">**RegistryRead** permissions</span></span> |
  | <span data-ttu-id="2b581-132">registryReadWrite</span><span class="sxs-lookup"><span data-stu-id="2b581-132">registryReadWrite</span></span> | <span data-ttu-id="2b581-133">**RegistryRead** and **RegistryWrite** permissions</span><span class="sxs-lookup"><span data-stu-id="2b581-133">**RegistryRead** and **RegistryWrite** permissions</span></span> |

* <span data-ttu-id="2b581-134">**Per-Device Security Credentials**.</span><span class="sxs-lookup"><span data-stu-id="2b581-134">**Per-Device Security Credentials**.</span></span> <span data-ttu-id="2b581-135">Each IoT Hub contains an [identity registry][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="2b581-135">Each IoT Hub contains an [identity registry][lnk-identity-registry].</span></span> <span data-ttu-id="2b581-136">For each device in this identity registry, you can configure security credentials that grant **DeviceConnect** permissions scoped to the corresponding device endpoints.</span><span class="sxs-lookup"><span data-stu-id="2b581-136">For each device in this identity registry, you can configure security credentials that grant **DeviceConnect** permissions scoped to the corresponding device endpoints.</span></span>

<span data-ttu-id="2b581-137">For example, in a typical IoT solution:</span><span class="sxs-lookup"><span data-stu-id="2b581-137">For example, in a typical IoT solution:</span></span>

* <span data-ttu-id="2b581-138">The device management component uses the *registryReadWrite* policy.</span><span class="sxs-lookup"><span data-stu-id="2b581-138">The device management component uses the *registryReadWrite* policy.</span></span>
* <span data-ttu-id="2b581-139">The event processor component uses the *service* policy.</span><span class="sxs-lookup"><span data-stu-id="2b581-139">The event processor component uses the *service* policy.</span></span>
* <span data-ttu-id="2b581-140">The run-time device business logic component uses the *service* policy.</span><span class="sxs-lookup"><span data-stu-id="2b581-140">The run-time device business logic component uses the *service* policy.</span></span>
* <span data-ttu-id="2b581-141">Individual devices connect using credentials stored in the IoT hub's identity registry.</span><span class="sxs-lookup"><span data-stu-id="2b581-141">Individual devices connect using credentials stored in the IoT hub's identity registry.</span></span>

> [!NOTE]
> <span data-ttu-id="2b581-142">See [permissions](#iot-hub-permissions) for detailed information.</span><span class="sxs-lookup"><span data-stu-id="2b581-142">See [permissions](#iot-hub-permissions) for detailed information.</span></span>

## <a name="authentication"></a><span data-ttu-id="2b581-143">Authentication</span><span class="sxs-lookup"><span data-stu-id="2b581-143">Authentication</span></span>

<span data-ttu-id="2b581-144">Azure IoT Hub grants access to endpoints by verifying a token against the shared access policies and identity registry security credentials.</span><span class="sxs-lookup"><span data-stu-id="2b581-144">Azure IoT Hub grants access to endpoints by verifying a token against the shared access policies and identity registry security credentials.</span></span>

<span data-ttu-id="2b581-145">Security credentials, such as symmetric keys, are never sent over the wire.</span><span class="sxs-lookup"><span data-stu-id="2b581-145">Security credentials, such as symmetric keys, are never sent over the wire.</span></span>

> [!NOTE]
> <span data-ttu-id="2b581-146">The Azure IoT Hub resource provider is secured through your Azure subscription, as are all providers in the [Azure Resource Manager][lnk-azure-resource-manager].</span><span class="sxs-lookup"><span data-stu-id="2b581-146">The Azure IoT Hub resource provider is secured through your Azure subscription, as are all providers in the [Azure Resource Manager][lnk-azure-resource-manager].</span></span>

<span data-ttu-id="2b581-147">For more information about how to construct and use security tokens, see [IoT Hub security tokens][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="2b581-147">For more information about how to construct and use security tokens, see [IoT Hub security tokens][lnk-sas-tokens].</span></span>

### <a name="protocol-specifics"></a><span data-ttu-id="2b581-148">Protocol specifics</span><span class="sxs-lookup"><span data-stu-id="2b581-148">Protocol specifics</span></span>

<span data-ttu-id="2b581-149">Each supported protocol, such as MQTT, AMQP, and HTTPS, transports tokens in different ways.</span><span class="sxs-lookup"><span data-stu-id="2b581-149">Each supported protocol, such as MQTT, AMQP, and HTTPS, transports tokens in different ways.</span></span>

<span data-ttu-id="2b581-150">When using MQTT, the CONNECT packet has the deviceId as the ClientId, `{iothubhostname}/{deviceId}` in the Username field, and a SAS token in the Password field.</span><span class="sxs-lookup"><span data-stu-id="2b581-150">When using MQTT, the CONNECT packet has the deviceId as the ClientId, `{iothubhostname}/{deviceId}` in the Username field, and a SAS token in the Password field.</span></span> <span data-ttu-id="2b581-151">`{iothubhostname}` should be the full CName of the IoT hub (for example, contoso.azure-devices.net).</span><span class="sxs-lookup"><span data-stu-id="2b581-151">`{iothubhostname}` should be the full CName of the IoT hub (for example, contoso.azure-devices.net).</span></span>

<span data-ttu-id="2b581-152">When using [AMQP][lnk-amqp], IoT Hub supports [SASL PLAIN][lnk-sasl-plain] and [AMQP Claims-Based-Security][lnk-cbs].</span><span class="sxs-lookup"><span data-stu-id="2b581-152">When using [AMQP][lnk-amqp], IoT Hub supports [SASL PLAIN][lnk-sasl-plain] and [AMQP Claims-Based-Security][lnk-cbs].</span></span>

<span data-ttu-id="2b581-153">If you use AMQP claims-based-security, the standard specifies how to transmit these tokens.</span><span class="sxs-lookup"><span data-stu-id="2b581-153">If you use AMQP claims-based-security, the standard specifies how to transmit these tokens.</span></span>

<span data-ttu-id="2b581-154">For SASL PLAIN, the **username** can be:</span><span class="sxs-lookup"><span data-stu-id="2b581-154">For SASL PLAIN, the **username** can be:</span></span>

* <span data-ttu-id="2b581-155">`{policyName}@sas.root.{iothubName}` if using IoT hub-level tokens.</span><span class="sxs-lookup"><span data-stu-id="2b581-155">`{policyName}@sas.root.{iothubName}` if using IoT hub-level tokens.</span></span>
* <span data-ttu-id="2b581-156">`{deviceId}@sas.{iothubname}` if using device-scoped tokens.</span><span class="sxs-lookup"><span data-stu-id="2b581-156">`{deviceId}@sas.{iothubname}` if using device-scoped tokens.</span></span>

<span data-ttu-id="2b581-157">In both cases, the password field contains the token, as described in [IoT Hub security tokens][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="2b581-157">In both cases, the password field contains the token, as described in [IoT Hub security tokens][lnk-sas-tokens].</span></span>

<span data-ttu-id="2b581-158">HTTPS implements authentication by including a valid token in the **Authorization** request header.</span><span class="sxs-lookup"><span data-stu-id="2b581-158">HTTPS implements authentication by including a valid token in the **Authorization** request header.</span></span>

#### <a name="example"></a><span data-ttu-id="2b581-159">Example</span><span class="sxs-lookup"><span data-stu-id="2b581-159">Example</span></span>

<span data-ttu-id="2b581-160">Username (DeviceId is case-sensitive): `iothubname.azure-devices.net/DeviceId`</span><span class="sxs-lookup"><span data-stu-id="2b581-160">Username (DeviceId is case-sensitive): `iothubname.azure-devices.net/DeviceId`</span></span>

<span data-ttu-id="2b581-161">Password (You can generate a SAS token with the [device explorer][lnk-device-explorer] tool, the CLI extension command [az iot hub generate-sas-token](https://docs.microsoft.com/cli/azure/ext/azure-cli-iot-ext/iot/hub?view=azure-cli-latest#ext-azure-cli-iot-ext-az-iot-hub-generate-sas-token), or the [Azure IoT Toolkit extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-toolkit)):</span><span class="sxs-lookup"><span data-stu-id="2b581-161">Password (You can generate a SAS token with the [device explorer][lnk-device-explorer] tool, the CLI extension command [az iot hub generate-sas-token](https://docs.microsoft.com/cli/azure/ext/azure-cli-iot-ext/iot/hub?view=azure-cli-latest#ext-azure-cli-iot-ext-az-iot-hub-generate-sas-token), or the [Azure IoT Toolkit extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-toolkit)):</span></span>

`SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501`

> [!NOTE]
> <span data-ttu-id="2b581-162">The [Azure IoT SDKs][lnk-sdks] automatically generate tokens when connecting to the service.</span><span class="sxs-lookup"><span data-stu-id="2b581-162">The [Azure IoT SDKs][lnk-sdks] automatically generate tokens when connecting to the service.</span></span> <span data-ttu-id="2b581-163">In some cases, the Azure IoT SDKs do not support all the protocols or all the authentication methods.</span><span class="sxs-lookup"><span data-stu-id="2b581-163">In some cases, the Azure IoT SDKs do not support all the protocols or all the authentication methods.</span></span>

### <a name="special-considerations-for-sasl-plain"></a><span data-ttu-id="2b581-164">Special considerations for SASL PLAIN</span><span class="sxs-lookup"><span data-stu-id="2b581-164">Special considerations for SASL PLAIN</span></span>

<span data-ttu-id="2b581-165">When using SASL PLAIN with AMQP, a client connecting to an IoT hub can use a single token for each TCP connection.</span><span class="sxs-lookup"><span data-stu-id="2b581-165">When using SASL PLAIN with AMQP, a client connecting to an IoT hub can use a single token for each TCP connection.</span></span> <span data-ttu-id="2b581-166">When the token expires, the TCP connection disconnects from the service and triggers a reconnection.</span><span class="sxs-lookup"><span data-stu-id="2b581-166">When the token expires, the TCP connection disconnects from the service and triggers a reconnection.</span></span> <span data-ttu-id="2b581-167">This behavior, while not problematic for a back-end app, is damaging for a device app for the following reasons:</span><span class="sxs-lookup"><span data-stu-id="2b581-167">This behavior, while not problematic for a back-end app, is damaging for a device app for the following reasons:</span></span>

* <span data-ttu-id="2b581-168">Gateways usually connect on behalf of many devices.</span><span class="sxs-lookup"><span data-stu-id="2b581-168">Gateways usually connect on behalf of many devices.</span></span> <span data-ttu-id="2b581-169">When using SASL PLAIN, they have to create a distinct TCP connection for each device connecting to an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="2b581-169">When using SASL PLAIN, they have to create a distinct TCP connection for each device connecting to an IoT hub.</span></span> <span data-ttu-id="2b581-170">This scenario considerably increases the consumption of power and networking resources, and increases the latency of each device connection.</span><span class="sxs-lookup"><span data-stu-id="2b581-170">This scenario considerably increases the consumption of power and networking resources, and increases the latency of each device connection.</span></span>
* <span data-ttu-id="2b581-171">Resource-constrained devices are adversely affected by the increased use of resources to reconnect after each token expiration.</span><span class="sxs-lookup"><span data-stu-id="2b581-171">Resource-constrained devices are adversely affected by the increased use of resources to reconnect after each token expiration.</span></span>

## <a name="scope-iot-hub-level-credentials"></a><span data-ttu-id="2b581-172">Scope IoT hub-level credentials</span><span class="sxs-lookup"><span data-stu-id="2b581-172">Scope IoT hub-level credentials</span></span>

<span data-ttu-id="2b581-173">You can scope IoT hub-level security policies by creating tokens with a restricted resource URI.</span><span class="sxs-lookup"><span data-stu-id="2b581-173">You can scope IoT hub-level security policies by creating tokens with a restricted resource URI.</span></span> <span data-ttu-id="2b581-174">For example, the endpoint to send device-to-cloud messages from a device is **/devices/{deviceId}/messages/events**.</span><span class="sxs-lookup"><span data-stu-id="2b581-174">For example, the endpoint to send device-to-cloud messages from a device is **/devices/{deviceId}/messages/events**.</span></span> <span data-ttu-id="2b581-175">You can also use an IoT hub-level shared access policy with **DeviceConnect** permissions to sign a token whose resourceURI is **/devices/{deviceId}**.</span><span class="sxs-lookup"><span data-stu-id="2b581-175">You can also use an IoT hub-level shared access policy with **DeviceConnect** permissions to sign a token whose resourceURI is **/devices/{deviceId}**.</span></span> <span data-ttu-id="2b581-176">This approach creates a token that is only usable to send messages on behalf of device **deviceId**.</span><span class="sxs-lookup"><span data-stu-id="2b581-176">This approach creates a token that is only usable to send messages on behalf of device **deviceId**.</span></span>

<span data-ttu-id="2b581-177">This mechanism is similar to the [Event Hubs publisher policy][lnk-event-hubs-publisher-policy], and enables you to implement custom authentication methods.</span><span class="sxs-lookup"><span data-stu-id="2b581-177">This mechanism is similar to the [Event Hubs publisher policy][lnk-event-hubs-publisher-policy], and enables you to implement custom authentication methods.</span></span>

## <a name="security-tokens"></a><span data-ttu-id="2b581-178">Security tokens</span><span class="sxs-lookup"><span data-stu-id="2b581-178">Security tokens</span></span>

<span data-ttu-id="2b581-179">IoT Hub uses security tokens to authenticate devices and services to avoid sending keys on the wire.</span><span class="sxs-lookup"><span data-stu-id="2b581-179">IoT Hub uses security tokens to authenticate devices and services to avoid sending keys on the wire.</span></span> <span data-ttu-id="2b581-180">Additionally, security tokens are limited in time validity and scope.</span><span class="sxs-lookup"><span data-stu-id="2b581-180">Additionally, security tokens are limited in time validity and scope.</span></span> <span data-ttu-id="2b581-181">[Azure IoT SDKs][lnk-sdks] automatically generate tokens without requiring any special configuration.</span><span class="sxs-lookup"><span data-stu-id="2b581-181">[Azure IoT SDKs][lnk-sdks] automatically generate tokens without requiring any special configuration.</span></span> <span data-ttu-id="2b581-182">Some scenarios do require you to generate and use security tokens directly.</span><span class="sxs-lookup"><span data-stu-id="2b581-182">Some scenarios do require you to generate and use security tokens directly.</span></span> <span data-ttu-id="2b581-183">Such scenarios include:</span><span class="sxs-lookup"><span data-stu-id="2b581-183">Such scenarios include:</span></span>

* <span data-ttu-id="2b581-184">The direct use of the MQTT, AMQP, or HTTPS surfaces.</span><span class="sxs-lookup"><span data-stu-id="2b581-184">The direct use of the MQTT, AMQP, or HTTPS surfaces.</span></span>
* <span data-ttu-id="2b581-185">The implementation of the token service pattern, as explained in [Custom device authentication][lnk-custom-auth].</span><span class="sxs-lookup"><span data-stu-id="2b581-185">The implementation of the token service pattern, as explained in [Custom device authentication][lnk-custom-auth].</span></span>

<span data-ttu-id="2b581-186">IoT Hub also allows devices to authenticate with IoT Hub using [X.509 certificates][lnk-x509].</span><span class="sxs-lookup"><span data-stu-id="2b581-186">IoT Hub also allows devices to authenticate with IoT Hub using [X.509 certificates][lnk-x509].</span></span>

### <a name="security-token-structure"></a><span data-ttu-id="2b581-187">Security token structure</span><span class="sxs-lookup"><span data-stu-id="2b581-187">Security token structure</span></span>

<span data-ttu-id="2b581-188">You use security tokens to grant time-bounded access to devices and services to specific functionality in IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2b581-188">You use security tokens to grant time-bounded access to devices and services to specific functionality in IoT Hub.</span></span> <span data-ttu-id="2b581-189">To get authorization to connect to IoT Hub, devices and services must send security tokens signed with either a shared access or symmetric key.</span><span class="sxs-lookup"><span data-stu-id="2b581-189">To get authorization to connect to IoT Hub, devices and services must send security tokens signed with either a shared access or symmetric key.</span></span> <span data-ttu-id="2b581-190">These keys are stored with a device identity in the identity registry.</span><span class="sxs-lookup"><span data-stu-id="2b581-190">These keys are stored with a device identity in the identity registry.</span></span>

<span data-ttu-id="2b581-191">A token signed with a shared access key grants access to all the functionality associated with the shared access policy permissions.</span><span class="sxs-lookup"><span data-stu-id="2b581-191">A token signed with a shared access key grants access to all the functionality associated with the shared access policy permissions.</span></span> <span data-ttu-id="2b581-192">A token signed with a device identity's symmetric key only grants the **DeviceConnect** permission for the associated device identity.</span><span class="sxs-lookup"><span data-stu-id="2b581-192">A token signed with a device identity's symmetric key only grants the **DeviceConnect** permission for the associated device identity.</span></span>

<span data-ttu-id="2b581-193">The security token has the following format:</span><span class="sxs-lookup"><span data-stu-id="2b581-193">The security token has the following format:</span></span>

`SharedAccessSignature sig={signature-string}&se={expiry}&skn={policyName}&sr={URL-encoded-resourceURI}`

<span data-ttu-id="2b581-194">Here are the expected values:</span><span class="sxs-lookup"><span data-stu-id="2b581-194">Here are the expected values:</span></span>

| <span data-ttu-id="2b581-195">Value</span><span class="sxs-lookup"><span data-stu-id="2b581-195">Value</span></span> | <span data-ttu-id="2b581-196">Description</span><span class="sxs-lookup"><span data-stu-id="2b581-196">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2b581-197">{signature}</span><span class="sxs-lookup"><span data-stu-id="2b581-197">{signature}</span></span> |<span data-ttu-id="2b581-198">An HMAC-SHA256 signature string of the form: `{URL-encoded-resourceURI} + "\n" + expiry`.</span><span class="sxs-lookup"><span data-stu-id="2b581-198">An HMAC-SHA256 signature string of the form: `{URL-encoded-resourceURI} + "\n" + expiry`.</span></span> <span data-ttu-id="2b581-199">**Important**: The key is decoded from base64 and used as key to perform the HMAC-SHA256 computation.</span><span class="sxs-lookup"><span data-stu-id="2b581-199">**Important**: The key is decoded from base64 and used as key to perform the HMAC-SHA256 computation.</span></span> |
| <span data-ttu-id="2b581-200">{resourceURI}</span><span class="sxs-lookup"><span data-stu-id="2b581-200">{resourceURI}</span></span> |<span data-ttu-id="2b581-201">URI prefix (by segment) of the endpoints that can be accessed with this token, starting with host name of the IoT hub (no protocol).</span><span class="sxs-lookup"><span data-stu-id="2b581-201">URI prefix (by segment) of the endpoints that can be accessed with this token, starting with host name of the IoT hub (no protocol).</span></span> <span data-ttu-id="2b581-202">For example, `myHub.azure-devices.net/devices/device1`</span><span class="sxs-lookup"><span data-stu-id="2b581-202">For example, `myHub.azure-devices.net/devices/device1`</span></span> |
| <span data-ttu-id="2b581-203">{expiry}</span><span class="sxs-lookup"><span data-stu-id="2b581-203">{expiry}</span></span> |<span data-ttu-id="2b581-204">UTF8 strings for number of seconds since the epoch 00:00:00 UTC on 1 January 1970.</span><span class="sxs-lookup"><span data-stu-id="2b581-204">UTF8 strings for number of seconds since the epoch 00:00:00 UTC on 1 January 1970.</span></span> |
| <span data-ttu-id="2b581-205">{URL-encoded-resourceURI}</span><span class="sxs-lookup"><span data-stu-id="2b581-205">{URL-encoded-resourceURI}</span></span> |<span data-ttu-id="2b581-206">Lower case URL-encoding of the lower case resource URI</span><span class="sxs-lookup"><span data-stu-id="2b581-206">Lower case URL-encoding of the lower case resource URI</span></span> |
| <span data-ttu-id="2b581-207">{policyName}</span><span class="sxs-lookup"><span data-stu-id="2b581-207">{policyName}</span></span> |<span data-ttu-id="2b581-208">The name of the shared access policy to which this token refers.</span><span class="sxs-lookup"><span data-stu-id="2b581-208">The name of the shared access policy to which this token refers.</span></span> <span data-ttu-id="2b581-209">Absent if the token refers to device-registry credentials.</span><span class="sxs-lookup"><span data-stu-id="2b581-209">Absent if the token refers to device-registry credentials.</span></span> |

<span data-ttu-id="2b581-210">**Note on prefix**: The URI prefix is computed by segment and not by character.</span><span class="sxs-lookup"><span data-stu-id="2b581-210">**Note on prefix**: The URI prefix is computed by segment and not by character.</span></span> <span data-ttu-id="2b581-211">For example `/a/b` is a prefix for `/a/b/c` but not for `/a/bc`.</span><span class="sxs-lookup"><span data-stu-id="2b581-211">For example `/a/b` is a prefix for `/a/b/c` but not for `/a/bc`.</span></span>

<span data-ttu-id="2b581-212">The following Node.js snippet shows a function called **generateSasToken** that computes the token from the inputs `resourceUri, signingKey, policyName, expiresInMins`.</span><span class="sxs-lookup"><span data-stu-id="2b581-212">The following Node.js snippet shows a function called **generateSasToken** that computes the token from the inputs `resourceUri, signingKey, policyName, expiresInMins`.</span></span> <span data-ttu-id="2b581-213">The next sections detail how to initialize the different inputs for the different token use cases.</span><span class="sxs-lookup"><span data-stu-id="2b581-213">The next sections detail how to initialize the different inputs for the different token use cases.</span></span>

```nodejs
var generateSasToken = function(resourceUri, signingKey, policyName, expiresInMins) {
    resourceUri = encodeURIComponent(resourceUri);

    // Set expiration in seconds
    var expires = (Date.now() / 1000) + expiresInMins * 60;
    expires = Math.ceil(expires);
    var toSign = resourceUri + '\n' + expires;

    // Use crypto
    var hmac = crypto.createHmac('sha256', new Buffer(signingKey, 'base64'));
    hmac.update(toSign);
    var base64UriEncoded = encodeURIComponent(hmac.digest('base64'));

    // Construct autorization string
    var token = "SharedAccessSignature sr=" + resourceUri + "&sig="
    + base64UriEncoded + "&se=" + expires;
    if (policyName) token += "&skn="+policyName;
    return token;
};
```

<span data-ttu-id="2b581-214">As a comparison, the equivalent Python code to generate a security token is:</span><span class="sxs-lookup"><span data-stu-id="2b581-214">As a comparison, the equivalent Python code to generate a security token is:</span></span>

```python
from base64 import b64encode, b64decode
from hashlib import sha256
from time import time
from urllib import quote_plus, urlencode
from hmac import HMAC

def generate_sas_token(uri, key, policy_name, expiry=3600):
    ttl = time() + expiry
    sign_key = "%s\n%d" % ((quote_plus(uri)), int(ttl))
    print sign_key
    signature = b64encode(HMAC(b64decode(key), sign_key, sha256).digest())

    rawtoken = {
        'sr' :  uri,
        'sig': signature,
        'se' : str(int(ttl))
    }

    if policy_name is not None:
        rawtoken['skn'] = policy_name

    return 'SharedAccessSignature ' + urlencode(rawtoken)
```

<span data-ttu-id="2b581-215">The functionality in C# to generate a security token is:</span><span class="sxs-lookup"><span data-stu-id="2b581-215">The functionality in C# to generate a security token is:</span></span>

```csharp
using System;
using System.Globalization;
using System.Net;
using System.Net.Http;
using System.Security.Cryptography;
using System.Text;

public static string generateSasToken(string resourceUri, string key, string policyName, int expiryInSeconds = 3600)
{
    TimeSpan fromEpochStart = DateTime.UtcNow - new DateTime(1970, 1, 1);
    string expiry = Convert.ToString((int)fromEpochStart.TotalSeconds + expiryInSeconds);

    string stringToSign = WebUtility.UrlEncode(resourceUri) + "\n" + expiry;

    HMACSHA256 hmac = new HMACSHA256(Convert.FromBase64String(key));
    string signature = Convert.ToBase64String(hmac.ComputeHash(Encoding.UTF8.GetBytes(stringToSign)));

    string token = String.Format(CultureInfo.InvariantCulture, "SharedAccessSignature sr={0}&sig={1}&se={2}", WebUtility.UrlEncode(resourceUri), WebUtility.UrlEncode(signature), expiry);

    if (!String.IsNullOrEmpty(policyName))
    {
        token += "&skn=" + policyName;
    }

    return token;
}

```


> [!NOTE]
> <span data-ttu-id="2b581-216">Since the time validity of the token is validated on IoT Hub machines, the drift on the clock of the machine that generates the token must be minimal.</span><span class="sxs-lookup"><span data-stu-id="2b581-216">Since the time validity of the token is validated on IoT Hub machines, the drift on the clock of the machine that generates the token must be minimal.</span></span>

### <a name="use-sas-tokens-in-a-device-app"></a><span data-ttu-id="2b581-217">Use SAS tokens in a device app</span><span class="sxs-lookup"><span data-stu-id="2b581-217">Use SAS tokens in a device app</span></span>

<span data-ttu-id="2b581-218">There are two ways to obtain **DeviceConnect** permissions with IoT Hub with security tokens: use a [symmetric device key from the identity registry](#use-a-symmetric-key-in-the-identity-registry), or use a [shared access key](#use-a-shared-access-policy).</span><span class="sxs-lookup"><span data-stu-id="2b581-218">There are two ways to obtain **DeviceConnect** permissions with IoT Hub with security tokens: use a [symmetric device key from the identity registry](#use-a-symmetric-key-in-the-identity-registry), or use a [shared access key](#use-a-shared-access-policy).</span></span>

<span data-ttu-id="2b581-219">Remember that all functionality accessible from devices is exposed by design on endpoints with prefix `/devices/{deviceId}`.</span><span class="sxs-lookup"><span data-stu-id="2b581-219">Remember that all functionality accessible from devices is exposed by design on endpoints with prefix `/devices/{deviceId}`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2b581-220">The only way that IoT Hub authenticates a specific device is using the device identity symmetric key.</span><span class="sxs-lookup"><span data-stu-id="2b581-220">The only way that IoT Hub authenticates a specific device is using the device identity symmetric key.</span></span> <span data-ttu-id="2b581-221">In cases when a shared access policy is used to access device functionality, the solution must consider the component issuing the security token as a trusted subcomponent.</span><span class="sxs-lookup"><span data-stu-id="2b581-221">In cases when a shared access policy is used to access device functionality, the solution must consider the component issuing the security token as a trusted subcomponent.</span></span>

<span data-ttu-id="2b581-222">The device-facing endpoints are (irrespective of the protocol):</span><span class="sxs-lookup"><span data-stu-id="2b581-222">The device-facing endpoints are (irrespective of the protocol):</span></span>

| <span data-ttu-id="2b581-223">Endpoint</span><span class="sxs-lookup"><span data-stu-id="2b581-223">Endpoint</span></span> | <span data-ttu-id="2b581-224">Functionality</span><span class="sxs-lookup"><span data-stu-id="2b581-224">Functionality</span></span> |
| --- | --- |
| `{iot hub host name}/devices/{deviceId}/messages/events` |<span data-ttu-id="2b581-225">Send device-to-cloud messages.</span><span class="sxs-lookup"><span data-stu-id="2b581-225">Send device-to-cloud messages.</span></span> |
| `{iot hub host name}/devices/{deviceId}/messages/devicebound` |<span data-ttu-id="2b581-226">Receive cloud-to-device messages.</span><span class="sxs-lookup"><span data-stu-id="2b581-226">Receive cloud-to-device messages.</span></span> |

### <a name="use-a-symmetric-key-in-the-identity-registry"></a><span data-ttu-id="2b581-227">Use a symmetric key in the identity registry</span><span class="sxs-lookup"><span data-stu-id="2b581-227">Use a symmetric key in the identity registry</span></span>

<span data-ttu-id="2b581-228">When using a device identity's symmetric key to generate a token, the policyName (`skn`) element of the token is omitted.</span><span class="sxs-lookup"><span data-stu-id="2b581-228">When using a device identity's symmetric key to generate a token, the policyName (`skn`) element of the token is omitted.</span></span>

<span data-ttu-id="2b581-229">For example, a token created to access all device functionality should have the following parameters:</span><span class="sxs-lookup"><span data-stu-id="2b581-229">For example, a token created to access all device functionality should have the following parameters:</span></span>

* <span data-ttu-id="2b581-230">resource URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span><span class="sxs-lookup"><span data-stu-id="2b581-230">resource URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span></span>
* <span data-ttu-id="2b581-231">signing key: any symmetric key for the `{device id}` identity,</span><span class="sxs-lookup"><span data-stu-id="2b581-231">signing key: any symmetric key for the `{device id}` identity,</span></span>
* <span data-ttu-id="2b581-232">no policy name,</span><span class="sxs-lookup"><span data-stu-id="2b581-232">no policy name,</span></span>
* <span data-ttu-id="2b581-233">any expiration time.</span><span class="sxs-lookup"><span data-stu-id="2b581-233">any expiration time.</span></span>

<span data-ttu-id="2b581-234">An example using the preceding Node.js function would be:</span><span class="sxs-lookup"><span data-stu-id="2b581-234">An example using the preceding Node.js function would be:</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var deviceKey ="...";

var token = generateSasToken(endpoint, deviceKey, null, 60);
```

<span data-ttu-id="2b581-235">The result, which grants access to all functionality for device1, would be:</span><span class="sxs-lookup"><span data-stu-id="2b581-235">The result, which grants access to all functionality for device1, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697`

> [!NOTE]
> <span data-ttu-id="2b581-236">It's possible to generate a SAS token with the [device explorer][lnk-device-explorer] tool, the CLI extension command [az iot hub generate-sas-token](https://docs.microsoft.com/cli/azure/ext/azure-cli-iot-ext/iot/hub?view=azure-cli-latest#ext-azure-cli-iot-ext-az-iot-hub-generate-sas-token), or the [Azure IoT Toolkit extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-toolkit).</span><span class="sxs-lookup"><span data-stu-id="2b581-236">It's possible to generate a SAS token with the [device explorer][lnk-device-explorer] tool, the CLI extension command [az iot hub generate-sas-token](https://docs.microsoft.com/cli/azure/ext/azure-cli-iot-ext/iot/hub?view=azure-cli-latest#ext-azure-cli-iot-ext-az-iot-hub-generate-sas-token), or the [Azure IoT Toolkit extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-toolkit).</span></span>

### <a name="use-a-shared-access-policy"></a><span data-ttu-id="2b581-237">Use a shared access policy</span><span class="sxs-lookup"><span data-stu-id="2b581-237">Use a shared access policy</span></span>

<span data-ttu-id="2b581-238">When you create a token from a shared access policy, set the `skn` field to the name of the policy.</span><span class="sxs-lookup"><span data-stu-id="2b581-238">When you create a token from a shared access policy, set the `skn` field to the name of the policy.</span></span> <span data-ttu-id="2b581-239">This policy must grant the **DeviceConnect** permission.</span><span class="sxs-lookup"><span data-stu-id="2b581-239">This policy must grant the **DeviceConnect** permission.</span></span>

<span data-ttu-id="2b581-240">The two main scenarios for using shared access policies to access device functionality are:</span><span class="sxs-lookup"><span data-stu-id="2b581-240">The two main scenarios for using shared access policies to access device functionality are:</span></span>

* <span data-ttu-id="2b581-241">[cloud protocol gateways][lnk-endpoints],</span><span class="sxs-lookup"><span data-stu-id="2b581-241">[cloud protocol gateways][lnk-endpoints],</span></span>
* <span data-ttu-id="2b581-242">[token services][lnk-custom-auth] used to implement custom authentication schemes.</span><span class="sxs-lookup"><span data-stu-id="2b581-242">[token services][lnk-custom-auth] used to implement custom authentication schemes.</span></span>

<span data-ttu-id="2b581-243">Since the shared access policy can potentially grant access to connect as any device, it is important to use the correct resource URI when creating security tokens.</span><span class="sxs-lookup"><span data-stu-id="2b581-243">Since the shared access policy can potentially grant access to connect as any device, it is important to use the correct resource URI when creating security tokens.</span></span> <span data-ttu-id="2b581-244">This setting is especially important for token services, which have to scope the token to a specific device using the resource URI.</span><span class="sxs-lookup"><span data-stu-id="2b581-244">This setting is especially important for token services, which have to scope the token to a specific device using the resource URI.</span></span> <span data-ttu-id="2b581-245">This point is less relevant for protocol gateways as they are already mediating traffic for all devices.</span><span class="sxs-lookup"><span data-stu-id="2b581-245">This point is less relevant for protocol gateways as they are already mediating traffic for all devices.</span></span>

<span data-ttu-id="2b581-246">As an example, a token service using the pre-created shared access policy called **device** would create a token with the following parameters:</span><span class="sxs-lookup"><span data-stu-id="2b581-246">As an example, a token service using the pre-created shared access policy called **device** would create a token with the following parameters:</span></span>

* <span data-ttu-id="2b581-247">resource URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span><span class="sxs-lookup"><span data-stu-id="2b581-247">resource URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span></span>
* <span data-ttu-id="2b581-248">signing key: one of the keys of the `device` policy,</span><span class="sxs-lookup"><span data-stu-id="2b581-248">signing key: one of the keys of the `device` policy,</span></span>
* <span data-ttu-id="2b581-249">policy name: `device`,</span><span class="sxs-lookup"><span data-stu-id="2b581-249">policy name: `device`,</span></span>
* <span data-ttu-id="2b581-250">any expiration time.</span><span class="sxs-lookup"><span data-stu-id="2b581-250">any expiration time.</span></span>

<span data-ttu-id="2b581-251">An example using the preceding Node.js function would be:</span><span class="sxs-lookup"><span data-stu-id="2b581-251">An example using the preceding Node.js function would be:</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

<span data-ttu-id="2b581-252">The result, which grants access to all functionality for device1, would be:</span><span class="sxs-lookup"><span data-stu-id="2b581-252">The result, which grants access to all functionality for device1, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697&skn=device`

<span data-ttu-id="2b581-253">A protocol gateway could use the same token for all devices simply setting the resource URI to `myhub.azure-devices.net/devices`.</span><span class="sxs-lookup"><span data-stu-id="2b581-253">A protocol gateway could use the same token for all devices simply setting the resource URI to `myhub.azure-devices.net/devices`.</span></span>

### <a name="use-security-tokens-from-service-components"></a><span data-ttu-id="2b581-254">Use security tokens from service components</span><span class="sxs-lookup"><span data-stu-id="2b581-254">Use security tokens from service components</span></span>

<span data-ttu-id="2b581-255">Service components can only generate security tokens using shared access policies granting the appropriate permissions as explained previously.</span><span class="sxs-lookup"><span data-stu-id="2b581-255">Service components can only generate security tokens using shared access policies granting the appropriate permissions as explained previously.</span></span>

<span data-ttu-id="2b581-256">Here are the service functions exposed on the endpoints:</span><span class="sxs-lookup"><span data-stu-id="2b581-256">Here are the service functions exposed on the endpoints:</span></span>

| <span data-ttu-id="2b581-257">Endpoint</span><span class="sxs-lookup"><span data-stu-id="2b581-257">Endpoint</span></span> | <span data-ttu-id="2b581-258">Functionality</span><span class="sxs-lookup"><span data-stu-id="2b581-258">Functionality</span></span> |
| --- | --- |
| `{iot hub host name}/devices` |<span data-ttu-id="2b581-259">Create, update, retrieve, and delete device identities.</span><span class="sxs-lookup"><span data-stu-id="2b581-259">Create, update, retrieve, and delete device identities.</span></span> |
| `{iot hub host name}/messages/events` |<span data-ttu-id="2b581-260">Receive device-to-cloud messages.</span><span class="sxs-lookup"><span data-stu-id="2b581-260">Receive device-to-cloud messages.</span></span> |
| `{iot hub host name}/servicebound/feedback` |<span data-ttu-id="2b581-261">Receive feedback for cloud-to-device messages.</span><span class="sxs-lookup"><span data-stu-id="2b581-261">Receive feedback for cloud-to-device messages.</span></span> |
| `{iot hub host name}/devicebound` |<span data-ttu-id="2b581-262">Send cloud-to-device messages.</span><span class="sxs-lookup"><span data-stu-id="2b581-262">Send cloud-to-device messages.</span></span> |

<span data-ttu-id="2b581-263">As an example, a service generating using the pre-created shared access policy called **registryRead** would create a token with the following parameters:</span><span class="sxs-lookup"><span data-stu-id="2b581-263">As an example, a service generating using the pre-created shared access policy called **registryRead** would create a token with the following parameters:</span></span>

* <span data-ttu-id="2b581-264">resource URI: `{IoT hub name}.azure-devices.net/devices`,</span><span class="sxs-lookup"><span data-stu-id="2b581-264">resource URI: `{IoT hub name}.azure-devices.net/devices`,</span></span>
* <span data-ttu-id="2b581-265">signing key: one of the keys of the `registryRead` policy,</span><span class="sxs-lookup"><span data-stu-id="2b581-265">signing key: one of the keys of the `registryRead` policy,</span></span>
* <span data-ttu-id="2b581-266">policy name: `registryRead`,</span><span class="sxs-lookup"><span data-stu-id="2b581-266">policy name: `registryRead`,</span></span>
* <span data-ttu-id="2b581-267">any expiration time.</span><span class="sxs-lookup"><span data-stu-id="2b581-267">any expiration time.</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

<span data-ttu-id="2b581-268">The result, which would grant access to read all device identities, would be:</span><span class="sxs-lookup"><span data-stu-id="2b581-268">The result, which would grant access to read all device identities, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices&sig=JdyscqTpXdEJs49elIUCcohw2DlFDR3zfH5KqGJo4r4%3D&se=1456973447&skn=registryRead`

## <a name="supported-x509-certificates"></a><span data-ttu-id="2b581-269">Supported X.509 certificates</span><span class="sxs-lookup"><span data-stu-id="2b581-269">Supported X.509 certificates</span></span>

<span data-ttu-id="2b581-270">You can use any X.509 certificate to authenticate a device with IoT Hub by uploading either a certificate thumbprint or a certificate authority (CA) to Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2b581-270">You can use any X.509 certificate to authenticate a device with IoT Hub by uploading either a certificate thumbprint or a certificate authority (CA) to Azure IoT Hub.</span></span> <span data-ttu-id="2b581-271">Authentication using certificate thumbprints only verifies that the presented thumbprint matches the configured thumbprint.</span><span class="sxs-lookup"><span data-stu-id="2b581-271">Authentication using certificate thumbprints only verifies that the presented thumbprint matches the configured thumbprint.</span></span> <span data-ttu-id="2b581-272">Authentication using certificate authority validates the certificate chain.</span><span class="sxs-lookup"><span data-stu-id="2b581-272">Authentication using certificate authority validates the certificate chain.</span></span> 

<span data-ttu-id="2b581-273">Supported certificates include:</span><span class="sxs-lookup"><span data-stu-id="2b581-273">Supported certificates include:</span></span>

* <span data-ttu-id="2b581-274">**An existing X.509 certificate**.</span><span class="sxs-lookup"><span data-stu-id="2b581-274">**An existing X.509 certificate**.</span></span> <span data-ttu-id="2b581-275">A device may already have an X.509 certificate associated with it.</span><span class="sxs-lookup"><span data-stu-id="2b581-275">A device may already have an X.509 certificate associated with it.</span></span> <span data-ttu-id="2b581-276">The device can use this certificate to authenticate with IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2b581-276">The device can use this certificate to authenticate with IoT Hub.</span></span> <span data-ttu-id="2b581-277">Works with either thumbprint or CA authentication.</span><span class="sxs-lookup"><span data-stu-id="2b581-277">Works with either thumbprint or CA authentication.</span></span> 
* <span data-ttu-id="2b581-278">**CA-signed X.509 certificate**.</span><span class="sxs-lookup"><span data-stu-id="2b581-278">**CA-signed X.509 certificate**.</span></span> <span data-ttu-id="2b581-279">To identify a device and authenticate it with IoT Hub, you can use an X.509 certificate generated and signed by a Certification Authority (CA).</span><span class="sxs-lookup"><span data-stu-id="2b581-279">To identify a device and authenticate it with IoT Hub, you can use an X.509 certificate generated and signed by a Certification Authority (CA).</span></span> <span data-ttu-id="2b581-280">Works with either thumbprint or CA authentication.</span><span class="sxs-lookup"><span data-stu-id="2b581-280">Works with either thumbprint or CA authentication.</span></span>
* <span data-ttu-id="2b581-281">**A self-generated and self-signed X-509 certificate**.</span><span class="sxs-lookup"><span data-stu-id="2b581-281">**A self-generated and self-signed X-509 certificate**.</span></span> <span data-ttu-id="2b581-282">A device manufacturer or in-house deployer can generate these certificates and store the corresponding private key (and certificate) on the device.</span><span class="sxs-lookup"><span data-stu-id="2b581-282">A device manufacturer or in-house deployer can generate these certificates and store the corresponding private key (and certificate) on the device.</span></span> <span data-ttu-id="2b581-283">You can use tools such as [OpenSSL][lnk-openssl] and [Windows SelfSignedCertificate][lnk-selfsigned] utility for this purpose.</span><span class="sxs-lookup"><span data-stu-id="2b581-283">You can use tools such as [OpenSSL][lnk-openssl] and [Windows SelfSignedCertificate][lnk-selfsigned] utility for this purpose.</span></span> <span data-ttu-id="2b581-284">Only works with thumbprint authentication.</span><span class="sxs-lookup"><span data-stu-id="2b581-284">Only works with thumbprint authentication.</span></span> 

<span data-ttu-id="2b581-285">A device may either use an X.509 certificate or a security token for authentication, but not both.</span><span class="sxs-lookup"><span data-stu-id="2b581-285">A device may either use an X.509 certificate or a security token for authentication, but not both.</span></span>

<span data-ttu-id="2b581-286">For more information about authentication using certificate authority, see [Device Authentication using X.509 CA Certificates](iot-hub-x509ca-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2b581-286">For more information about authentication using certificate authority, see [Device Authentication using X.509 CA Certificates](iot-hub-x509ca-overview.md).</span></span>

### <a name="register-an-x509-certificate-for-a-device"></a><span data-ttu-id="2b581-287">Register an X.509 certificate for a device</span><span class="sxs-lookup"><span data-stu-id="2b581-287">Register an X.509 certificate for a device</span></span>

<span data-ttu-id="2b581-288">The [Azure IoT Service SDK for C#][lnk-service-sdk] (version 1.0.8+) supports registering a device that uses an X.509 certificate for authentication.</span><span class="sxs-lookup"><span data-stu-id="2b581-288">The [Azure IoT Service SDK for C#][lnk-service-sdk] (version 1.0.8+) supports registering a device that uses an X.509 certificate for authentication.</span></span> <span data-ttu-id="2b581-289">Other APIs such as import/export of devices also support X.509 certificates.</span><span class="sxs-lookup"><span data-stu-id="2b581-289">Other APIs such as import/export of devices also support X.509 certificates.</span></span>

<span data-ttu-id="2b581-290">You can also use the CLI extension command [az iot hub device-identity](https://docs.microsoft.com/cli/azure/ext/azure-cli-iot-ext/iot/hub/device-identity?view=azure-cli-latest) to configure X.509 certificates for devices.</span><span class="sxs-lookup"><span data-stu-id="2b581-290">You can also use the CLI extension command [az iot hub device-identity](https://docs.microsoft.com/cli/azure/ext/azure-cli-iot-ext/iot/hub/device-identity?view=azure-cli-latest) to configure X.509 certificates for devices.</span></span>

### <a name="c-support"></a><span data-ttu-id="2b581-291">C\# Support</span><span class="sxs-lookup"><span data-stu-id="2b581-291">C\# Support</span></span>

<span data-ttu-id="2b581-292">The **RegistryManager** class provides a programmatic way to register a device.</span><span class="sxs-lookup"><span data-stu-id="2b581-292">The **RegistryManager** class provides a programmatic way to register a device.</span></span> <span data-ttu-id="2b581-293">In particular, the **AddDeviceAsync** and **UpdateDeviceAsync** methods enable you to register and update a device in the IoT Hub identity registry.</span><span class="sxs-lookup"><span data-stu-id="2b581-293">In particular, the **AddDeviceAsync** and **UpdateDeviceAsync** methods enable you to register and update a device in the IoT Hub identity registry.</span></span> <span data-ttu-id="2b581-294">These two methods take a **Device** instance as input.</span><span class="sxs-lookup"><span data-stu-id="2b581-294">These two methods take a **Device** instance as input.</span></span> <span data-ttu-id="2b581-295">The **Device** class includes an **Authentication** property that allows you to specify primary and secondary X.509 certificate thumbprints.</span><span class="sxs-lookup"><span data-stu-id="2b581-295">The **Device** class includes an **Authentication** property that allows you to specify primary and secondary X.509 certificate thumbprints.</span></span> <span data-ttu-id="2b581-296">The thumbprint represents a SHA256 hash of the X.509 certificate (stored using binary DER encoding).</span><span class="sxs-lookup"><span data-stu-id="2b581-296">The thumbprint represents a SHA256 hash of the X.509 certificate (stored using binary DER encoding).</span></span> <span data-ttu-id="2b581-297">You have the option of specifying a primary thumbprint or a secondary thumbprint or both.</span><span class="sxs-lookup"><span data-stu-id="2b581-297">You have the option of specifying a primary thumbprint or a secondary thumbprint or both.</span></span> <span data-ttu-id="2b581-298">Primary and secondary thumbprints are supported to handle certificate rollover scenarios.</span><span class="sxs-lookup"><span data-stu-id="2b581-298">Primary and secondary thumbprints are supported to handle certificate rollover scenarios.</span></span>

<span data-ttu-id="2b581-299">Here is a sample C\# code snippet to register a device using an X.509 certificate thumbprint:</span><span class="sxs-lookup"><span data-stu-id="2b581-299">Here is a sample C\# code snippet to register a device using an X.509 certificate thumbprint:</span></span>

```csharp
var device = new Device(deviceId)
{
  Authentication = new AuthenticationMechanism()
  {
    X509Thumbprint = new X509Thumbprint()
    {
      PrimaryThumbprint = "B4172AB44C28F3B9E117648C6F7294978A00CDCBA34A46A1B8588B3F7D82C4F1"
    }
  }
};
RegistryManager registryManager = RegistryManager.CreateFromConnectionString(deviceGatewayConnectionString);
await registryManager.AddDeviceAsync(device);
```

### <a name="use-an-x509-certificate-during-run-time-operations"></a><span data-ttu-id="2b581-300">Use an X.509 certificate during run-time operations</span><span class="sxs-lookup"><span data-stu-id="2b581-300">Use an X.509 certificate during run-time operations</span></span>

<span data-ttu-id="2b581-301">The [Azure IoT device SDK for .NET][lnk-client-sdk] (version 1.0.11+) supports the use of X.509 certificates.</span><span class="sxs-lookup"><span data-stu-id="2b581-301">The [Azure IoT device SDK for .NET][lnk-client-sdk] (version 1.0.11+) supports the use of X.509 certificates.</span></span>

### <a name="c-support"></a><span data-ttu-id="2b581-302">C\# Support</span><span class="sxs-lookup"><span data-stu-id="2b581-302">C\# Support</span></span>

<span data-ttu-id="2b581-303">The class **DeviceAuthenticationWithX509Certificate** supports the creation of **DeviceClient** instances using an X.509 certificate.</span><span class="sxs-lookup"><span data-stu-id="2b581-303">The class **DeviceAuthenticationWithX509Certificate** supports the creation of **DeviceClient** instances using an X.509 certificate.</span></span> <span data-ttu-id="2b581-304">The X.509 certificate must be in the PFX (also called PKCS #12) format that includes the private key.</span><span class="sxs-lookup"><span data-stu-id="2b581-304">The X.509 certificate must be in the PFX (also called PKCS #12) format that includes the private key.</span></span>

<span data-ttu-id="2b581-305">Here is a sample code snippet:</span><span class="sxs-lookup"><span data-stu-id="2b581-305">Here is a sample code snippet:</span></span>

```csharp
var authMethod = new DeviceAuthenticationWithX509Certificate("<device id>", x509Certificate);

var deviceClient = DeviceClient.Create("<IotHub DNS HostName>", authMethod);
```

## <a name="custom-device-and-module-authentication"></a><span data-ttu-id="2b581-306">Custom device and module authentication</span><span class="sxs-lookup"><span data-stu-id="2b581-306">Custom device and module authentication</span></span>

<span data-ttu-id="2b581-307">You can use the IoT Hub [identity registry][lnk-identity-registry] to configure per-device/module security credentials and access control using [tokens][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="2b581-307">You can use the IoT Hub [identity registry][lnk-identity-registry] to configure per-device/module security credentials and access control using [tokens][lnk-sas-tokens].</span></span> <span data-ttu-id="2b581-308">If an IoT solution already has a custom identity registry and/or authentication scheme, consider creating a *token service* to integrate this infrastructure with IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2b581-308">If an IoT solution already has a custom identity registry and/or authentication scheme, consider creating a *token service* to integrate this infrastructure with IoT Hub.</span></span> <span data-ttu-id="2b581-309">In this way, you can use other IoT features in your solution.</span><span class="sxs-lookup"><span data-stu-id="2b581-309">In this way, you can use other IoT features in your solution.</span></span>

<span data-ttu-id="2b581-310">A token service is a custom cloud service.</span><span class="sxs-lookup"><span data-stu-id="2b581-310">A token service is a custom cloud service.</span></span> <span data-ttu-id="2b581-311">It uses an IoT Hub *shared access policy* with **DeviceConnect** or **ModuleConnect** permissions to create *device-scoped* or *module-scoped* tokens.</span><span class="sxs-lookup"><span data-stu-id="2b581-311">It uses an IoT Hub *shared access policy* with **DeviceConnect** or **ModuleConnect** permissions to create *device-scoped* or *module-scoped* tokens.</span></span> <span data-ttu-id="2b581-312">These tokens enable a device and module to connect to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="2b581-312">These tokens enable a device and module to connect to your IoT hub.</span></span>

![Steps of the token service pattern][img-tokenservice]

<span data-ttu-id="2b581-314">Here are the main steps of the token service pattern:</span><span class="sxs-lookup"><span data-stu-id="2b581-314">Here are the main steps of the token service pattern:</span></span>

1. <span data-ttu-id="2b581-315">Create an IoT Hub shared access policy with **DeviceConnect** or **ModuleConnect** permissions for your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="2b581-315">Create an IoT Hub shared access policy with **DeviceConnect** or **ModuleConnect** permissions for your IoT hub.</span></span> <span data-ttu-id="2b581-316">You can create this policy in the [Azure portal][lnk-management-portal] or programmatically.</span><span class="sxs-lookup"><span data-stu-id="2b581-316">You can create this policy in the [Azure portal][lnk-management-portal] or programmatically.</span></span> <span data-ttu-id="2b581-317">The token service uses this policy to sign the tokens it creates.</span><span class="sxs-lookup"><span data-stu-id="2b581-317">The token service uses this policy to sign the tokens it creates.</span></span>
1. <span data-ttu-id="2b581-318">When a device/module needs to access your IoT hub, it requests a signed token from your token service.</span><span class="sxs-lookup"><span data-stu-id="2b581-318">When a device/module needs to access your IoT hub, it requests a signed token from your token service.</span></span> <span data-ttu-id="2b581-319">The device can authenticate with your custom identity registry/authentication scheme to determine the device/module identity that the token service uses to create the token.</span><span class="sxs-lookup"><span data-stu-id="2b581-319">The device can authenticate with your custom identity registry/authentication scheme to determine the device/module identity that the token service uses to create the token.</span></span>
1. <span data-ttu-id="2b581-320">The token service returns a token.</span><span class="sxs-lookup"><span data-stu-id="2b581-320">The token service returns a token.</span></span> <span data-ttu-id="2b581-321">The token is created by using `/devices/{deviceId}` or `/devices/{deviceId}/module/{moduleId}` as `resourceURI`, with `deviceId` as the device being authenticated or `moduleId` as the module being authenticated.</span><span class="sxs-lookup"><span data-stu-id="2b581-321">The token is created by using `/devices/{deviceId}` or `/devices/{deviceId}/module/{moduleId}` as `resourceURI`, with `deviceId` as the device being authenticated or `moduleId` as the module being authenticated.</span></span> <span data-ttu-id="2b581-322">The token service uses the shared access policy to construct the token.</span><span class="sxs-lookup"><span data-stu-id="2b581-322">The token service uses the shared access policy to construct the token.</span></span>
1. <span data-ttu-id="2b581-323">The device/module uses the token directly with the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="2b581-323">The device/module uses the token directly with the IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="2b581-324">You can use the .NET class [SharedAccessSignatureBuilder][lnk-dotnet-sas] or the Java class [IotHubServiceSasToken][lnk-java-sas] to create a token in your token service.</span><span class="sxs-lookup"><span data-stu-id="2b581-324">You can use the .NET class [SharedAccessSignatureBuilder][lnk-dotnet-sas] or the Java class [IotHubServiceSasToken][lnk-java-sas] to create a token in your token service.</span></span>

<span data-ttu-id="2b581-325">The token service can set the token expiration as desired.</span><span class="sxs-lookup"><span data-stu-id="2b581-325">The token service can set the token expiration as desired.</span></span> <span data-ttu-id="2b581-326">When the token expires, the IoT hub severs the device/module connection.</span><span class="sxs-lookup"><span data-stu-id="2b581-326">When the token expires, the IoT hub severs the device/module connection.</span></span> <span data-ttu-id="2b581-327">Then, the device/module must request a new token from the token service.</span><span class="sxs-lookup"><span data-stu-id="2b581-327">Then, the device/module must request a new token from the token service.</span></span> <span data-ttu-id="2b581-328">A short expiry time increases the load on both the device/module and the token service.</span><span class="sxs-lookup"><span data-stu-id="2b581-328">A short expiry time increases the load on both the device/module and the token service.</span></span>

<span data-ttu-id="2b581-329">For a device/module to connect to your hub, you must still add it to the IoT Hub identity registry — even though it is using a token and not a key to connect.</span><span class="sxs-lookup"><span data-stu-id="2b581-329">For a device/module to connect to your hub, you must still add it to the IoT Hub identity registry — even though it is using a token and not a key to connect.</span></span> <span data-ttu-id="2b581-330">Therefore, you can continue to use per-device/per-module access control by enabling or disabling device/module identities in the [identity registry][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="2b581-330">Therefore, you can continue to use per-device/per-module access control by enabling or disabling device/module identities in the [identity registry][lnk-identity-registry].</span></span> <span data-ttu-id="2b581-331">This approach mitigates the risks of using tokens with long expiry times.</span><span class="sxs-lookup"><span data-stu-id="2b581-331">This approach mitigates the risks of using tokens with long expiry times.</span></span>

### <a name="comparison-with-a-custom-gateway"></a><span data-ttu-id="2b581-332">Comparison with a custom gateway</span><span class="sxs-lookup"><span data-stu-id="2b581-332">Comparison with a custom gateway</span></span>

<span data-ttu-id="2b581-333">The token service pattern is the recommended way to implement a custom identity registry/authentication scheme with IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2b581-333">The token service pattern is the recommended way to implement a custom identity registry/authentication scheme with IoT Hub.</span></span> <span data-ttu-id="2b581-334">This pattern is recommended because IoT Hub continues to handle most of the solution traffic.</span><span class="sxs-lookup"><span data-stu-id="2b581-334">This pattern is recommended because IoT Hub continues to handle most of the solution traffic.</span></span> <span data-ttu-id="2b581-335">However, if the custom authentication scheme is so intertwined with the protocol, you may require a *custom gateway* to process all the traffic.</span><span class="sxs-lookup"><span data-stu-id="2b581-335">However, if the custom authentication scheme is so intertwined with the protocol, you may require a *custom gateway* to process all the traffic.</span></span> <span data-ttu-id="2b581-336">An example of such a scenario is using[Transport Layer Security (TLS) and pre-shared keys (PSKs)][lnk-tls-psk].</span><span class="sxs-lookup"><span data-stu-id="2b581-336">An example of such a scenario is using[Transport Layer Security (TLS) and pre-shared keys (PSKs)][lnk-tls-psk].</span></span> <span data-ttu-id="2b581-337">For more information, see the [protocol gateway][lnk-protocols] article.</span><span class="sxs-lookup"><span data-stu-id="2b581-337">For more information, see the [protocol gateway][lnk-protocols] article.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="2b581-338">Reference topics:</span><span class="sxs-lookup"><span data-stu-id="2b581-338">Reference topics:</span></span>

<span data-ttu-id="2b581-339">The following reference topics provide you with more information about controlling access to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="2b581-339">The following reference topics provide you with more information about controlling access to your IoT hub.</span></span>

## <a name="iot-hub-permissions"></a><span data-ttu-id="2b581-340">IoT Hub permissions</span><span class="sxs-lookup"><span data-stu-id="2b581-340">IoT Hub permissions</span></span>

<span data-ttu-id="2b581-341">The following table lists the permissions you can use to control access to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="2b581-341">The following table lists the permissions you can use to control access to your IoT hub.</span></span>

| <span data-ttu-id="2b581-342">Permission</span><span class="sxs-lookup"><span data-stu-id="2b581-342">Permission</span></span> | <span data-ttu-id="2b581-343">Notes</span><span class="sxs-lookup"><span data-stu-id="2b581-343">Notes</span></span> |
| --- | --- |
| <span data-ttu-id="2b581-344">**RegistryRead**</span><span class="sxs-lookup"><span data-stu-id="2b581-344">**RegistryRead**</span></span> |<span data-ttu-id="2b581-345">Grants read access to the identity registry.</span><span class="sxs-lookup"><span data-stu-id="2b581-345">Grants read access to the identity registry.</span></span> <span data-ttu-id="2b581-346">For more information, see [Identity registry][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="2b581-346">For more information, see [Identity registry][lnk-identity-registry].</span></span> <br/><span data-ttu-id="2b581-347">This permission is used by back-end cloud services.</span><span class="sxs-lookup"><span data-stu-id="2b581-347">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="2b581-348">**RegistryReadWrite**</span><span class="sxs-lookup"><span data-stu-id="2b581-348">**RegistryReadWrite**</span></span> |<span data-ttu-id="2b581-349">Grants read and write access to the identity registry.</span><span class="sxs-lookup"><span data-stu-id="2b581-349">Grants read and write access to the identity registry.</span></span> <span data-ttu-id="2b581-350">For more information, see [Identity registry][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="2b581-350">For more information, see [Identity registry][lnk-identity-registry].</span></span> <br/><span data-ttu-id="2b581-351">This permission is used by back-end cloud services.</span><span class="sxs-lookup"><span data-stu-id="2b581-351">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="2b581-352">**ServiceConnect**</span><span class="sxs-lookup"><span data-stu-id="2b581-352">**ServiceConnect**</span></span> |<span data-ttu-id="2b581-353">Grants access to cloud service-facing communication and monitoring endpoints.</span><span class="sxs-lookup"><span data-stu-id="2b581-353">Grants access to cloud service-facing communication and monitoring endpoints.</span></span> <br/><span data-ttu-id="2b581-354">Grants permission to receive device-to-cloud messages, send cloud-to-device messages, and retrieve the corresponding delivery acknowledgments.</span><span class="sxs-lookup"><span data-stu-id="2b581-354">Grants permission to receive device-to-cloud messages, send cloud-to-device messages, and retrieve the corresponding delivery acknowledgments.</span></span> <br/><span data-ttu-id="2b581-355">Grants permission to retrieve delivery acknowledgements for file uploads.</span><span class="sxs-lookup"><span data-stu-id="2b581-355">Grants permission to retrieve delivery acknowledgements for file uploads.</span></span> <br/><span data-ttu-id="2b581-356">Grants permission to access twins to update tags and desired properties, retrieve reported properties, and run queries.</span><span class="sxs-lookup"><span data-stu-id="2b581-356">Grants permission to access twins to update tags and desired properties, retrieve reported properties, and run queries.</span></span> <br/><span data-ttu-id="2b581-357">This permission is used by back-end cloud services.</span><span class="sxs-lookup"><span data-stu-id="2b581-357">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="2b581-358">**DeviceConnect**</span><span class="sxs-lookup"><span data-stu-id="2b581-358">**DeviceConnect**</span></span> |<span data-ttu-id="2b581-359">Grants access to device-facing endpoints.</span><span class="sxs-lookup"><span data-stu-id="2b581-359">Grants access to device-facing endpoints.</span></span> <br/><span data-ttu-id="2b581-360">Grants permission to send device-to-cloud messages and receive cloud-to-device messages.</span><span class="sxs-lookup"><span data-stu-id="2b581-360">Grants permission to send device-to-cloud messages and receive cloud-to-device messages.</span></span> <br/><span data-ttu-id="2b581-361">Grants permission to perform file upload from a device.</span><span class="sxs-lookup"><span data-stu-id="2b581-361">Grants permission to perform file upload from a device.</span></span> <br/><span data-ttu-id="2b581-362">Grants permission to receive device twin desired property notifications and update device twin reported properties.</span><span class="sxs-lookup"><span data-stu-id="2b581-362">Grants permission to receive device twin desired property notifications and update device twin reported properties.</span></span> <br/><span data-ttu-id="2b581-363">Grants permission to perform file uploads.</span><span class="sxs-lookup"><span data-stu-id="2b581-363">Grants permission to perform file uploads.</span></span> <br/><span data-ttu-id="2b581-364">This permission is used by devices.</span><span class="sxs-lookup"><span data-stu-id="2b581-364">This permission is used by devices.</span></span> |

## <a name="additional-reference-material"></a><span data-ttu-id="2b581-365">Additional reference material</span><span class="sxs-lookup"><span data-stu-id="2b581-365">Additional reference material</span></span>

<span data-ttu-id="2b581-366">Other reference topics in the IoT Hub developer guide include:</span><span class="sxs-lookup"><span data-stu-id="2b581-366">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="2b581-367">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span><span class="sxs-lookup"><span data-stu-id="2b581-367">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="2b581-368">[Throttling and quotas][lnk-quotas] describes the quotas and throttling behaviors that apply to the IoT Hub service.</span><span class="sxs-lookup"><span data-stu-id="2b581-368">[Throttling and quotas][lnk-quotas] describes the quotas and throttling behaviors that apply to the IoT Hub service.</span></span>
* <span data-ttu-id="2b581-369">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2b581-369">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="2b581-370">[IoT Hub query language][lnk-query] describes the query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span><span class="sxs-lookup"><span data-stu-id="2b581-370">[IoT Hub query language][lnk-query] describes the query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="2b581-371">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span><span class="sxs-lookup"><span data-stu-id="2b581-371">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b581-372">Next steps</span><span class="sxs-lookup"><span data-stu-id="2b581-372">Next steps</span></span>

<span data-ttu-id="2b581-373">Now that you have learned how to control access IoT Hub, you may be interested in the following IoT Hub developer guide topics:</span><span class="sxs-lookup"><span data-stu-id="2b581-373">Now that you have learned how to control access IoT Hub, you may be interested in the following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="2b581-374">[Use device twins to synchronize state and configurations][lnk-devguide-device-twins]</span><span class="sxs-lookup"><span data-stu-id="2b581-374">[Use device twins to synchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="2b581-375">[Invoke a direct method on a device][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="2b581-375">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="2b581-376">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="2b581-376">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="2b581-377">If you would like to try out some of the concepts described in this article, see the following IoT Hub tutorials:</span><span class="sxs-lookup"><span data-stu-id="2b581-377">If you would like to try out some of the concepts described in this article, see the following IoT Hub tutorials:</span></span>

* <span data-ttu-id="2b581-378">[Get started with Azure IoT Hub][lnk-getstarted-tutorial]</span><span class="sxs-lookup"><span data-stu-id="2b581-378">[Get started with Azure IoT Hub][lnk-getstarted-tutorial]</span></span>
* <span data-ttu-id="2b581-379">[How to send cloud-to-device messages with IoT Hub][lnk-c2d-tutorial]</span><span class="sxs-lookup"><span data-stu-id="2b581-379">[How to send cloud-to-device messages with IoT Hub][lnk-c2d-tutorial]</span></span>
* <span data-ttu-id="2b581-380">[How to process IoT Hub device-to-cloud messages][lnk-d2c-tutorial]</span><span class="sxs-lookup"><span data-stu-id="2b581-380">[How to process IoT Hub device-to-cloud messages][lnk-d2c-tutorial]</span></span>

<!-- links and images -->

[img-tokenservice]: ./media/iot-hub-devguide-security/tokenservice.png
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-openssl]: https://www.openssl.org/
[lnk-selfsigned]: https://docs.microsoft.com/powershell/module/pkiclient/new-selfsignedcertificate

[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-sas-tokens]: iot-hub-devguide-security.md#security-tokens
[lnk-amqp]: https://www.amqp.org/
[lnk-azure-resource-manager]: ../azure-resource-manager/resource-group-overview.md
[lnk-cbs]: https://www.oasis-open.org/committees/download.php/50506/amqp-cbs-v1%200-wd02%202013-08-12.doc
[lnk-event-hubs-publisher-policy]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-99ce67ab
[lnk-management-portal]: https://portal.azure.com
[lnk-sasl-plain]: http://tools.ietf.org/html/rfc4616
[lnk-identity-registry]: iot-hub-devguide-identity-registry.md
[lnk-dotnet-sas]: https://msdn.microsoft.com/library/microsoft.azure.devices.common.security.sharedaccesssignaturebuilder.aspx
[lnk-java-sas]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.service.auth._iot_hub_service_sas_token
[lnk-tls-psk]: https://tools.ietf.org/html/rfc4279
[lnk-protocols]: iot-hub-protocol-gateway.md
[lnk-custom-auth]: iot-hub-devguide-security.md#custom-device-and-module-authentication
[lnk-x509]: iot-hub-devguide-security.md#supported-x509-certificates
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-service-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/service
[lnk-client-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer
[lnk-getstarted-tutorial]: quickstart-send-telemetry-node.md
[lnk-c2d-tutorial]: iot-hub-csharp-csharp-c2d.md
[lnk-d2c-tutorial]: tutorial-routing.md
