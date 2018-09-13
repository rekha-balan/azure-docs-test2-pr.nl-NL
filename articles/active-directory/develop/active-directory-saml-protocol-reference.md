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
ms.openlocfilehash: 398b20d02b84f4ae4b7b06712f233628afddc7ad
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670450"
---
# <a name="how-azure-active-directory-uses-the-saml-protocol"></a><span data-ttu-id="fdb0d-103">How Azure Active Directory uses the SAML protocol</span><span class="sxs-lookup"><span data-stu-id="fdb0d-103">How Azure Active Directory uses the SAML protocol</span></span>
<span data-ttu-id="fdb0d-104">Azure Active Directory (Azure AD) uses the SAML 2.0 protocol to enable applications to provide a single sign-on experience to their users.</span><span class="sxs-lookup"><span data-stu-id="fdb0d-104">Azure Active Directory (Azure AD) uses the SAML 2.0 protocol to enable applications to provide a single sign-on experience to their users.</span></span> <span data-ttu-id="fdb0d-105">The [Single Sign-On](active-directory-single-sign-on-protocol-reference.md) and [Single Sign-Out](active-directory-single-sign-out-protocol-reference.md) SAML profiles of Azure AD explain how SAML assertions, protocols and bindings are used in the identity provider service.</span><span class="sxs-lookup"><span data-stu-id="fdb0d-105">The [Single Sign-On](active-directory-single-sign-on-protocol-reference.md) and [Single Sign-Out](active-directory-single-sign-out-protocol-reference.md) SAML profiles of Azure AD explain how SAML assertions, protocols and bindings are used in the identity provider service.</span></span>

<span data-ttu-id="fdb0d-106">SAML Protocol requires the identity provider (Azure AD) and the service provider (the application) to exchange information about themselves.</span><span class="sxs-lookup"><span data-stu-id="fdb0d-106">SAML Protocol requires the identity provider (Azure AD) and the service provider (the application) to exchange information about themselves.</span></span>

<span data-ttu-id="fdb0d-107">When an application is registered with Azure AD, the app developer registers federation-related information with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fdb0d-107">When an application is registered with Azure AD, the app developer registers federation-related information with Azure AD.</span></span> <span data-ttu-id="fdb0d-108">This includes the **Redirect URI** and **Metadata URI** of the application.</span><span class="sxs-lookup"><span data-stu-id="fdb0d-108">This includes the **Redirect URI** and **Metadata URI** of the application.</span></span>

<span data-ttu-id="fdb0d-109">Azure AD uses the **Metadata URI** of the cloud service to retrieve the signing key and the logout URI of the cloud service.</span><span class="sxs-lookup"><span data-stu-id="fdb0d-109">Azure AD uses the **Metadata URI** of the cloud service to retrieve the signing key and the logout URI of the cloud service.</span></span> <span data-ttu-id="fdb0d-110">If the application does not support a metadata URI, the developer must contact Microsoft support to provide the logout URI and signing key.</span><span class="sxs-lookup"><span data-stu-id="fdb0d-110">If the application does not support a metadata URI, the developer must contact Microsoft support to provide the logout URI and signing key.</span></span>

<span data-ttu-id="fdb0d-111">Azure Active Directory exposes tenant-specific and common (tenant-independent) single sign-on and single sign-out endpoints.</span><span class="sxs-lookup"><span data-stu-id="fdb0d-111">Azure Active Directory exposes tenant-specific and common (tenant-independent) single sign-on and single sign-out endpoints.</span></span> <span data-ttu-id="fdb0d-112">These URLs represent addressable locations -- they are not just an identifiers -- so you can go to the endpoint to read the metadata.</span><span class="sxs-lookup"><span data-stu-id="fdb0d-112">These URLs represent addressable locations -- they are not just an identifiers -- so you can go to the endpoint to read the metadata.</span></span>

* <span data-ttu-id="fdb0d-113">The Tenant-specific endpoint is located at `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span><span class="sxs-lookup"><span data-stu-id="fdb0d-113">The Tenant-specific endpoint is located at `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span>  <span data-ttu-id="fdb0d-114">The <TenantDomainName> placeholder represents a registered domain name or TenantID GUID of an Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="fdb0d-114">The <TenantDomainName> placeholder represents a registered domain name or TenantID GUID of an Azure AD tenant.</span></span> <span data-ttu-id="fdb0d-115">For example, the federation metadata of the contoso.com tenant is at: https://login.microsoftonline.com/contoso.com/FederationMetadata/2007-06/FederationMetadata.xml</span><span class="sxs-lookup"><span data-stu-id="fdb0d-115">For example, the federation metadata of the contoso.com tenant is at: https://login.microsoftonline.com/contoso.com/FederationMetadata/2007-06/FederationMetadata.xml</span></span>

* <span data-ttu-id="fdb0d-116">The Tenant-independent endpoint is located at `https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml`.In this endpoint address, **common** appears, instead of a tenant domain name or ID.</span><span class="sxs-lookup"><span data-stu-id="fdb0d-116">The Tenant-independent endpoint is located at `https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml`.In this endpoint address, **common** appears, instead of a tenant domain name or ID.</span></span>

<span data-ttu-id="fdb0d-117">For information about the Federation Metadata documents that Azure AD publishes, see [Federation Metadata](active-directory-federation-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="fdb0d-117">For information about the Federation Metadata documents that Azure AD publishes, see [Federation Metadata](active-directory-federation-metadata.md).</span></span>
