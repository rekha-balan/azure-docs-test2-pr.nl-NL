---
title: 'Azure Active Directory Domain Services: Enable kerberos constrained delegation | Microsoft Docs'
description: Enable kerberos constrained delegation on Azure Active Directory Domain Services managed domains
services: active-directory-ds
documentationcenter: ''
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: f36f16a7bb00ace9fd5164eb38ba77f015f22f5c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555866"
---
# <a name="configure-kerberos-constrained-delegation-kcd-on-a-managed-domain"></a><span data-ttu-id="645d2-103">Configure kerberos constrained delegation (KCD) on a managed domain</span><span class="sxs-lookup"><span data-stu-id="645d2-103">Configure kerberos constrained delegation (KCD) on a managed domain</span></span>
<span data-ttu-id="645d2-104">Many applications need to access resources in the context of the user.</span><span class="sxs-lookup"><span data-stu-id="645d2-104">Many applications need to access resources in the context of the user.</span></span> <span data-ttu-id="645d2-105">Active Directory supports a mechanism called Kerberos delegation, which enables this use-case.</span><span class="sxs-lookup"><span data-stu-id="645d2-105">Active Directory supports a mechanism called Kerberos delegation, which enables this use-case.</span></span> <span data-ttu-id="645d2-106">Further, you can restrict delegation so that only specific resources can be accessed in the context of the user.</span><span class="sxs-lookup"><span data-stu-id="645d2-106">Further, you can restrict delegation so that only specific resources can be accessed in the context of the user.</span></span> <span data-ttu-id="645d2-107">Azure AD Domain Services managed domains are different from traditional Active Directory domains since they are more securely locked down.</span><span class="sxs-lookup"><span data-stu-id="645d2-107">Azure AD Domain Services managed domains are different from traditional Active Directory domains since they are more securely locked down.</span></span>

<span data-ttu-id="645d2-108">This article shows you how to configure kerberos constrained delegation on an Azure AD Domain Services managed domain.</span><span class="sxs-lookup"><span data-stu-id="645d2-108">This article shows you how to configure kerberos constrained delegation on an Azure AD Domain Services managed domain.</span></span>

## <a name="kerberos-constrained-delegation-kcd"></a><span data-ttu-id="645d2-109">Kerberos constrained delegation (KCD)</span><span class="sxs-lookup"><span data-stu-id="645d2-109">Kerberos constrained delegation (KCD)</span></span>
<span data-ttu-id="645d2-110">Kerberos delegation enables an account to impersonate another security principal (such as a user) to access resources.</span><span class="sxs-lookup"><span data-stu-id="645d2-110">Kerberos delegation enables an account to impersonate another security principal (such as a user) to access resources.</span></span> <span data-ttu-id="645d2-111">Consider a web application that accesses a back-end web API in the context of a user.</span><span class="sxs-lookup"><span data-stu-id="645d2-111">Consider a web application that accesses a back-end web API in the context of a user.</span></span> <span data-ttu-id="645d2-112">In this example, the web application (running in the context of a service account or a computer/machine account) impersonates the user when accessing the resource (back-end web API).</span><span class="sxs-lookup"><span data-stu-id="645d2-112">In this example, the web application (running in the context of a service account or a computer/machine account) impersonates the user when accessing the resource (back-end web API).</span></span> <span data-ttu-id="645d2-113">Kerberos delegation is insecure since it does not restrict the resources the impersonating account can access in the context of the user.</span><span class="sxs-lookup"><span data-stu-id="645d2-113">Kerberos delegation is insecure since it does not restrict the resources the impersonating account can access in the context of the user.</span></span>

<span data-ttu-id="645d2-114">Kerberos constrained delegation (KCD) restricts the services/resources to which the specified server can act on the behalf of a user.</span><span class="sxs-lookup"><span data-stu-id="645d2-114">Kerberos constrained delegation (KCD) restricts the services/resources to which the specified server can act on the behalf of a user.</span></span> <span data-ttu-id="645d2-115">Traditional KCD requires domain administrator privileges to configure a domain account for a service and it restricts the account to a single domain.</span><span class="sxs-lookup"><span data-stu-id="645d2-115">Traditional KCD requires domain administrator privileges to configure a domain account for a service and it restricts the account to a single domain.</span></span>

<span data-ttu-id="645d2-116">Traditional KCD also has a few issues associated with it.</span><span class="sxs-lookup"><span data-stu-id="645d2-116">Traditional KCD also has a few issues associated with it.</span></span> <span data-ttu-id="645d2-117">In earlier operating systems where the domain administrator configured the service, the service administrator had no useful way to know which front-end services delegated to the resource services they owned.</span><span class="sxs-lookup"><span data-stu-id="645d2-117">In earlier operating systems where the domain administrator configured the service, the service administrator had no useful way to know which front-end services delegated to the resource services they owned.</span></span> <span data-ttu-id="645d2-118">And any front-end service that could delegate to a resource service represented a potential attack point.</span><span class="sxs-lookup"><span data-stu-id="645d2-118">And any front-end service that could delegate to a resource service represented a potential attack point.</span></span> <span data-ttu-id="645d2-119">If a server that hosted a front-end service was compromised, and it was configured to delegate to resource services, the resource services could also be compromised.</span><span class="sxs-lookup"><span data-stu-id="645d2-119">If a server that hosted a front-end service was compromised, and it was configured to delegate to resource services, the resource services could also be compromised.</span></span>

