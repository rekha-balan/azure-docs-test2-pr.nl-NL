---
title: Automate Azure Application Insights processes with Microsoft Flow
description: Learn how you can use Microsoft Flow to quickly automate repeatable processes by using the Application Insights connector.
services: application-insights
documentationcenter: ''
author: mrbullwinkle
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: conceptual
ms.date: 06/25/2017
ms.author: mbullwin
ms.openlocfilehash: 449a6274b67f3eb72ea6d8bd19f555fc59158d7e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868539"
---
# <a name="automate-azure-application-insights-processes-with-the-connector-for-microsoft-flow"></a><span data-ttu-id="fa460-103">Automate Azure Application Insights processes with the connector for Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="fa460-103">Automate Azure Application Insights processes with the connector for Microsoft Flow</span></span>

<span data-ttu-id="fa460-104">Do you find yourself repeatedly running the same queries on your telemetry data to check that your service is functioning properly?</span><span class="sxs-lookup"><span data-stu-id="fa460-104">Do you find yourself repeatedly running the same queries on your telemetry data to check that your service is functioning properly?</span></span> <span data-ttu-id="fa460-105">Are you looking to automate these queries for finding trends and anomalies and then build your own workflows around them?</span><span class="sxs-lookup"><span data-stu-id="fa460-105">Are you looking to automate these queries for finding trends and anomalies and then build your own workflows around them?</span></span> <span data-ttu-id="fa460-106">The Azure Application Insights connector (preview) for Microsoft Flow is the right tool for these purposes.</span><span class="sxs-lookup"><span data-stu-id="fa460-106">The Azure Application Insights connector (preview) for Microsoft Flow is the right tool for these purposes.</span></span>

<span data-ttu-id="fa460-107">With this integration, you can now automate numerous processes without writing a single line of code.</span><span class="sxs-lookup"><span data-stu-id="fa460-107">With this integration, you can now automate numerous processes without writing a single line of code.</span></span> <span data-ttu-id="fa460-108">After you create a flow by using an Application Insights action, the flow automatically runs your Application Insights Analytics query.</span><span class="sxs-lookup"><span data-stu-id="fa460-108">After you create a flow by using an Application Insights action, the flow automatically runs your Application Insights Analytics query.</span></span> 

<span data-ttu-id="fa460-109">You can add additional actions as well.</span><span class="sxs-lookup"><span data-stu-id="fa460-109">You can add additional actions as well.</span></span> <span data-ttu-id="fa460-110">Microsoft Flow makes hundreds of actions available.</span><span class="sxs-lookup"><span data-stu-id="fa460-110">Microsoft Flow makes hundreds of actions available.</span></span> <span data-ttu-id="fa460-111">For example, you can use Microsoft Flow to automatically send an email notification or create a bug in Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="fa460-111">For example, you can use Microsoft Flow to automatically send an email notification or create a bug in Azure DevOps.</span></span> <span data-ttu-id="fa460-112">You can also use one of the many [templates](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) that are available for the connector for Microsoft Flow.</span><span class="sxs-lookup"><span data-stu-id="fa460-112">You can also use one of the many [templates](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) that are available for the connector for Microsoft Flow.</span></span> <span data-ttu-id="fa460-113">These templates speed up the process of creating a flow.</span><span class="sxs-lookup"><span data-stu-id="fa460-113">These templates speed up the process of creating a flow.</span></span> 

