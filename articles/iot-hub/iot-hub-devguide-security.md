---
title: Understand Azure IoT Hub security | Microsoft Docs
description: Developer guide - how to control access to IoT Hub for device apps and back-end apps. Includes information about security tokens and support for X.509 certificates.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: ''
ms.assetid: 45631e70-865b-4e06-bb1d-aae1175a52ba
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: dobett
ms.openlocfilehash: fb91c848d1372ae4d381d8dbea3983808e0a0ec0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556720"
---
# <a name="control-access-to-iot-hub"></a><span data-ttu-id="75c4f-104">Control access to IoT Hub</span><span class="sxs-lookup"><span data-stu-id="75c4f-104">Control access to IoT Hub</span></span>

## <a name="overview"></a><span data-ttu-id="75c4f-105">Overview</span><span class="sxs-lookup"><span data-stu-id="75c4f-105">Overview</span></span>

<span data-ttu-id="75c4f-106">This article describes the options for securing your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="75c4f-106">This article describes the options for securing your IoT hub.</span></span> <span data-ttu-id="75c4f-107">IoT Hub uses *permissions* to grant access to each IoT hub endpoint.</span><span class="sxs-lookup"><span data-stu-id="75c4f-107">IoT Hub uses *permissions* to grant access to each IoT hub endpoint.</span></span> <span data-ttu-id="75c4f-108">Permissions limit the access to an IoT hub based on functionality.</span><span class="sxs-lookup"><span data-stu-id="75c4f-108">Permissions limit the access to an IoT hub based on functionality.</span></span>

<span data-ttu-id="75c4f-109">This article describes:</span><span class="sxs-lookup"><span data-stu-id="75c4f-109">This article describes:</span></span>

* <span data-ttu-id="75c4f-110">The different permissions that you can grant to a device or back-end app to access your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="75c4f-110">The different permissions that you can grant to a device or back-end app to access your IoT hub.</span></span>
* <span data-ttu-id="75c4f-111">The authentication process and the tokens it uses to verify permissions.</span><span class="sxs-lookup"><span data-stu-id="75c4f-111">The authentication process and the tokens it uses to verify permissions.</span></span>
* <span data-ttu-id="75c4f-112">How to scope credentials to limit access to specific resources.</span><span class="sxs-lookup"><span data-stu-id="75c4f-112">How to scope credentials to limit access to specific resources.</span></span>
* <span data-ttu-id="75c4f-113">IoT Hub support for X.509 certificates.</span><span class="sxs-lookup"><span data-stu-id="75c4f-113">IoT Hub support for X.509 certificates.</span></span>
* <span data-ttu-id="75c4f-114">Custom device authentication mechanisms that use existing device identity registries or authentication schemes.</span><span class="sxs-lookup"><span data-stu-id="75c4f-114">Custom device authentication mechanisms that use existing device identity registries or authentication schemes.</span></span>

### <a name="when-to-use"></a><span data-ttu-id="75c4f-115">When to use</span><span class="sxs-lookup"><span data-stu-id="75c4f-115">When to use</span></span>

<span data-ttu-id="75c4f-116">You must have appropriate permissions to access any of the IoT Hub endpoints.</span><span class="sxs-lookup"><span data-stu-id="75c4f-116">You must have appropriate permissions to access any of the IoT Hub endpoints.</span></span> <span data-ttu-id="75c4f-117">For example, a device must include a token containing security credentials along with every message it sends to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="75c4f-117">For example, a device must include a token containing security credentials along with every message it sends to IoT Hub.</span></span>

## <a name="access-control-and-permissions"></a><span data-ttu-id="75c4f-118">Access control and permissions</span><span class="sxs-lookup"><span data-stu-id="75c4f-118">Access control and permissions</span></span>

