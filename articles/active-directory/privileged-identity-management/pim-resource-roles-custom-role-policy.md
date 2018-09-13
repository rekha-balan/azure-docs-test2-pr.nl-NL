---
title: Use custom roles for Azure resources in PIM | Microsoft Docs
description: Learn how to use custom roles for Azure resources in Azure AD Privileged Identity Management (PIM).
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
ms.service: active-directory
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.component: pim
ms.date: 03/30/2018
ms.author: rolyon
ms.openlocfilehash: b01e785ac85c71b2982561e8b5e118775750fc69
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855773"
---
# <a name="use-custom-roles-for-azure-resources-in-pim"></a><span data-ttu-id="f076f-103">Use custom roles for Azure resources in PIM</span><span class="sxs-lookup"><span data-stu-id="f076f-103">Use custom roles for Azure resources in PIM</span></span>

<span data-ttu-id="f076f-104">You might need to apply strict Privileged Identity Management (PIM) settings to some members of a role, while providing greater autonomy for others.</span><span class="sxs-lookup"><span data-stu-id="f076f-104">You might need to apply strict Privileged Identity Management (PIM) settings to some members of a role, while providing greater autonomy for others.</span></span> <span data-ttu-id="f076f-105">Consider a scenario in which your organization hires several contract associates to assist in the development of an application that will run in an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="f076f-105">Consider a scenario in which your organization hires several contract associates to assist in the development of an application that will run in an Azure subscription.</span></span>

<span data-ttu-id="f076f-106">As a resource administrator, you want employees to be eligible for access without requiring approval.</span><span class="sxs-lookup"><span data-stu-id="f076f-106">As a resource administrator, you want employees to be eligible for access without requiring approval.</span></span> <span data-ttu-id="f076f-107">However, all contract associates must be approved when they request access to the organization's resources.</span><span class="sxs-lookup"><span data-stu-id="f076f-107">However, all contract associates must be approved when they request access to the organization's resources.</span></span>

<span data-ttu-id="f076f-108">Follow the steps outlined in the next section to set up targeted PIM settings for Azure resource roles.</span><span class="sxs-lookup"><span data-stu-id="f076f-108">Follow the steps outlined in the next section to set up targeted PIM settings for Azure resource roles.</span></span>

## <a name="create-the-custom-role"></a><span data-ttu-id="f076f-109">Create the custom role</span><span class="sxs-lookup"><span data-stu-id="f076f-109">Create the custom role</span></span>

<span data-ttu-id="f076f-110">To create a custom role for a resource, follow the steps described in [Create custom roles for Azure Role-Based Access Control](../role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="f076f-110">To create a custom role for a resource, follow the steps described in [Create custom roles for Azure Role-Based Access Control](../role-based-access-control-custom-roles.md).</span></span>

<span data-ttu-id="f076f-111">When you create custom role, include a descriptive name so you can easily remember which built-in role you intended to duplicate.</span><span class="sxs-lookup"><span data-stu-id="f076f-111">When you create custom role, include a descriptive name so you can easily remember which built-in role you intended to duplicate.</span></span>

> [!NOTE]
> <span data-ttu-id="f076f-112">Ensure that the custom role is a duplicate of the built-in role you want to duplicate, and that its scope matches the built-in role.</span><span class="sxs-lookup"><span data-stu-id="f076f-112">Ensure that the custom role is a duplicate of the built-in role you want to duplicate, and that its scope matches the built-in role.</span></span>

## <a name="apply-pim-settings"></a><span data-ttu-id="f076f-113">Apply PIM settings</span><span class="sxs-lookup"><span data-stu-id="f076f-113">Apply PIM settings</span></span>

<span data-ttu-id="f076f-114">After the role is created in your tenant, in the Azure portal, go to the **Privileged Identity Management - Azure resources** pane.</span><span class="sxs-lookup"><span data-stu-id="f076f-114">After the role is created in your tenant, in the Azure portal, go to the **Privileged Identity Management - Azure resources** pane.</span></span> <span data-ttu-id="f076f-115">Select the resource that the role applies to.</span><span class="sxs-lookup"><span data-stu-id="f076f-115">Select the resource that the role applies to.</span></span>

![The "Privileged Identity Management - Azure resources" pane](media/azure-pim-resource-rbac/aadpim_manage_azure_resource_some_there.png)

<span data-ttu-id="f076f-117">[Configure PIM role settings](pim-resource-roles-configure-role-settings.md) that should apply to these members of the role.</span><span class="sxs-lookup"><span data-stu-id="f076f-117">[Configure PIM role settings](pim-resource-roles-configure-role-settings.md) that should apply to these members of the role.</span></span>

<span data-ttu-id="f076f-118">Finally, [assign roles](pim-resource-roles-assign-roles.md) to the distinct group of members that you want to target with these settings.</span><span class="sxs-lookup"><span data-stu-id="f076f-118">Finally, [assign roles](pim-resource-roles-assign-roles.md) to the distinct group of members that you want to target with these settings.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f076f-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="f076f-119">Next steps</span></span>

- [<span data-ttu-id="f076f-120">Configure Azure resource role settings in PIM</span><span class="sxs-lookup"><span data-stu-id="f076f-120">Configure Azure resource role settings in PIM</span></span>](pim-resource-roles-configure-role-settings.md)
- [<span data-ttu-id="f076f-121">Custom roles in Azure</span><span class="sxs-lookup"><span data-stu-id="f076f-121">Custom roles in Azure</span></span>](../../role-based-access-control/custom-roles.md)
