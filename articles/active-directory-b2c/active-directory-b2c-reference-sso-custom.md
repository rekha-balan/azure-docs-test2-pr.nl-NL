---
title: Single sign-on session management using custom policies in Azure Active Directory B2C | Microsoft Docs
description: Learn how to manage SSO sessions using custom policies in Azure AD B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: reference
ms.date: 09/10/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: bd41ce5ba0cc738c1fd0d61d080e63753706f975
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969411"
---
# <a name="single-sign-on-session-management-in-azure-active-directory-b2c"></a><span data-ttu-id="f601c-103">Single sign-on session management in Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="f601c-103">Single sign-on session management in Azure Active Directory B2C</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="f601c-104">Single sign-on (SSO) session management in Azure Active Directory (Azure AD) B2C enables an administrator to control interaction with a user after the user has already authenticated.</span><span class="sxs-lookup"><span data-stu-id="f601c-104">Single sign-on (SSO) session management in Azure Active Directory (Azure AD) B2C enables an administrator to control interaction with a user after the user has already authenticated.</span></span> <span data-ttu-id="f601c-105">For example, the administrator can control whether the selection of identity providers is displayed, or whether local account details need to be entered again.</span><span class="sxs-lookup"><span data-stu-id="f601c-105">For example, the administrator can control whether the selection of identity providers is displayed, or whether local account details need to be entered again.</span></span> <span data-ttu-id="f601c-106">This article describes how to configure the SSO settings for Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="f601c-106">This article describes how to configure the SSO settings for Azure AD B2C.</span></span>

<span data-ttu-id="f601c-107">SSO session management has two parts.</span><span class="sxs-lookup"><span data-stu-id="f601c-107">SSO session management has two parts.</span></span> <span data-ttu-id="f601c-108">The first deals with the user's interactions directly with Azure AD B2C and the other deals with the user's interactions with external parties such as Facebook.</span><span class="sxs-lookup"><span data-stu-id="f601c-108">The first deals with the user's interactions directly with Azure AD B2C and the other deals with the user's interactions with external parties such as Facebook.</span></span> <span data-ttu-id="f601c-109">Azure AD B2C does not override or bypass SSO sessions that might be held by external parties.</span><span class="sxs-lookup"><span data-stu-id="f601c-109">Azure AD B2C does not override or bypass SSO sessions that might be held by external parties.</span></span> <span data-ttu-id="f601c-110">Rather the route through Azure AD B2C to get to the external party is “remembered”, avoiding the need to reprompt the user to select their social or enterprise identity provider.</span><span class="sxs-lookup"><span data-stu-id="f601c-110">Rather the route through Azure AD B2C to get to the external party is “remembered”, avoiding the need to reprompt the user to select their social or enterprise identity provider.</span></span> <span data-ttu-id="f601c-111">The ultimate SSO decision remains with the external party.</span><span class="sxs-lookup"><span data-stu-id="f601c-111">The ultimate SSO decision remains with the external party.</span></span>

<span data-ttu-id="f601c-112">SSO session management uses the same semantics as any other technical profile in custom policies.</span><span class="sxs-lookup"><span data-stu-id="f601c-112">SSO session management uses the same semantics as any other technical profile in custom policies.</span></span> <span data-ttu-id="f601c-113">When an orchestration step is executed, the technical profile associated with the step is queried for a `UseTechnicalProfileForSessionManagement` reference.</span><span class="sxs-lookup"><span data-stu-id="f601c-113">When an orchestration step is executed, the technical profile associated with the step is queried for a `UseTechnicalProfileForSessionManagement` reference.</span></span> <span data-ttu-id="f601c-114">If one exists, the referenced SSO session provider is then checked to see if the user is a session participant.</span><span class="sxs-lookup"><span data-stu-id="f601c-114">If one exists, the referenced SSO session provider is then checked to see if the user is a session participant.</span></span> <span data-ttu-id="f601c-115">If so, the SSO session provider is used to repopulate the session.</span><span class="sxs-lookup"><span data-stu-id="f601c-115">If so, the SSO session provider is used to repopulate the session.</span></span> <span data-ttu-id="f601c-116">Similarly, when the execution of an orchestration step is complete, the provider is used to store information in the session if an SSO session provider has been specified.</span><span class="sxs-lookup"><span data-stu-id="f601c-116">Similarly, when the execution of an orchestration step is complete, the provider is used to store information in the session if an SSO session provider has been specified.</span></span>

<span data-ttu-id="f601c-117">Azure AD B2C has defined a number of SSO session providers that can be used:</span><span class="sxs-lookup"><span data-stu-id="f601c-117">Azure AD B2C has defined a number of SSO session providers that can be used:</span></span>

