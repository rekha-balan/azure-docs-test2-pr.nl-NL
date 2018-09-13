---
title: Signing Key Rollover in Azure AD | Microsoft Docs
description: This article discusses the signing key rollover best practices for Azure Active Directory
services: active-directory
documentationcenter: .net
author: gsacavdm
manager: krassk
editor: ''
ms.assetid: ed964056-0723-42fe-bb69-e57323b9407f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2016
ms.author: gsacavdm
ms.openlocfilehash: a13bedc2ad31e45f3525a87655b6c46e653cee16
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548902"
---
# <a name="signing-key-rollover-in-azure-active-directory"></a><span data-ttu-id="5a3e9-103">Signing key rollover in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5a3e9-103">Signing key rollover in Azure Active Directory</span></span>
<span data-ttu-id="5a3e9-104">This topic discusses what you need to know about the public keys that are used in Azure Active Directory (Azure AD) to sign security tokens.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-104">This topic discusses what you need to know about the public keys that are used in Azure Active Directory (Azure AD) to sign security tokens.</span></span> <span data-ttu-id="5a3e9-105">It is important to note that these keys rollover on a periodic basis and, in an emergency, could be rolled over immediately.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-105">It is important to note that these keys rollover on a periodic basis and, in an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="5a3e9-106">All applications that use Azure AD should be able to programmatically handle the key rollover process or establish a periodic manual rollover process.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-106">All applications that use Azure AD should be able to programmatically handle the key rollover process or establish a periodic manual rollover process.</span></span> <span data-ttu-id="5a3e9-107">Continue reading to understand how the keys work, how to assess the impact of the rollover to your application and how to update your application or establish a periodic manual rollover process to handle key rollover if necessary.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-107">Continue reading to understand how the keys work, how to assess the impact of the rollover to your application and how to update your application or establish a periodic manual rollover process to handle key rollover if necessary.</span></span>

