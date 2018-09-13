---
title: How to delegate user registration and product subscription
description: Learn how to delegate user registration and product subscription to a third party in Azure API Management.
services: api-management
documentationcenter: ''
author: antonba
manager: erikre
editor: ''
ms.assetid: 8b7ad5ee-a873-4966-a400-7e508bbbe158
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: b5d5ea002cbde6f448b7ad2d24b3104678f320c2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549846"
---
# <a name="how-to-delegate-user-registration-and-product-subscription"></a><span data-ttu-id="0e38c-103">How to delegate user registration and product subscription</span><span class="sxs-lookup"><span data-stu-id="0e38c-103">How to delegate user registration and product subscription</span></span>
<span data-ttu-id="0e38c-104">Delegation allows you to use your existing website for handling developer sign-in/sign-up and subscription to products as opposed to using the built-in functionality in the developer portal.</span><span class="sxs-lookup"><span data-stu-id="0e38c-104">Delegation allows you to use your existing website for handling developer sign-in/sign-up and subscription to products as opposed to using the built-in functionality in the developer portal.</span></span> <span data-ttu-id="0e38c-105">This enables your website to own the user data and perform the validation of these steps in a custom way.</span><span class="sxs-lookup"><span data-stu-id="0e38c-105">This enables your website to own the user data and perform the validation of these steps in a custom way.</span></span>

## <span data-ttu-id="0e38c-106"><a name="delegate-signin-up"> </a>Delegating developer sign-in and sign-up</span><span class="sxs-lookup"><span data-stu-id="0e38c-106"><a name="delegate-signin-up"> </a>Delegating developer sign-in and sign-up</span></span>
<span data-ttu-id="0e38c-107">To delegate developer sign-in and sign-up to your existing website you will need to create a special delegation endpoint on your site that acts as the entry-point for any such request initiated from the API Management developer portal.</span><span class="sxs-lookup"><span data-stu-id="0e38c-107">To delegate developer sign-in and sign-up to your existing website you will need to create a special delegation endpoint on your site that acts as the entry-point for any such request initiated from the API Management developer portal.</span></span>

<span data-ttu-id="0e38c-108">The final workflow will be as follows:</span><span class="sxs-lookup"><span data-stu-id="0e38c-108">The final workflow will be as follows:</span></span>

1. <span data-ttu-id="0e38c-109">Developer clicks on the sign-in or sign-up link at the API Management developer portal</span><span class="sxs-lookup"><span data-stu-id="0e38c-109">Developer clicks on the sign-in or sign-up link at the API Management developer portal</span></span>
2. <span data-ttu-id="0e38c-110">Browser is redirected to the delegation endpoint</span><span class="sxs-lookup"><span data-stu-id="0e38c-110">Browser is redirected to the delegation endpoint</span></span>
3. <span data-ttu-id="0e38c-111">Delegation endpoint in return redirects to or presents UI asking user to sign-in or sign-up</span><span class="sxs-lookup"><span data-stu-id="0e38c-111">Delegation endpoint in return redirects to or presents UI asking user to sign-in or sign-up</span></span>
4. <span data-ttu-id="0e38c-112">On success, the user is redirected back to the API Management developer portal page they started from</span><span class="sxs-lookup"><span data-stu-id="0e38c-112">On success, the user is redirected back to the API Management developer portal page they started from</span></span>

<span data-ttu-id="0e38c-113">To begin, let's first set-up API Management to route requests via your delegation endpoint.</span><span class="sxs-lookup"><span data-stu-id="0e38c-113">To begin, let's first set-up API Management to route requests via your delegation endpoint.</span></span> <span data-ttu-id="0e38c-114">In the API Management publisher portal, click on **Security** and then click the **Delegation** tab. Click the checkbox to enable 'Delegate sign-in & sign-up'.</span><span class="sxs-lookup"><span data-stu-id="0e38c-114">In the API Management publisher portal, click on **Security** and then click the **Delegation** tab. Click the checkbox to enable 'Delegate sign-in & sign-up'.</span></span>