* <span data-ttu-id="f601c-118">NoopSSOSessionProvider</span><span class="sxs-lookup"><span data-stu-id="f601c-118">NoopSSOSessionProvider</span></span>
* <span data-ttu-id="f601c-119">DefaultSSOSessionProvider</span><span class="sxs-lookup"><span data-stu-id="f601c-119">DefaultSSOSessionProvider</span></span>
* <span data-ttu-id="f601c-120">ExternalLoginSSOSessionProvider</span><span class="sxs-lookup"><span data-stu-id="f601c-120">ExternalLoginSSOSessionProvider</span></span>
* <span data-ttu-id="f601c-121">SamlSSOSessionProvider</span><span class="sxs-lookup"><span data-stu-id="f601c-121">SamlSSOSessionProvider</span></span>

<span data-ttu-id="f601c-122">SSO management classes are specified using the `<UseTechnicalProfileForSessionManagement ReferenceId=“{ID}" />` element of a technical profile.</span><span class="sxs-lookup"><span data-stu-id="f601c-122">SSO management classes are specified using the `<UseTechnicalProfileForSessionManagement ReferenceId=“{ID}" />` element of a technical profile.</span></span>

## <a name="noopssosessionprovider"></a><span data-ttu-id="f601c-123">NoopSSOSessionProvider</span><span class="sxs-lookup"><span data-stu-id="f601c-123">NoopSSOSessionProvider</span></span>

<span data-ttu-id="f601c-124">As the name dictates, this provider does nothing.</span><span class="sxs-lookup"><span data-stu-id="f601c-124">As the name dictates, this provider does nothing.</span></span> <span data-ttu-id="f601c-125">This provider can be used for suppressing SSO behavior for a specific technical profile.</span><span class="sxs-lookup"><span data-stu-id="f601c-125">This provider can be used for suppressing SSO behavior for a specific technical profile.</span></span>

## <a name="defaultssosessionprovider"></a><span data-ttu-id="f601c-126">DefaultSSOSessionProvider</span><span class="sxs-lookup"><span data-stu-id="f601c-126">DefaultSSOSessionProvider</span></span>

<span data-ttu-id="f601c-127">This provider can be used for storing claims in a session.</span><span class="sxs-lookup"><span data-stu-id="f601c-127">This provider can be used for storing claims in a session.</span></span> <span data-ttu-id="f601c-128">This provider is typically referenced in a technical profile used for managing local accounts.</span><span class="sxs-lookup"><span data-stu-id="f601c-128">This provider is typically referenced in a technical profile used for managing local accounts.</span></span> <span data-ttu-id="f601c-129">When using the DefaultSSOSessionProvider to store claims in a session, you need to ensure that any claims that need to be returned to the application or used by pre-conditions in subsequent steps, are stored in the session or augmented by a read from the users profile in directory.</span><span class="sxs-lookup"><span data-stu-id="f601c-129">When using the DefaultSSOSessionProvider to store claims in a session, you need to ensure that any claims that need to be returned to the application or used by pre-conditions in subsequent steps, are stored in the session or augmented by a read from the users profile in directory.</span></span> <span data-ttu-id="f601c-130">This will ensure that your authentication journey’s will not fail on missing claims.</span><span class="sxs-lookup"><span data-stu-id="f601c-130">This will ensure that your authentication journey’s will not fail on missing claims.</span></span>

```XML
<TechnicalProfile Id="SM-AAD">
    <DisplayName>Session Mananagement Provider</DisplayName>
    <Protocol Name="Proprietary" Handler="Web.TPEngine.SSO.DefaultSSOSessionProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
    <PersistedClaims>
        <PersistedClaim ClaimTypeReferenceId="objectId" />
        <PersistedClaim ClaimTypeReferenceId="newUser" />
        <PersistedClaim ClaimTypeReferenceId="executed-SelfAsserted-Input" />
    </PersistedClaims>
    <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="objectIdFromSession" DefaultValue="true" />
    </OutputClaims>
</TechnicalProfile>
```

<span data-ttu-id="f601c-131">To add claims in the session, use the `<PersistedClaims>` element of the technical profile.</span><span class="sxs-lookup"><span data-stu-id="f601c-131">To add claims in the session, use the `<PersistedClaims>` element of the technical profile.</span></span> <span data-ttu-id="f601c-132">When the provider is used to repopulate the session, the persisted claims are added to the claims bag.</span><span class="sxs-lookup"><span data-stu-id="f601c-132">When the provider is used to repopulate the session, the persisted claims are added to the claims bag.</span></span> <span data-ttu-id="f601c-133">`<OutputClaims>` is used for retrieving claims from the session.</span><span class="sxs-lookup"><span data-stu-id="f601c-133">`<OutputClaims>` is used for retrieving claims from the session.</span></span>

## <a name="externalloginssosessionprovider"></a><span data-ttu-id="f601c-134">ExternalLoginSSOSessionProvider</span><span class="sxs-lookup"><span data-stu-id="f601c-134">ExternalLoginSSOSessionProvider</span></span>

