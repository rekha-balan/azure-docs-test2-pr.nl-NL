---
title: Discover Azure resources to manage in PIM | Microsoft Docs
description: Learn how to discover Azure resources to manage in Azure AD Privileged Identity Management (PIM).
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
ms.date: 08/30/2018
ms.author: rolyon
ms.openlocfilehash: d9a6ab49d619e487eee6fb13abe128cfc167b560
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870480"
---
# <a name="discover-azure-resources-to-manage-in-pim"></a><span data-ttu-id="9cc16-103">Discover Azure resources to manage in PIM</span><span class="sxs-lookup"><span data-stu-id="9cc16-103">Discover Azure resources to manage in PIM</span></span>

<span data-ttu-id="9cc16-104">Using Azure AD Privileged Identity Management (PIM), you can improve the protection of your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="9cc16-104">Using Azure AD Privileged Identity Management (PIM), you can improve the protection of your Azure resources.</span></span> <span data-ttu-id="9cc16-105">This is helpful to organizations that already use PIM to protect Azure AD directory roles, and to management group and subscription owners who are looking to secure production resources.</span><span class="sxs-lookup"><span data-stu-id="9cc16-105">This is helpful to organizations that already use PIM to protect Azure AD directory roles, and to management group and subscription owners who are looking to secure production resources.</span></span>

<span data-ttu-id="9cc16-106">When you first set up PIM for Azure resources, you need to discover and select the resources to protect with PIM.</span><span class="sxs-lookup"><span data-stu-id="9cc16-106">When you first set up PIM for Azure resources, you need to discover and select the resources to protect with PIM.</span></span> <span data-ttu-id="9cc16-107">There's no limit to the number of resources that you can manage with PIM.</span><span class="sxs-lookup"><span data-stu-id="9cc16-107">There's no limit to the number of resources that you can manage with PIM.</span></span> <span data-ttu-id="9cc16-108">However, we recommend starting with your most critical (production) resources.</span><span class="sxs-lookup"><span data-stu-id="9cc16-108">However, we recommend starting with your most critical (production) resources.</span></span>

## <a name="discover-resources"></a><span data-ttu-id="9cc16-109">Discover resources</span><span class="sxs-lookup"><span data-stu-id="9cc16-109">Discover resources</span></span>

1. <span data-ttu-id="9cc16-110">Sign in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9cc16-110">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>

1. <span data-ttu-id="9cc16-111">Open **Azure AD Privileged Identity Management**.</span><span class="sxs-lookup"><span data-stu-id="9cc16-111">Open **Azure AD Privileged Identity Management**.</span></span>

1. <span data-ttu-id="9cc16-112">Click **Azure resources**.</span><span class="sxs-lookup"><span data-stu-id="9cc16-112">Click **Azure resources**.</span></span>

    <span data-ttu-id="9cc16-113">If this is your first time using PIM for Azure resources, you'll see a Discover resources pane.</span><span class="sxs-lookup"><span data-stu-id="9cc16-113">If this is your first time using PIM for Azure resources, you'll see a Discover resources pane.</span></span>

    ![Discover resources - first time](./media/pim-resource-roles-discover-resources/discover-resources-first-run.png)

    <span data-ttu-id="9cc16-115">If another resource or directory administrator in your organization is already managing Azure resources in PIM, you'll see a list of the resources that are currently being managed.</span><span class="sxs-lookup"><span data-stu-id="9cc16-115">If another resource or directory administrator in your organization is already managing Azure resources in PIM, you'll see a list of the resources that are currently being managed.</span></span>

    ![Discover resources pane](./media/pim-resource-roles-discover-resources/discover-resources.png)

1. <span data-ttu-id="9cc16-117">Click **Discover resources** to launch the discovery experience.</span><span class="sxs-lookup"><span data-stu-id="9cc16-117">Click **Discover resources** to launch the discovery experience.</span></span>

    ![Discovery pane](./media/pim-resource-roles-discover-resources/discovery-pane.png)

1. <span data-ttu-id="9cc16-119">On the Discovery pane, use **Resource state filter** and **Select resource type** to filter the management groups or subscriptions you have write permission to.</span><span class="sxs-lookup"><span data-stu-id="9cc16-119">On the Discovery pane, use **Resource state filter** and **Select resource type** to filter the management groups or subscriptions you have write permission to.</span></span> <span data-ttu-id="9cc16-120">It's probably easiest to start with **All** initially.</span><span class="sxs-lookup"><span data-stu-id="9cc16-120">It's probably easiest to start with **All** initially.</span></span>

    <span data-ttu-id="9cc16-121">You can only search for and select management group or subscription resources to manage using PIM.</span><span class="sxs-lookup"><span data-stu-id="9cc16-121">You can only search for and select management group or subscription resources to manage using PIM.</span></span> <span data-ttu-id="9cc16-122">When you manage a management group or a subscription in PIM, you can also manage its child resources.</span><span class="sxs-lookup"><span data-stu-id="9cc16-122">When you manage a management group or a subscription in PIM, you can also manage its child resources.</span></span>

1. <span data-ttu-id="9cc16-123">Add a checkmark next to any unmanaged resources you want to manage.</span><span class="sxs-lookup"><span data-stu-id="9cc16-123">Add a checkmark next to any unmanaged resources you want to manage.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9cc16-124">Once a management group or subscription is set to managed, it can't be unmanaged.</span><span class="sxs-lookup"><span data-stu-id="9cc16-124">Once a management group or subscription is set to managed, it can't be unmanaged.</span></span> <span data-ttu-id="9cc16-125">This prevents another resource administrator from removing PIM settings.</span><span class="sxs-lookup"><span data-stu-id="9cc16-125">This prevents another resource administrator from removing PIM settings.</span></span>

    ![Discovery - Manage resource](./media/pim-resource-roles-discover-resources/discovery-manage-resource.png)

1. <span data-ttu-id="9cc16-127">Click **Manage resource** to start managing the selected resources.</span><span class="sxs-lookup"><span data-stu-id="9cc16-127">Click **Manage resource** to start managing the selected resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9cc16-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="9cc16-128">Next steps</span></span>

- [<span data-ttu-id="9cc16-129">Configure Azure resource role settings in PIM</span><span class="sxs-lookup"><span data-stu-id="9cc16-129">Configure Azure resource role settings in PIM</span></span>](pim-resource-roles-configure-role-settings.md)
- [<span data-ttu-id="9cc16-130">Assign Azure resource roles in PIM</span><span class="sxs-lookup"><span data-stu-id="9cc16-130">Assign Azure resource roles in PIM</span></span>](pim-resource-roles-assign-roles.md)
