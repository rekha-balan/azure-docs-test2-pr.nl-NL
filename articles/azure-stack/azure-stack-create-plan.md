---
title: Create a plan in Azure Stack | Microsoft Docs
description: As a service administrator, create a plan that lets subscribers provision virtual machines.
services: azure-stack
documentationcenter: ''
author: ErikjeMS
manager: byronr
editor: ''
ms.assetid: 3dc92e5c-c004-49db-9a94-783f1f798b98
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 3/1/2017
ms.author: erikje
ms.openlocfilehash: 3dbc39550b0f8a76303e57d485f0c29b50f7f689
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552846"
---
# <a name="create-a-plan-in-azure-stack"></a><span data-ttu-id="80fc7-103">Create a plan in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="80fc7-103">Create a plan in Azure Stack</span></span>
<span data-ttu-id="80fc7-104">[Plans](azure-stack-key-features.md) are groupings of one or more services.</span><span class="sxs-lookup"><span data-stu-id="80fc7-104">[Plans](azure-stack-key-features.md) are groupings of one or more services.</span></span> <span data-ttu-id="80fc7-105">As a provider, you can create plans to offer to your tenants.</span><span class="sxs-lookup"><span data-stu-id="80fc7-105">As a provider, you can create plans to offer to your tenants.</span></span> <span data-ttu-id="80fc7-106">In turn, your tenants subscribe to your offers to use the plans and services they include.</span><span class="sxs-lookup"><span data-stu-id="80fc7-106">In turn, your tenants subscribe to your offers to use the plans and services they include.</span></span> <span data-ttu-id="80fc7-107">This example shows you how to create a plan that includes the compute, network, and storage resource providers.</span><span class="sxs-lookup"><span data-stu-id="80fc7-107">This example shows you how to create a plan that includes the compute, network, and storage resource providers.</span></span> <span data-ttu-id="80fc7-108">This plan gives subscribers the ability to provision virtual machines.</span><span class="sxs-lookup"><span data-stu-id="80fc7-108">This plan gives subscribers the ability to provision virtual machines.</span></span>

1. <span data-ttu-id="80fc7-109">In an internet browser, navigate to https://adminportal.local.azurestack.external.</span><span class="sxs-lookup"><span data-stu-id="80fc7-109">In an internet browser, navigate to https://adminportal.local.azurestack.external.</span></span>
2. <span data-ttu-id="80fc7-110">[Sign in](azure-stack-connect-azure-stack.md) to the Azure Stack Portal as a service administrator.</span><span class="sxs-lookup"><span data-stu-id="80fc7-110">[Sign in](azure-stack-connect-azure-stack.md) to the Azure Stack Portal as a service administrator.</span></span> <span data-ttu-id="80fc7-111">Enter the credentials for the account that you created during step 5 of the [Run the PowerShell script](azure-stack-run-powershell-script.md) section.</span><span class="sxs-lookup"><span data-stu-id="80fc7-111">Enter the credentials for the account that you created during step 5 of the [Run the PowerShell script](azure-stack-run-powershell-script.md) section.</span></span>

   <span data-ttu-id="80fc7-112">Service administrators can create offers and plans, and manage users.</span><span class="sxs-lookup"><span data-stu-id="80fc7-112">Service administrators can create offers and plans, and manage users.</span></span>
