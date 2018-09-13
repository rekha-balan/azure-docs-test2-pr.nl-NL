---
title: Create and Manager Action Groups in Azure Portal | Microsoft Docs
description: ''
author: anirudhcavale
manager: carmonm
editor: ''
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: ''
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: 310ee8e3de58801c285ba97cb406d8ac16bdbf6a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670992"
---
# <a name="create-and-manage-action-groups-in-azure-portal"></a><span data-ttu-id="1fc75-102">Create and Manage Action Groups in Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1fc75-102">Create and Manage Action Groups in Azure Portal</span></span>
## <a name="overview"></a><span data-ttu-id="1fc75-103">Overview</span><span class="sxs-lookup"><span data-stu-id="1fc75-103">Overview</span></span> ##
<span data-ttu-id="1fc75-104">This article shows you how to create and manage action groups in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1fc75-104">This article shows you how to create and manage action groups in the Azure portal.</span></span>

<span data-ttu-id="1fc75-105">Action groups enable you to configure a list of receivers.</span><span class="sxs-lookup"><span data-stu-id="1fc75-105">Action groups enable you to configure a list of receivers.</span></span> <span data-ttu-id="1fc75-106">These groups can then be leveraged when defining activity log alerts; ensuring that a particular action group is notified when the activity log alert is triggered.</span><span class="sxs-lookup"><span data-stu-id="1fc75-106">These groups can then be leveraged when defining activity log alerts; ensuring that a particular action group is notified when the activity log alert is triggered.</span></span>

<span data-ttu-id="1fc75-107">An action group can have up to 10 of each action type.</span><span class="sxs-lookup"><span data-stu-id="1fc75-107">An action group can have up to 10 of each action type.</span></span> <span data-ttu-id="1fc75-108">An action is defined by the combination of:</span><span class="sxs-lookup"><span data-stu-id="1fc75-108">An action is defined by the combination of:</span></span>

<span data-ttu-id="1fc75-109">**Name:** A unique identifier within the action group.</span><span class="sxs-lookup"><span data-stu-id="1fc75-109">**Name:** A unique identifier within the action group.</span></span>  
<span data-ttu-id="1fc75-110">**Action Type:** This defines the action that will be performed.</span><span class="sxs-lookup"><span data-stu-id="1fc75-110">**Action Type:** This defines the action that will be performed.</span></span> <span data-ttu-id="1fc75-111">Options are send SMS, send Email, or call a Webhook.</span><span class="sxs-lookup"><span data-stu-id="1fc75-111">Options are send SMS, send Email, or call a Webhook.</span></span>  
<span data-ttu-id="1fc75-112">**Details:** Based on the action type, the corresponding phone number, email address or webhook URI needs to be provided.</span><span class="sxs-lookup"><span data-stu-id="1fc75-112">**Details:** Based on the action type, the corresponding phone number, email address or webhook URI needs to be provided.</span></span>

