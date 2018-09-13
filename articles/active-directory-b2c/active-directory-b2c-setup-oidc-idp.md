---
title: Adding OpenID Connect identity providers in built-in policies in Azure Active Directory B2C | Microsoft Docs
description: Overview guide on how to add OpenID Connect providers in built-in policies within Azure AD B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 04/27/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: e5baf95cd2426c9753620cba7c5a67b4c1672788
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871166"
---
# <a name="azure-active-directory-b2c-add-a-custom-openid-connect-identity-provider-in-built-in-policies"></a><span data-ttu-id="7ee46-103">Azure Active Directory B2C: Add a custom OpenID Connect identity provider in built-in policies</span><span class="sxs-lookup"><span data-stu-id="7ee46-103">Azure Active Directory B2C: Add a custom OpenID Connect identity provider in built-in policies</span></span>

>[!NOTE]
> <span data-ttu-id="7ee46-104">This feature is in public preview.</span><span class="sxs-lookup"><span data-stu-id="7ee46-104">This feature is in public preview.</span></span> <span data-ttu-id="7ee46-105">Do not use the feature in production environments.</span><span class="sxs-lookup"><span data-stu-id="7ee46-105">Do not use the feature in production environments.</span></span>

<span data-ttu-id="7ee46-106">[OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html) is an authentication protocol, built on top of OAuth 2.0, that can be used to securely sign users in.</span><span class="sxs-lookup"><span data-stu-id="7ee46-106">[OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html) is an authentication protocol, built on top of OAuth 2.0, that can be used to securely sign users in.</span></span> <span data-ttu-id="7ee46-107">Most identity providers that use this protocol, such as [Azure AD](active-directory-b2c-setup-oidc-azure-active-directory.md), are supported in Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="7ee46-107">Most identity providers that use this protocol, such as [Azure AD](active-directory-b2c-setup-oidc-azure-active-directory.md), are supported in Azure AD B2C.</span></span> <span data-ttu-id="7ee46-108">This article explains how you can add custom OpenID Connect identity providers into your built-in policies.</span><span class="sxs-lookup"><span data-stu-id="7ee46-108">This article explains how you can add custom OpenID Connect identity providers into your built-in policies.</span></span>

## <a name="configuring-a-custom-openid-connect-identity-provider"></a><span data-ttu-id="7ee46-109">Configuring a custom OpenID Connect identity provider</span><span class="sxs-lookup"><span data-stu-id="7ee46-109">Configuring a custom OpenID Connect identity provider</span></span>

<span data-ttu-id="7ee46-110">To add a custom OpenID Connect identity provider:</span><span class="sxs-lookup"><span data-stu-id="7ee46-110">To add a custom OpenID Connect identity provider:</span></span>