<span data-ttu-id="f601c-135">This provider is used to suppress the “choose identity provider” screen.</span><span class="sxs-lookup"><span data-stu-id="f601c-135">This provider is used to suppress the “choose identity provider” screen.</span></span> <span data-ttu-id="f601c-136">It is typically referenced in a technical profile configured for an external identity provider, such as Facebook.</span><span class="sxs-lookup"><span data-stu-id="f601c-136">It is typically referenced in a technical profile configured for an external identity provider, such as Facebook.</span></span> 

```XML
<TechnicalProfile Id="SM-SocialLogin">
    <DisplayName>Session Mananagement Provider</DisplayName>
    <Protocol Name="Proprietary" Handler="Web.TPEngine.SSO.ExternalLoginSSOSessionProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
</TechnicalProfile>
```

## <a name="samlssosessionprovider"></a><span data-ttu-id="f601c-137">SamlSSOSessionProvider</span><span class="sxs-lookup"><span data-stu-id="f601c-137">SamlSSOSessionProvider</span></span>

<span data-ttu-id="f601c-138">This provider is used for managing the Azure AD B2C SAML sessions between apps as well as external SAML identity providers.</span><span class="sxs-lookup"><span data-stu-id="f601c-138">This provider is used for managing the Azure AD B2C SAML sessions between apps as well as external SAML identity providers.</span></span>

```XML
<TechnicalProfile Id="SM-Reflector-SAML">
    <DisplayName>Session Management Provider</DisplayName>
    <Protocol Name="Proprietary" Handler="Web.TPEngine.SSO.SamlSSOSessionProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
    <Metadata>
        <Item Key="IncludeSessionIndex">false</Item>
        <Item Key="RegisterServiceProviders">false</Item>
    </Metadata>
</TechnicalProfile>
```

<span data-ttu-id="f601c-139">There are two metadata items in the technical profile:</span><span class="sxs-lookup"><span data-stu-id="f601c-139">There are two metadata items in the technical profile:</span></span>

| <span data-ttu-id="f601c-140">Item</span><span class="sxs-lookup"><span data-stu-id="f601c-140">Item</span></span> | <span data-ttu-id="f601c-141">Default Value</span><span class="sxs-lookup"><span data-stu-id="f601c-141">Default Value</span></span> | <span data-ttu-id="f601c-142">Possible Values</span><span class="sxs-lookup"><span data-stu-id="f601c-142">Possible Values</span></span> | <span data-ttu-id="f601c-143">Description</span><span class="sxs-lookup"><span data-stu-id="f601c-143">Description</span></span>
| --- | --- | --- | --- |
| <span data-ttu-id="f601c-144">IncludeSessionIndex</span><span class="sxs-lookup"><span data-stu-id="f601c-144">IncludeSessionIndex</span></span> | <span data-ttu-id="f601c-145">true</span><span class="sxs-lookup"><span data-stu-id="f601c-145">true</span></span> | <span data-ttu-id="f601c-146">true/false</span><span class="sxs-lookup"><span data-stu-id="f601c-146">true/false</span></span> | <span data-ttu-id="f601c-147">Indicates to the provider that the session index should be stored.</span><span class="sxs-lookup"><span data-stu-id="f601c-147">Indicates to the provider that the session index should be stored.</span></span> |
| <span data-ttu-id="f601c-148">RegisterServiceProviders</span><span class="sxs-lookup"><span data-stu-id="f601c-148">RegisterServiceProviders</span></span> | <span data-ttu-id="f601c-149">true</span><span class="sxs-lookup"><span data-stu-id="f601c-149">true</span></span> | <span data-ttu-id="f601c-150">true/false</span><span class="sxs-lookup"><span data-stu-id="f601c-150">true/false</span></span> | <span data-ttu-id="f601c-151">Indicates that the provider should register all SAML service providers that have been issued an assertion.</span><span class="sxs-lookup"><span data-stu-id="f601c-151">Indicates that the provider should register all SAML service providers that have been issued an assertion.</span></span> |

<span data-ttu-id="f601c-152">When using the provider for storing a SAML identity provider session, the items above should both be false.</span><span class="sxs-lookup"><span data-stu-id="f601c-152">When using the provider for storing a SAML identity provider session, the items above should both be false.</span></span> <span data-ttu-id="f601c-153">When using the provider for storing the B2C SAML session, the items above should be true or omitted as the defaults are true.</span><span class="sxs-lookup"><span data-stu-id="f601c-153">When using the provider for storing the B2C SAML session, the items above should be true or omitted as the defaults are true.</span></span> <span data-ttu-id="f601c-154">SAML session logout requires the `SessionIndex` and `NameID` to complete.</span><span class="sxs-lookup"><span data-stu-id="f601c-154">SAML session logout requires the `SessionIndex` and `NameID` to complete.</span></span>

