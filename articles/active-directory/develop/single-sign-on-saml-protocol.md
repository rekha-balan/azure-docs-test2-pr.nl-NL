---
title: Azure Single Sign On SAML Protocol | Microsoft Docs
description: This article describes the Single Sign On SAML protocol in Azure Active Directory
services: active-directory
documentationcenter: .net
author: CelesteDG
manager: mtillman
editor: ''
ms.assetid: ad8437f5-b887-41ff-bd77-779ddafc33fb
ms.service: active-directory
ms.component: develop
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: celested
ms.custom: aaddev
ms.reviewer: hirsin
ms.openlocfilehash: edb8ae501548775932a259621c19acece474018d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870712"
---
# <a name="single-sign-on-saml-protocol"></a><span data-ttu-id="8aa6e-103">Single Sign-On SAML protocol</span><span class="sxs-lookup"><span data-stu-id="8aa6e-103">Single Sign-On SAML protocol</span></span>

<span data-ttu-id="8aa6e-104">This article covers the SAML 2.0 authentication requests and responses that Azure Active Directory (Azure AD) supports for Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-104">This article covers the SAML 2.0 authentication requests and responses that Azure Active Directory (Azure AD) supports for Single Sign-On.</span></span>

<span data-ttu-id="8aa6e-105">The protocol diagram below describes the single sign-on sequence.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-105">The protocol diagram below describes the single sign-on sequence.</span></span> <span data-ttu-id="8aa6e-106">The cloud service (the service provider) uses an HTTP Redirect binding to pass an `AuthnRequest` (authentication request) element to Azure AD (the identity provider).</span><span class="sxs-lookup"><span data-stu-id="8aa6e-106">The cloud service (the service provider) uses an HTTP Redirect binding to pass an `AuthnRequest` (authentication request) element to Azure AD (the identity provider).</span></span> <span data-ttu-id="8aa6e-107">Azure AD then uses an HTTP post binding to post a `Response` element to the cloud service.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-107">Azure AD then uses an HTTP post binding to post a `Response` element to the cloud service.</span></span>

![Single Sign On Workflow](./media/single-sign-on-saml-protocol/active-directory-saml-single-sign-on-workflow.png)

## <a name="authnrequest"></a><span data-ttu-id="8aa6e-109">AuthnRequest</span><span class="sxs-lookup"><span data-stu-id="8aa6e-109">AuthnRequest</span></span>

<span data-ttu-id="8aa6e-110">To request a user authentication, cloud services send an `AuthnRequest` element to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-110">To request a user authentication, cloud services send an `AuthnRequest` element to Azure AD.</span></span> <span data-ttu-id="8aa6e-111">A sample SAML 2.0 `AuthnRequest` could look like the following example:</span><span class="sxs-lookup"><span data-stu-id="8aa6e-111">A sample SAML 2.0 `AuthnRequest` could look like the following example:</span></span>

```
<samlp:AuthnRequest
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="id6c1c178c166d486687be4aaf5e482730"
Version="2.0" IssueInstant="2013-03-18T03:28:54.1839884Z"
xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
<Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://www.contoso.com</Issuer>
</samlp:AuthnRequest>
```

