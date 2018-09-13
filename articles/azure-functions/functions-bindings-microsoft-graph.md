---
title: Microsoft Graph bindings for Azure Functions
description: Understand how to use Microsoft Graph triggers and bindings in Azure Functions.
services: functions
author: mattchenderson
manager: jeconnoc
ms.service: azure-functions
ms.devlang: multiple
ms.topic: conceptual
ms.date: 12/20/2017
ms.author: mahender
ms.openlocfilehash: 128e7f693755e7baf752d546fddd786b07c0de78
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965872"
---
# <a name="microsoft-graph-bindings-for-azure-functions"></a><span data-ttu-id="36457-103">Microsoft Graph bindings for Azure Functions</span><span class="sxs-lookup"><span data-stu-id="36457-103">Microsoft Graph bindings for Azure Functions</span></span>

<span data-ttu-id="36457-104">This article explains how to configure and work with Microsoft Graph triggers and bindings in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="36457-104">This article explains how to configure and work with Microsoft Graph triggers and bindings in Azure Functions.</span></span> <span data-ttu-id="36457-105">With these, you can use Azure Functions to work with data, insights, and events from the [Microsoft Graph](https://graph.microsoft.io).</span><span class="sxs-lookup"><span data-stu-id="36457-105">With these, you can use Azure Functions to work with data, insights, and events from the [Microsoft Graph](https://graph.microsoft.io).</span></span>

<span data-ttu-id="36457-106">The Microsoft Graph extension provides the following bindings:</span><span class="sxs-lookup"><span data-stu-id="36457-106">The Microsoft Graph extension provides the following bindings:</span></span>
- <span data-ttu-id="36457-107">An [auth token input binding](#token-input) allows you to interact with any Microsoft Graph API.</span><span class="sxs-lookup"><span data-stu-id="36457-107">An [auth token input binding](#token-input) allows you to interact with any Microsoft Graph API.</span></span>
- <span data-ttu-id="36457-108">An [Excel table input binding](#excel-input) allows you to read data from Excel.</span><span class="sxs-lookup"><span data-stu-id="36457-108">An [Excel table input binding](#excel-input) allows you to read data from Excel.</span></span>
- <span data-ttu-id="36457-109">An [Excel table output binding](#excel-output) allows you to modify Excel data.</span><span class="sxs-lookup"><span data-stu-id="36457-109">An [Excel table output binding](#excel-output) allows you to modify Excel data.</span></span>
- <span data-ttu-id="36457-110">A [OneDrive file input binding](#onedrive-input) allows you to read files from OneDrive.</span><span class="sxs-lookup"><span data-stu-id="36457-110">A [OneDrive file input binding](#onedrive-input) allows you to read files from OneDrive.</span></span>
- <span data-ttu-id="36457-111">A [OneDrive file output binding](#onedrive-output) allows you to write to files in OneDrive.</span><span class="sxs-lookup"><span data-stu-id="36457-111">A [OneDrive file output binding](#onedrive-output) allows you to write to files in OneDrive.</span></span>
- <span data-ttu-id="36457-112">An [Outlook message output binding](#outlook-output) allows you to send email through Outlook.</span><span class="sxs-lookup"><span data-stu-id="36457-112">An [Outlook message output binding](#outlook-output) allows you to send email through Outlook.</span></span>
- <span data-ttu-id="36457-113">A collection of [Microsoft Graph webhook triggers and bindings](#webhooks) allows you to react to events from the Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="36457-113">A collection of [Microsoft Graph webhook triggers and bindings](#webhooks) allows you to react to events from the Microsoft Graph.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

> [!Note]
> <span data-ttu-id="36457-114">Microsoft Graph bindings are currently in preview for Azure Functions version 2.x.</span><span class="sxs-lookup"><span data-stu-id="36457-114">Microsoft Graph bindings are currently in preview for Azure Functions version 2.x.</span></span> <span data-ttu-id="36457-115">They are not supported in Functions version 1.x.</span><span class="sxs-lookup"><span data-stu-id="36457-115">They are not supported in Functions version 1.x.</span></span>

## <a name="packages"></a><span data-ttu-id="36457-116">Packages</span><span class="sxs-lookup"><span data-stu-id="36457-116">Packages</span></span>

<span data-ttu-id="36457-117">The auth token input binding is provided in the [Microsoft.Azure.WebJobs.Extensions.AuthTokens](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.AuthTokens/) NuGet package.</span><span class="sxs-lookup"><span data-stu-id="36457-117">The auth token input binding is provided in the [Microsoft.Azure.WebJobs.Extensions.AuthTokens](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.AuthTokens/) NuGet package.</span></span> <span data-ttu-id="36457-118">The other Microsoft Graph bindings are provided in the [Microsoft.Azure.WebJobs.Extensions.MicrosoftGraph](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.MicrosoftGraph/) package.</span><span class="sxs-lookup"><span data-stu-id="36457-118">The other Microsoft Graph bindings are provided in the [Microsoft.Azure.WebJobs.Extensions.MicrosoftGraph](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.MicrosoftGraph/) package.</span></span> <span data-ttu-id="36457-119">Source code for the packages is in the [azure-functions-microsoftgraph-extension](https://github.com/Azure/azure-functions-microsoftgraph-extension/) GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="36457-119">Source code for the packages is in the [azure-functions-microsoftgraph-extension](https://github.com/Azure/azure-functions-microsoftgraph-extension/) GitHub repository.</span></span>

[!INCLUDE [functions-package-v2](../../includes/functions-package-v2.md)]

## <a name="setting-up-the-extensions"></a><span data-ttu-id="36457-120">Setting up the extensions</span><span class="sxs-lookup"><span data-stu-id="36457-120">Setting up the extensions</span></span>

<span data-ttu-id="36457-121">Microsoft Graph bindings are available through _binding extensions_.</span><span class="sxs-lookup"><span data-stu-id="36457-121">Microsoft Graph bindings are available through _binding extensions_.</span></span> <span data-ttu-id="36457-122">Binding extensions are optional components to the Azure Functions runtime.</span><span class="sxs-lookup"><span data-stu-id="36457-122">Binding extensions are optional components to the Azure Functions runtime.</span></span> <span data-ttu-id="36457-123">This section shows how to set up the Microsoft Graph and auth token extensions.</span><span class="sxs-lookup"><span data-stu-id="36457-123">This section shows how to set up the Microsoft Graph and auth token extensions.</span></span>

### <a name="enabling-functions-20-preview"></a><span data-ttu-id="36457-124">Enabling Functions 2.0 preview</span><span class="sxs-lookup"><span data-stu-id="36457-124">Enabling Functions 2.0 preview</span></span>

<span data-ttu-id="36457-125">Binding extensions are available only for Azure Functions 2.0 preview.</span><span class="sxs-lookup"><span data-stu-id="36457-125">Binding extensions are available only for Azure Functions 2.0 preview.</span></span> 

<span data-ttu-id="36457-126">For information about how to set a function app to use the preview 2.0 version of the Functions runtime, see [How to target Azure Functions runtime versions](set-runtime-version.md).</span><span class="sxs-lookup"><span data-stu-id="36457-126">For information about how to set a function app to use the preview 2.0 version of the Functions runtime, see [How to target Azure Functions runtime versions](set-runtime-version.md).</span></span>

### <a name="installing-the-extension"></a><span data-ttu-id="36457-127">Installing the extension</span><span class="sxs-lookup"><span data-stu-id="36457-127">Installing the extension</span></span>

<span data-ttu-id="36457-128">To install an extension from the Azure portal, navigate to either a template or binding that references it.</span><span class="sxs-lookup"><span data-stu-id="36457-128">To install an extension from the Azure portal, navigate to either a template or binding that references it.</span></span> <span data-ttu-id="36457-129">Create a new function, and while in the template selection screen, choose the "Microsoft Graph" scenario.</span><span class="sxs-lookup"><span data-stu-id="36457-129">Create a new function, and while in the template selection screen, choose the "Microsoft Graph" scenario.</span></span> <span data-ttu-id="36457-130">Select one of the templates from this scenario.</span><span class="sxs-lookup"><span data-stu-id="36457-130">Select one of the templates from this scenario.</span></span> <span data-ttu-id="36457-131">Alternatively, you can navigate to the "Integrate" tab of an existing function and select one of the bindings covered in this article.</span><span class="sxs-lookup"><span data-stu-id="36457-131">Alternatively, you can navigate to the "Integrate" tab of an existing function and select one of the bindings covered in this article.</span></span>

<span data-ttu-id="36457-132">In both cases, a warning will appear which specifies the extension to be installed.</span><span class="sxs-lookup"><span data-stu-id="36457-132">In both cases, a warning will appear which specifies the extension to be installed.</span></span> <span data-ttu-id="36457-133">Click **Install** to obtain the extension.</span><span class="sxs-lookup"><span data-stu-id="36457-133">Click **Install** to obtain the extension.</span></span> <span data-ttu-id="36457-134">Each extension only needs to be installed once per function app.</span><span class="sxs-lookup"><span data-stu-id="36457-134">Each extension only needs to be installed once per function app.</span></span> 

> [!Note] 
> <span data-ttu-id="36457-135">The in-portal installation process can take up to 10 minutes on a consumption plan.</span><span class="sxs-lookup"><span data-stu-id="36457-135">The in-portal installation process can take up to 10 minutes on a consumption plan.</span></span>

<span data-ttu-id="36457-136">If you are using Visual Studio, you can get the extensions by installing [the NuGet packages that are listed earlier in this article](#packages).</span><span class="sxs-lookup"><span data-stu-id="36457-136">If you are using Visual Studio, you can get the extensions by installing [the NuGet packages that are listed earlier in this article](#packages).</span></span>

### <a name="configuring-authentication--authorization"></a><span data-ttu-id="36457-137">Configuring Authentication / Authorization</span><span class="sxs-lookup"><span data-stu-id="36457-137">Configuring Authentication / Authorization</span></span>

<span data-ttu-id="36457-138">The bindings outlined in this article require an identity to be used.</span><span class="sxs-lookup"><span data-stu-id="36457-138">The bindings outlined in this article require an identity to be used.</span></span> <span data-ttu-id="36457-139">This allows the Microsoft Graph to enforce permissions and audit interactions.</span><span class="sxs-lookup"><span data-stu-id="36457-139">This allows the Microsoft Graph to enforce permissions and audit interactions.</span></span> <span data-ttu-id="36457-140">The identity can be a user accessing your application or the application itself.</span><span class="sxs-lookup"><span data-stu-id="36457-140">The identity can be a user accessing your application or the application itself.</span></span> <span data-ttu-id="36457-141">To configure this identity, set up [App Service Authentication / Authorization](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview) with Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="36457-141">To configure this identity, set up [App Service Authentication / Authorization](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview) with Azure Active Directory.</span></span> <span data-ttu-id="36457-142">You will also need to request any resource permissions your functions require.</span><span class="sxs-lookup"><span data-stu-id="36457-142">You will also need to request any resource permissions your functions require.</span></span>

> [!Note] 
> <span data-ttu-id="36457-143">The Microsoft Graph extension only supports Azure AD authentication.</span><span class="sxs-lookup"><span data-stu-id="36457-143">The Microsoft Graph extension only supports Azure AD authentication.</span></span> <span data-ttu-id="36457-144">Users need to log in with a work or school account.</span><span class="sxs-lookup"><span data-stu-id="36457-144">Users need to log in with a work or school account.</span></span>

<span data-ttu-id="36457-145">If you're using the Azure portal, you'll see a warning below the prompt to install the extension.</span><span class="sxs-lookup"><span data-stu-id="36457-145">If you're using the Azure portal, you'll see a warning below the prompt to install the extension.</span></span> <span data-ttu-id="36457-146">The warning prompts you to configure App Service Authentication / Authorization and request any permissions the template or binding requires.</span><span class="sxs-lookup"><span data-stu-id="36457-146">The warning prompts you to configure App Service Authentication / Authorization and request any permissions the template or binding requires.</span></span> <span data-ttu-id="36457-147">Click **Configure Azure AD now** or **Add permissions now** as appropriate.</span><span class="sxs-lookup"><span data-stu-id="36457-147">Click **Configure Azure AD now** or **Add permissions now** as appropriate.</span></span>



<a name="token-input"></a>
## <a name="auth-token"></a><span data-ttu-id="36457-148">Auth token</span><span class="sxs-lookup"><span data-stu-id="36457-148">Auth token</span></span>

<span data-ttu-id="36457-149">The auth token input binding gets an Azure AD token for a given resource and provides it to your code as a string.</span><span class="sxs-lookup"><span data-stu-id="36457-149">The auth token input binding gets an Azure AD token for a given resource and provides it to your code as a string.</span></span> <span data-ttu-id="36457-150">The resource can be any for which the application has permissions.</span><span class="sxs-lookup"><span data-stu-id="36457-150">The resource can be any for which the application has permissions.</span></span> 

<span data-ttu-id="36457-151">This section contains the following subsections:</span><span class="sxs-lookup"><span data-stu-id="36457-151">This section contains the following subsections:</span></span>

* [<span data-ttu-id="36457-152">Example</span><span class="sxs-lookup"><span data-stu-id="36457-152">Example</span></span>](#auth-token---example)
* [<span data-ttu-id="36457-153">Attributes</span><span class="sxs-lookup"><span data-stu-id="36457-153">Attributes</span></span>](#auth-token---attributes)
* [<span data-ttu-id="36457-154">Configuration</span><span class="sxs-lookup"><span data-stu-id="36457-154">Configuration</span></span>](#auth-token---configuration)
* [<span data-ttu-id="36457-155">Usage</span><span class="sxs-lookup"><span data-stu-id="36457-155">Usage</span></span>](#auth-token---usage)

### <a name="auth-token---example"></a><span data-ttu-id="36457-156">Auth token - example</span><span class="sxs-lookup"><span data-stu-id="36457-156">Auth token - example</span></span>

<span data-ttu-id="36457-157">See the language-specific example:</span><span class="sxs-lookup"><span data-stu-id="36457-157">See the language-specific example:</span></span>

* [<span data-ttu-id="36457-158">C# script (.csx)</span><span class="sxs-lookup"><span data-stu-id="36457-158">C# script (.csx)</span></span>](#auth-token---c-script-example)
* [<span data-ttu-id="36457-159">JavaScript</span><span class="sxs-lookup"><span data-stu-id="36457-159">JavaScript</span></span>](#auth-token---javascript-example)

#### <a name="auth-token---c-script-example"></a><span data-ttu-id="36457-160">Auth token - C# script example</span><span class="sxs-lookup"><span data-stu-id="36457-160">Auth token - C# script example</span></span>

<span data-ttu-id="36457-161">The following example gets user profile information.</span><span class="sxs-lookup"><span data-stu-id="36457-161">The following example gets user profile information.</span></span>

<span data-ttu-id="36457-162">The *function.json* file defines an HTTP trigger with a token input binding:</span><span class="sxs-lookup"><span data-stu-id="36457-162">The *function.json* file defines an HTTP trigger with a token input binding:</span></span>

```json
{
  "bindings": [
    {
      "name": "req",
      "type": "httpTrigger",
      "direction": "in"
    },
    {
      "type": "token",
      "direction": "in",
      "name": "graphToken",
      "resource": "https://graph.microsoft.com",
      "identity": "userFromRequest"
    },
    {
      "name": "$return",
      "type": "http",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="36457-163">The C# script code uses the token to make an HTTP call to the Microsoft Graph and returns the result:</span><span class="sxs-lookup"><span data-stu-id="36457-163">The C# script code uses the token to make an HTTP call to the Microsoft Graph and returns the result:</span></span>

```csharp
using System.Net; 
using System.Net.Http; 
using System.Net.Http.Headers; 

public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, string graphToken, TraceWriter log)
{
    HttpClient client = new HttpClient();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", graphToken);
    return await client.GetAsync("https://graph.microsoft.com/v1.0/me/");
}
```

#### <a name="auth-token---javascript-example"></a><span data-ttu-id="36457-164">Auth token - JavaScript example</span><span class="sxs-lookup"><span data-stu-id="36457-164">Auth token - JavaScript example</span></span>

<span data-ttu-id="36457-165">The following example gets user profile information.</span><span class="sxs-lookup"><span data-stu-id="36457-165">The following example gets user profile information.</span></span>

<span data-ttu-id="36457-166">The *function.json* file defines an HTTP trigger with a token input binding:</span><span class="sxs-lookup"><span data-stu-id="36457-166">The *function.json* file defines an HTTP trigger with a token input binding:</span></span>

```json
{
  "bindings": [
    {
      "name": "req",
      "type": "httpTrigger",
      "direction": "in"
    },
    {
      "type": "token",
      "direction": "in",
      "name": "graphToken",
      "resource": "https://graph.microsoft.com",
      "identity": "userFromRequest"
    },
    {
      "name": "res",
      "type": "http",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="36457-167">The JavaScript code uses the token to make an HTTP call to the Microsoft Graph and returns the result.</span><span class="sxs-lookup"><span data-stu-id="36457-167">The JavaScript code uses the token to make an HTTP call to the Microsoft Graph and returns the result.</span></span>

```js
const rp = require('request-promise');

module.exports = function (context, req) {
    let token = "Bearer " + context.bindings.graphToken;

    let options = {
        uri: 'https://graph.microsoft.com/v1.0/me/',
        headers: {
            'Authorization': token
        }
    };
    
    rp(options)
        .then(function(profile) {
            context.res = {
                body: profile
            };
            context.done();
        })
        .catch(function(err) {
            context.res = {
                status: 500,
                body: err
            };
            context.done();
        });
};
```

### <a name="auth-token---attributes"></a><span data-ttu-id="36457-168">Auth token - attributes</span><span class="sxs-lookup"><span data-stu-id="36457-168">Auth token - attributes</span></span>

<span data-ttu-id="36457-169">In [C# class libraries](functions-dotnet-class-library.md), use the [Token](https://github.com/Azure/azure-functions-microsoftgraph-extension/blob/master/src/TokenBinding/TokenAttribute.cs) attribute.</span><span class="sxs-lookup"><span data-stu-id="36457-169">In [C# class libraries](functions-dotnet-class-library.md), use the [Token](https://github.com/Azure/azure-functions-microsoftgraph-extension/blob/master/src/TokenBinding/TokenAttribute.cs) attribute.</span></span>

### <a name="auth-token---configuration"></a><span data-ttu-id="36457-170">Auth token - configuration</span><span class="sxs-lookup"><span data-stu-id="36457-170">Auth token - configuration</span></span>

<span data-ttu-id="36457-171">The following table explains the binding configuration properties that you set in the *function.json* file and the `Token` attribute.</span><span class="sxs-lookup"><span data-stu-id="36457-171">The following table explains the binding configuration properties that you set in the *function.json* file and the `Token` attribute.</span></span>

|<span data-ttu-id="36457-172">function.json property</span><span class="sxs-lookup"><span data-stu-id="36457-172">function.json property</span></span> | <span data-ttu-id="36457-173">Attribute property</span><span class="sxs-lookup"><span data-stu-id="36457-173">Attribute property</span></span> |<span data-ttu-id="36457-174">Description</span><span class="sxs-lookup"><span data-stu-id="36457-174">Description</span></span>|
|---------|---------|----------------------|
|<span data-ttu-id="36457-175">**name**</span><span class="sxs-lookup"><span data-stu-id="36457-175">**name**</span></span>||<span data-ttu-id="36457-176">Required - the variable name used in function code for the auth token.</span><span class="sxs-lookup"><span data-stu-id="36457-176">Required - the variable name used in function code for the auth token.</span></span> <span data-ttu-id="36457-177">See [Using an auth token input binding from code](#token-input-code).</span><span class="sxs-lookup"><span data-stu-id="36457-177">See [Using an auth token input binding from code](#token-input-code).</span></span>|
|<span data-ttu-id="36457-178">**type**</span><span class="sxs-lookup"><span data-stu-id="36457-178">**type**</span></span>||<span data-ttu-id="36457-179">Required - must be set to `token`.</span><span class="sxs-lookup"><span data-stu-id="36457-179">Required - must be set to `token`.</span></span>|
|<span data-ttu-id="36457-180">**direction**</span><span class="sxs-lookup"><span data-stu-id="36457-180">**direction**</span></span>||<span data-ttu-id="36457-181">Required - must be set to `in`.</span><span class="sxs-lookup"><span data-stu-id="36457-181">Required - must be set to `in`.</span></span>|
|<span data-ttu-id="36457-182">**identity**</span><span class="sxs-lookup"><span data-stu-id="36457-182">**identity**</span></span>|<span data-ttu-id="36457-183">**Identity**</span><span class="sxs-lookup"><span data-stu-id="36457-183">**Identity**</span></span>|<span data-ttu-id="36457-184">Required - The identity that will be used to perform the action.</span><span class="sxs-lookup"><span data-stu-id="36457-184">Required - The identity that will be used to perform the action.</span></span> <span data-ttu-id="36457-185">Can be one of the following values:</span><span class="sxs-lookup"><span data-stu-id="36457-185">Can be one of the following values:</span></span><ul><li><span data-ttu-id="36457-186"><code>userFromRequest</code> - Only valid with [HTTP trigger].</span><span class="sxs-lookup"><span data-stu-id="36457-186"><code>userFromRequest</code> - Only valid with [HTTP trigger].</span></span> <span data-ttu-id="36457-187">Uses the identity of the calling user.</span><span class="sxs-lookup"><span data-stu-id="36457-187">Uses the identity of the calling user.</span></span></li><li><span data-ttu-id="36457-188"><code>userFromId</code> - Uses the identity of a previously logged-in user with the specified ID.</span><span class="sxs-lookup"><span data-stu-id="36457-188"><code>userFromId</code> - Uses the identity of a previously logged-in user with the specified ID.</span></span> <span data-ttu-id="36457-189">See the <code>userId</code> property.</span><span class="sxs-lookup"><span data-stu-id="36457-189">See the <code>userId</code> property.</span></span></li><li><span data-ttu-id="36457-190"><code>userFromToken</code> - Uses the identity represented by the specified token.</span><span class="sxs-lookup"><span data-stu-id="36457-190"><code>userFromToken</code> - Uses the identity represented by the specified token.</span></span> <span data-ttu-id="36457-191">See the <code>userToken</code> property.</span><span class="sxs-lookup"><span data-stu-id="36457-191">See the <code>userToken</code> property.</span></span></li><li><span data-ttu-id="36457-192"><code>clientCredentials</code> - Uses the identity of the function app.</span><span class="sxs-lookup"><span data-stu-id="36457-192"><code>clientCredentials</code> - Uses the identity of the function app.</span></span></li></ul>|
|<span data-ttu-id="36457-193">**userId**</span><span class="sxs-lookup"><span data-stu-id="36457-193">**userId**</span></span>|<span data-ttu-id="36457-194">**UserId**</span><span class="sxs-lookup"><span data-stu-id="36457-194">**UserId**</span></span>  |<span data-ttu-id="36457-195">Needed if and only if _identity_ is set to `userFromId`.</span><span class="sxs-lookup"><span data-stu-id="36457-195">Needed if and only if _identity_ is set to `userFromId`.</span></span> <span data-ttu-id="36457-196">A user principal ID associated with a previously logged-in user.</span><span class="sxs-lookup"><span data-stu-id="36457-196">A user principal ID associated with a previously logged-in user.</span></span>|
|<span data-ttu-id="36457-197">**userToken**</span><span class="sxs-lookup"><span data-stu-id="36457-197">**userToken**</span></span>|<span data-ttu-id="36457-198">**UserToken**</span><span class="sxs-lookup"><span data-stu-id="36457-198">**UserToken**</span></span>|<span data-ttu-id="36457-199">Needed if and only if _identity_ is set to `userFromToken`.</span><span class="sxs-lookup"><span data-stu-id="36457-199">Needed if and only if _identity_ is set to `userFromToken`.</span></span> <span data-ttu-id="36457-200">A token valid for the function app.</span><span class="sxs-lookup"><span data-stu-id="36457-200">A token valid for the function app.</span></span> |
|<span data-ttu-id="36457-201">**Resource**</span><span class="sxs-lookup"><span data-stu-id="36457-201">**Resource**</span></span>|<span data-ttu-id="36457-202">**resource**</span><span class="sxs-lookup"><span data-stu-id="36457-202">**resource**</span></span>|<span data-ttu-id="36457-203">Required - An Azure AD resource URL for which the token is being requested.</span><span class="sxs-lookup"><span data-stu-id="36457-203">Required - An Azure AD resource URL for which the token is being requested.</span></span>|

<a name="token-input-code"></a>
### <a name="auth-token---usage"></a><span data-ttu-id="36457-204">Auth token - usage</span><span class="sxs-lookup"><span data-stu-id="36457-204">Auth token - usage</span></span>

<span data-ttu-id="36457-205">The binding itself does not require any Azure AD permissions, but depending on how the token is used, you may need to request additional permissions.</span><span class="sxs-lookup"><span data-stu-id="36457-205">The binding itself does not require any Azure AD permissions, but depending on how the token is used, you may need to request additional permissions.</span></span> <span data-ttu-id="36457-206">Check the requirements of the resource you intend to access with the token.</span><span class="sxs-lookup"><span data-stu-id="36457-206">Check the requirements of the resource you intend to access with the token.</span></span>

<span data-ttu-id="36457-207">The token is always presented to code as a string.</span><span class="sxs-lookup"><span data-stu-id="36457-207">The token is always presented to code as a string.</span></span>




<a name="excel-input"></a>
## <a name="excel-input"></a><span data-ttu-id="36457-208">Excel input</span><span class="sxs-lookup"><span data-stu-id="36457-208">Excel input</span></span>

<span data-ttu-id="36457-209">The Excel table input binding reads the contents of an Excel table stored in OneDrive.</span><span class="sxs-lookup"><span data-stu-id="36457-209">The Excel table input binding reads the contents of an Excel table stored in OneDrive.</span></span>

<span data-ttu-id="36457-210">This section contains the following subsections:</span><span class="sxs-lookup"><span data-stu-id="36457-210">This section contains the following subsections:</span></span>

* [<span data-ttu-id="36457-211">Example</span><span class="sxs-lookup"><span data-stu-id="36457-211">Example</span></span>](#excel-input---example)
* [<span data-ttu-id="36457-212">Attributes</span><span class="sxs-lookup"><span data-stu-id="36457-212">Attributes</span></span>](#excel-input---attributes)
* [<span data-ttu-id="36457-213">Configuration</span><span class="sxs-lookup"><span data-stu-id="36457-213">Configuration</span></span>](#excel-input---configuration)
* [<span data-ttu-id="36457-214">Usage</span><span class="sxs-lookup"><span data-stu-id="36457-214">Usage</span></span>](#excel-input---usage)

### <a name="excel-input---example"></a><span data-ttu-id="36457-215">Excel input - example</span><span class="sxs-lookup"><span data-stu-id="36457-215">Excel input - example</span></span>

<span data-ttu-id="36457-216">See the language-specific example:</span><span class="sxs-lookup"><span data-stu-id="36457-216">See the language-specific example:</span></span>

* [<span data-ttu-id="36457-217">C# script (.csx)</span><span class="sxs-lookup"><span data-stu-id="36457-217">C# script (.csx)</span></span>](#excel-input---c-script-example)
* [<span data-ttu-id="36457-218">JavaScript</span><span class="sxs-lookup"><span data-stu-id="36457-218">JavaScript</span></span>](#excel-input---javascript-example)

#### <a name="excel-input---c-script-example"></a><span data-ttu-id="36457-219">Excel input - C# script example</span><span class="sxs-lookup"><span data-stu-id="36457-219">Excel input - C# script example</span></span>

<span data-ttu-id="36457-220">The following *function.json* file defines an HTTP trigger with an Excel input binding:</span><span class="sxs-lookup"><span data-stu-id="36457-220">The following *function.json* file defines an HTTP trigger with an Excel input binding:</span></span>

```json
{
  "bindings": [
    {
      "authLevel": "anonymous",
      "name": "req",
      "type": "httpTrigger",
      "direction": "in"
    },
    {
      "type": "excel",
      "direction": "in",
      "name": "excelTableData",
      "path": "{query.workbook}",
      "identity": "UserFromRequest",
      "tableName": "{query.table}"
    },
    {
      "name": "$return",
      "type": "http",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="36457-221">The following C# script code reads the contents of the specified table and returns them to the user:</span><span class="sxs-lookup"><span data-stu-id="36457-221">The following C# script code reads the contents of the specified table and returns them to the user:</span></span>

```csharp
using System.Net;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Primitives; 

public static IActionResult Run(HttpRequest req, string[][] excelTableData, TraceWriter log)
{
    return new OkObjectResult(excelTableData);
}
```

#### <a name="excel-input---javascript-example"></a><span data-ttu-id="36457-222">Excel input - JavaScript example</span><span class="sxs-lookup"><span data-stu-id="36457-222">Excel input - JavaScript example</span></span>

<span data-ttu-id="36457-223">The following *function.json* file defines an HTTP trigger with an Excel input binding:</span><span class="sxs-lookup"><span data-stu-id="36457-223">The following *function.json* file defines an HTTP trigger with an Excel input binding:</span></span>

```json
{
  "bindings": [
    {
      "authLevel": "anonymous",
      "name": "req",
      "type": "httpTrigger",
      "direction": "in"
    },
    {
      "type": "excel",
      "direction": "in",
      "name": "excelTableData",
      "path": "{query.workbook}",
      "identity": "UserFromRequest",
      "tableName": "{query.table}"
    },
    {
      "name": "res",
      "type": "http",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="36457-224">The following JavaScript code reads the contents of the specified table and returns them to the user.</span><span class="sxs-lookup"><span data-stu-id="36457-224">The following JavaScript code reads the contents of the specified table and returns them to the user.</span></span>

```js
module.exports = function (context, req) {
    context.res = {
        body: context.bindings.excelTableData
    };
    context.done();
};
```

### <a name="excel-input---attributes"></a><span data-ttu-id="36457-225">Excel input - attributes</span><span class="sxs-lookup"><span data-stu-id="36457-225">Excel input - attributes</span></span>

<span data-ttu-id="36457-226">In [C# class libraries](functions-dotnet-class-library.md), use the [Excel](https://github.com/Azure/azure-functions-microsoftgraph-extension/blob/master/src/MicrosoftGraphBinding/Bindings/ExcelAttribute.cs) attribute.</span><span class="sxs-lookup"><span data-stu-id="36457-226">In [C# class libraries](functions-dotnet-class-library.md), use the [Excel](https://github.com/Azure/azure-functions-microsoftgraph-extension/blob/master/src/MicrosoftGraphBinding/Bindings/ExcelAttribute.cs) attribute.</span></span>

### <a name="excel-input---configuration"></a><span data-ttu-id="36457-227">Excel input - configuration</span><span class="sxs-lookup"><span data-stu-id="36457-227">Excel input - configuration</span></span>

<span data-ttu-id="36457-228">The following table explains the binding configuration properties that you set in the *function.json* file and the `Excel` attribute.</span><span class="sxs-lookup"><span data-stu-id="36457-228">The following table explains the binding configuration properties that you set in the *function.json* file and the `Excel` attribute.</span></span>

|<span data-ttu-id="36457-229">function.json property</span><span class="sxs-lookup"><span data-stu-id="36457-229">function.json property</span></span> | <span data-ttu-id="36457-230">Attribute property</span><span class="sxs-lookup"><span data-stu-id="36457-230">Attribute property</span></span> |<span data-ttu-id="36457-231">Description</span><span class="sxs-lookup"><span data-stu-id="36457-231">Description</span></span>|
|---------|---------|----------------------|
|<span data-ttu-id="36457-232">**name**</span><span class="sxs-lookup"><span data-stu-id="36457-232">**name**</span></span>||<span data-ttu-id="36457-233">Required - the variable name used in function code for the Excel table.</span><span class="sxs-lookup"><span data-stu-id="36457-233">Required - the variable name used in function code for the Excel table.</span></span> <span data-ttu-id="36457-234">See [Using an Excel table input binding from code](#excel-input-code).</span><span class="sxs-lookup"><span data-stu-id="36457-234">See [Using an Excel table input binding from code](#excel-input-code).</span></span>|
|<span data-ttu-id="36457-235">**type**</span><span class="sxs-lookup"><span data-stu-id="36457-235">**type**</span></span>||<span data-ttu-id="36457-236">Required - must be set to `excel`.</span><span class="sxs-lookup"><span data-stu-id="36457-236">Required - must be set to `excel`.</span></span>|
|<span data-ttu-id="36457-237">**direction**</span><span class="sxs-lookup"><span data-stu-id="36457-237">**direction**</span></span>||<span data-ttu-id="36457-238">Required - must be set to `in`.</span><span class="sxs-lookup"><span data-stu-id="36457-238">Required - must be set to `in`.</span></span>|
|<span data-ttu-id="36457-239">**identity**</span><span class="sxs-lookup"><span data-stu-id="36457-239">**identity**</span></span>|<span data-ttu-id="36457-240">**Identity**</span><span class="sxs-lookup"><span data-stu-id="36457-240">**Identity**</span></span>|<span data-ttu-id="36457-241">Required - The identity that will be used to perform the action.</span><span class="sxs-lookup"><span data-stu-id="36457-241">Required - The identity that will be used to perform the action.</span></span> <span data-ttu-id="36457-242">Can be one of the following values:</span><span class="sxs-lookup"><span data-stu-id="36457-242">Can be one of the following values:</span></span><ul><li><span data-ttu-id="36457-243"><code>userFromRequest</code> - Only valid with [HTTP trigger].</span><span class="sxs-lookup"><span data-stu-id="36457-243"><code>userFromRequest</code> - Only valid with [HTTP trigger].</span></span> <span data-ttu-id="36457-244">Uses the identity of the calling user.</span><span class="sxs-lookup"><span data-stu-id="36457-244">Uses the identity of the calling user.</span></span></li><li><span data-ttu-id="36457-245"><code>userFromId</code> - Uses the identity of a previously logged-in user with the specified ID.</span><span class="sxs-lookup"><span data-stu-id="36457-245"><code>userFromId</code> - Uses the identity of a previously logged-in user with the specified ID.</span></span> <span data-ttu-id="36457-246">See the <code>userId</code> property.</span><span class="sxs-lookup"><span data-stu-id="36457-246">See the <code>userId</code> property.</span></span></li><li><span data-ttu-id="36457-247"><code>userFromToken</code> - Uses the identity represented by the specified token.</span><span class="sxs-lookup"><span data-stu-id="36457-247"><code>userFromToken</code> - Uses the identity represented by the specified token.</span></span> <span data-ttu-id="36457-248">See the <code>userToken</code> property.</span><span class="sxs-lookup"><span data-stu-id="36457-248">See the <code>userToken</code> property.</span></span></li><li><span data-ttu-id="36457-249"><code>clientCredentials</code> - Uses the identity of the function app.</span><span class="sxs-lookup"><span data-stu-id="36457-249"><code>clientCredentials</code> - Uses the identity of the function app.</span></span></li></ul>|
|<span data-ttu-id="36457-250">**userId**</span><span class="sxs-lookup"><span data-stu-id="36457-250">**userId**</span></span>|<span data-ttu-id="36457-251">**UserId**</span><span class="sxs-lookup"><span data-stu-id="36457-251">**UserId**</span></span>  |<span data-ttu-id="36457-252">Needed if and only if _identity_ is set to `userFromId`.</span><span class="sxs-lookup"><span data-stu-id="36457-252">Needed if and only if _identity_ is set to `userFromId`.</span></span> <span data-ttu-id="36457-253">A user principal ID associated with a previously logged-in user.</span><span class="sxs-lookup"><span data-stu-id="36457-253">A user principal ID associated with a previously logged-in user.</span></span>|
|<span data-ttu-id="36457-254">**userToken**</span><span class="sxs-lookup"><span data-stu-id="36457-254">**userToken**</span></span>|<span data-ttu-id="36457-255">**UserToken**</span><span class="sxs-lookup"><span data-stu-id="36457-255">**UserToken**</span></span>|<span data-ttu-id="36457-256">Needed if and only if _identity_ is set to `userFromToken`.</span><span class="sxs-lookup"><span data-stu-id="36457-256">Needed if and only if _identity_ is set to `userFromToken`.</span></span> <span data-ttu-id="36457-257">A token valid for the function app.</span><span class="sxs-lookup"><span data-stu-id="36457-257">A token valid for the function app.</span></span> |
|<span data-ttu-id="36457-258">**path**</span><span class="sxs-lookup"><span data-stu-id="36457-258">**path**</span></span>|<span data-ttu-id="36457-259">**Path**</span><span class="sxs-lookup"><span data-stu-id="36457-259">**Path**</span></span>|<span data-ttu-id="36457-260">Required - the path in OneDrive to the Excel workbook.</span><span class="sxs-lookup"><span data-stu-id="36457-260">Required - the path in OneDrive to the Excel workbook.</span></span>|
|<span data-ttu-id="36457-261">**worksheetName**</span><span class="sxs-lookup"><span data-stu-id="36457-261">**worksheetName**</span></span>|<span data-ttu-id="36457-262">**WorksheetName**</span><span class="sxs-lookup"><span data-stu-id="36457-262">**WorksheetName**</span></span>|<span data-ttu-id="36457-263">The worksheet in which the table is found.</span><span class="sxs-lookup"><span data-stu-id="36457-263">The worksheet in which the table is found.</span></span>|
|<span data-ttu-id="36457-264">**tableName**</span><span class="sxs-lookup"><span data-stu-id="36457-264">**tableName**</span></span>|<span data-ttu-id="36457-265">**TableName**</span><span class="sxs-lookup"><span data-stu-id="36457-265">**TableName**</span></span>|<span data-ttu-id="36457-266">The name of the table.</span><span class="sxs-lookup"><span data-stu-id="36457-266">The name of the table.</span></span> <span data-ttu-id="36457-267">If not specified, the contents of the worksheet will be used.</span><span class="sxs-lookup"><span data-stu-id="36457-267">If not specified, the contents of the worksheet will be used.</span></span>|

<a name="excel-input-code"></a>
### <a name="excel-input---usage"></a><span data-ttu-id="36457-268">Excel input - usage</span><span class="sxs-lookup"><span data-stu-id="36457-268">Excel input - usage</span></span>

<span data-ttu-id="36457-269">This binding requires the following Azure AD permissions:</span><span class="sxs-lookup"><span data-stu-id="36457-269">This binding requires the following Azure AD permissions:</span></span>
|<span data-ttu-id="36457-270">Resource</span><span class="sxs-lookup"><span data-stu-id="36457-270">Resource</span></span>|<span data-ttu-id="36457-271">Permission</span><span class="sxs-lookup"><span data-stu-id="36457-271">Permission</span></span>|
|--------|--------|
|<span data-ttu-id="36457-272">Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="36457-272">Microsoft Graph</span></span>|<span data-ttu-id="36457-273">Read user files</span><span class="sxs-lookup"><span data-stu-id="36457-273">Read user files</span></span>|

<span data-ttu-id="36457-274">The binding exposes the following types to .NET functions:</span><span class="sxs-lookup"><span data-stu-id="36457-274">The binding exposes the following types to .NET functions:</span></span>
- <span data-ttu-id="36457-275">string[][]</span><span class="sxs-lookup"><span data-stu-id="36457-275">string[][]</span></span>
- <span data-ttu-id="36457-276">Microsoft.Graph.WorkbookTable</span><span class="sxs-lookup"><span data-stu-id="36457-276">Microsoft.Graph.WorkbookTable</span></span>
- <span data-ttu-id="36457-277">Custom object types (using structural model binding)</span><span class="sxs-lookup"><span data-stu-id="36457-277">Custom object types (using structural model binding)</span></span>










<a name="excel-output"></a>
## <a name="excel-output"></a><span data-ttu-id="36457-278">Excel output</span><span class="sxs-lookup"><span data-stu-id="36457-278">Excel output</span></span>

<span data-ttu-id="36457-279">The Excel output binding modifies the contents of an Excel table stored in OneDrive.</span><span class="sxs-lookup"><span data-stu-id="36457-279">The Excel output binding modifies the contents of an Excel table stored in OneDrive.</span></span>

<span data-ttu-id="36457-280">This section contains the following subsections:</span><span class="sxs-lookup"><span data-stu-id="36457-280">This section contains the following subsections:</span></span>

* [<span data-ttu-id="36457-281">Example</span><span class="sxs-lookup"><span data-stu-id="36457-281">Example</span></span>](#excel-output---example)
* [<span data-ttu-id="36457-282">Attributes</span><span class="sxs-lookup"><span data-stu-id="36457-282">Attributes</span></span>](#excel-output---attributes)
* [<span data-ttu-id="36457-283">Configuration</span><span class="sxs-lookup"><span data-stu-id="36457-283">Configuration</span></span>](#excel-output---configuration)
* [<span data-ttu-id="36457-284">Usage</span><span class="sxs-lookup"><span data-stu-id="36457-284">Usage</span></span>](#excel-output---usage)

### <a name="excel-output---example"></a><span data-ttu-id="36457-285">Excel output - example</span><span class="sxs-lookup"><span data-stu-id="36457-285">Excel output - example</span></span>

<span data-ttu-id="36457-286">See the language-specific example:</span><span class="sxs-lookup"><span data-stu-id="36457-286">See the language-specific example:</span></span>

* [<span data-ttu-id="36457-287">C# script (.csx)</span><span class="sxs-lookup"><span data-stu-id="36457-287">C# script (.csx)</span></span>](#excel-output---c-script-example)
* [<span data-ttu-id="36457-288">JavaScript</span><span class="sxs-lookup"><span data-stu-id="36457-288">JavaScript</span></span>](#excel-output---javascript-example)

#### <a name="excel-output---c-script-example"></a><span data-ttu-id="36457-289">Excel output - C# script example</span><span class="sxs-lookup"><span data-stu-id="36457-289">Excel output - C# script example</span></span>

<span data-ttu-id="36457-290">The following example adds rows to an Excel table.</span><span class="sxs-lookup"><span data-stu-id="36457-290">The following example adds rows to an Excel table.</span></span>

<span data-ttu-id="36457-291">The *function.json* file defines an HTTP trigger with an Excel output binding:</span><span class="sxs-lookup"><span data-stu-id="36457-291">The *function.json* file defines an HTTP trigger with an Excel output binding:</span></span>

```json
{
  "bindings": [
    {
      "authLevel": "anonymous",
      "name": "req",
      "type": "httpTrigger",
      "direction": "in"
    },
    {
      "name": "newExcelRow",
      "type": "excel",
      "direction": "out",
      "identity": "userFromRequest",
      "updateType": "append",
      "path": "{query.workbook}",
      "tableName": "{query.table}"
    },
    {
      "name": "$return",
      "type": "http",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="36457-292">The C# script code adds a new row to the table (assumed to be single-column) based on input from the query string:</span><span class="sxs-lookup"><span data-stu-id="36457-292">The C# script code adds a new row to the table (assumed to be single-column) based on input from the query string:</span></span>

```csharp
using System.Net;
using System.Text;

public static async Task Run(HttpRequest req, IAsyncCollector<object> newExcelRow, TraceWriter log)
{
    string input = req.Query
        .FirstOrDefault(q => string.Compare(q.Key, "text", true) == 0)
        .Value;
    await newExcelRow.AddAsync(new {
        Text = input
        // Add other properties for additional columns here
    });
    return;
}
```

#### <a name="excel-output---javascript-example"></a><span data-ttu-id="36457-293">Excel output - JavaScript example</span><span class="sxs-lookup"><span data-stu-id="36457-293">Excel output - JavaScript example</span></span>

<span data-ttu-id="36457-294">The following example adds rows to an Excel table.</span><span class="sxs-lookup"><span data-stu-id="36457-294">The following example adds rows to an Excel table.</span></span>

<span data-ttu-id="36457-295">The *function.json* file defines an HTTP trigger with an Excel output binding:</span><span class="sxs-lookup"><span data-stu-id="36457-295">The *function.json* file defines an HTTP trigger with an Excel output binding:</span></span>

```json
{
  "bindings": [
    {
      "authLevel": "anonymous",
      "name": "req",
      "type": "httpTrigger",
      "direction": "in"
    },
    {
      "name": "newExcelRow",
      "type": "excel",
      "direction": "out",
      "identity": "userFromRequest",
      "updateType": "append",
      "path": "{query.workbook}",
      "tableName": "{query.table}"
    },
    {
      "name": "res",
      "type": "http",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="36457-296">The following JavaScript code adds a new row to the table (assumed to be single-column) based on input from the query string.</span><span class="sxs-lookup"><span data-stu-id="36457-296">The following JavaScript code adds a new row to the table (assumed to be single-column) based on input from the query string.</span></span>

```js
module.exports = function (context, req) {
    context.bindings.newExcelRow = {
        text: req.query.text
        // Add other properties for additional columns here
    }
    context.done();
};
```

### <a name="excel-output---attributes"></a><span data-ttu-id="36457-297">Excel output - attributes</span><span class="sxs-lookup"><span data-stu-id="36457-297">Excel output - attributes</span></span>

<span data-ttu-id="36457-298">In [C# class libraries](functions-dotnet-class-library.md), use the [Excel](https://github.com/Azure/azure-functions-microsoftgraph-extension/blob/master/src/MicrosoftGraphBinding/Bindings/ExcelAttribute.cs) attribute.</span><span class="sxs-lookup"><span data-stu-id="36457-298">In [C# class libraries](functions-dotnet-class-library.md), use the [Excel](https://github.com/Azure/azure-functions-microsoftgraph-extension/blob/master/src/MicrosoftGraphBinding/Bindings/ExcelAttribute.cs) attribute.</span></span>

### <a name="excel-output---configuration"></a><span data-ttu-id="36457-299">Excel output - configuration</span><span class="sxs-lookup"><span data-stu-id="36457-299">Excel output - configuration</span></span>

<span data-ttu-id="36457-300">The following table explains the binding configuration properties that you set in the *function.json* file and the `Excel` attribute.</span><span class="sxs-lookup"><span data-stu-id="36457-300">The following table explains the binding configuration properties that you set in the *function.json* file and the `Excel` attribute.</span></span>

|<span data-ttu-id="36457-301">function.json property</span><span class="sxs-lookup"><span data-stu-id="36457-301">function.json property</span></span> | <span data-ttu-id="36457-302">Attribute property</span><span class="sxs-lookup"><span data-stu-id="36457-302">Attribute property</span></span> |<span data-ttu-id="36457-303">Description</span><span class="sxs-lookup"><span data-stu-id="36457-303">Description</span></span>|
|---------|---------|----------------------|
|<span data-ttu-id="36457-304">**name**</span><span class="sxs-lookup"><span data-stu-id="36457-304">**name**</span></span>||<span data-ttu-id="36457-305">Required - the variable name used in function code for the auth token.</span><span class="sxs-lookup"><span data-stu-id="36457-305">Required - the variable name used in function code for the auth token.</span></span> <span data-ttu-id="36457-306">See [Using an Excel table output binding from code](#excel-output-code).</span><span class="sxs-lookup"><span data-stu-id="36457-306">See [Using an Excel table output binding from code](#excel-output-code).</span></span>|
|<span data-ttu-id="36457-307">**type**</span><span class="sxs-lookup"><span data-stu-id="36457-307">**type**</span></span>||<span data-ttu-id="36457-308">Required - must be set to `excel`.</span><span class="sxs-lookup"><span data-stu-id="36457-308">Required - must be set to `excel`.</span></span>|
|<span data-ttu-id="36457-309">**direction**</span><span class="sxs-lookup"><span data-stu-id="36457-309">**direction**</span></span>||<span data-ttu-id="36457-310">Required - must be set to `out`.</span><span class="sxs-lookup"><span data-stu-id="36457-310">Required - must be set to `out`.</span></span>|
|<span data-ttu-id="36457-311">**identity**</span><span class="sxs-lookup"><span data-stu-id="36457-311">**identity**</span></span>|<span data-ttu-id="36457-312">**Identity**</span><span class="sxs-lookup"><span data-stu-id="36457-312">**Identity**</span></span>|<span data-ttu-id="36457-313">Required - The identity that will be used to perform the action.</span><span class="sxs-lookup"><span data-stu-id="36457-313">Required - The identity that will be used to perform the action.</span></span> <span data-ttu-id="36457-314">Can be one of the following values:</span><span class="sxs-lookup"><span data-stu-id="36457-314">Can be one of the following values:</span></span><ul><li><span data-ttu-id="36457-315"><code>userFromRequest</code> - Only valid with [HTTP trigger].</span><span class="sxs-lookup"><span data-stu-id="36457-315"><code>userFromRequest</code> - Only valid with [HTTP trigger].</span></span> <span data-ttu-id="36457-316">Uses the identity of the calling user.</span><span class="sxs-lookup"><span data-stu-id="36457-316">Uses the identity of the calling user.</span></span></li><li><span data-ttu-id="36457-317"><code>userFromId</code> - Uses the identity of a previously logged-in user with the specified ID.</span><span class="sxs-lookup"><span data-stu-id="36457-317"><code>userFromId</code> - Uses the identity of a previously logged-in user with the specified ID.</span></span> <span data-ttu-id="36457-318">See the <code>userId</code> property.</span><span class="sxs-lookup"><span data-stu-id="36457-318">See the <code>userId</code> property.</span></span></li><li><span data-ttu-id="36457-319"><code>userFromToken</code> - Uses the identity represented by the specified token.</span><span class="sxs-lookup"><span data-stu-id="36457-319"><code>userFromToken</code> - Uses the identity represented by the specified token.</span></span> <span data-ttu-id="36457-320">See the <code>userToken</code> property.</span><span class="sxs-lookup"><span data-stu-id="36457-320">See the <code>userToken</code> property.</span></span></li><li><span data-ttu-id="36457-321"><code>clientCredentials</code> - Uses the identity of the function app.</span><span class="sxs-lookup"><span data-stu-id="36457-321"><code>clientCredentials</code> - Uses the identity of the function app.</span></span></li></ul>|
|<span data-ttu-id="36457-322">**UserId**</span><span class="sxs-lookup"><span data-stu-id="36457-322">**UserId**</span></span> |<span data-ttu-id="36457-323">**userId**</span><span class="sxs-lookup"><span data-stu-id="36457-323">**userId**</span></span> |<span data-ttu-id="36457-324">Needed if and only if _identity_ is set to `userFromId`.</span><span class="sxs-lookup"><span data-stu-id="36457-324">Needed if and only if _identity_ is set to `userFromId`.</span></span> <span data-ttu-id="36457-325">A user principal ID associated with a previously logged-in user.</span><span class="sxs-lookup"><span data-stu-id="36457-325">A user principal ID associated with a previously logged-in user.</span></span>|
|<span data-ttu-id="36457-326">**userToken**</span><span class="sxs-lookup"><span data-stu-id="36457-326">**userToken**</span></span>|<span data-ttu-id="36457-327">**UserToken**</span><span class="sxs-lookup"><span data-stu-id="36457-327">**UserToken**</span></span>|<span data-ttu-id="36457-328">Needed if and only if _identity_ is set to `userFromToken`.</span><span class="sxs-lookup"><span data-stu-id="36457-328">Needed if and only if _identity_ is set to `userFromToken`.</span></span> <span data-ttu-id="36457-329">A token valid for the function app.</span><span class="sxs-lookup"><span data-stu-id="36457-329">A token valid for the function app.</span></span> |
|<span data-ttu-id="36457-330">**path**</span><span class="sxs-lookup"><span data-stu-id="36457-330">**path**</span></span>|<span data-ttu-id="36457-331">**Path**</span><span class="sxs-lookup"><span data-stu-id="36457-331">**Path**</span></span>|<span data-ttu-id="36457-332">Required - the path in OneDrive to the Excel workbook.</span><span class="sxs-lookup"><span data-stu-id="36457-332">Required - the path in OneDrive to the Excel workbook.</span></span>|
|<span data-ttu-id="36457-333">**worksheetName**</span><span class="sxs-lookup"><span data-stu-id="36457-333">**worksheetName**</span></span>|<span data-ttu-id="36457-334">**WorksheetName**</span><span class="sxs-lookup"><span data-stu-id="36457-334">**WorksheetName**</span></span>|<span data-ttu-id="36457-335">The worksheet in which the table is found.</span><span class="sxs-lookup"><span data-stu-id="36457-335">The worksheet in which the table is found.</span></span>|
|<span data-ttu-id="36457-336">**tableName**</span><span class="sxs-lookup"><span data-stu-id="36457-336">**tableName**</span></span>|<span data-ttu-id="36457-337">**TableName**</span><span class="sxs-lookup"><span data-stu-id="36457-337">**TableName**</span></span>|<span data-ttu-id="36457-338">The name of the table.</span><span class="sxs-lookup"><span data-stu-id="36457-338">The name of the table.</span></span> <span data-ttu-id="36457-339">If not specified, the contents of the worksheet will be used.</span><span class="sxs-lookup"><span data-stu-id="36457-339">If not specified, the contents of the worksheet will be used.</span></span>|
|<span data-ttu-id="36457-340">**updateType**</span><span class="sxs-lookup"><span data-stu-id="36457-340">**updateType**</span></span>|<span data-ttu-id="36457-341">**UpdateType**</span><span class="sxs-lookup"><span data-stu-id="36457-341">**UpdateType**</span></span>|<span data-ttu-id="36457-342">Required - The type of change to make to the table.</span><span class="sxs-lookup"><span data-stu-id="36457-342">Required - The type of change to make to the table.</span></span> <span data-ttu-id="36457-343">Can be one of the following values:</span><span class="sxs-lookup"><span data-stu-id="36457-343">Can be one of the following values:</span></span><ul><li><span data-ttu-id="36457-344"><code>update</code> - Replaces the contents of the table in OneDrive.</span><span class="sxs-lookup"><span data-stu-id="36457-344"><code>update</code> - Replaces the contents of the table in OneDrive.</span></span></li><li><span data-ttu-id="36457-345"><code>append</code> - Adds the payload to the end of the table in OneDrive by creating new rows.</span><span class="sxs-lookup"><span data-stu-id="36457-345"><code>append</code> - Adds the payload to the end of the table in OneDrive by creating new rows.</span></span></li></ul>|

<a name="excel-output-code"></a>
### <a name="excel-output---usage"></a><span data-ttu-id="36457-346">Excel output - usage</span><span class="sxs-lookup"><span data-stu-id="36457-346">Excel output - usage</span></span>

<span data-ttu-id="36457-347">This binding requires the following Azure AD permissions:</span><span class="sxs-lookup"><span data-stu-id="36457-347">This binding requires the following Azure AD permissions:</span></span>
|<span data-ttu-id="36457-348">Resource</span><span class="sxs-lookup"><span data-stu-id="36457-348">Resource</span></span>|<span data-ttu-id="36457-349">Permission</span><span class="sxs-lookup"><span data-stu-id="36457-349">Permission</span></span>|
|--------|--------|
|<span data-ttu-id="36457-350">Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="36457-350">Microsoft Graph</span></span>|<span data-ttu-id="36457-351">Have full access to user files</span><span class="sxs-lookup"><span data-stu-id="36457-351">Have full access to user files</span></span>|

<span data-ttu-id="36457-352">The binding exposes the following types to .NET functions:</span><span class="sxs-lookup"><span data-stu-id="36457-352">The binding exposes the following types to .NET functions:</span></span>
- <span data-ttu-id="36457-353">string[][]</span><span class="sxs-lookup"><span data-stu-id="36457-353">string[][]</span></span>
- <span data-ttu-id="36457-354">Newtonsoft.Json.Linq.JObject</span><span class="sxs-lookup"><span data-stu-id="36457-354">Newtonsoft.Json.Linq.JObject</span></span>
- <span data-ttu-id="36457-355">Microsoft.Graph.WorkbookTable</span><span class="sxs-lookup"><span data-stu-id="36457-355">Microsoft.Graph.WorkbookTable</span></span>
- <span data-ttu-id="36457-356">Custom object types (using structural model binding)</span><span class="sxs-lookup"><span data-stu-id="36457-356">Custom object types (using structural model binding)</span></span>





<a name="onedrive-input"></a>
## <a name="file-input"></a><span data-ttu-id="36457-357">File input</span><span class="sxs-lookup"><span data-stu-id="36457-357">File input</span></span>

<span data-ttu-id="36457-358">The OneDrive File input binding reads the contents of a file stored in OneDrive.</span><span class="sxs-lookup"><span data-stu-id="36457-358">The OneDrive File input binding reads the contents of a file stored in OneDrive.</span></span>

<span data-ttu-id="36457-359">This section contains the following subsections:</span><span class="sxs-lookup"><span data-stu-id="36457-359">This section contains the following subsections:</span></span>

* [<span data-ttu-id="36457-360">Example</span><span class="sxs-lookup"><span data-stu-id="36457-360">Example</span></span>](#file-input---example)
* [<span data-ttu-id="36457-361">Attributes</span><span class="sxs-lookup"><span data-stu-id="36457-361">Attributes</span></span>](#file-input---attributes)
* [<span data-ttu-id="36457-362">Configuration</span><span class="sxs-lookup"><span data-stu-id="36457-362">Configuration</span></span>](#file-input---configuration)
* [<span data-ttu-id="36457-363">Usage</span><span class="sxs-lookup"><span data-stu-id="36457-363">Usage</span></span>](#file-input---usage)

### <a name="file-input---example"></a><span data-ttu-id="36457-364">File input - example</span><span class="sxs-lookup"><span data-stu-id="36457-364">File input - example</span></span>

<span data-ttu-id="36457-365">See the language-specific example:</span><span class="sxs-lookup"><span data-stu-id="36457-365">See the language-specific example:</span></span>

* [<span data-ttu-id="36457-366">C# script (.csx)</span><span class="sxs-lookup"><span data-stu-id="36457-366">C# script (.csx)</span></span>](#file-input---c-script-example)
* [<span data-ttu-id="36457-367">JavaScript</span><span class="sxs-lookup"><span data-stu-id="36457-367">JavaScript</span></span>](#file-input---javascript-example)

#### <a name="file-input---c-script-example"></a><span data-ttu-id="36457-368">File input - C# script example</span><span class="sxs-lookup"><span data-stu-id="36457-368">File input - C# script example</span></span>

<span data-ttu-id="36457-369">The following example reads a file that is stored in OneDrive.</span><span class="sxs-lookup"><span data-stu-id="36457-369">The following example reads a file that is stored in OneDrive.</span></span>

<span data-ttu-id="36457-370">The *function.json* file defines an HTTP trigger with a OneDrive file input binding:</span><span class="sxs-lookup"><span data-stu-id="36457-370">The *function.json* file defines an HTTP trigger with a OneDrive file input binding:</span></span>

```json
{
  "bindings": [
    {
      "authLevel": "anonymous",
      "name": "req",
      "type": "httpTrigger",
      "direction": "in"
    },
    {
      "name": "myOneDriveFile",
      "type": "onedrive",
      "direction": "in",
      "path": "{query.filename}",
      "identity": "userFromRequest"
    },
    {
      "name": "$return",
      "type": "http",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="36457-371">The C# script code reads the file specified in the query string and logs its length:</span><span class="sxs-lookup"><span data-stu-id="36457-371">The C# script code reads the file specified in the query string and logs its length:</span></span>

```csharp
using System.Net;

public static void Run(HttpRequestMessage req, Stream myOneDriveFile, TraceWriter log)
{
    log.Info(myOneDriveFile.Length.ToString());
}
```

#### <a name="file-input---javascript-example"></a><span data-ttu-id="36457-372">File input - JavaScript example</span><span class="sxs-lookup"><span data-stu-id="36457-372">File input - JavaScript example</span></span>

<span data-ttu-id="36457-373">The following example reads a file that is stored in OneDrive.</span><span class="sxs-lookup"><span data-stu-id="36457-373">The following example reads a file that is stored in OneDrive.</span></span>

<span data-ttu-id="36457-374">The *function.json* file defines an HTTP trigger with a OneDrive file input binding:</span><span class="sxs-lookup"><span data-stu-id="36457-374">The *function.json* file defines an HTTP trigger with a OneDrive file input binding:</span></span>

```json
{
  "bindings": [
    {
      "authLevel": "anonymous",
      "name": "req",
      "type": "httpTrigger",
      "direction": "in"
    },
    {
      "name": "myOneDriveFile",
      "type": "onedrive",
      "direction": "in",
      "path": "{query.filename}",
      "identity": "userFromRequest"
    },
    {
      "name": "res",
      "type": "http",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="36457-375">The following JavaScript code reads the file specified in the query string and returns its length.</span><span class="sxs-lookup"><span data-stu-id="36457-375">The following JavaScript code reads the file specified in the query string and returns its length.</span></span>

```js
module.exports = function (context, req) {
    context.res = {
        body: context.bindings.myOneDriveFile.length
    };
    context.done();
};
```

### <a name="file-input---attributes"></a><span data-ttu-id="36457-376">File input - attributes</span><span class="sxs-lookup"><span data-stu-id="36457-376">File input - attributes</span></span>

<span data-ttu-id="36457-377">In [C# class libraries](functions-dotnet-class-library.md), use the [OneDrive](https://github.com/Azure/azure-functions-microsoftgraph-extension/blob/master/src/MicrosoftGraphBinding/Bindings/OneDriveAttribute.cs) attribute.</span><span class="sxs-lookup"><span data-stu-id="36457-377">In [C# class libraries](functions-dotnet-class-library.md), use the [OneDrive](https://github.com/Azure/azure-functions-microsoftgraph-extension/blob/master/src/MicrosoftGraphBinding/Bindings/OneDriveAttribute.cs) attribute.</span></span>

### <a name="file-input---configuration"></a><span data-ttu-id="36457-378">File input - configuration</span><span class="sxs-lookup"><span data-stu-id="36457-378">File input - configuration</span></span>

<span data-ttu-id="36457-379">The following table explains the binding configuration properties that you set in the *function.json* file and the `OneDrive` attribute.</span><span class="sxs-lookup"><span data-stu-id="36457-379">The following table explains the binding configuration properties that you set in the *function.json* file and the `OneDrive` attribute.</span></span>

|<span data-ttu-id="36457-380">function.json property</span><span class="sxs-lookup"><span data-stu-id="36457-380">function.json property</span></span> | <span data-ttu-id="36457-381">Attribute property</span><span class="sxs-lookup"><span data-stu-id="36457-381">Attribute property</span></span> |<span data-ttu-id="36457-382">Description</span><span class="sxs-lookup"><span data-stu-id="36457-382">Description</span></span>|
|---------|---------|----------------------|
|<span data-ttu-id="36457-383">**name**</span><span class="sxs-lookup"><span data-stu-id="36457-383">**name**</span></span>||<span data-ttu-id="36457-384">Required - the variable name used in function code for the file.</span><span class="sxs-lookup"><span data-stu-id="36457-384">Required - the variable name used in function code for the file.</span></span> <span data-ttu-id="36457-385">See [Using a OneDrive file input binding from code](#onedrive-input-code).</span><span class="sxs-lookup"><span data-stu-id="36457-385">See [Using a OneDrive file input binding from code](#onedrive-input-code).</span></span>|
|<span data-ttu-id="36457-386">**type**</span><span class="sxs-lookup"><span data-stu-id="36457-386">**type**</span></span>||<span data-ttu-id="36457-387">Required - must be set to `onedrive`.</span><span class="sxs-lookup"><span data-stu-id="36457-387">Required - must be set to `onedrive`.</span></span>|
|<span data-ttu-id="36457-388">**direction**</span><span class="sxs-lookup"><span data-stu-id="36457-388">**direction**</span></span>||<span data-ttu-id="36457-389">Required - must be set to `in`.</span><span class="sxs-lookup"><span data-stu-id="36457-389">Required - must be set to `in`.</span></span>|
|<span data-ttu-id="36457-390">**identity**</span><span class="sxs-lookup"><span data-stu-id="36457-390">**identity**</span></span>|<span data-ttu-id="36457-391">**Identity**</span><span class="sxs-lookup"><span data-stu-id="36457-391">**Identity**</span></span>|<span data-ttu-id="36457-392">Required - The identity that will be used to perform the action.</span><span class="sxs-lookup"><span data-stu-id="36457-392">Required - The identity that will be used to perform the action.</span></span> <span data-ttu-id="36457-393">Can be one of the following values:</span><span class="sxs-lookup"><span data-stu-id="36457-393">Can be one of the following values:</span></span><ul><li><span data-ttu-id="36457-394"><code>userFromRequest</code> - Only valid with [HTTP trigger].</span><span class="sxs-lookup"><span data-stu-id="36457-394"><code>userFromRequest</code> - Only valid with [HTTP trigger].</span></span> <span data-ttu-id="36457-395">Uses the identity of the calling user.</span><span class="sxs-lookup"><span data-stu-id="36457-395">Uses the identity of the calling user.</span></span></li><li><span data-ttu-id="36457-396"><code>userFromId</code> - Uses the identity of a previously logged-in user with the specified ID.</span><span class="sxs-lookup"><span data-stu-id="36457-396"><code>userFromId</code> - Uses the identity of a previously logged-in user with the specified ID.</span></span> <span data-ttu-id="36457-397">See the <code>userId</code> property.</span><span class="sxs-lookup"><span data-stu-id="36457-397">See the <code>userId</code> property.</span></span></li><li><span data-ttu-id="36457-398"><code>userFromToken</code> - Uses the identity represented by the specified token.</span><span class="sxs-lookup"><span data-stu-id="36457-398"><code>userFromToken</code> - Uses the identity represented by the specified token.</span></span> <span data-ttu-id="36457-399">See the <code>userToken</code> property.</span><span class="sxs-lookup"><span data-stu-id="36457-399">See the <code>userToken</code> property.</span></span></li><li><span data-ttu-id="36457-400"><code>clientCredentials</code> - Uses the identity of the function app.</span><span class="sxs-lookup"><span data-stu-id="36457-400"><code>clientCredentials</code> - Uses the identity of the function app.</span></span></li></ul>|
|<span data-ttu-id="36457-401">**userId**</span><span class="sxs-lookup"><span data-stu-id="36457-401">**userId**</span></span>|<span data-ttu-id="36457-402">**UserId**</span><span class="sxs-lookup"><span data-stu-id="36457-402">**UserId**</span></span>  |<span data-ttu-id="36457-403">Needed if and only if _identity_ is set to `userFromId`.</span><span class="sxs-lookup"><span data-stu-id="36457-403">Needed if and only if _identity_ is set to `userFromId`.</span></span> <span data-ttu-id="36457-404">A user principal ID associated with a previously logged-in user.</span><span class="sxs-lookup"><span data-stu-id="36457-404">A user principal ID associated with a previously logged-in user.</span></span>|
|<span data-ttu-id="36457-405">**userToken**</span><span class="sxs-lookup"><span data-stu-id="36457-405">**userToken**</span></span>|<span data-ttu-id="36457-406">**UserToken**</span><span class="sxs-lookup"><span data-stu-id="36457-406">**UserToken**</span></span>|<span data-ttu-id="36457-407">Needed if and only if _identity_ is set to `userFromToken`.</span><span class="sxs-lookup"><span data-stu-id="36457-407">Needed if and only if _identity_ is set to `userFromToken`.</span></span> <span data-ttu-id="36457-408">A token valid for the function app.</span><span class="sxs-lookup"><span data-stu-id="36457-408">A token valid for the function app.</span></span> |
|<span data-ttu-id="36457-409">**path**</span><span class="sxs-lookup"><span data-stu-id="36457-409">**path**</span></span>|<span data-ttu-id="36457-410">**Path**</span><span class="sxs-lookup"><span data-stu-id="36457-410">**Path**</span></span>|<span data-ttu-id="36457-411">Required - the path in OneDrive to the file.</span><span class="sxs-lookup"><span data-stu-id="36457-411">Required - the path in OneDrive to the file.</span></span>|

<a name="onedrive-input-code"></a>
### <a name="file-input---usage"></a><span data-ttu-id="36457-412">File input - usage</span><span class="sxs-lookup"><span data-stu-id="36457-412">File input - usage</span></span>

<span data-ttu-id="36457-413">This binding requires the following Azure AD permissions:</span><span class="sxs-lookup"><span data-stu-id="36457-413">This binding requires the following Azure AD permissions:</span></span>
|<span data-ttu-id="36457-414">Resource</span><span class="sxs-lookup"><span data-stu-id="36457-414">Resource</span></span>|<span data-ttu-id="36457-415">Permission</span><span class="sxs-lookup"><span data-stu-id="36457-415">Permission</span></span>|
|--------|--------|
|<span data-ttu-id="36457-416">Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="36457-416">Microsoft Graph</span></span>|<span data-ttu-id="36457-417">Read user files</span><span class="sxs-lookup"><span data-stu-id="36457-417">Read user files</span></span>|

<span data-ttu-id="36457-418">The binding exposes the following types to .NET functions:</span><span class="sxs-lookup"><span data-stu-id="36457-418">The binding exposes the following types to .NET functions:</span></span>
- <span data-ttu-id="36457-419">byte[]</span><span class="sxs-lookup"><span data-stu-id="36457-419">byte[]</span></span>
- <span data-ttu-id="36457-420">Stream</span><span class="sxs-lookup"><span data-stu-id="36457-420">Stream</span></span>
- <span data-ttu-id="36457-421">string</span><span class="sxs-lookup"><span data-stu-id="36457-421">string</span></span>
- <span data-ttu-id="36457-422">Microsoft.Graph.DriveItem</span><span class="sxs-lookup"><span data-stu-id="36457-422">Microsoft.Graph.DriveItem</span></span>






<a name="onedrive-output"></a>
## <a name="file-output"></a><span data-ttu-id="36457-423">File output</span><span class="sxs-lookup"><span data-stu-id="36457-423">File output</span></span>

<span data-ttu-id="36457-424">The OneDrive file output binding modifies the contents of a file stored in OneDrive.</span><span class="sxs-lookup"><span data-stu-id="36457-424">The OneDrive file output binding modifies the contents of a file stored in OneDrive.</span></span>

<span data-ttu-id="36457-425">This section contains the following subsections:</span><span class="sxs-lookup"><span data-stu-id="36457-425">This section contains the following subsections:</span></span>

* [<span data-ttu-id="36457-426">Example</span><span class="sxs-lookup"><span data-stu-id="36457-426">Example</span></span>](#file-output---example)
* [<span data-ttu-id="36457-427">Attributes</span><span class="sxs-lookup"><span data-stu-id="36457-427">Attributes</span></span>](#file-output---attributes)
* [<span data-ttu-id="36457-428">Configuration</span><span class="sxs-lookup"><span data-stu-id="36457-428">Configuration</span></span>](#file-output---configuration)
* [<span data-ttu-id="36457-429">Usage</span><span class="sxs-lookup"><span data-stu-id="36457-429">Usage</span></span>](#file-output---usage)

### <a name="file-output---example"></a><span data-ttu-id="36457-430">File output - example</span><span class="sxs-lookup"><span data-stu-id="36457-430">File output - example</span></span>

<span data-ttu-id="36457-431">See the language-specific example:</span><span class="sxs-lookup"><span data-stu-id="36457-431">See the language-specific example:</span></span>

* [<span data-ttu-id="36457-432">C# script (.csx)</span><span class="sxs-lookup"><span data-stu-id="36457-432">C# script (.csx)</span></span>](#file-output---c-script-example)
* [<span data-ttu-id="36457-433">JavaScript</span><span class="sxs-lookup"><span data-stu-id="36457-433">JavaScript</span></span>](#file-output---javascript-example)

#### <a name="file-output---c-script-example"></a><span data-ttu-id="36457-434">File output - C# script example</span><span class="sxs-lookup"><span data-stu-id="36457-434">File output - C# script example</span></span>

<span data-ttu-id="36457-435">The following example writes to a file that is stored in OneDrive.</span><span class="sxs-lookup"><span data-stu-id="36457-435">The following example writes to a file that is stored in OneDrive.</span></span>

<span data-ttu-id="36457-436">The *function.json* file defines an HTTP trigger with a OneDrive output binding:</span><span class="sxs-lookup"><span data-stu-id="36457-436">The *function.json* file defines an HTTP trigger with a OneDrive output binding:</span></span>

```json
{
  "bindings": [
    {
      "authLevel": "anonymous",
      "name": "req",
      "type": "httpTrigger",
      "direction": "in"
    },
    {
      "name": "myOneDriveFile",
      "type": "onedrive",
      "direction": "out",
      "path": "FunctionsTest.txt",
      "identity": "userFromRequest"
    },
    {
      "name": "$return",
      "type": "http",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="36457-437">The C# script code gets text from the query string and writes it to a text file (FunctionsTest.txt as defined in the preceding example) at the root of the caller's OneDrive:</span><span class="sxs-lookup"><span data-stu-id="36457-437">The C# script code gets text from the query string and writes it to a text file (FunctionsTest.txt as defined in the preceding example) at the root of the caller's OneDrive:</span></span>

```csharp
using System.Net;
using System.Text;

public static async Task Run(HttpRequest req, TraceWriter log, Stream myOneDriveFile)
{
    string data = req.Query
        .FirstOrDefault(q => string.Compare(q.Key, "text", true) == 0)
        .Value;
    await myOneDriveFile.WriteAsync(Encoding.UTF8.GetBytes(data), 0, data.Length);
    return;
}
```

#### <a name="file-output---javascript-example"></a><span data-ttu-id="36457-438">File output - JavaScript example</span><span class="sxs-lookup"><span data-stu-id="36457-438">File output - JavaScript example</span></span>

<span data-ttu-id="36457-439">The following example writes to a file that is stored in OneDrive.</span><span class="sxs-lookup"><span data-stu-id="36457-439">The following example writes to a file that is stored in OneDrive.</span></span>

<span data-ttu-id="36457-440">The *function.json* file defines an HTTP trigger with a OneDrive output binding:</span><span class="sxs-lookup"><span data-stu-id="36457-440">The *function.json* file defines an HTTP trigger with a OneDrive output binding:</span></span>

```json
{
  "bindings": [
    {
      "authLevel": "anonymous",
      "name": "req",
      "type": "httpTrigger",
      "direction": "in"
    },
    {
      "name": "myOneDriveFile",
      "type": "onedrive",
      "direction": "out",
      "path": "FunctionsTest.txt",
      "identity": "userFromRequest"
    },
    {
      "name": "res",
      "type": "http",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="36457-441">The JavaScript code gets text from the query string and writes it to a text file (FunctionsTest.txt as defined in the config above) at the root of the caller's OneDrive.</span><span class="sxs-lookup"><span data-stu-id="36457-441">The JavaScript code gets text from the query string and writes it to a text file (FunctionsTest.txt as defined in the config above) at the root of the caller's OneDrive.</span></span>

```js
module.exports = function (context, req) {
    context.bindings.myOneDriveFile = req.query.text;
    context.done();
};
```

### <a name="file-output---attributes"></a><span data-ttu-id="36457-442">File output - attributes</span><span class="sxs-lookup"><span data-stu-id="36457-442">File output - attributes</span></span>

<span data-ttu-id="36457-443">In [C# class libraries](functions-dotnet-class-library.md), use the [OneDrive](https://github.com/Azure/azure-functions-microsoftgraph-extension/blob/master/src/MicrosoftGraphBinding/Bindings/OneDriveAttribute.cs) attribute.</span><span class="sxs-lookup"><span data-stu-id="36457-443">In [C# class libraries](functions-dotnet-class-library.md), use the [OneDrive](https://github.com/Azure/azure-functions-microsoftgraph-extension/blob/master/src/MicrosoftGraphBinding/Bindings/OneDriveAttribute.cs) attribute.</span></span>

### <a name="file-output---configuration"></a><span data-ttu-id="36457-444">File output - configuration</span><span class="sxs-lookup"><span data-stu-id="36457-444">File output - configuration</span></span>

<span data-ttu-id="36457-445">The following table explains the binding configuration properties that you set in the *function.json* file and the `OneDrive` attribute.</span><span class="sxs-lookup"><span data-stu-id="36457-445">The following table explains the binding configuration properties that you set in the *function.json* file and the `OneDrive` attribute.</span></span>

|<span data-ttu-id="36457-446">function.json property</span><span class="sxs-lookup"><span data-stu-id="36457-446">function.json property</span></span> | <span data-ttu-id="36457-447">Attribute property</span><span class="sxs-lookup"><span data-stu-id="36457-447">Attribute property</span></span> |<span data-ttu-id="36457-448">Description</span><span class="sxs-lookup"><span data-stu-id="36457-448">Description</span></span>|
|---------|---------|----------------------|
|<span data-ttu-id="36457-449">**name**</span><span class="sxs-lookup"><span data-stu-id="36457-449">**name**</span></span>||<span data-ttu-id="36457-450">Required - the variable name used in function code for file.</span><span class="sxs-lookup"><span data-stu-id="36457-450">Required - the variable name used in function code for file.</span></span> <span data-ttu-id="36457-451">See [Using a OneDrive file output binding from code](#onedrive-output-code).</span><span class="sxs-lookup"><span data-stu-id="36457-451">See [Using a OneDrive file output binding from code](#onedrive-output-code).</span></span>|
|<span data-ttu-id="36457-452">**type**</span><span class="sxs-lookup"><span data-stu-id="36457-452">**type**</span></span>||<span data-ttu-id="36457-453">Required - must be set to `onedrive`.</span><span class="sxs-lookup"><span data-stu-id="36457-453">Required - must be set to `onedrive`.</span></span>|
|<span data-ttu-id="36457-454">**direction**</span><span class="sxs-lookup"><span data-stu-id="36457-454">**direction**</span></span>||<span data-ttu-id="36457-455">Required - must be set to `out`.</span><span class="sxs-lookup"><span data-stu-id="36457-455">Required - must be set to `out`.</span></span>|
|<span data-ttu-id="36457-456">**identity**</span><span class="sxs-lookup"><span data-stu-id="36457-456">**identity**</span></span>|<span data-ttu-id="36457-457">**Identity**</span><span class="sxs-lookup"><span data-stu-id="36457-457">**Identity**</span></span>|<span data-ttu-id="36457-458">Required - The identity that will be used to perform the action.</span><span class="sxs-lookup"><span data-stu-id="36457-458">Required - The identity that will be used to perform the action.</span></span> <span data-ttu-id="36457-459">Can be one of the following values:</span><span class="sxs-lookup"><span data-stu-id="36457-459">Can be one of the following values:</span></span><ul><li><span data-ttu-id="36457-460"><code>userFromRequest</code> - Only valid with [HTTP trigger].</span><span class="sxs-lookup"><span data-stu-id="36457-460"><code>userFromRequest</code> - Only valid with [HTTP trigger].</span></span> <span data-ttu-id="36457-461">Uses the identity of the calling user.</span><span class="sxs-lookup"><span data-stu-id="36457-461">Uses the identity of the calling user.</span></span></li><li><span data-ttu-id="36457-462"><code>userFromId</code> - Uses the identity of a previously logged-in user with the specified ID.</span><span class="sxs-lookup"><span data-stu-id="36457-462"><code>userFromId</code> - Uses the identity of a previously logged-in user with the specified ID.</span></span> <span data-ttu-id="36457-463">See the <code>userId</code> property.</span><span class="sxs-lookup"><span data-stu-id="36457-463">See the <code>userId</code> property.</span></span></li><li><span data-ttu-id="36457-464"><code>userFromToken</code> - Uses the identity represented by the specified token.</span><span class="sxs-lookup"><span data-stu-id="36457-464"><code>userFromToken</code> - Uses the identity represented by the specified token.</span></span> <span data-ttu-id="36457-465">See the <code>userToken</code> property.</span><span class="sxs-lookup"><span data-stu-id="36457-465">See the <code>userToken</code> property.</span></span></li><li><span data-ttu-id="36457-466"><code>clientCredentials</code> - Uses the identity of the function app.</span><span class="sxs-lookup"><span data-stu-id="36457-466"><code>clientCredentials</code> - Uses the identity of the function app.</span></span></li></ul>|
|<span data-ttu-id="36457-467">**UserId**</span><span class="sxs-lookup"><span data-stu-id="36457-467">**UserId**</span></span> |<span data-ttu-id="36457-468">**userId**</span><span class="sxs-lookup"><span data-stu-id="36457-468">**userId**</span></span> |<span data-ttu-id="36457-469">Needed if and only if _identity_ is set to `userFromId`.</span><span class="sxs-lookup"><span data-stu-id="36457-469">Needed if and only if _identity_ is set to `userFromId`.</span></span> <span data-ttu-id="36457-470">A user principal ID associated with a previously logged-in user.</span><span class="sxs-lookup"><span data-stu-id="36457-470">A user principal ID associated with a previously logged-in user.</span></span>|
|<span data-ttu-id="36457-471">**userToken**</span><span class="sxs-lookup"><span data-stu-id="36457-471">**userToken**</span></span>|<span data-ttu-id="36457-472">**UserToken**</span><span class="sxs-lookup"><span data-stu-id="36457-472">**UserToken**</span></span>|<span data-ttu-id="36457-473">Needed if and only if _identity_ is set to `userFromToken`.</span><span class="sxs-lookup"><span data-stu-id="36457-473">Needed if and only if _identity_ is set to `userFromToken`.</span></span> <span data-ttu-id="36457-474">A token valid for the function app.</span><span class="sxs-lookup"><span data-stu-id="36457-474">A token valid for the function app.</span></span> |
|<span data-ttu-id="36457-475">**path**</span><span class="sxs-lookup"><span data-stu-id="36457-475">**path**</span></span>|<span data-ttu-id="36457-476">**Path**</span><span class="sxs-lookup"><span data-stu-id="36457-476">**Path**</span></span>|<span data-ttu-id="36457-477">Required - the path in OneDrive to the file.</span><span class="sxs-lookup"><span data-stu-id="36457-477">Required - the path in OneDrive to the file.</span></span>|

<a name="onedrive-output-code"></a>
#### <a name="file-output---usage"></a><span data-ttu-id="36457-478">File output - usage</span><span class="sxs-lookup"><span data-stu-id="36457-478">File output - usage</span></span>

<span data-ttu-id="36457-479">This binding requires the following Azure AD permissions:</span><span class="sxs-lookup"><span data-stu-id="36457-479">This binding requires the following Azure AD permissions:</span></span>
|<span data-ttu-id="36457-480">Resource</span><span class="sxs-lookup"><span data-stu-id="36457-480">Resource</span></span>|<span data-ttu-id="36457-481">Permission</span><span class="sxs-lookup"><span data-stu-id="36457-481">Permission</span></span>|
|--------|--------|
|<span data-ttu-id="36457-482">Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="36457-482">Microsoft Graph</span></span>|<span data-ttu-id="36457-483">Have full access to user files</span><span class="sxs-lookup"><span data-stu-id="36457-483">Have full access to user files</span></span>|

<span data-ttu-id="36457-484">The binding exposes the following types to .NET functions:</span><span class="sxs-lookup"><span data-stu-id="36457-484">The binding exposes the following types to .NET functions:</span></span>
- <span data-ttu-id="36457-485">byte[]</span><span class="sxs-lookup"><span data-stu-id="36457-485">byte[]</span></span>
- <span data-ttu-id="36457-486">Stream</span><span class="sxs-lookup"><span data-stu-id="36457-486">Stream</span></span>
- <span data-ttu-id="36457-487">string</span><span class="sxs-lookup"><span data-stu-id="36457-487">string</span></span>
- <span data-ttu-id="36457-488">Microsoft.Graph.DriveItem</span><span class="sxs-lookup"><span data-stu-id="36457-488">Microsoft.Graph.DriveItem</span></span>





<a name="outlook-output"></a>
## <a name="outlook-output"></a><span data-ttu-id="36457-489">Outlook output</span><span class="sxs-lookup"><span data-stu-id="36457-489">Outlook output</span></span>

<span data-ttu-id="36457-490">The Outlook message output binding sends a mail message through Outlook.</span><span class="sxs-lookup"><span data-stu-id="36457-490">The Outlook message output binding sends a mail message through Outlook.</span></span>

<span data-ttu-id="36457-491">This section contains the following subsections:</span><span class="sxs-lookup"><span data-stu-id="36457-491">This section contains the following subsections:</span></span>

* [<span data-ttu-id="36457-492">Example</span><span class="sxs-lookup"><span data-stu-id="36457-492">Example</span></span>](#outlook-output---example)
* [<span data-ttu-id="36457-493">Attributes</span><span class="sxs-lookup"><span data-stu-id="36457-493">Attributes</span></span>](#outlook-output---attributes)
* [<span data-ttu-id="36457-494">Configuration</span><span class="sxs-lookup"><span data-stu-id="36457-494">Configuration</span></span>](#outlook-output---configuration)
* [<span data-ttu-id="36457-495">Usage</span><span class="sxs-lookup"><span data-stu-id="36457-495">Usage</span></span>](#outlook-outnput---usage)

### <a name="outlook-output---example"></a><span data-ttu-id="36457-496">Outlook output - example</span><span class="sxs-lookup"><span data-stu-id="36457-496">Outlook output - example</span></span>

<span data-ttu-id="36457-497">See the language-specific example:</span><span class="sxs-lookup"><span data-stu-id="36457-497">See the language-specific example:</span></span>

* [<span data-ttu-id="36457-498">C# script (.csx)</span><span class="sxs-lookup"><span data-stu-id="36457-498">C# script (.csx)</span></span>](#outlook-output---c-script-example)
* [<span data-ttu-id="36457-499">JavaScript</span><span class="sxs-lookup"><span data-stu-id="36457-499">JavaScript</span></span>](#outlook-output---javascript-example)

#### <a name="outlook-output---c-script-example"></a><span data-ttu-id="36457-500">Outlook output - C# script example</span><span class="sxs-lookup"><span data-stu-id="36457-500">Outlook output - C# script example</span></span>

<span data-ttu-id="36457-501">The following example sends an email through Outlook.</span><span class="sxs-lookup"><span data-stu-id="36457-501">The following example sends an email through Outlook.</span></span>

<span data-ttu-id="36457-502">The *function.json* file defines an HTTP trigger with an Outlook message output binding:</span><span class="sxs-lookup"><span data-stu-id="36457-502">The *function.json* file defines an HTTP trigger with an Outlook message output binding:</span></span>

```json
{
  "bindings": [
    {
      "name": "req",
      "type": "httpTrigger",
      "direction": "in"
    },
    {
      "name": "message",
      "type": "outlook",
      "direction": "out",
      "identity": "userFromRequest"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="36457-503">The C# script code sends a mail from the caller to a recipient specified in the query string:</span><span class="sxs-lookup"><span data-stu-id="36457-503">The C# script code sends a mail from the caller to a recipient specified in the query string:</span></span>

```csharp
using System.Net;

public static void Run(HttpRequest req, out Message message, TraceWriter log)
{ 
    string emailAddress = req.Query["to"];
    message = new Message(){
        subject = "Greetings",
        body = "Sent from Azure Functions",
        recipient = new Recipient() {
            address = emailAddress
        }
    };
}

public class Message {
    public String subject {get; set;}
    public String body {get; set;}
    public Recipient recipient {get; set;}
}

public class Recipient {
    public String address {get; set;}
    public String name {get; set;}
}
```

#### <a name="outlook-output---javascript-example"></a><span data-ttu-id="36457-504">Outlook output - JavaScript example</span><span class="sxs-lookup"><span data-stu-id="36457-504">Outlook output - JavaScript example</span></span>

<span data-ttu-id="36457-505">The following example sends an email through Outlook.</span><span class="sxs-lookup"><span data-stu-id="36457-505">The following example sends an email through Outlook.</span></span>

<span data-ttu-id="36457-506">The *function.json* file defines an HTTP trigger with an Outlook message output binding:</span><span class="sxs-lookup"><span data-stu-id="36457-506">The *function.json* file defines an HTTP trigger with an Outlook message output binding:</span></span>

```json
{
  "bindings": [
    {
      "name": "req",
      "type": "httpTrigger",
      "direction": "in"
    },
    {
      "name": "message",
      "type": "outlook",
      "direction": "out",
      "identity": "userFromRequest"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="36457-507">The JavaScript code sends a mail from the caller to a recipient specified in the query string:</span><span class="sxs-lookup"><span data-stu-id="36457-507">The JavaScript code sends a mail from the caller to a recipient specified in the query string:</span></span>

```js
module.exports = function (context, req) {
    context.bindings.message = {
        subject: "Greetings",
        body: "Sent from Azure Functions with JavaScript",
        recipient: {
            address: req.query.to 
        } 
    };
    context.done();
};
```

### <a name="outlook-output---attributes"></a><span data-ttu-id="36457-508">Outlook output - attributes</span><span class="sxs-lookup"><span data-stu-id="36457-508">Outlook output - attributes</span></span>

<span data-ttu-id="36457-509">In [C# class libraries](functions-dotnet-class-library.md), use the [Outlook](https://github.com/Azure/azure-functions-microsoftgraph-extension/blob/master/src/MicrosoftGraphBinding/Bindings/OutlookAttribute.cs) attribute.</span><span class="sxs-lookup"><span data-stu-id="36457-509">In [C# class libraries](functions-dotnet-class-library.md), use the [Outlook](https://github.com/Azure/azure-functions-microsoftgraph-extension/blob/master/src/MicrosoftGraphBinding/Bindings/OutlookAttribute.cs) attribute.</span></span>

### <a name="outlook-output---configuration"></a><span data-ttu-id="36457-510">Outlook output - configuration</span><span class="sxs-lookup"><span data-stu-id="36457-510">Outlook output - configuration</span></span>

<span data-ttu-id="36457-511">The following table explains the binding configuration properties that you set in the *function.json* file and the `Outlook` attribute.</span><span class="sxs-lookup"><span data-stu-id="36457-511">The following table explains the binding configuration properties that you set in the *function.json* file and the `Outlook` attribute.</span></span>

|<span data-ttu-id="36457-512">function.json property</span><span class="sxs-lookup"><span data-stu-id="36457-512">function.json property</span></span> | <span data-ttu-id="36457-513">Attribute property</span><span class="sxs-lookup"><span data-stu-id="36457-513">Attribute property</span></span> |<span data-ttu-id="36457-514">Description</span><span class="sxs-lookup"><span data-stu-id="36457-514">Description</span></span>|
|---------|---------|----------------------|
|<span data-ttu-id="36457-515">**name**</span><span class="sxs-lookup"><span data-stu-id="36457-515">**name**</span></span>||<span data-ttu-id="36457-516">Required - the variable name used in function code for the mail message.</span><span class="sxs-lookup"><span data-stu-id="36457-516">Required - the variable name used in function code for the mail message.</span></span> <span data-ttu-id="36457-517">See [Using an Outlook message output binding from code](#outlook-output-code).</span><span class="sxs-lookup"><span data-stu-id="36457-517">See [Using an Outlook message output binding from code](#outlook-output-code).</span></span>|
|<span data-ttu-id="36457-518">**type**</span><span class="sxs-lookup"><span data-stu-id="36457-518">**type**</span></span>||<span data-ttu-id="36457-519">Required - must be set to `outlook`.</span><span class="sxs-lookup"><span data-stu-id="36457-519">Required - must be set to `outlook`.</span></span>|
|<span data-ttu-id="36457-520">**direction**</span><span class="sxs-lookup"><span data-stu-id="36457-520">**direction**</span></span>||<span data-ttu-id="36457-521">Required - must be set to `out`.</span><span class="sxs-lookup"><span data-stu-id="36457-521">Required - must be set to `out`.</span></span>|
|<span data-ttu-id="36457-522">**identity**</span><span class="sxs-lookup"><span data-stu-id="36457-522">**identity**</span></span>|<span data-ttu-id="36457-523">**Identity**</span><span class="sxs-lookup"><span data-stu-id="36457-523">**Identity**</span></span>|<span data-ttu-id="36457-524">Required - The identity that will be used to perform the action.</span><span class="sxs-lookup"><span data-stu-id="36457-524">Required - The identity that will be used to perform the action.</span></span> <span data-ttu-id="36457-525">Can be one of the following values:</span><span class="sxs-lookup"><span data-stu-id="36457-525">Can be one of the following values:</span></span><ul><li><span data-ttu-id="36457-526"><code>userFromRequest</code> - Only valid with [HTTP trigger].</span><span class="sxs-lookup"><span data-stu-id="36457-526"><code>userFromRequest</code> - Only valid with [HTTP trigger].</span></span> <span data-ttu-id="36457-527">Uses the identity of the calling user.</span><span class="sxs-lookup"><span data-stu-id="36457-527">Uses the identity of the calling user.</span></span></li><li><span data-ttu-id="36457-528"><code>userFromId</code> - Uses the identity of a previously logged-in user with the specified ID.</span><span class="sxs-lookup"><span data-stu-id="36457-528"><code>userFromId</code> - Uses the identity of a previously logged-in user with the specified ID.</span></span> <span data-ttu-id="36457-529">See the <code>userId</code> property.</span><span class="sxs-lookup"><span data-stu-id="36457-529">See the <code>userId</code> property.</span></span></li><li><span data-ttu-id="36457-530"><code>userFromToken</code> - Uses the identity represented by the specified token.</span><span class="sxs-lookup"><span data-stu-id="36457-530"><code>userFromToken</code> - Uses the identity represented by the specified token.</span></span> <span data-ttu-id="36457-531">See the <code>userToken</code> property.</span><span class="sxs-lookup"><span data-stu-id="36457-531">See the <code>userToken</code> property.</span></span></li><li><span data-ttu-id="36457-532"><code>clientCredentials</code> - Uses the identity of the function app.</span><span class="sxs-lookup"><span data-stu-id="36457-532"><code>clientCredentials</code> - Uses the identity of the function app.</span></span></li></ul>|
|<span data-ttu-id="36457-533">**userId**</span><span class="sxs-lookup"><span data-stu-id="36457-533">**userId**</span></span>|<span data-ttu-id="36457-534">**UserId**</span><span class="sxs-lookup"><span data-stu-id="36457-534">**UserId**</span></span>  |<span data-ttu-id="36457-535">Needed if and only if _identity_ is set to `userFromId`.</span><span class="sxs-lookup"><span data-stu-id="36457-535">Needed if and only if _identity_ is set to `userFromId`.</span></span> <span data-ttu-id="36457-536">A user principal ID associated with a previously logged-in user.</span><span class="sxs-lookup"><span data-stu-id="36457-536">A user principal ID associated with a previously logged-in user.</span></span>|
|<span data-ttu-id="36457-537">**userToken**</span><span class="sxs-lookup"><span data-stu-id="36457-537">**userToken**</span></span>|<span data-ttu-id="36457-538">**UserToken**</span><span class="sxs-lookup"><span data-stu-id="36457-538">**UserToken**</span></span>|<span data-ttu-id="36457-539">Needed if and only if _identity_ is set to `userFromToken`.</span><span class="sxs-lookup"><span data-stu-id="36457-539">Needed if and only if _identity_ is set to `userFromToken`.</span></span> <span data-ttu-id="36457-540">A token valid for the function app.</span><span class="sxs-lookup"><span data-stu-id="36457-540">A token valid for the function app.</span></span> |

<a name="outlook-output-code"></a>
### <a name="outlook-output---usage"></a><span data-ttu-id="36457-541">Outlook output - usage</span><span class="sxs-lookup"><span data-stu-id="36457-541">Outlook output - usage</span></span>

<span data-ttu-id="36457-542">This binding requires the following Azure AD permissions:</span><span class="sxs-lookup"><span data-stu-id="36457-542">This binding requires the following Azure AD permissions:</span></span>
|<span data-ttu-id="36457-543">Resource</span><span class="sxs-lookup"><span data-stu-id="36457-543">Resource</span></span>|<span data-ttu-id="36457-544">Permission</span><span class="sxs-lookup"><span data-stu-id="36457-544">Permission</span></span>|
|--------|--------|
|<span data-ttu-id="36457-545">Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="36457-545">Microsoft Graph</span></span>|<span data-ttu-id="36457-546">Send mail as user</span><span class="sxs-lookup"><span data-stu-id="36457-546">Send mail as user</span></span>|

<span data-ttu-id="36457-547">The binding exposes the following types to .NET functions:</span><span class="sxs-lookup"><span data-stu-id="36457-547">The binding exposes the following types to .NET functions:</span></span>
- <span data-ttu-id="36457-548">Microsoft.Graph.Message</span><span class="sxs-lookup"><span data-stu-id="36457-548">Microsoft.Graph.Message</span></span>
- <span data-ttu-id="36457-549">Newtonsoft.Json.Linq.JObject</span><span class="sxs-lookup"><span data-stu-id="36457-549">Newtonsoft.Json.Linq.JObject</span></span>
- <span data-ttu-id="36457-550">string</span><span class="sxs-lookup"><span data-stu-id="36457-550">string</span></span>
- <span data-ttu-id="36457-551">Custom object types (using structural model binding)</span><span class="sxs-lookup"><span data-stu-id="36457-551">Custom object types (using structural model binding)</span></span>






## <a name="webhooks"></a><span data-ttu-id="36457-552">Webhooks</span><span class="sxs-lookup"><span data-stu-id="36457-552">Webhooks</span></span>

<span data-ttu-id="36457-553">Webhooks allow you to react to events in the Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="36457-553">Webhooks allow you to react to events in the Microsoft Graph.</span></span> <span data-ttu-id="36457-554">To support webhooks, functions are needed to create, refresh, and react to _webhook subscriptions_.</span><span class="sxs-lookup"><span data-stu-id="36457-554">To support webhooks, functions are needed to create, refresh, and react to _webhook subscriptions_.</span></span> <span data-ttu-id="36457-555">A complete webhook solution requires a combination of the following bindings:</span><span class="sxs-lookup"><span data-stu-id="36457-555">A complete webhook solution requires a combination of the following bindings:</span></span>
- <span data-ttu-id="36457-556">A [Microsoft Graph webhook trigger](#webhook-trigger) allows you to react to an incoming webhook.</span><span class="sxs-lookup"><span data-stu-id="36457-556">A [Microsoft Graph webhook trigger](#webhook-trigger) allows you to react to an incoming webhook.</span></span>
- <span data-ttu-id="36457-557">A [Microsoft Graph webhook subscription input binding](#webhook-input) allows you to list existing subscriptions and optionally refresh them.</span><span class="sxs-lookup"><span data-stu-id="36457-557">A [Microsoft Graph webhook subscription input binding](#webhook-input) allows you to list existing subscriptions and optionally refresh them.</span></span>
- <span data-ttu-id="36457-558">A [Microsoft Graph webhook subscription output binding](#webhook-output) allows you to create or delete webhook subscriptions.</span><span class="sxs-lookup"><span data-stu-id="36457-558">A [Microsoft Graph webhook subscription output binding](#webhook-output) allows you to create or delete webhook subscriptions.</span></span>

<span data-ttu-id="36457-559">The bindings themselves do not require any Azure AD permissions, but you need to request permissions relevant to the resource type you wish to react to.</span><span class="sxs-lookup"><span data-stu-id="36457-559">The bindings themselves do not require any Azure AD permissions, but you need to request permissions relevant to the resource type you wish to react to.</span></span> <span data-ttu-id="36457-560">For a list of which permissions are needed for each resource type, see [subscription permissions](https://developer.microsoft.com/en-us/graph/docs/api-reference/v1.0/api/subscription_post_subscriptions).</span><span class="sxs-lookup"><span data-stu-id="36457-560">For a list of which permissions are needed for each resource type, see [subscription permissions](https://developer.microsoft.com/en-us/graph/docs/api-reference/v1.0/api/subscription_post_subscriptions).</span></span>

<span data-ttu-id="36457-561">For more information about webhooks, see [Working with webhooks in Microsoft Graph].</span><span class="sxs-lookup"><span data-stu-id="36457-561">For more information about webhooks, see [Working with webhooks in Microsoft Graph].</span></span>





## <a name="webhook-trigger"></a><span data-ttu-id="36457-562">Webhook trigger</span><span class="sxs-lookup"><span data-stu-id="36457-562">Webhook trigger</span></span>

<span data-ttu-id="36457-563">The Microsoft Graph webhook trigger allows a function to react to an incoming webhook from the Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="36457-563">The Microsoft Graph webhook trigger allows a function to react to an incoming webhook from the Microsoft Graph.</span></span> <span data-ttu-id="36457-564">Each instance of this trigger can react to one Microsoft Graph resource type.</span><span class="sxs-lookup"><span data-stu-id="36457-564">Each instance of this trigger can react to one Microsoft Graph resource type.</span></span>

<span data-ttu-id="36457-565">This section contains the following subsections:</span><span class="sxs-lookup"><span data-stu-id="36457-565">This section contains the following subsections:</span></span>

* [<span data-ttu-id="36457-566">Example</span><span class="sxs-lookup"><span data-stu-id="36457-566">Example</span></span>](#webhook-trigger---example)
* [<span data-ttu-id="36457-567">Attributes</span><span class="sxs-lookup"><span data-stu-id="36457-567">Attributes</span></span>](#webhook-trigger---attributes)
* [<span data-ttu-id="36457-568">Configuration</span><span class="sxs-lookup"><span data-stu-id="36457-568">Configuration</span></span>](#webhook-trigger---configuration)
* [<span data-ttu-id="36457-569">Usage</span><span class="sxs-lookup"><span data-stu-id="36457-569">Usage</span></span>](#webhook-trigger---usage)

### <a name="webhook-trigger---example"></a><span data-ttu-id="36457-570">Webhook trigger - example</span><span class="sxs-lookup"><span data-stu-id="36457-570">Webhook trigger - example</span></span>

<span data-ttu-id="36457-571">See the language-specific example:</span><span class="sxs-lookup"><span data-stu-id="36457-571">See the language-specific example:</span></span>

* [<span data-ttu-id="36457-572">C# script (.csx)</span><span class="sxs-lookup"><span data-stu-id="36457-572">C# script (.csx)</span></span>](#webhook-trigger---c-script-example)
* [<span data-ttu-id="36457-573">JavaScript</span><span class="sxs-lookup"><span data-stu-id="36457-573">JavaScript</span></span>](#webhook-trigger---javascript-example)

#### <a name="webhook-trigger---c-script-example"></a><span data-ttu-id="36457-574">Webhook trigger - C# script example</span><span class="sxs-lookup"><span data-stu-id="36457-574">Webhook trigger - C# script example</span></span>

<span data-ttu-id="36457-575">The following example handles webhooks for incoming Outlook messages.</span><span class="sxs-lookup"><span data-stu-id="36457-575">The following example handles webhooks for incoming Outlook messages.</span></span> <span data-ttu-id="36457-576">To use a webhook trigger you [create a subscription](#webhook-output---example), and you can [refresh the subscription](#webhook-subscription-refresh) to prevent it from expiring.</span><span class="sxs-lookup"><span data-stu-id="36457-576">To use a webhook trigger you [create a subscription](#webhook-output---example), and you can [refresh the subscription](#webhook-subscription-refresh) to prevent it from expiring.</span></span>

<span data-ttu-id="36457-577">The *function.json* file defines a webhook trigger:</span><span class="sxs-lookup"><span data-stu-id="36457-577">The *function.json* file defines a webhook trigger:</span></span>

```json
{
  "bindings": [
    {
      "name": "msg",
      "type": "GraphWebhookTrigger",
      "direction": "in",
      "resourceType": "#Microsoft.Graph.Message"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="36457-578">The C# script code reacts to incoming mail messages and logs the body of those sent by the recipient and containing "Azure Functions" in the subject:</span><span class="sxs-lookup"><span data-stu-id="36457-578">The C# script code reacts to incoming mail messages and logs the body of those sent by the recipient and containing "Azure Functions" in the subject:</span></span>

```csharp
#r "Microsoft.Graph"
using Microsoft.Graph;
using System.Net;

public static async Task Run(Message msg, TraceWriter log)  
{
    log.Info("Microsoft Graph webhook trigger function processed a request.");

    // Testable by sending oneself an email with the subject "Azure Functions" and some text body
    if (msg.Subject.Contains("Azure Functions") && msg.From.Equals(msg.Sender)) {
        log.Info($"Processed email: {msg.BodyPreview}");
    }
}
```

#### <a name="webhook-trigger---javascript-example"></a><span data-ttu-id="36457-579">Webhook trigger - JavaScript example</span><span class="sxs-lookup"><span data-stu-id="36457-579">Webhook trigger - JavaScript example</span></span>

<span data-ttu-id="36457-580">The following example handles webhooks for incoming Outlook messages.</span><span class="sxs-lookup"><span data-stu-id="36457-580">The following example handles webhooks for incoming Outlook messages.</span></span> <span data-ttu-id="36457-581">To use a webhook trigger you [create a subscription](#webhook-output---example), and you can [refresh the subscription](#webhook-subscription-refresh) to prevent it from expiring.</span><span class="sxs-lookup"><span data-stu-id="36457-581">To use a webhook trigger you [create a subscription](#webhook-output---example), and you can [refresh the subscription](#webhook-subscription-refresh) to prevent it from expiring.</span></span>

<span data-ttu-id="36457-582">The *function.json* file defines a webhook trigger:</span><span class="sxs-lookup"><span data-stu-id="36457-582">The *function.json* file defines a webhook trigger:</span></span>

```json
{
  "bindings": [
    {
      "name": "msg",
      "type": "GraphWebhookTrigger",
      "direction": "in",
      "resourceType": "#Microsoft.Graph.Message"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="36457-583">The JavaScript code reacts to incoming mail messages and logs the body of those sent by the recipient and containing "Azure Functions" in the subject:</span><span class="sxs-lookup"><span data-stu-id="36457-583">The JavaScript code reacts to incoming mail messages and logs the body of those sent by the recipient and containing "Azure Functions" in the subject:</span></span>

```js
module.exports = function (context) {
    context.log("Microsoft Graph webhook trigger function processed a request.");
    const msg = context.bindings.msg
    // Testable by sending oneself an email with the subject "Azure Functions" and some text body
    if((msg.subject.indexOf("Azure Functions") > -1) && (msg.from === msg.sender) ) {
      context.log(`Processed email: ${msg.bodyPreview}`);
    }
    context.done();
};
```

### <a name="webhook-trigger---attributes"></a><span data-ttu-id="36457-584">Webhook trigger - attributes</span><span class="sxs-lookup"><span data-stu-id="36457-584">Webhook trigger - attributes</span></span>

<span data-ttu-id="36457-585">In [C# class libraries](functions-dotnet-class-library.md), use the [GraphWebHookTrigger](https://github.com/Azure/azure-functions-microsoftgraph-extension/blob/master/src/MicrosoftGraphBinding/Bindings/GraphWebHookTriggerAttribute.cs) attribute.</span><span class="sxs-lookup"><span data-stu-id="36457-585">In [C# class libraries](functions-dotnet-class-library.md), use the [GraphWebHookTrigger](https://github.com/Azure/azure-functions-microsoftgraph-extension/blob/master/src/MicrosoftGraphBinding/Bindings/GraphWebHookTriggerAttribute.cs) attribute.</span></span>

### <a name="webhook-trigger---configuration"></a><span data-ttu-id="36457-586">Webhook trigger - configuration</span><span class="sxs-lookup"><span data-stu-id="36457-586">Webhook trigger - configuration</span></span>

<span data-ttu-id="36457-587">The following table explains the binding configuration properties that you set in the *function.json* file and the `GraphWebHookTrigger` attribute.</span><span class="sxs-lookup"><span data-stu-id="36457-587">The following table explains the binding configuration properties that you set in the *function.json* file and the `GraphWebHookTrigger` attribute.</span></span>

|<span data-ttu-id="36457-588">function.json property</span><span class="sxs-lookup"><span data-stu-id="36457-588">function.json property</span></span> | <span data-ttu-id="36457-589">Attribute property</span><span class="sxs-lookup"><span data-stu-id="36457-589">Attribute property</span></span> |<span data-ttu-id="36457-590">Description</span><span class="sxs-lookup"><span data-stu-id="36457-590">Description</span></span>|
|---------|---------|----------------------|
|<span data-ttu-id="36457-591">**name**</span><span class="sxs-lookup"><span data-stu-id="36457-591">**name**</span></span>||<span data-ttu-id="36457-592">Required - the variable name used in function code for the mail message.</span><span class="sxs-lookup"><span data-stu-id="36457-592">Required - the variable name used in function code for the mail message.</span></span> <span data-ttu-id="36457-593">See [Using an Outlook message output binding from code](#outlook-output-code).</span><span class="sxs-lookup"><span data-stu-id="36457-593">See [Using an Outlook message output binding from code](#outlook-output-code).</span></span>|
|<span data-ttu-id="36457-594">**type**</span><span class="sxs-lookup"><span data-stu-id="36457-594">**type**</span></span>||<span data-ttu-id="36457-595">Required - must be set to `graphWebhook`.</span><span class="sxs-lookup"><span data-stu-id="36457-595">Required - must be set to `graphWebhook`.</span></span>|
|<span data-ttu-id="36457-596">**direction**</span><span class="sxs-lookup"><span data-stu-id="36457-596">**direction**</span></span>||<span data-ttu-id="36457-597">Required - must be set to `trigger`.</span><span class="sxs-lookup"><span data-stu-id="36457-597">Required - must be set to `trigger`.</span></span>|
|<span data-ttu-id="36457-598">**resourceType**</span><span class="sxs-lookup"><span data-stu-id="36457-598">**resourceType**</span></span>|<span data-ttu-id="36457-599">**ResourceType**</span><span class="sxs-lookup"><span data-stu-id="36457-599">**ResourceType**</span></span>|<span data-ttu-id="36457-600">Required - the graph resource for which this function should respond to webhooks.</span><span class="sxs-lookup"><span data-stu-id="36457-600">Required - the graph resource for which this function should respond to webhooks.</span></span> <span data-ttu-id="36457-601">Can be one of the following values:</span><span class="sxs-lookup"><span data-stu-id="36457-601">Can be one of the following values:</span></span><ul><li><span data-ttu-id="36457-602"><code>#Microsoft.Graph.Message</code> - changes made to Outlook messages.</span><span class="sxs-lookup"><span data-stu-id="36457-602"><code>#Microsoft.Graph.Message</code> - changes made to Outlook messages.</span></span></li><li><span data-ttu-id="36457-603"><code>#Microsoft.Graph.DriveItem</code> - changes made to OneDrive root items.</span><span class="sxs-lookup"><span data-stu-id="36457-603"><code>#Microsoft.Graph.DriveItem</code> - changes made to OneDrive root items.</span></span></li><li><span data-ttu-id="36457-604"><code>#Microsoft.Graph.Contact</code> - changes made to personal contacts in Outlook.</span><span class="sxs-lookup"><span data-stu-id="36457-604"><code>#Microsoft.Graph.Contact</code> - changes made to personal contacts in Outlook.</span></span></li><li><span data-ttu-id="36457-605"><code>#Microsoft.Graph.Event</code> - changes made to Outlook calendar items.</span><span class="sxs-lookup"><span data-stu-id="36457-605"><code>#Microsoft.Graph.Event</code> - changes made to Outlook calendar items.</span></span></li></ul>|

> [!Note]
> <span data-ttu-id="36457-606">A function app can only have one function that is registered against a given `resourceType` value.</span><span class="sxs-lookup"><span data-stu-id="36457-606">A function app can only have one function that is registered against a given `resourceType` value.</span></span>

### <a name="webhook-trigger---usage"></a><span data-ttu-id="36457-607">Webhook trigger - usage</span><span class="sxs-lookup"><span data-stu-id="36457-607">Webhook trigger - usage</span></span>

<span data-ttu-id="36457-608">The binding exposes the following types to .NET functions:</span><span class="sxs-lookup"><span data-stu-id="36457-608">The binding exposes the following types to .NET functions:</span></span>
- <span data-ttu-id="36457-609">Microsoft Graph SDK types relevant to the resource type, such as `Microsoft.Graph.Message` or `Microsoft.Graph.DriveItem`.</span><span class="sxs-lookup"><span data-stu-id="36457-609">Microsoft Graph SDK types relevant to the resource type, such as `Microsoft.Graph.Message` or `Microsoft.Graph.DriveItem`.</span></span>
- <span data-ttu-id="36457-610">Custom object types (using structural model binding)</span><span class="sxs-lookup"><span data-stu-id="36457-610">Custom object types (using structural model binding)</span></span>




<a name="webhook-input"></a>
## <a name="webhook-input"></a><span data-ttu-id="36457-611">Webhook input</span><span class="sxs-lookup"><span data-stu-id="36457-611">Webhook input</span></span>

<span data-ttu-id="36457-612">The Microsoft Graph webhook input binding allows you to retrieve the list of subscriptions managed by this function app.</span><span class="sxs-lookup"><span data-stu-id="36457-612">The Microsoft Graph webhook input binding allows you to retrieve the list of subscriptions managed by this function app.</span></span> <span data-ttu-id="36457-613">The binding reads from function app storage, so it does not reflect other subscriptions created from outside the app.</span><span class="sxs-lookup"><span data-stu-id="36457-613">The binding reads from function app storage, so it does not reflect other subscriptions created from outside the app.</span></span>

<span data-ttu-id="36457-614">This section contains the following subsections:</span><span class="sxs-lookup"><span data-stu-id="36457-614">This section contains the following subsections:</span></span>

* [<span data-ttu-id="36457-615">Example</span><span class="sxs-lookup"><span data-stu-id="36457-615">Example</span></span>](#webhook-input---example)
* [<span data-ttu-id="36457-616">Attributes</span><span class="sxs-lookup"><span data-stu-id="36457-616">Attributes</span></span>](#webhook-input---attributes)
* [<span data-ttu-id="36457-617">Configuration</span><span class="sxs-lookup"><span data-stu-id="36457-617">Configuration</span></span>](#webhook-input---configuration)
* [<span data-ttu-id="36457-618">Usage</span><span class="sxs-lookup"><span data-stu-id="36457-618">Usage</span></span>](#webhook-input---usage)

### <a name="webhook-input---example"></a><span data-ttu-id="36457-619">Webhook input - example</span><span class="sxs-lookup"><span data-stu-id="36457-619">Webhook input - example</span></span>

<span data-ttu-id="36457-620">See the language-specific example:</span><span class="sxs-lookup"><span data-stu-id="36457-620">See the language-specific example:</span></span>

* [<span data-ttu-id="36457-621">C# script (.csx)</span><span class="sxs-lookup"><span data-stu-id="36457-621">C# script (.csx)</span></span>](#webhook-input---c-script-example)
* [<span data-ttu-id="36457-622">JavaScript</span><span class="sxs-lookup"><span data-stu-id="36457-622">JavaScript</span></span>](#webhook-input---javascript-example)

#### <a name="webhook-input---c-script-example"></a><span data-ttu-id="36457-623">Webhook input - C# script example</span><span class="sxs-lookup"><span data-stu-id="36457-623">Webhook input - C# script example</span></span>

<span data-ttu-id="36457-624">The following example gets all subscriptions for the calling user and deletes them.</span><span class="sxs-lookup"><span data-stu-id="36457-624">The following example gets all subscriptions for the calling user and deletes them.</span></span>

<span data-ttu-id="36457-625">The *function.json* file defines an HTTP trigger with a subscription input binding and a subscription output binding that uses the delete action:</span><span class="sxs-lookup"><span data-stu-id="36457-625">The *function.json* file defines an HTTP trigger with a subscription input binding and a subscription output binding that uses the delete action:</span></span>

```json
{
  "bindings": [
    {
      "name": "req",
      "type": "httpTrigger",
      "direction": "in"
    },
    {
      "type": "graphWebhookSubscription",
      "name": "existingSubscriptions",
      "direction": "in",
      "filter": "userFromRequest"
    },
    {
      "type": "graphWebhookSubscription",
      "name": "subscriptionsToDelete",
      "direction": "out",
      "action": "delete",
      "identity": "userFromRequest"
    },
    {
      "type": "http",
      "name": "res",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="36457-626">The C# script code gets the subscriptions and deletes them:</span><span class="sxs-lookup"><span data-stu-id="36457-626">The C# script code gets the subscriptions and deletes them:</span></span>

```csharp
using System.Net;

public static async Task Run(HttpRequest req, string[] existingSubscriptions, IAsyncCollector<string> subscriptionsToDelete, TraceWriter log)
{
    log.Info("C# HTTP trigger function processed a request.");
    foreach (var subscription in existingSubscriptions)
    {
        log.Info($"Deleting subscription {subscription}");
        await subscriptionsToDelete.AddAsync(subscription);
    }
}
```

#### <a name="webhook-input---javascript-example"></a><span data-ttu-id="36457-627">Webhook input - JavaScript example</span><span class="sxs-lookup"><span data-stu-id="36457-627">Webhook input - JavaScript example</span></span>

<span data-ttu-id="36457-628">The following example gets all subscriptions for the calling user and deletes them.</span><span class="sxs-lookup"><span data-stu-id="36457-628">The following example gets all subscriptions for the calling user and deletes them.</span></span>

<span data-ttu-id="36457-629">The *function.json* file defines an HTTP trigger with a subscription input binding and a subscription output binding that uses the delete action:</span><span class="sxs-lookup"><span data-stu-id="36457-629">The *function.json* file defines an HTTP trigger with a subscription input binding and a subscription output binding that uses the delete action:</span></span>

```json
{
  "bindings": [
    {
      "name": "req",
      "type": "httpTrigger",
      "direction": "in"
    },
    {
      "type": "graphWebhookSubscription",
      "name": "existingSubscriptions",
      "direction": "in",
      "filter": "userFromRequest"
    },
    {
      "type": "graphWebhookSubscription",
      "name": "subscriptionsToDelete",
      "direction": "out",
      "action": "delete",
      "identity": "userFromRequest"
    },
    {
      "type": "http",
      "name": "res",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="36457-630">The JavaScript code gets the subscriptions and deletes them:</span><span class="sxs-lookup"><span data-stu-id="36457-630">The JavaScript code gets the subscriptions and deletes them:</span></span>

```js
module.exports = function (context, req) {
    const existing = context.bindings.existingSubscriptions;
    var toDelete = [];
    for (var i = 0; i < existing.length; i++) {
        context.log(`Deleting subscription ${existing[i]}`);
        todelete.push(existing[i]);
    }
    context.bindings.subscriptionsToDelete = toDelete;
    context.done();
};
```

### <a name="webhook-input---attributes"></a><span data-ttu-id="36457-631">Webhook input - attributes</span><span class="sxs-lookup"><span data-stu-id="36457-631">Webhook input - attributes</span></span>

<span data-ttu-id="36457-632">In [C# class libraries](functions-dotnet-class-library.md), use the [GraphWebHookSubscription](https://github.com/Azure/azure-functions-microsoftgraph-extension/blob/master/src/MicrosoftGraphBinding/Bindings/GraphWebHookSubscriptionAttribute.cs) attribute.</span><span class="sxs-lookup"><span data-stu-id="36457-632">In [C# class libraries](functions-dotnet-class-library.md), use the [GraphWebHookSubscription](https://github.com/Azure/azure-functions-microsoftgraph-extension/blob/master/src/MicrosoftGraphBinding/Bindings/GraphWebHookSubscriptionAttribute.cs) attribute.</span></span>

### <a name="webhook-input---configuration"></a><span data-ttu-id="36457-633">Webhook input - configuration</span><span class="sxs-lookup"><span data-stu-id="36457-633">Webhook input - configuration</span></span>

<span data-ttu-id="36457-634">The following table explains the binding configuration properties that you set in the *function.json* file and the `GraphWebHookSubscription` attribute.</span><span class="sxs-lookup"><span data-stu-id="36457-634">The following table explains the binding configuration properties that you set in the *function.json* file and the `GraphWebHookSubscription` attribute.</span></span>

|<span data-ttu-id="36457-635">function.json property</span><span class="sxs-lookup"><span data-stu-id="36457-635">function.json property</span></span> | <span data-ttu-id="36457-636">Attribute property</span><span class="sxs-lookup"><span data-stu-id="36457-636">Attribute property</span></span> |<span data-ttu-id="36457-637">Description</span><span class="sxs-lookup"><span data-stu-id="36457-637">Description</span></span>|
|---------|---------|----------------------|
|<span data-ttu-id="36457-638">**name**</span><span class="sxs-lookup"><span data-stu-id="36457-638">**name**</span></span>||<span data-ttu-id="36457-639">Required - the variable name used in function code for the mail message.</span><span class="sxs-lookup"><span data-stu-id="36457-639">Required - the variable name used in function code for the mail message.</span></span> <span data-ttu-id="36457-640">See [Using an Outlook message output binding from code](#outlook-output-code).</span><span class="sxs-lookup"><span data-stu-id="36457-640">See [Using an Outlook message output binding from code](#outlook-output-code).</span></span>|
|<span data-ttu-id="36457-641">**type**</span><span class="sxs-lookup"><span data-stu-id="36457-641">**type**</span></span>||<span data-ttu-id="36457-642">Required - must be set to `graphWebhookSubscription`.</span><span class="sxs-lookup"><span data-stu-id="36457-642">Required - must be set to `graphWebhookSubscription`.</span></span>|
|<span data-ttu-id="36457-643">**direction**</span><span class="sxs-lookup"><span data-stu-id="36457-643">**direction**</span></span>||<span data-ttu-id="36457-644">Required - must be set to `in`.</span><span class="sxs-lookup"><span data-stu-id="36457-644">Required - must be set to `in`.</span></span>|
|<span data-ttu-id="36457-645">**filter**</span><span class="sxs-lookup"><span data-stu-id="36457-645">**filter**</span></span>|<span data-ttu-id="36457-646">**Filter**</span><span class="sxs-lookup"><span data-stu-id="36457-646">**Filter**</span></span>| <span data-ttu-id="36457-647">If set to `userFromRequest`, then the binding will only retrieve subscriptions owned by the calling user (valid only with [HTTP trigger]).</span><span class="sxs-lookup"><span data-stu-id="36457-647">If set to `userFromRequest`, then the binding will only retrieve subscriptions owned by the calling user (valid only with [HTTP trigger]).</span></span>| 

### <a name="webhook-input---usage"></a><span data-ttu-id="36457-648">Webhook input - usage</span><span class="sxs-lookup"><span data-stu-id="36457-648">Webhook input - usage</span></span>

<span data-ttu-id="36457-649">The binding exposes the following types to .NET functions:</span><span class="sxs-lookup"><span data-stu-id="36457-649">The binding exposes the following types to .NET functions:</span></span>
- <span data-ttu-id="36457-650">string[]</span><span class="sxs-lookup"><span data-stu-id="36457-650">string[]</span></span>
- <span data-ttu-id="36457-651">Custom object type arrays</span><span class="sxs-lookup"><span data-stu-id="36457-651">Custom object type arrays</span></span>
- <span data-ttu-id="36457-652">Newtonsoft.Json.Linq.JObject[]</span><span class="sxs-lookup"><span data-stu-id="36457-652">Newtonsoft.Json.Linq.JObject[]</span></span>
- <span data-ttu-id="36457-653">Microsoft.Graph.Subscription[]</span><span class="sxs-lookup"><span data-stu-id="36457-653">Microsoft.Graph.Subscription[]</span></span>





## <a name="webhook-output"></a><span data-ttu-id="36457-654">Webhook output</span><span class="sxs-lookup"><span data-stu-id="36457-654">Webhook output</span></span>

<span data-ttu-id="36457-655">The webhook subscription output binding allows you to create, delete, and refresh webhook subscriptions in the Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="36457-655">The webhook subscription output binding allows you to create, delete, and refresh webhook subscriptions in the Microsoft Graph.</span></span>

<span data-ttu-id="36457-656">This section contains the following subsections:</span><span class="sxs-lookup"><span data-stu-id="36457-656">This section contains the following subsections:</span></span>

* [<span data-ttu-id="36457-657">Example</span><span class="sxs-lookup"><span data-stu-id="36457-657">Example</span></span>](#webhook-output---example)
* [<span data-ttu-id="36457-658">Attributes</span><span class="sxs-lookup"><span data-stu-id="36457-658">Attributes</span></span>](#webhook-output---attributes)
* [<span data-ttu-id="36457-659">Configuration</span><span class="sxs-lookup"><span data-stu-id="36457-659">Configuration</span></span>](#webhook-output---configuration)
* [<span data-ttu-id="36457-660">Usage</span><span class="sxs-lookup"><span data-stu-id="36457-660">Usage</span></span>](#webhook-output---usage)

### <a name="webhook-output---example"></a><span data-ttu-id="36457-661">Webhook output - example</span><span class="sxs-lookup"><span data-stu-id="36457-661">Webhook output - example</span></span>

<span data-ttu-id="36457-662">See the language-specific example:</span><span class="sxs-lookup"><span data-stu-id="36457-662">See the language-specific example:</span></span>

* [<span data-ttu-id="36457-663">C# script (.csx)</span><span class="sxs-lookup"><span data-stu-id="36457-663">C# script (.csx)</span></span>](#webhook-output---c-script-example)
* [<span data-ttu-id="36457-664">JavaScript</span><span class="sxs-lookup"><span data-stu-id="36457-664">JavaScript</span></span>](#webhook-output---javascript-example)

#### <a name="webhook-output---c-script-example"></a><span data-ttu-id="36457-665">Webhook output - C# script example</span><span class="sxs-lookup"><span data-stu-id="36457-665">Webhook output - C# script example</span></span>

<span data-ttu-id="36457-666">The following example creates a subscription.</span><span class="sxs-lookup"><span data-stu-id="36457-666">The following example creates a subscription.</span></span> <span data-ttu-id="36457-667">You can [refresh the subscription](#webhook-subscription-refresh) to prevent it from expiring.</span><span class="sxs-lookup"><span data-stu-id="36457-667">You can [refresh the subscription](#webhook-subscription-refresh) to prevent it from expiring.</span></span>

<span data-ttu-id="36457-668">The *function.json* file defines an HTTP trigger with a subscription output binding using the create action:</span><span class="sxs-lookup"><span data-stu-id="36457-668">The *function.json* file defines an HTTP trigger with a subscription output binding using the create action:</span></span>

```json
{
  "bindings": [
    {
      "name": "req",
      "type": "httpTrigger",
      "direction": "in"
    },
    {
      "type": "graphWebhookSubscription",
      "name": "clientState",
      "direction": "out",
      "action": "create",
      "subscriptionResource": "me/mailFolders('Inbox')/messages",
      "changeTypes": [
        "created"
      ],
      "identity": "userFromRequest"
    },
    {
      "type": "http",
      "name": "$return",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="36457-669">The C# script code registers a webhook that will notify this function app when the calling user receives an Outlook message:</span><span class="sxs-lookup"><span data-stu-id="36457-669">The C# script code registers a webhook that will notify this function app when the calling user receives an Outlook message:</span></span>

```csharp
using System;
using System.Net;

public static HttpResponseMessage run(HttpRequestMessage req, out string clientState, TraceWriter log)
{
  log.Info("C# HTTP trigger function processed a request.");
    clientState = Guid.NewGuid().ToString();
    return new HttpResponseMessage(HttpStatusCode.OK);
}
```

#### <a name="webhook-output---javascript-example"></a><span data-ttu-id="36457-670">Webhook output - JavaScript example</span><span class="sxs-lookup"><span data-stu-id="36457-670">Webhook output - JavaScript example</span></span>

<span data-ttu-id="36457-671">The following example creates a subscription.</span><span class="sxs-lookup"><span data-stu-id="36457-671">The following example creates a subscription.</span></span> <span data-ttu-id="36457-672">You can [refresh the subscription](#webhook-subscription-refresh) to prevent it from expiring.</span><span class="sxs-lookup"><span data-stu-id="36457-672">You can [refresh the subscription](#webhook-subscription-refresh) to prevent it from expiring.</span></span>

<span data-ttu-id="36457-673">The *function.json* file defines an HTTP trigger with a subscription output binding using the create action:</span><span class="sxs-lookup"><span data-stu-id="36457-673">The *function.json* file defines an HTTP trigger with a subscription output binding using the create action:</span></span>

```json
{
  "bindings": [
    {
      "name": "req",
      "type": "httpTrigger",
      "direction": "in"
    },
    {
      "type": "graphWebhookSubscription",
      "name": "clientState",
      "direction": "out",
      "action": "create",
      "subscriptionResource": "me/mailFolders('Inbox')/messages",
      "changeTypes": [
        "created"
      ],
      "identity": "userFromRequest"
    },
    {
      "type": "http",
      "name": "$return",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="36457-674">The JavaScript code registers a webhook that will notify this function app when the calling user receives an Outlook message:</span><span class="sxs-lookup"><span data-stu-id="36457-674">The JavaScript code registers a webhook that will notify this function app when the calling user receives an Outlook message:</span></span>

```js
const uuidv4 = require('uuid/v4');

module.exports = function (context, req) {
    context.bindings.clientState = uuidv4();
    context.done();
};
```

### <a name="webhook-output---attributes"></a><span data-ttu-id="36457-675">Webhook output - attributes</span><span class="sxs-lookup"><span data-stu-id="36457-675">Webhook output - attributes</span></span>

<span data-ttu-id="36457-676">In [C# class libraries](functions-dotnet-class-library.md), use the [GraphWebHookSubscription](https://github.com/Azure/azure-functions-microsoftgraph-extension/blob/master/src/MicrosoftGraphBinding/Bindings/GraphWebHookSubscriptionAttribute.cs) attribute.</span><span class="sxs-lookup"><span data-stu-id="36457-676">In [C# class libraries](functions-dotnet-class-library.md), use the [GraphWebHookSubscription](https://github.com/Azure/azure-functions-microsoftgraph-extension/blob/master/src/MicrosoftGraphBinding/Bindings/GraphWebHookSubscriptionAttribute.cs) attribute.</span></span>

### <a name="webhook-output---configuration"></a><span data-ttu-id="36457-677">Webhook output - configuration</span><span class="sxs-lookup"><span data-stu-id="36457-677">Webhook output - configuration</span></span>

<span data-ttu-id="36457-678">The following table explains the binding configuration properties that you set in the *function.json* file and the `GraphWebHookSubscription` attribute.</span><span class="sxs-lookup"><span data-stu-id="36457-678">The following table explains the binding configuration properties that you set in the *function.json* file and the `GraphWebHookSubscription` attribute.</span></span>

|<span data-ttu-id="36457-679">function.json property</span><span class="sxs-lookup"><span data-stu-id="36457-679">function.json property</span></span> | <span data-ttu-id="36457-680">Attribute property</span><span class="sxs-lookup"><span data-stu-id="36457-680">Attribute property</span></span> |<span data-ttu-id="36457-681">Description</span><span class="sxs-lookup"><span data-stu-id="36457-681">Description</span></span>|
|---------|---------|----------------------|
|<span data-ttu-id="36457-682">**name**</span><span class="sxs-lookup"><span data-stu-id="36457-682">**name**</span></span>||<span data-ttu-id="36457-683">Required - the variable name used in function code for the mail message.</span><span class="sxs-lookup"><span data-stu-id="36457-683">Required - the variable name used in function code for the mail message.</span></span> <span data-ttu-id="36457-684">See [Using an Outlook message output binding from code](#outlook-output-code).</span><span class="sxs-lookup"><span data-stu-id="36457-684">See [Using an Outlook message output binding from code](#outlook-output-code).</span></span>|
|<span data-ttu-id="36457-685">**type**</span><span class="sxs-lookup"><span data-stu-id="36457-685">**type**</span></span>||<span data-ttu-id="36457-686">Required - must be set to `graphWebhookSubscription`.</span><span class="sxs-lookup"><span data-stu-id="36457-686">Required - must be set to `graphWebhookSubscription`.</span></span>|
|<span data-ttu-id="36457-687">**direction**</span><span class="sxs-lookup"><span data-stu-id="36457-687">**direction**</span></span>||<span data-ttu-id="36457-688">Required - must be set to `out`.</span><span class="sxs-lookup"><span data-stu-id="36457-688">Required - must be set to `out`.</span></span>|
|<span data-ttu-id="36457-689">**identity**</span><span class="sxs-lookup"><span data-stu-id="36457-689">**identity**</span></span>|<span data-ttu-id="36457-690">**Identity**</span><span class="sxs-lookup"><span data-stu-id="36457-690">**Identity**</span></span>|<span data-ttu-id="36457-691">Required - The identity that will be used to perform the action.</span><span class="sxs-lookup"><span data-stu-id="36457-691">Required - The identity that will be used to perform the action.</span></span> <span data-ttu-id="36457-692">Can be one of the following values:</span><span class="sxs-lookup"><span data-stu-id="36457-692">Can be one of the following values:</span></span><ul><li><span data-ttu-id="36457-693"><code>userFromRequest</code> - Only valid with [HTTP trigger].</span><span class="sxs-lookup"><span data-stu-id="36457-693"><code>userFromRequest</code> - Only valid with [HTTP trigger].</span></span> <span data-ttu-id="36457-694">Uses the identity of the calling user.</span><span class="sxs-lookup"><span data-stu-id="36457-694">Uses the identity of the calling user.</span></span></li><li><span data-ttu-id="36457-695"><code>userFromId</code> - Uses the identity of a previously logged-in user with the specified ID.</span><span class="sxs-lookup"><span data-stu-id="36457-695"><code>userFromId</code> - Uses the identity of a previously logged-in user with the specified ID.</span></span> <span data-ttu-id="36457-696">See the <code>userId</code> property.</span><span class="sxs-lookup"><span data-stu-id="36457-696">See the <code>userId</code> property.</span></span></li><li><span data-ttu-id="36457-697"><code>userFromToken</code> - Uses the identity represented by the specified token.</span><span class="sxs-lookup"><span data-stu-id="36457-697"><code>userFromToken</code> - Uses the identity represented by the specified token.</span></span> <span data-ttu-id="36457-698">See the <code>userToken</code> property.</span><span class="sxs-lookup"><span data-stu-id="36457-698">See the <code>userToken</code> property.</span></span></li><li><span data-ttu-id="36457-699"><code>clientCredentials</code> - Uses the identity of the function app.</span><span class="sxs-lookup"><span data-stu-id="36457-699"><code>clientCredentials</code> - Uses the identity of the function app.</span></span></li></ul>|
|<span data-ttu-id="36457-700">**userId**</span><span class="sxs-lookup"><span data-stu-id="36457-700">**userId**</span></span>|<span data-ttu-id="36457-701">**UserId**</span><span class="sxs-lookup"><span data-stu-id="36457-701">**UserId**</span></span>  |<span data-ttu-id="36457-702">Needed if and only if _identity_ is set to `userFromId`.</span><span class="sxs-lookup"><span data-stu-id="36457-702">Needed if and only if _identity_ is set to `userFromId`.</span></span> <span data-ttu-id="36457-703">A user principal ID associated with a previously logged-in user.</span><span class="sxs-lookup"><span data-stu-id="36457-703">A user principal ID associated with a previously logged-in user.</span></span>|
|<span data-ttu-id="36457-704">**userToken**</span><span class="sxs-lookup"><span data-stu-id="36457-704">**userToken**</span></span>|<span data-ttu-id="36457-705">**UserToken**</span><span class="sxs-lookup"><span data-stu-id="36457-705">**UserToken**</span></span>|<span data-ttu-id="36457-706">Needed if and only if _identity_ is set to `userFromToken`.</span><span class="sxs-lookup"><span data-stu-id="36457-706">Needed if and only if _identity_ is set to `userFromToken`.</span></span> <span data-ttu-id="36457-707">A token valid for the function app.</span><span class="sxs-lookup"><span data-stu-id="36457-707">A token valid for the function app.</span></span> |
|<span data-ttu-id="36457-708">**action**</span><span class="sxs-lookup"><span data-stu-id="36457-708">**action**</span></span>|<span data-ttu-id="36457-709">**Action**</span><span class="sxs-lookup"><span data-stu-id="36457-709">**Action**</span></span>|<span data-ttu-id="36457-710">Required - specifies the action the binding should perform.</span><span class="sxs-lookup"><span data-stu-id="36457-710">Required - specifies the action the binding should perform.</span></span> <span data-ttu-id="36457-711">Can be one of the following values:</span><span class="sxs-lookup"><span data-stu-id="36457-711">Can be one of the following values:</span></span><ul><li><span data-ttu-id="36457-712"><code>create</code> - Registers a new subscription.</span><span class="sxs-lookup"><span data-stu-id="36457-712"><code>create</code> - Registers a new subscription.</span></span></li><li><span data-ttu-id="36457-713"><code>delete</code> - Deletes a specified subscription.</span><span class="sxs-lookup"><span data-stu-id="36457-713"><code>delete</code> - Deletes a specified subscription.</span></span></li><li><span data-ttu-id="36457-714"><code>refresh</code> - Refreshes a specified subscription to keep it from expiring.</span><span class="sxs-lookup"><span data-stu-id="36457-714"><code>refresh</code> - Refreshes a specified subscription to keep it from expiring.</span></span></li></ul>|
|<span data-ttu-id="36457-715">**subscriptionResource**</span><span class="sxs-lookup"><span data-stu-id="36457-715">**subscriptionResource**</span></span>|<span data-ttu-id="36457-716">**SubscriptionResource**</span><span class="sxs-lookup"><span data-stu-id="36457-716">**SubscriptionResource**</span></span>|<span data-ttu-id="36457-717">Needed if and only if the _action_ is set to `create`.</span><span class="sxs-lookup"><span data-stu-id="36457-717">Needed if and only if the _action_ is set to `create`.</span></span> <span data-ttu-id="36457-718">Specifies the Microsoft Graph resource that will be monitored for changes.</span><span class="sxs-lookup"><span data-stu-id="36457-718">Specifies the Microsoft Graph resource that will be monitored for changes.</span></span> <span data-ttu-id="36457-719">See [Working with webhooks in Microsoft Graph].</span><span class="sxs-lookup"><span data-stu-id="36457-719">See [Working with webhooks in Microsoft Graph].</span></span> |
|<span data-ttu-id="36457-720">**changeType**</span><span class="sxs-lookup"><span data-stu-id="36457-720">**changeType**</span></span>|<span data-ttu-id="36457-721">**ChangeType**</span><span class="sxs-lookup"><span data-stu-id="36457-721">**ChangeType**</span></span>|<span data-ttu-id="36457-722">Needed if and only if the _action_ is set to `create`.</span><span class="sxs-lookup"><span data-stu-id="36457-722">Needed if and only if the _action_ is set to `create`.</span></span> <span data-ttu-id="36457-723">Indicates the type of change in the subscribed resource that will raise a notification.</span><span class="sxs-lookup"><span data-stu-id="36457-723">Indicates the type of change in the subscribed resource that will raise a notification.</span></span> <span data-ttu-id="36457-724">The supported values are: `created`, `updated`, `deleted`.</span><span class="sxs-lookup"><span data-stu-id="36457-724">The supported values are: `created`, `updated`, `deleted`.</span></span> <span data-ttu-id="36457-725">Multiple values can be combined using a comma-separated list.</span><span class="sxs-lookup"><span data-stu-id="36457-725">Multiple values can be combined using a comma-separated list.</span></span>|

### <a name="webhook-output---usage"></a><span data-ttu-id="36457-726">Webhook output - usage</span><span class="sxs-lookup"><span data-stu-id="36457-726">Webhook output - usage</span></span>

<span data-ttu-id="36457-727">The binding exposes the following types to .NET functions:</span><span class="sxs-lookup"><span data-stu-id="36457-727">The binding exposes the following types to .NET functions:</span></span>
- <span data-ttu-id="36457-728">string</span><span class="sxs-lookup"><span data-stu-id="36457-728">string</span></span>
- <span data-ttu-id="36457-729">Microsoft.Graph.Subscription</span><span class="sxs-lookup"><span data-stu-id="36457-729">Microsoft.Graph.Subscription</span></span>




<a name="webhook-examples"></a>
## <a name="webhook-subscription-refresh"></a><span data-ttu-id="36457-730">Webhook subscription refresh</span><span class="sxs-lookup"><span data-stu-id="36457-730">Webhook subscription refresh</span></span>

<span data-ttu-id="36457-731">There are two approaches to refreshing subscriptions:</span><span class="sxs-lookup"><span data-stu-id="36457-731">There are two approaches to refreshing subscriptions:</span></span>

- <span data-ttu-id="36457-732">Use the application identity to deal with all subscriptions.</span><span class="sxs-lookup"><span data-stu-id="36457-732">Use the application identity to deal with all subscriptions.</span></span> <span data-ttu-id="36457-733">This will require consent from an Azure Active Directory admin. This can be used by all languages supported by Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="36457-733">This will require consent from an Azure Active Directory admin. This can be used by all languages supported by Azure Functions.</span></span>
- <span data-ttu-id="36457-734">Use the identity associated with each subscription by manually binding each user ID.</span><span class="sxs-lookup"><span data-stu-id="36457-734">Use the identity associated with each subscription by manually binding each user ID.</span></span> <span data-ttu-id="36457-735">This will require some custom code to perform the binding.</span><span class="sxs-lookup"><span data-stu-id="36457-735">This will require some custom code to perform the binding.</span></span> <span data-ttu-id="36457-736">This can only be used by .NET functions.</span><span class="sxs-lookup"><span data-stu-id="36457-736">This can only be used by .NET functions.</span></span>

<span data-ttu-id="36457-737">This section contains an example for each of these approaches:</span><span class="sxs-lookup"><span data-stu-id="36457-737">This section contains an example for each of these approaches:</span></span>

* [<span data-ttu-id="36457-738">App identity example</span><span class="sxs-lookup"><span data-stu-id="36457-738">App identity example</span></span>](#webhook-subscription-refresh---app-identity-example)
* [<span data-ttu-id="36457-739">User identity example</span><span class="sxs-lookup"><span data-stu-id="36457-739">User identity example</span></span>](#webhook-subscription-refresh---user-identity-example)

### <a name="webhook-subscription-refresh---app-identity-example"></a><span data-ttu-id="36457-740">Webhook Subscription refresh - app identity example</span><span class="sxs-lookup"><span data-stu-id="36457-740">Webhook Subscription refresh - app identity example</span></span>

<span data-ttu-id="36457-741">See the language-specific example:</span><span class="sxs-lookup"><span data-stu-id="36457-741">See the language-specific example:</span></span>

* [<span data-ttu-id="36457-742">C# script (.csx)</span><span class="sxs-lookup"><span data-stu-id="36457-742">C# script (.csx)</span></span>](#app-identity-refresh---c-script-example)
* [<span data-ttu-id="36457-743">JavaScript</span><span class="sxs-lookup"><span data-stu-id="36457-743">JavaScript</span></span>](#app-identity-refresh---javascript-example)

### <a name="app-identity-refresh---c-script-example"></a><span data-ttu-id="36457-744">App identity refresh - C# script example</span><span class="sxs-lookup"><span data-stu-id="36457-744">App identity refresh - C# script example</span></span>

<span data-ttu-id="36457-745">The following example uses the application identity to refresh a subscription.</span><span class="sxs-lookup"><span data-stu-id="36457-745">The following example uses the application identity to refresh a subscription.</span></span>

<span data-ttu-id="36457-746">The *function.json* defines a timer trigger with a subscription input binding and a  subscription output binding:</span><span class="sxs-lookup"><span data-stu-id="36457-746">The *function.json* defines a timer trigger with a subscription input binding and a  subscription output binding:</span></span>

```json
{
  "bindings": [
    {
      "name": "myTimer",
      "type": "timerTrigger",
      "direction": "in",
      "schedule": "0 * * */2 * *"
    },
    {
      "type": "graphWebhookSubscription",
      "name": "existingSubscriptions",
      "direction": "in"
    },
    {
      "type": "graphWebhookSubscription",
      "name": "subscriptionsToRefresh",
      "direction": "out",
      "action": "refresh",
      "identity": "clientCredentials"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="36457-747">The C# script code refreshes the subscriptions:</span><span class="sxs-lookup"><span data-stu-id="36457-747">The C# script code refreshes the subscriptions:</span></span>

```csharp
using System;

public static void Run(TimerInfo myTimer, string[] existingSubscriptions, ICollector<string> subscriptionsToRefresh, TraceWriter log)
{
    // This template uses application permissions and requires consent from an Azure Active Directory admin.
    // See https://go.microsoft.com/fwlink/?linkid=858780
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
    foreach (var subscription in existingSubscriptions)
    {
      log.Info($"Refreshing subscription {subscription}");
      subscriptionsToRefresh.Add(subscription);
    }
}
```

### <a name="app-identity-refresh---c-script-example"></a><span data-ttu-id="36457-748">App identity refresh - C# script example</span><span class="sxs-lookup"><span data-stu-id="36457-748">App identity refresh - C# script example</span></span>

<span data-ttu-id="36457-749">The following example uses the application identity to refresh a subscription.</span><span class="sxs-lookup"><span data-stu-id="36457-749">The following example uses the application identity to refresh a subscription.</span></span>

<span data-ttu-id="36457-750">The *function.json* defines a timer trigger with a subscription input binding and a  subscription output binding:</span><span class="sxs-lookup"><span data-stu-id="36457-750">The *function.json* defines a timer trigger with a subscription input binding and a  subscription output binding:</span></span>

```json
{
  "bindings": [
    {
      "name": "myTimer",
      "type": "timerTrigger",
      "direction": "in",
      "schedule": "0 * * */2 * *"
    },
    {
      "type": "graphWebhookSubscription",
      "name": "existingSubscriptions",
      "direction": "in"
    },
    {
      "type": "graphWebhookSubscription",
      "name": "subscriptionsToRefresh",
      "direction": "out",
      "action": "refresh",
      "identity": "clientCredentials"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="36457-751">The JavaScript code refreshes the subscriptions:</span><span class="sxs-lookup"><span data-stu-id="36457-751">The JavaScript code refreshes the subscriptions:</span></span>

```js
// This template uses application permissions and requires consent from an Azure Active Directory admin.
// See https://go.microsoft.com/fwlink/?linkid=858780

module.exports = function (context) {
    const existing = context.bindings.existingSubscriptions;
    var toRefresh = [];
    for (var i = 0; i < existing.length; i++) {
        context.log(`Refreshing subscription ${existing[i]}`);
        toRefresh.push(existing[i]);
    }
    context.bindings.subscriptionsToRefresh = toRefresh;
    context.done();
};
```

### <a name="webhook-subscription-refresh---user-identity-example"></a><span data-ttu-id="36457-752">Webhook Subscription refresh - user identity example</span><span class="sxs-lookup"><span data-stu-id="36457-752">Webhook Subscription refresh - user identity example</span></span>

<span data-ttu-id="36457-753">The following example uses the user identity to refresh a subscription.</span><span class="sxs-lookup"><span data-stu-id="36457-753">The following example uses the user identity to refresh a subscription.</span></span>

<span data-ttu-id="36457-754">The *function.json* file defines a timer trigger and defers the subscription input binding to the function code:</span><span class="sxs-lookup"><span data-stu-id="36457-754">The *function.json* file defines a timer trigger and defers the subscription input binding to the function code:</span></span>

```json
{
  "bindings": [
    {
      "name": "myTimer",
      "type": "timerTrigger",
      "direction": "in",
      "schedule": "0 * * */2 * *"
    },
    {
      "type": "graphWebhookSubscription",
      "name": "existingSubscriptions",
      "direction": "in"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="36457-755">The C# script code refreshes the subscriptions and creates the output binding in code, using each user's identity:</span><span class="sxs-lookup"><span data-stu-id="36457-755">The C# script code refreshes the subscriptions and creates the output binding in code, using each user's identity:</span></span>

```csharp
using System;

public static async Task Run(TimerInfo myTimer, UserSubscription[] existingSubscriptions, IBinder binder, TraceWriter log)
{
  log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
    foreach (var subscription in existingSubscriptions)
    {
        // binding in code to allow dynamic identity
        using (var subscriptionsToRefresh = await binder.BindAsync<IAsyncCollector<string>>(
            new GraphWebhookSubscriptionAttribute() {
                Action = "refresh",
                Identity = "userFromId",
                UserId = subscription.UserId
            }
        ))
        {
            log.Info($"Refreshing subscription {subscription}");
            await subscriptionsToRefresh.AddAsync(subscription);
        }

    }
}

public class UserSubscription {
    public string UserId {get; set;}
    public string Id {get; set;}
}
```

## <a name="next-steps"></a><span data-ttu-id="36457-756">Next steps</span><span class="sxs-lookup"><span data-stu-id="36457-756">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="36457-757">Learn more about Azure functions triggers and bindings</span><span class="sxs-lookup"><span data-stu-id="36457-757">Learn more about Azure functions triggers and bindings</span></span>](functions-triggers-bindings.md)

[HTTP trigger]: functions-bindings-http-webhook.md
[Working with webhooks in Microsoft Graph]: https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/webhooks
