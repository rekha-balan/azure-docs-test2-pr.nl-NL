---
title: Troubleshoot Secure LDAP (LDAPS) in Azure AD Domain Services | Microsoft Docs
description: Troubleshoot Secure LDAP (LDAPS) for an Azure AD Domain Services managed domain
services: active-directory-ds
documentationcenter: ''
author: mahesh-unnikrishnan
manager: mtillman
editor: curtand
ms.assetid: 445c60da-e115-447b-841d-96739975bdf6
ms.service: active-directory
ms.component: domain-services
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 08/01/2018
ms.author: maheshu
ms.openlocfilehash: 9713a06bbf6a61b316e061cb851721a3554cd632
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864882"
---
# <a name="troubleshoot-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="31181-103">Troubleshoot Secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span><span class="sxs-lookup"><span data-stu-id="31181-103">Troubleshoot Secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="connection-issues"></a><span data-ttu-id="31181-104">Connection issues</span><span class="sxs-lookup"><span data-stu-id="31181-104">Connection issues</span></span>
<span data-ttu-id="31181-105">If you have trouble connecting to the managed domain using secure LDAP:</span><span class="sxs-lookup"><span data-stu-id="31181-105">If you have trouble connecting to the managed domain using secure LDAP:</span></span>

* <span data-ttu-id="31181-106">The issuer chain of the secure LDAP certificate must be trusted on the client.</span><span class="sxs-lookup"><span data-stu-id="31181-106">The issuer chain of the secure LDAP certificate must be trusted on the client.</span></span> <span data-ttu-id="31181-107">You may choose to add the Root certification authority to the trusted root certificate store on the client to establish the trust.</span><span class="sxs-lookup"><span data-stu-id="31181-107">You may choose to add the Root certification authority to the trusted root certificate store on the client to establish the trust.</span></span>
* <span data-ttu-id="31181-108">Verify that the LDAP client (for example, ldp.exe) connects to the secure LDAP endpoint using a DNS name, not the IP address.</span><span class="sxs-lookup"><span data-stu-id="31181-108">Verify that the LDAP client (for example, ldp.exe) connects to the secure LDAP endpoint using a DNS name, not the IP address.</span></span>
* <span data-ttu-id="31181-109">Check the DNS name the LDAP client connects to.</span><span class="sxs-lookup"><span data-stu-id="31181-109">Check the DNS name the LDAP client connects to.</span></span> <span data-ttu-id="31181-110">It must resolve to the public IP address for secure LDAP on the managed domain.</span><span class="sxs-lookup"><span data-stu-id="31181-110">It must resolve to the public IP address for secure LDAP on the managed domain.</span></span>
* <span data-ttu-id="31181-111">Verify the secure LDAP certificate for your managed domain has the DNS name in the Subject or the Subject Alternative Names attribute.</span><span class="sxs-lookup"><span data-stu-id="31181-111">Verify the secure LDAP certificate for your managed domain has the DNS name in the Subject or the Subject Alternative Names attribute.</span></span>
* <span data-ttu-id="31181-112">The NSG settings for the virtual network must allow the traffic to port 636 from the internet.</span><span class="sxs-lookup"><span data-stu-id="31181-112">The NSG settings for the virtual network must allow the traffic to port 636 from the internet.</span></span> <span data-ttu-id="31181-113">This step applies only if you've enabled secure LDAP access over the internet.</span><span class="sxs-lookup"><span data-stu-id="31181-113">This step applies only if you've enabled secure LDAP access over the internet.</span></span>


## <a name="need-help"></a><span data-ttu-id="31181-114">Need help?</span><span class="sxs-lookup"><span data-stu-id="31181-114">Need help?</span></span>
<span data-ttu-id="31181-115">If you still have trouble connecting to the managed domain using secure LDAP, [contact the product team](active-directory-ds-contact-us.md) for help.</span><span class="sxs-lookup"><span data-stu-id="31181-115">If you still have trouble connecting to the managed domain using secure LDAP, [contact the product team](active-directory-ds-contact-us.md) for help.</span></span> <span data-ttu-id="31181-116">Include the following information to help diagnose the issue better:</span><span class="sxs-lookup"><span data-stu-id="31181-116">Include the following information to help diagnose the issue better:</span></span>
* <span data-ttu-id="31181-117">A screenshot of ldp.exe making the connection and failing.</span><span class="sxs-lookup"><span data-stu-id="31181-117">A screenshot of ldp.exe making the connection and failing.</span></span>
* <span data-ttu-id="31181-118">Your Azure AD tenant ID, and the DNS domain name of your managed domain.</span><span class="sxs-lookup"><span data-stu-id="31181-118">Your Azure AD tenant ID, and the DNS domain name of your managed domain.</span></span>
* <span data-ttu-id="31181-119">Exact user name that you're trying to bind as.</span><span class="sxs-lookup"><span data-stu-id="31181-119">Exact user name that you're trying to bind as.</span></span>


## <a name="related-content"></a><span data-ttu-id="31181-120">Related content</span><span class="sxs-lookup"><span data-stu-id="31181-120">Related content</span></span>
* [<span data-ttu-id="31181-121">Azure AD Domain Services - Getting Started guide</span><span class="sxs-lookup"><span data-stu-id="31181-121">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="31181-122">Administer an Azure AD Domain Services managed domain</span><span class="sxs-lookup"><span data-stu-id="31181-122">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="31181-123">LDAP query basics</span><span class="sxs-lookup"><span data-stu-id="31181-123">LDAP query basics</span></span>](https://technet.microsoft.com/library/aa996205.aspx)
* [<span data-ttu-id="31181-124">Administer Group Policy on an Azure AD Domain Services managed domain</span><span class="sxs-lookup"><span data-stu-id="31181-124">Administer Group Policy on an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-group-policy.md)
* [<span data-ttu-id="31181-125">Network security groups</span><span class="sxs-lookup"><span data-stu-id="31181-125">Network security groups</span></span>](../virtual-network/security-overview.md)
* [<span data-ttu-id="31181-126">Create a Network Security Group</span><span class="sxs-lookup"><span data-stu-id="31181-126">Create a Network Security Group</span></span>](../virtual-network/tutorial-filter-network-traffic.md)
