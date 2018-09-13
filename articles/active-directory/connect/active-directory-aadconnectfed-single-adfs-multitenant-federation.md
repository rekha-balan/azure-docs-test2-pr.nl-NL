---
title: Federating multiple Azure AD with single AD FS | Microsoft Docs
description: In this document you will learn how to federate multiple Azure AD with a single AD FS.
keywords: federate, ADFS, AD FS, multiple tenants, single AD FS, one ADFS, multi-tenant federation, multi-forest adfs, aad connect, federation, cross-tenant federation
services: active-directory
documentationcenter: ''
author: billmath
manager: mtillman
editor: ''
ms.assetid: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.component: hybrid
ms.author: billmath
ms.openlocfilehash: 91436af0aa26c079d5cd2cc19d16a1ff0354e860
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44821176"
---
# <a name="federate-multiple-instances-of-azure-ad-with-single-instance-of-ad-fs"></a><span data-ttu-id="64d88-104">Federate multiple instances of Azure AD with single instance of AD FS</span><span class="sxs-lookup"><span data-stu-id="64d88-104">Federate multiple instances of Azure AD with single instance of AD FS</span></span>

<span data-ttu-id="64d88-105">A single high available AD FS farm can federate multiple forests if they have 2-way trust between them.</span><span class="sxs-lookup"><span data-stu-id="64d88-105">A single high available AD FS farm can federate multiple forests if they have 2-way trust between them.</span></span> <span data-ttu-id="64d88-106">These multiple forests may or may not correspond to the same Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="64d88-106">These multiple forests may or may not correspond to the same Azure Active Directory.</span></span> <span data-ttu-id="64d88-107">This article provides instructions on how to configure federation between a single AD FS deployment and more than one forests that sync to different Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64d88-107">This article provides instructions on how to configure federation between a single AD FS deployment and more than one forests that sync to different Azure AD.</span></span>

![Multi-tenant federation with single AD FS](media/active-directory-aadconnectfed-single-adfs-multitenant-federation/concept.png)
 
> [!NOTE]
> <span data-ttu-id="64d88-109">Device writeback and automatic device join are not supported in this scenario.</span><span class="sxs-lookup"><span data-stu-id="64d88-109">Device writeback and automatic device join are not supported in this scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="64d88-110">Azure AD Connect cannot be used to configure federation in this scenario as Azure AD Connect can configure federation for domains in a single Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64d88-110">Azure AD Connect cannot be used to configure federation in this scenario as Azure AD Connect can configure federation for domains in a single Azure AD.</span></span>

## <a name="steps-for-federating-ad-fs-with-multiple-azure-ad"></a><span data-ttu-id="64d88-111">Steps for federating AD FS with multiple Azure AD</span><span class="sxs-lookup"><span data-stu-id="64d88-111">Steps for federating AD FS with multiple Azure AD</span></span>

<span data-ttu-id="64d88-112">Consider a domain contoso.com in Azure Active Directory contoso.onmicrosoft.com is already federated with the AD FS on-premises installed in contoso.com on-premises Active Directory environment.</span><span class="sxs-lookup"><span data-stu-id="64d88-112">Consider a domain contoso.com in Azure Active Directory contoso.onmicrosoft.com is already federated with the AD FS on-premises installed in contoso.com on-premises Active Directory environment.</span></span> <span data-ttu-id="64d88-113">Fabrikam.com is a domain in fabrikam.onmicrosoft.com Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="64d88-113">Fabrikam.com is a domain in fabrikam.onmicrosoft.com Azure Active Directory.</span></span>

## <a name="step-1-establish-a-two-way-trust"></a><span data-ttu-id="64d88-114">Step 1: Establish a two-way trust</span><span class="sxs-lookup"><span data-stu-id="64d88-114">Step 1: Establish a two-way trust</span></span>
 