![Delegation page][api-management-delegation-signin-up]

* <span data-ttu-id="0e38c-116">Decide what the URL of your special delegation endpoint will be and enter it in the **Delegation endpoint URL** field.</span><span class="sxs-lookup"><span data-stu-id="0e38c-116">Decide what the URL of your special delegation endpoint will be and enter it in the **Delegation endpoint URL** field.</span></span> 
* <span data-ttu-id="0e38c-117">Within the **Delegation authentication key** field enter a secret that will be used to compute a signature provided to you for verification to ensure that the request is indeed coming from Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="0e38c-117">Within the **Delegation authentication key** field enter a secret that will be used to compute a signature provided to you for verification to ensure that the request is indeed coming from Azure API Management.</span></span> <span data-ttu-id="0e38c-118">You can click the **generate** button to have API Managemnet randomly generate a key for you.</span><span class="sxs-lookup"><span data-stu-id="0e38c-118">You can click the **generate** button to have API Managemnet randomly generate a key for you.</span></span>

<span data-ttu-id="0e38c-119">Now you need to create the **delegation endpoint**.</span><span class="sxs-lookup"><span data-stu-id="0e38c-119">Now you need to create the **delegation endpoint**.</span></span> <span data-ttu-id="0e38c-120">It has to perform a number of actions:</span><span class="sxs-lookup"><span data-stu-id="0e38c-120">It has to perform a number of actions:</span></span>

1. <span data-ttu-id="0e38c-121">Receive a request in the following form:</span><span class="sxs-lookup"><span data-stu-id="0e38c-121">Receive a request in the following form:</span></span>
   
   > <span data-ttu-id="0e38c-122">*http://www.yourwebsite.com/apimdelegation?operation=SignIn&returnUrl={URL of source page}&salt={string}&sig={string}*</span><span class="sxs-lookup"><span data-stu-id="0e38c-122">*http://www.yourwebsite.com/apimdelegation?operation=SignIn&returnUrl={URL of source page}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="0e38c-123">Query parameters for the sign-in / sign-up case:</span><span class="sxs-lookup"><span data-stu-id="0e38c-123">Query parameters for the sign-in / sign-up case:</span></span>
   
   * <span data-ttu-id="0e38c-124">**operation**: identifies what type of delegation request it is - it can only be **SignIn** in this case</span><span class="sxs-lookup"><span data-stu-id="0e38c-124">**operation**: identifies what type of delegation request it is - it can only be **SignIn** in this case</span></span>
   * <span data-ttu-id="0e38c-125">**returnUrl**: the URL of the page where the user clicked on a sign-in or sign-up link</span><span class="sxs-lookup"><span data-stu-id="0e38c-125">**returnUrl**: the URL of the page where the user clicked on a sign-in or sign-up link</span></span>
   * <span data-ttu-id="0e38c-126">**salt**: a special salt string used for computing a security hash</span><span class="sxs-lookup"><span data-stu-id="0e38c-126">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="0e38c-127">**sig**: a computed security hash to be used for comparison to your own computed hash</span><span class="sxs-lookup"><span data-stu-id="0e38c-127">**sig**: a computed security hash to be used for comparison to your own computed hash</span></span>
