---
title: Automate Azure Application Insights processes by using Logic Apps.
description: Learn how you can quickly automate repeatable processes by adding the Application Insights connector to your logic app.
services: application-insights
documentationcenter: ''
author: mrbullwinkle
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: conceptual
ms.date: 06/29/2017
ms.author: mbullwin
ms.openlocfilehash: 91b5c2c23445e5cd3445d1d5b640cb3ecb8e5e7a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966588"
---
# <a name="automate-application-insights-processes-by-using-logic-apps"></a><span data-ttu-id="728c4-103">Automate Application Insights processes by using Logic Apps</span><span class="sxs-lookup"><span data-stu-id="728c4-103">Automate Application Insights processes by using Logic Apps</span></span>

<span data-ttu-id="728c4-104">Do you find yourself repeatedly running the same queries on your telemetry data to check whether your service is functioning properly?</span><span class="sxs-lookup"><span data-stu-id="728c4-104">Do you find yourself repeatedly running the same queries on your telemetry data to check whether your service is functioning properly?</span></span> <span data-ttu-id="728c4-105">Are you looking to automate these queries for finding trends and anomalies and then build your own workflows around them?</span><span class="sxs-lookup"><span data-stu-id="728c4-105">Are you looking to automate these queries for finding trends and anomalies and then build your own workflows around them?</span></span> <span data-ttu-id="728c4-106">The Azure Application Insights connector (preview) for Logic Apps is the right tool for this purpose.</span><span class="sxs-lookup"><span data-stu-id="728c4-106">The Azure Application Insights connector (preview) for Logic Apps is the right tool for this purpose.</span></span>

<span data-ttu-id="728c4-107">With this integration, you can automate numerous processes without writing a single line of code.</span><span class="sxs-lookup"><span data-stu-id="728c4-107">With this integration, you can automate numerous processes without writing a single line of code.</span></span> <span data-ttu-id="728c4-108">You can create a logic app with the Application Insights connector to quickly automate any Application Insights process.</span><span class="sxs-lookup"><span data-stu-id="728c4-108">You can create a logic app with the Application Insights connector to quickly automate any Application Insights process.</span></span> 

<span data-ttu-id="728c4-109">You can add additional actions as well.</span><span class="sxs-lookup"><span data-stu-id="728c4-109">You can add additional actions as well.</span></span> <span data-ttu-id="728c4-110">The Logic Apps feature of Azure App Service makes hundreds of actions available.</span><span class="sxs-lookup"><span data-stu-id="728c4-110">The Logic Apps feature of Azure App Service makes hundreds of actions available.</span></span> <span data-ttu-id="728c4-111">For example, by using a logic app, you can automatically send an email notification or create a bug in Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="728c4-111">For example, by using a logic app, you can automatically send an email notification or create a bug in Azure DevOps.</span></span> <span data-ttu-id="728c4-112">You can also use one of the many available [templates](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) to help speed up the process of creating your logic app.</span><span class="sxs-lookup"><span data-stu-id="728c4-112">You can also use one of the many available [templates](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) to help speed up the process of creating your logic app.</span></span> 

## <a name="create-a-logic-app-for-application-insights"></a><span data-ttu-id="728c4-113">Create a logic app for Application Insights</span><span class="sxs-lookup"><span data-stu-id="728c4-113">Create a logic app for Application Insights</span></span>

<span data-ttu-id="728c4-114">In this tutorial, you learn how to create a logic app that uses the Analytics autocluster algorithm to group attributes in the data for a web application.</span><span class="sxs-lookup"><span data-stu-id="728c4-114">In this tutorial, you learn how to create a logic app that uses the Analytics autocluster algorithm to group attributes in the data for a web application.</span></span> <span data-ttu-id="728c4-115">The flow automatically sends the results by email, just one example of how you can use Application Insights Analytics and Logic Apps together.</span><span class="sxs-lookup"><span data-stu-id="728c4-115">The flow automatically sends the results by email, just one example of how you can use Application Insights Analytics and Logic Apps together.</span></span> 

### <a name="step-1-create-a-logic-app"></a><span data-ttu-id="728c4-116">Step 1: Create a logic app</span><span class="sxs-lookup"><span data-stu-id="728c4-116">Step 1: Create a logic app</span></span>
1. <span data-ttu-id="728c4-117">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="728c4-117">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="728c4-118">Click **Create a resource**, select **Web + Mobile**, and then select **Logic App**.</span><span class="sxs-lookup"><span data-stu-id="728c4-118">Click **Create a resource**, select **Web + Mobile**, and then select **Logic App**.</span></span>

    ![New logic app window](./media/automate-with-logic-apps/logicapp1.png)

### <a name="step-2-create-a-trigger-for-your-logic-app"></a><span data-ttu-id="728c4-120">Step 2: Create a trigger for your logic app</span><span class="sxs-lookup"><span data-stu-id="728c4-120">Step 2: Create a trigger for your logic app</span></span>
1. <span data-ttu-id="728c4-121">In the **Logic App Designer** window, under **Start with a common trigger**, select **Recurrence**.</span><span class="sxs-lookup"><span data-stu-id="728c4-121">In the **Logic App Designer** window, under **Start with a common trigger**, select **Recurrence**.</span></span>

    ![Logic App Designer window](./media/automate-with-logic-apps/logicapp2.png)

