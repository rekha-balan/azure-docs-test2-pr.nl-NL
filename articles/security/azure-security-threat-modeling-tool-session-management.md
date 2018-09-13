---
title: Session Management - Microsoft Threat Modeling Tool - Azure | Microsoft Docs
description: mitigations for threats exposed in the Threat Modeling Tool
services: security
documentationcenter: na
author: jegeib
manager: jegeib
editor: jegeib
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/07/2017
ms.author: jegeib
ms.openlocfilehash: 97953779f1132d89c7ad07abdb4e08c0f476f4b9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44779173"
---
# <a name="security-frame-session-management"></a><span data-ttu-id="dfb5b-103">Security Frame: Session Management</span><span class="sxs-lookup"><span data-stu-id="dfb5b-103">Security Frame: Session Management</span></span>
| <span data-ttu-id="dfb5b-104">Product/Service</span><span class="sxs-lookup"><span data-stu-id="dfb5b-104">Product/Service</span></span> | <span data-ttu-id="dfb5b-105">Article</span><span class="sxs-lookup"><span data-stu-id="dfb5b-105">Article</span></span> |
| --------------- | ------- |
| <span data-ttu-id="dfb5b-106">**Azure AD**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-106">**Azure AD**</span></span>    | <ul><li>[<span data-ttu-id="dfb5b-107">Implement proper logout using ADAL methods when using Azure AD</span><span class="sxs-lookup"><span data-stu-id="dfb5b-107">Implement proper logout using ADAL methods when using Azure AD</span></span>](#logout-adal)</li></ul> |
| <span data-ttu-id="dfb5b-108">IoT Device</span><span class="sxs-lookup"><span data-stu-id="dfb5b-108">IoT Device</span></span> | <ul><li>[<span data-ttu-id="dfb5b-109">Use finite lifetimes for generated SaS tokens</span><span class="sxs-lookup"><span data-stu-id="dfb5b-109">Use finite lifetimes for generated SaS tokens</span></span>](#finite-tokens)</li></ul> |
| <span data-ttu-id="dfb5b-110">**Azure Document DB**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-110">**Azure Document DB**</span></span> | <ul><li>[<span data-ttu-id="dfb5b-111">Use minimum token lifetimes for generated Resource tokens</span><span class="sxs-lookup"><span data-stu-id="dfb5b-111">Use minimum token lifetimes for generated Resource tokens</span></span>](#resource-tokens)</li></ul> |
| <span data-ttu-id="dfb5b-112">**ADFS**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-112">**ADFS**</span></span> | <ul><li>[<span data-ttu-id="dfb5b-113">Implement proper logout using WsFederation methods when using ADFS</span><span class="sxs-lookup"><span data-stu-id="dfb5b-113">Implement proper logout using WsFederation methods when using ADFS</span></span>](#wsfederation-logout)</li></ul> |
| <span data-ttu-id="dfb5b-114">**Identity Server**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-114">**Identity Server**</span></span> | <ul><li>[<span data-ttu-id="dfb5b-115">Implement proper logout when using Identity Server</span><span class="sxs-lookup"><span data-stu-id="dfb5b-115">Implement proper logout when using Identity Server</span></span>](#proper-logout)</li></ul> |
| <span data-ttu-id="dfb5b-116">**Web Application**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-116">**Web Application**</span></span> | <ul><li>[<span data-ttu-id="dfb5b-117">Applications available over HTTPS must use secure cookies</span><span class="sxs-lookup"><span data-stu-id="dfb5b-117">Applications available over HTTPS must use secure cookies</span></span>](#https-secure-cookies)</li><li>[<span data-ttu-id="dfb5b-118">All http based application should specify http only for cookie definition</span><span class="sxs-lookup"><span data-stu-id="dfb5b-118">All http based application should specify http only for cookie definition</span></span>](#cookie-definition)</li><li>[<span data-ttu-id="dfb5b-119">Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET web pages</span><span class="sxs-lookup"><span data-stu-id="dfb5b-119">Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET web pages</span></span>](#csrf-asp)</li><li>[<span data-ttu-id="dfb5b-120">Set up session for inactivity lifetime</span><span class="sxs-lookup"><span data-stu-id="dfb5b-120">Set up session for inactivity lifetime</span></span>](#inactivity-lifetime)</li><li>[<span data-ttu-id="dfb5b-121">Implement proper logout from the application</span><span class="sxs-lookup"><span data-stu-id="dfb5b-121">Implement proper logout from the application</span></span>](#proper-app-logout)</li></ul> |
| <span data-ttu-id="dfb5b-122">**Web API**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-122">**Web API**</span></span> | <ul><li>[<span data-ttu-id="dfb5b-123">Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET Web APIs</span><span class="sxs-lookup"><span data-stu-id="dfb5b-123">Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET Web APIs</span></span>](#csrf-api)</li></ul> |

## <a id="logout-adal"></a><span data-ttu-id="dfb5b-124">Implement proper logout using ADAL methods when using Azure AD</span><span class="sxs-lookup"><span data-stu-id="dfb5b-124">Implement proper logout using ADAL methods when using Azure AD</span></span>

| <span data-ttu-id="dfb5b-125">Title</span><span class="sxs-lookup"><span data-stu-id="dfb5b-125">Title</span></span>                   | <span data-ttu-id="dfb5b-126">Details</span><span class="sxs-lookup"><span data-stu-id="dfb5b-126">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="dfb5b-127">**Component**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-127">**Component**</span></span>               | <span data-ttu-id="dfb5b-128">Azure AD</span><span class="sxs-lookup"><span data-stu-id="dfb5b-128">Azure AD</span></span> | 
| <span data-ttu-id="dfb5b-129">**SDL Phase**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-129">**SDL Phase**</span></span>               | <span data-ttu-id="dfb5b-130">Build</span><span class="sxs-lookup"><span data-stu-id="dfb5b-130">Build</span></span> |  
| <span data-ttu-id="dfb5b-131">**Applicable Technologies**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-131">**Applicable Technologies**</span></span> | <span data-ttu-id="dfb5b-132">Generic</span><span class="sxs-lookup"><span data-stu-id="dfb5b-132">Generic</span></span> |
| <span data-ttu-id="dfb5b-133">**Attributes**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-133">**Attributes**</span></span>              | <span data-ttu-id="dfb5b-134">N/A</span><span class="sxs-lookup"><span data-stu-id="dfb5b-134">N/A</span></span>  |
| <span data-ttu-id="dfb5b-135">**References**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-135">**References**</span></span>              | <span data-ttu-id="dfb5b-136">N/A</span><span class="sxs-lookup"><span data-stu-id="dfb5b-136">N/A</span></span>  |
| <span data-ttu-id="dfb5b-137">**Steps**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-137">**Steps**</span></span> | <span data-ttu-id="dfb5b-138">If the application relies on access token issued by Azure AD, the logout event handler should call</span><span class="sxs-lookup"><span data-stu-id="dfb5b-138">If the application relies on access token issued by Azure AD, the logout event handler should call</span></span> |

### <a name="example"></a><span data-ttu-id="dfb5b-139">Example</span><span class="sxs-lookup"><span data-stu-id="dfb5b-139">Example</span></span>
```csharp
HttpContext.GetOwinContext().Authentication.SignOut(OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType)
```

### <a name="example"></a><span data-ttu-id="dfb5b-140">Example</span><span class="sxs-lookup"><span data-stu-id="dfb5b-140">Example</span></span>
<span data-ttu-id="dfb5b-141">It should also destroy user's session by calling Session.Abandon() method.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-141">It should also destroy user's session by calling Session.Abandon() method.</span></span> <span data-ttu-id="dfb5b-142">Following method shows secure implementation of user logout:</span><span class="sxs-lookup"><span data-stu-id="dfb5b-142">Following method shows secure implementation of user logout:</span></span>
```csharp
    [HttpPost]
        [ValidateAntiForgeryToken]
        public void LogOff()
        {
            string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
            AuthenticationContext authContext = new AuthenticationContext(Authority + TenantId, new NaiveSessionCache(userObjectID));
            authContext.TokenCache.Clear();
            Session.Clear();
            Session.Abandon();
            Response.SetCookie(new HttpCookie("ASP.NET_SessionId", string.Empty));
            HttpContext.GetOwinContext().Authentication.SignOut(
                OpenIdConnectAuthenticationDefaults.AuthenticationType,
                CookieAuthenticationDefaults.AuthenticationType);
        } 
```

## <a id="finite-tokens"></a><span data-ttu-id="dfb5b-143">Use finite lifetimes for generated SaS tokens</span><span class="sxs-lookup"><span data-stu-id="dfb5b-143">Use finite lifetimes for generated SaS tokens</span></span>

| <span data-ttu-id="dfb5b-144">Title</span><span class="sxs-lookup"><span data-stu-id="dfb5b-144">Title</span></span>                   | <span data-ttu-id="dfb5b-145">Details</span><span class="sxs-lookup"><span data-stu-id="dfb5b-145">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="dfb5b-146">**Component**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-146">**Component**</span></span>               | <span data-ttu-id="dfb5b-147">IoT Device</span><span class="sxs-lookup"><span data-stu-id="dfb5b-147">IoT Device</span></span> | 
| <span data-ttu-id="dfb5b-148">**SDL Phase**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-148">**SDL Phase**</span></span>               | <span data-ttu-id="dfb5b-149">Build</span><span class="sxs-lookup"><span data-stu-id="dfb5b-149">Build</span></span> |  
| <span data-ttu-id="dfb5b-150">**Applicable Technologies**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-150">**Applicable Technologies**</span></span> | <span data-ttu-id="dfb5b-151">Generic</span><span class="sxs-lookup"><span data-stu-id="dfb5b-151">Generic</span></span> |
| <span data-ttu-id="dfb5b-152">**Attributes**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-152">**Attributes**</span></span>              | <span data-ttu-id="dfb5b-153">N/A</span><span class="sxs-lookup"><span data-stu-id="dfb5b-153">N/A</span></span>  |
| <span data-ttu-id="dfb5b-154">**References**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-154">**References**</span></span>              | <span data-ttu-id="dfb5b-155">N/A</span><span class="sxs-lookup"><span data-stu-id="dfb5b-155">N/A</span></span>  |
| <span data-ttu-id="dfb5b-156">**Steps**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-156">**Steps**</span></span> | <span data-ttu-id="dfb5b-157">SaS tokens generated for authenticating to Azure IoT Hub should have a finite expiry period.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-157">SaS tokens generated for authenticating to Azure IoT Hub should have a finite expiry period.</span></span> <span data-ttu-id="dfb5b-158">Keep the SaS token lifetimes to a minimum to limit the amount of time they can be replayed in case the tokens are compromised.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-158">Keep the SaS token lifetimes to a minimum to limit the amount of time they can be replayed in case the tokens are compromised.</span></span>|

## <a id="resource-tokens"></a><span data-ttu-id="dfb5b-159">Use minimum token lifetimes for generated Resource tokens</span><span class="sxs-lookup"><span data-stu-id="dfb5b-159">Use minimum token lifetimes for generated Resource tokens</span></span>

| <span data-ttu-id="dfb5b-160">Title</span><span class="sxs-lookup"><span data-stu-id="dfb5b-160">Title</span></span>                   | <span data-ttu-id="dfb5b-161">Details</span><span class="sxs-lookup"><span data-stu-id="dfb5b-161">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="dfb5b-162">**Component**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-162">**Component**</span></span>               | <span data-ttu-id="dfb5b-163">Azure Document DB</span><span class="sxs-lookup"><span data-stu-id="dfb5b-163">Azure Document DB</span></span> | 
| <span data-ttu-id="dfb5b-164">**SDL Phase**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-164">**SDL Phase**</span></span>               | <span data-ttu-id="dfb5b-165">Build</span><span class="sxs-lookup"><span data-stu-id="dfb5b-165">Build</span></span> |  
| <span data-ttu-id="dfb5b-166">**Applicable Technologies**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-166">**Applicable Technologies**</span></span> | <span data-ttu-id="dfb5b-167">Generic</span><span class="sxs-lookup"><span data-stu-id="dfb5b-167">Generic</span></span> |
| <span data-ttu-id="dfb5b-168">**Attributes**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-168">**Attributes**</span></span>              | <span data-ttu-id="dfb5b-169">N/A</span><span class="sxs-lookup"><span data-stu-id="dfb5b-169">N/A</span></span>  |
| <span data-ttu-id="dfb5b-170">**References**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-170">**References**</span></span>              | <span data-ttu-id="dfb5b-171">N/A</span><span class="sxs-lookup"><span data-stu-id="dfb5b-171">N/A</span></span>  |
| <span data-ttu-id="dfb5b-172">**Steps**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-172">**Steps**</span></span> | <span data-ttu-id="dfb5b-173">Reduce the timespan of resource token to a minimum value required.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-173">Reduce the timespan of resource token to a minimum value required.</span></span> <span data-ttu-id="dfb5b-174">Resource tokens have a default valid timespan of 1 hour.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-174">Resource tokens have a default valid timespan of 1 hour.</span></span>|

## <a id="wsfederation-logout"></a><span data-ttu-id="dfb5b-175">Implement proper logout using WsFederation methods when using ADFS</span><span class="sxs-lookup"><span data-stu-id="dfb5b-175">Implement proper logout using WsFederation methods when using ADFS</span></span>

| <span data-ttu-id="dfb5b-176">Title</span><span class="sxs-lookup"><span data-stu-id="dfb5b-176">Title</span></span>                   | <span data-ttu-id="dfb5b-177">Details</span><span class="sxs-lookup"><span data-stu-id="dfb5b-177">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="dfb5b-178">**Component**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-178">**Component**</span></span>               | <span data-ttu-id="dfb5b-179">ADFS</span><span class="sxs-lookup"><span data-stu-id="dfb5b-179">ADFS</span></span> | 
| <span data-ttu-id="dfb5b-180">**SDL Phase**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-180">**SDL Phase**</span></span>               | <span data-ttu-id="dfb5b-181">Build</span><span class="sxs-lookup"><span data-stu-id="dfb5b-181">Build</span></span> |  
| <span data-ttu-id="dfb5b-182">**Applicable Technologies**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-182">**Applicable Technologies**</span></span> | <span data-ttu-id="dfb5b-183">Generic</span><span class="sxs-lookup"><span data-stu-id="dfb5b-183">Generic</span></span> |
| <span data-ttu-id="dfb5b-184">**Attributes**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-184">**Attributes**</span></span>              | <span data-ttu-id="dfb5b-185">N/A</span><span class="sxs-lookup"><span data-stu-id="dfb5b-185">N/A</span></span>  |
| <span data-ttu-id="dfb5b-186">**References**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-186">**References**</span></span>              | <span data-ttu-id="dfb5b-187">N/A</span><span class="sxs-lookup"><span data-stu-id="dfb5b-187">N/A</span></span>  |
| <span data-ttu-id="dfb5b-188">**Steps**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-188">**Steps**</span></span> | <span data-ttu-id="dfb5b-189">If the application relies on STS token issued by ADFS, the logout event handler should call WSFederationAuthenticationModule.FederatedSignOut() method to log out the user.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-189">If the application relies on STS token issued by ADFS, the logout event handler should call WSFederationAuthenticationModule.FederatedSignOut() method to log out the user.</span></span> <span data-ttu-id="dfb5b-190">Also the current session should be destroyed, and the session token value should be reset and nullified.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-190">Also the current session should be destroyed, and the session token value should be reset and nullified.</span></span>|

### <a name="example"></a><span data-ttu-id="dfb5b-191">Example</span><span class="sxs-lookup"><span data-stu-id="dfb5b-191">Example</span></span>
```csharp
        [HttpPost, ValidateAntiForgeryToken]
        [Authorization]
        public ActionResult SignOut(string redirectUrl)
        {
            if (!this.User.Identity.IsAuthenticated)
            {
                return this.View("LogOff", null);
            }

            // Removes the user profile.
            this.Session.Clear();
            this.Session.Abandon();
            HttpContext.Current.Response.Cookies.Add(new System.Web.HttpCookie("ASP.NET_SessionId", string.Empty)
                {
                    Expires = DateTime.Now.AddDays(-1D),
                    Secure = true,
                    HttpOnly = true
                });

            // Signs out at the specified security token service (STS) by using the WS-Federation protocol.
            Uri signOutUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Issuer);
            Uri replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm);
            if (!string.IsNullOrEmpty(redirectUrl))
            {
                replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm + redirectUrl);
            }
           //     Signs out of the current session and raises the appropriate events.
            var authModule = FederatedAuthentication.WSFederationAuthenticationModule;
            authModule.SignOut(false);
        //     Signs out at the specified security token service (STS) by using the WS-Federation
        //     protocol.            
            WSFederationAuthenticationModule.FederatedSignOut(signOutUrl, replyUrl);
            return new RedirectResult(redirectUrl);
        }
```

## <a id="proper-logout"></a><span data-ttu-id="dfb5b-192">Implement proper logout when using Identity Server</span><span class="sxs-lookup"><span data-stu-id="dfb5b-192">Implement proper logout when using Identity Server</span></span>

| <span data-ttu-id="dfb5b-193">Title</span><span class="sxs-lookup"><span data-stu-id="dfb5b-193">Title</span></span>                   | <span data-ttu-id="dfb5b-194">Details</span><span class="sxs-lookup"><span data-stu-id="dfb5b-194">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="dfb5b-195">**Component**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-195">**Component**</span></span>               | <span data-ttu-id="dfb5b-196">Identity Server</span><span class="sxs-lookup"><span data-stu-id="dfb5b-196">Identity Server</span></span> | 
| <span data-ttu-id="dfb5b-197">**SDL Phase**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-197">**SDL Phase**</span></span>               | <span data-ttu-id="dfb5b-198">Build</span><span class="sxs-lookup"><span data-stu-id="dfb5b-198">Build</span></span> |  
| <span data-ttu-id="dfb5b-199">**Applicable Technologies**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-199">**Applicable Technologies**</span></span> | <span data-ttu-id="dfb5b-200">Generic</span><span class="sxs-lookup"><span data-stu-id="dfb5b-200">Generic</span></span> |
| <span data-ttu-id="dfb5b-201">**Attributes**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-201">**Attributes**</span></span>              | <span data-ttu-id="dfb5b-202">N/A</span><span class="sxs-lookup"><span data-stu-id="dfb5b-202">N/A</span></span>  |
| <span data-ttu-id="dfb5b-203">**References**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-203">**References**</span></span>              | [<span data-ttu-id="dfb5b-204">IdentityServer3-Federated sign out</span><span class="sxs-lookup"><span data-stu-id="dfb5b-204">IdentityServer3-Federated sign out</span></span>](https://identityserver.github.io/Documentation/docsv2/advanced/federated-signout.html) |
| <span data-ttu-id="dfb5b-205">**Steps**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-205">**Steps**</span></span> | <span data-ttu-id="dfb5b-206">IdentityServer supports the ability to federate with external identity providers.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-206">IdentityServer supports the ability to federate with external identity providers.</span></span> <span data-ttu-id="dfb5b-207">When a user signs out of an upstream identity provider, depending upon the protocol used, it might be possible to receive a notification when the user signs out. It allows IdentityServer to notify its clients so they can also sign the user out. Check the documentation in the references section for the implementation details.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-207">When a user signs out of an upstream identity provider, depending upon the protocol used, it might be possible to receive a notification when the user signs out. It allows IdentityServer to notify its clients so they can also sign the user out. Check the documentation in the references section for the implementation details.</span></span>|

## <a id="https-secure-cookies"></a><span data-ttu-id="dfb5b-208">Applications available over HTTPS must use secure cookies</span><span class="sxs-lookup"><span data-stu-id="dfb5b-208">Applications available over HTTPS must use secure cookies</span></span>

| <span data-ttu-id="dfb5b-209">Title</span><span class="sxs-lookup"><span data-stu-id="dfb5b-209">Title</span></span>                   | <span data-ttu-id="dfb5b-210">Details</span><span class="sxs-lookup"><span data-stu-id="dfb5b-210">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="dfb5b-211">**Component**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-211">**Component**</span></span>               | <span data-ttu-id="dfb5b-212">Web Application</span><span class="sxs-lookup"><span data-stu-id="dfb5b-212">Web Application</span></span> | 
| <span data-ttu-id="dfb5b-213">**SDL Phase**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-213">**SDL Phase**</span></span>               | <span data-ttu-id="dfb5b-214">Build</span><span class="sxs-lookup"><span data-stu-id="dfb5b-214">Build</span></span> |  
| <span data-ttu-id="dfb5b-215">**Applicable Technologies**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-215">**Applicable Technologies**</span></span> | <span data-ttu-id="dfb5b-216">Generic</span><span class="sxs-lookup"><span data-stu-id="dfb5b-216">Generic</span></span> |
| <span data-ttu-id="dfb5b-217">**Attributes**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-217">**Attributes**</span></span>              | <span data-ttu-id="dfb5b-218">EnvironmentType - OnPrem</span><span class="sxs-lookup"><span data-stu-id="dfb5b-218">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="dfb5b-219">**References**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-219">**References**</span></span>              | <span data-ttu-id="dfb5b-220">[httpCookies Element (ASP.NET Settings Schema)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [HttpCookie.Secure Property](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx)</span><span class="sxs-lookup"><span data-stu-id="dfb5b-220">[httpCookies Element (ASP.NET Settings Schema)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [HttpCookie.Secure Property](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx)</span></span> |
| <span data-ttu-id="dfb5b-221">**Steps**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-221">**Steps**</span></span> | <span data-ttu-id="dfb5b-222">Cookies are normally only accessible to the domain for which they were scoped.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-222">Cookies are normally only accessible to the domain for which they were scoped.</span></span> <span data-ttu-id="dfb5b-223">Unfortunately, the definition of "domain" does not include the protocol so cookies that are created over HTTPS are accessible over HTTP.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-223">Unfortunately, the definition of "domain" does not include the protocol so cookies that are created over HTTPS are accessible over HTTP.</span></span> <span data-ttu-id="dfb5b-224">The "secure" attribute indicates to the browser that the cookie should only be made available over HTTPS.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-224">The "secure" attribute indicates to the browser that the cookie should only be made available over HTTPS.</span></span> <span data-ttu-id="dfb5b-225">Ensure that all cookies set over HTTPS use the **secure** attribute.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-225">Ensure that all cookies set over HTTPS use the **secure** attribute.</span></span> <span data-ttu-id="dfb5b-226">The requirement can be enforced in the web.config file by setting the requireSSL attribute to true.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-226">The requirement can be enforced in the web.config file by setting the requireSSL attribute to true.</span></span> <span data-ttu-id="dfb5b-227">It is the preferred approach because it will enforce the **secure** attribute for all current and future cookies without the need to make any additional code changes.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-227">It is the preferred approach because it will enforce the **secure** attribute for all current and future cookies without the need to make any additional code changes.</span></span>|

### <a name="example"></a><span data-ttu-id="dfb5b-228">Example</span><span class="sxs-lookup"><span data-stu-id="dfb5b-228">Example</span></span>
```csharp
<configuration>
  <system.web>
    <httpCookies requireSSL="true"/>
  </system.web>
</configuration>
```
<span data-ttu-id="dfb5b-229">The setting is enforced even if HTTP is used to access the application.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-229">The setting is enforced even if HTTP is used to access the application.</span></span> <span data-ttu-id="dfb5b-230">If HTTP is used to access the application, the setting breaks the application because the cookies are set with the secure attribute and the browser will not send them back to the application.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-230">If HTTP is used to access the application, the setting breaks the application because the cookies are set with the secure attribute and the browser will not send them back to the application.</span></span>

| <span data-ttu-id="dfb5b-231">Title</span><span class="sxs-lookup"><span data-stu-id="dfb5b-231">Title</span></span>                   | <span data-ttu-id="dfb5b-232">Details</span><span class="sxs-lookup"><span data-stu-id="dfb5b-232">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="dfb5b-233">**Component**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-233">**Component**</span></span>               | <span data-ttu-id="dfb5b-234">Web Application</span><span class="sxs-lookup"><span data-stu-id="dfb5b-234">Web Application</span></span> | 
| <span data-ttu-id="dfb5b-235">**SDL Phase**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-235">**SDL Phase**</span></span>               | <span data-ttu-id="dfb5b-236">Build</span><span class="sxs-lookup"><span data-stu-id="dfb5b-236">Build</span></span> |  
| <span data-ttu-id="dfb5b-237">**Applicable Technologies**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-237">**Applicable Technologies**</span></span> | <span data-ttu-id="dfb5b-238">Web Forms, MVC5</span><span class="sxs-lookup"><span data-stu-id="dfb5b-238">Web Forms, MVC5</span></span> |
| <span data-ttu-id="dfb5b-239">**Attributes**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-239">**Attributes**</span></span>              | <span data-ttu-id="dfb5b-240">EnvironmentType - OnPrem</span><span class="sxs-lookup"><span data-stu-id="dfb5b-240">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="dfb5b-241">**References**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-241">**References**</span></span>              | <span data-ttu-id="dfb5b-242">N/A</span><span class="sxs-lookup"><span data-stu-id="dfb5b-242">N/A</span></span>  |
| <span data-ttu-id="dfb5b-243">**Steps**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-243">**Steps**</span></span> | <span data-ttu-id="dfb5b-244">When the web application is the Relying Party, and the IdP is ADFS server, the FedAuth token's secure attribute can be configured by setting requireSSL to True in `system.identityModel.services` section of web.config:</span><span class="sxs-lookup"><span data-stu-id="dfb5b-244">When the web application is the Relying Party, and the IdP is ADFS server, the FedAuth token's secure attribute can be configured by setting requireSSL to True in `system.identityModel.services` section of web.config:</span></span>|

### <a name="example"></a><span data-ttu-id="dfb5b-245">Example</span><span class="sxs-lookup"><span data-stu-id="dfb5b-245">Example</span></span>
```csharp
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:20:0" />
    ....  
    </federationConfiguration>
  </system.identityModel.services>
```

## <a id="cookie-definition"></a><span data-ttu-id="dfb5b-246">All http based application should specify http only for cookie definition</span><span class="sxs-lookup"><span data-stu-id="dfb5b-246">All http based application should specify http only for cookie definition</span></span>

| <span data-ttu-id="dfb5b-247">Title</span><span class="sxs-lookup"><span data-stu-id="dfb5b-247">Title</span></span>                   | <span data-ttu-id="dfb5b-248">Details</span><span class="sxs-lookup"><span data-stu-id="dfb5b-248">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="dfb5b-249">**Component**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-249">**Component**</span></span>               | <span data-ttu-id="dfb5b-250">Web Application</span><span class="sxs-lookup"><span data-stu-id="dfb5b-250">Web Application</span></span> | 
| <span data-ttu-id="dfb5b-251">**SDL Phase**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-251">**SDL Phase**</span></span>               | <span data-ttu-id="dfb5b-252">Build</span><span class="sxs-lookup"><span data-stu-id="dfb5b-252">Build</span></span> |  
| <span data-ttu-id="dfb5b-253">**Applicable Technologies**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-253">**Applicable Technologies**</span></span> | <span data-ttu-id="dfb5b-254">Generic</span><span class="sxs-lookup"><span data-stu-id="dfb5b-254">Generic</span></span> |
| <span data-ttu-id="dfb5b-255">**Attributes**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-255">**Attributes**</span></span>              | <span data-ttu-id="dfb5b-256">N/A</span><span class="sxs-lookup"><span data-stu-id="dfb5b-256">N/A</span></span>  |
| <span data-ttu-id="dfb5b-257">**References**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-257">**References**</span></span>              | [<span data-ttu-id="dfb5b-258">Secure Cookie Attribute</span><span class="sxs-lookup"><span data-stu-id="dfb5b-258">Secure Cookie Attribute</span></span>](https://en.wikipedia.org/wiki/HTTP_cookie#Secure_cookie) |
| <span data-ttu-id="dfb5b-259">**Steps**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-259">**Steps**</span></span> | <span data-ttu-id="dfb5b-260">To mitigate the risk of information disclosure with a cross-site scripting (XSS) attack, a new attribute - httpOnly - was introduced to cookies and is supported by all major browsers.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-260">To mitigate the risk of information disclosure with a cross-site scripting (XSS) attack, a new attribute - httpOnly - was introduced to cookies and is supported by all major browsers.</span></span> <span data-ttu-id="dfb5b-261">The attribute specifies that a cookie is not accessible through script.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-261">The attribute specifies that a cookie is not accessible through script.</span></span> <span data-ttu-id="dfb5b-262">By using HttpOnly cookies, a web application reduces the possibility that sensitive information contained in the cookie can be stolen via script and sent to an attacker's website.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-262">By using HttpOnly cookies, a web application reduces the possibility that sensitive information contained in the cookie can be stolen via script and sent to an attacker's website.</span></span> |

### <a name="example"></a><span data-ttu-id="dfb5b-263">Example</span><span class="sxs-lookup"><span data-stu-id="dfb5b-263">Example</span></span>
<span data-ttu-id="dfb5b-264">All HTTP-based applications that use cookies should specify HttpOnly in the cookie definition, by implementing following configuration in web.config:</span><span class="sxs-lookup"><span data-stu-id="dfb5b-264">All HTTP-based applications that use cookies should specify HttpOnly in the cookie definition, by implementing following configuration in web.config:</span></span>
```XML
<system.web>
.
.
   <httpCookies requireSSL="false" httpOnlyCookies="true"/>
.
.
</system.web>
```

| <span data-ttu-id="dfb5b-265">Title</span><span class="sxs-lookup"><span data-stu-id="dfb5b-265">Title</span></span>                   | <span data-ttu-id="dfb5b-266">Details</span><span class="sxs-lookup"><span data-stu-id="dfb5b-266">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="dfb5b-267">**Component**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-267">**Component**</span></span>               | <span data-ttu-id="dfb5b-268">Web Application</span><span class="sxs-lookup"><span data-stu-id="dfb5b-268">Web Application</span></span> | 
| <span data-ttu-id="dfb5b-269">**SDL Phase**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-269">**SDL Phase**</span></span>               | <span data-ttu-id="dfb5b-270">Build</span><span class="sxs-lookup"><span data-stu-id="dfb5b-270">Build</span></span> |  
| <span data-ttu-id="dfb5b-271">**Applicable Technologies**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-271">**Applicable Technologies**</span></span> | <span data-ttu-id="dfb5b-272">Web Forms</span><span class="sxs-lookup"><span data-stu-id="dfb5b-272">Web Forms</span></span> |
| <span data-ttu-id="dfb5b-273">**Attributes**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-273">**Attributes**</span></span>              | <span data-ttu-id="dfb5b-274">N/A</span><span class="sxs-lookup"><span data-stu-id="dfb5b-274">N/A</span></span>  |
| <span data-ttu-id="dfb5b-275">**References**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-275">**References**</span></span>              | [<span data-ttu-id="dfb5b-276">FormsAuthentication.RequireSSL Property</span><span class="sxs-lookup"><span data-stu-id="dfb5b-276">FormsAuthentication.RequireSSL Property</span></span>](https://msdn.microsoft.com/library/system.web.security.formsauthentication.requiressl.aspx) |
| <span data-ttu-id="dfb5b-277">**Steps**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-277">**Steps**</span></span> | <span data-ttu-id="dfb5b-278">The RequireSSL property value is set in the configuration file for an ASP.NET application by using the requireSSL attribute of the configuration element.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-278">The RequireSSL property value is set in the configuration file for an ASP.NET application by using the requireSSL attribute of the configuration element.</span></span> <span data-ttu-id="dfb5b-279">You can specify in the Web.config file for your ASP.NET application whether SSL (Secure Sockets Layer) is required to return the forms-authentication cookie to the server by setting the requireSSL attribute.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-279">You can specify in the Web.config file for your ASP.NET application whether SSL (Secure Sockets Layer) is required to return the forms-authentication cookie to the server by setting the requireSSL attribute.</span></span>|

### <a name="example"></a><span data-ttu-id="dfb5b-280">Example</span><span class="sxs-lookup"><span data-stu-id="dfb5b-280">Example</span></span> 
<span data-ttu-id="dfb5b-281">The following code example sets the requireSSL attribute in the Web.config file.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-281">The following code example sets the requireSSL attribute in the Web.config file.</span></span>
```XML
<authentication mode="Forms">
  <forms loginUrl="member_login.aspx" cookieless="UseCookies" requireSSL="true"/>
</authentication>
```

| <span data-ttu-id="dfb5b-282">Title</span><span class="sxs-lookup"><span data-stu-id="dfb5b-282">Title</span></span>                   | <span data-ttu-id="dfb5b-283">Details</span><span class="sxs-lookup"><span data-stu-id="dfb5b-283">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="dfb5b-284">**Component**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-284">**Component**</span></span>               | <span data-ttu-id="dfb5b-285">Web Application</span><span class="sxs-lookup"><span data-stu-id="dfb5b-285">Web Application</span></span> | 
| <span data-ttu-id="dfb5b-286">**SDL Phase**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-286">**SDL Phase**</span></span>               | <span data-ttu-id="dfb5b-287">Build</span><span class="sxs-lookup"><span data-stu-id="dfb5b-287">Build</span></span> |  
| <span data-ttu-id="dfb5b-288">**Applicable Technologies**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-288">**Applicable Technologies**</span></span> | <span data-ttu-id="dfb5b-289">MVC5</span><span class="sxs-lookup"><span data-stu-id="dfb5b-289">MVC5</span></span> |
| <span data-ttu-id="dfb5b-290">**Attributes**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-290">**Attributes**</span></span>              | <span data-ttu-id="dfb5b-291">EnvironmentType - OnPrem</span><span class="sxs-lookup"><span data-stu-id="dfb5b-291">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="dfb5b-292">**References**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-292">**References**</span></span>              | [<span data-ttu-id="dfb5b-293">Windows Identity Foundation (WIF) Configuration – Part II</span><span class="sxs-lookup"><span data-stu-id="dfb5b-293">Windows Identity Foundation (WIF) Configuration – Part II</span></span>](https://blogs.msdn.microsoft.com/alikl/2011/02/01/windows-identity-foundation-wif-configuration-part-ii-cookiehandler-chunkedcookiehandler-customcookiehandler/) |
| <span data-ttu-id="dfb5b-294">**Steps**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-294">**Steps**</span></span> | <span data-ttu-id="dfb5b-295">To set httpOnly attribute for FedAuth cookies, hideFromCsript attribute value should be set to True.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-295">To set httpOnly attribute for FedAuth cookies, hideFromCsript attribute value should be set to True.</span></span> |

### <a name="example"></a><span data-ttu-id="dfb5b-296">Example</span><span class="sxs-lookup"><span data-stu-id="dfb5b-296">Example</span></span>
<span data-ttu-id="dfb5b-297">Following configuration shows the correct configuration:</span><span class="sxs-lookup"><span data-stu-id="dfb5b-297">Following configuration shows the correct configuration:</span></span>
```XML
<federatedAuthentication>
<cookieHandler mode="Custom"
                       hideFromScript="true"
                       name="FedAuth"
                       path="/"
                       requireSsl="true"
                       persistentSessionLifetime="25">
</cookieHandler>
</federatedAuthentication>
```

## <a id="csrf-asp"></a><span data-ttu-id="dfb5b-298">Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET web pages</span><span class="sxs-lookup"><span data-stu-id="dfb5b-298">Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET web pages</span></span>

| <span data-ttu-id="dfb5b-299">Title</span><span class="sxs-lookup"><span data-stu-id="dfb5b-299">Title</span></span>                   | <span data-ttu-id="dfb5b-300">Details</span><span class="sxs-lookup"><span data-stu-id="dfb5b-300">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="dfb5b-301">**Component**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-301">**Component**</span></span>               | <span data-ttu-id="dfb5b-302">Web Application</span><span class="sxs-lookup"><span data-stu-id="dfb5b-302">Web Application</span></span> | 
| <span data-ttu-id="dfb5b-303">**SDL Phase**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-303">**SDL Phase**</span></span>               | <span data-ttu-id="dfb5b-304">Build</span><span class="sxs-lookup"><span data-stu-id="dfb5b-304">Build</span></span> |  
| <span data-ttu-id="dfb5b-305">**Applicable Technologies**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-305">**Applicable Technologies**</span></span> | <span data-ttu-id="dfb5b-306">Generic</span><span class="sxs-lookup"><span data-stu-id="dfb5b-306">Generic</span></span> |
| <span data-ttu-id="dfb5b-307">**Attributes**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-307">**Attributes**</span></span>              | <span data-ttu-id="dfb5b-308">N/A</span><span class="sxs-lookup"><span data-stu-id="dfb5b-308">N/A</span></span>  |
| <span data-ttu-id="dfb5b-309">**References**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-309">**References**</span></span>              | <span data-ttu-id="dfb5b-310">N/A</span><span class="sxs-lookup"><span data-stu-id="dfb5b-310">N/A</span></span>  |
| <span data-ttu-id="dfb5b-311">**Steps**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-311">**Steps**</span></span> | <span data-ttu-id="dfb5b-312">Cross-site request forgery (CSRF or XSRF) is a type of attack in which an attacker can carry out actions in the security context of a different user's established session on a web site.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-312">Cross-site request forgery (CSRF or XSRF) is a type of attack in which an attacker can carry out actions in the security context of a different user's established session on a web site.</span></span> <span data-ttu-id="dfb5b-313">The goal is to modify or delete content, if the targeted web site relies exclusively on session cookies to authenticate received request.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-313">The goal is to modify or delete content, if the targeted web site relies exclusively on session cookies to authenticate received request.</span></span> <span data-ttu-id="dfb5b-314">An attacker could exploit this vulnerability by getting a different user's browser to load a URL with a command from a vulnerable site on which the user is already logged in.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-314">An attacker could exploit this vulnerability by getting a different user's browser to load a URL with a command from a vulnerable site on which the user is already logged in.</span></span> <span data-ttu-id="dfb5b-315">There are many ways for an attacker to do that, such as by hosting a different web site that loads a resource from the vulnerable server, or getting the user to click a link.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-315">There are many ways for an attacker to do that, such as by hosting a different web site that loads a resource from the vulnerable server, or getting the user to click a link.</span></span> <span data-ttu-id="dfb5b-316">The attack can be prevented if the server sends an additional token to the client, requires the client to include that token in all future requests, and verifies that all future requests include a token that pertains to the current session, such as by using the ASP.NET AntiForgeryToken or ViewState.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-316">The attack can be prevented if the server sends an additional token to the client, requires the client to include that token in all future requests, and verifies that all future requests include a token that pertains to the current session, such as by using the ASP.NET AntiForgeryToken or ViewState.</span></span> |

| <span data-ttu-id="dfb5b-317">Title</span><span class="sxs-lookup"><span data-stu-id="dfb5b-317">Title</span></span>                   | <span data-ttu-id="dfb5b-318">Details</span><span class="sxs-lookup"><span data-stu-id="dfb5b-318">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="dfb5b-319">**Component**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-319">**Component**</span></span>               | <span data-ttu-id="dfb5b-320">Web Application</span><span class="sxs-lookup"><span data-stu-id="dfb5b-320">Web Application</span></span> | 
| <span data-ttu-id="dfb5b-321">**SDL Phase**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-321">**SDL Phase**</span></span>               | <span data-ttu-id="dfb5b-322">Build</span><span class="sxs-lookup"><span data-stu-id="dfb5b-322">Build</span></span> |  
| <span data-ttu-id="dfb5b-323">**Applicable Technologies**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-323">**Applicable Technologies**</span></span> | <span data-ttu-id="dfb5b-324">MVC5, MVC6</span><span class="sxs-lookup"><span data-stu-id="dfb5b-324">MVC5, MVC6</span></span> |
| <span data-ttu-id="dfb5b-325">**Attributes**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-325">**Attributes**</span></span>              | <span data-ttu-id="dfb5b-326">N/A</span><span class="sxs-lookup"><span data-stu-id="dfb5b-326">N/A</span></span>  |
| <span data-ttu-id="dfb5b-327">**References**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-327">**References**</span></span>              | [<span data-ttu-id="dfb5b-328">XSRF/CSRF Prevention in ASP.NET MVC and Web Pages</span><span class="sxs-lookup"><span data-stu-id="dfb5b-328">XSRF/CSRF Prevention in ASP.NET MVC and Web Pages</span></span>](http://www.asp.net/mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages) |
| <span data-ttu-id="dfb5b-329">**Steps**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-329">**Steps**</span></span> | <span data-ttu-id="dfb5b-330">Anti-CSRF and ASP.NET MVC forms - Use the `AntiForgeryToken` helper method on Views; put an `Html.AntiForgeryToken()` into the form, for example,</span><span class="sxs-lookup"><span data-stu-id="dfb5b-330">Anti-CSRF and ASP.NET MVC forms - Use the `AntiForgeryToken` helper method on Views; put an `Html.AntiForgeryToken()` into the form, for example,</span></span>|

### <a name="example"></a><span data-ttu-id="dfb5b-331">Example</span><span class="sxs-lookup"><span data-stu-id="dfb5b-331">Example</span></span>
```csharp
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
```

### <a name="example"></a><span data-ttu-id="dfb5b-332">Example</span><span class="sxs-lookup"><span data-stu-id="dfb5b-332">Example</span></span>
```csharp
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a><span data-ttu-id="dfb5b-333">Example</span><span class="sxs-lookup"><span data-stu-id="dfb5b-333">Example</span></span>
<span data-ttu-id="dfb5b-334">At the same time, Html.AntiForgeryToken() gives the visitor a cookie called __RequestVerificationToken, with the same value as the random hidden value shown above.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-334">At the same time, Html.AntiForgeryToken() gives the visitor a cookie called __RequestVerificationToken, with the same value as the random hidden value shown above.</span></span> <span data-ttu-id="dfb5b-335">Next, to validate an incoming form post, add the [ValidateAntiForgeryToken] filter to the target action method.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-335">Next, to validate an incoming form post, add the [ValidateAntiForgeryToken] filter to the target action method.</span></span> <span data-ttu-id="dfb5b-336">For example:</span><span class="sxs-lookup"><span data-stu-id="dfb5b-336">For example:</span></span>
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
<span data-ttu-id="dfb5b-337">Authorization filter that checks that:</span><span class="sxs-lookup"><span data-stu-id="dfb5b-337">Authorization filter that checks that:</span></span>
* <span data-ttu-id="dfb5b-338">The incoming request has a cookie called __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="dfb5b-338">The incoming request has a cookie called __RequestVerificationToken</span></span>
* <span data-ttu-id="dfb5b-339">The incoming request has a `Request.Form` entry called __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="dfb5b-339">The incoming request has a `Request.Form` entry called __RequestVerificationToken</span></span>
* <span data-ttu-id="dfb5b-340">These cookie and `Request.Form` values match Assuming all is well, the request goes through as normal.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-340">These cookie and `Request.Form` values match Assuming all is well, the request goes through as normal.</span></span> <span data-ttu-id="dfb5b-341">But if not, then an authorization failure with message “A required anti-forgery token was not supplied or was invalid”.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-341">But if not, then an authorization failure with message “A required anti-forgery token was not supplied or was invalid”.</span></span> 

### <a name="example"></a><span data-ttu-id="dfb5b-342">Example</span><span class="sxs-lookup"><span data-stu-id="dfb5b-342">Example</span></span>
<span data-ttu-id="dfb5b-343">Anti-CSRF and AJAX: The form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-343">Anti-CSRF and AJAX: The form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="dfb5b-344">One solution is to send the tokens in a custom HTTP header.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-344">One solution is to send the tokens in a custom HTTP header.</span></span> <span data-ttu-id="dfb5b-345">The following code uses Razor syntax to generate the tokens, and then adds the tokens to an AJAX request.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-345">The following code uses Razor syntax to generate the tokens, and then adds the tokens to an AJAX request.</span></span> 
```csharp
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }

    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a><span data-ttu-id="dfb5b-346">Example</span><span class="sxs-lookup"><span data-stu-id="dfb5b-346">Example</span></span>
<span data-ttu-id="dfb5b-347">When you process the request, extract the tokens from the request header.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-347">When you process the request, extract the tokens from the request header.</span></span> <span data-ttu-id="dfb5b-348">Then call the AntiForgery.Validate method to validate the tokens.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-348">Then call the AntiForgery.Validate method to validate the tokens.</span></span> <span data-ttu-id="dfb5b-349">The Validate method throws an exception if the tokens are not valid.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-349">The Validate method throws an exception if the tokens are not valid.</span></span>
```csharp
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

| <span data-ttu-id="dfb5b-350">Title</span><span class="sxs-lookup"><span data-stu-id="dfb5b-350">Title</span></span>                   | <span data-ttu-id="dfb5b-351">Details</span><span class="sxs-lookup"><span data-stu-id="dfb5b-351">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="dfb5b-352">**Component**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-352">**Component**</span></span>               | <span data-ttu-id="dfb5b-353">Web Application</span><span class="sxs-lookup"><span data-stu-id="dfb5b-353">Web Application</span></span> | 
| <span data-ttu-id="dfb5b-354">**SDL Phase**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-354">**SDL Phase**</span></span>               | <span data-ttu-id="dfb5b-355">Build</span><span class="sxs-lookup"><span data-stu-id="dfb5b-355">Build</span></span> |  
| <span data-ttu-id="dfb5b-356">**Applicable Technologies**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-356">**Applicable Technologies**</span></span> | <span data-ttu-id="dfb5b-357">Web Forms</span><span class="sxs-lookup"><span data-stu-id="dfb5b-357">Web Forms</span></span> |
| <span data-ttu-id="dfb5b-358">**Attributes**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-358">**Attributes**</span></span>              | <span data-ttu-id="dfb5b-359">N/A</span><span class="sxs-lookup"><span data-stu-id="dfb5b-359">N/A</span></span>  |
| <span data-ttu-id="dfb5b-360">**References**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-360">**References**</span></span>              | [<span data-ttu-id="dfb5b-361">Take Advantage of ASP.NET Built-in Features to Fend Off Web Attacks</span><span class="sxs-lookup"><span data-stu-id="dfb5b-361">Take Advantage of ASP.NET Built-in Features to Fend Off Web Attacks</span></span>](https://msdn.microsoft.com/library/ms972969.aspx#securitybarriers_topic2) |
| <span data-ttu-id="dfb5b-362">**Steps**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-362">**Steps**</span></span> | <span data-ttu-id="dfb5b-363">CSRF attacks in WebForm based applications can be mitigated by setting ViewStateUserKey to a random string that varies for each user - user ID or, better yet, session ID.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-363">CSRF attacks in WebForm based applications can be mitigated by setting ViewStateUserKey to a random string that varies for each user - user ID or, better yet, session ID.</span></span> <span data-ttu-id="dfb5b-364">For a number of technical and social reasons, session ID is a much better fit because a session ID is unpredictable, times out, and varies on a per-user basis.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-364">For a number of technical and social reasons, session ID is a much better fit because a session ID is unpredictable, times out, and varies on a per-user basis.</span></span>|

### <a name="example"></a><span data-ttu-id="dfb5b-365">Example</span><span class="sxs-lookup"><span data-stu-id="dfb5b-365">Example</span></span>
<span data-ttu-id="dfb5b-366">Here's the code you need to have in all of your pages:</span><span class="sxs-lookup"><span data-stu-id="dfb5b-366">Here's the code you need to have in all of your pages:</span></span>
```csharp
void Page_Init (object sender, EventArgs e) {
   ViewStateUserKey = Session.SessionID;
   :
}
```

## <a id="inactivity-lifetime"></a><span data-ttu-id="dfb5b-367">Set up session for inactivity lifetime</span><span class="sxs-lookup"><span data-stu-id="dfb5b-367">Set up session for inactivity lifetime</span></span>

| <span data-ttu-id="dfb5b-368">Title</span><span class="sxs-lookup"><span data-stu-id="dfb5b-368">Title</span></span>                   | <span data-ttu-id="dfb5b-369">Details</span><span class="sxs-lookup"><span data-stu-id="dfb5b-369">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="dfb5b-370">**Component**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-370">**Component**</span></span>               | <span data-ttu-id="dfb5b-371">Web Application</span><span class="sxs-lookup"><span data-stu-id="dfb5b-371">Web Application</span></span> | 
| <span data-ttu-id="dfb5b-372">**SDL Phase**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-372">**SDL Phase**</span></span>               | <span data-ttu-id="dfb5b-373">Build</span><span class="sxs-lookup"><span data-stu-id="dfb5b-373">Build</span></span> |  
| <span data-ttu-id="dfb5b-374">**Applicable Technologies**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-374">**Applicable Technologies**</span></span> | <span data-ttu-id="dfb5b-375">Generic</span><span class="sxs-lookup"><span data-stu-id="dfb5b-375">Generic</span></span> |
| <span data-ttu-id="dfb5b-376">**Attributes**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-376">**Attributes**</span></span>              | <span data-ttu-id="dfb5b-377">N/A</span><span class="sxs-lookup"><span data-stu-id="dfb5b-377">N/A</span></span>  |
| <span data-ttu-id="dfb5b-378">**References**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-378">**References**</span></span>              | <span data-ttu-id="dfb5b-379">[HttpSessionState.Timeout Property](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="dfb5b-379">[HttpSessionState.Timeout Property](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx)</span></span> |
| <span data-ttu-id="dfb5b-380">**Steps**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-380">**Steps**</span></span> | <span data-ttu-id="dfb5b-381">Session timeout represents the event occurring when a user does not perform any action on a web site during a interval (defined by web server).</span><span class="sxs-lookup"><span data-stu-id="dfb5b-381">Session timeout represents the event occurring when a user does not perform any action on a web site during a interval (defined by web server).</span></span> <span data-ttu-id="dfb5b-382">The event, on server side, change the status of the user session to 'invalid' (for example  "not used anymore") and instruct the web server to destroy it (deleting all data contained into it).</span><span class="sxs-lookup"><span data-stu-id="dfb5b-382">The event, on server side, change the status of the user session to 'invalid' (for example  "not used anymore") and instruct the web server to destroy it (deleting all data contained into it).</span></span> <span data-ttu-id="dfb5b-383">The following code example sets the timeout session attribute to 15 minutes in the Web.config file.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-383">The following code example sets the timeout session attribute to 15 minutes in the Web.config file.</span></span>|

### <a name="example"></a><span data-ttu-id="dfb5b-384">Example</span><span class="sxs-lookup"><span data-stu-id="dfb5b-384">Example</span></span>
```XML 
<configuration>
  <system.web>
    <sessionState mode="InProc" cookieless="true" timeout="15" />
  </system.web>
</configuration>
```

## <a id="threat-detection"></a><span data-ttu-id="dfb5b-385">Enable Threat detection on Azure SQL</span><span class="sxs-lookup"><span data-stu-id="dfb5b-385">Enable Threat detection on Azure SQL</span></span>
```

| Title                   | Details      |
| ----------------------- | ------------ |
| **Component**               | Web Application | 
| **SDL Phase**               | Build |  
| **Applicable Technologies** | Web Forms |
| **Attributes**              | N/A  |
| **References**              | [forms Element for authentication (ASP.NET Settings Schema)](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx) |
| **Steps** | Set the Forms Authentication Ticket cookie timeout to 15 minutes|

### Example
```XML
<forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms>
```

| <span data-ttu-id="dfb5b-386">Title</span><span class="sxs-lookup"><span data-stu-id="dfb5b-386">Title</span></span>                   | <span data-ttu-id="dfb5b-387">Details</span><span class="sxs-lookup"><span data-stu-id="dfb5b-387">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="dfb5b-388">**Component**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-388">**Component**</span></span>               | <span data-ttu-id="dfb5b-389">Web Application</span><span class="sxs-lookup"><span data-stu-id="dfb5b-389">Web Application</span></span> | 
| <span data-ttu-id="dfb5b-390">**SDL Phase**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-390">**SDL Phase**</span></span>               | <span data-ttu-id="dfb5b-391">Build</span><span class="sxs-lookup"><span data-stu-id="dfb5b-391">Build</span></span> |  
| <span data-ttu-id="dfb5b-392">**Applicable Technologies**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-392">**Applicable Technologies**</span></span> | <span data-ttu-id="dfb5b-393">Web Forms, MVC5</span><span class="sxs-lookup"><span data-stu-id="dfb5b-393">Web Forms, MVC5</span></span> |
| <span data-ttu-id="dfb5b-394">**Attributes**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-394">**Attributes**</span></span>              | <span data-ttu-id="dfb5b-395">EnvironmentType - OnPrem</span><span class="sxs-lookup"><span data-stu-id="dfb5b-395">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="dfb5b-396">**References**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-396">**References**</span></span>              | [<span data-ttu-id="dfb5b-397">asdeqa</span><span class="sxs-lookup"><span data-stu-id="dfb5b-397">asdeqa</span></span>](https://skf.azurewebsites.net/Mitigations/Details/wefr) |
| <span data-ttu-id="dfb5b-398">**Steps**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-398">**Steps**</span></span> | <span data-ttu-id="dfb5b-399">When the web application is Relying Party and ADFS is the STS, the lifetime of the authentication cookies - FedAuth tokens - can be set by the following configuration in web.config:</span><span class="sxs-lookup"><span data-stu-id="dfb5b-399">When the web application is Relying Party and ADFS is the STS, the lifetime of the authentication cookies - FedAuth tokens - can be set by the following configuration in web.config:</span></span>|

### <a name="example"></a><span data-ttu-id="dfb5b-400">Example</span><span class="sxs-lookup"><span data-stu-id="dfb5b-400">Example</span></span>
```XML
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:15:0" />
      <!-- Set requireHttps=true; -->
      <wsFederation passiveRedirectEnabled="true" issuer="http://localhost:39529/" realm="https://localhost:44302/" reply="https://localhost:44302/" requireHttps="true"/>
      <!--
      Use the code below to enable encryption-decryption of claims received from ADFS. Thumbprint value varies based on the certificate being used.
      <serviceCertificate>
        <certificateReference findValue="4FBBBA33A1D11A9022A5BF3492FF83320007686A" storeLocation="LocalMachine" storeName="My" x509FindType="FindByThumbprint" />
      </serviceCertificate>
      -->
    </federationConfiguration>
  </system.identityModel.services>
```

### <a name="example"></a><span data-ttu-id="dfb5b-401">Example</span><span class="sxs-lookup"><span data-stu-id="dfb5b-401">Example</span></span>
<span data-ttu-id="dfb5b-402">Also the ADFS issued SAML claim token's lifetime should be set to 15 minutes, by executing the following powershell command on the ADFS server:</span><span class="sxs-lookup"><span data-stu-id="dfb5b-402">Also the ADFS issued SAML claim token's lifetime should be set to 15 minutes, by executing the following powershell command on the ADFS server:</span></span>
```csharp
Set-ADFSRelyingPartyTrust -TargetName “<RelyingPartyWebApp>” -ClaimsProviderName @(“Active Directory”) -TokenLifetime 15 -AlwaysRequireAuthentication $true
```

## <a id="proper-app-logout"></a><span data-ttu-id="dfb5b-403">Implement proper logout from the application</span><span class="sxs-lookup"><span data-stu-id="dfb5b-403">Implement proper logout from the application</span></span>

| <span data-ttu-id="dfb5b-404">Title</span><span class="sxs-lookup"><span data-stu-id="dfb5b-404">Title</span></span>                   | <span data-ttu-id="dfb5b-405">Details</span><span class="sxs-lookup"><span data-stu-id="dfb5b-405">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="dfb5b-406">**Component**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-406">**Component**</span></span>               | <span data-ttu-id="dfb5b-407">Web Application</span><span class="sxs-lookup"><span data-stu-id="dfb5b-407">Web Application</span></span> | 
| <span data-ttu-id="dfb5b-408">**SDL Phase**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-408">**SDL Phase**</span></span>               | <span data-ttu-id="dfb5b-409">Build</span><span class="sxs-lookup"><span data-stu-id="dfb5b-409">Build</span></span> |  
| <span data-ttu-id="dfb5b-410">**Applicable Technologies**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-410">**Applicable Technologies**</span></span> | <span data-ttu-id="dfb5b-411">Generic</span><span class="sxs-lookup"><span data-stu-id="dfb5b-411">Generic</span></span> |
| <span data-ttu-id="dfb5b-412">**Attributes**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-412">**Attributes**</span></span>              | <span data-ttu-id="dfb5b-413">N/A</span><span class="sxs-lookup"><span data-stu-id="dfb5b-413">N/A</span></span>  |
| <span data-ttu-id="dfb5b-414">**References**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-414">**References**</span></span>              | <span data-ttu-id="dfb5b-415">N/A</span><span class="sxs-lookup"><span data-stu-id="dfb5b-415">N/A</span></span>  |
| <span data-ttu-id="dfb5b-416">**Steps**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-416">**Steps**</span></span> | <span data-ttu-id="dfb5b-417">Perform proper Sign Out from the application, when user presses log out button.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-417">Perform proper Sign Out from the application, when user presses log out button.</span></span> <span data-ttu-id="dfb5b-418">Upon logout, application should destroy user's session, and also reset and nullify session cookie value, along with resetting and nullifying authentication cookie value.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-418">Upon logout, application should destroy user's session, and also reset and nullify session cookie value, along with resetting and nullifying authentication cookie value.</span></span> <span data-ttu-id="dfb5b-419">Also, when multiple sessions are tied to a single user identity, they must be collectively terminated on the server side at timeout or logout.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-419">Also, when multiple sessions are tied to a single user identity, they must be collectively terminated on the server side at timeout or logout.</span></span> <span data-ttu-id="dfb5b-420">Lastly, ensure that Logout functionality is available on every page.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-420">Lastly, ensure that Logout functionality is available on every page.</span></span> |

## <a id="csrf-api"></a><span data-ttu-id="dfb5b-421">Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET Web APIs</span><span class="sxs-lookup"><span data-stu-id="dfb5b-421">Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET Web APIs</span></span>

| <span data-ttu-id="dfb5b-422">Title</span><span class="sxs-lookup"><span data-stu-id="dfb5b-422">Title</span></span>                   | <span data-ttu-id="dfb5b-423">Details</span><span class="sxs-lookup"><span data-stu-id="dfb5b-423">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="dfb5b-424">**Component**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-424">**Component**</span></span>               | <span data-ttu-id="dfb5b-425">Web API</span><span class="sxs-lookup"><span data-stu-id="dfb5b-425">Web API</span></span> | 
| <span data-ttu-id="dfb5b-426">**SDL Phase**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-426">**SDL Phase**</span></span>               | <span data-ttu-id="dfb5b-427">Build</span><span class="sxs-lookup"><span data-stu-id="dfb5b-427">Build</span></span> |  
| <span data-ttu-id="dfb5b-428">**Applicable Technologies**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-428">**Applicable Technologies**</span></span> | <span data-ttu-id="dfb5b-429">Generic</span><span class="sxs-lookup"><span data-stu-id="dfb5b-429">Generic</span></span> |
| <span data-ttu-id="dfb5b-430">**Attributes**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-430">**Attributes**</span></span>              | <span data-ttu-id="dfb5b-431">N/A</span><span class="sxs-lookup"><span data-stu-id="dfb5b-431">N/A</span></span>  |
| <span data-ttu-id="dfb5b-432">**References**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-432">**References**</span></span>              | <span data-ttu-id="dfb5b-433">N/A</span><span class="sxs-lookup"><span data-stu-id="dfb5b-433">N/A</span></span>  |
| <span data-ttu-id="dfb5b-434">**Steps**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-434">**Steps**</span></span> | <span data-ttu-id="dfb5b-435">Cross-site request forgery (CSRF or XSRF) is a type of attack in which an attacker can carry out actions in the security context of a different user's established session on a web site.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-435">Cross-site request forgery (CSRF or XSRF) is a type of attack in which an attacker can carry out actions in the security context of a different user's established session on a web site.</span></span> <span data-ttu-id="dfb5b-436">The goal is to modify or delete content, if the targeted web site relies exclusively on session cookies to authenticate received request.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-436">The goal is to modify or delete content, if the targeted web site relies exclusively on session cookies to authenticate received request.</span></span> <span data-ttu-id="dfb5b-437">An attacker could exploit this vulnerability by getting a different user's browser to load a URL with a command from a vulnerable site on which the user is already logged in.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-437">An attacker could exploit this vulnerability by getting a different user's browser to load a URL with a command from a vulnerable site on which the user is already logged in.</span></span> <span data-ttu-id="dfb5b-438">There are many ways for an attacker to do that, such as by hosting a different web site that loads a resource from the vulnerable server, or getting the user to click a link.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-438">There are many ways for an attacker to do that, such as by hosting a different web site that loads a resource from the vulnerable server, or getting the user to click a link.</span></span> <span data-ttu-id="dfb5b-439">The attack can be prevented if the server sends an additional token to the client, requires the client to include that token in all future requests, and verifies that all future requests include a token that pertains to the current session, such as by using the ASP.NET AntiForgeryToken or ViewState.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-439">The attack can be prevented if the server sends an additional token to the client, requires the client to include that token in all future requests, and verifies that all future requests include a token that pertains to the current session, such as by using the ASP.NET AntiForgeryToken or ViewState.</span></span> |

| <span data-ttu-id="dfb5b-440">Title</span><span class="sxs-lookup"><span data-stu-id="dfb5b-440">Title</span></span>                   | <span data-ttu-id="dfb5b-441">Details</span><span class="sxs-lookup"><span data-stu-id="dfb5b-441">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="dfb5b-442">**Component**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-442">**Component**</span></span>               | <span data-ttu-id="dfb5b-443">Web API</span><span class="sxs-lookup"><span data-stu-id="dfb5b-443">Web API</span></span> | 
| <span data-ttu-id="dfb5b-444">**SDL Phase**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-444">**SDL Phase**</span></span>               | <span data-ttu-id="dfb5b-445">Build</span><span class="sxs-lookup"><span data-stu-id="dfb5b-445">Build</span></span> |  
| <span data-ttu-id="dfb5b-446">**Applicable Technologies**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-446">**Applicable Technologies**</span></span> | <span data-ttu-id="dfb5b-447">MVC5, MVC6</span><span class="sxs-lookup"><span data-stu-id="dfb5b-447">MVC5, MVC6</span></span> |
| <span data-ttu-id="dfb5b-448">**Attributes**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-448">**Attributes**</span></span>              | <span data-ttu-id="dfb5b-449">N/A</span><span class="sxs-lookup"><span data-stu-id="dfb5b-449">N/A</span></span>  |
| <span data-ttu-id="dfb5b-450">**References**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-450">**References**</span></span>              | [<span data-ttu-id="dfb5b-451">Preventing Cross-Site Request Forgery (CSRF) Attacks in ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="dfb5b-451">Preventing Cross-Site Request Forgery (CSRF) Attacks in ASP.NET Web API</span></span>](http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks) |
| <span data-ttu-id="dfb5b-452">**Steps**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-452">**Steps**</span></span> | <span data-ttu-id="dfb5b-453">Anti-CSRF and AJAX: The form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-453">Anti-CSRF and AJAX: The form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="dfb5b-454">One solution is to send the tokens in a custom HTTP header.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-454">One solution is to send the tokens in a custom HTTP header.</span></span> <span data-ttu-id="dfb5b-455">The following code uses Razor syntax to generate the tokens, and then adds the tokens to an AJAX request.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-455">The following code uses Razor syntax to generate the tokens, and then adds the tokens to an AJAX request.</span></span> |

### <a name="example"></a><span data-ttu-id="dfb5b-456">Example</span><span class="sxs-lookup"><span data-stu-id="dfb5b-456">Example</span></span>
```Javascript
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }
    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a><span data-ttu-id="dfb5b-457">Example</span><span class="sxs-lookup"><span data-stu-id="dfb5b-457">Example</span></span>
<span data-ttu-id="dfb5b-458">When you process the request, extract the tokens from the request header.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-458">When you process the request, extract the tokens from the request header.</span></span> <span data-ttu-id="dfb5b-459">Then call the AntiForgery.Validate method to validate the tokens.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-459">Then call the AntiForgery.Validate method to validate the tokens.</span></span> <span data-ttu-id="dfb5b-460">The Validate method throws an exception if the tokens are not valid.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-460">The Validate method throws an exception if the tokens are not valid.</span></span>
```csharp
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

### <a name="example"></a><span data-ttu-id="dfb5b-461">Example</span><span class="sxs-lookup"><span data-stu-id="dfb5b-461">Example</span></span>
<span data-ttu-id="dfb5b-462">Anti-CSRF and ASP.NET MVC forms - Use the AntiForgeryToken helper method on Views; put an Html.AntiForgeryToken() into the form, for example,</span><span class="sxs-lookup"><span data-stu-id="dfb5b-462">Anti-CSRF and ASP.NET MVC forms - Use the AntiForgeryToken helper method on Views; put an Html.AntiForgeryToken() into the form, for example,</span></span>
```csharp
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
}
```

### <a name="example"></a><span data-ttu-id="dfb5b-463">Example</span><span class="sxs-lookup"><span data-stu-id="dfb5b-463">Example</span></span>
<span data-ttu-id="dfb5b-464">The example above will output something like the following:</span><span class="sxs-lookup"><span data-stu-id="dfb5b-464">The example above will output something like the following:</span></span>
```csharp
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a><span data-ttu-id="dfb5b-465">Example</span><span class="sxs-lookup"><span data-stu-id="dfb5b-465">Example</span></span>
<span data-ttu-id="dfb5b-466">At the same time, Html.AntiForgeryToken() gives the visitor a cookie called __RequestVerificationToken, with the same value as the random hidden value shown above.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-466">At the same time, Html.AntiForgeryToken() gives the visitor a cookie called __RequestVerificationToken, with the same value as the random hidden value shown above.</span></span> <span data-ttu-id="dfb5b-467">Next, to validate an incoming form post, add the [ValidateAntiForgeryToken] filter to the target action method.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-467">Next, to validate an incoming form post, add the [ValidateAntiForgeryToken] filter to the target action method.</span></span> <span data-ttu-id="dfb5b-468">For example:</span><span class="sxs-lookup"><span data-stu-id="dfb5b-468">For example:</span></span>
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
<span data-ttu-id="dfb5b-469">Authorization filter that checks that:</span><span class="sxs-lookup"><span data-stu-id="dfb5b-469">Authorization filter that checks that:</span></span>
* <span data-ttu-id="dfb5b-470">The incoming request has a cookie called __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="dfb5b-470">The incoming request has a cookie called __RequestVerificationToken</span></span>
* <span data-ttu-id="dfb5b-471">The incoming request has a `Request.Form` entry called __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="dfb5b-471">The incoming request has a `Request.Form` entry called __RequestVerificationToken</span></span>
* <span data-ttu-id="dfb5b-472">These cookie and `Request.Form` values match Assuming all is well, the request goes through as normal.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-472">These cookie and `Request.Form` values match Assuming all is well, the request goes through as normal.</span></span> <span data-ttu-id="dfb5b-473">But if not, then an authorization failure with message “A required anti-forgery token was not supplied or was invalid”.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-473">But if not, then an authorization failure with message “A required anti-forgery token was not supplied or was invalid”.</span></span>

| <span data-ttu-id="dfb5b-474">Title</span><span class="sxs-lookup"><span data-stu-id="dfb5b-474">Title</span></span>                   | <span data-ttu-id="dfb5b-475">Details</span><span class="sxs-lookup"><span data-stu-id="dfb5b-475">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="dfb5b-476">**Component**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-476">**Component**</span></span>               | <span data-ttu-id="dfb5b-477">Web API</span><span class="sxs-lookup"><span data-stu-id="dfb5b-477">Web API</span></span> | 
| <span data-ttu-id="dfb5b-478">**SDL Phase**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-478">**SDL Phase**</span></span>               | <span data-ttu-id="dfb5b-479">Build</span><span class="sxs-lookup"><span data-stu-id="dfb5b-479">Build</span></span> |  
| <span data-ttu-id="dfb5b-480">**Applicable Technologies**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-480">**Applicable Technologies**</span></span> | <span data-ttu-id="dfb5b-481">MVC5, MVC6</span><span class="sxs-lookup"><span data-stu-id="dfb5b-481">MVC5, MVC6</span></span> |
| <span data-ttu-id="dfb5b-482">**Attributes**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-482">**Attributes**</span></span>              | <span data-ttu-id="dfb5b-483">Identity Provider - ADFS, Identity Provider - Azure AD</span><span class="sxs-lookup"><span data-stu-id="dfb5b-483">Identity Provider - ADFS, Identity Provider - Azure AD</span></span> |
| <span data-ttu-id="dfb5b-484">**References**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-484">**References**</span></span>              | [<span data-ttu-id="dfb5b-485">Secure a Web API with Individual Accounts and Local Login in ASP.NET Web API 2.2</span><span class="sxs-lookup"><span data-stu-id="dfb5b-485">Secure a Web API with Individual Accounts and Local Login in ASP.NET Web API 2.2</span></span>](http://www.asp.net/web-api/overview/security/individual-accounts-in-web-api) |
| <span data-ttu-id="dfb5b-486">**Steps**</span><span class="sxs-lookup"><span data-stu-id="dfb5b-486">**Steps**</span></span> | <span data-ttu-id="dfb5b-487">If the Web API is secured using OAuth 2.0, then it expects a bearer token in Authorization request header and grants access to the request only if the token is valid.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-487">If the Web API is secured using OAuth 2.0, then it expects a bearer token in Authorization request header and grants access to the request only if the token is valid.</span></span> <span data-ttu-id="dfb5b-488">Unlike cookie based authentication, browsers do not attach the bearer tokens to requests.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-488">Unlike cookie based authentication, browsers do not attach the bearer tokens to requests.</span></span> <span data-ttu-id="dfb5b-489">The requesting client needs to explicitly attach the bearer token in the request header.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-489">The requesting client needs to explicitly attach the bearer token in the request header.</span></span> <span data-ttu-id="dfb5b-490">Therefore, for ASP.NET Web APIs protected using OAuth 2.0, bearer tokens are considered as a defense against CSRF attacks.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-490">Therefore, for ASP.NET Web APIs protected using OAuth 2.0, bearer tokens are considered as a defense against CSRF attacks.</span></span> <span data-ttu-id="dfb5b-491">Please note that if the MVC portion of the application uses forms authentication (i.e., uses cookies), anti-forgery tokens have to be used by the MVC web app.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-491">Please note that if the MVC portion of the application uses forms authentication (i.e., uses cookies), anti-forgery tokens have to be used by the MVC web app.</span></span> |

### <a name="example"></a><span data-ttu-id="dfb5b-492">Example</span><span class="sxs-lookup"><span data-stu-id="dfb5b-492">Example</span></span>
<span data-ttu-id="dfb5b-493">The Web API has to be informed to rely ONLY on bearer tokens and not on cookies.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-493">The Web API has to be informed to rely ONLY on bearer tokens and not on cookies.</span></span> <span data-ttu-id="dfb5b-494">It can be done by the following configuration in `WebApiConfig.Register` method:</span><span class="sxs-lookup"><span data-stu-id="dfb5b-494">It can be done by the following configuration in `WebApiConfig.Register` method:</span></span>

```csharp
config.SuppressDefaultHostAuthentication();
config.Filters.Add(new HostAuthenticationFilter(OAuthDefaults.AuthenticationType));
```

<span data-ttu-id="dfb5b-495">The SuppressDefaultHostAuthentication method tells Web API to ignore any authentication that happens before the request reaches the Web API pipeline, either by IIS or by OWIN middleware.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-495">The SuppressDefaultHostAuthentication method tells Web API to ignore any authentication that happens before the request reaches the Web API pipeline, either by IIS or by OWIN middleware.</span></span> <span data-ttu-id="dfb5b-496">That way, we can restrict Web API to authenticate only using bearer tokens.</span><span class="sxs-lookup"><span data-stu-id="dfb5b-496">That way, we can restrict Web API to authenticate only using bearer tokens.</span></span>