| <span data-ttu-id="8aa6e-112">Parameter</span><span class="sxs-lookup"><span data-stu-id="8aa6e-112">Parameter</span></span> |  | <span data-ttu-id="8aa6e-113">Description</span><span class="sxs-lookup"><span data-stu-id="8aa6e-113">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8aa6e-114">ID</span><span class="sxs-lookup"><span data-stu-id="8aa6e-114">ID</span></span> | <span data-ttu-id="8aa6e-115">Required</span><span class="sxs-lookup"><span data-stu-id="8aa6e-115">Required</span></span> | <span data-ttu-id="8aa6e-116">Azure AD uses this attribute to populate the `InResponseTo` attribute of the returned response.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-116">Azure AD uses this attribute to populate the `InResponseTo` attribute of the returned response.</span></span> <span data-ttu-id="8aa6e-117">ID must not begin with a number, so a common strategy is to prepend a string like "id" to the string representation of a GUID.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-117">ID must not begin with a number, so a common strategy is to prepend a string like "id" to the string representation of a GUID.</span></span> <span data-ttu-id="8aa6e-118">For example, `id6c1c178c166d486687be4aaf5e482730` is a valid ID.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-118">For example, `id6c1c178c166d486687be4aaf5e482730` is a valid ID.</span></span> |
| <span data-ttu-id="8aa6e-119">Version</span><span class="sxs-lookup"><span data-stu-id="8aa6e-119">Version</span></span> | <span data-ttu-id="8aa6e-120">Required</span><span class="sxs-lookup"><span data-stu-id="8aa6e-120">Required</span></span> | <span data-ttu-id="8aa6e-121">This parameter should be set to **2.0**.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-121">This parameter should be set to **2.0**.</span></span> |
| <span data-ttu-id="8aa6e-122">IssueInstant</span><span class="sxs-lookup"><span data-stu-id="8aa6e-122">IssueInstant</span></span> | <span data-ttu-id="8aa6e-123">Required</span><span class="sxs-lookup"><span data-stu-id="8aa6e-123">Required</span></span> | <span data-ttu-id="8aa6e-124">This is a DateTime string with a UTC value and [round-trip format ("o")](https://msdn.microsoft.com/library/az4se3k1.aspx).</span><span class="sxs-lookup"><span data-stu-id="8aa6e-124">This is a DateTime string with a UTC value and [round-trip format ("o")](https://msdn.microsoft.com/library/az4se3k1.aspx).</span></span> <span data-ttu-id="8aa6e-125">Azure AD expects a DateTime value of this type, but doesn't evaluate or use the value.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-125">Azure AD expects a DateTime value of this type, but doesn't evaluate or use the value.</span></span> |
| <span data-ttu-id="8aa6e-126">AssertionConsumerServiceUrl</span><span class="sxs-lookup"><span data-stu-id="8aa6e-126">AssertionConsumerServiceUrl</span></span> | <span data-ttu-id="8aa6e-127">Optional</span><span class="sxs-lookup"><span data-stu-id="8aa6e-127">Optional</span></span> | <span data-ttu-id="8aa6e-128">If provided, this parameter must match the `RedirectUri` of the cloud service in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-128">If provided, this parameter must match the `RedirectUri` of the cloud service in Azure AD.</span></span> |
| <span data-ttu-id="8aa6e-129">ForceAuthn</span><span class="sxs-lookup"><span data-stu-id="8aa6e-129">ForceAuthn</span></span> | <span data-ttu-id="8aa6e-130">Optional</span><span class="sxs-lookup"><span data-stu-id="8aa6e-130">Optional</span></span> | <span data-ttu-id="8aa6e-131">This is a boolean value.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-131">This is a boolean value.</span></span> <span data-ttu-id="8aa6e-132">If true, it means that the user will be forced to re-authenticate, even if they have a valid session with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-132">If true, it means that the user will be forced to re-authenticate, even if they have a valid session with Azure AD.</span></span> |
| <span data-ttu-id="8aa6e-133">IsPassive</span><span class="sxs-lookup"><span data-stu-id="8aa6e-133">IsPassive</span></span> | <span data-ttu-id="8aa6e-134">Optional</span><span class="sxs-lookup"><span data-stu-id="8aa6e-134">Optional</span></span> | <span data-ttu-id="8aa6e-135">This is a boolean value that specifies whether Azure AD should authenticate the user silently, without user interaction, using the session cookie if one exists.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-135">This is a boolean value that specifies whether Azure AD should authenticate the user silently, without user interaction, using the session cookie if one exists.</span></span> <span data-ttu-id="8aa6e-136">If this is true, Azure AD will attempt to authenticate the user using  the session cookie.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-136">If this is true, Azure AD will attempt to authenticate the user using  the session cookie.</span></span> |

<span data-ttu-id="8aa6e-137">All other `AuthnRequest` attributes, such as Consent, Destination, AssertionConsumerServiceIndex, AttributeConsumerServiceIndex, and ProviderName are **ignored**.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-137">All other `AuthnRequest` attributes, such as Consent, Destination, AssertionConsumerServiceIndex, AttributeConsumerServiceIndex, and ProviderName are **ignored**.</span></span>

<span data-ttu-id="8aa6e-138">Azure AD also ignores the `Conditions` element in `AuthnRequest`.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-138">Azure AD also ignores the `Conditions` element in `AuthnRequest`.</span></span>

### <a name="issuer"></a><span data-ttu-id="8aa6e-139">Issuer</span><span class="sxs-lookup"><span data-stu-id="8aa6e-139">Issuer</span></span>

<span data-ttu-id="8aa6e-140">The `Issuer` element in an `AuthnRequest` must exactly match one of the **ServicePrincipalNames** in the cloud service in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-140">The `Issuer` element in an `AuthnRequest` must exactly match one of the **ServicePrincipalNames** in the cloud service in Azure AD.</span></span> <span data-ttu-id="8aa6e-141">Typically, this is set to the **App ID URI** that is specified during application registration.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-141">Typically, this is set to the **App ID URI** that is specified during application registration.</span></span>

<span data-ttu-id="8aa6e-142">A SAML excerpt containing the `Issuer` element looks like the following sample:</span><span class="sxs-lookup"><span data-stu-id="8aa6e-142">A SAML excerpt containing the `Issuer` element looks like the following sample:</span></span>

```
<Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://www.contoso.com</Issuer>
```

### <a name="nameidpolicy"></a><span data-ttu-id="8aa6e-143">NameIDPolicy</span><span class="sxs-lookup"><span data-stu-id="8aa6e-143">NameIDPolicy</span></span>

<span data-ttu-id="8aa6e-144">This element requests a particular name ID format in the response and is optional in `AuthnRequest` elements sent to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-144">This element requests a particular name ID format in the response and is optional in `AuthnRequest` elements sent to Azure AD.</span></span>

<span data-ttu-id="8aa6e-145">A `NameIdPolicy` element looks like the following sample:</span><span class="sxs-lookup"><span data-stu-id="8aa6e-145">A `NameIdPolicy` element looks like the following sample:</span></span>

```
<NameIDPolicy Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent"/>
```

<span data-ttu-id="8aa6e-146">If `NameIDPolicy` is provided, you can include its optional `Format` attribute.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-146">If `NameIDPolicy` is provided, you can include its optional `Format` attribute.</span></span> <span data-ttu-id="8aa6e-147">The `Format` attribute can have only one of the following values; any other value results in an error.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-147">The `Format` attribute can have only one of the following values; any other value results in an error.</span></span>

* <span data-ttu-id="8aa6e-148">`urn:oasis:names:tc:SAML:2.0:nameid-format:persistent`: Azure Active Directory issues the NameID claim as a pairwise identifier.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-148">`urn:oasis:names:tc:SAML:2.0:nameid-format:persistent`: Azure Active Directory issues the NameID claim as a pairwise identifier.</span></span>
* <span data-ttu-id="8aa6e-149">`urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress`: Azure Active Directory issues the NameID claim in e-mail address format.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-149">`urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress`: Azure Active Directory issues the NameID claim in e-mail address format.</span></span>
* <span data-ttu-id="8aa6e-150">`urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified`: This value permits Azure Active Directory to select the claim format.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-150">`urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified`: This value permits Azure Active Directory to select the claim format.</span></span> <span data-ttu-id="8aa6e-151">Azure Active Directory issues the NameID as a pairwise identifier.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-151">Azure Active Directory issues the NameID as a pairwise identifier.</span></span>
* <span data-ttu-id="8aa6e-152">`urn:oasis:names:tc:SAML:2.0:nameid-format:transient`: Azure Active Directory issues the NameID claim as a randomly generated value that is unique to the current SSO operation.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-152">`urn:oasis:names:tc:SAML:2.0:nameid-format:transient`: Azure Active Directory issues the NameID claim as a randomly generated value that is unique to the current SSO operation.</span></span> <span data-ttu-id="8aa6e-153">This means that the value is temporary and cannot be used to identify the authenticating user.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-153">This means that the value is temporary and cannot be used to identify the authenticating user.</span></span>

<span data-ttu-id="8aa6e-154">Azure AD ignores the `AllowCreate` attribute.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-154">Azure AD ignores the `AllowCreate` attribute.</span></span>

### <a name="requestauthncontext"></a><span data-ttu-id="8aa6e-155">RequestAuthnContext</span><span class="sxs-lookup"><span data-stu-id="8aa6e-155">RequestAuthnContext</span></span>
<span data-ttu-id="8aa6e-156">The `RequestedAuthnContext` element specifies the desired authentication methods.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-156">The `RequestedAuthnContext` element specifies the desired authentication methods.</span></span> <span data-ttu-id="8aa6e-157">It is optional in `AuthnRequest` elements sent to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-157">It is optional in `AuthnRequest` elements sent to Azure AD.</span></span> <span data-ttu-id="8aa6e-158">Azure AD supports only one `AuthnContextClassRef` value: `urn:oasis:names:tc:SAML:2.0:ac:classes:Password`.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-158">Azure AD supports only one `AuthnContextClassRef` value: `urn:oasis:names:tc:SAML:2.0:ac:classes:Password`.</span></span>

### <a name="scoping"></a><span data-ttu-id="8aa6e-159">Scoping</span><span class="sxs-lookup"><span data-stu-id="8aa6e-159">Scoping</span></span>
<span data-ttu-id="8aa6e-160">The `Scoping` element, which includes a list of identity providers, is optional in `AuthnRequest` elements sent to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-160">The `Scoping` element, which includes a list of identity providers, is optional in `AuthnRequest` elements sent to Azure AD.</span></span>

<span data-ttu-id="8aa6e-161">If provided, don't include the `ProxyCount` attribute, `IDPListOption` or `RequesterID` element, as they aren't supported.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-161">If provided, don't include the `ProxyCount` attribute, `IDPListOption` or `RequesterID` element, as they aren't supported.</span></span>

### <a name="signature"></a><span data-ttu-id="8aa6e-162">Signature</span><span class="sxs-lookup"><span data-stu-id="8aa6e-162">Signature</span></span>
<span data-ttu-id="8aa6e-163">Don't include a `Signature` element in `AuthnRequest` elements, as Azure AD does not support signed authentication requests.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-163">Don't include a `Signature` element in `AuthnRequest` elements, as Azure AD does not support signed authentication requests.</span></span>

### <a name="subject"></a><span data-ttu-id="8aa6e-164">Subject</span><span class="sxs-lookup"><span data-stu-id="8aa6e-164">Subject</span></span>
<span data-ttu-id="8aa6e-165">Azure AD ignores the `Subject` element of `AuthnRequest` elements.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-165">Azure AD ignores the `Subject` element of `AuthnRequest` elements.</span></span>

## <a name="response"></a><span data-ttu-id="8aa6e-166">Response</span><span class="sxs-lookup"><span data-stu-id="8aa6e-166">Response</span></span>
<span data-ttu-id="8aa6e-167">When a requested sign-on completes successfully, Azure AD posts a response to the cloud service.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-167">When a requested sign-on completes successfully, Azure AD posts a response to the cloud service.</span></span> <span data-ttu-id="8aa6e-168">A response to a successful sign-on attempt looks like the following sample:</span><span class="sxs-lookup"><span data-stu-id="8aa6e-168">A response to a successful sign-on attempt looks like the following sample:</span></span>

```
<samlp:Response ID="_a4958bfd-e107-4e67-b06d-0d85ade2e76a" Version="2.0" IssueInstant="2013-03-18T07:38:15.144Z" Destination="https://contoso.com/identity/inboundsso.aspx" InResponseTo="id758d0ef385634593a77bdf7e632984b6" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion"> https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
  <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
    ...
  </ds:Signature>
  <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success" />
  </samlp:Status>
  <Assertion ID="_bf9c623d-cc20-407a-9a59-c2d0aee84d12" IssueInstant="2013-03-18T07:38:15.144Z" Version="2.0" xmlns="urn:oasis:names:tc:SAML:2.0:assertion">
    <Issuer>https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
    <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      ...
    </ds:Signature>
    <Subject>
      <NameID>Uz2Pqz1X7pxe4XLWxV9KJQ+n59d573SepSAkuYKSde8=</NameID>
      <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
        <SubjectConfirmationData InResponseTo="id758d0ef385634593a77bdf7e632984b6" NotOnOrAfter="2013-03-18T07:43:15.144Z" Recipient="https://contoso.com/identity/inboundsso.aspx" />
      </SubjectConfirmation>
    </Subject>
    <Conditions NotBefore="2013-03-18T07:38:15.128Z" NotOnOrAfter="2013-03-18T08:48:15.128Z">
      <AudienceRestriction>
        <Audience>https://www.contoso.com</Audience>
      </AudienceRestriction>
    </Conditions>
    <AttributeStatement>
      <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name">
        <AttributeValue>testuser@contoso.com</AttributeValue>
      </Attribute>
      <Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">
        <AttributeValue>3F2504E0-4F89-11D3-9A0C-0305E82C3301</AttributeValue>
      </Attribute>
      ...
    </AttributeStatement>
    <AuthnStatement AuthnInstant="2013-03-18T07:33:56.000Z" SessionIndex="_bf9c623d-cc20-407a-9a59-c2d0aee84d12">
      <AuthnContext>
        <AuthnContextClassRef> urn:oasis:names:tc:SAML:2.0:ac:classes:Password</AuthnContextClassRef>
      </AuthnContext>
    </AuthnStatement>
  </Assertion>
</samlp:Response>
```

### <a name="response"></a><span data-ttu-id="8aa6e-169">Response</span><span class="sxs-lookup"><span data-stu-id="8aa6e-169">Response</span></span>

<span data-ttu-id="8aa6e-170">The `Response` element includes the result of the authorization request.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-170">The `Response` element includes the result of the authorization request.</span></span> <span data-ttu-id="8aa6e-171">Azure AD sets the `ID`, `Version` and `IssueInstant` values in the `Response` element.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-171">Azure AD sets the `ID`, `Version` and `IssueInstant` values in the `Response` element.</span></span> <span data-ttu-id="8aa6e-172">It also sets the following attributes:</span><span class="sxs-lookup"><span data-stu-id="8aa6e-172">It also sets the following attributes:</span></span>

* <span data-ttu-id="8aa6e-173">`Destination`: When sign-on completes successfully, this is set to the `RedirectUri` of the service provider (cloud service).</span><span class="sxs-lookup"><span data-stu-id="8aa6e-173">`Destination`: When sign-on completes successfully, this is set to the `RedirectUri` of the service provider (cloud service).</span></span>
* <span data-ttu-id="8aa6e-174">`InResponseTo`: This is set to the `ID` attribute of the `AuthnRequest` element that initiated the response.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-174">`InResponseTo`: This is set to the `ID` attribute of the `AuthnRequest` element that initiated the response.</span></span>

### <a name="issuer"></a><span data-ttu-id="8aa6e-175">Issuer</span><span class="sxs-lookup"><span data-stu-id="8aa6e-175">Issuer</span></span>

<span data-ttu-id="8aa6e-176">Azure AD sets the `Issuer` element to `https://login.microsoftonline.com/<TenantIDGUID>/` where <TenantIDGUID> is the tenant ID of the Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-176">Azure AD sets the `Issuer` element to `https://login.microsoftonline.com/<TenantIDGUID>/` where <TenantIDGUID> is the tenant ID of the Azure AD tenant.</span></span>

<span data-ttu-id="8aa6e-177">For example, a response with Issuer element could look like the following sample:</span><span class="sxs-lookup"><span data-stu-id="8aa6e-177">For example, a response with Issuer element could look like the following sample:</span></span>

```
<Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion"> https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
```

### <a name="status"></a><span data-ttu-id="8aa6e-178">Status</span><span class="sxs-lookup"><span data-stu-id="8aa6e-178">Status</span></span>

<span data-ttu-id="8aa6e-179">The `Status` element conveys the success or failure of sign-on.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-179">The `Status` element conveys the success or failure of sign-on.</span></span> <span data-ttu-id="8aa6e-180">It includes the `StatusCode` element, which contains a code or a set of nested codes that represents the status of the request.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-180">It includes the `StatusCode` element, which contains a code or a set of nested codes that represents the status of the request.</span></span> <span data-ttu-id="8aa6e-181">It also includes the `StatusMessage` element, which contains custom error messages that are generated during the sign-on process.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-181">It also includes the `StatusMessage` element, which contains custom error messages that are generated during the sign-on process.</span></span>

<!-- TODO: Add a authentication protocol error reference -->

<span data-ttu-id="8aa6e-182">The following sample is a SAML response to an unsuccessful sign-on attempt.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-182">The following sample is a SAML response to an unsuccessful sign-on attempt.</span></span>

```
<samlp:Response ID="_f0961a83-d071-4be5-a18c-9ae7b22987a4" Version="2.0" IssueInstant="2013-03-18T08:49:24.405Z" InResponseTo="iddce91f96e56747b5ace6d2e2aa9d4f8c" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://sts.windows.net/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
  <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Requester">
      <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:RequestUnsupported" />
    </samlp:StatusCode>
    <samlp:StatusMessage>AADSTS75006: An error occurred while processing a SAML2 Authentication request. AADSTS90011: The SAML authentication request property 'NameIdentifierPolicy/SPNameQualifier' is not supported.
Trace ID: 66febed4-e737-49ff-ac23-464ba090d57c
Timestamp: 2013-03-18 08:49:24Z</samlp:StatusMessage>
  </samlp:Status>
```

### <a name="assertion"></a><span data-ttu-id="8aa6e-183">Assertion</span><span class="sxs-lookup"><span data-stu-id="8aa6e-183">Assertion</span></span>

<span data-ttu-id="8aa6e-184">In addition to the `ID`, `IssueInstant` and `Version`, Azure AD sets the following elements in the `Assertion` element of the response.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-184">In addition to the `ID`, `IssueInstant` and `Version`, Azure AD sets the following elements in the `Assertion` element of the response.</span></span>

#### <a name="issuer"></a><span data-ttu-id="8aa6e-185">Issuer</span><span class="sxs-lookup"><span data-stu-id="8aa6e-185">Issuer</span></span>

<span data-ttu-id="8aa6e-186">This is set to `https://sts.windows.net/<TenantIDGUID>/`where <TenantIDGUID> is the Tenant ID of the Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-186">This is set to `https://sts.windows.net/<TenantIDGUID>/`where <TenantIDGUID> is the Tenant ID of the Azure AD tenant.</span></span>

```
<Issuer>https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
```

#### <a name="signature"></a><span data-ttu-id="8aa6e-187">Signature</span><span class="sxs-lookup"><span data-stu-id="8aa6e-187">Signature</span></span>

<span data-ttu-id="8aa6e-188">Azure AD signs the assertion in response to a successful sign-on.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-188">Azure AD signs the assertion in response to a successful sign-on.</span></span> <span data-ttu-id="8aa6e-189">The `Signature` element contains a digital signature that the cloud service can use to authenticate the source to verify the integrity of the assertion.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-189">The `Signature` element contains a digital signature that the cloud service can use to authenticate the source to verify the integrity of the assertion.</span></span>

<span data-ttu-id="8aa6e-190">To generate this digital signature, Azure AD uses the signing key in the `IDPSSODescriptor` element of its metadata document.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-190">To generate this digital signature, Azure AD uses the signing key in the `IDPSSODescriptor` element of its metadata document.</span></span>

```
<ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      digital_signature_here
    </ds:Signature>
```

#### <a name="subject"></a><span data-ttu-id="8aa6e-191">Subject</span><span class="sxs-lookup"><span data-stu-id="8aa6e-191">Subject</span></span>

<span data-ttu-id="8aa6e-192">This specifies the principal that is the subject of the statements in the assertion.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-192">This specifies the principal that is the subject of the statements in the assertion.</span></span> <span data-ttu-id="8aa6e-193">It contains a `NameID` element, which represents the authenticated user.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-193">It contains a `NameID` element, which represents the authenticated user.</span></span> <span data-ttu-id="8aa6e-194">The `NameID` value is a targeted identifier that is directed only to the service provider that is the audience for the token.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-194">The `NameID` value is a targeted identifier that is directed only to the service provider that is the audience for the token.</span></span> <span data-ttu-id="8aa6e-195">It is persistent - it can be revoked, but is never reassigned.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-195">It is persistent - it can be revoked, but is never reassigned.</span></span> <span data-ttu-id="8aa6e-196">It is also opaque, in that it does not reveal anything about the user and cannot be used as an identifier for attribute queries.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-196">It is also opaque, in that it does not reveal anything about the user and cannot be used as an identifier for attribute queries.</span></span>

<span data-ttu-id="8aa6e-197">The `Method` attribute of the `SubjectConfirmation` element is always set to `urn:oasis:names:tc:SAML:2.0:cm:bearer`.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-197">The `Method` attribute of the `SubjectConfirmation` element is always set to `urn:oasis:names:tc:SAML:2.0:cm:bearer`.</span></span>

```
<Subject>
      <NameID>Uz2Pqz1X7pxe4XLWxV9KJQ+n59d573SepSAkuYKSde8=</NameID>
      <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
        <SubjectConfirmationData InResponseTo="id758d0ef385634593a77bdf7e632984b6" NotOnOrAfter="2013-03-18T07:43:15.144Z" Recipient="https://contoso.com/identity/inboundsso.aspx" />
      </SubjectConfirmation>
</Subject>
```

#### <a name="conditions"></a><span data-ttu-id="8aa6e-198">Conditions</span><span class="sxs-lookup"><span data-stu-id="8aa6e-198">Conditions</span></span>

<span data-ttu-id="8aa6e-199">This element specifies conditions that define the acceptable use of SAML assertions.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-199">This element specifies conditions that define the acceptable use of SAML assertions.</span></span>

```
<Conditions NotBefore="2013-03-18T07:38:15.128Z" NotOnOrAfter="2013-03-18T08:48:15.128Z">
      <AudienceRestriction>
        <Audience>https://www.contoso.com</Audience>
      </AudienceRestriction>
</Conditions>
```

<span data-ttu-id="8aa6e-200">The `NotBefore` and `NotOnOrAfter` attributes specify the interval during which the assertion is valid.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-200">The `NotBefore` and `NotOnOrAfter` attributes specify the interval during which the assertion is valid.</span></span>

* <span data-ttu-id="8aa6e-201">The value of the `NotBefore` attribute is equal to or slightly (less than a second) later than the value of `IssueInstant` attribute of the `Assertion` element.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-201">The value of the `NotBefore` attribute is equal to or slightly (less than a second) later than the value of `IssueInstant` attribute of the `Assertion` element.</span></span> <span data-ttu-id="8aa6e-202">Azure AD does not account for any time difference between itself and the cloud service (service provider), and does not add any buffer to this time.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-202">Azure AD does not account for any time difference between itself and the cloud service (service provider), and does not add any buffer to this time.</span></span>
* <span data-ttu-id="8aa6e-203">The value of the `NotOnOrAfter` attribute is 70 minutes later than the value of the `NotBefore` attribute.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-203">The value of the `NotOnOrAfter` attribute is 70 minutes later than the value of the `NotBefore` attribute.</span></span>

#### <a name="audience"></a><span data-ttu-id="8aa6e-204">Audience</span><span class="sxs-lookup"><span data-stu-id="8aa6e-204">Audience</span></span>

<span data-ttu-id="8aa6e-205">This contains a URI that identifies an intended audience.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-205">This contains a URI that identifies an intended audience.</span></span> <span data-ttu-id="8aa6e-206">Azure AD sets the value of this element to the value of `Issuer` element of the `AuthnRequest` that initiated the sign-on.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-206">Azure AD sets the value of this element to the value of `Issuer` element of the `AuthnRequest` that initiated the sign-on.</span></span> <span data-ttu-id="8aa6e-207">To evaluate the `Audience` value, use the value of the `App ID URI` that was specified during application registration.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-207">To evaluate the `Audience` value, use the value of the `App ID URI` that was specified during application registration.</span></span>

```
<AudienceRestriction>
        <Audience>https://www.contoso.com</Audience>
</AudienceRestriction>
```

<span data-ttu-id="8aa6e-208">Like the `Issuer` value, the `Audience` value must exactly match one of the service principal names that represents the cloud service in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-208">Like the `Issuer` value, the `Audience` value must exactly match one of the service principal names that represents the cloud service in Azure AD.</span></span> <span data-ttu-id="8aa6e-209">However, if the value of the `Issuer` element is not a URI value, the `Audience` value in the response is the `Issuer` value prefixed with `spn:`.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-209">However, if the value of the `Issuer` element is not a URI value, the `Audience` value in the response is the `Issuer` value prefixed with `spn:`.</span></span>

#### <a name="attributestatement"></a><span data-ttu-id="8aa6e-210">AttributeStatement</span><span class="sxs-lookup"><span data-stu-id="8aa6e-210">AttributeStatement</span></span>

<span data-ttu-id="8aa6e-211">This contains claims about the subject or user.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-211">This contains claims about the subject or user.</span></span> <span data-ttu-id="8aa6e-212">The following excerpt contains a sample `AttributeStatement` element.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-212">The following excerpt contains a sample `AttributeStatement` element.</span></span> <span data-ttu-id="8aa6e-213">The ellipsis indicates that the element can include multiple attributes and attribute values.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-213">The ellipsis indicates that the element can include multiple attributes and attribute values.</span></span>

```
<AttributeStatement>
      <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name">
        <AttributeValue>testuser@contoso.com</AttributeValue>
      </Attribute>
      <Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">
        <AttributeValue>3F2504E0-4F89-11D3-9A0C-0305E82C3301</AttributeValue>
      </Attribute>
      ...
</AttributeStatement>
```        

* <span data-ttu-id="8aa6e-214">**Name Claim** - The value of the `Name` attribute (`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`) is the user principal name of the authenticated user, such as `testuser@managedtenant.com`.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-214">**Name Claim** - The value of the `Name` attribute (`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`) is the user principal name of the authenticated user, such as `testuser@managedtenant.com`.</span></span>
* <span data-ttu-id="8aa6e-215">**ObjectIdentifier Claim** - The value of the `ObjectIdentifier` attribute (`http://schemas.microsoft.com/identity/claims/objectidentifier`) is the `ObjectId` of the directory object that represents the authenticated user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-215">**ObjectIdentifier Claim** - The value of the `ObjectIdentifier` attribute (`http://schemas.microsoft.com/identity/claims/objectidentifier`) is the `ObjectId` of the directory object that represents the authenticated user in Azure AD.</span></span> <span data-ttu-id="8aa6e-216">`ObjectId` is an immutable, globally unique, and reuse safe identifier of the authenticated user.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-216">`ObjectId` is an immutable, globally unique, and reuse safe identifier of the authenticated user.</span></span>

#### <a name="authnstatement"></a><span data-ttu-id="8aa6e-217">AuthnStatement</span><span class="sxs-lookup"><span data-stu-id="8aa6e-217">AuthnStatement</span></span>

<span data-ttu-id="8aa6e-218">This element asserts that the assertion subject was authenticated by a particular means at a particular time.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-218">This element asserts that the assertion subject was authenticated by a particular means at a particular time.</span></span>

* <span data-ttu-id="8aa6e-219">The `AuthnInstant` attribute specifies the time at which the user authenticated with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-219">The `AuthnInstant` attribute specifies the time at which the user authenticated with Azure AD.</span></span>
* <span data-ttu-id="8aa6e-220">The `AuthnContext` element specifies the authentication context used to authenticate the user.</span><span class="sxs-lookup"><span data-stu-id="8aa6e-220">The `AuthnContext` element specifies the authentication context used to authenticate the user.</span></span>

```
<AuthnStatement AuthnInstant="2013-03-18T07:33:56.000Z" SessionIndex="_bf9c623d-cc20-407a-9a59-c2d0aee84d12">
      <AuthnContext>
        <AuthnContextClassRef> urn:oasis:names:tc:SAML:2.0:ac:classes:Password</AuthnContextClassRef>
      </AuthnContext>
</AuthnStatement>
```
