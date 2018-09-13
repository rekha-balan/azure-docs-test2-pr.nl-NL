---
title: Delete an Azure Log Analytics workspace | Microsoft Docs
description: Learn how to delete your Log Analytics workspace if you created one in a personal subscription or restructure your workspace model.
services: log-analytics
documentationcenter: log-analytics
author: mgoedtel
manager: carmonm
editor: ''
ms.assetid: ''
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 05/07/2018
ms.author: magoedte
ms.component: na
ms.openlocfilehash: 54f2af60751ed0d9c64e71efad6fa9aa3ef06589
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869931"
---
# <a name="delete-an-azure-log-analytics-workspace-with-the-azure-portal"></a><span data-ttu-id="57df3-103">Delete an Azure Log Analytics workspace with the Azure portal</span><span class="sxs-lookup"><span data-stu-id="57df3-103">Delete an Azure Log Analytics workspace with the Azure portal</span></span>
<span data-ttu-id="57df3-104">This article shows how to use the Azure portal to delete a Log Analytics workspace that you may no longer require.</span><span class="sxs-lookup"><span data-stu-id="57df3-104">This article shows how to use the Azure portal to delete a Log Analytics workspace that you may no longer require.</span></span> 

## <a name="to-delete-a-workspace"></a><span data-ttu-id="57df3-105">To delete a workspace</span><span class="sxs-lookup"><span data-stu-id="57df3-105">To delete a workspace</span></span> 
<span data-ttu-id="57df3-106">When you delete a Log Analytics workspace, all data related to your workspace is deleted from the service within 30 days.</span><span class="sxs-lookup"><span data-stu-id="57df3-106">When you delete a Log Analytics workspace, all data related to your workspace is deleted from the service within 30 days.</span></span>  <span data-ttu-id="57df3-107">You want to exercise caution when you delete a workspace because there might be important data and configuration that may negatively impact your service operations.</span><span class="sxs-lookup"><span data-stu-id="57df3-107">You want to exercise caution when you delete a workspace because there might be important data and configuration that may negatively impact your service operations.</span></span> <span data-ttu-id="57df3-108">Consider the other Azure services and sources that store its data in Log Analytics, such as:</span><span class="sxs-lookup"><span data-stu-id="57df3-108">Consider the other Azure services and sources that store its data in Log Analytics, such as:</span></span>

* <span data-ttu-id="57df3-109">Application Insights</span><span class="sxs-lookup"><span data-stu-id="57df3-109">Application Insights</span></span>
* <span data-ttu-id="57df3-110">Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="57df3-110">Azure Security Center</span></span>
* <span data-ttu-id="57df3-111">Azure Automation</span><span class="sxs-lookup"><span data-stu-id="57df3-111">Azure Automation</span></span>
* <span data-ttu-id="57df3-112">Agents running on Windows and Linux virtual machines</span><span class="sxs-lookup"><span data-stu-id="57df3-112">Agents running on Windows and Linux virtual machines</span></span>
* <span data-ttu-id="57df3-113">Agents running on Windows and Linux computers in your environment</span><span class="sxs-lookup"><span data-stu-id="57df3-113">Agents running on Windows and Linux computers in your environment</span></span>
* <span data-ttu-id="57df3-114">System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="57df3-114">System Center Operations Manager</span></span>
* <span data-ttu-id="57df3-115">Management solutions</span><span class="sxs-lookup"><span data-stu-id="57df3-115">Management solutions</span></span> 

<span data-ttu-id="57df3-116">Any agents and System Center Operations Manager management groups configured to report to the workspace continue to in an orphaned state.</span><span class="sxs-lookup"><span data-stu-id="57df3-116">Any agents and System Center Operations Manager management groups configured to report to the workspace continue to in an orphaned state.</span></span>  <span data-ttu-id="57df3-117">Inventory what agents, solutions, and other Azure services are integrated with the workspace before you proceed.</span><span class="sxs-lookup"><span data-stu-id="57df3-117">Inventory what agents, solutions, and other Azure services are integrated with the workspace before you proceed.</span></span>   
 
<span data-ttu-id="57df3-118">If you are an administrator and there are multiple users associated with the workspace, the association between those users and the workspace is broken.</span><span class="sxs-lookup"><span data-stu-id="57df3-118">If you are an administrator and there are multiple users associated with the workspace, the association between those users and the workspace is broken.</span></span> <span data-ttu-id="57df3-119">If the users are associated with other workspaces, then they can continue using Log Analytics with those other workspaces.</span><span class="sxs-lookup"><span data-stu-id="57df3-119">If the users are associated with other workspaces, then they can continue using Log Analytics with those other workspaces.</span></span> <span data-ttu-id="57df3-120">However, if they are not associated with other workspaces then they need to create a workspace to use Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="57df3-120">However, if they are not associated with other workspaces then they need to create a workspace to use Log Analytics.</span></span> 

1. <span data-ttu-id="57df3-121">Sign into the [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="57df3-121">Sign into the [Azure portal](http://portal.azure.com).</span></span> 
2. <span data-ttu-id="57df3-122">In the Azure portal, click **More services** found on the lower left-hand corner.</span><span class="sxs-lookup"><span data-stu-id="57df3-122">In the Azure portal, click **More services** found on the lower left-hand corner.</span></span> <span data-ttu-id="57df3-123">In the list of resources, type **Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="57df3-123">In the list of resources, type **Log Analytics**.</span></span> <span data-ttu-id="57df3-124">As you begin typing, the list filters based on your input.</span><span class="sxs-lookup"><span data-stu-id="57df3-124">As you begin typing, the list filters based on your input.</span></span> <span data-ttu-id="57df3-125">Select **Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="57df3-125">Select **Log Analytics**.</span></span>
3. <span data-ttu-id="57df3-126">In the Log Analytics subscriptions pane, select a workspace and then click **Delete**  from the top of the middle pane.</span><span class="sxs-lookup"><span data-stu-id="57df3-126">In the Log Analytics subscriptions pane, select a workspace and then click **Delete**  from the top of the middle pane.</span></span><br><br> <span data-ttu-id="57df3-127">![Delete option from Workspace properties pane](media/log-analytics-manage-del-workspace/log-analytics-delete-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="57df3-127">![Delete option from Workspace properties pane](media/log-analytics-manage-del-workspace/log-analytics-delete-workspace.png)</span></span><br>  
4. <span data-ttu-id="57df3-128">When the confirmation message window appears asking you to confirm deletion of the workspace, click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="57df3-128">When the confirmation message window appears asking you to confirm deletion of the workspace, click **Yes**.</span></span><br><br> <span data-ttu-id="57df3-129">![Confirm deletion of workspace](media/log-analytics-manage-del-workspace/log-analytics-delete-workspace-confirm.png)</span><span class="sxs-lookup"><span data-stu-id="57df3-129">![Confirm deletion of workspace](media/log-analytics-manage-del-workspace/log-analytics-delete-workspace-confirm.png)</span></span>

