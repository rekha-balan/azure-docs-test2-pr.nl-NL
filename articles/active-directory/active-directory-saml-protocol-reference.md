---
title: Azure AD SAML Protocol Reference | Microsoft Docs
description: This article provides an overview of the Single Sign-On and Single Sign-Out SAML profiles in Azure Active Directory.
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: ''
ms.assetid: 88125cfc-45c1-448b-9903-a629d8f31b01
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: priyamo
ms.openlocfilehash: 53e9fd58e72d83db32fa1fab937b4618cd4cd159
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662683"
---
# <a name="how-azure-active-directory-uses-the-saml-protocol"></a><span data-ttu-id="04f78-103">How Azure Active Directory uses the SAML protocol</span><span class="sxs-lookup"><span data-stu-id="04f78-103">How Azure Active Directory uses the SAML protocol</span></span>
<span data-ttu-id="04f78-104">Azure Active Directory (Azure AD) uses the SAML 2.0 protocol to enable applications to provide a single sign-on experience to their users.</span><span class="sxs-lookup"><span data-stu-id="04f78-104">Azure Active Directory (Azure AD) uses the SAML 2.0 protocol to enable applications to provide a single sign-on experience to their users.</span></span> <span data-ttu-id="04f78-105">The [Single Sign-On](active-directory-single-sign-on-protocol-reference.md) and [Single Sign-Out](active-directory-single-sign-out-protocol-reference.md) SAML profiles of Azure AD explain how SAML assertions, protocols and bindings are used in the identity provider service.</span><span class="sxs-lookup"><span data-stu-id="04f78-105">The [Single Sign-On](active-directory-single-sign-on-protocol-reference.md) and [Single Sign-Out](active-directory-single-sign-out-protocol-reference.md) SAML profiles of Azure AD explain how SAML assertions, protocols and bindings are used in the identity provider service.</span></span>

<span data-ttu-id="04f78-106">SAML Protocol requires the identity provider (Azure AD) and the service provider (the application) to exchange information about themselves.</span><span class="sxs-lookup"><span data-stu-id="04f78-106">SAML Protocol requires the identity provider (Azure AD) and the service provider (the application) to exchange information about themselves.</span></span>

<span data-ttu-id="04f78-107">When an application is registered with Azure AD, the app developer registers federation-related information with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="04f78-107">When an application is registered with Azure AD, the app developer registers federation-related information with Azure AD.</span></span> <span data-ttu-id="04f78-108">This includes the **Redirect URI** of the application.</span><span class="sxs-lookup"><span data-stu-id="04f78-108">This includes the **Redirect URI** of the application.</span></span>

<span data-ttu-id="04f78-109">Azure Active Directory exposes tenant-specific and common (tenant-independent) single sign-on and single sign-out endpoints.</span><span class="sxs-lookup"><span data-stu-id="04f78-109">Azure Active Directory exposes tenant-specific and common (tenant-independent) single sign-on and single sign-out endpoints.</span></span> <span data-ttu-id="04f78-110">These URLs represent addressable locations -- they are not just an identifiers -- so you can go to the endpoint to read the metadata.</span><span class="sxs-lookup"><span data-stu-id="04f78-110">These URLs represent addressable locations -- they are not just an identifiers -- so you can go to the endpoint to read the metadata.</span></span>

* <span data-ttu-id="04f78-111">The Tenant-specific endpoint is located at `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span><span class="sxs-lookup"><span data-stu-id="04f78-111">The Tenant-specific endpoint is located at `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span>  <span data-ttu-id="04f78-112">The <TenantDomainName> placeholder represents a registered domain name or TenantID GUID of an Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="04f78-112">The <TenantDomainName> placeholder represents a registered domain name or TenantID GUID of an Azure AD tenant.</span></span> <span data-ttu-id="04f78-113">For example, the federation metadata of the contoso.com tenant is at: https://login.microsoftonline.com/contoso.com/FederationMetadata/2007-06/FederationMetadata.xml</span><span class="sxs-lookup"><span data-stu-id="04f78-113">For example, the federation metadata of the contoso.com tenant is at: https://login.microsoftonline.com/contoso.com/FederationMetadata/2007-06/FederationMetadata.xml</span></span>

* <span data-ttu-id="04f78-114">The Tenant-independent endpoint is located at `https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml`.In this endpoint address, **common** appears, instead of a tenant domain name or ID.</span><span class="sxs-lookup"><span data-stu-id="04f78-114">The Tenant-independent endpoint is located at `https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml`.In this endpoint address, **common** appears, instead of a tenant domain name or ID.</span></span>

<span data-ttu-id="04f78-115">For information about the Federation Metadata documents that Azure AD publishes, see [Federation Metadata](active-directory-federation-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="04f78-115">For information about the Federation Metadata documents that Azure AD publishes, see [Federation Metadata](active-directory-federation-metadata.md).</span></span>