<span data-ttu-id="64d88-115">For AD FS in contoso.com to be able to authenticate users in fabrikam.com, a two-way trust is needed between contoso.com and fabrikam.com.</span><span class="sxs-lookup"><span data-stu-id="64d88-115">For AD FS in contoso.com to be able to authenticate users in fabrikam.com, a two-way trust is needed between contoso.com and fabrikam.com.</span></span> <span data-ttu-id="64d88-116">Follow the guideline in this [article](https://technet.microsoft.com/library/cc816590.aspx) to create the two-way trust.</span><span class="sxs-lookup"><span data-stu-id="64d88-116">Follow the guideline in this [article](https://technet.microsoft.com/library/cc816590.aspx) to create the two-way trust.</span></span>
 
## <a name="step-2-modify-contosocom-federation-settings"></a><span data-ttu-id="64d88-117">Step 2: Modify contoso.com federation settings</span><span class="sxs-lookup"><span data-stu-id="64d88-117">Step 2: Modify contoso.com federation settings</span></span> 
 
<span data-ttu-id="64d88-118">The default issuer set for a single domain federated to AD FS is "http://ADFSServiceFQDN/adfs/services/trust", for example, “http://fs.contoso.com/adfs/services/trust”.</span><span class="sxs-lookup"><span data-stu-id="64d88-118">The default issuer set for a single domain federated to AD FS is "http://ADFSServiceFQDN/adfs/services/trust", for example, “http://fs.contoso.com/adfs/services/trust”.</span></span> <span data-ttu-id="64d88-119">Azure Active Directory requires unique issuer for each federated domain.</span><span class="sxs-lookup"><span data-stu-id="64d88-119">Azure Active Directory requires unique issuer for each federated domain.</span></span> <span data-ttu-id="64d88-120">Since the same AD FS is going to federate two domains, the issuer value needs to be modified so that it is unique for each domain AD FS federates with Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="64d88-120">Since the same AD FS is going to federate two domains, the issuer value needs to be modified so that it is unique for each domain AD FS federates with Azure Active Directory.</span></span> 
 
<span data-ttu-id="64d88-121">On the AD FS server, open Azure AD PowerShell and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="64d88-121">On the AD FS server, open Azure AD PowerShell and perform the following steps:</span></span>
 
<span data-ttu-id="64d88-122">Connect to the Azure Active Directory that contains the domain contoso.com Connect-MsolService Update the federation settings for contoso.com Update-MsolFederatedDomain -DomainName contoso.com –SupportMultipleDomain</span><span class="sxs-lookup"><span data-stu-id="64d88-122">Connect to the Azure Active Directory that contains the domain contoso.com Connect-MsolService Update the federation settings for contoso.com Update-MsolFederatedDomain -DomainName contoso.com –SupportMultipleDomain</span></span>
 
<span data-ttu-id="64d88-123">Issuer in the domain federation setting will be changed to "http://contoso.com/adfs/services/trust" and an issuance claim rule will be added for the Azure AD Relying Party Trust to issue the correct issuerId value based on the UPN suffix.</span><span class="sxs-lookup"><span data-stu-id="64d88-123">Issuer in the domain federation setting will be changed to "http://contoso.com/adfs/services/trust" and an issuance claim rule will be added for the Azure AD Relying Party Trust to issue the correct issuerId value based on the UPN suffix.</span></span>
 
## <a name="step-3-federate-fabrikamcom-with-ad-fs"></a><span data-ttu-id="64d88-124">Step 3: Federate fabrikam.com with AD FS</span><span class="sxs-lookup"><span data-stu-id="64d88-124">Step 3: Federate fabrikam.com with AD FS</span></span>
 
<span data-ttu-id="64d88-125">In Azure AD powershell session perform the following steps: Connect to Azure Active Directory that contains the domain fabrikam.com</span><span class="sxs-lookup"><span data-stu-id="64d88-125">In Azure AD powershell session perform the following steps: Connect to Azure Active Directory that contains the domain fabrikam.com</span></span>

    Connect-MsolService
<span data-ttu-id="64d88-126">Convert the fabrikam.com managed domain to federated:</span><span class="sxs-lookup"><span data-stu-id="64d88-126">Convert the fabrikam.com managed domain to federated:</span></span>

    Convert-MsolDomainToFederated -DomainName fabrikam.com -Verbose -SupportMultipleDomain
 
<span data-ttu-id="64d88-127">The above operation will federate the domain fabrikam.com with the same AD FS.</span><span class="sxs-lookup"><span data-stu-id="64d88-127">The above operation will federate the domain fabrikam.com with the same AD FS.</span></span> <span data-ttu-id="64d88-128">You can verify the domain settings by using Get-MsolDomainFederationSettings for both domains.</span><span class="sxs-lookup"><span data-stu-id="64d88-128">You can verify the domain settings by using Get-MsolDomainFederationSettings for both domains.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64d88-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="64d88-129">Next steps</span></span>
[<span data-ttu-id="64d88-130">Connect Active Directory with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="64d88-130">Connect Active Directory with Azure Active Directory</span></span>](active-directory-aadconnect.md)
