---
title: Security endpoints in IoT Device Provisioning Service | Microsoft Docs
description: Concepts - how to control access to IoT Device Provisioning Service for backend apps. Includes information about security tokens.
author: wesmc7777
manager: timlt
ms.service: iot-dps
services: iot-dps
ms.topic: conceptual
ms.date: 09/28/2017
ms.author: wesmc
ms.openlocfilehash: e476ca498e4dc1b36d18927beddc812d6d803120
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968330"
---
# <a name="control-access-to-azure-iot-hub-device-provisioning-service"></a><span data-ttu-id="d09e4-104">Control access to Azure IoT Hub Device Provisioning Service</span><span class="sxs-lookup"><span data-stu-id="d09e4-104">Control access to Azure IoT Hub Device Provisioning Service</span></span>

<span data-ttu-id="d09e4-105">This article describes the options for securing your IoT Device Provisioning service.</span><span class="sxs-lookup"><span data-stu-id="d09e4-105">This article describes the options for securing your IoT Device Provisioning service.</span></span> <span data-ttu-id="d09e4-106">The provisioning service uses *permissions* to grant access to each endpoint.</span><span class="sxs-lookup"><span data-stu-id="d09e4-106">The provisioning service uses *permissions* to grant access to each endpoint.</span></span> <span data-ttu-id="d09e4-107">Permissions limit the access to a service instance based on functionality.</span><span class="sxs-lookup"><span data-stu-id="d09e4-107">Permissions limit the access to a service instance based on functionality.</span></span>

<span data-ttu-id="d09e4-108">This article describes:</span><span class="sxs-lookup"><span data-stu-id="d09e4-108">This article describes:</span></span>

* <span data-ttu-id="d09e4-109">The different permissions that you can grant to a backend app to access your provisioning service.</span><span class="sxs-lookup"><span data-stu-id="d09e4-109">The different permissions that you can grant to a backend app to access your provisioning service.</span></span>
* <span data-ttu-id="d09e4-110">The authentication process and the tokens it uses to verify permissions.</span><span class="sxs-lookup"><span data-stu-id="d09e4-110">The authentication process and the tokens it uses to verify permissions.</span></span>

### <a name="when-to-use"></a><span data-ttu-id="d09e4-111">When to use</span><span class="sxs-lookup"><span data-stu-id="d09e4-111">When to use</span></span>

<span data-ttu-id="d09e4-112">You must have appropriate permissions to access any of the provisioning service endpoints.</span><span class="sxs-lookup"><span data-stu-id="d09e4-112">You must have appropriate permissions to access any of the provisioning service endpoints.</span></span> <span data-ttu-id="d09e4-113">For example, a backend app must include a token containing security credentials along with every message it sends to the service.</span><span class="sxs-lookup"><span data-stu-id="d09e4-113">For example, a backend app must include a token containing security credentials along with every message it sends to the service.</span></span>

## <a name="access-control-and-permissions"></a><span data-ttu-id="d09e4-114">Access control and permissions</span><span class="sxs-lookup"><span data-stu-id="d09e4-114">Access control and permissions</span></span>

