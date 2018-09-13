---
title: Manage permissions to resources per user in Azure Stack (service administrator and tenant) | Microsoft Docs
description: As a service administrator or tenant, learn how to manage RBAC permissions.
services: azure-stack
documentationcenter: ''
author: Heathl17
manager: byronr
editor: ''
ms.assetid: cccac19a-e1bf-4e36-8ac8-2228e8487646
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: helaw
ms.openlocfilehash: caf9a6790039a9da1cc91d6566c196da41667713
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671336"
---
# <a name="manage-role-based-access-control"></a><span data-ttu-id="d092d-103">Manage Role-Based Access Control</span><span class="sxs-lookup"><span data-stu-id="d092d-103">Manage Role-Based Access Control</span></span>
<span data-ttu-id="d092d-104">A user in Azure Stack can be a reader, owner, or contributor for each instance of a subscription, resource group, or service.</span><span class="sxs-lookup"><span data-stu-id="d092d-104">A user in Azure Stack can be a reader, owner, or contributor for each instance of a subscription, resource group, or service.</span></span> <span data-ttu-id="d092d-105">For example, User A might have reader permissions to Subscription 1, but have owner permissions to Virtual Machine 7.</span><span class="sxs-lookup"><span data-stu-id="d092d-105">For example, User A might have reader permissions to Subscription 1, but have owner permissions to Virtual Machine 7.</span></span>

* <span data-ttu-id="d092d-106">Reader: User can view everything, but can’t make any changes.</span><span class="sxs-lookup"><span data-stu-id="d092d-106">Reader: User can view everything, but can’t make any changes.</span></span>
* <span data-ttu-id="d092d-107">Contributor: User can manage everything except access to resources.</span><span class="sxs-lookup"><span data-stu-id="d092d-107">Contributor: User can manage everything except access to resources.</span></span>
* <span data-ttu-id="d092d-108">Owner: User can manage everything, including access to resources.</span><span class="sxs-lookup"><span data-stu-id="d092d-108">Owner: User can manage everything, including access to resources.</span></span>

## <a name="set-access-permissions-for-a-user"></a><span data-ttu-id="d092d-109">Set access permissions for a user</span><span class="sxs-lookup"><span data-stu-id="d092d-109">Set access permissions for a user</span></span>
1. <span data-ttu-id="d092d-110">Sign in with an account that has owner permissions to the resource you want to manage.</span><span class="sxs-lookup"><span data-stu-id="d092d-110">Sign in with an account that has owner permissions to the resource you want to manage.</span></span>
2. <span data-ttu-id="d092d-111">In the blade for the resource, click the **Access** icon ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-manage-permissions/image1.png).</span><span class="sxs-lookup"><span data-stu-id="d092d-111">In the blade for the resource, click the **Access** icon ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-manage-permissions/image1.png).</span></span>
3. <span data-ttu-id="d092d-112">In the **Users** blade, click **Roles**.</span><span class="sxs-lookup"><span data-stu-id="d092d-112">In the **Users** blade, click **Roles**.</span></span>
4. <span data-ttu-id="d092d-113">In the **Roles** blade, click **Add** to add permissions for the user.</span><span class="sxs-lookup"><span data-stu-id="d092d-113">In the **Roles** blade, click **Add** to add permissions for the user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d092d-114">Next steps</span><span class="sxs-lookup"><span data-stu-id="d092d-114">Next steps</span></span>
[<span data-ttu-id="d092d-115">Add an Azure Stack tenant</span><span class="sxs-lookup"><span data-stu-id="d092d-115">Add an Azure Stack tenant</span></span>](azure-stack-add-new-user-aad.md)