2. <span data-ttu-id="0e38c-128">Verify that the request is coming from Azure API Management (optional, but highly recommended for security)</span><span class="sxs-lookup"><span data-stu-id="0e38c-128">Verify that the request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="0e38c-129">Compute an HMAC-SHA512 hash of a string based on the **returnUrl** and **salt** query parameters ([example code provided below]):</span><span class="sxs-lookup"><span data-stu-id="0e38c-129">Compute an HMAC-SHA512 hash of a string based on the **returnUrl** and **salt** query parameters ([example code provided below]):</span></span>
     
     > <span data-ttu-id="0e38c-130">HMAC(**salt** + '\n' + **returnUrl**)</span><span class="sxs-lookup"><span data-stu-id="0e38c-130">HMAC(**salt** + '\n' + **returnUrl**)</span></span>
     > 
     > 
   * <span data-ttu-id="0e38c-131">Compare the above-computed hash to the value of the **sig** query parameter.</span><span class="sxs-lookup"><span data-stu-id="0e38c-131">Compare the above-computed hash to the value of the **sig** query parameter.</span></span> <span data-ttu-id="0e38c-132">If the two hashes match, move on to the next step, otherwise deny the request.</span><span class="sxs-lookup"><span data-stu-id="0e38c-132">If the two hashes match, move on to the next step, otherwise deny the request.</span></span>
3. <span data-ttu-id="0e38c-133">Verify that you are receiving a request for sign-in/sign-up: the **operation** query parameter will be set to "**SignIn**".</span><span class="sxs-lookup"><span data-stu-id="0e38c-133">Verify that you are receiving a request for sign-in/sign-up: the **operation** query parameter will be set to "**SignIn**".</span></span>
4. <span data-ttu-id="0e38c-134">Present the user with UI to sign-in or sign-up</span><span class="sxs-lookup"><span data-stu-id="0e38c-134">Present the user with UI to sign-in or sign-up</span></span>
5. <span data-ttu-id="0e38c-135">If the user is signing-up you have to create a corresponding account for them in API Management.</span><span class="sxs-lookup"><span data-stu-id="0e38c-135">If the user is signing-up you have to create a corresponding account for them in API Management.</span></span> <span data-ttu-id="0e38c-136">[Create a user] with the API Management REST API.</span><span class="sxs-lookup"><span data-stu-id="0e38c-136">[Create a user] with the API Management REST API.</span></span> <span data-ttu-id="0e38c-137">When doing so, ensure that you set the user ID to the same it is in your user store or to an ID that you can keep track of.</span><span class="sxs-lookup"><span data-stu-id="0e38c-137">When doing so, ensure that you set the user ID to the same it is in your user store or to an ID that you can keep track of.</span></span>
6. <span data-ttu-id="0e38c-138">When the user is successfully authenticated:</span><span class="sxs-lookup"><span data-stu-id="0e38c-138">When the user is successfully authenticated:</span></span>
   
   * <span data-ttu-id="0e38c-139">[request a single-sign-on (SSO) token] via the API Management REST API</span><span class="sxs-lookup"><span data-stu-id="0e38c-139">[request a single-sign-on (SSO) token] via the API Management REST API</span></span>
   * <span data-ttu-id="0e38c-140">append a returnUrl query parameter to the SSO URL you have received from the API call above:</span><span class="sxs-lookup"><span data-stu-id="0e38c-140">append a returnUrl query parameter to the SSO URL you have received from the API call above:</span></span>
     
     > <span data-ttu-id="0e38c-141">e.g. https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span><span class="sxs-lookup"><span data-stu-id="0e38c-141">e.g. https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span></span> 
     > 
     > 
   * <span data-ttu-id="0e38c-142">redirect the user to the above produced URL</span><span class="sxs-lookup"><span data-stu-id="0e38c-142">redirect the user to the above produced URL</span></span>

<span data-ttu-id="0e38c-143">In addition to the **SignIn** operation, you can also perform account management by following the previous steps and using one of the following operations.</span><span class="sxs-lookup"><span data-stu-id="0e38c-143">In addition to the **SignIn** operation, you can also perform account management by following the previous steps and using one of the following operations.</span></span>

* <span data-ttu-id="0e38c-144">**ChangePassword**</span><span class="sxs-lookup"><span data-stu-id="0e38c-144">**ChangePassword**</span></span>
* <span data-ttu-id="0e38c-145">**ChangeProfile**</span><span class="sxs-lookup"><span data-stu-id="0e38c-145">**ChangeProfile**</span></span>
* <span data-ttu-id="0e38c-146">**CloseAccount**</span><span class="sxs-lookup"><span data-stu-id="0e38c-146">**CloseAccount**</span></span>