<span data-ttu-id="d09e4-115">You can grant [permissions](#device-provisioning-service-permissions) in the following ways:</span><span class="sxs-lookup"><span data-stu-id="d09e4-115">You can grant [permissions](#device-provisioning-service-permissions) in the following ways:</span></span>

* <span data-ttu-id="d09e4-116">**Shared access authorization policies**.</span><span class="sxs-lookup"><span data-stu-id="d09e4-116">**Shared access authorization policies**.</span></span> <span data-ttu-id="d09e4-117">Shared access policies can grant any combination of [permissions](#device-provisioning-service-permissions).</span><span class="sxs-lookup"><span data-stu-id="d09e4-117">Shared access policies can grant any combination of [permissions](#device-provisioning-service-permissions).</span></span> <span data-ttu-id="d09e4-118">You can define policies in the [Azure portal][lnk-management-portal], or programmatically by using the [Device Provisioning Service REST APIs][lnk-resource-provider-apis].</span><span class="sxs-lookup"><span data-stu-id="d09e4-118">You can define policies in the [Azure portal][lnk-management-portal], or programmatically by using the [Device Provisioning Service REST APIs][lnk-resource-provider-apis].</span></span> <span data-ttu-id="d09e4-119">A newly created provisioning service has the following default policy:</span><span class="sxs-lookup"><span data-stu-id="d09e4-119">A newly created provisioning service has the following default policy:</span></span>

* <span data-ttu-id="d09e4-120">**provisioningserviceowner**: Policy with all permissions.</span><span class="sxs-lookup"><span data-stu-id="d09e4-120">**provisioningserviceowner**: Policy with all permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="d09e4-121">See [permissions](#device-provisioning-service-permissions) for detailed information.</span><span class="sxs-lookup"><span data-stu-id="d09e4-121">See [permissions](#device-provisioning-service-permissions) for detailed information.</span></span>

## <a name="authentication"></a><span data-ttu-id="d09e4-122">Authentication</span><span class="sxs-lookup"><span data-stu-id="d09e4-122">Authentication</span></span>

<span data-ttu-id="d09e4-123">Azure IoT Hub Device Provisioning Service grants access to endpoints by verifying a token against the shared access policies.</span><span class="sxs-lookup"><span data-stu-id="d09e4-123">Azure IoT Hub Device Provisioning Service grants access to endpoints by verifying a token against the shared access policies.</span></span> <span data-ttu-id="d09e4-124">Security credentials, such as symmetric keys, are never sent over the wire.</span><span class="sxs-lookup"><span data-stu-id="d09e4-124">Security credentials, such as symmetric keys, are never sent over the wire.</span></span>

> [!NOTE]
> <span data-ttu-id="d09e4-125">The Device Provisioning Service resource provider is secured through your Azure subscription, as are all providers in the [Azure Resource Manager][lnk-azure-resource-manager].</span><span class="sxs-lookup"><span data-stu-id="d09e4-125">The Device Provisioning Service resource provider is secured through your Azure subscription, as are all providers in the [Azure Resource Manager][lnk-azure-resource-manager].</span></span>

<span data-ttu-id="d09e4-126">For more information about how to construct and use security tokens, see the next section.</span><span class="sxs-lookup"><span data-stu-id="d09e4-126">For more information about how to construct and use security tokens, see the next section.</span></span>

<span data-ttu-id="d09e4-127">HTTP is the only supported protocol, and it implements authentication by including a valid token in the **Authorization** request header.</span><span class="sxs-lookup"><span data-stu-id="d09e4-127">HTTP is the only supported protocol, and it implements authentication by including a valid token in the **Authorization** request header.</span></span>

#### <a name="example"></a><span data-ttu-id="d09e4-128">Example</span><span class="sxs-lookup"><span data-stu-id="d09e4-128">Example</span></span>
```csharp
SharedAccessSignature sr = 
   mydps.azure-devices-provisioning.net&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501&skn=provisioningserviceowner`\
```

> [!NOTE]
> <span data-ttu-id="d09e4-129">The [Azure IoT Device Provisioning Service SDKs][lnk-sdks] automatically generate tokens when connecting to the service.</span><span class="sxs-lookup"><span data-stu-id="d09e4-129">The [Azure IoT Device Provisioning Service SDKs][lnk-sdks] automatically generate tokens when connecting to the service.</span></span>

## <a name="security-tokens"></a><span data-ttu-id="d09e4-130">Security tokens</span><span class="sxs-lookup"><span data-stu-id="d09e4-130">Security tokens</span></span>

<span data-ttu-id="d09e4-131">The Device Provisioning Service uses security tokens to authenticate services to avoid sending keys on the wire.</span><span class="sxs-lookup"><span data-stu-id="d09e4-131">The Device Provisioning Service uses security tokens to authenticate services to avoid sending keys on the wire.</span></span> <span data-ttu-id="d09e4-132">Additionally, security tokens are limited in time validity and scope.</span><span class="sxs-lookup"><span data-stu-id="d09e4-132">Additionally, security tokens are limited in time validity and scope.</span></span> <span data-ttu-id="d09e4-133">[Azure IoT Device Provisioning Service SDKs][lnk-sdks] automatically generate tokens without requiring any special configuration.</span><span class="sxs-lookup"><span data-stu-id="d09e4-133">[Azure IoT Device Provisioning Service SDKs][lnk-sdks] automatically generate tokens without requiring any special configuration.</span></span> <span data-ttu-id="d09e4-134">Some scenarios do require you to generate and use security tokens directly.</span><span class="sxs-lookup"><span data-stu-id="d09e4-134">Some scenarios do require you to generate and use security tokens directly.</span></span> <span data-ttu-id="d09e4-135">Such scenarios include the direct use of the HTTP surface.</span><span class="sxs-lookup"><span data-stu-id="d09e4-135">Such scenarios include the direct use of the HTTP surface.</span></span>

### <a name="security-token-structure"></a><span data-ttu-id="d09e4-136">Security token structure</span><span class="sxs-lookup"><span data-stu-id="d09e4-136">Security token structure</span></span>

<span data-ttu-id="d09e4-137">You use security tokens to grant time-bounded access for services to specific functionality in IoT Device Provisioning Service.</span><span class="sxs-lookup"><span data-stu-id="d09e4-137">You use security tokens to grant time-bounded access for services to specific functionality in IoT Device Provisioning Service.</span></span> <span data-ttu-id="d09e4-138">To get authorization to connect to the provisioning service, services must send security tokens signed with either a shared access or symmetric key.</span><span class="sxs-lookup"><span data-stu-id="d09e4-138">To get authorization to connect to the provisioning service, services must send security tokens signed with either a shared access or symmetric key.</span></span>

<span data-ttu-id="d09e4-139">A token signed with a shared access key grants access to all the functionality associated with the shared access policy permissions.</span><span class="sxs-lookup"><span data-stu-id="d09e4-139">A token signed with a shared access key grants access to all the functionality associated with the shared access policy permissions.</span></span> 

<span data-ttu-id="d09e4-140">The security token has the following format:</span><span class="sxs-lookup"><span data-stu-id="d09e4-140">The security token has the following format:</span></span>

`SharedAccessSignature sig={signature}&se={expiry}&skn={policyName}&sr={URL-encoded-resourceURI}`

<span data-ttu-id="d09e4-141">Here are the expected values:</span><span class="sxs-lookup"><span data-stu-id="d09e4-141">Here are the expected values:</span></span>

| <span data-ttu-id="d09e4-142">Value</span><span class="sxs-lookup"><span data-stu-id="d09e4-142">Value</span></span> | <span data-ttu-id="d09e4-143">Description</span><span class="sxs-lookup"><span data-stu-id="d09e4-143">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d09e4-144">{signature}</span><span class="sxs-lookup"><span data-stu-id="d09e4-144">{signature}</span></span> |<span data-ttu-id="d09e4-145">An HMAC-SHA256 signature string of the form: `{URL-encoded-resourceURI} + "\n" + expiry`.</span><span class="sxs-lookup"><span data-stu-id="d09e4-145">An HMAC-SHA256 signature string of the form: `{URL-encoded-resourceURI} + "\n" + expiry`.</span></span> <span data-ttu-id="d09e4-146">**Important**: The key is decoded from base64 and used as key to perform the HMAC-SHA256 computation.</span><span class="sxs-lookup"><span data-stu-id="d09e4-146">**Important**: The key is decoded from base64 and used as key to perform the HMAC-SHA256 computation.</span></span>|
| <span data-ttu-id="d09e4-147">{expiry}</span><span class="sxs-lookup"><span data-stu-id="d09e4-147">{expiry}</span></span> |<span data-ttu-id="d09e4-148">UTF8 strings for number of seconds since the epoch 00:00:00 UTC on 1 January 1970.</span><span class="sxs-lookup"><span data-stu-id="d09e4-148">UTF8 strings for number of seconds since the epoch 00:00:00 UTC on 1 January 1970.</span></span> |
| <span data-ttu-id="d09e4-149">{URL-encoded-resourceURI}</span><span class="sxs-lookup"><span data-stu-id="d09e4-149">{URL-encoded-resourceURI}</span></span> | <span data-ttu-id="d09e4-150">Lower case URL-encoding of the lower case resource URI.</span><span class="sxs-lookup"><span data-stu-id="d09e4-150">Lower case URL-encoding of the lower case resource URI.</span></span> <span data-ttu-id="d09e4-151">URI prefix (by segment) of the endpoints that can be accessed with this token, starting with host name of the IoT Device Provisioning Service (no protocol).</span><span class="sxs-lookup"><span data-stu-id="d09e4-151">URI prefix (by segment) of the endpoints that can be accessed with this token, starting with host name of the IoT Device Provisioning Service (no protocol).</span></span> <span data-ttu-id="d09e4-152">For example, `mydps.azure-devices-provisioning.net`.</span><span class="sxs-lookup"><span data-stu-id="d09e4-152">For example, `mydps.azure-devices-provisioning.net`.</span></span> |
| <span data-ttu-id="d09e4-153">{policyName}</span><span class="sxs-lookup"><span data-stu-id="d09e4-153">{policyName}</span></span> |<span data-ttu-id="d09e4-154">The name of the shared access policy to which this token refers.</span><span class="sxs-lookup"><span data-stu-id="d09e4-154">The name of the shared access policy to which this token refers.</span></span> |

<span data-ttu-id="d09e4-155">**Note on prefix**: The URI prefix is computed by segment and not by character.</span><span class="sxs-lookup"><span data-stu-id="d09e4-155">**Note on prefix**: The URI prefix is computed by segment and not by character.</span></span> <span data-ttu-id="d09e4-156">For example `/a/b` is a prefix for `/a/b/c` but not for `/a/bc`.</span><span class="sxs-lookup"><span data-stu-id="d09e4-156">For example `/a/b` is a prefix for `/a/b/c` but not for `/a/bc`.</span></span>

<span data-ttu-id="d09e4-157">The following Node.js snippet shows a function called **generateSasToken** that computes the token from the inputs `resourceUri, signingKey, policyName, expiresInMins`.</span><span class="sxs-lookup"><span data-stu-id="d09e4-157">The following Node.js snippet shows a function called **generateSasToken** that computes the token from the inputs `resourceUri, signingKey, policyName, expiresInMins`.</span></span> <span data-ttu-id="d09e4-158">The next sections detail how to initialize the different inputs for the different token use cases.</span><span class="sxs-lookup"><span data-stu-id="d09e4-158">The next sections detail how to initialize the different inputs for the different token use cases.</span></span>

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

    // Construct authorization string
    var token = "SharedAccessSignature sr=" + resourceUri + "&sig="
    + base64UriEncoded + "&se=" + expires + "&skn="+ policyName;
    return token;
};
```

<span data-ttu-id="d09e4-159">As a comparison, the equivalent Python code to generate a security token is:</span><span class="sxs-lookup"><span data-stu-id="d09e4-159">As a comparison, the equivalent Python code to generate a security token is:</span></span>

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
        'se' : str(int(ttl)),
        'skn' : policy_name
    }

    return 'SharedAccessSignature ' + urlencode(rawtoken)
```

> [!NOTE]
> <span data-ttu-id="d09e4-160">Since the time validity of the token is validated on IoT Device Provisioning Service machines, the drift on the clock of the machine that generates the token must be minimal.</span><span class="sxs-lookup"><span data-stu-id="d09e4-160">Since the time validity of the token is validated on IoT Device Provisioning Service machines, the drift on the clock of the machine that generates the token must be minimal.</span></span>

### <a name="use-security-tokens-from-service-components"></a><span data-ttu-id="d09e4-161">Use security tokens from service components</span><span class="sxs-lookup"><span data-stu-id="d09e4-161">Use security tokens from service components</span></span>

<span data-ttu-id="d09e4-162">Service components can only generate security tokens using shared access policies granting the appropriate permissions as explained previously.</span><span class="sxs-lookup"><span data-stu-id="d09e4-162">Service components can only generate security tokens using shared access policies granting the appropriate permissions as explained previously.</span></span>

<span data-ttu-id="d09e4-163">Here are the service functions exposed on the endpoints:</span><span class="sxs-lookup"><span data-stu-id="d09e4-163">Here are the service functions exposed on the endpoints:</span></span>

| <span data-ttu-id="d09e4-164">Endpoint</span><span class="sxs-lookup"><span data-stu-id="d09e4-164">Endpoint</span></span> | <span data-ttu-id="d09e4-165">Functionality</span><span class="sxs-lookup"><span data-stu-id="d09e4-165">Functionality</span></span> |
| --- | --- |
| `{your-service}.azure-devices-provisioning.net/enrollments` |<span data-ttu-id="d09e4-166">Provides device enrollment operations with the Device Provisioning Service.</span><span class="sxs-lookup"><span data-stu-id="d09e4-166">Provides device enrollment operations with the Device Provisioning Service.</span></span> |
| `{your-service}.azure-devices-provisioning.net/enrollmentGroups` |<span data-ttu-id="d09e4-167">Provides operations for managing device enrollment groups.</span><span class="sxs-lookup"><span data-stu-id="d09e4-167">Provides operations for managing device enrollment groups.</span></span> |
| `{your-service}.azure-devices-provisioning.net/registrations/{id}` |<span data-ttu-id="d09e4-168">Provides operations for retrieving and managing the status of device registrations.</span><span class="sxs-lookup"><span data-stu-id="d09e4-168">Provides operations for retrieving and managing the status of device registrations.</span></span> |


<span data-ttu-id="d09e4-169">As an example, a service generated using a pre-created shared access policy called **enrollmentread** would create a token with the following parameters:</span><span class="sxs-lookup"><span data-stu-id="d09e4-169">As an example, a service generated using a pre-created shared access policy called **enrollmentread** would create a token with the following parameters:</span></span>

* <span data-ttu-id="d09e4-170">resource URI: `{mydps}.azure-devices-provisioning.net`,</span><span class="sxs-lookup"><span data-stu-id="d09e4-170">resource URI: `{mydps}.azure-devices-provisioning.net`,</span></span>
* <span data-ttu-id="d09e4-171">signing key: one of the keys of the `enrollmentread` policy,</span><span class="sxs-lookup"><span data-stu-id="d09e4-171">signing key: one of the keys of the `enrollmentread` policy,</span></span>
* <span data-ttu-id="d09e4-172">policy name: `enrollmentread`,</span><span class="sxs-lookup"><span data-stu-id="d09e4-172">policy name: `enrollmentread`,</span></span>
* <span data-ttu-id="d09e4-173">any expiration time.backn</span><span class="sxs-lookup"><span data-stu-id="d09e4-173">any expiration time.backn</span></span>

![Create a shared access policy for your Device Provisioning service instance in the portal][img-add-shared-access-policy]

```nodejs
var endpoint ="mydps.azure-devices-provisioning.net";
var policyName = 'enrollmentread'; 
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

<span data-ttu-id="d09e4-175">The result, which would grant access to read all enrollment records, would be:</span><span class="sxs-lookup"><span data-stu-id="d09e4-175">The result, which would grant access to read all enrollment records, would be:</span></span>

`SharedAccessSignature sr=mydps.azure-devices-provisioning.net&sig=JdyscqTpXdEJs49elIUCcohw2DlFDR3zfH5KqGJo4r4%3D&se=1456973447&skn=enrollmentread`

## <a name="reference-topics"></a><span data-ttu-id="d09e4-176">Reference topics:</span><span class="sxs-lookup"><span data-stu-id="d09e4-176">Reference topics:</span></span>

<span data-ttu-id="d09e4-177">The following reference topics provide you with more information about controlling access to your IoT Device Provisioning Service.</span><span class="sxs-lookup"><span data-stu-id="d09e4-177">The following reference topics provide you with more information about controlling access to your IoT Device Provisioning Service.</span></span>

### <a name="device-provisioning-service-permissions"></a><span data-ttu-id="d09e4-178">Device Provisioning Service permissions</span><span class="sxs-lookup"><span data-stu-id="d09e4-178">Device Provisioning Service permissions</span></span>

<span data-ttu-id="d09e4-179">The following table lists the permissions you can use to control access to your IoT Device Provisioning Service.</span><span class="sxs-lookup"><span data-stu-id="d09e4-179">The following table lists the permissions you can use to control access to your IoT Device Provisioning Service.</span></span>

| <span data-ttu-id="d09e4-180">Permission</span><span class="sxs-lookup"><span data-stu-id="d09e4-180">Permission</span></span> | <span data-ttu-id="d09e4-181">Notes</span><span class="sxs-lookup"><span data-stu-id="d09e4-181">Notes</span></span> |
| --- | --- |
| <span data-ttu-id="d09e4-182">**ServiceConfig**</span><span class="sxs-lookup"><span data-stu-id="d09e4-182">**ServiceConfig**</span></span> |<span data-ttu-id="d09e4-183">Grants access to change the service configurations.</span><span class="sxs-lookup"><span data-stu-id="d09e4-183">Grants access to change the service configurations.</span></span> <br/><span data-ttu-id="d09e4-184">This permission is used by backend cloud services.</span><span class="sxs-lookup"><span data-stu-id="d09e4-184">This permission is used by backend cloud services.</span></span> |
| <span data-ttu-id="d09e4-185">**EnrollmentRead**</span><span class="sxs-lookup"><span data-stu-id="d09e4-185">**EnrollmentRead**</span></span> |<span data-ttu-id="d09e4-186">Grants read access to the device enrollments and enrollment groups.</span><span class="sxs-lookup"><span data-stu-id="d09e4-186">Grants read access to the device enrollments and enrollment groups.</span></span> <br/><span data-ttu-id="d09e4-187">This permission is used by backend cloud services.</span><span class="sxs-lookup"><span data-stu-id="d09e4-187">This permission is used by backend cloud services.</span></span> |
| <span data-ttu-id="d09e4-188">**EnrollmentWrite**</span><span class="sxs-lookup"><span data-stu-id="d09e4-188">**EnrollmentWrite**</span></span> |<span data-ttu-id="d09e4-189">Grants write access to the device enrollments and enrollment groups.</span><span class="sxs-lookup"><span data-stu-id="d09e4-189">Grants write access to the device enrollments and enrollment groups.</span></span> <br/><span data-ttu-id="d09e4-190">This permission is used by backend cloud services.</span><span class="sxs-lookup"><span data-stu-id="d09e4-190">This permission is used by backend cloud services.</span></span> |
| <span data-ttu-id="d09e4-191">**RegistrationStatusRead**</span><span class="sxs-lookup"><span data-stu-id="d09e4-191">**RegistrationStatusRead**</span></span> |<span data-ttu-id="d09e4-192">Grants read access to the device registration status.</span><span class="sxs-lookup"><span data-stu-id="d09e4-192">Grants read access to the device registration status.</span></span> <br/><span data-ttu-id="d09e4-193">This permission is used by backend cloud services.</span><span class="sxs-lookup"><span data-stu-id="d09e4-193">This permission is used by backend cloud services.</span></span> |
| <span data-ttu-id="d09e4-194">**RegistrationStatusWrite**</span><span class="sxs-lookup"><span data-stu-id="d09e4-194">**RegistrationStatusWrite**</span></span>  |<span data-ttu-id="d09e4-195">Grants delete access to the device registration status.</span><span class="sxs-lookup"><span data-stu-id="d09e4-195">Grants delete access to the device registration status.</span></span> <br/><span data-ttu-id="d09e4-196">This permission is used by backend cloud services.</span><span class="sxs-lookup"><span data-stu-id="d09e4-196">This permission is used by backend cloud services.</span></span> |

<!-- links and images -->

[img-add-shared-access-policy]: ./media/how-to-control-access/how-to-add-shared-access-policy.PNG
[lnk-sdks]: ../iot-hub/iot-hub-devguide-sdks.md
[lnk-management-portal]: https://portal.azure.com
[lnk-azure-resource-manager]: ../azure-resource-manager/resource-group-overview.md
[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iot-dps/
