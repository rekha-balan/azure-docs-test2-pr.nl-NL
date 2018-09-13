---
title: Characteristics of Azure Active Directory tenant interaction | Microsoft Docs
description: Manage your Azure Active tenant tenants by understanding your tenants as fully independent resources
services: active-tenant
documentationcenter: ''
author: curtand
manager: mtillman
editor: ''
ms.service: active-directory
ms.topic: article
ms.workload: identity
ms.component: users-groups-roles
ms.date: 10/10/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017;it-pro
ms.reviewer: piotrci
ms.openlocfilehash: 85f7cddb7231bf9c5e45de87af3c922148f214be
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857721"
---
# <a name="understand-how-multiple-azure-active-directory-tenants-interact"></a><span data-ttu-id="b4d3d-103">Understand how multiple Azure Active Directory tenants interact</span><span class="sxs-lookup"><span data-stu-id="b4d3d-103">Understand how multiple Azure Active Directory tenants interact</span></span>

<span data-ttu-id="b4d3d-104">In Azure Active Directory (Azure AD), each tenant is a fully independent resource: a peer that is logically independent from the other tenants that you manage.</span><span class="sxs-lookup"><span data-stu-id="b4d3d-104">In Azure Active Directory (Azure AD), each tenant is a fully independent resource: a peer that is logically independent from the other tenants that you manage.</span></span> <span data-ttu-id="b4d3d-105">There is no parent-child relationship between tenants.</span><span class="sxs-lookup"><span data-stu-id="b4d3d-105">There is no parent-child relationship between tenants.</span></span> <span data-ttu-id="b4d3d-106">This independence between tenants includes resource independence, administrative independence, and synchronization independence.</span><span class="sxs-lookup"><span data-stu-id="b4d3d-106">This independence between tenants includes resource independence, administrative independence, and synchronization independence.</span></span>

## <a name="resource-independence"></a><span data-ttu-id="b4d3d-107">Resource independence</span><span class="sxs-lookup"><span data-stu-id="b4d3d-107">Resource independence</span></span>
* <span data-ttu-id="b4d3d-108">If you create or delete a resource in one tenant, it has no impact on any resource in another tenant, with the partial exception of external users.</span><span class="sxs-lookup"><span data-stu-id="b4d3d-108">If you create or delete a resource in one tenant, it has no impact on any resource in another tenant, with the partial exception of external users.</span></span> 
* <span data-ttu-id="b4d3d-109">If you use one of your domain names with one tenant, it cannot be used with any other tenant.</span><span class="sxs-lookup"><span data-stu-id="b4d3d-109">If you use one of your domain names with one tenant, it cannot be used with any other tenant.</span></span>

## <a name="administrative-independence"></a><span data-ttu-id="b4d3d-110">Administrative independence</span><span class="sxs-lookup"><span data-stu-id="b4d3d-110">Administrative independence</span></span>
<span data-ttu-id="b4d3d-111">If a non-administrative user of tenant 'Contoso' creates a test tenant 'Test,' then:</span><span class="sxs-lookup"><span data-stu-id="b4d3d-111">If a non-administrative user of tenant 'Contoso' creates a test tenant 'Test,' then:</span></span>

* <span data-ttu-id="b4d3d-112">By default, the user who creates a tenant is added as an external user in that new tenant, and assigned the global administrator role in that tenant.</span><span class="sxs-lookup"><span data-stu-id="b4d3d-112">By default, the user who creates a tenant is added as an external user in that new tenant, and assigned the global administrator role in that tenant.</span></span>
* <span data-ttu-id="b4d3d-113">The administrators of tenant 'Contoso' have no direct administrative privileges to tenant 'Test,' unless an administrator of 'Test' specifically grants them these privileges.</span><span class="sxs-lookup"><span data-stu-id="b4d3d-113">The administrators of tenant 'Contoso' have no direct administrative privileges to tenant 'Test,' unless an administrator of 'Test' specifically grants them these privileges.</span></span> <span data-ttu-id="b4d3d-114">However, administrators of 'Contoso' can control access to tenant 'Test' if they control the user account that created 'Test.'</span><span class="sxs-lookup"><span data-stu-id="b4d3d-114">However, administrators of 'Contoso' can control access to tenant 'Test' if they control the user account that created 'Test.'</span></span>
* <span data-ttu-id="b4d3d-115">If you add/remove an administrator role for a user in one tenant, the change does not affect the administrator roles that the user has in another tenant.</span><span class="sxs-lookup"><span data-stu-id="b4d3d-115">If you add/remove an administrator role for a user in one tenant, the change does not affect the administrator roles that the user has in another tenant.</span></span>