<span data-ttu-id="0e38c-147">You must pass the following query parameters for account management operations.</span><span class="sxs-lookup"><span data-stu-id="0e38c-147">You must pass the following query parameters for account management operations.</span></span>

* <span data-ttu-id="0e38c-148">**operation**: identifies what type of delegation request it is (ChangePassword, ChangeProfile, or CloseAccount)</span><span class="sxs-lookup"><span data-stu-id="0e38c-148">**operation**: identifies what type of delegation request it is (ChangePassword, ChangeProfile, or CloseAccount)</span></span>
* <span data-ttu-id="0e38c-149">**userId**: the user id of the account to manage</span><span class="sxs-lookup"><span data-stu-id="0e38c-149">**userId**: the user id of the account to manage</span></span>
* <span data-ttu-id="0e38c-150">**salt**: a special salt string used for computing a security hash</span><span class="sxs-lookup"><span data-stu-id="0e38c-150">**salt**: a special salt string used for computing a security hash</span></span>
* <span data-ttu-id="0e38c-151">**sig**: a computed security hash to be used for comparison to your own computed hash</span><span class="sxs-lookup"><span data-stu-id="0e38c-151">**sig**: a computed security hash to be used for comparison to your own computed hash</span></span>

## <span data-ttu-id="0e38c-152"><a name="delegate-product-subscription"> </a>Delegating product subscription</span><span class="sxs-lookup"><span data-stu-id="0e38c-152"><a name="delegate-product-subscription"> </a>Delegating product subscription</span></span>
<span data-ttu-id="0e38c-153">Delegating product subscription works similarly to delegating user sign-in/-up.</span><span class="sxs-lookup"><span data-stu-id="0e38c-153">Delegating product subscription works similarly to delegating user sign-in/-up.</span></span> <span data-ttu-id="0e38c-154">The final workflow would be as follows:</span><span class="sxs-lookup"><span data-stu-id="0e38c-154">The final workflow would be as follows:</span></span>

1. <span data-ttu-id="0e38c-155">Developer selects a product in the API Management developer portal and clicks on the Subscribe button</span><span class="sxs-lookup"><span data-stu-id="0e38c-155">Developer selects a product in the API Management developer portal and clicks on the Subscribe button</span></span>
2. <span data-ttu-id="0e38c-156">Browser is redirected to the delegation endpoint</span><span class="sxs-lookup"><span data-stu-id="0e38c-156">Browser is redirected to the delegation endpoint</span></span>
3. <span data-ttu-id="0e38c-157">Delegation endpoint performs required product subscription steps - this is up to you and may entail redirecting to another page to request billing information, asking additional questions, or simply storing the information and not requiring any user action</span><span class="sxs-lookup"><span data-stu-id="0e38c-157">Delegation endpoint performs required product subscription steps - this is up to you and may entail redirecting to another page to request billing information, asking additional questions, or simply storing the information and not requiring any user action</span></span>

<span data-ttu-id="0e38c-158">To enable the functionality, on the **Delegation** page click **Delegate product subscription**.</span><span class="sxs-lookup"><span data-stu-id="0e38c-158">To enable the functionality, on the **Delegation** page click **Delegate product subscription**.</span></span>

<span data-ttu-id="0e38c-159">Then ensure the delegation endpoint performs the following actions:</span><span class="sxs-lookup"><span data-stu-id="0e38c-159">Then ensure the delegation endpoint performs the following actions:</span></span>

