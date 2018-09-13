---
title: Manage permissions to resources per user in Azure Stack (service administrator and tenant) | Microsoft Docs
description: As a service administrator or tenant, learn how to manage RBAC permissions.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/10/2018
ms.author: mabrigg
ms.reviewer: thoroet
ms.openlocfilehash: ab61e1f892f46ad36df741b7a72afcfcbaa0ed87
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44788897"
---
# <a name="manage-role-based-access-control"></a><span data-ttu-id="7fd9d-103">Manage Role-Based Access Control</span><span class="sxs-lookup"><span data-stu-id="7fd9d-103">Manage Role-Based Access Control</span></span>

<span data-ttu-id="7fd9d-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="7fd9d-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="7fd9d-105">A user in Azure Stack can be a reader, owner, or contributor for each instance of a subscription, resource group, or service.</span><span class="sxs-lookup"><span data-stu-id="7fd9d-105">A user in Azure Stack can be a reader, owner, or contributor for each instance of a subscription, resource group, or service.</span></span> <span data-ttu-id="7fd9d-106">For example, User A might have reader permissions to Subscription One, but have owner permissions to Virtual Machine Seven.</span><span class="sxs-lookup"><span data-stu-id="7fd9d-106">For example, User A might have reader permissions to Subscription One, but have owner permissions to Virtual Machine Seven.</span></span>

 - <span data-ttu-id="7fd9d-107">Reader: User can view everything, but can’t make any changes.</span><span class="sxs-lookup"><span data-stu-id="7fd9d-107">Reader: User can view everything, but can’t make any changes.</span></span>
 - <span data-ttu-id="7fd9d-108">Contributor: User can manage everything except access to resources.</span><span class="sxs-lookup"><span data-stu-id="7fd9d-108">Contributor: User can manage everything except access to resources.</span></span>
 - <span data-ttu-id="7fd9d-109">Owner: User can manage everything, including access to resources.</span><span class="sxs-lookup"><span data-stu-id="7fd9d-109">Owner: User can manage everything, including access to resources.</span></span>

## <a name="set-access-permissions-for-a-user"></a><span data-ttu-id="7fd9d-110">Set access permissions for a user</span><span class="sxs-lookup"><span data-stu-id="7fd9d-110">Set access permissions for a user</span></span>

1. <span data-ttu-id="7fd9d-111">Sign in with an account that has owner permissions to the resource you want to manage.</span><span class="sxs-lookup"><span data-stu-id="7fd9d-111">Sign in with an account that has owner permissions to the resource you want to manage.</span></span>
2. <span data-ttu-id="7fd9d-112">In the blade for the resource, click the **Access** icon ![](media/azure-stack-manage-permissions/image1.png).</span><span class="sxs-lookup"><span data-stu-id="7fd9d-112">In the blade for the resource, click the **Access** icon ![](media/azure-stack-manage-permissions/image1.png).</span></span>
3. <span data-ttu-id="7fd9d-113">In the **Users** blade, click **Roles**.</span><span class="sxs-lookup"><span data-stu-id="7fd9d-113">In the **Users** blade, click **Roles**.</span></span>
4. <span data-ttu-id="7fd9d-114">In the **Roles** blade, click **Add** to add permissions for the user.</span><span class="sxs-lookup"><span data-stu-id="7fd9d-114">In the **Roles** blade, click **Add** to add permissions for the user.</span></span>

## <a name="set-access-permissions-for-a-universal-group"></a><span data-ttu-id="7fd9d-115">Set access permissions for a universal group</span><span class="sxs-lookup"><span data-stu-id="7fd9d-115">Set access permissions for a universal group</span></span> 

> [!Note]  
<span data-ttu-id="7fd9d-116">Applicable only to Active Directory Federated Services (AD FS).</span><span class="sxs-lookup"><span data-stu-id="7fd9d-116">Applicable only to Active Directory Federated Services (AD FS).</span></span>

1. <span data-ttu-id="7fd9d-117">Sign in with an account that has owner permissions to the resource you want to manage.</span><span class="sxs-lookup"><span data-stu-id="7fd9d-117">Sign in with an account that has owner permissions to the resource you want to manage.</span></span>
2. <span data-ttu-id="7fd9d-118">In the blade for the resource, click the **Access** icon ![](media/azure-stack-manage-permissions/image1.png).</span><span class="sxs-lookup"><span data-stu-id="7fd9d-118">In the blade for the resource, click the **Access** icon ![](media/azure-stack-manage-permissions/image1.png).</span></span>
3. <span data-ttu-id="7fd9d-119">In the **Users** blade, click **Roles**.</span><span class="sxs-lookup"><span data-stu-id="7fd9d-119">In the **Users** blade, click **Roles**.</span></span>
4. <span data-ttu-id="7fd9d-120">In the **Roles** blade, click **Add** to add permissions for the Universal Group Active Directory Group.</span><span class="sxs-lookup"><span data-stu-id="7fd9d-120">In the **Roles** blade, click **Add** to add permissions for the Universal Group Active Directory Group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7fd9d-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="7fd9d-121">Next steps</span></span>
[<span data-ttu-id="7fd9d-122">Add an Azure Stack tenant</span><span class="sxs-lookup"><span data-stu-id="7fd9d-122">Add an Azure Stack tenant</span></span>](azure-stack-add-new-user-aad.md)