3. <span data-ttu-id="80fc7-113">To create a plan and offer that tenants can subscribe to, click **New** > **Tenant Offers + Plans** > **Plan**.</span><span class="sxs-lookup"><span data-stu-id="80fc7-113">To create a plan and offer that tenants can subscribe to, click **New** > **Tenant Offers + Plans** > **Plan**.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-create-plan/image01.png)
4. <span data-ttu-id="80fc7-114">In the **New Plan** blade, fill in **Display Name** and **Resource Name**.</span><span class="sxs-lookup"><span data-stu-id="80fc7-114">In the **New Plan** blade, fill in **Display Name** and **Resource Name**.</span></span> <span data-ttu-id="80fc7-115">The Display Name is the plan's friendly name that tenants see.</span><span class="sxs-lookup"><span data-stu-id="80fc7-115">The Display Name is the plan's friendly name that tenants see.</span></span> <span data-ttu-id="80fc7-116">Only the admin can see the Resource Name.</span><span class="sxs-lookup"><span data-stu-id="80fc7-116">Only the admin can see the Resource Name.</span></span> <span data-ttu-id="80fc7-117">It's the name that admins use to work with the plan as an Azure Resource Manager resource.</span><span class="sxs-lookup"><span data-stu-id="80fc7-117">It's the name that admins use to work with the plan as an Azure Resource Manager resource.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-create-plan/image02.png)
5. <span data-ttu-id="80fc7-118">Create a new **Resource Group**, or select an existing one, as a container for the plan.</span><span class="sxs-lookup"><span data-stu-id="80fc7-118">Create a new **Resource Group**, or select an existing one, as a container for the plan.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-create-plan/image02a.png)
6. <span data-ttu-id="80fc7-119">Click **Services**, select **Microsoft.Compute**, **Microsoft.Network**, and **Microsoft.Storage**, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="80fc7-119">Click **Services**, select **Microsoft.Compute**, **Microsoft.Network**, and **Microsoft.Storage**, and then click **Select**.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-create-plan/image03.png)
7. <span data-ttu-id="80fc7-120">Click **Quotas**, click **Microsoft.Storage (local)**, and then either select the default quota or click **Create new quota** to customize the quota.</span><span class="sxs-lookup"><span data-stu-id="80fc7-120">Click **Quotas**, click **Microsoft.Storage (local)**, and then either select the default quota or click **Create new quota** to customize the quota.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-create-plan/image04.png)
8. <span data-ttu-id="80fc7-121">Type a name for the quota, click **Quota Settings**, set the quota values and click **OK**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="80fc7-121">Type a name for the quota, click **Quota Settings**, set the quota values and click **OK**, and then click **OK**.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-create-plan/image06.png)
9. <span data-ttu-id="80fc7-122">Click **Microsoft.Network (local)**, and then either select the default quota or click **Create new quota** to customize the quota.</span><span class="sxs-lookup"><span data-stu-id="80fc7-122">Click **Microsoft.Network (local)**, and then either select the default quota or click **Create new quota** to customize the quota.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-create-plan/image07.png)
10. <span data-ttu-id="80fc7-123">Type a name for the quota, click **Quota Settings**, set the quota values and click **OK**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="80fc7-123">Type a name for the quota, click **Quota Settings**, set the quota values and click **OK**, and then click **OK**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-create-plan/image08.png)
11. <span data-ttu-id="80fc7-124">Click **Microsoft.Compute (local)**, and then either select the default quota or click **Create new quota** to customize the quota.</span><span class="sxs-lookup"><span data-stu-id="80fc7-124">Click **Microsoft.Compute (local)**, and then either select the default quota or click **Create new quota** to customize the quota.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-create-plan/image09.png)
12. <span data-ttu-id="80fc7-125">Type a name for the quota, click **Quota Settings**, set the quota values and click **OK**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="80fc7-125">Type a name for the quota, click **Quota Settings**, set the quota values and click **OK**, and then click **OK**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-create-plan/image10.png)
13. <span data-ttu-id="80fc7-126">In the **Quotas** blade, click **OK**, and then in the **New Plan** blade, click **Create** to create the plan.</span><span class="sxs-lookup"><span data-stu-id="80fc7-126">In the **Quotas** blade, click **OK**, and then in the **New Plan** blade, click **Create** to create the plan.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-create-plan/image11.png)
14. <span data-ttu-id="80fc7-127">To see your new plan, click **All resources**, then search for the plan and click its name.</span><span class="sxs-lookup"><span data-stu-id="80fc7-127">To see your new plan, click **All resources**, then search for the plan and click its name.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-create-plan/image12.png)

## <a name="next-steps"></a><span data-ttu-id="80fc7-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="80fc7-128">Next steps</span></span>
[<span data-ttu-id="80fc7-129">Create an offer</span><span class="sxs-lookup"><span data-stu-id="80fc7-129">Create an offer</span></span>](azure-stack-create-offer.md)