1. <span data-ttu-id="7ee46-111">Follow these steps to [navigate to the Azure AD B2C settings](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7ee46-111">Follow these steps to [navigate to the Azure AD B2C settings](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) in the Azure portal.</span></span>
1. <span data-ttu-id="7ee46-112">Click on **Identity Providers**.</span><span class="sxs-lookup"><span data-stu-id="7ee46-112">Click on **Identity Providers**.</span></span>
1. <span data-ttu-id="7ee46-113">Click on **Add**.</span><span class="sxs-lookup"><span data-stu-id="7ee46-113">Click on **Add**.</span></span>
1. <span data-ttu-id="7ee46-114">For the **Identity provider type**, select **OpenID Connect**.</span><span class="sxs-lookup"><span data-stu-id="7ee46-114">For the **Identity provider type**, select **OpenID Connect**.</span></span>

### <a name="setting-up-the-openid-connect-identity-provider"></a><span data-ttu-id="7ee46-115">Setting up the OpenID Connect identity provider</span><span class="sxs-lookup"><span data-stu-id="7ee46-115">Setting up the OpenID Connect identity provider</span></span>

#### <a name="metadata-url"></a><span data-ttu-id="7ee46-116">Metadata URL</span><span class="sxs-lookup"><span data-stu-id="7ee46-116">Metadata URL</span></span>

<span data-ttu-id="7ee46-117">As per specification, every OpenID Connect identity providers describes a metadata document that contains most of the information required to perform sign-in.</span><span class="sxs-lookup"><span data-stu-id="7ee46-117">As per specification, every OpenID Connect identity providers describes a metadata document that contains most of the information required to perform sign-in.</span></span> <span data-ttu-id="7ee46-118">This includes information such as the URLs to use and the location of the service's public signing keys.</span><span class="sxs-lookup"><span data-stu-id="7ee46-118">This includes information such as the URLs to use and the location of the service's public signing keys.</span></span> <span data-ttu-id="7ee46-119">The OpenID Connect metadata document is always located at an endpoint that ends in `.well-known\openid-configuration`.</span><span class="sxs-lookup"><span data-stu-id="7ee46-119">The OpenID Connect metadata document is always located at an endpoint that ends in `.well-known\openid-configuration`.</span></span>

<span data-ttu-id="7ee46-120">For the OpenID Connect identity provider you are looking to add, enter its metadata URL.</span><span class="sxs-lookup"><span data-stu-id="7ee46-120">For the OpenID Connect identity provider you are looking to add, enter its metadata URL.</span></span>

#### <a name="client-id-and-secret"></a><span data-ttu-id="7ee46-121">Client ID and secret</span><span class="sxs-lookup"><span data-stu-id="7ee46-121">Client ID and secret</span></span>

<span data-ttu-id="7ee46-122">To allow users to sign in, the identity provider will require developers to register an application in their service.</span><span class="sxs-lookup"><span data-stu-id="7ee46-122">To allow users to sign in, the identity provider will require developers to register an application in their service.</span></span> <span data-ttu-id="7ee46-123">This application will have an ID (referred to as the **client ID**) and a **client secret**.</span><span class="sxs-lookup"><span data-stu-id="7ee46-123">This application will have an ID (referred to as the **client ID**) and a **client secret**.</span></span> <span data-ttu-id="7ee46-124">Copy these values from the identity provider and enter them into the corresponding fields.</span><span class="sxs-lookup"><span data-stu-id="7ee46-124">Copy these values from the identity provider and enter them into the corresponding fields.</span></span>

> [!NOTE]
> <span data-ttu-id="7ee46-125">The client secret is optional.</span><span class="sxs-lookup"><span data-stu-id="7ee46-125">The client secret is optional.</span></span> <span data-ttu-id="7ee46-126">However, you must enter a client secret if you would like to use the [authorization code flow](http://openid.net/specs/openid-connect-core-1_0.html#CodeFlowAuth), which uses the secret to exchange the code for the token.</span><span class="sxs-lookup"><span data-stu-id="7ee46-126">However, you must enter a client secret if you would like to use the [authorization code flow](http://openid.net/specs/openid-connect-core-1_0.html#CodeFlowAuth), which uses the secret to exchange the code for the token.</span></span>

#### <a name="scope"></a><span data-ttu-id="7ee46-127">Scope</span><span class="sxs-lookup"><span data-stu-id="7ee46-127">Scope</span></span>

<span data-ttu-id="7ee46-128">Scopes define the information and permissions you are looking to gather from your custom identity provider.</span><span class="sxs-lookup"><span data-stu-id="7ee46-128">Scopes define the information and permissions you are looking to gather from your custom identity provider.</span></span> <span data-ttu-id="7ee46-129">OpenID Connect requests must contain the `openid` scope value in order to receive the ID token from the identity provider.</span><span class="sxs-lookup"><span data-stu-id="7ee46-129">OpenID Connect requests must contain the `openid` scope value in order to receive the ID token from the identity provider.</span></span> <span data-ttu-id="7ee46-130">Without the ID token, users will not be able to sign into Azure AD B2C using the custom identity provider.</span><span class="sxs-lookup"><span data-stu-id="7ee46-130">Without the ID token, users will not be able to sign into Azure AD B2C using the custom identity provider.</span></span>

<span data-ttu-id="7ee46-131">Other scopes can be appended (separated by space).</span><span class="sxs-lookup"><span data-stu-id="7ee46-131">Other scopes can be appended (separated by space).</span></span> <span data-ttu-id="7ee46-132">Refer to the custom identity provider's documentation to see what other scopes may be available.</span><span class="sxs-lookup"><span data-stu-id="7ee46-132">Refer to the custom identity provider's documentation to see what other scopes may be available.</span></span>

#### <a name="response-type"></a><span data-ttu-id="7ee46-133">Response type</span><span class="sxs-lookup"><span data-stu-id="7ee46-133">Response type</span></span>

<span data-ttu-id="7ee46-134">The response type describes what kind of information will be sent back in the initial call to the `authorization_endpoint` of the custom identity provider.</span><span class="sxs-lookup"><span data-stu-id="7ee46-134">The response type describes what kind of information will be sent back in the initial call to the `authorization_endpoint` of the custom identity provider.</span></span> 

* <span data-ttu-id="7ee46-135">`code`: As per the [authorization code flow](http://openid.net/specs/openid-connect-core-1_0.html#CodeFlowAuth), a code will be returned back to Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="7ee46-135">`code`: As per the [authorization code flow](http://openid.net/specs/openid-connect-core-1_0.html#CodeFlowAuth), a code will be returned back to Azure AD B2C.</span></span> <span data-ttu-id="7ee46-136">Azure AD B2C will then proceed to call the `token_endpoint` to exchange the code for the token.</span><span class="sxs-lookup"><span data-stu-id="7ee46-136">Azure AD B2C will then proceed to call the `token_endpoint` to exchange the code for the token.</span></span>
* <span data-ttu-id="7ee46-137">`token`: An access token will be returned back to Azure AD B2C from the custom identity provider.</span><span class="sxs-lookup"><span data-stu-id="7ee46-137">`token`: An access token will be returned back to Azure AD B2C from the custom identity provider.</span></span>
* <span data-ttu-id="7ee46-138">`id_token`: An ID token will be returned back to Azure AD B2C from the custom identity provider.</span><span class="sxs-lookup"><span data-stu-id="7ee46-138">`id_token`: An ID token will be returned back to Azure AD B2C from the custom identity provider.</span></span>


#### <a name="response-mode"></a><span data-ttu-id="7ee46-139">Response mode</span><span class="sxs-lookup"><span data-stu-id="7ee46-139">Response mode</span></span>

<span data-ttu-id="7ee46-140">The response mode defines the method that should be used to send the data back from the custom identity provider to Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="7ee46-140">The response mode defines the method that should be used to send the data back from the custom identity provider to Azure AD B2C.</span></span>

* <span data-ttu-id="7ee46-141">`form_post`: This response mode is recommended for best security.</span><span class="sxs-lookup"><span data-stu-id="7ee46-141">`form_post`: This response mode is recommended for best security.</span></span> <span data-ttu-id="7ee46-142">The response is transmitted via the HTTP `POST` method, with the code or token being encoded in the body using the `application/x-www-form-urlencoded` format.</span><span class="sxs-lookup"><span data-stu-id="7ee46-142">The response is transmitted via the HTTP `POST` method, with the code or token being encoded in the body using the `application/x-www-form-urlencoded` format.</span></span>
* <span data-ttu-id="7ee46-143">`query`: The code or token will be returned as a query parameter.</span><span class="sxs-lookup"><span data-stu-id="7ee46-143">`query`: The code or token will be returned as a query parameter.</span></span>


#### <a name="domain-hint"></a><span data-ttu-id="7ee46-144">Domain hint</span><span class="sxs-lookup"><span data-stu-id="7ee46-144">Domain hint</span></span>

<span data-ttu-id="7ee46-145">The domain hint can be used to skip directly to the sign in page of the specified identity provider, instead of having the user make a selection among the list of available identity providers.</span><span class="sxs-lookup"><span data-stu-id="7ee46-145">The domain hint can be used to skip directly to the sign in page of the specified identity provider, instead of having the user make a selection among the list of available identity providers.</span></span> <span data-ttu-id="7ee46-146">To allow this kind of behavior, enter a value for the domain hint.</span><span class="sxs-lookup"><span data-stu-id="7ee46-146">To allow this kind of behavior, enter a value for the domain hint.</span></span>

<span data-ttu-id="7ee46-147">To jump to the custom identity provider, append the parameter `domain_hint=<domain hint value>` to the end of your request when calling Azure AD B2C for sign in.</span><span class="sxs-lookup"><span data-stu-id="7ee46-147">To jump to the custom identity provider, append the parameter `domain_hint=<domain hint value>` to the end of your request when calling Azure AD B2C for sign in.</span></span>


### <a name="mapping-the-claims-from-the-openid-connect-identity-provider"></a><span data-ttu-id="7ee46-148">Mapping the claims from the OpenID Connect identity provider</span><span class="sxs-lookup"><span data-stu-id="7ee46-148">Mapping the claims from the OpenID Connect identity provider</span></span>

<span data-ttu-id="7ee46-149">After the custom identity provider sends an ID token back to Azure AD B2C, Azure AD B2C needs to be able to map the claims from the received token to the claims that Azure AD B2C recognizes and uses.</span><span class="sxs-lookup"><span data-stu-id="7ee46-149">After the custom identity provider sends an ID token back to Azure AD B2C, Azure AD B2C needs to be able to map the claims from the received token to the claims that Azure AD B2C recognizes and uses.</span></span> 

<span data-ttu-id="7ee46-150">For each of the mappings below, refer to the documentation of the custom identity provider to understand the claims that are returned back in the identity provider's tokens.</span><span class="sxs-lookup"><span data-stu-id="7ee46-150">For each of the mappings below, refer to the documentation of the custom identity provider to understand the claims that are returned back in the identity provider's tokens.</span></span>

* <span data-ttu-id="7ee46-151">`User ID`: Enter the claim that provides the unique identifier for the signed in user.</span><span class="sxs-lookup"><span data-stu-id="7ee46-151">`User ID`: Enter the claim that provides the unique identifier for the signed in user.</span></span>
* <span data-ttu-id="7ee46-152">`Display Name`: Enter the claim that provides the display name or full name for the user.</span><span class="sxs-lookup"><span data-stu-id="7ee46-152">`Display Name`: Enter the claim that provides the display name or full name for the user.</span></span>
* <span data-ttu-id="7ee46-153">`Given Name`: Enter the claim that provides the first name of the user.</span><span class="sxs-lookup"><span data-stu-id="7ee46-153">`Given Name`: Enter the claim that provides the first name of the user.</span></span>
* <span data-ttu-id="7ee46-154">`Surname`: Enter the claim that provides the last name of the user.</span><span class="sxs-lookup"><span data-stu-id="7ee46-154">`Surname`: Enter the claim that provides the last name of the user.</span></span>
* <span data-ttu-id="7ee46-155">`Email`: Enter the claim that provides the email address of the user.</span><span class="sxs-lookup"><span data-stu-id="7ee46-155">`Email`: Enter the claim that provides the email address of the user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ee46-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="7ee46-156">Next steps</span></span>

<span data-ttu-id="7ee46-157">Add the custom OpenID Connect identity provider to your [built-in policy](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="7ee46-157">Add the custom OpenID Connect identity provider to your [built-in policy](active-directory-b2c-reference-policies.md).</span></span>