<!--The Application Insights connector also works with [Azure Power Apps](https://powerapps.microsoft.com/en-us/) and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/?v=17.23h). --> 

## <a name="create-a-flow-for-application-insights"></a><span data-ttu-id="fa460-114">Create a flow for Application Insights</span><span class="sxs-lookup"><span data-stu-id="fa460-114">Create a flow for Application Insights</span></span>

<span data-ttu-id="fa460-115">In this tutorial, you will learn how to create a flow that uses the Analytics auto-cluster algorithm to group attributes in the data for a web application.</span><span class="sxs-lookup"><span data-stu-id="fa460-115">In this tutorial, you will learn how to create a flow that uses the Analytics auto-cluster algorithm to group attributes in the data for a web application.</span></span> <span data-ttu-id="fa460-116">The flow automatically sends the results by email, just one example of how you can use Microsoft Flow and Application Insights Analytics together.</span><span class="sxs-lookup"><span data-stu-id="fa460-116">The flow automatically sends the results by email, just one example of how you can use Microsoft Flow and Application Insights Analytics together.</span></span> 

### <a name="step-1-create-a-flow"></a><span data-ttu-id="fa460-117">Step 1: Create a flow</span><span class="sxs-lookup"><span data-stu-id="fa460-117">Step 1: Create a flow</span></span>
1. <span data-ttu-id="fa460-118">Sign in to [Microsoft Flow](http://flow.microsoft.com), and then select **My Flows**.</span><span class="sxs-lookup"><span data-stu-id="fa460-118">Sign in to [Microsoft Flow](http://flow.microsoft.com), and then select **My Flows**.</span></span>
1. <span data-ttu-id="fa460-119">Click **Create a flow from blank**.</span><span class="sxs-lookup"><span data-stu-id="fa460-119">Click **Create a flow from blank**.</span></span>

### <a name="step-2-create-a-trigger-for-your-flow"></a><span data-ttu-id="fa460-120">Step 2: Create a trigger for your flow</span><span class="sxs-lookup"><span data-stu-id="fa460-120">Step 2: Create a trigger for your flow</span></span>
1. <span data-ttu-id="fa460-121">Select **Schedule**, and then select **Schedule - Recurrence**.</span><span class="sxs-lookup"><span data-stu-id="fa460-121">Select **Schedule**, and then select **Schedule - Recurrence**.</span></span>
1. <span data-ttu-id="fa460-122">In the **Frequency** box, select **Day**, and in the **Interval** box, enter **1**.</span><span class="sxs-lookup"><span data-stu-id="fa460-122">In the **Frequency** box, select **Day**, and in the **Interval** box, enter **1**.</span></span>

    ![Microsoft Flow trigger dialog box](./media/app-insights-automate-with-flow/flow1.png)


### <a name="step-3-add-an-application-insights-action"></a><span data-ttu-id="fa460-124">Step 3: Add an Application Insights action</span><span class="sxs-lookup"><span data-stu-id="fa460-124">Step 3: Add an Application Insights action</span></span>
1. <span data-ttu-id="fa460-125">Click **New step**, and then click **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="fa460-125">Click **New step**, and then click **Add an action**.</span></span>
1. <span data-ttu-id="fa460-126">Search for **Azure Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="fa460-126">Search for **Azure Application Insights**.</span></span>
1. <span data-ttu-id="fa460-127">Click **Azure Application Insights – Visualize Analytics query Preview**.</span><span class="sxs-lookup"><span data-stu-id="fa460-127">Click **Azure Application Insights – Visualize Analytics query Preview**.</span></span>

    ![Run Analytics query window](./media/app-insights-automate-with-flow/flow2.png)

### <a name="step-4-connect-to-an-application-insights-resource"></a><span data-ttu-id="fa460-129">Step 4: Connect to an Application Insights resource</span><span class="sxs-lookup"><span data-stu-id="fa460-129">Step 4: Connect to an Application Insights resource</span></span>

<span data-ttu-id="fa460-130">To complete this step, you need an application ID and an API key for your resource.</span><span class="sxs-lookup"><span data-stu-id="fa460-130">To complete this step, you need an application ID and an API key for your resource.</span></span> <span data-ttu-id="fa460-131">You can retrieve them from the Azure portal, as shown in the following diagram:</span><span class="sxs-lookup"><span data-stu-id="fa460-131">You can retrieve them from the Azure portal, as shown in the following diagram:</span></span>

![Application ID in the Azure portal](./media/app-insights-automate-with-flow/appid.png) 

- <span data-ttu-id="fa460-133">Provide a name for your connection, along with the application ID and API key.</span><span class="sxs-lookup"><span data-stu-id="fa460-133">Provide a name for your connection, along with the application ID and API key.</span></span>

    ![Microsoft Flow connection window](./media/app-insights-automate-with-flow/flow3.png)

### <a name="step-5-specify-the-analytics-query-and-chart-type"></a><span data-ttu-id="fa460-135">Step 5: Specify the Analytics query and chart type</span><span class="sxs-lookup"><span data-stu-id="fa460-135">Step 5: Specify the Analytics query and chart type</span></span>
<span data-ttu-id="fa460-136">This example query selects the failed requests within the last day and correlates them with exceptions that occurred as part of the operation.</span><span class="sxs-lookup"><span data-stu-id="fa460-136">This example query selects the failed requests within the last day and correlates them with exceptions that occurred as part of the operation.</span></span> <span data-ttu-id="fa460-137">Analytics correlates them based on the operation_Id identifier.</span><span class="sxs-lookup"><span data-stu-id="fa460-137">Analytics correlates them based on the operation_Id identifier.</span></span> <span data-ttu-id="fa460-138">The query then segments the results by using the autocluster algorithm.</span><span class="sxs-lookup"><span data-stu-id="fa460-138">The query then segments the results by using the autocluster algorithm.</span></span> 

<span data-ttu-id="fa460-139">When you create your own queries, verify that they are working properly in Analytics before you add it to your flow.</span><span class="sxs-lookup"><span data-stu-id="fa460-139">When you create your own queries, verify that they are working properly in Analytics before you add it to your flow.</span></span>

- <span data-ttu-id="fa460-140">Add the following Analytics query, and then select the HTML table chart type.</span><span class="sxs-lookup"><span data-stu-id="fa460-140">Add the following Analytics query, and then select the HTML table chart type.</span></span> 

    ```
    requests
    | where timestamp > ago(1d)
    | where success == "False"
    | project name, operation_Id
    | join ( exceptions
        | project problemId, outerMessage, operation_Id
    ) on operation_Id
    | evaluate autocluster()
    ```
    
    ![Analytics query configuration window](./media/app-insights-automate-with-flow/flow4.png)

### <a name="step-6-configure-the-flow-to-send-email"></a><span data-ttu-id="fa460-142">Step 6: Configure the flow to send email</span><span class="sxs-lookup"><span data-stu-id="fa460-142">Step 6: Configure the flow to send email</span></span>

1. <span data-ttu-id="fa460-143">Click **New step**, and then click **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="fa460-143">Click **New step**, and then click **Add an action**.</span></span>
1. <span data-ttu-id="fa460-144">Search for **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="fa460-144">Search for **Office 365 Outlook**.</span></span>
1. <span data-ttu-id="fa460-145">Click **Office 365 Outlook – Send an email**.</span><span class="sxs-lookup"><span data-stu-id="fa460-145">Click **Office 365 Outlook – Send an email**.</span></span>

    ![Office 365 Outlook selection window](./media/app-insights-automate-with-flow/flow2b.png)

1. <span data-ttu-id="fa460-147">In the **Send an email** window, do the following:</span><span class="sxs-lookup"><span data-stu-id="fa460-147">In the **Send an email** window, do the following:</span></span>

   <span data-ttu-id="fa460-148">a.</span><span class="sxs-lookup"><span data-stu-id="fa460-148">a.</span></span> <span data-ttu-id="fa460-149">Type the email address of the recipient.</span><span class="sxs-lookup"><span data-stu-id="fa460-149">Type the email address of the recipient.</span></span>

   <span data-ttu-id="fa460-150">b.</span><span class="sxs-lookup"><span data-stu-id="fa460-150">b.</span></span> <span data-ttu-id="fa460-151">Type a subject for the email.</span><span class="sxs-lookup"><span data-stu-id="fa460-151">Type a subject for the email.</span></span>

   <span data-ttu-id="fa460-152">c.</span><span class="sxs-lookup"><span data-stu-id="fa460-152">c.</span></span> <span data-ttu-id="fa460-153">Click anywhere in the **Body** box and then, on the dynamic content menu that opens at the right, select **Body**.</span><span class="sxs-lookup"><span data-stu-id="fa460-153">Click anywhere in the **Body** box and then, on the dynamic content menu that opens at the right, select **Body**.</span></span>

   <span data-ttu-id="fa460-154">d.</span><span class="sxs-lookup"><span data-stu-id="fa460-154">d.</span></span> <span data-ttu-id="fa460-155">Click **Show advanced options**.</span><span class="sxs-lookup"><span data-stu-id="fa460-155">Click **Show advanced options**.</span></span>

    ![Office 365 Outlook configuration](./media/app-insights-automate-with-flow/flow5.png)

1. <span data-ttu-id="fa460-157">On the dynamic content menu, do the following:</span><span class="sxs-lookup"><span data-stu-id="fa460-157">On the dynamic content menu, do the following:</span></span>

    <span data-ttu-id="fa460-158">a.</span><span class="sxs-lookup"><span data-stu-id="fa460-158">a.</span></span> <span data-ttu-id="fa460-159">Select **Attachment Name**.</span><span class="sxs-lookup"><span data-stu-id="fa460-159">Select **Attachment Name**.</span></span>

    <span data-ttu-id="fa460-160">b.</span><span class="sxs-lookup"><span data-stu-id="fa460-160">b.</span></span> <span data-ttu-id="fa460-161">Select **Attachment Content**.</span><span class="sxs-lookup"><span data-stu-id="fa460-161">Select **Attachment Content**.</span></span>
    
    <span data-ttu-id="fa460-162">c.</span><span class="sxs-lookup"><span data-stu-id="fa460-162">c.</span></span> <span data-ttu-id="fa460-163">In the **Is HTML** box, select **Yes**.</span><span class="sxs-lookup"><span data-stu-id="fa460-163">In the **Is HTML** box, select **Yes**.</span></span>

    ![Office 365 email configuration window](./media/app-insights-automate-with-flow/flow7.png)

### <a name="step-7-save-and-test-your-flow"></a><span data-ttu-id="fa460-165">Step 7: Save and test your flow</span><span class="sxs-lookup"><span data-stu-id="fa460-165">Step 7: Save and test your flow</span></span>
- <span data-ttu-id="fa460-166">In the **Flow name** box, add a name for your flow, and then click **Create flow**.</span><span class="sxs-lookup"><span data-stu-id="fa460-166">In the **Flow name** box, add a name for your flow, and then click **Create flow**.</span></span>

    ![Flow-creation window](./media/app-insights-automate-with-flow/flow8.png)

<span data-ttu-id="fa460-168">You can wait for the trigger to run this action, or you can run the flow immediately by [running the trigger on demand](https://flow.microsoft.com/blog/run-now-and-six-more-services/).</span><span class="sxs-lookup"><span data-stu-id="fa460-168">You can wait for the trigger to run this action, or you can run the flow immediately by [running the trigger on demand](https://flow.microsoft.com/blog/run-now-and-six-more-services/).</span></span>

<span data-ttu-id="fa460-169">When the flow runs, the recipients you have specified in the email list receive an email message that looks like the following:</span><span class="sxs-lookup"><span data-stu-id="fa460-169">When the flow runs, the recipients you have specified in the email list receive an email message that looks like the following:</span></span>

![Sample email](./media/app-insights-automate-with-flow/flow9.png)


## <a name="next-steps"></a><span data-ttu-id="fa460-171">Next steps</span><span class="sxs-lookup"><span data-stu-id="fa460-171">Next steps</span></span>

- <span data-ttu-id="fa460-172">Learn more about creating [Analytics queries](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="fa460-172">Learn more about creating [Analytics queries](app-insights-analytics-using.md).</span></span>
- <span data-ttu-id="fa460-173">Learn more about [Microsoft Flow](https://ms.flow.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="fa460-173">Learn more about [Microsoft Flow](https://ms.flow.microsoft.com).</span></span>



<!--Link references-->