<span data-ttu-id="1fc75-113">You can configure and get information about service health notification alerts using:</span><span class="sxs-lookup"><span data-stu-id="1fc75-113">You can configure and get information about service health notification alerts using:</span></span>
* [<span data-ttu-id="1fc75-114">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1fc75-114">Azure Portal</span></span>](monitoring-action-groups.md)
- [<span data-ttu-id="1fc75-115">Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="1fc75-115">Resource Manager templates</span></span>](monitoring-create-action-group-with-resource-manager-template.md)

## <a name="creating-an-action-group-for-the-azure-portal"></a><span data-ttu-id="1fc75-116">Creating an action group for the Azure portal</span><span class="sxs-lookup"><span data-stu-id="1fc75-116">Creating an action group for the Azure portal</span></span> ##
1.  <span data-ttu-id="1fc75-117">In the [portal](https://portal.azure.com), navigate to the **Monitor** service</span><span class="sxs-lookup"><span data-stu-id="1fc75-117">In the [portal](https://portal.azure.com), navigate to the **Monitor** service</span></span>

    ![Monitor](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-action-groups/home-monitor.PNG)
2.  <span data-ttu-id="1fc75-119">Click the **Monitor** option to open up the Monitor blade.</span><span class="sxs-lookup"><span data-stu-id="1fc75-119">Click the **Monitor** option to open up the Monitor blade.</span></span> <span data-ttu-id="1fc75-120">This blade brings together all your monitoring settings and data into one consolidated view.</span><span class="sxs-lookup"><span data-stu-id="1fc75-120">This blade brings together all your monitoring settings and data into one consolidated view.</span></span> <span data-ttu-id="1fc75-121">It first opens to the **Activity log** section.</span><span class="sxs-lookup"><span data-stu-id="1fc75-121">It first opens to the **Activity log** section.</span></span>

3.  <span data-ttu-id="1fc75-122">Now click on **Action groups** section</span><span class="sxs-lookup"><span data-stu-id="1fc75-122">Now click on **Action groups** section</span></span>

    ![Action-Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-action-groups/action-groups-blade.PNG)
4.  <span data-ttu-id="1fc75-124">Click on the **Add** action group command and fill in the fields</span><span class="sxs-lookup"><span data-stu-id="1fc75-124">Click on the **Add** action group command and fill in the fields</span></span>

    ![Add-Action-Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-action-groups/add-action-group.PNG)
5.  <span data-ttu-id="1fc75-126">Provide a **Name** and **Short Name** for the action group; The Short Name will be referenced in notifications sent to this group</span><span class="sxs-lookup"><span data-stu-id="1fc75-126">Provide a **Name** and **Short Name** for the action group; The Short Name will be referenced in notifications sent to this group</span></span>

      ![Action-Group-Define](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-action-groups/action-group-define.PNG)

6.  <span data-ttu-id="1fc75-128">The **Subscription** is the one the Action group will be saved in.</span><span class="sxs-lookup"><span data-stu-id="1fc75-128">The **Subscription** is the one the Action group will be saved in.</span></span> <span data-ttu-id="1fc75-129">It will be auto filled to the subscription you are currently operating under.</span><span class="sxs-lookup"><span data-stu-id="1fc75-129">It will be auto filled to the subscription you are currently operating under.</span></span>

7.  <span data-ttu-id="1fc75-130">Choose the **Resource Group** for this action group.</span><span class="sxs-lookup"><span data-stu-id="1fc75-130">Choose the **Resource Group** for this action group.</span></span>

8.  <span data-ttu-id="1fc75-131">Then, define a list of actions through a combination of:</span><span class="sxs-lookup"><span data-stu-id="1fc75-131">Then, define a list of actions through a combination of:</span></span>
  1. <span data-ttu-id="1fc75-132">**Name:** A unique identifier within the action group.</span><span class="sxs-lookup"><span data-stu-id="1fc75-132">**Name:** A unique identifier within the action group.</span></span>
  2. <span data-ttu-id="1fc75-133">**Action Type:** This defines the action that will be performed.</span><span class="sxs-lookup"><span data-stu-id="1fc75-133">**Action Type:** This defines the action that will be performed.</span></span> <span data-ttu-id="1fc75-134">Options are send SMS, send Email, or call a Webhook.</span><span class="sxs-lookup"><span data-stu-id="1fc75-134">Options are send SMS, send Email, or call a Webhook.</span></span>
  3. <span data-ttu-id="1fc75-135">**Details:** Based on the action type, the corresponding phone number, email address or webhook URI needs to be provided.</span><span class="sxs-lookup"><span data-stu-id="1fc75-135">**Details:** Based on the action type, the corresponding phone number, email address or webhook URI needs to be provided.</span></span>

9.  <span data-ttu-id="1fc75-136">Select **OK** when done to create the action group.</span><span class="sxs-lookup"><span data-stu-id="1fc75-136">Select **OK** when done to create the action group.</span></span>

## <a name="managing-your-action-groups"></a><span data-ttu-id="1fc75-137">Managing your action groups</span><span class="sxs-lookup"><span data-stu-id="1fc75-137">Managing your action groups</span></span> ##
<span data-ttu-id="1fc75-138">Once you have created an action group, it will be visible in the Action groups section of the Monitor service.</span><span class="sxs-lookup"><span data-stu-id="1fc75-138">Once you have created an action group, it will be visible in the Action groups section of the Monitor service.</span></span> <span data-ttu-id="1fc75-139">Select the action group you wish to manage, you will be able to:</span><span class="sxs-lookup"><span data-stu-id="1fc75-139">Select the action group you wish to manage, you will be able to:</span></span>
* <span data-ttu-id="1fc75-140">Add, edit, or remove receivers.</span><span class="sxs-lookup"><span data-stu-id="1fc75-140">Add, edit, or remove receivers.</span></span>
-   <span data-ttu-id="1fc75-141">Delete the action group.</span><span class="sxs-lookup"><span data-stu-id="1fc75-141">Delete the action group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1fc75-142">Next Steps:</span><span class="sxs-lookup"><span data-stu-id="1fc75-142">Next Steps:</span></span> ##
<span data-ttu-id="1fc75-143">Learn more on [SMS alert behavior](monitoring-sms-alert-behavior.md)</span><span class="sxs-lookup"><span data-stu-id="1fc75-143">Learn more on [SMS alert behavior](monitoring-sms-alert-behavior.md)</span></span>  
<span data-ttu-id="1fc75-144">Get an [understanding of the activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md)</span><span class="sxs-lookup"><span data-stu-id="1fc75-144">Get an [understanding of the activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md)</span></span>  
<span data-ttu-id="1fc75-145">Learn more about [rate limiting](monitoring-alerts-rate-limiting.md) on alerts</span><span class="sxs-lookup"><span data-stu-id="1fc75-145">Learn more about [rate limiting](monitoring-alerts-rate-limiting.md) on alerts</span></span>  
<span data-ttu-id="1fc75-146">Get an [overview of activity log alerts](monitoring-overview-alerts.md) and learn how to get alerted</span><span class="sxs-lookup"><span data-stu-id="1fc75-146">Get an [overview of activity log alerts](monitoring-overview-alerts.md) and learn how to get alerted</span></span>  
<span data-ttu-id="1fc75-147">How to [configure alerts whenever a service health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md)</span><span class="sxs-lookup"><span data-stu-id="1fc75-147">How to [configure alerts whenever a service health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md)</span></span>