## <a name="overview-of-signing-keys-in-azure-ad"></a><span data-ttu-id="5a3e9-108">Overview of signing keys in Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a3e9-108">Overview of signing keys in Azure AD</span></span>
<span data-ttu-id="5a3e9-109">Azure AD uses public-key cryptography built on industry standards to establish trust between itself and the applications that use it.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-109">Azure AD uses public-key cryptography built on industry standards to establish trust between itself and the applications that use it.</span></span> <span data-ttu-id="5a3e9-110">In practical terms, this works in the following way: Azure AD uses a signing key that consists of a public and private key pair.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-110">In practical terms, this works in the following way: Azure AD uses a signing key that consists of a public and private key pair.</span></span> <span data-ttu-id="5a3e9-111">When a user signs in to an application that uses Azure AD for authentication, Azure AD creates a security token that contains information about the user.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-111">When a user signs in to an application that uses Azure AD for authentication, Azure AD creates a security token that contains information about the user.</span></span> <span data-ttu-id="5a3e9-112">This token is signed by Azure AD using its private key before it is sent back to the application.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-112">This token is signed by Azure AD using its private key before it is sent back to the application.</span></span> <span data-ttu-id="5a3e9-113">To verify that the token is valid and actually originated from Azure AD, the application must validate the token’s signature using the public key exposed by Azure AD that is contained in the tenant’s [OpenID Connect discovery document](http://openid.net/specs/openid-connect-discovery-1_0.html) or SAML/WS-Fed [federation metadata document](active-directory-federation-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="5a3e9-113">To verify that the token is valid and actually originated from Azure AD, the application must validate the token’s signature using the public key exposed by Azure AD that is contained in the tenant’s [OpenID Connect discovery document](http://openid.net/specs/openid-connect-discovery-1_0.html) or SAML/WS-Fed [federation metadata document](active-directory-federation-metadata.md).</span></span>

<span data-ttu-id="5a3e9-114">For security purposes, Azure AD’s signing key rolls on a periodic basis and, in the case of an emergency, could be rolled over immediately.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-114">For security purposes, Azure AD’s signing key rolls on a periodic basis and, in the case of an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="5a3e9-115">Any application that integrates with Azure AD should be prepared to handle a key rollover event no matter how frequently it may occur.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-115">Any application that integrates with Azure AD should be prepared to handle a key rollover event no matter how frequently it may occur.</span></span> <span data-ttu-id="5a3e9-116">If it doesn’t, and your application attempts to use an expired key to verify the signature on a token, the sign-in request will fail.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-116">If it doesn’t, and your application attempts to use an expired key to verify the signature on a token, the sign-in request will fail.</span></span>

<span data-ttu-id="5a3e9-117">There is always more than one valid key available in the OpenID Connect discovery document and the federation metadata document.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-117">There is always more than one valid key available in the OpenID Connect discovery document and the federation metadata document.</span></span> <span data-ttu-id="5a3e9-118">Your application should be prepared to use any of the keys specified in the document, since one key may be rolled soon, another may be its replacement, and so forth.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-118">Your application should be prepared to use any of the keys specified in the document, since one key may be rolled soon, another may be its replacement, and so forth.</span></span>

## <a name="how-to-assess-if-your-application-will-be-affected-and-what-to-do-about-it"></a><span data-ttu-id="5a3e9-119">How to assess if your application will be affected and what to do about it</span><span class="sxs-lookup"><span data-stu-id="5a3e9-119">How to assess if your application will be affected and what to do about it</span></span>
<span data-ttu-id="5a3e9-120">How your application handles key rollover depends on variables such as the type of application or what identity protocol and library was used.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-120">How your application handles key rollover depends on variables such as the type of application or what identity protocol and library was used.</span></span> <span data-ttu-id="5a3e9-121">The sections below assess whether the most common types of applications are impacted by the key rollover and provide guidance on how to update the application to support automatic rollover or manually update the key.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-121">The sections below assess whether the most common types of applications are impacted by the key rollover and provide guidance on how to update the application to support automatic rollover or manually update the key.</span></span>

* [<span data-ttu-id="5a3e9-122">Native client applications accessing resources</span><span class="sxs-lookup"><span data-stu-id="5a3e9-122">Native client applications accessing resources</span></span>](#nativeclient)
* [<span data-ttu-id="5a3e9-123">Web applications / APIs accessing resources</span><span class="sxs-lookup"><span data-stu-id="5a3e9-123">Web applications / APIs accessing resources</span></span>](#webclient)
* [<span data-ttu-id="5a3e9-124">Web applications / APIs protecting resources and built using Azure App Services</span><span class="sxs-lookup"><span data-stu-id="5a3e9-124">Web applications / APIs protecting resources and built using Azure App Services</span></span>](#appservices)
* [<span data-ttu-id="5a3e9-125">Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span><span class="sxs-lookup"><span data-stu-id="5a3e9-125">Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>](#owin)
* [<span data-ttu-id="5a3e9-126">Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span><span class="sxs-lookup"><span data-stu-id="5a3e9-126">Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>](#owincore)
* [<span data-ttu-id="5a3e9-127">Web applications / APIs protecting resources using Node.js passport-azure-ad module</span><span class="sxs-lookup"><span data-stu-id="5a3e9-127">Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>](#passport)
* [<span data-ttu-id="5a3e9-128">Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="5a3e9-128">Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>](#vs2015)
* [<span data-ttu-id="5a3e9-129">Web applications protecting resources and created with Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="5a3e9-129">Web applications protecting resources and created with Visual Studio 2013</span></span>](#vs2013)
* [<span data-ttu-id="5a3e9-130">Web APIs protecting resources and created with Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="5a3e9-130">Web APIs protecting resources and created with Visual Studio 2013</span></span>](#vs2013_webapi)
* [<span data-ttu-id="5a3e9-131">Web applications protecting resources and created with Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="5a3e9-131">Web applications protecting resources and created with Visual Studio 2012</span></span>](#vs2012)
* [<span data-ttu-id="5a3e9-132">Web applications protecting resources and created with Visual Studio 2010, 2008 o using Windows Identity Foundation</span><span class="sxs-lookup"><span data-stu-id="5a3e9-132">Web applications protecting resources and created with Visual Studio 2010, 2008 o using Windows Identity Foundation</span></span>](#vs2010)
* [<span data-ttu-id="5a3e9-133">Web applications / APIs protecting resources using any other libraries or manually implementing any of the supported protocols</span><span class="sxs-lookup"><span data-stu-id="5a3e9-133">Web applications / APIs protecting resources using any other libraries or manually implementing any of the supported protocols</span></span>](#other)

<span data-ttu-id="5a3e9-134">This guidance is **not** applicable for:</span><span class="sxs-lookup"><span data-stu-id="5a3e9-134">This guidance is **not** applicable for:</span></span>

* <span data-ttu-id="5a3e9-135">Applications added from Azure AD Application Gallery (including Custom) have separate guidance with regards to signing keys.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-135">Applications added from Azure AD Application Gallery (including Custom) have separate guidance with regards to signing keys.</span></span> [<span data-ttu-id="5a3e9-136">More information.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-136">More information.</span></span>](../active-directory-sso-certs.md)
* <span data-ttu-id="5a3e9-137">On-premises applications published via application proxy don't have to worry about signing keys.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-137">On-premises applications published via application proxy don't have to worry about signing keys.</span></span>

### <a name="nativeclient"></a><span data-ttu-id="5a3e9-138">Native client applications accessing resources</span><span class="sxs-lookup"><span data-stu-id="5a3e9-138">Native client applications accessing resources</span></span>
<span data-ttu-id="5a3e9-139">Applications that are only accessing resources (i.e</span><span class="sxs-lookup"><span data-stu-id="5a3e9-139">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="5a3e9-140">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along to the resource owner.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-140">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along to the resource owner.</span></span> <span data-ttu-id="5a3e9-141">Given that they are not protecting any resources, they do not inspect the token and therefore do not need to ensure it is properly signed.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-141">Given that they are not protecting any resources, they do not inspect the token and therefore do not need to ensure it is properly signed.</span></span>

<span data-ttu-id="5a3e9-142">Native client applications, whether desktop or mobile, fall into this category and are thus not impacted by the rollover.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-142">Native client applications, whether desktop or mobile, fall into this category and are thus not impacted by the rollover.</span></span>

### <a name="webclient"></a><span data-ttu-id="5a3e9-143">Web applications / APIs accessing resources</span><span class="sxs-lookup"><span data-stu-id="5a3e9-143">Web applications / APIs accessing resources</span></span>
<span data-ttu-id="5a3e9-144">Applications that are only accessing resources (i.e</span><span class="sxs-lookup"><span data-stu-id="5a3e9-144">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="5a3e9-145">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along to the resource owner.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-145">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along to the resource owner.</span></span> <span data-ttu-id="5a3e9-146">Given that they are not protecting any resources, they do not inspect the token and therefore do not need to ensure it is properly signed.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-146">Given that they are not protecting any resources, they do not inspect the token and therefore do not need to ensure it is properly signed.</span></span>

<span data-ttu-id="5a3e9-147">Web applications and web APIs that are using the app-only flow (client credentials / client certificate), fall into this category and are thus not impacted by the rollover.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-147">Web applications and web APIs that are using the app-only flow (client credentials / client certificate), fall into this category and are thus not impacted by the rollover.</span></span>

### <a name="appservices"></a><span data-ttu-id="5a3e9-148">Web applications / APIs protecting resources and built using Azure App Services</span><span class="sxs-lookup"><span data-stu-id="5a3e9-148">Web applications / APIs protecting resources and built using Azure App Services</span></span>
<span data-ttu-id="5a3e9-149">Azure App Services' Authentication / Authorization (EasyAuth) functionality already has the necessary logic to handle key rollover automatically.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-149">Azure App Services' Authentication / Authorization (EasyAuth) functionality already has the necessary logic to handle key rollover automatically.</span></span>

### <a name="owin"></a><span data-ttu-id="5a3e9-150">Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span><span class="sxs-lookup"><span data-stu-id="5a3e9-150">Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>
<span data-ttu-id="5a3e9-151">If your application is using the .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware, it already has the necessary logic to handle key rollover automatically.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-151">If your application is using the .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware, it already has the necessary logic to handle key rollover automatically.</span></span>

<span data-ttu-id="5a3e9-152">You can confirm that your application is using any of these by looking for any of the following snippets in your application's Startup.cs or Startup.Auth.cs</span><span class="sxs-lookup"><span data-stu-id="5a3e9-152">You can confirm that your application is using any of these by looking for any of the following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseWsFederationAuthentication(
    new WsFederationAuthenticationOptions
    {
     // ...
     });
```
```
 app.UseWindowsAzureActiveDirectoryBearerAuthentication(
     new WindowsAzureActiveDirectoryBearerAuthenticationOptions
     {
     // ...
     });
```

### <a name="owincore"></a><span data-ttu-id="5a3e9-153">Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span><span class="sxs-lookup"><span data-stu-id="5a3e9-153">Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>
<span data-ttu-id="5a3e9-154">If your application is using the .NET Core OWIN OpenID Connect  or JwtBearerAuthentication middleware, it already has the necessary logic to handle key rollover automatically.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-154">If your application is using the .NET Core OWIN OpenID Connect  or JwtBearerAuthentication middleware, it already has the necessary logic to handle key rollover automatically.</span></span>

<span data-ttu-id="5a3e9-155">You can confirm that your application is using any of these by looking for any of the following snippets in your application's Startup.cs or Startup.Auth.cs</span><span class="sxs-lookup"><span data-stu-id="5a3e9-155">You can confirm that your application is using any of these by looking for any of the following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseJwtBearerAuthentication(
    new JwtBearerAuthenticationOptions
    {
     // ...
     });
```

### <a name="passport"></a><span data-ttu-id="5a3e9-156">Web applications / APIs protecting resources using Node.js passport-azure-ad module</span><span class="sxs-lookup"><span data-stu-id="5a3e9-156">Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>
<span data-ttu-id="5a3e9-157">If your application is using the Node.js passport-ad module, it already has the necessary logic to handle key rollover automatically.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-157">If your application is using the Node.js passport-ad module, it already has the necessary logic to handle key rollover automatically.</span></span>

<span data-ttu-id="5a3e9-158">You can confirm that your application passport-ad by searching for the following snippet in your application's app.js</span><span class="sxs-lookup"><span data-stu-id="5a3e9-158">You can confirm that your application passport-ad by searching for the following snippet in your application's app.js</span></span>

```
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

passport.use(new OIDCStrategy({
    //...
));
```

### <a name="vs2015"></a><span data-ttu-id="5a3e9-159">Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="5a3e9-159">Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>
<span data-ttu-id="5a3e9-160">If your application was built using a web application template in Visual Studio 2015 or Visual Studio 2017 and you selected **Work And School Accounts** from the **Change Authentication** menu, it already has the necessary logic to handle key rollover automatically.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-160">If your application was built using a web application template in Visual Studio 2015 or Visual Studio 2017 and you selected **Work And School Accounts** from the **Change Authentication** menu, it already has the necessary logic to handle key rollover automatically.</span></span> <span data-ttu-id="5a3e9-161">This logic, embedded in the OWIN OpenID Connect middleware, retrieves and caches the keys from the OpenID Connect discovery document and periodically refreshes them.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-161">This logic, embedded in the OWIN OpenID Connect middleware, retrieves and caches the keys from the OpenID Connect discovery document and periodically refreshes them.</span></span>

<span data-ttu-id="5a3e9-162">If you added authentication to your solution manually, your application might not have the necessary key rollover logic.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-162">If you added authentication to your solution manually, your application might not have the necessary key rollover logic.</span></span> <span data-ttu-id="5a3e9-163">You will need to write it yourself, or follow the steps in [Web applications / APIs using any other libraries or manually implementing any of the supported protocols.](#other).</span><span class="sxs-lookup"><span data-stu-id="5a3e9-163">You will need to write it yourself, or follow the steps in [Web applications / APIs using any other libraries or manually implementing any of the supported protocols.](#other).</span></span>

### <a name="vs2013"></a><span data-ttu-id="5a3e9-164">Web applications protecting resources and created with Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="5a3e9-164">Web applications protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="5a3e9-165">If your application was built using a web application template in Visual Studio 2013 and you selected **Organizational Accounts** from the **Change Authentication** menu, it already has the necessary logic to handle key rollover automatically.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-165">If your application was built using a web application template in Visual Studio 2013 and you selected **Organizational Accounts** from the **Change Authentication** menu, it already has the necessary logic to handle key rollover automatically.</span></span> <span data-ttu-id="5a3e9-166">This logic stores your organization’s unique identifier and the signing key information in two database tables associated with the project.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-166">This logic stores your organization’s unique identifier and the signing key information in two database tables associated with the project.</span></span> <span data-ttu-id="5a3e9-167">You can find the connection string for the database in the project’s Web.config file.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-167">You can find the connection string for the database in the project’s Web.config file.</span></span>

<span data-ttu-id="5a3e9-168">If you added authentication to your solution manually, your application might not have the necessary key rollover logic.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-168">If you added authentication to your solution manually, your application might not have the necessary key rollover logic.</span></span> <span data-ttu-id="5a3e9-169">You will need to write it yourself, or follow the steps in [Web applications / APIs using any other libraries or manually implementing any of the supported protocols.](#other).</span><span class="sxs-lookup"><span data-stu-id="5a3e9-169">You will need to write it yourself, or follow the steps in [Web applications / APIs using any other libraries or manually implementing any of the supported protocols.](#other).</span></span>

<span data-ttu-id="5a3e9-170">The following steps will help you verify that the logic is working properly in your application.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-170">The following steps will help you verify that the logic is working properly in your application.</span></span>

1. <span data-ttu-id="5a3e9-171">In Visual Studio 2013, open the solution, and then click on the **Server Explorer** tab on the right window.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-171">In Visual Studio 2013, open the solution, and then click on the **Server Explorer** tab on the right window.</span></span>
2. <span data-ttu-id="5a3e9-172">Expand **Data Connections**, **DefaultConnection**, and then **Tables**.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-172">Expand **Data Connections**, **DefaultConnection**, and then **Tables**.</span></span> <span data-ttu-id="5a3e9-173">Locate the **IssuingAuthorityKeys** table, right-click it, and then click **Show Table Data**.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-173">Locate the **IssuingAuthorityKeys** table, right-click it, and then click **Show Table Data**.</span></span>
3. <span data-ttu-id="5a3e9-174">In the **IssuingAuthorityKeys** table, there will be at least one row, which corresponds to the thumbprint value for the key.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-174">In the **IssuingAuthorityKeys** table, there will be at least one row, which corresponds to the thumbprint value for the key.</span></span> <span data-ttu-id="5a3e9-175">Delete any rows in the table.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-175">Delete any rows in the table.</span></span>
4. <span data-ttu-id="5a3e9-176">Right-click the **Tenants** table, and then click **Show Table Data**.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-176">Right-click the **Tenants** table, and then click **Show Table Data**.</span></span>
5. <span data-ttu-id="5a3e9-177">In the **Tenants** table, there will be at least one row, which corresponds to a unique directory tenant identifier.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-177">In the **Tenants** table, there will be at least one row, which corresponds to a unique directory tenant identifier.</span></span> <span data-ttu-id="5a3e9-178">Delete any rows in the table.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-178">Delete any rows in the table.</span></span> <span data-ttu-id="5a3e9-179">If you don't delete the rows in both the **Tenants** table and **IssuingAuthorityKeys** table, you will get an error at runtime.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-179">If you don't delete the rows in both the **Tenants** table and **IssuingAuthorityKeys** table, you will get an error at runtime.</span></span>
6. <span data-ttu-id="5a3e9-180">Build and run the application.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-180">Build and run the application.</span></span> <span data-ttu-id="5a3e9-181">After you have logged in to your account, you can stop the application.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-181">After you have logged in to your account, you can stop the application.</span></span>
7. <span data-ttu-id="5a3e9-182">Return to the **Server Explorer** and look at the values in the **IssuingAuthorityKeys** and **Tenants** table.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-182">Return to the **Server Explorer** and look at the values in the **IssuingAuthorityKeys** and **Tenants** table.</span></span> <span data-ttu-id="5a3e9-183">You’ll notice that they have been automatically repopulated with the appropriate information from the federation metadata document.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-183">You’ll notice that they have been automatically repopulated with the appropriate information from the federation metadata document.</span></span>

### <a name="vs2013"></a><span data-ttu-id="5a3e9-184">Web APIs protecting resources and created with Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="5a3e9-184">Web APIs protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="5a3e9-185">If you created a web API application in Visual Studio 2013 using the Web API template, and then selected **Organizational Accounts** from the **Change Authentication** menu, you already have the necessary logic in your application.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-185">If you created a web API application in Visual Studio 2013 using the Web API template, and then selected **Organizational Accounts** from the **Change Authentication** menu, you already have the necessary logic in your application.</span></span>

<span data-ttu-id="5a3e9-186">If you manually configured authentication, follow the instructions below to learn how to configure your Web API to automatically update its key information.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-186">If you manually configured authentication, follow the instructions below to learn how to configure your Web API to automatically update its key information.</span></span>

<span data-ttu-id="5a3e9-187">The following code snippet demonstrates how to get the latest keys from the federation metadata document, and then use the [JWT Token Handler](https://msdn.microsoft.com/library/dn205065.aspx) to validate the token.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-187">The following code snippet demonstrates how to get the latest keys from the federation metadata document, and then use the [JWT Token Handler](https://msdn.microsoft.com/library/dn205065.aspx) to validate the token.</span></span> <span data-ttu-id="5a3e9-188">The code snippet assumes that you will use your own caching mechanism for persisting the key to validate future tokens from Azure AD, whether it be in a database, configuration file, or elsewhere.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-188">The code snippet assumes that you will use your own caching mechanism for persisting the key to validate future tokens from Azure AD, whether it be in a database, configuration file, or elsewhere.</span></span>

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IdentityModel.Tokens;
using System.Configuration;
using System.Security.Cryptography.X509Certificates;
using System.Xml;
using System.IdentityModel.Metadata;
using System.ServiceModel.Security;
using System.Threading;

namespace JWTValidation
{
    public class JWTValidator
    {
        private string MetadataAddress = "[Your Federation Metadata document address goes here]";

        // Validates the JWT Token that's part of the Authorization header in an HTTP request.
        public void ValidateJwtToken(string token)
        {
            JwtSecurityTokenHandler tokenHandler = new JwtSecurityTokenHandler()
            {
                // Do not disable for production code
                CertificateValidator = X509CertificateValidator.None
            };

            TokenValidationParameters validationParams = new TokenValidationParameters()
            {
                AllowedAudience = "[Your App ID URI goes here, as registered in the Azure Classic Portal]",
                ValidIssuer = "[The issuer for the token goes here, such as https://sts.windows.net/68b98905-130e-4d7c-b6e1-a158a9ed8449/]",
                SigningTokens = GetSigningCertificates(MetadataAddress)

                // Cache the signing tokens by your desired mechanism
            };

            Thread.CurrentPrincipal = tokenHandler.ValidateToken(token, validationParams);
        }

        // Returns a list of certificates from the specified metadata document.
        public List<X509SecurityToken> GetSigningCertificates(string metadataAddress)
        {
            List<X509SecurityToken> tokens = new List<X509SecurityToken>();

            if (metadataAddress == null)
            {
                throw new ArgumentNullException(metadataAddress);
            }

            using (XmlReader metadataReader = XmlReader.Create(metadataAddress))
            {
                MetadataSerializer serializer = new MetadataSerializer()
                {
                    // Do not disable for production code
                    CertificateValidationMode = X509CertificateValidationMode.None
                };

                EntityDescriptor metadata = serializer.ReadMetadata(metadataReader) as EntityDescriptor;

                if (metadata != null)
                {
                    SecurityTokenServiceDescriptor stsd = metadata.RoleDescriptors.OfType<SecurityTokenServiceDescriptor>().First();

                    if (stsd != null)
                    {
                        IEnumerable<X509RawDataKeyIdentifierClause> x509DataClauses = stsd.Keys.Where(key => key.KeyInfo != null && (key.Use == KeyType.Signing || key.Use == KeyType.Unspecified)).
                                                             Select(key => key.KeyInfo.OfType<X509RawDataKeyIdentifierClause>().First());

                        tokens.AddRange(x509DataClauses.Select(token => new X509SecurityToken(new X509Certificate2(token.GetX509RawData()))));
                    }
                    else
                    {
                        throw new InvalidOperationException("There is no RoleDescriptor of type SecurityTokenServiceType in the metadata");
                    }
                }
                else
                {
                    throw new Exception("Invalid Federation Metadata document");
                }
            }
            return tokens;
        }
    }
}
```

### <a name="vs2012"></a><span data-ttu-id="5a3e9-189">Web applications protecting resources and created with Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="5a3e9-189">Web applications protecting resources and created with Visual Studio 2012</span></span>
<span data-ttu-id="5a3e9-190">If your application was built in Visual Studio 2012, you probably used the Identity and Access Tool to configure your application.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-190">If your application was built in Visual Studio 2012, you probably used the Identity and Access Tool to configure your application.</span></span> <span data-ttu-id="5a3e9-191">It’s also likely that you are using the [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx).</span><span class="sxs-lookup"><span data-stu-id="5a3e9-191">It’s also likely that you are using the [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx).</span></span> <span data-ttu-id="5a3e9-192">The VINR is responsible for maintaining information about trusted identity providers (Azure AD) and the keys used to validate tokens issued by them.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-192">The VINR is responsible for maintaining information about trusted identity providers (Azure AD) and the keys used to validate tokens issued by them.</span></span> <span data-ttu-id="5a3e9-193">The VINR also makes it easy to automatically update the key information stored in a Web.config file by downloading the latest federation metadata document associated with your directory, checking if the configuration is out of date with the latest document, and updating the application to use the new key as necessary.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-193">The VINR also makes it easy to automatically update the key information stored in a Web.config file by downloading the latest federation metadata document associated with your directory, checking if the configuration is out of date with the latest document, and updating the application to use the new key as necessary.</span></span>

<span data-ttu-id="5a3e9-194">If you created your application using any of the code samples or walkthrough documentation provided by Microsoft, the key rollover logic is already included in your project.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-194">If you created your application using any of the code samples or walkthrough documentation provided by Microsoft, the key rollover logic is already included in your project.</span></span> <span data-ttu-id="5a3e9-195">You will notice that the code below already exists in your project.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-195">You will notice that the code below already exists in your project.</span></span> <span data-ttu-id="5a3e9-196">If your application does not already have this logic, follow the steps below to add it and to verify that it’s working correctly.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-196">If your application does not already have this logic, follow the steps below to add it and to verify that it’s working correctly.</span></span>

1. <span data-ttu-id="5a3e9-197">In **Solution Explorer**, add a reference to the **System.IdentityModel** assembly for the appropriate project.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-197">In **Solution Explorer**, add a reference to the **System.IdentityModel** assembly for the appropriate project.</span></span>
2. <span data-ttu-id="5a3e9-198">Open the **Global.asax.cs** file and add the following using directives:</span><span class="sxs-lookup"><span data-stu-id="5a3e9-198">Open the **Global.asax.cs** file and add the following using directives:</span></span>
   ```
   using System.Configuration;
   using System.IdentityModel.Tokens;
   ```
3. <span data-ttu-id="5a3e9-199">Add the following method to the **Global.asax.cs** file:</span><span class="sxs-lookup"><span data-stu-id="5a3e9-199">Add the following method to the **Global.asax.cs** file:</span></span>
   ```
   protected void RefreshValidationSettings()
   {
    string configPath = AppDomain.CurrentDomain.BaseDirectory + "\\" + "Web.config";
    string metadataAddress =
                  ConfigurationManager.AppSettings["ida:FederationMetadataLocation"];
    ValidatingIssuerNameRegistry.WriteToConfig(metadataAddress, configPath);
   }
   ```
4. <span data-ttu-id="5a3e9-200">Invoke the **RefreshValidationSettings()** method in the **Application_Start()** method in **Global.asax.cs** as shown:</span><span class="sxs-lookup"><span data-stu-id="5a3e9-200">Invoke the **RefreshValidationSettings()** method in the **Application_Start()** method in **Global.asax.cs** as shown:</span></span>
   ```
   protected void Application_Start()
   {
    AreaRegistration.RegisterAllAreas();
    ...
    RefreshValidationSettings();
   }
   ```

<span data-ttu-id="5a3e9-201">Once you have followed these steps, your application’s Web.config will be updated with the latest information from the federation metadata document, including the latest keys.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-201">Once you have followed these steps, your application’s Web.config will be updated with the latest information from the federation metadata document, including the latest keys.</span></span> <span data-ttu-id="5a3e9-202">This update will occur every time your application pool recycles in IIS; by default IIS is set to recycle applications every 29 hours.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-202">This update will occur every time your application pool recycles in IIS; by default IIS is set to recycle applications every 29 hours.</span></span>

<span data-ttu-id="5a3e9-203">Follow the steps below to verify that the key rollover logic is working.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-203">Follow the steps below to verify that the key rollover logic is working.</span></span>

1. <span data-ttu-id="5a3e9-204">After you have verified that your application is using the code above, open the **Web.config** file and navigate to the **<issuerNameRegistry>** block, specifically looking for the following few lines:</span><span class="sxs-lookup"><span data-stu-id="5a3e9-204">After you have verified that your application is using the code above, open the **Web.config** file and navigate to the **<issuerNameRegistry>** block, specifically looking for the following few lines:</span></span>
   ```
   <issuerNameRegistry type="System.IdentityModel.Tokens.ValidatingIssuerNameRegistry, System.IdentityModel.Tokens.ValidatingIssuerNameRegistry">
        <authority name="https://sts.windows.net/ec4187af-07da-4f01-b18f-64c2f5abecea/">
          <keys>
            <add thumbprint="3A38FA984E8560F19AADC9F86FE9594BB6AD049B" />
          </keys>
   ```
2. <span data-ttu-id="5a3e9-205">In the **<add thumbprint=””>** setting, change the thumbprint value by replacing any character with a different one.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-205">In the **<add thumbprint=””>** setting, change the thumbprint value by replacing any character with a different one.</span></span> <span data-ttu-id="5a3e9-206">Save the **Web.config** file.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-206">Save the **Web.config** file.</span></span>
3. <span data-ttu-id="5a3e9-207">Build the application, and then run it.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-207">Build the application, and then run it.</span></span> <span data-ttu-id="5a3e9-208">If you can complete the sign-in process, your application is successfully updating the key by downloading the required information from your directory’s federation metadata document.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-208">If you can complete the sign-in process, your application is successfully updating the key by downloading the required information from your directory’s federation metadata document.</span></span> <span data-ttu-id="5a3e9-209">If you are having issues signing in, ensure the changes in your application are correct by reading the [Adding Sign-On to Your Web Application Using Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) topic, or downloading and inspecting the following code sample: [Multi-Tenant Cloud Application for Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).</span><span class="sxs-lookup"><span data-stu-id="5a3e9-209">If you are having issues signing in, ensure the changes in your application are correct by reading the [Adding Sign-On to Your Web Application Using Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) topic, or downloading and inspecting the following code sample: [Multi-Tenant Cloud Application for Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).</span></span>

### <a name="vs2010"></a><span data-ttu-id="5a3e9-210">Web applications protecting resources and created with Visual Studio 2008 or 2010 and Windows Identity Foundation (WIF) v1.0 for .NET 3.5</span><span class="sxs-lookup"><span data-stu-id="5a3e9-210">Web applications protecting resources and created with Visual Studio 2008 or 2010 and Windows Identity Foundation (WIF) v1.0 for .NET 3.5</span></span>
<span data-ttu-id="5a3e9-211">If you built an application on WIF v1.0, there is no provided mechanism to automatically refresh your application’s configuration to use a new key.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-211">If you built an application on WIF v1.0, there is no provided mechanism to automatically refresh your application’s configuration to use a new key.</span></span>

* <span data-ttu-id="5a3e9-212">*Easiest way* Use the FedUtil tooling included in the WIF SDK, which can retrieve the latest metadata document and update your configuration.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-212">*Easiest way* Use the FedUtil tooling included in the WIF SDK, which can retrieve the latest metadata document and update your configuration.</span></span>
* <span data-ttu-id="5a3e9-213">Update your application to .NET 4.5, which includes the newest version of WIF located in the System namespace.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-213">Update your application to .NET 4.5, which includes the newest version of WIF located in the System namespace.</span></span> <span data-ttu-id="5a3e9-214">You can then use the [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) to perform automatic updates of the application’s configuration.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-214">You can then use the [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) to perform automatic updates of the application’s configuration.</span></span>
* <span data-ttu-id="5a3e9-215">Perform a manual rollover as per the instructions at the end of this guidance document.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-215">Perform a manual rollover as per the instructions at the end of this guidance document.</span></span>

<span data-ttu-id="5a3e9-216">Instructions to use the FedUtil to update your configuration:</span><span class="sxs-lookup"><span data-stu-id="5a3e9-216">Instructions to use the FedUtil to update your configuration:</span></span>

1. <span data-ttu-id="5a3e9-217">Verify that you have the WIF v1.0 SDK installed on your development machine for Visual Studio 2008 or 2010.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-217">Verify that you have the WIF v1.0 SDK installed on your development machine for Visual Studio 2008 or 2010.</span></span> <span data-ttu-id="5a3e9-218">You can [download it from here](https://www.microsoft.com/en-us/download/details.aspx?id=4451) if you have not yet installed it.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-218">You can [download it from here](https://www.microsoft.com/en-us/download/details.aspx?id=4451) if you have not yet installed it.</span></span>
2. <span data-ttu-id="5a3e9-219">In Visual Studio, open the solution, and then right-click the applicable project and select **Update federation metadata**.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-219">In Visual Studio, open the solution, and then right-click the applicable project and select **Update federation metadata**.</span></span> <span data-ttu-id="5a3e9-220">If this option is not available, FedUtil and/or the WIF v1.0 SDK has not been installed.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-220">If this option is not available, FedUtil and/or the WIF v1.0 SDK has not been installed.</span></span>
3. <span data-ttu-id="5a3e9-221">From the prompt, select **Update** to begin updating your federation metadata.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-221">From the prompt, select **Update** to begin updating your federation metadata.</span></span> <span data-ttu-id="5a3e9-222">If you have access to the server environment where the application is hosted, you can optionally use FedUtil’s [automatic metadata update scheduler](https://msdn.microsoft.com/library/ee517272.aspx).</span><span class="sxs-lookup"><span data-stu-id="5a3e9-222">If you have access to the server environment where the application is hosted, you can optionally use FedUtil’s [automatic metadata update scheduler](https://msdn.microsoft.com/library/ee517272.aspx).</span></span>
4. <span data-ttu-id="5a3e9-223">Click **Finish** to complete the update process.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-223">Click **Finish** to complete the update process.</span></span>

### <a name="other"></a><span data-ttu-id="5a3e9-224">Web applications / APIs protecting resources using any other libraries or manually implementing any of the supported protocols</span><span class="sxs-lookup"><span data-stu-id="5a3e9-224">Web applications / APIs protecting resources using any other libraries or manually implementing any of the supported protocols</span></span>
<span data-ttu-id="5a3e9-225">If you are using some other library or manually implemented any of the supported protocols, you'll need to review the library or your implementation to ensure that the key is being retrieved from either the OpenID Connect discovery document or the federation metadata document.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-225">If you are using some other library or manually implemented any of the supported protocols, you'll need to review the library or your implementation to ensure that the key is being retrieved from either the OpenID Connect discovery document or the federation metadata document.</span></span> <span data-ttu-id="5a3e9-226">One way to check for this is to do a search in your code or the library's code for any calls out to either the OpenID discovery document or the federation metadata document.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-226">One way to check for this is to do a search in your code or the library's code for any calls out to either the OpenID discovery document or the federation metadata document.</span></span>

<span data-ttu-id="5a3e9-227">If they key is being stored somewhere or hardcoded in your application, you can manually retrieve the key and update it accordingly by perform a manual rollover as per the instructions at the end of this guidance document.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-227">If they key is being stored somewhere or hardcoded in your application, you can manually retrieve the key and update it accordingly by perform a manual rollover as per the instructions at the end of this guidance document.</span></span> <span data-ttu-id="5a3e9-228">**It is strongly encouraged that you enhance your application to support automatic rollover** using any of the approaches outline in this article to avoid future disruptions and overhead if Azure AD increases it's rollover cadence or has an emergency out-of-band rollover.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-228">**It is strongly encouraged that you enhance your application to support automatic rollover** using any of the approaches outline in this article to avoid future disruptions and overhead if Azure AD increases it's rollover cadence or has an emergency out-of-band rollover.</span></span>

## <a name="how-to-test-your-application-to-determine-if-it-will-be-affected"></a><span data-ttu-id="5a3e9-229">How to test your application to determine if it will be affected</span><span class="sxs-lookup"><span data-stu-id="5a3e9-229">How to test your application to determine if it will be affected</span></span>
<span data-ttu-id="5a3e9-230">You can validate whether your application supports automatic key rollover by downloading the scripts and following the instructions in [this GitHub repository.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span><span class="sxs-lookup"><span data-stu-id="5a3e9-230">You can validate whether your application supports automatic key rollover by downloading the scripts and following the instructions in [this GitHub repository.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span></span>

## <a name="how-to-perform-a-manual-rollover-if-you-application-does-not-support-automatic-rollover"></a><span data-ttu-id="5a3e9-231">How to perform a manual rollover if you application does not support automatic rollover</span><span class="sxs-lookup"><span data-stu-id="5a3e9-231">How to perform a manual rollover if you application does not support automatic rollover</span></span>
<span data-ttu-id="5a3e9-232">If your application does **not** support automatic rollover, you will need to establish a process that periodically monitors Azure AD's signing keys and performs a manual rollover accordingly.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-232">If your application does **not** support automatic rollover, you will need to establish a process that periodically monitors Azure AD's signing keys and performs a manual rollover accordingly.</span></span> <span data-ttu-id="5a3e9-233">[This GitHub repository](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) contains scripts and instructions on how to do this.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-233">[This GitHub repository](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) contains scripts and instructions on how to do this.</span></span>