1. <span data-ttu-id="0e38c-160">Receive a request in the following form:</span><span class="sxs-lookup"><span data-stu-id="0e38c-160">Receive a request in the following form:</span></span>
   
   > <span data-ttu-id="0e38c-161">*http://www.yourwebsite.com/apimdelegation?operation={operation}&productId={product to subscribe to}&userId={user making request}&salt={string}&sig={string}*</span><span class="sxs-lookup"><span data-stu-id="0e38c-161">*http://www.yourwebsite.com/apimdelegation?operation={operation}&productId={product to subscribe to}&userId={user making request}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="0e38c-162">Query parameters for the product subscription case:</span><span class="sxs-lookup"><span data-stu-id="0e38c-162">Query parameters for the product subscription case:</span></span>
   
   * <span data-ttu-id="0e38c-163">**operation**: identifies what type of delegation request it is.</span><span class="sxs-lookup"><span data-stu-id="0e38c-163">**operation**: identifies what type of delegation request it is.</span></span> <span data-ttu-id="0e38c-164">For product subscription requests the valid options are:</span><span class="sxs-lookup"><span data-stu-id="0e38c-164">For product subscription requests the valid options are:</span></span>
     * <span data-ttu-id="0e38c-165">"Subscribe": a request to subscribe the user to a given product with provided ID (see below)</span><span class="sxs-lookup"><span data-stu-id="0e38c-165">"Subscribe": a request to subscribe the user to a given product with provided ID (see below)</span></span>
     * <span data-ttu-id="0e38c-166">"Unsubscribe": a request to unsubscribe a user from a product</span><span class="sxs-lookup"><span data-stu-id="0e38c-166">"Unsubscribe": a request to unsubscribe a user from a product</span></span>
     * <span data-ttu-id="0e38c-167">"Renew": a requst to renew a subscription (e.g. that may be expiring)</span><span class="sxs-lookup"><span data-stu-id="0e38c-167">"Renew": a requst to renew a subscription (e.g. that may be expiring)</span></span>
   * <span data-ttu-id="0e38c-168">**productId**: the ID of the product the user requested to subscribe to</span><span class="sxs-lookup"><span data-stu-id="0e38c-168">**productId**: the ID of the product the user requested to subscribe to</span></span>
   * <span data-ttu-id="0e38c-169">**userId**: the ID of the user for whom the request is made</span><span class="sxs-lookup"><span data-stu-id="0e38c-169">**userId**: the ID of the user for whom the request is made</span></span>
   * <span data-ttu-id="0e38c-170">**salt**: a special salt string used for computing a security hash</span><span class="sxs-lookup"><span data-stu-id="0e38c-170">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="0e38c-171">**sig**: a computed security hash to be used for comparison to your own computed hash</span><span class="sxs-lookup"><span data-stu-id="0e38c-171">**sig**: a computed security hash to be used for comparison to your own computed hash</span></span>
2. <span data-ttu-id="0e38c-172">Verify that the request is coming from Azure API Management (optional, but highly recommended for security)</span><span class="sxs-lookup"><span data-stu-id="0e38c-172">Verify that the request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="0e38c-173">Compute an HMAC-SHA512 of a string based on the **productId**, **userId** and **salt** query parameters:</span><span class="sxs-lookup"><span data-stu-id="0e38c-173">Compute an HMAC-SHA512 of a string based on the **productId**, **userId** and **salt** query parameters:</span></span>
     
     > <span data-ttu-id="0e38c-174">HMAC(**salt** + '\n' + **productId** + '\n' + **userId**)</span><span class="sxs-lookup"><span data-stu-id="0e38c-174">HMAC(**salt** + '\n' + **productId** + '\n' + **userId**)</span></span>
     > 
     > 
   * <span data-ttu-id="0e38c-175">Compare the above-computed hash to the value of the **sig** query parameter.</span><span class="sxs-lookup"><span data-stu-id="0e38c-175">Compare the above-computed hash to the value of the **sig** query parameter.</span></span> <span data-ttu-id="0e38c-176">If the two hashes match, move on to the next step, otherwise deny the request.</span><span class="sxs-lookup"><span data-stu-id="0e38c-176">If the two hashes match, move on to the next step, otherwise deny the request.</span></span>