1. <span data-ttu-id="728c4-123">In the **Frequency** box, select **Day** and then, in the **Interval** box, type **1**.</span><span class="sxs-lookup"><span data-stu-id="728c4-123">In the **Frequency** box, select **Day** and then, in the **Interval** box, type **1**.</span></span>

    ![Logic App Designer "Recurrence" window](./media/automate-with-logic-apps/step2b.png)

### <a name="step-3-add-an-application-insights-action"></a><span data-ttu-id="728c4-125">Step 3: Add an Application Insights action</span><span class="sxs-lookup"><span data-stu-id="728c4-125">Step 3: Add an Application Insights action</span></span>
1. <span data-ttu-id="728c4-126">Click **New step**, and then click **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="728c4-126">Click **New step**, and then click **Add an action**.</span></span>

1. <span data-ttu-id="728c4-127">In the **Choose an action** search box, type **Azure Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="728c4-127">In the **Choose an action** search box, type **Azure Application Insights**.</span></span>

1. <span data-ttu-id="728c4-128">Under **Actions**, click **Azure Application Insights – Visualize Analytics query Preview**.</span><span class="sxs-lookup"><span data-stu-id="728c4-128">Under **Actions**, click **Azure Application Insights – Visualize Analytics query Preview**.</span></span>

    ![Logic App Designer "Choose an action" window](./media/automate-with-logic-apps/flow2.png)

### <a name="step-4-connect-to-an-application-insights-resource"></a><span data-ttu-id="728c4-130">Step 4: Connect to an Application Insights resource</span><span class="sxs-lookup"><span data-stu-id="728c4-130">Step 4: Connect to an Application Insights resource</span></span>

<span data-ttu-id="728c4-131">To complete this step, you need an application ID and an API key for your resource.</span><span class="sxs-lookup"><span data-stu-id="728c4-131">To complete this step, you need an application ID and an API key for your resource.</span></span> <span data-ttu-id="728c4-132">You can retrieve them from the Azure portal, as shown in the following diagram:</span><span class="sxs-lookup"><span data-stu-id="728c4-132">You can retrieve them from the Azure portal, as shown in the following diagram:</span></span>

![Application ID in the Azure portal](./media/automate-with-logic-apps/appid.png) 

<span data-ttu-id="728c4-134">Provide a name for your connection, the application ID, and the API key.</span><span class="sxs-lookup"><span data-stu-id="728c4-134">Provide a name for your connection, the application ID, and the API key.</span></span>

![Logic App Designer flow connection window](./media/automate-with-logic-apps/flow3.png)

### <a name="step-5-specify-the-analytics-query-and-chart-type"></a><span data-ttu-id="728c4-136">Step 5: Specify the Analytics query and chart type</span><span class="sxs-lookup"><span data-stu-id="728c4-136">Step 5: Specify the Analytics query and chart type</span></span>
<span data-ttu-id="728c4-137">In the following example, the query selects the failed requests within the last day and correlates them with exceptions that occurred as part of the operation.</span><span class="sxs-lookup"><span data-stu-id="728c4-137">In the following example, the query selects the failed requests within the last day and correlates them with exceptions that occurred as part of the operation.</span></span> <span data-ttu-id="728c4-138">Analytics correlates the failed requests, based on the operation_Id identifier.</span><span class="sxs-lookup"><span data-stu-id="728c4-138">Analytics correlates the failed requests, based on the operation_Id identifier.</span></span> <span data-ttu-id="728c4-139">The query then segments the results by using the autocluster algorithm.</span><span class="sxs-lookup"><span data-stu-id="728c4-139">The query then segments the results by using the autocluster algorithm.</span></span> 

<span data-ttu-id="728c4-140">When you create your own queries, verify that they are working properly in Analytics before you add it to your flow.</span><span class="sxs-lookup"><span data-stu-id="728c4-140">When you create your own queries, verify that they are working properly in Analytics before you add it to your flow.</span></span>

1. <span data-ttu-id="728c4-141">In the **Query** box, add the following Analytics query:</span><span class="sxs-lookup"><span data-stu-id="728c4-141">In the **Query** box, add the following Analytics query:</span></span> 

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

1. <span data-ttu-id="728c4-142">In the **Chart Type** box, select **Html Table**.</span><span class="sxs-lookup"><span data-stu-id="728c4-142">In the **Chart Type** box, select **Html Table**.</span></span>

    ![Analytics query configuration window](./media/automate-with-logic-apps/flow4.png)

### <a name="step-6-configure-the-logic-app-to-send-email"></a><span data-ttu-id="728c4-144">Step 6: Configure the logic app to send email</span><span class="sxs-lookup"><span data-stu-id="728c4-144">Step 6: Configure the logic app to send email</span></span>

1. <span data-ttu-id="728c4-145">Click **New step**, and then select **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="728c4-145">Click **New step**, and then select **Add an action**.</span></span>

1. <span data-ttu-id="728c4-146">In the search box, type **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="728c4-146">In the search box, type **Office 365 Outlook**.</span></span>