> [!NOTE]
> <span data-ttu-id="645d2-120">On an Azure AD Domain Services managed domain, you do not have domain administrator privileges.</span><span class="sxs-lookup"><span data-stu-id="645d2-120">On an Azure AD Domain Services managed domain, you do not have domain administrator privileges.</span></span> <span data-ttu-id="645d2-121">Therefore, **traditional KCD cannot be configured on a managed domain**.</span><span class="sxs-lookup"><span data-stu-id="645d2-121">Therefore, **traditional KCD cannot be configured on a managed domain**.</span></span> <span data-ttu-id="645d2-122">Use resource-based KCD as described in this article.</span><span class="sxs-lookup"><span data-stu-id="645d2-122">Use resource-based KCD as described in this article.</span></span> <span data-ttu-id="645d2-123">This mechanism is also more secure.</span><span class="sxs-lookup"><span data-stu-id="645d2-123">This mechanism is also more secure.</span></span>
>
>

## <a name="resource-based-kerberos-constrained-delegation"></a><span data-ttu-id="645d2-124">Resource-based kerberos constrained delegation</span><span class="sxs-lookup"><span data-stu-id="645d2-124">Resource-based kerberos constrained delegation</span></span>
<span data-ttu-id="645d2-125">In Windows Server 2012 R2 and Windows Server 2012, the ability to configure constrained delegation for the service has been transferred from the domain administrator to the service administrator.</span><span class="sxs-lookup"><span data-stu-id="645d2-125">In Windows Server 2012 R2 and Windows Server 2012, the ability to configure constrained delegation for the service has been transferred from the domain administrator to the service administrator.</span></span> <span data-ttu-id="645d2-126">In this way, the back-end service administrator can allow or deny front-end services.</span><span class="sxs-lookup"><span data-stu-id="645d2-126">In this way, the back-end service administrator can allow or deny front-end services.</span></span> <span data-ttu-id="645d2-127">This model is known as **resource-based kerberos constrained delegation**.</span><span class="sxs-lookup"><span data-stu-id="645d2-127">This model is known as **resource-based kerberos constrained delegation**.</span></span>

<span data-ttu-id="645d2-128">Resource-based KCD is configured using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="645d2-128">Resource-based KCD is configured using PowerShell.</span></span> <span data-ttu-id="645d2-129">You use the Set-ADComputer or Set-ADUser cmdlets, depending on whether the impersonating account is a computer account or a user account/service account.</span><span class="sxs-lookup"><span data-stu-id="645d2-129">You use the Set-ADComputer or Set-ADUser cmdlets, depending on whether the impersonating account is a computer account or a user account/service account.</span></span>

### <a name="configure-resource-based-kcd-for-a-computer-account-on-a-managed-domain"></a><span data-ttu-id="645d2-130">Configure resource-based KCD for a computer account on a managed domain</span><span class="sxs-lookup"><span data-stu-id="645d2-130">Configure resource-based KCD for a computer account on a managed domain</span></span>
<span data-ttu-id="645d2-131">Assume you have a web app running on the computer 'contoso100-webapp.contoso100.com'.</span><span class="sxs-lookup"><span data-stu-id="645d2-131">Assume you have a web app running on the computer 'contoso100-webapp.contoso100.com'.</span></span> <span data-ttu-id="645d2-132">It needs to access the resource (a web API running on 'contoso100-api.contoso100.com') in the context of domain users.</span><span class="sxs-lookup"><span data-stu-id="645d2-132">It needs to access the resource (a web API running on 'contoso100-api.contoso100.com') in the context of domain users.</span></span> <span data-ttu-id="645d2-133">Here's how you would set up resource-based KCD for this scenario.</span><span class="sxs-lookup"><span data-stu-id="645d2-133">Here's how you would set up resource-based KCD for this scenario.</span></span>

```
$ImpersonatingAccount = Get-ADComputer -Identity contoso100-webapp.contoso100.com
Set-ADComputer contoso100-api.contoso100.com -PrincipalsAllowedToDelegateToAccount $ImpersonatingAccount
```

### <a name="configure-resource-based-kcd-for-a-user-account-on-a-managed-domain"></a><span data-ttu-id="645d2-134">Configure resource-based KCD for a user account on a managed domain</span><span class="sxs-lookup"><span data-stu-id="645d2-134">Configure resource-based KCD for a user account on a managed domain</span></span>
<span data-ttu-id="645d2-135">Assume you have a web app running as a service account 'appsvc' and it needs to access the resource (a web API running as a service account - 'backendsvc') in the context of domain users.</span><span class="sxs-lookup"><span data-stu-id="645d2-135">Assume you have a web app running as a service account 'appsvc' and it needs to access the resource (a web API running as a service account - 'backendsvc') in the context of domain users.</span></span> <span data-ttu-id="645d2-136">Here's how you would set up resource-based KCD for this scenario.</span><span class="sxs-lookup"><span data-stu-id="645d2-136">Here's how you would set up resource-based KCD for this scenario.</span></span>

```
$ImpersonatingAccount = Get-ADUser -Identity appsvc
Set-ADUser backendsvc -PrincipalsAllowedToDelegateToAccount $ImpersonatingAccount
```

## <a name="related-content"></a><span data-ttu-id="645d2-137">Related Content</span><span class="sxs-lookup"><span data-stu-id="645d2-137">Related Content</span></span>
* [<span data-ttu-id="645d2-138">Azure AD Domain Services - Getting Started guide</span><span class="sxs-lookup"><span data-stu-id="645d2-138">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="645d2-139">Kerberos Constrained Delegation Overview</span><span class="sxs-lookup"><span data-stu-id="645d2-139">Kerberos Constrained Delegation Overview</span></span>](https://technet.microsoft.com/library/jj553400.aspx)