3. <span data-ttu-id="0e38c-177">Perform any product subscription processing based on the type of operation requested in **operation** - e.g. billing, further questions, etc.</span><span class="sxs-lookup"><span data-stu-id="0e38c-177">Perform any product subscription processing based on the type of operation requested in **operation** - e.g. billing, further questions, etc.</span></span>
4. <span data-ttu-id="0e38c-178">On successfully subscribing the user to the product on your side, subscribe the user to the API Management product by [calling the REST API for product subscription].</span><span class="sxs-lookup"><span data-stu-id="0e38c-178">On successfully subscribing the user to the product on your side, subscribe the user to the API Management product by [calling the REST API for product subscription].</span></span>

## <span data-ttu-id="0e38c-179"><a name="delegate-example-code"> </a> Example Code</span><span class="sxs-lookup"><span data-stu-id="0e38c-179"><a name="delegate-example-code"> </a> Example Code</span></span>
<span data-ttu-id="0e38c-180">These code samples show how to take the *delegation validation key*, which is set in the Delegation screen of the publisher portal, to create a HMAC which is then used to validate the signature, proving the validity of the passed returnUrl.</span><span class="sxs-lookup"><span data-stu-id="0e38c-180">These code samples show how to take the *delegation validation key*, which is set in the Delegation screen of the publisher portal, to create a HMAC which is then used to validate the signature, proving the validity of the passed returnUrl.</span></span> <span data-ttu-id="0e38c-181">The same code works for the productId and userId with slight modification.</span><span class="sxs-lookup"><span data-stu-id="0e38c-181">The same code works for the productId and userId with slight modification.</span></span>

<span data-ttu-id="0e38c-182">**C# code to generate hash of returnUrl**</span><span class="sxs-lookup"><span data-stu-id="0e38c-182">**C# code to generate hash of returnUrl**</span></span>

```c#
using System.Security.Cryptography;

string key = "delegation validation key";
string returnUrl = "returnUrl query parameter";
string salt = "salt query parameter";
string signature;
using (var encoder = new HMACSHA512(Convert.FromBase64String(key)))
{
    signature = Convert.ToBase64String(encoder.ComputeHash(Encoding.UTF8.GetBytes(salt + "\n" + returnUrl)));
    // change to (salt + "\n" + productId + "\n" + userId) when delegating product subscription
    // compare signature to sig query parameter
}
```

<span data-ttu-id="0e38c-183">**NodeJS code to generate hash of returnUrl**</span><span class="sxs-lookup"><span data-stu-id="0e38c-183">**NodeJS code to generate hash of returnUrl**</span></span>

```
var crypto = require('crypto');

var key = 'delegation validation key'; 
var returnUrl = 'returnUrl query parameter';
var salt = 'salt query parameter';

var hmac = crypto.createHmac('sha512', new Buffer(key, 'base64'));
var digest = hmac.update(salt + '\n' + returnUrl).digest();
// change to (salt + "\n" + productId + "\n" + userId) when delegating product subscription
// compare signature to sig query parameter

var signature = digest.toString('base64');
```

## <a name="next-steps"></a><span data-ttu-id="0e38c-184">Next steps</span><span class="sxs-lookup"><span data-stu-id="0e38c-184">Next steps</span></span>
<span data-ttu-id="0e38c-185">For more information on delegation, see the following video.</span><span class="sxs-lookup"><span data-stu-id="0e38c-185">For more information on delegation, see the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Delegating-User-Authentication-and-Product-Subscription-to-a-3rd-Party-Site/player]
> 
> 

[Delegating developer sign-in and sign-up]: #delegate-signin-up
[Delegating product subscription]: #delegate-product-subscription
[request a single-sign-on (SSO) token]: http://go.microsoft.com/fwlink/?LinkId=507409
[create a user]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser
[calling the REST API for product subscription]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO
[Next steps]: #next-steps
[example code provided below]: #delegate-example-code

[api-management-delegation-signin-up]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-setup-delegation/api-management-delegation-signin-up.png 

