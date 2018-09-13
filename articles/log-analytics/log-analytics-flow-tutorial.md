---
title: Automate Azure Log Analytics processes with Microsoft Flow
description: Learn how you can use Microsoft Flow to quickly automate repeatable processes by using the Azure Log Analytics connector.
services: log-analytics
documentationcenter: ''
author: mgoedtel
manager: carmonm
ms.service: log-analytics
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 09/29/2017
ms.author: bwren
ms.component: na
ms.openlocfilehash: d623cd4cb1a62fab7b5f8cc4e9686d88cde94ed8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864968"
---
# <a name="automate-log-analytics-processes-with-the-connector-for-microsoft-flow"></a><span data-ttu-id="6da50-103">Automate Log Analytics processes with the connector for Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="6da50-103">Automate Log Analytics processes with the connector for Microsoft Flow</span></span>
<span data-ttu-id="6da50-104">[Microsoft Flow](https://ms.flow.microsoft.com) allows you to create automated workflows using hundreds of actions for a variety of services.</span><span class="sxs-lookup"><span data-stu-id="6da50-104">[Microsoft Flow](https://ms.flow.microsoft.com) allows you to create automated workflows using hundreds of actions for a variety of services.</span></span> <span data-ttu-id="6da50-105">Output from one action can be used as input to another allowing you to create integration between different services.</span><span class="sxs-lookup"><span data-stu-id="6da50-105">Output from one action can be used as input to another allowing you to create integration between different services.</span></span>  <span data-ttu-id="6da50-106">The Azure Log Analytics connector for Microsoft Flow allow you to build workflows that include data retrieved by log searches in Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="6da50-106">The Azure Log Analytics connector for Microsoft Flow allow you to build workflows that include data retrieved by log searches in Log Analytics.</span></span>

<span data-ttu-id="6da50-107">For example, you can use Microsoft Flow to use Log Analytics data in an email notification from Office 365, create a bug in Azure DevOps, or post a Slack message.</span><span class="sxs-lookup"><span data-stu-id="6da50-107">For example, you can use Microsoft Flow to use Log Analytics data in an email notification from Office 365, create a bug in Azure DevOps, or post a Slack message.</span></span>  <span data-ttu-id="6da50-108">You can trigger a workflow by a simple schedule or from some action in a connected service such as when a mail or a tweet is received.</span><span class="sxs-lookup"><span data-stu-id="6da50-108">You can trigger a workflow by a simple schedule or from some action in a connected service such as when a mail or a tweet is received.</span></span>  

<span data-ttu-id="6da50-109">The tutorial in this article shows you how to create a flow that automatically sends the results of a Log Analytics log search by email, just one example of how you can use Log Analytics in Microsoft Flow.</span><span class="sxs-lookup"><span data-stu-id="6da50-109">The tutorial in this article shows you how to create a flow that automatically sends the results of a Log Analytics log search by email, just one example of how you can use Log Analytics in Microsoft Flow.</span></span> 


## <a name="step-1-create-a-flow"></a><span data-ttu-id="6da50-110">Step 1: Create a flow</span><span class="sxs-lookup"><span data-stu-id="6da50-110">Step 1: Create a flow</span></span>
1. <span data-ttu-id="6da50-111">Sign in to [Microsoft Flow](http://flow.microsoft.com), and select **My Flows**.</span><span class="sxs-lookup"><span data-stu-id="6da50-111">Sign in to [Microsoft Flow](http://flow.microsoft.com), and select **My Flows**.</span></span>
2. <span data-ttu-id="6da50-112">Click **+ Create from blank**.</span><span class="sxs-lookup"><span data-stu-id="6da50-112">Click **+ Create from blank**.</span></span>

## <a name="step-2-create-a-trigger-for-your-flow"></a><span data-ttu-id="6da50-113">Step 2: Create a trigger for your flow</span><span class="sxs-lookup"><span data-stu-id="6da50-113">Step 2: Create a trigger for your flow</span></span>
1. <span data-ttu-id="6da50-114">Click **Search hundreds of connectors and triggers**.</span><span class="sxs-lookup"><span data-stu-id="6da50-114">Click **Search hundreds of connectors and triggers**.</span></span>
2. <span data-ttu-id="6da50-115">Type **Schedule** in the search box.</span><span class="sxs-lookup"><span data-stu-id="6da50-115">Type **Schedule** in the search box.</span></span>
3. <span data-ttu-id="6da50-116">Select **Schedule**, and then select **Schedule - Recurrence**.</span><span class="sxs-lookup"><span data-stu-id="6da50-116">Select **Schedule**, and then select **Schedule - Recurrence**.</span></span>
4. <span data-ttu-id="6da50-117">In the **Frequency** box select **Day** and in the **Interval** box, enter **1**.</span><span class="sxs-lookup"><span data-stu-id="6da50-117">In the **Frequency** box select **Day** and in the **Interval** box, enter **1**.</span></span><br><br><span data-ttu-id="6da50-118">![Microsoft Flow trigger dialog box](media/log-analytics-flow-tutorial/flow01.png)</span><span class="sxs-lookup"><span data-stu-id="6da50-118">![Microsoft Flow trigger dialog box](media/log-analytics-flow-tutorial/flow01.png)</span></span>


## <a name="step-3-add-a-log-analytics-action"></a><span data-ttu-id="6da50-119">Step 3: Add a Log Analytics action</span><span class="sxs-lookup"><span data-stu-id="6da50-119">Step 3: Add a Log Analytics action</span></span>
1. <span data-ttu-id="6da50-120">Click **+ New step**, and then click **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="6da50-120">Click **+ New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="6da50-121">Search for **Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="6da50-121">Search for **Log Analytics**.</span></span>
3. <span data-ttu-id="6da50-122">Click **Azure Log Analytics – Run query and visualize results**.</span><span class="sxs-lookup"><span data-stu-id="6da50-122">Click **Azure Log Analytics – Run query and visualize results**.</span></span><br><br><span data-ttu-id="6da50-123">![Log Analytics run query window](media/log-analytics-flow-tutorial/flow02.png)</span><span class="sxs-lookup"><span data-stu-id="6da50-123">![Log Analytics run query window](media/log-analytics-flow-tutorial/flow02.png)</span></span>

## <a name="step-4-configure-the-log-analytics-action"></a><span data-ttu-id="6da50-124">Step 4: Configure the Log Analytics action</span><span class="sxs-lookup"><span data-stu-id="6da50-124">Step 4: Configure the Log Analytics action</span></span>

1. <span data-ttu-id="6da50-125">Specify the details for your workspace including the Subscription ID, Resource Group, and Workspace Name.</span><span class="sxs-lookup"><span data-stu-id="6da50-125">Specify the details for your workspace including the Subscription ID, Resource Group, and Workspace Name.</span></span>
2. <span data-ttu-id="6da50-126">Add the following Log Analytics query to the **Query** window.</span><span class="sxs-lookup"><span data-stu-id="6da50-126">Add the following Log Analytics query to the **Query** window.</span></span>  <span data-ttu-id="6da50-127">This is only a sample query, and you can replace with any other that returns data.</span><span class="sxs-lookup"><span data-stu-id="6da50-127">This is only a sample query, and you can replace with any other that returns data.</span></span>
```
    Event
    | where EventLevelName == "Error" 
    | where TimeGenerated > ago(1day)
    | summarize count() by Computer
    | sort by Computer
```

2. <span data-ttu-id="6da50-128">Select **HTML Table** for the **Chart Type**.</span><span class="sxs-lookup"><span data-stu-id="6da50-128">Select **HTML Table** for the **Chart Type**.</span></span><br><br><span data-ttu-id="6da50-129">![Log Analytics action](media/log-analytics-flow-tutorial/flow03.png)</span><span class="sxs-lookup"><span data-stu-id="6da50-129">![Log Analytics action](media/log-analytics-flow-tutorial/flow03.png)</span></span>

## <a name="step-5-configure-the-flow-to-send-email"></a><span data-ttu-id="6da50-130">Step 5: Configure the flow to send email</span><span class="sxs-lookup"><span data-stu-id="6da50-130">Step 5: Configure the flow to send email</span></span>

1. <span data-ttu-id="6da50-131">Click **New step**, and then click **+ Add an action**.</span><span class="sxs-lookup"><span data-stu-id="6da50-131">Click **New step**, and then click **+ Add an action**.</span></span>
2. <span data-ttu-id="6da50-132">Search for **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="6da50-132">Search for **Office 365 Outlook**.</span></span>
3. <span data-ttu-id="6da50-133">Click **Office 365 Outlook – Send an email**.</span><span class="sxs-lookup"><span data-stu-id="6da50-133">Click **Office 365 Outlook – Send an email**.</span></span><br><br><span data-ttu-id="6da50-134">![Office 365 Outlook selection window](media/log-analytics-flow-tutorial/flow04.png)</span><span class="sxs-lookup"><span data-stu-id="6da50-134">![Office 365 Outlook selection window](media/log-analytics-flow-tutorial/flow04.png)</span></span>

4. <span data-ttu-id="6da50-135">Specify the email address of a recipient in the **To** window and a subject for the email in **Subject**.</span><span class="sxs-lookup"><span data-stu-id="6da50-135">Specify the email address of a recipient in the **To** window and a subject for the email in **Subject**.</span></span>
5. <span data-ttu-id="6da50-136">Click anywhere in the **Body** box.</span><span class="sxs-lookup"><span data-stu-id="6da50-136">Click anywhere in the **Body** box.</span></span>  <span data-ttu-id="6da50-137">A **Dynamic content** window opens with values from previous actions.</span><span class="sxs-lookup"><span data-stu-id="6da50-137">A **Dynamic content** window opens with values from previous actions.</span></span>  
6. <span data-ttu-id="6da50-138">Select **Body**.</span><span class="sxs-lookup"><span data-stu-id="6da50-138">Select **Body**.</span></span>  <span data-ttu-id="6da50-139">This is the results of the query in the Log Analytics action.</span><span class="sxs-lookup"><span data-stu-id="6da50-139">This is the results of the query in the Log Analytics action.</span></span>
6. <span data-ttu-id="6da50-140">Click **Show advanced options**.</span><span class="sxs-lookup"><span data-stu-id="6da50-140">Click **Show advanced options**.</span></span>
7. <span data-ttu-id="6da50-141">In the **Is HTML** box, select **Yes**.</span><span class="sxs-lookup"><span data-stu-id="6da50-141">In the **Is HTML** box, select **Yes**.</span></span><br><br><span data-ttu-id="6da50-142">![Office 365 email configuration window](media/log-analytics-flow-tutorial/flow05.png)</span><span class="sxs-lookup"><span data-stu-id="6da50-142">![Office 365 email configuration window](media/log-analytics-flow-tutorial/flow05.png)</span></span>

## <a name="step-6-save-and-test-your-flow"></a><span data-ttu-id="6da50-143">Step 6: Save and test your flow</span><span class="sxs-lookup"><span data-stu-id="6da50-143">Step 6: Save and test your flow</span></span>
1. <span data-ttu-id="6da50-144">In the **Flow name** box, add a name for your flow, and then click **Create flow**.</span><span class="sxs-lookup"><span data-stu-id="6da50-144">In the **Flow name** box, add a name for your flow, and then click **Create flow**.</span></span><br><br><span data-ttu-id="6da50-145">![Save flow](media/log-analytics-flow-tutorial/flow06.png)</span><span class="sxs-lookup"><span data-stu-id="6da50-145">![Save flow](media/log-analytics-flow-tutorial/flow06.png)</span></span>
2. <span data-ttu-id="6da50-146">The flow is now created and will run after a day which is the schedule you specified.</span><span class="sxs-lookup"><span data-stu-id="6da50-146">The flow is now created and will run after a day which is the schedule you specified.</span></span> 
3. <span data-ttu-id="6da50-147">To immediately test the flow, click **Run Now** and then **Run flow**.</span><span class="sxs-lookup"><span data-stu-id="6da50-147">To immediately test the flow, click **Run Now** and then **Run flow**.</span></span><br><br><span data-ttu-id="6da50-148">![Run flow](media/log-analytics-flow-tutorial/flow07.png)</span><span class="sxs-lookup"><span data-stu-id="6da50-148">![Run flow](media/log-analytics-flow-tutorial/flow07.png)</span></span>
3. <span data-ttu-id="6da50-149">When the flow completes, check the mail of the recipient that you specified.</span><span class="sxs-lookup"><span data-stu-id="6da50-149">When the flow completes, check the mail of the recipient that you specified.</span></span>  <span data-ttu-id="6da50-150">You should have received a mail with a body similar to the following:</span><span class="sxs-lookup"><span data-stu-id="6da50-150">You should have received a mail with a body similar to the following:</span></span><br><br>![Sample email](media/log-analytics-flow-tutorial/flow08.png)


## <a name="next-steps"></a><span data-ttu-id="6da50-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="6da50-152">Next steps</span></span>

- <span data-ttu-id="6da50-153">Learn more about [log searches in Log Analytics](log-analytics-log-search-new.md).</span><span class="sxs-lookup"><span data-stu-id="6da50-153">Learn more about [log searches in Log Analytics](log-analytics-log-search-new.md).</span></span>
- <span data-ttu-id="6da50-154">Learn more about [Microsoft Flow](https://ms.flow.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="6da50-154">Learn more about [Microsoft Flow](https://ms.flow.microsoft.com).</span></span>