## <a name="synchronization-independence"></a><span data-ttu-id="b4d3d-116">Synchronization independence</span><span class="sxs-lookup"><span data-stu-id="b4d3d-116">Synchronization independence</span></span>
<span data-ttu-id="b4d3d-117">You can configure each Azure AD tenant independently to get data synchronized from a single instance of either:</span><span class="sxs-lookup"><span data-stu-id="b4d3d-117">You can configure each Azure AD tenant independently to get data synchronized from a single instance of either:</span></span>

* <span data-ttu-id="b4d3d-118">The Azure AD Connect tool, to synchronize data with a single AD forest.</span><span class="sxs-lookup"><span data-stu-id="b4d3d-118">The Azure AD Connect tool, to synchronize data with a single AD forest.</span></span>
* <span data-ttu-id="b4d3d-119">The Azure Active tenant Connector for Forefront Identity Manager, to synchronize data with one or more on-premises forests, and/or non-Azure AD data sources.</span><span class="sxs-lookup"><span data-stu-id="b4d3d-119">The Azure Active tenant Connector for Forefront Identity Manager, to synchronize data with one or more on-premises forests, and/or non-Azure AD data sources.</span></span>

## <a name="add-an-azure-ad-tenant"></a><span data-ttu-id="b4d3d-120">Add an Azure AD tenant</span><span class="sxs-lookup"><span data-stu-id="b4d3d-120">Add an Azure AD tenant</span></span>
<span data-ttu-id="b4d3d-121">To add an Azure AD tenant in the Azure portal, sign in to [the Azure portal](https://portal.azure.com) with an account that is an Azure AD global administrator, and, on the left, select **New**.</span><span class="sxs-lookup"><span data-stu-id="b4d3d-121">To add an Azure AD tenant in the Azure portal, sign in to [the Azure portal](https://portal.azure.com) with an account that is an Azure AD global administrator, and, on the left, select **New**.</span></span>

> [!NOTE]
> <span data-ttu-id="b4d3d-122">Unlike other Azure resources, your tenants are not child resources of an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="b4d3d-122">Unlike other Azure resources, your tenants are not child resources of an Azure subscription.</span></span> <span data-ttu-id="b4d3d-123">If your Azure subscription is canceled or expired, you can still access your tenant data using Azure PowerShell, the Azure Graph API, or the Office 365 Admin Center.</span><span class="sxs-lookup"><span data-stu-id="b4d3d-123">If your Azure subscription is canceled or expired, you can still access your tenant data using Azure PowerShell, the Azure Graph API, or the Office 365 Admin Center.</span></span> <span data-ttu-id="b4d3d-124">You can also [associate another subscription with the tenant](../fundamentals/active-directory-how-subscriptions-associated-directory.md).</span><span class="sxs-lookup"><span data-stu-id="b4d3d-124">You can also [associate another subscription with the tenant](../fundamentals/active-directory-how-subscriptions-associated-directory.md).</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="b4d3d-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="b4d3d-125">Next steps</span></span>
<span data-ttu-id="b4d3d-126">For a broad overview of Azure AD licensing issues and best practices, see [What is Azure Active tenant licensing?](../fundamentals/active-directory-licensing-whatis-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b4d3d-126">For a broad overview of Azure AD licensing issues and best practices, see [What is Azure Active tenant licensing?](../fundamentals/active-directory-licensing-whatis-azure-portal.md).</span></span>
