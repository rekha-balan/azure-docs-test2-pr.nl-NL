---
title: Azure Single Sign Out SAML Protocol | Microsoft Docs
description: This article describes the Single Sign-Out SAML Protocol in Azure Active Directory
services: active-directory
documentationcenter: .net
author: CelesteDG
manager: mtillman
editor: ''
ms.assetid: 0e4aa75d-d1ad-4bde-a94c-d8a41fb0abe6
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
ms.openlocfilehash: b1c0dddec93e913e543558893979b95c8f53ad47
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857229"
---
# <a name="single-sign-out-saml-protocol"></a><span data-ttu-id="cb2a8-103">Single Sign-Out SAML Protocol</span><span class="sxs-lookup"><span data-stu-id="cb2a8-103">Single Sign-Out SAML Protocol</span></span>

<span data-ttu-id="cb2a8-104">Azure Active Directory (Azure AD) supports the SAML 2.0 web browser single sign-out profile.</span><span class="sxs-lookup"><span data-stu-id="cb2a8-104">Azure Active Directory (Azure AD) supports the SAML 2.0 web browser single sign-out profile.</span></span> <span data-ttu-id="cb2a8-105">For single sign-out to work correctly, the **LogoutURL** for the application must be explicitly registered with Azure AD during application registration.</span><span class="sxs-lookup"><span data-stu-id="cb2a8-105">For single sign-out to work correctly, the **LogoutURL** for the application must be explicitly registered with Azure AD during application registration.</span></span> <span data-ttu-id="cb2a8-106">Azure AD uses the LogoutURL to redirect users after they're signed out.</span><span class="sxs-lookup"><span data-stu-id="cb2a8-106">Azure AD uses the LogoutURL to redirect users after they're signed out.</span></span>

<span data-ttu-id="cb2a8-107">The following diagram shows the workflow of the Azure AD single sign-out process.</span><span class="sxs-lookup"><span data-stu-id="cb2a8-107">The following diagram shows the workflow of the Azure AD single sign-out process.</span></span>

![Azure AD Single Sign Out Workflow](./media/single-sign-out-saml-protocol/active-directory-saml-single-sign-out-workflow.png)

## <a name="logoutrequest"></a><span data-ttu-id="cb2a8-109">LogoutRequest</span><span class="sxs-lookup"><span data-stu-id="cb2a8-109">LogoutRequest</span></span>
<span data-ttu-id="cb2a8-110">The cloud service sends a `LogoutRequest` message to Azure AD to indicate that a session has been terminated.</span><span class="sxs-lookup"><span data-stu-id="cb2a8-110">The cloud service sends a `LogoutRequest` message to Azure AD to indicate that a session has been terminated.</span></span> <span data-ttu-id="cb2a8-111">The following excerpt shows a sample `LogoutRequest` element.</span><span class="sxs-lookup"><span data-stu-id="cb2a8-111">The following excerpt shows a sample `LogoutRequest` element.</span></span>

```
<samlp:LogoutRequest xmlns="urn:oasis:names:tc:SAML:2.0:metadata" ID="idaa6ebe6839094fe4abc4ebd5281ec780" Version="2.0" IssueInstant="2013-03-28T07:10:49.6004822Z" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://www.workaad.com</Issuer>
  <NameID xmlns="urn:oasis:names:tc:SAML:2.0:assertion"> Uz2Pqz1X7pxe4XLWxV9KJQ+n59d573SepSAkuYKSde8=</NameID>
</samlp:LogoutRequest>
```

### <a name="logoutrequest"></a><span data-ttu-id="cb2a8-112">LogoutRequest</span><span class="sxs-lookup"><span data-stu-id="cb2a8-112">LogoutRequest</span></span>
<span data-ttu-id="cb2a8-113">The `LogoutRequest` element sent to Azure AD requires the following attributes:</span><span class="sxs-lookup"><span data-stu-id="cb2a8-113">The `LogoutRequest` element sent to Azure AD requires the following attributes:</span></span>