1. <span data-ttu-id="728c4-147">Click **Office 365 Outlook – Send an email**.</span><span class="sxs-lookup"><span data-stu-id="728c4-147">Click **Office 365 Outlook – Send an email**.</span></span>

    ![Office 365 Outlook selection](./media/automate-with-logic-apps/flow2b.png)

1. <span data-ttu-id="728c4-149">In the **Send an email** window, do the following:</span><span class="sxs-lookup"><span data-stu-id="728c4-149">In the **Send an email** window, do the following:</span></span>

   <span data-ttu-id="728c4-150">a.</span><span class="sxs-lookup"><span data-stu-id="728c4-150">a.</span></span> <span data-ttu-id="728c4-151">Type the email address of the recipient.</span><span class="sxs-lookup"><span data-stu-id="728c4-151">Type the email address of the recipient.</span></span>

   <span data-ttu-id="728c4-152">b.</span><span class="sxs-lookup"><span data-stu-id="728c4-152">b.</span></span> <span data-ttu-id="728c4-153">Type a subject for the email.</span><span class="sxs-lookup"><span data-stu-id="728c4-153">Type a subject for the email.</span></span>

   <span data-ttu-id="728c4-154">c.</span><span class="sxs-lookup"><span data-stu-id="728c4-154">c.</span></span> <span data-ttu-id="728c4-155">Click anywhere in the **Body** box and then, on the dynamic content menu that opens at the right, select **Body**.</span><span class="sxs-lookup"><span data-stu-id="728c4-155">Click anywhere in the **Body** box and then, on the dynamic content menu that opens at the right, select **Body**.</span></span>

   <span data-ttu-id="728c4-156">d.</span><span class="sxs-lookup"><span data-stu-id="728c4-156">d.</span></span> <span data-ttu-id="728c4-157">Click **Show advanced options**.</span><span class="sxs-lookup"><span data-stu-id="728c4-157">Click **Show advanced options**.</span></span>

      ![Office 365 Outlook configuration](./media/automate-with-logic-apps/flow5.png)

1. <span data-ttu-id="728c4-159">On the dynamic content menu, do the following:</span><span class="sxs-lookup"><span data-stu-id="728c4-159">On the dynamic content menu, do the following:</span></span>

    <span data-ttu-id="728c4-160">a.</span><span class="sxs-lookup"><span data-stu-id="728c4-160">a.</span></span> <span data-ttu-id="728c4-161">Select **Attachment Name**.</span><span class="sxs-lookup"><span data-stu-id="728c4-161">Select **Attachment Name**.</span></span>

    <span data-ttu-id="728c4-162">b.</span><span class="sxs-lookup"><span data-stu-id="728c4-162">b.</span></span> <span data-ttu-id="728c4-163">Select **Attachment Content**.</span><span class="sxs-lookup"><span data-stu-id="728c4-163">Select **Attachment Content**.</span></span>
    
    <span data-ttu-id="728c4-164">c.</span><span class="sxs-lookup"><span data-stu-id="728c4-164">c.</span></span> <span data-ttu-id="728c4-165">In the **Is HTML** box, select **Yes**.</span><span class="sxs-lookup"><span data-stu-id="728c4-165">In the **Is HTML** box, select **Yes**.</span></span>

      ![Office 365 email configuration screen](./media/automate-with-logic-apps/flow7.png)

### <a name="step-7-save-and-test-your-logic-app"></a><span data-ttu-id="728c4-167">Step 7: Save and test your logic app</span><span class="sxs-lookup"><span data-stu-id="728c4-167">Step 7: Save and test your logic app</span></span>
* <span data-ttu-id="728c4-168">Click **Save** to save your changes.</span><span class="sxs-lookup"><span data-stu-id="728c4-168">Click **Save** to save your changes.</span></span>

<span data-ttu-id="728c4-169">You can wait for the trigger to run the logic app, or you can run the logic app immediately by selecting **Run**.</span><span class="sxs-lookup"><span data-stu-id="728c4-169">You can wait for the trigger to run the logic app, or you can run the logic app immediately by selecting **Run**.</span></span>

![Logic app creation screen](./media/automate-with-logic-apps/step7.png)

<span data-ttu-id="728c4-171">When your logic app runs, the recipients you specified in the email list will receive an email that looks like the following:</span><span class="sxs-lookup"><span data-stu-id="728c4-171">When your logic app runs, the recipients you specified in the email list will receive an email that looks like the following:</span></span>

![Logic app email message](./media/automate-with-logic-apps/flow9.png)

## <a name="next-steps"></a><span data-ttu-id="728c4-173">Next steps</span><span class="sxs-lookup"><span data-stu-id="728c4-173">Next steps</span></span>

- <span data-ttu-id="728c4-174">Learn more about creating [Analytics queries](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="728c4-174">Learn more about creating [Analytics queries](app-insights-analytics-using.md).</span></span>
- <span data-ttu-id="728c4-175">Learn more about [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).</span><span class="sxs-lookup"><span data-stu-id="728c4-175">Learn more about [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).</span></span>



<!--Link references-->