<span data-ttu-id="75c4f-119">You can grant [permissions](#iot-hub-permissions) in the following ways:</span><span class="sxs-lookup"><span data-stu-id="75c4f-119">You can grant [permissions](#iot-hub-permissions) in the following ways:</span></span>

* <span data-ttu-id="75c4f-120">**IoT hub-level shared access policies**.</span><span class="sxs-lookup"><span data-stu-id="75c4f-120">**IoT hub-level shared access policies**.</span></span> <span data-ttu-id="75c4f-121">Shared access policies can grant any combination of [permissions](#iot-hub-permissions).</span><span class="sxs-lookup"><span data-stu-id="75c4f-121">Shared access policies can grant any combination of [permissions](#iot-hub-permissions).</span></span> <span data-ttu-id="75c4f-122">You can define policies in the [Azure portal][lnk-management-portal], or programmatically by using the [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span><span class="sxs-lookup"><span data-stu-id="75c4f-122">You can define policies in the [Azure portal][lnk-management-portal], or programmatically by using the [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span></span> <span data-ttu-id="75c4f-123">A newly created IoT hub has the following default policies:</span><span class="sxs-lookup"><span data-stu-id="75c4f-123">A newly created IoT hub has the following default policies:</span></span>

  * <span data-ttu-id="75c4f-124">**iothubowner**: Policy with all permissions.</span><span class="sxs-lookup"><span data-stu-id="75c4f-124">**iothubowner**: Policy with all permissions.</span></span>
  * <span data-ttu-id="75c4f-125">**service**: Policy with **ServiceConnect** permission.</span><span class="sxs-lookup"><span data-stu-id="75c4f-125">**service**: Policy with **ServiceConnect** permission.</span></span>
  * <span data-ttu-id="75c4f-126">**device**: Policy with **DeviceConnect** permission.</span><span class="sxs-lookup"><span data-stu-id="75c4f-126">**device**: Policy with **DeviceConnect** permission.</span></span>
  * <span data-ttu-id="75c4f-127">**registryRead**: Policy with **RegistryRead** permission.</span><span class="sxs-lookup"><span data-stu-id="75c4f-127">**registryRead**: Policy with **RegistryRead** permission.</span></span>
  * <span data-ttu-id="75c4f-128">**registryReadWrite**: Policy with **RegistryRead** and RegistryWrite permissions.</span><span class="sxs-lookup"><span data-stu-id="75c4f-128">**registryReadWrite**: Policy with **RegistryRead** and RegistryWrite permissions.</span></span>
  * <span data-ttu-id="75c4f-129">**Per-device security credentials**.</span><span class="sxs-lookup"><span data-stu-id="75c4f-129">**Per-device security credentials**.</span></span> <span data-ttu-id="75c4f-130">Each IoT Hub contains an [identity registry][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="75c4f-130">Each IoT Hub contains an [identity registry][lnk-identity-registry].</span></span> <span data-ttu-id="75c4f-131">For each device in this identity registry, you can configure security credentials that grant **DeviceConnect** permissions scoped to the corresponding device endpoints.</span><span class="sxs-lookup"><span data-stu-id="75c4f-131">For each device in this identity registry, you can configure security credentials that grant **DeviceConnect** permissions scoped to the corresponding device endpoints.</span></span>

<span data-ttu-id="75c4f-132">For example, in a typical IoT solution:</span><span class="sxs-lookup"><span data-stu-id="75c4f-132">For example, in a typical IoT solution:</span></span>

* <span data-ttu-id="75c4f-133">The device management component uses the *registryReadWrite* policy.</span><span class="sxs-lookup"><span data-stu-id="75c4f-133">The device management component uses the *registryReadWrite* policy.</span></span>
* <span data-ttu-id="75c4f-134">The event processor component uses the *service* policy.</span><span class="sxs-lookup"><span data-stu-id="75c4f-134">The event processor component uses the *service* policy.</span></span>
* <span data-ttu-id="75c4f-135">The run-time device business logic component uses the *service* policy.</span><span class="sxs-lookup"><span data-stu-id="75c4f-135">The run-time device business logic component uses the *service* policy.</span></span>
* <span data-ttu-id="75c4f-136">Individual devices connect using credentials stored in the IoT hub's identity registry.</span><span class="sxs-lookup"><span data-stu-id="75c4f-136">Individual devices connect using credentials stored in the IoT hub's identity registry.</span></span>

> [!NOTE]
> <span data-ttu-id="75c4f-137">See [permissions](#iot-hub-permissions) for detailed information.</span><span class="sxs-lookup"><span data-stu-id="75c4f-137">See [permissions](#iot-hub-permissions) for detailed information.</span></span>

## <a name="authentication"></a><span data-ttu-id="75c4f-138">Authentication</span><span class="sxs-lookup"><span data-stu-id="75c4f-138">Authentication</span></span>

<span data-ttu-id="75c4f-139">Azure IoT Hub grants access to endpoints by verifying a token against the shared access policies and identity registry security credentials.</span><span class="sxs-lookup"><span data-stu-id="75c4f-139">Azure IoT Hub grants access to endpoints by verifying a token against the shared access policies and identity registry security credentials.</span></span>

<span data-ttu-id="75c4f-140">Security credentials, such as symmetric keys, are never sent over the wire.</span><span class="sxs-lookup"><span data-stu-id="75c4f-140">Security credentials, such as symmetric keys, are never sent over the wire.</span></span>

> [!NOTE]
> <span data-ttu-id="75c4f-141">The Azure IoT Hub resource provider is secured through your Azure subscription, as are all providers in the [Azure Resource Manager][lnk-azure-resource-manager].</span><span class="sxs-lookup"><span data-stu-id="75c4f-141">The Azure IoT Hub resource provider is secured through your Azure subscription, as are all providers in the [Azure Resource Manager][lnk-azure-resource-manager].</span></span>

<span data-ttu-id="75c4f-142">For more information about how to construct and use security tokens, see [IoT Hub security tokens][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="75c4f-142">For more information about how to construct and use security tokens, see [IoT Hub security tokens][lnk-sas-tokens].</span></span>

### <a name="protocol-specifics"></a><span data-ttu-id="75c4f-143">Protocol specifics</span><span class="sxs-lookup"><span data-stu-id="75c4f-143">Protocol specifics</span></span>

<span data-ttu-id="75c4f-144">Each supported protocol, such as MQTT, AMQP, and HTTP, transports tokens in different ways.</span><span class="sxs-lookup"><span data-stu-id="75c4f-144">Each supported protocol, such as MQTT, AMQP, and HTTP, transports tokens in different ways.</span></span>

<span data-ttu-id="75c4f-145">When using MQTT, the CONNECT packet has the deviceId as the ClientId, {iothubhostname}/{deviceId} in the Username field, and a SAS token in the Password field.</span><span class="sxs-lookup"><span data-stu-id="75c4f-145">When using MQTT, the CONNECT packet has the deviceId as the ClientId, {iothubhostname}/{deviceId} in the Username field, and a SAS token in the Password field.</span></span> <span data-ttu-id="75c4f-146">{iothubhostname} should be the full CName of the IoT hub (for example, contoso.azure-devices.net).</span><span class="sxs-lookup"><span data-stu-id="75c4f-146">{iothubhostname} should be the full CName of the IoT hub (for example, contoso.azure-devices.net).</span></span>

<span data-ttu-id="75c4f-147">When using [AMQP][lnk-amqp], IoT Hub supports [SASL PLAIN][lnk-sasl-plain] and [AMQP Claims-Based-Security][lnk-cbs].</span><span class="sxs-lookup"><span data-stu-id="75c4f-147">When using [AMQP][lnk-amqp], IoT Hub supports [SASL PLAIN][lnk-sasl-plain] and [AMQP Claims-Based-Security][lnk-cbs].</span></span>

<span data-ttu-id="75c4f-148">If you use AMQP claims-based-security, the standard specifies how to transmit these tokens.</span><span class="sxs-lookup"><span data-stu-id="75c4f-148">If you use AMQP claims-based-security, the standard specifies how to transmit these tokens.</span></span>

<span data-ttu-id="75c4f-149">For SASL PLAIN, the **username** can be:</span><span class="sxs-lookup"><span data-stu-id="75c4f-149">For SASL PLAIN, the **username** can be:</span></span>

* <span data-ttu-id="75c4f-150">`{policyName}@sas.root.{iothubName}` if using IoT hub-level tokens.</span><span class="sxs-lookup"><span data-stu-id="75c4f-150">`{policyName}@sas.root.{iothubName}` if using IoT hub-level tokens.</span></span>
* <span data-ttu-id="75c4f-151">`{deviceId}@sas.{iothubname}` if using device-scoped tokens.</span><span class="sxs-lookup"><span data-stu-id="75c4f-151">`{deviceId}@sas.{iothubname}` if using device-scoped tokens.</span></span>

<span data-ttu-id="75c4f-152">In both cases, the password field contains the token, as described in [IoT Hub security tokens][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="75c4f-152">In both cases, the password field contains the token, as described in [IoT Hub security tokens][lnk-sas-tokens].</span></span>

<span data-ttu-id="75c4f-153">HTTP implements authentication by including a valid token in the **Authorization** request header.</span><span class="sxs-lookup"><span data-stu-id="75c4f-153">HTTP implements authentication by including a valid token in the **Authorization** request header.</span></span>

#### <a name="example"></a><span data-ttu-id="75c4f-154">Example</span><span class="sxs-lookup"><span data-stu-id="75c4f-154">Example</span></span>

<span data-ttu-id="75c4f-155">Username (DeviceId is case-sensitive): `iothubname.azure-devices.net/DeviceId`</span><span class="sxs-lookup"><span data-stu-id="75c4f-155">Username (DeviceId is case-sensitive): `iothubname.azure-devices.net/DeviceId`</span></span>

<span data-ttu-id="75c4f-156">Password (Generate SAS token with the [device explorer][lnk-device-explorer] tool): `SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501`</span><span class="sxs-lookup"><span data-stu-id="75c4f-156">Password (Generate SAS token with the [device explorer][lnk-device-explorer] tool): `SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501`</span></span>

> [!NOTE]
> <span data-ttu-id="75c4f-157">The [Azure IoT SDKs][lnk-sdks] automatically generate tokens when connecting to the service.</span><span class="sxs-lookup"><span data-stu-id="75c4f-157">The [Azure IoT SDKs][lnk-sdks] automatically generate tokens when connecting to the service.</span></span> <span data-ttu-id="75c4f-158">In some cases, the Azure IoT SDKs do not support all the protocols or all the authentication methods.</span><span class="sxs-lookup"><span data-stu-id="75c4f-158">In some cases, the Azure IoT SDKs do not support all the protocols or all the authentication methods.</span></span>

### <a name="special-considerations-for-sasl-plain"></a><span data-ttu-id="75c4f-159">Special considerations for SASL PLAIN</span><span class="sxs-lookup"><span data-stu-id="75c4f-159">Special considerations for SASL PLAIN</span></span>

<span data-ttu-id="75c4f-160">When using SASL PLAIN with AMQP, a client connecting to an IoT hub can use a single token for each TCP connection.</span><span class="sxs-lookup"><span data-stu-id="75c4f-160">When using SASL PLAIN with AMQP, a client connecting to an IoT hub can use a single token for each TCP connection.</span></span> <span data-ttu-id="75c4f-161">When the token expires, the TCP connection disconnects from the service and triggers a reconnect.</span><span class="sxs-lookup"><span data-stu-id="75c4f-161">When the token expires, the TCP connection disconnects from the service and triggers a reconnect.</span></span> <span data-ttu-id="75c4f-162">This behavior, while not problematic for a back-end app, is damaging for a device app for the following reasons:</span><span class="sxs-lookup"><span data-stu-id="75c4f-162">This behavior, while not problematic for a back-end app, is damaging for a device app for the following reasons:</span></span>

* <span data-ttu-id="75c4f-163">Gateways usually connect on behalf of many devices.</span><span class="sxs-lookup"><span data-stu-id="75c4f-163">Gateways usually connect on behalf of many devices.</span></span> <span data-ttu-id="75c4f-164">When using SASL PLAIN, they have to create a distinct TCP connection for each device connecting to an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="75c4f-164">When using SASL PLAIN, they have to create a distinct TCP connection for each device connecting to an IoT hub.</span></span> <span data-ttu-id="75c4f-165">This scenario considerably increases the consumption of power and networking resources, and increases the latency of each device connection.</span><span class="sxs-lookup"><span data-stu-id="75c4f-165">This scenario considerably increases the consumption of power and networking resources, and increases the latency of each device connection.</span></span>
* <span data-ttu-id="75c4f-166">Resource-constrained devices are adversely affected by the increased use of resources to reconnect after each token expiration.</span><span class="sxs-lookup"><span data-stu-id="75c4f-166">Resource-constrained devices are adversely affected by the increased use of resources to reconnect after each token expiration.</span></span>

## <a name="scope-iot-hub-level-credentials"></a><span data-ttu-id="75c4f-167">Scope IoT hub-level credentials</span><span class="sxs-lookup"><span data-stu-id="75c4f-167">Scope IoT hub-level credentials</span></span>

<span data-ttu-id="75c4f-168">You can scope IoT hub-level security policies by creating tokens with a restricted resource URI.</span><span class="sxs-lookup"><span data-stu-id="75c4f-168">You can scope IoT hub-level security policies by creating tokens with a restricted resource URI.</span></span> <span data-ttu-id="75c4f-169">For example, the endpoint to send device-to-cloud messages from a device is **/devices/{deviceId}/messages/events**.</span><span class="sxs-lookup"><span data-stu-id="75c4f-169">For example, the endpoint to send device-to-cloud messages from a device is **/devices/{deviceId}/messages/events**.</span></span> <span data-ttu-id="75c4f-170">You can also use an IoT hub-level shared access policy with **DeviceConnect** permissions to sign a token whose resourceURI is **/devices/{deviceId}**.</span><span class="sxs-lookup"><span data-stu-id="75c4f-170">You can also use an IoT hub-level shared access policy with **DeviceConnect** permissions to sign a token whose resourceURI is **/devices/{deviceId}**.</span></span> <span data-ttu-id="75c4f-171">This approach creates a token that is only usable to send messages on behalf of device **deviceId**.</span><span class="sxs-lookup"><span data-stu-id="75c4f-171">This approach creates a token that is only usable to send messages on behalf of device **deviceId**.</span></span>

<span data-ttu-id="75c4f-172">This mechanism is similar to the [Event Hubs publisher policy][lnk-event-hubs-publisher-policy], and enables you to implement custom authentication methods.</span><span class="sxs-lookup"><span data-stu-id="75c4f-172">This mechanism is similar to the [Event Hubs publisher policy][lnk-event-hubs-publisher-policy], and enables you to implement custom authentication methods.</span></span>

## <a name="security-tokens"></a><span data-ttu-id="75c4f-173">Security tokens</span><span class="sxs-lookup"><span data-stu-id="75c4f-173">Security tokens</span></span>

<span data-ttu-id="75c4f-174">IoT Hub uses security tokens to authenticate devices and services to avoid sending keys on the wire.</span><span class="sxs-lookup"><span data-stu-id="75c4f-174">IoT Hub uses security tokens to authenticate devices and services to avoid sending keys on the wire.</span></span> <span data-ttu-id="75c4f-175">Additionally, security tokens are limited in time validity and scope.</span><span class="sxs-lookup"><span data-stu-id="75c4f-175">Additionally, security tokens are limited in time validity and scope.</span></span> <span data-ttu-id="75c4f-176">[Azure IoT SDKs][lnk-sdks] automatically generate tokens without requiring any special configuration.</span><span class="sxs-lookup"><span data-stu-id="75c4f-176">[Azure IoT SDKs][lnk-sdks] automatically generate tokens without requiring any special configuration.</span></span> <span data-ttu-id="75c4f-177">Some scenarios, however, require you to generate and use security tokens directly.</span><span class="sxs-lookup"><span data-stu-id="75c4f-177">Some scenarios, however, require you to generate and use security tokens directly.</span></span> <span data-ttu-id="75c4f-178">These scenarios include the direct use of the MQTT, AMQP, or HTTP surfaces, or the implementation of the token service pattern, as explained in [Custom device authentication][lnk-custom-auth].</span><span class="sxs-lookup"><span data-stu-id="75c4f-178">These scenarios include the direct use of the MQTT, AMQP, or HTTP surfaces, or the implementation of the token service pattern, as explained in [Custom device authentication][lnk-custom-auth].</span></span>

<span data-ttu-id="75c4f-179">IoT Hub also allows devices to authenticate with IoT Hub using [X.509 certificates][lnk-x509].</span><span class="sxs-lookup"><span data-stu-id="75c4f-179">IoT Hub also allows devices to authenticate with IoT Hub using [X.509 certificates][lnk-x509].</span></span> 

### <a name="security-token-structure"></a><span data-ttu-id="75c4f-180">Security token structure</span><span class="sxs-lookup"><span data-stu-id="75c4f-180">Security token structure</span></span>

<span data-ttu-id="75c4f-181">You use security tokens to grant time-bounded access to devices and services to specific functionality in IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="75c4f-181">You use security tokens to grant time-bounded access to devices and services to specific functionality in IoT Hub.</span></span> <span data-ttu-id="75c4f-182">To ensure that only authorized devices and services can connect, security tokens must be signed with either a shared access key or a symmetric key.</span><span class="sxs-lookup"><span data-stu-id="75c4f-182">To ensure that only authorized devices and services can connect, security tokens must be signed with either a shared access key or a symmetric key.</span></span> <span data-ttu-id="75c4f-183">These keys are stored with a device identity in the identity registry.</span><span class="sxs-lookup"><span data-stu-id="75c4f-183">These keys are stored with a device identity in the identity registry.</span></span>

<span data-ttu-id="75c4f-184">A token signed with a shared access key grants access to all the functionality associated with the shared access policy permissions.</span><span class="sxs-lookup"><span data-stu-id="75c4f-184">A token signed with a shared access key grants access to all the functionality associated with the shared access policy permissions.</span></span> <span data-ttu-id="75c4f-185">On the other hand, a token signed with a device identity's symmetric key only grants the **DeviceConnect** permission for the associated device identity.</span><span class="sxs-lookup"><span data-stu-id="75c4f-185">On the other hand, a token signed with a device identity's symmetric key only grants the **DeviceConnect** permission for the associated device identity.</span></span>

<span data-ttu-id="75c4f-186">The security token has the following format:</span><span class="sxs-lookup"><span data-stu-id="75c4f-186">The security token has the following format:</span></span>

`SharedAccessSignature sig={signature-string}&se={expiry}&skn={policyName}&sr={URL-encoded-resourceURI}`

<span data-ttu-id="75c4f-187">Here are the expected values:</span><span class="sxs-lookup"><span data-stu-id="75c4f-187">Here are the expected values:</span></span>

| <span data-ttu-id="75c4f-188">Value</span><span class="sxs-lookup"><span data-stu-id="75c4f-188">Value</span></span> | <span data-ttu-id="75c4f-189">Description</span><span class="sxs-lookup"><span data-stu-id="75c4f-189">Description</span></span> |
| --- | --- |
| <span data-ttu-id="75c4f-190">{signature}</span><span class="sxs-lookup"><span data-stu-id="75c4f-190">{signature}</span></span> |<span data-ttu-id="75c4f-191">An HMAC-SHA256 signature string of the form: `{URL-encoded-resourceURI} + "\n" + expiry`.</span><span class="sxs-lookup"><span data-stu-id="75c4f-191">An HMAC-SHA256 signature string of the form: `{URL-encoded-resourceURI} + "\n" + expiry`.</span></span> <span data-ttu-id="75c4f-192">**Important**: The key is decoded from base64 and used as key to perform the HMAC-SHA256 computation.</span><span class="sxs-lookup"><span data-stu-id="75c4f-192">**Important**: The key is decoded from base64 and used as key to perform the HMAC-SHA256 computation.</span></span> |
| <span data-ttu-id="75c4f-193">{resourceURI}</span><span class="sxs-lookup"><span data-stu-id="75c4f-193">{resourceURI}</span></span> |<span data-ttu-id="75c4f-194">URI prefix (by segment) of the endpoints that can be accessed with this token, starting with host name of the IoT hub (no protocol).</span><span class="sxs-lookup"><span data-stu-id="75c4f-194">URI prefix (by segment) of the endpoints that can be accessed with this token, starting with host name of the IoT hub (no protocol).</span></span> <span data-ttu-id="75c4f-195">For example, `myHub.azure-devices.net/devices/device1`</span><span class="sxs-lookup"><span data-stu-id="75c4f-195">For example, `myHub.azure-devices.net/devices/device1`</span></span> |
| <span data-ttu-id="75c4f-196">{expiry}</span><span class="sxs-lookup"><span data-stu-id="75c4f-196">{expiry}</span></span> |<span data-ttu-id="75c4f-197">UTF8 strings for number of seconds since the epoch 00:00:00 UTC on 1 January 1970.</span><span class="sxs-lookup"><span data-stu-id="75c4f-197">UTF8 strings for number of seconds since the epoch 00:00:00 UTC on 1 January 1970.</span></span> |
| <span data-ttu-id="75c4f-198">{URL-encoded-resourceURI}</span><span class="sxs-lookup"><span data-stu-id="75c4f-198">{URL-encoded-resourceURI}</span></span> |<span data-ttu-id="75c4f-199">Lower case URL-encoding of the lower case resource URI</span><span class="sxs-lookup"><span data-stu-id="75c4f-199">Lower case URL-encoding of the lower case resource URI</span></span> |
| <span data-ttu-id="75c4f-200">{policyName}</span><span class="sxs-lookup"><span data-stu-id="75c4f-200">{policyName}</span></span> |<span data-ttu-id="75c4f-201">The name of the shared access policy to which this token refers.</span><span class="sxs-lookup"><span data-stu-id="75c4f-201">The name of the shared access policy to which this token refers.</span></span> <span data-ttu-id="75c4f-202">Absent if the token refers to device-registry credentials.</span><span class="sxs-lookup"><span data-stu-id="75c4f-202">Absent if the token refers to device-registry credentials.</span></span> |

<span data-ttu-id="75c4f-203">**Note on prefix**: The URI prefix is computed by segment and not by character.</span><span class="sxs-lookup"><span data-stu-id="75c4f-203">**Note on prefix**: The URI prefix is computed by segment and not by character.</span></span> <span data-ttu-id="75c4f-204">For example `/a/b` is a prefix for `/a/b/c` but not for `/a/bc`.</span><span class="sxs-lookup"><span data-stu-id="75c4f-204">For example `/a/b` is a prefix for `/a/b/c` but not for `/a/bc`.</span></span>

<span data-ttu-id="75c4f-205">The following Node.js snippet shows a function called **generateSasToken** that computes the token from the inputs `resourceUri, signingKey, policyName, expiresInMins`.</span><span class="sxs-lookup"><span data-stu-id="75c4f-205">The following Node.js snippet shows a function called **generateSasToken** that computes the token from the inputs `resourceUri, signingKey, policyName, expiresInMins`.</span></span> <span data-ttu-id="75c4f-206">The next sections detail how to initialize the different inputs for the different token use cases.</span><span class="sxs-lookup"><span data-stu-id="75c4f-206">The next sections detail how to initialize the different inputs for the different token use cases.</span></span>

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

<span data-ttu-id="75c4f-207">As a comparison, the equivalent Python code to generate a security token is:</span><span class="sxs-lookup"><span data-stu-id="75c4f-207">As a comparison, the equivalent Python code to generate a security token is:</span></span>

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

> [!NOTE]
> <span data-ttu-id="75c4f-208">Since the time validity of the token is validated on IoT Hub machines, the drift on the clock of the machine that generates the token must be minimal.</span><span class="sxs-lookup"><span data-stu-id="75c4f-208">Since the time validity of the token is validated on IoT Hub machines, the drift on the clock of the machine that generates the token must be minimal.</span></span>

### <a name="use-sas-tokens-in-a-device-app"></a><span data-ttu-id="75c4f-209">Use SAS tokens in a device app</span><span class="sxs-lookup"><span data-stu-id="75c4f-209">Use SAS tokens in a device app</span></span>

<span data-ttu-id="75c4f-210">There are two ways to obtain **DeviceConnect** permissions with IoT Hub with security tokens: use a [symmetric device key from the identity registry](#use-a-symmetric-key-in-the-identity-registry), or use a [shared access key](#use-a-shared-access-policy).</span><span class="sxs-lookup"><span data-stu-id="75c4f-210">There are two ways to obtain **DeviceConnect** permissions with IoT Hub with security tokens: use a [symmetric device key from the identity registry](#use-a-symmetric-key-in-the-identity-registry), or use a [shared access key](#use-a-shared-access-policy).</span></span>

<span data-ttu-id="75c4f-211">Remember that all functionality accessible from devices is exposed by design on endpoints with prefix `/devices/{deviceId}`.</span><span class="sxs-lookup"><span data-stu-id="75c4f-211">Remember that all functionality accessible from devices is exposed by design on endpoints with prefix `/devices/{deviceId}`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="75c4f-212">The only way that IoT Hub authenticates a specific device is using the device identity symmetric key.</span><span class="sxs-lookup"><span data-stu-id="75c4f-212">The only way that IoT Hub authenticates a specific device is using the device identity symmetric key.</span></span> <span data-ttu-id="75c4f-213">In cases when a shared access policy is used to access device functionality, the solution must consider the component issuing the security token as a trusted subcomponent.</span><span class="sxs-lookup"><span data-stu-id="75c4f-213">In cases when a shared access policy is used to access device functionality, the solution must consider the component issuing the security token as a trusted subcomponent.</span></span>

<span data-ttu-id="75c4f-214">The device-facing endpoints are (irrespective of the protocol):</span><span class="sxs-lookup"><span data-stu-id="75c4f-214">The device-facing endpoints are (irrespective of the protocol):</span></span>

| <span data-ttu-id="75c4f-215">Endpoint</span><span class="sxs-lookup"><span data-stu-id="75c4f-215">Endpoint</span></span> | <span data-ttu-id="75c4f-216">Functionality</span><span class="sxs-lookup"><span data-stu-id="75c4f-216">Functionality</span></span> |
| --- | --- |
| `{iot hub host name}/devices/{deviceId}/messages/events` |<span data-ttu-id="75c4f-217">Send device-to-cloud messages.</span><span class="sxs-lookup"><span data-stu-id="75c4f-217">Send device-to-cloud messages.</span></span> |
| `{iot hub host name}/devices/{deviceId}/devicebound` |<span data-ttu-id="75c4f-218">Receive cloud-to-device messages.</span><span class="sxs-lookup"><span data-stu-id="75c4f-218">Receive cloud-to-device messages.</span></span> |

### <a name="use-a-symmetric-key-in-the-identity-registry"></a><span data-ttu-id="75c4f-219">Use a symmetric key in the identity registry</span><span class="sxs-lookup"><span data-stu-id="75c4f-219">Use a symmetric key in the identity registry</span></span>

<span data-ttu-id="75c4f-220">When using a device identity's symmetric key to generate a token, the policyName (`skn`) element of the token is omitted.</span><span class="sxs-lookup"><span data-stu-id="75c4f-220">When using a device identity's symmetric key to generate a token, the policyName (`skn`) element of the token is omitted.</span></span>

<span data-ttu-id="75c4f-221">For example, a token created to access all device functionality should have the following parameters:</span><span class="sxs-lookup"><span data-stu-id="75c4f-221">For example, a token created to access all device functionality should have the following parameters:</span></span>

* <span data-ttu-id="75c4f-222">resource URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span><span class="sxs-lookup"><span data-stu-id="75c4f-222">resource URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span></span>
* <span data-ttu-id="75c4f-223">signing key: any symmetric key for the `{device id}` identity,</span><span class="sxs-lookup"><span data-stu-id="75c4f-223">signing key: any symmetric key for the `{device id}` identity,</span></span>
* <span data-ttu-id="75c4f-224">no policy name,</span><span class="sxs-lookup"><span data-stu-id="75c4f-224">no policy name,</span></span>
* <span data-ttu-id="75c4f-225">any expiration time.</span><span class="sxs-lookup"><span data-stu-id="75c4f-225">any expiration time.</span></span>

<span data-ttu-id="75c4f-226">An example using the preceding Node.js function would be:</span><span class="sxs-lookup"><span data-stu-id="75c4f-226">An example using the preceding Node.js function would be:</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var deviceKey ="...";

var token = generateSasToken(endpoint, deviceKey, null, 60);
```

<span data-ttu-id="75c4f-227">The result, which grants access to all functionality for device1, would be:</span><span class="sxs-lookup"><span data-stu-id="75c4f-227">The result, which grants access to all functionality for device1, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697`

> [!NOTE]
> <span data-ttu-id="75c4f-228">It is possible to generate a SAS token using the .NET [device explorer][lnk-device-explorer] tool or the cross-platform, node-based [iothub-explorer][lnk-iothub-explorer] command-line utility.</span><span class="sxs-lookup"><span data-stu-id="75c4f-228">It is possible to generate a SAS token using the .NET [device explorer][lnk-device-explorer] tool or the cross-platform, node-based [iothub-explorer][lnk-iothub-explorer] command-line utility.</span></span>

### <a name="use-a-shared-access-policy"></a><span data-ttu-id="75c4f-229">Use a shared access policy</span><span class="sxs-lookup"><span data-stu-id="75c4f-229">Use a shared access policy</span></span>

<span data-ttu-id="75c4f-230">When creating a token from a shared access policy, the policy name field `skn` must be set to the name of the policy used.</span><span class="sxs-lookup"><span data-stu-id="75c4f-230">When creating a token from a shared access policy, the policy name field `skn` must be set to the name of the policy used.</span></span> <span data-ttu-id="75c4f-231">It is also required that the policy grants the **DeviceConnect** permission.</span><span class="sxs-lookup"><span data-stu-id="75c4f-231">It is also required that the policy grants the **DeviceConnect** permission.</span></span>

<span data-ttu-id="75c4f-232">The two main scenarios for using shared access policies to access device functionality are:</span><span class="sxs-lookup"><span data-stu-id="75c4f-232">The two main scenarios for using shared access policies to access device functionality are:</span></span>

* <span data-ttu-id="75c4f-233">[cloud protocol gateways][lnk-endpoints],</span><span class="sxs-lookup"><span data-stu-id="75c4f-233">[cloud protocol gateways][lnk-endpoints],</span></span>
* <span data-ttu-id="75c4f-234">[token services][lnk-custom-auth] used to implement custom authentication schemes.</span><span class="sxs-lookup"><span data-stu-id="75c4f-234">[token services][lnk-custom-auth] used to implement custom authentication schemes.</span></span>

<span data-ttu-id="75c4f-235">Since the shared access policy can potentially grant access to connect as any device, it is important to use the correct resource URI when creating security tokens.</span><span class="sxs-lookup"><span data-stu-id="75c4f-235">Since the shared access policy can potentially grant access to connect as any device, it is important to use the correct resource URI when creating security tokens.</span></span> <span data-ttu-id="75c4f-236">This is especially important for token services, which have to scope the token to a specific device using the resource URI.</span><span class="sxs-lookup"><span data-stu-id="75c4f-236">This is especially important for token services, which have to scope the token to a specific device using the resource URI.</span></span> <span data-ttu-id="75c4f-237">This point is less relevant for protocol gateways as they are already mediating traffic for all devices.</span><span class="sxs-lookup"><span data-stu-id="75c4f-237">This point is less relevant for protocol gateways as they are already mediating traffic for all devices.</span></span>

<span data-ttu-id="75c4f-238">As an example, a token service using the pre-created shared access policy called **device** would create a token with the following parameters:</span><span class="sxs-lookup"><span data-stu-id="75c4f-238">As an example, a token service using the pre-created shared access policy called **device** would create a token with the following parameters:</span></span>

* <span data-ttu-id="75c4f-239">resource URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span><span class="sxs-lookup"><span data-stu-id="75c4f-239">resource URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span></span>
* <span data-ttu-id="75c4f-240">signing key: one of the keys of the `device` policy,</span><span class="sxs-lookup"><span data-stu-id="75c4f-240">signing key: one of the keys of the `device` policy,</span></span>
* <span data-ttu-id="75c4f-241">policy name: `device`,</span><span class="sxs-lookup"><span data-stu-id="75c4f-241">policy name: `device`,</span></span>
* <span data-ttu-id="75c4f-242">any expiration time.</span><span class="sxs-lookup"><span data-stu-id="75c4f-242">any expiration time.</span></span>

<span data-ttu-id="75c4f-243">An example using the preceding Node.js function would be:</span><span class="sxs-lookup"><span data-stu-id="75c4f-243">An example using the preceding Node.js function would be:</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

<span data-ttu-id="75c4f-244">The result, which grants access to all functionality for device1, would be:</span><span class="sxs-lookup"><span data-stu-id="75c4f-244">The result, which grants access to all functionality for device1, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697&skn=device`

<span data-ttu-id="75c4f-245">A protocol gateway could use the same token for all devices simply setting the resource URI to `myhub.azure-devices.net/devices`.</span><span class="sxs-lookup"><span data-stu-id="75c4f-245">A protocol gateway could use the same token for all devices simply setting the resource URI to `myhub.azure-devices.net/devices`.</span></span>

### <a name="use-security-tokens-from-service-components"></a><span data-ttu-id="75c4f-246">Use security tokens from service components</span><span class="sxs-lookup"><span data-stu-id="75c4f-246">Use security tokens from service components</span></span>

<span data-ttu-id="75c4f-247">Service components can only generate security tokens using shared access policies granting the appropriate permissions as explained previously.</span><span class="sxs-lookup"><span data-stu-id="75c4f-247">Service components can only generate security tokens using shared access policies granting the appropriate permissions as explained previously.</span></span>

<span data-ttu-id="75c4f-248">Here are the service functions exposed on the endpoints:</span><span class="sxs-lookup"><span data-stu-id="75c4f-248">Here are the service functions exposed on the endpoints:</span></span>

| <span data-ttu-id="75c4f-249">Endpoint</span><span class="sxs-lookup"><span data-stu-id="75c4f-249">Endpoint</span></span> | <span data-ttu-id="75c4f-250">Functionality</span><span class="sxs-lookup"><span data-stu-id="75c4f-250">Functionality</span></span> |
| --- | --- |
| `{iot hub host name}/devices` |<span data-ttu-id="75c4f-251">Create, update, retrieve, and delete device identities.</span><span class="sxs-lookup"><span data-stu-id="75c4f-251">Create, update, retrieve, and delete device identities.</span></span> |
| `{iot hub host name}/messages/events` |<span data-ttu-id="75c4f-252">Receive device-to-cloud messages.</span><span class="sxs-lookup"><span data-stu-id="75c4f-252">Receive device-to-cloud messages.</span></span> |
| `{iot hub host name}/servicebound/feedback` |<span data-ttu-id="75c4f-253">Receive feedback for cloud-to-device messages.</span><span class="sxs-lookup"><span data-stu-id="75c4f-253">Receive feedback for cloud-to-device messages.</span></span> |
| `{iot hub host name}/devicebound` |<span data-ttu-id="75c4f-254">Send cloud-to-device messages.</span><span class="sxs-lookup"><span data-stu-id="75c4f-254">Send cloud-to-device messages.</span></span> |

<span data-ttu-id="75c4f-255">As an example, a service generating using the pre-created shared access policy called **registryRead** would create a token with the following parameters:</span><span class="sxs-lookup"><span data-stu-id="75c4f-255">As an example, a service generating using the pre-created shared access policy called **registryRead** would create a token with the following parameters:</span></span>

* <span data-ttu-id="75c4f-256">resource URI: `{IoT hub name}.azure-devices.net/devices`,</span><span class="sxs-lookup"><span data-stu-id="75c4f-256">resource URI: `{IoT hub name}.azure-devices.net/devices`,</span></span>
* <span data-ttu-id="75c4f-257">signing key: one of the keys of the `registryRead` policy,</span><span class="sxs-lookup"><span data-stu-id="75c4f-257">signing key: one of the keys of the `registryRead` policy,</span></span>
* <span data-ttu-id="75c4f-258">policy name: `registryRead`,</span><span class="sxs-lookup"><span data-stu-id="75c4f-258">policy name: `registryRead`,</span></span>
* <span data-ttu-id="75c4f-259">any expiration time.</span><span class="sxs-lookup"><span data-stu-id="75c4f-259">any expiration time.</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

<span data-ttu-id="75c4f-260">The result, which would grant access to read all device identities, would be:</span><span class="sxs-lookup"><span data-stu-id="75c4f-260">The result, which would grant access to read all device identities, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices&sig=JdyscqTpXdEJs49elIUCcohw2DlFDR3zfH5KqGJo4r4%3D&se=1456973447&skn=registryRead`

## <a name="supported-x509-certificates"></a><span data-ttu-id="75c4f-261">Supported X.509 certificates</span><span class="sxs-lookup"><span data-stu-id="75c4f-261">Supported X.509 certificates</span></span>

<span data-ttu-id="75c4f-262">You can use any X.509 certificate to authenticate a device with IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="75c4f-262">You can use any X.509 certificate to authenticate a device with IoT Hub.</span></span> <span data-ttu-id="75c4f-263">Certificates include:</span><span class="sxs-lookup"><span data-stu-id="75c4f-263">Certificates include:</span></span>

* <span data-ttu-id="75c4f-264">**An existing X.509 certificate**.</span><span class="sxs-lookup"><span data-stu-id="75c4f-264">**An existing X.509 certificate**.</span></span> <span data-ttu-id="75c4f-265">A device may already have an X.509 certificate associated with it.</span><span class="sxs-lookup"><span data-stu-id="75c4f-265">A device may already have an X.509 certificate associated with it.</span></span> <span data-ttu-id="75c4f-266">The device can use this certificate to authenticate with IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="75c4f-266">The device can use this certificate to authenticate with IoT Hub.</span></span>
* <span data-ttu-id="75c4f-267">**A self-generated and self-signed X-509 certificate**.</span><span class="sxs-lookup"><span data-stu-id="75c4f-267">**A self-generated and self-signed X-509 certificate**.</span></span> <span data-ttu-id="75c4f-268">A device manufacturer or in-house deployer can generate these certificates and store the corresponding private key (and certificate) on the device.</span><span class="sxs-lookup"><span data-stu-id="75c4f-268">A device manufacturer or in-house deployer can generate these certificates and store the corresponding private key (and certificate) on the device.</span></span> <span data-ttu-id="75c4f-269">You can use tools such as [OpenSSL][lnk-openssl] and [Windows SelfSignedCertificate][lnk-selfsigned] utility for this purpose.</span><span class="sxs-lookup"><span data-stu-id="75c4f-269">You can use tools such as [OpenSSL][lnk-openssl] and [Windows SelfSignedCertificate][lnk-selfsigned] utility for this purpose.</span></span>
* <span data-ttu-id="75c4f-270">**CA-signed X.509 certificate**.</span><span class="sxs-lookup"><span data-stu-id="75c4f-270">**CA-signed X.509 certificate**.</span></span> <span data-ttu-id="75c4f-271">You can also use an X.509 certificate generated and signed by a Certification Authority (CA) to identify a device and authenticate a device with IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="75c4f-271">You can also use an X.509 certificate generated and signed by a Certification Authority (CA) to identify a device and authenticate a device with IoT Hub.</span></span> <span data-ttu-id="75c4f-272">IoTHub only verifies that the thumbprint presented matches the configured thumbprint.</span><span class="sxs-lookup"><span data-stu-id="75c4f-272">IoTHub only verifies that the thumbprint presented matches the configured thumbprint.</span></span> <span data-ttu-id="75c4f-273">IotHub does not validate the certificate chain.</span><span class="sxs-lookup"><span data-stu-id="75c4f-273">IotHub does not validate the certificate chain.</span></span>

<span data-ttu-id="75c4f-274">A device may either use an X.509 certificate or a security token for authentication, but not both.</span><span class="sxs-lookup"><span data-stu-id="75c4f-274">A device may either use an X.509 certificate or a security token for authentication, but not both.</span></span>

### <a name="register-an-x509-certificate-for-a-device"></a><span data-ttu-id="75c4f-275">Register an X.509 certificate for a device</span><span class="sxs-lookup"><span data-stu-id="75c4f-275">Register an X.509 certificate for a device</span></span>

<span data-ttu-id="75c4f-276">The [Azure IoT Service SDK for C#][lnk-service-sdk] (version 1.0.8+) supports registering a device that uses an X.509 certificate for authentication.</span><span class="sxs-lookup"><span data-stu-id="75c4f-276">The [Azure IoT Service SDK for C#][lnk-service-sdk] (version 1.0.8+) supports registering a device that uses an X.509 certificate for authentication.</span></span> <span data-ttu-id="75c4f-277">Other APIs such as import/export of devices also support X.509 certificates.</span><span class="sxs-lookup"><span data-stu-id="75c4f-277">Other APIs such as import/export of devices also support X.509 certificates.</span></span>

### <a name="c-support"></a><span data-ttu-id="75c4f-278">C\# Support</span><span class="sxs-lookup"><span data-stu-id="75c4f-278">C\# Support</span></span>

<span data-ttu-id="75c4f-279">The **RegistryManager** class provides a programmatic way to register a device.</span><span class="sxs-lookup"><span data-stu-id="75c4f-279">The **RegistryManager** class provides a programmatic way to register a device.</span></span> <span data-ttu-id="75c4f-280">In particular, the **AddDeviceAsync** and **UpdateDeviceAsync** methods enable you to register and update a device in the IoT Hub identity registry.</span><span class="sxs-lookup"><span data-stu-id="75c4f-280">In particular, the **AddDeviceAsync** and **UpdateDeviceAsync** methods enable you to register and update a device in the IoT Hub identity registry.</span></span> <span data-ttu-id="75c4f-281">These two methods take a **Device** instance as input.</span><span class="sxs-lookup"><span data-stu-id="75c4f-281">These two methods take a **Device** instance as input.</span></span> <span data-ttu-id="75c4f-282">The **Device** class includes an **Authentication** property that allows you to specify primary and secondary X.509 certificate thumbprints.</span><span class="sxs-lookup"><span data-stu-id="75c4f-282">The **Device** class includes an **Authentication** property that allows you to specify primary and secondary X.509 certificate thumbprints.</span></span> <span data-ttu-id="75c4f-283">The thumbprint represents a SHA-1 hash of the X.509 certificate (stored using binary DER encoding).</span><span class="sxs-lookup"><span data-stu-id="75c4f-283">The thumbprint represents a SHA-1 hash of the X.509 certificate (stored using binary DER encoding).</span></span> <span data-ttu-id="75c4f-284">You have the option of specifying a primary thumbprint or a secondary thumbprint or both.</span><span class="sxs-lookup"><span data-stu-id="75c4f-284">You have the option of specifying a primary thumbprint or a secondary thumbprint or both.</span></span> <span data-ttu-id="75c4f-285">Primary and secondary thumbprints are supported to handle certificate rollover scenarios.</span><span class="sxs-lookup"><span data-stu-id="75c4f-285">Primary and secondary thumbprints are supported to handle certificate rollover scenarios.</span></span>

> [!NOTE]
> <span data-ttu-id="75c4f-286">IoT Hub does not require or store the entire X.509 certificate, only the thumbprint.</span><span class="sxs-lookup"><span data-stu-id="75c4f-286">IoT Hub does not require or store the entire X.509 certificate, only the thumbprint.</span></span>

<span data-ttu-id="75c4f-287">Here is a sample C\# code snippet to register a device using an X.509 certificate:</span><span class="sxs-lookup"><span data-stu-id="75c4f-287">Here is a sample C\# code snippet to register a device using an X.509 certificate:</span></span>

```csharp
var device = new Device(deviceId)
{
  Authentication = new AuthenticationMechanism()
  {
    X509Thumbprint = new X509Thumbprint()
    {
      PrimaryThumbprint = "921BC9694ADEB8929D4F7FE4B9A3A6DE58B0790B"
    }
  }
};
RegistryManager registryManager = RegistryManager.CreateFromConnectionString(deviceGatewayConnectionString);
await registryManager.AddDeviceAsync(device);
```

### <a name="use-an-x509-certificate-during-run-time-operations"></a><span data-ttu-id="75c4f-288">Use an X.509 certificate during run-time operations</span><span class="sxs-lookup"><span data-stu-id="75c4f-288">Use an X.509 certificate during run-time operations</span></span>

<span data-ttu-id="75c4f-289">The [Azure IoT device SDK for .NET][lnk-client-sdk] (version 1.0.11+) supports the use of X.509 certificates.</span><span class="sxs-lookup"><span data-stu-id="75c4f-289">The [Azure IoT device SDK for .NET][lnk-client-sdk] (version 1.0.11+) supports the use of X.509 certificates.</span></span>

### <a name="c-support"></a><span data-ttu-id="75c4f-290">C\# Support</span><span class="sxs-lookup"><span data-stu-id="75c4f-290">C\# Support</span></span>

<span data-ttu-id="75c4f-291">The class **DeviceAuthenticationWithX509Certificate** supports the creation of **DeviceClient** instances using an X.509 certificate.</span><span class="sxs-lookup"><span data-stu-id="75c4f-291">The class **DeviceAuthenticationWithX509Certificate** supports the creation of **DeviceClient** instances using an X.509 certificate.</span></span> <span data-ttu-id="75c4f-292">The X.509 certificate must be in the PFX (also called PKCS #12) format that includes the private key.</span><span class="sxs-lookup"><span data-stu-id="75c4f-292">The X.509 certificate must be in the PFX (also called PKCS #12) format that includes the private key.</span></span>

<span data-ttu-id="75c4f-293">Here is a sample code snippet:</span><span class="sxs-lookup"><span data-stu-id="75c4f-293">Here is a sample code snippet:</span></span>

```csharp
var authMethod = new DeviceAuthenticationWithX509Certificate("<device id>", x509Certificate);

var deviceClient = DeviceClient.Create("<IotHub DNS HostName>", authMethod);
```

## <a name="custom-device-authentication"></a><span data-ttu-id="75c4f-294">Custom device authentication</span><span class="sxs-lookup"><span data-stu-id="75c4f-294">Custom device authentication</span></span>

<span data-ttu-id="75c4f-295">You can use the IoT Hub [identity registry][lnk-identity-registry] to configure per-device security credentials and access control using [tokens][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="75c4f-295">You can use the IoT Hub [identity registry][lnk-identity-registry] to configure per-device security credentials and access control using [tokens][lnk-sas-tokens].</span></span> <span data-ttu-id="75c4f-296">However, if an IoT solution already has a significant investment in a custom identity registry and/or authentication scheme, you can integrate this existing infrastructure with IoT Hub by creating a *token service*.</span><span class="sxs-lookup"><span data-stu-id="75c4f-296">However, if an IoT solution already has a significant investment in a custom identity registry and/or authentication scheme, you can integrate this existing infrastructure with IoT Hub by creating a *token service*.</span></span> <span data-ttu-id="75c4f-297">In this way, you can use other IoT features in your solution.</span><span class="sxs-lookup"><span data-stu-id="75c4f-297">In this way, you can use other IoT features in your solution.</span></span>

<span data-ttu-id="75c4f-298">A token service is a custom cloud service.</span><span class="sxs-lookup"><span data-stu-id="75c4f-298">A token service is a custom cloud service.</span></span> <span data-ttu-id="75c4f-299">It uses an IoT Hub *shared access policy* with **DeviceConnect** permissions to create *device-scoped* tokens.</span><span class="sxs-lookup"><span data-stu-id="75c4f-299">It uses an IoT Hub *shared access policy* with **DeviceConnect** permissions to create *device-scoped* tokens.</span></span> <span data-ttu-id="75c4f-300">These tokens enable a device to connect to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="75c4f-300">These tokens enable a device to connect to your IoT hub.</span></span>

![Steps of the token service pattern][img-tokenservice]

<span data-ttu-id="75c4f-302">Here are the main steps of the token service pattern:</span><span class="sxs-lookup"><span data-stu-id="75c4f-302">Here are the main steps of the token service pattern:</span></span>

1. <span data-ttu-id="75c4f-303">Create an IoT Hub shared access policy with **DeviceConnect** permissions for your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="75c4f-303">Create an IoT Hub shared access policy with **DeviceConnect** permissions for your IoT hub.</span></span> <span data-ttu-id="75c4f-304">You can create this policy in the [Azure portal][lnk-management-portal] or programmatically.</span><span class="sxs-lookup"><span data-stu-id="75c4f-304">You can create this policy in the [Azure portal][lnk-management-portal] or programmatically.</span></span> <span data-ttu-id="75c4f-305">The token service uses this policy to sign the tokens it creates.</span><span class="sxs-lookup"><span data-stu-id="75c4f-305">The token service uses this policy to sign the tokens it creates.</span></span>
1. <span data-ttu-id="75c4f-306">When a device needs to access your IoT hub, it requests a signed token from your token service.</span><span class="sxs-lookup"><span data-stu-id="75c4f-306">When a device needs to access your IoT hub, it requests a signed token from your token service.</span></span> <span data-ttu-id="75c4f-307">The device can authenticate with your custom identity registry/authentication scheme to determine the device identity that the token service uses to create the token.</span><span class="sxs-lookup"><span data-stu-id="75c4f-307">The device can authenticate with your custom identity registry/authentication scheme to determine the device identity that the token service uses to create the token.</span></span>
1. <span data-ttu-id="75c4f-308">The token service returns a token.</span><span class="sxs-lookup"><span data-stu-id="75c4f-308">The token service returns a token.</span></span> <span data-ttu-id="75c4f-309">The token is created by using `/devices/{deviceId}` as `resourceURI`, with `deviceId` as the device being authenticated.</span><span class="sxs-lookup"><span data-stu-id="75c4f-309">The token is created by using `/devices/{deviceId}` as `resourceURI`, with `deviceId` as the device being authenticated.</span></span> <span data-ttu-id="75c4f-310">The token service uses the shared access policy to construct the token.</span><span class="sxs-lookup"><span data-stu-id="75c4f-310">The token service uses the shared access policy to construct the token.</span></span>
1. <span data-ttu-id="75c4f-311">The device uses the token directly with the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="75c4f-311">The device uses the token directly with the IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="75c4f-312">You can use the .NET class [SharedAccessSignatureBuilder][lnk-dotnet-sas] or the Java class [IotHubServiceSasToken][lnk-java-sas] to create a token in your token service.</span><span class="sxs-lookup"><span data-stu-id="75c4f-312">You can use the .NET class [SharedAccessSignatureBuilder][lnk-dotnet-sas] or the Java class [IotHubServiceSasToken][lnk-java-sas] to create a token in your token service.</span></span>

<span data-ttu-id="75c4f-313">The token service can set the token expiration as desired.</span><span class="sxs-lookup"><span data-stu-id="75c4f-313">The token service can set the token expiration as desired.</span></span> <span data-ttu-id="75c4f-314">When the token expires, the IoT hub severs the device connection.</span><span class="sxs-lookup"><span data-stu-id="75c4f-314">When the token expires, the IoT hub severs the device connection.</span></span> <span data-ttu-id="75c4f-315">Then, the device must request a new token from the token service.</span><span class="sxs-lookup"><span data-stu-id="75c4f-315">Then, the device must request a new token from the token service.</span></span> <span data-ttu-id="75c4f-316">A short expiry time increases the load on both the device and the token service.</span><span class="sxs-lookup"><span data-stu-id="75c4f-316">A short expiry time increases the load on both the device and the token service.</span></span>

<span data-ttu-id="75c4f-317">For a device to connect to your hub, you must still add it to the IoT Hub identity registry — even though the device is using a token and not a device key to connect.</span><span class="sxs-lookup"><span data-stu-id="75c4f-317">For a device to connect to your hub, you must still add it to the IoT Hub identity registry — even though the device is using a token and not a device key to connect.</span></span> <span data-ttu-id="75c4f-318">Therefore, you can continue to use per-device access control by enabling or disabling device identities in the [IoT Hub identity registry][lnk-identity-registry] when the device authenticates with a token.</span><span class="sxs-lookup"><span data-stu-id="75c4f-318">Therefore, you can continue to use per-device access control by enabling or disabling device identities in the [IoT Hub identity registry][lnk-identity-registry] when the device authenticates with a token.</span></span> <span data-ttu-id="75c4f-319">This approach mitigates the risks of using tokens with long expiry times.</span><span class="sxs-lookup"><span data-stu-id="75c4f-319">This approach mitigates the risks of using tokens with long expiry times.</span></span>

### <a name="comparison-with-a-custom-gateway"></a><span data-ttu-id="75c4f-320">Comparison with a custom gateway</span><span class="sxs-lookup"><span data-stu-id="75c4f-320">Comparison with a custom gateway</span></span>

<span data-ttu-id="75c4f-321">The token service pattern is the recommended way to implement a custom identity registry/authentication scheme with IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="75c4f-321">The token service pattern is the recommended way to implement a custom identity registry/authentication scheme with IoT Hub.</span></span> <span data-ttu-id="75c4f-322">It is recommended because IoT Hub continues to handle most of the solution traffic.</span><span class="sxs-lookup"><span data-stu-id="75c4f-322">It is recommended because IoT Hub continues to handle most of the solution traffic.</span></span> <span data-ttu-id="75c4f-323">However, there are cases where the custom authentication scheme is so intertwined with the protocol that a service processing all the traffic (*custom gateway*) is required.</span><span class="sxs-lookup"><span data-stu-id="75c4f-323">However, there are cases where the custom authentication scheme is so intertwined with the protocol that a service processing all the traffic (*custom gateway*) is required.</span></span> <span data-ttu-id="75c4f-324">An example of such a scenario is using[Transport Layer Security (TLS) and pre-shared keys (PSKs)][lnk-tls-psk].</span><span class="sxs-lookup"><span data-stu-id="75c4f-324">An example of such a scenario is using[Transport Layer Security (TLS) and pre-shared keys (PSKs)][lnk-tls-psk].</span></span> <span data-ttu-id="75c4f-325">For more information, see the [protocol gateway][lnk-protocols] topic.</span><span class="sxs-lookup"><span data-stu-id="75c4f-325">For more information, see the [protocol gateway][lnk-protocols] topic.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="75c4f-326">Reference topics:</span><span class="sxs-lookup"><span data-stu-id="75c4f-326">Reference topics:</span></span>

<span data-ttu-id="75c4f-327">The following reference topics provide you with more information about controlling access to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="75c4f-327">The following reference topics provide you with more information about controlling access to your IoT hub.</span></span>

## <a name="iot-hub-permissions"></a><span data-ttu-id="75c4f-328">IoT Hub permissions</span><span class="sxs-lookup"><span data-stu-id="75c4f-328">IoT Hub permissions</span></span>

<span data-ttu-id="75c4f-329">The following table lists the permissions you can use to control access to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="75c4f-329">The following table lists the permissions you can use to control access to your IoT hub.</span></span>

| <span data-ttu-id="75c4f-330">Permission</span><span class="sxs-lookup"><span data-stu-id="75c4f-330">Permission</span></span> | <span data-ttu-id="75c4f-331">Notes</span><span class="sxs-lookup"><span data-stu-id="75c4f-331">Notes</span></span> |
| --- | --- |
| <span data-ttu-id="75c4f-332">**RegistryRead**</span><span class="sxs-lookup"><span data-stu-id="75c4f-332">**RegistryRead**</span></span> |<span data-ttu-id="75c4f-333">Grants read access to the identity registry.</span><span class="sxs-lookup"><span data-stu-id="75c4f-333">Grants read access to the identity registry.</span></span> <span data-ttu-id="75c4f-334">For more information, see [Identity registry][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="75c4f-334">For more information, see [Identity registry][lnk-identity-registry].</span></span> <br/><span data-ttu-id="75c4f-335">This permission is used by back-end cloud services.</span><span class="sxs-lookup"><span data-stu-id="75c4f-335">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="75c4f-336">**RegistryReadWrite**</span><span class="sxs-lookup"><span data-stu-id="75c4f-336">**RegistryReadWrite**</span></span> |<span data-ttu-id="75c4f-337">Grants read and write access to the identity registry.</span><span class="sxs-lookup"><span data-stu-id="75c4f-337">Grants read and write access to the identity registry.</span></span> <span data-ttu-id="75c4f-338">For more information, see [Identity registry][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="75c4f-338">For more information, see [Identity registry][lnk-identity-registry].</span></span> <br/><span data-ttu-id="75c4f-339">This permission is used by back-end cloud services.</span><span class="sxs-lookup"><span data-stu-id="75c4f-339">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="75c4f-340">**ServiceConnect**</span><span class="sxs-lookup"><span data-stu-id="75c4f-340">**ServiceConnect**</span></span> |<span data-ttu-id="75c4f-341">Grants access to cloud service-facing communication and monitoring endpoints.</span><span class="sxs-lookup"><span data-stu-id="75c4f-341">Grants access to cloud service-facing communication and monitoring endpoints.</span></span> <br/><span data-ttu-id="75c4f-342">Grants permission to receive device-to-cloud messages, send cloud-to-device messages, and retrieve the corresponding delivery acknowledgments.</span><span class="sxs-lookup"><span data-stu-id="75c4f-342">Grants permission to receive device-to-cloud messages, send cloud-to-device messages, and retrieve the corresponding delivery acknowledgments.</span></span> <br/><span data-ttu-id="75c4f-343">Grants permission to retrieve delivery acknowledgements for file uploads.</span><span class="sxs-lookup"><span data-stu-id="75c4f-343">Grants permission to retrieve delivery acknowledgements for file uploads.</span></span> <br/><span data-ttu-id="75c4f-344">Grants permission to access device twins to update tags and desired properties, retrieve reported properties, and run queries.</span><span class="sxs-lookup"><span data-stu-id="75c4f-344">Grants permission to access device twins to update tags and desired properties, retrieve reported properties, and run queries.</span></span> <br/><span data-ttu-id="75c4f-345">This permission is used by back-end cloud services.</span><span class="sxs-lookup"><span data-stu-id="75c4f-345">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="75c4f-346">**DeviceConnect**</span><span class="sxs-lookup"><span data-stu-id="75c4f-346">**DeviceConnect**</span></span> |<span data-ttu-id="75c4f-347">Grants access to device-facing endpoints.</span><span class="sxs-lookup"><span data-stu-id="75c4f-347">Grants access to device-facing endpoints.</span></span> <br/><span data-ttu-id="75c4f-348">Grants permission to send device-to-cloud messages and receive cloud-to-device messages.</span><span class="sxs-lookup"><span data-stu-id="75c4f-348">Grants permission to send device-to-cloud messages and receive cloud-to-device messages.</span></span> <br/><span data-ttu-id="75c4f-349">Grants permission to perform file upload from a device.</span><span class="sxs-lookup"><span data-stu-id="75c4f-349">Grants permission to perform file upload from a device.</span></span> <br/><span data-ttu-id="75c4f-350">Grants permission to receive device twin desired property notifications and update device twin reported properties.</span><span class="sxs-lookup"><span data-stu-id="75c4f-350">Grants permission to receive device twin desired property notifications and update device twin reported properties.</span></span> <br/><span data-ttu-id="75c4f-351">Grants permission to perform file uploads.</span><span class="sxs-lookup"><span data-stu-id="75c4f-351">Grants permission to perform file uploads.</span></span> <br/><span data-ttu-id="75c4f-352">This permission is used by devices.</span><span class="sxs-lookup"><span data-stu-id="75c4f-352">This permission is used by devices.</span></span> |

## <a name="additional-reference-material"></a><span data-ttu-id="75c4f-353">Additional reference material</span><span class="sxs-lookup"><span data-stu-id="75c4f-353">Additional reference material</span></span>

<span data-ttu-id="75c4f-354">Other reference topics in the IoT Hub developer guide include:</span><span class="sxs-lookup"><span data-stu-id="75c4f-354">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="75c4f-355">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span><span class="sxs-lookup"><span data-stu-id="75c4f-355">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="75c4f-356">[Throttling and quotas][lnk-quotas] describes the quotas that apply to the IoT Hub service and the throttling behavior to expect when you use the service.</span><span class="sxs-lookup"><span data-stu-id="75c4f-356">[Throttling and quotas][lnk-quotas] describes the quotas that apply to the IoT Hub service and the throttling behavior to expect when you use the service.</span></span>
* <span data-ttu-id="75c4f-357">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="75c4f-357">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="75c4f-358">[IoT Hub query language for device twins and jobs][lnk-query] describes the IoT Hub query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span><span class="sxs-lookup"><span data-stu-id="75c4f-358">[IoT Hub query language for device twins and jobs][lnk-query] describes the IoT Hub query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="75c4f-359">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span><span class="sxs-lookup"><span data-stu-id="75c4f-359">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="75c4f-360">Next steps</span><span class="sxs-lookup"><span data-stu-id="75c4f-360">Next steps</span></span>

<span data-ttu-id="75c4f-361">Now you have learned how to control access IoT Hub, you may be interested in the following IoT Hub developer guide topics:</span><span class="sxs-lookup"><span data-stu-id="75c4f-361">Now you have learned how to control access IoT Hub, you may be interested in the following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="75c4f-362">[Use device twins to synchronize state and configurations][lnk-devguide-device-twins]</span><span class="sxs-lookup"><span data-stu-id="75c4f-362">[Use device twins to synchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="75c4f-363">[Invoke a direct method on a device][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="75c4f-363">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="75c4f-364">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="75c4f-364">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="75c4f-365">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorials:</span><span class="sxs-lookup"><span data-stu-id="75c4f-365">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorials:</span></span>

* <span data-ttu-id="75c4f-366">[Get started with Azure IoT Hub][lnk-getstarted-tutorial]</span><span class="sxs-lookup"><span data-stu-id="75c4f-366">[Get started with Azure IoT Hub][lnk-getstarted-tutorial]</span></span>
* <span data-ttu-id="75c4f-367">[How to send cloud-to-device messages with IoT Hub][lnk-c2d-tutorial]</span><span class="sxs-lookup"><span data-stu-id="75c4f-367">[How to send cloud-to-device messages with IoT Hub][lnk-c2d-tutorial]</span></span>
* <span data-ttu-id="75c4f-368">[How to process IoT Hub device-to-cloud messages][lnk-d2c-tutorial]</span><span class="sxs-lookup"><span data-stu-id="75c4f-368">[How to process IoT Hub device-to-cloud messages][lnk-d2c-tutorial]</span></span>

<!-- links and images -->

[img-tokenservice]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-devguide-security/tokenservice.png
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-openssl]: https://www.openssl.org/
[lnk-selfsigned]: https://technet.microsoft.com/library/hh848633

[lnk-resource-provider-apis]: https://msdn.microsoft.com/library/mt548492.aspx
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
[lnk-custom-auth]: iot-hub-devguide-security.md#custom-device-authentication
[lnk-x509]: iot-hub-devguide-security.md#supported-x509-certificates
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-service-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/service
[lnk-client-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/azure/iothub-explorer

[lnk-getstarted-tutorial]: iot-hub-csharp-csharp-getstarted.md
[lnk-c2d-tutorial]: iot-hub-csharp-csharp-c2d.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