* <span data-ttu-id="cb2a8-114">`ID` - This identifies the sign-out request.</span><span class="sxs-lookup"><span data-stu-id="cb2a8-114">`ID` - This identifies the sign-out request.</span></span> <span data-ttu-id="cb2a8-115">The value of `ID` should not begin with a number.</span><span class="sxs-lookup"><span data-stu-id="cb2a8-115">The value of `ID` should not begin with a number.</span></span> <span data-ttu-id="cb2a8-116">The typical practice is to append **id** to the string representation of a GUID.</span><span class="sxs-lookup"><span data-stu-id="cb2a8-116">The typical practice is to append **id** to the string representation of a GUID.</span></span>
* <span data-ttu-id="cb2a8-117">`Version` - Set the value of this element to **2.0**.</span><span class="sxs-lookup"><span data-stu-id="cb2a8-117">`Version` - Set the value of this element to **2.0**.</span></span> <span data-ttu-id="cb2a8-118">This value is required.</span><span class="sxs-lookup"><span data-stu-id="cb2a8-118">This value is required.</span></span>
* <span data-ttu-id="cb2a8-119">`IssueInstant` - This is a `DateTime` string with a Coordinate Universal Time (UTC) value and [round-trip format ("o")](https://msdn.microsoft.com/library/az4se3k1.aspx).</span><span class="sxs-lookup"><span data-stu-id="cb2a8-119">`IssueInstant` - This is a `DateTime` string with a Coordinate Universal Time (UTC) value and [round-trip format ("o")](https://msdn.microsoft.com/library/az4se3k1.aspx).</span></span> <span data-ttu-id="cb2a8-120">Azure AD expects a value of this type, but doesn't enforce it.</span><span class="sxs-lookup"><span data-stu-id="cb2a8-120">Azure AD expects a value of this type, but doesn't enforce it.</span></span>

### <a name="issuer"></a><span data-ttu-id="cb2a8-121">Issuer</span><span class="sxs-lookup"><span data-stu-id="cb2a8-121">Issuer</span></span>
<span data-ttu-id="cb2a8-122">The `Issuer` element in a `LogoutRequest` must exactly match one of the **ServicePrincipalNames** in the cloud service in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cb2a8-122">The `Issuer` element in a `LogoutRequest` must exactly match one of the **ServicePrincipalNames** in the cloud service in Azure AD.</span></span> <span data-ttu-id="cb2a8-123">Typically, this is set to the **App ID URI** that is specified during application registration.</span><span class="sxs-lookup"><span data-stu-id="cb2a8-123">Typically, this is set to the **App ID URI** that is specified during application registration.</span></span>

### <a name="nameid"></a><span data-ttu-id="cb2a8-124">NameID</span><span class="sxs-lookup"><span data-stu-id="cb2a8-124">NameID</span></span>
<span data-ttu-id="cb2a8-125">The value of the `NameID` element must exactly match the `NameID` of the user that is being signed out.</span><span class="sxs-lookup"><span data-stu-id="cb2a8-125">The value of the `NameID` element must exactly match the `NameID` of the user that is being signed out.</span></span>

## <a name="logoutresponse"></a><span data-ttu-id="cb2a8-126">LogoutResponse</span><span class="sxs-lookup"><span data-stu-id="cb2a8-126">LogoutResponse</span></span>
<span data-ttu-id="cb2a8-127">Azure AD sends a `LogoutResponse` in response to a `LogoutRequest` element.</span><span class="sxs-lookup"><span data-stu-id="cb2a8-127">Azure AD sends a `LogoutResponse` in response to a `LogoutRequest` element.</span></span> <span data-ttu-id="cb2a8-128">The following excerpt shows a sample `LogoutResponse`.</span><span class="sxs-lookup"><span data-stu-id="cb2a8-128">The following excerpt shows a sample `LogoutResponse`.</span></span>

```
<samlp:LogoutResponse ID="_f0961a83-d071-4be5-a18c-9ae7b22987a4" Version="2.0" IssueInstant="2013-03-18T08:49:24.405Z" InResponseTo="iddce91f96e56747b5ace6d2e2aa9d4f8c" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://sts.windows.net/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
  <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success" />
  </samlp:Status>
</samlp:LogoutResponse>
```

### <a name="logoutresponse"></a><span data-ttu-id="cb2a8-129">LogoutResponse</span><span class="sxs-lookup"><span data-stu-id="cb2a8-129">LogoutResponse</span></span>
<span data-ttu-id="cb2a8-130">Azure AD sets the `ID`, `Version` and `IssueInstant` values in the `LogoutResponse` element.</span><span class="sxs-lookup"><span data-stu-id="cb2a8-130">Azure AD sets the `ID`, `Version` and `IssueInstant` values in the `LogoutResponse` element.</span></span> <span data-ttu-id="cb2a8-131">It also sets the `InResponseTo` element to the value of the `ID` attribute of the `LogoutRequest` that elicited the response.</span><span class="sxs-lookup"><span data-stu-id="cb2a8-131">It also sets the `InResponseTo` element to the value of the `ID` attribute of the `LogoutRequest` that elicited the response.</span></span>

### <a name="issuer"></a><span data-ttu-id="cb2a8-132">Issuer</span><span class="sxs-lookup"><span data-stu-id="cb2a8-132">Issuer</span></span>
<span data-ttu-id="cb2a8-133">Azure AD sets this value to `https://login.microsoftonline.com/<TenantIdGUID>/` where <TenantIdGUID> is the tenant ID of the Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="cb2a8-133">Azure AD sets this value to `https://login.microsoftonline.com/<TenantIdGUID>/` where <TenantIdGUID> is the tenant ID of the Azure AD tenant.</span></span>

<span data-ttu-id="cb2a8-134">To evaluate the value of the `Issuer` element, use the value of the **App ID URI** provided during application registration.</span><span class="sxs-lookup"><span data-stu-id="cb2a8-134">To evaluate the value of the `Issuer` element, use the value of the **App ID URI** provided during application registration.</span></span>

### <a name="status"></a><span data-ttu-id="cb2a8-135">Status</span><span class="sxs-lookup"><span data-stu-id="cb2a8-135">Status</span></span>
<span data-ttu-id="cb2a8-136">Azure AD uses the `StatusCode` element in the `Status` element to indicate the success or failure of sign-out. When the sign-out attempt fails, the `StatusCode` element can also contain custom error messages.</span><span class="sxs-lookup"><span data-stu-id="cb2a8-136">Azure AD uses the `StatusCode` element in the `Status` element to indicate the success or failure of sign-out. When the sign-out attempt fails, the `StatusCode` element can also contain custom error messages.</span></span>
