---
title: Scenario - Create a customer insights dashboard with Azure Serverless | Microsoft Docs
description: An example of how you can build a dashboard to manage customer feedback, social data, and more with Azure Logic Apps and Azure Functions.
keywords: ''
services: logic-apps
author: jeffhollan
manager: anneta
editor: ''
documentationcenter: ''
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/29/2017
ms.author: jehollan
ms.openlocfilehash: 57b34863c68d12044181cb9b2656e144fb098f62
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552509"
---
# <a name="create-a-real-time-customer-insights-dashboard-with-azure-logic-apps-and-azure-functions"></a><span data-ttu-id="45e7f-103">Create a real-time customer insights dashboard with Azure Logic Apps and Azure Functions</span><span class="sxs-lookup"><span data-stu-id="45e7f-103">Create a real-time customer insights dashboard with Azure Logic Apps and Azure Functions</span></span>

<span data-ttu-id="45e7f-104">Azure Serverless tools provide powerful capabilities to quickly build and host applications in the cloud, without having to think about infrastructure.</span><span class="sxs-lookup"><span data-stu-id="45e7f-104">Azure Serverless tools provide powerful capabilities to quickly build and host applications in the cloud, without having to think about infrastructure.</span></span>  <span data-ttu-id="45e7f-105">In this scenario, we will create a dashboard to trigger on customer feedback, analyze feedback with machine learning, and publish insights a source like Power BI or Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="45e7f-105">In this scenario, we will create a dashboard to trigger on customer feedback, analyze feedback with machine learning, and publish insights a source like Power BI or Azure Data Lake.</span></span>

## <a name="overview-of-the-scenario-and-tools-used"></a><span data-ttu-id="45e7f-106">Overview of the scenario and tools used</span><span class="sxs-lookup"><span data-stu-id="45e7f-106">Overview of the scenario and tools used</span></span>

<span data-ttu-id="45e7f-107">In order to implement this solution, we will leverage the two key components of serverless apps in Azure: [Azure Functions](https://azure.microsoft.com/services/functions/) and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span><span class="sxs-lookup"><span data-stu-id="45e7f-107">In order to implement this solution, we will leverage the two key components of serverless apps in Azure: [Azure Functions](https://azure.microsoft.com/services/functions/) and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span></span>

<span data-ttu-id="45e7f-108">Logic Apps is a serverless workflow engine in the cloud.</span><span class="sxs-lookup"><span data-stu-id="45e7f-108">Logic Apps is a serverless workflow engine in the cloud.</span></span>  <span data-ttu-id="45e7f-109">It provides orchestration across serverless components, and also connects to over 100 services and APIs.</span><span class="sxs-lookup"><span data-stu-id="45e7f-109">It provides orchestration across serverless components, and also connects to over 100 services and APIs.</span></span>  <span data-ttu-id="45e7f-110">For this scenario, we will create a logic app to trigger on feedback from customers.</span><span class="sxs-lookup"><span data-stu-id="45e7f-110">For this scenario, we will create a logic app to trigger on feedback from customers.</span></span>  <span data-ttu-id="45e7f-111">Some of the connectors that can assist in reacting to customer feedback include Outlook.com, Office 365, Survey Monkey, Twitter, and an HTTP Request [from a web form](https://blogs.msdn.microsoft.com/logicapps/2017/01/30/calling-a-logic-app-from-an-html-form/).</span><span class="sxs-lookup"><span data-stu-id="45e7f-111">Some of the connectors that can assist in reacting to customer feedback include Outlook.com, Office 365, Survey Monkey, Twitter, and an HTTP Request [from a web form](https://blogs.msdn.microsoft.com/logicapps/2017/01/30/calling-a-logic-app-from-an-html-form/).</span></span>  <span data-ttu-id="45e7f-112">For the workflow below, we will monitor a hashtag on Twitter.</span><span class="sxs-lookup"><span data-stu-id="45e7f-112">For the workflow below, we will monitor a hashtag on Twitter.</span></span>

<span data-ttu-id="45e7f-113">Functions provide serverless compute in the cloud.</span><span class="sxs-lookup"><span data-stu-id="45e7f-113">Functions provide serverless compute in the cloud.</span></span>  <span data-ttu-id="45e7f-114">In this scenario, we will use Azure Functions to flag tweets from customers based on a series of pre-defined key words.</span><span class="sxs-lookup"><span data-stu-id="45e7f-114">In this scenario, we will use Azure Functions to flag tweets from customers based on a series of pre-defined key words.</span></span>

<span data-ttu-id="45e7f-115">The entire solution can be [build in Visual Studio](logic-apps-deploy-from-vs.md) and [deployed as part of a resource template](logic-apps-create-deploy-template.md).</span><span class="sxs-lookup"><span data-stu-id="45e7f-115">The entire solution can be [build in Visual Studio](logic-apps-deploy-from-vs.md) and [deployed as part of a resource template](logic-apps-create-deploy-template.md).</span></span>  <span data-ttu-id="45e7f-116">There is also video walkthrough of the scenario [on Channel 9](http://aka.ms/logicappsdemo).</span><span class="sxs-lookup"><span data-stu-id="45e7f-116">There is also video walkthrough of the scenario [on Channel 9](http://aka.ms/logicappsdemo).</span></span>

## <a name="build-the-logic-app-to-trigger-on-customer-data"></a><span data-ttu-id="45e7f-117">Build the logic app to trigger on customer data</span><span class="sxs-lookup"><span data-stu-id="45e7f-117">Build the logic app to trigger on customer data</span></span>

<span data-ttu-id="45e7f-118">After [creating a logic app](logic-apps-create-a-logic-app.md) in Visual Studio or the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="45e7f-118">After [creating a logic app](logic-apps-create-a-logic-app.md) in Visual Studio or the Azure portal:</span></span>

1. <span data-ttu-id="45e7f-119">Add a trigger for **On New Tweets** from Twitter</span><span class="sxs-lookup"><span data-stu-id="45e7f-119">Add a trigger for **On New Tweets** from Twitter</span></span>
2. <span data-ttu-id="45e7f-120">Configure the trigger to listen to tweets on a keyword or hashtag.</span><span class="sxs-lookup"><span data-stu-id="45e7f-120">Configure the trigger to listen to tweets on a keyword or hashtag.</span></span>

   > [!NOTE]
   > <span data-ttu-id="45e7f-121">The recurrence property on the trigger will determine how frequently the logic app checks for new items on polling-based triggers</span><span class="sxs-lookup"><span data-stu-id="45e7f-121">The recurrence property on the trigger will determine how frequently the logic app checks for new items on polling-based triggers</span></span>

   ![Example of Twitter trigger][1]

<span data-ttu-id="45e7f-123">This app will now fire on all new tweets.</span><span class="sxs-lookup"><span data-stu-id="45e7f-123">This app will now fire on all new tweets.</span></span>  <span data-ttu-id="45e7f-124">We can then take that tweet data and understand more of the sentiment expressed.</span><span class="sxs-lookup"><span data-stu-id="45e7f-124">We can then take that tweet data and understand more of the sentiment expressed.</span></span>  <span data-ttu-id="45e7f-125">For this we use the [Azure Cognitive Service](https://azure.microsoft.com/services/cognitive-services/) to detect sentiment of text.</span><span class="sxs-lookup"><span data-stu-id="45e7f-125">For this we use the [Azure Cognitive Service](https://azure.microsoft.com/services/cognitive-services/) to detect sentiment of text.</span></span>

1. <span data-ttu-id="45e7f-126">Click **New Step**</span><span class="sxs-lookup"><span data-stu-id="45e7f-126">Click **New Step**</span></span>
1. <span data-ttu-id="45e7f-127">Select or search for the **Text Analytics** connector</span><span class="sxs-lookup"><span data-stu-id="45e7f-127">Select or search for the **Text Analytics** connector</span></span>
1. <span data-ttu-id="45e7f-128">Select the **Detect Sentiment** operation</span><span class="sxs-lookup"><span data-stu-id="45e7f-128">Select the **Detect Sentiment** operation</span></span>
1. <span data-ttu-id="45e7f-129">If prompted, provide a valid Cognitive Services key for the Text Analytics service</span><span class="sxs-lookup"><span data-stu-id="45e7f-129">If prompted, provide a valid Cognitive Services key for the Text Analytics service</span></span>
1. <span data-ttu-id="45e7f-130">Add the **Tweet Text** as the text to analyze.</span><span class="sxs-lookup"><span data-stu-id="45e7f-130">Add the **Tweet Text** as the text to analyze.</span></span>

<span data-ttu-id="45e7f-131">Now that we have the tweet data, and insights on the tweet, a number of other connectors may be relevant:</span><span class="sxs-lookup"><span data-stu-id="45e7f-131">Now that we have the tweet data, and insights on the tweet, a number of other connectors may be relevant:</span></span>
* <span data-ttu-id="45e7f-132">Power BI - Add Rows to Streaming Dataset: View tweets real time on a Power BI dashboard.</span><span class="sxs-lookup"><span data-stu-id="45e7f-132">Power BI - Add Rows to Streaming Dataset: View tweets real time on a Power BI dashboard.</span></span>
* <span data-ttu-id="45e7f-133">Azure Data Lake - Append file: Add customer data to an Azure Data Lake dataset to include in analytics jobs.</span><span class="sxs-lookup"><span data-stu-id="45e7f-133">Azure Data Lake - Append file: Add customer data to an Azure Data Lake dataset to include in analytics jobs.</span></span>
* <span data-ttu-id="45e7f-134">SQL - Add rows: Store data in a database for later retrieval.</span><span class="sxs-lookup"><span data-stu-id="45e7f-134">SQL - Add rows: Store data in a database for later retrieval.</span></span>
* <span data-ttu-id="45e7f-135">Slack - Send message: Alert a slack channel on negative feedback that requires actions.</span><span class="sxs-lookup"><span data-stu-id="45e7f-135">Slack - Send message: Alert a slack channel on negative feedback that requires actions.</span></span>

<span data-ttu-id="45e7f-136">An Azure Function can also be used to do more custom compute on top of the data.</span><span class="sxs-lookup"><span data-stu-id="45e7f-136">An Azure Function can also be used to do more custom compute on top of the data.</span></span>

## <a name="enriching-the-data-with-an-azure-function"></a><span data-ttu-id="45e7f-137">Enriching the data with an Azure Function</span><span class="sxs-lookup"><span data-stu-id="45e7f-137">Enriching the data with an Azure Function</span></span>

<span data-ttu-id="45e7f-138">Before we can create a function, we need to have a function app in our Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="45e7f-138">Before we can create a function, we need to have a function app in our Azure subscription.</span></span>  <span data-ttu-id="45e7f-139">Details on creating an Azure Function in the portal can [be found here](../azure-functions/functions-create-first-azure-function-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="45e7f-139">Details on creating an Azure Function in the portal can [be found here](../azure-functions/functions-create-first-azure-function-azure-portal.md)</span></span>

<span data-ttu-id="45e7f-140">For a function to be called directly from a logic app, it needs to have an HTTP trigger binding.</span><span class="sxs-lookup"><span data-stu-id="45e7f-140">For a function to be called directly from a logic app, it needs to have an HTTP trigger binding.</span></span>  <span data-ttu-id="45e7f-141">We recommend using the **HttpTrigger** template.</span><span class="sxs-lookup"><span data-stu-id="45e7f-141">We recommend using the **HttpTrigger** template.</span></span>

<span data-ttu-id="45e7f-142">In this scenario, the request body of the Azure Function would be the tweet text.</span><span class="sxs-lookup"><span data-stu-id="45e7f-142">In this scenario, the request body of the Azure Function would be the tweet text.</span></span>  <span data-ttu-id="45e7f-143">In the function code, simply define logic on if the tweet text contains a key word or phrase.</span><span class="sxs-lookup"><span data-stu-id="45e7f-143">In the function code, simply define logic on if the tweet text contains a key word or phrase.</span></span>  <span data-ttu-id="45e7f-144">The function itself could be kept as simple or complex as needed for the scenario.</span><span class="sxs-lookup"><span data-stu-id="45e7f-144">The function itself could be kept as simple or complex as needed for the scenario.</span></span>

<span data-ttu-id="45e7f-145">At the end of the function, simply return a response to the logic app with some data.</span><span class="sxs-lookup"><span data-stu-id="45e7f-145">At the end of the function, simply return a response to the logic app with some data.</span></span>  <span data-ttu-id="45e7f-146">This could be a simple boolean value (e.g. `containsKeyword`), or a complex object.</span><span class="sxs-lookup"><span data-stu-id="45e7f-146">This could be a simple boolean value (e.g. `containsKeyword`), or a complex object.</span></span>

![Configured Azure Function step][2]

> [!TIP]
> <span data-ttu-id="45e7f-148">When accessing a complex response from a function in a logic app, use the Parse JSON action.</span><span class="sxs-lookup"><span data-stu-id="45e7f-148">When accessing a complex response from a function in a logic app, use the Parse JSON action.</span></span>

<span data-ttu-id="45e7f-149">Once the function is saved, it can be added into the logic app created above.</span><span class="sxs-lookup"><span data-stu-id="45e7f-149">Once the function is saved, it can be added into the logic app created above.</span></span>  <span data-ttu-id="45e7f-150">In the logic app:</span><span class="sxs-lookup"><span data-stu-id="45e7f-150">In the logic app:</span></span>

1. <span data-ttu-id="45e7f-151">Click to add a **New Step**</span><span class="sxs-lookup"><span data-stu-id="45e7f-151">Click to add a **New Step**</span></span>
1. <span data-ttu-id="45e7f-152">Select the **Azure Functions** connector</span><span class="sxs-lookup"><span data-stu-id="45e7f-152">Select the **Azure Functions** connector</span></span>
1. <span data-ttu-id="45e7f-153">Select to choose an existing function, and browse to the function created</span><span class="sxs-lookup"><span data-stu-id="45e7f-153">Select to choose an existing function, and browse to the function created</span></span>
1. <span data-ttu-id="45e7f-154">Send in the **Tweet Text** for the **Request Body**</span><span class="sxs-lookup"><span data-stu-id="45e7f-154">Send in the **Tweet Text** for the **Request Body**</span></span>

## <a name="running-and-monitoring-the-solution"></a><span data-ttu-id="45e7f-155">Running and monitoring the solution</span><span class="sxs-lookup"><span data-stu-id="45e7f-155">Running and monitoring the solution</span></span>

<span data-ttu-id="45e7f-156">One of the benefits of authoring serverless orchestrations in Logic Apps is the rich debug and monitoring capabilities.</span><span class="sxs-lookup"><span data-stu-id="45e7f-156">One of the benefits of authoring serverless orchestrations in Logic Apps is the rich debug and monitoring capabilities.</span></span>  <span data-ttu-id="45e7f-157">Any run (current or historic) can be viewed from within Visual Studio, the Azure portal, or via the REST API and SDKs.</span><span class="sxs-lookup"><span data-stu-id="45e7f-157">Any run (current or historic) can be viewed from within Visual Studio, the Azure portal, or via the REST API and SDKs.</span></span>

<span data-ttu-id="45e7f-158">One of the easiest ways to test a logic app is using the **Run** button in the designer.</span><span class="sxs-lookup"><span data-stu-id="45e7f-158">One of the easiest ways to test a logic app is using the **Run** button in the designer.</span></span>  <span data-ttu-id="45e7f-159">Clicking **Run** will continue to poll the trigger every 5 seconds until an event is detected, and give a live view as the run progresses.</span><span class="sxs-lookup"><span data-stu-id="45e7f-159">Clicking **Run** will continue to poll the trigger every 5 seconds until an event is detected, and give a live view as the run progresses.</span></span>

<span data-ttu-id="45e7f-160">Previous run histories can be viewed on the Overview blade in the Azure portal, or using the Visual Studio Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="45e7f-160">Previous run histories can be viewed on the Overview blade in the Azure portal, or using the Visual Studio Cloud Explorer.</span></span>

## <a name="creating-a-deployment-template-for-automated-deployments"></a><span data-ttu-id="45e7f-161">Creating a deployment template for automated deployments</span><span class="sxs-lookup"><span data-stu-id="45e7f-161">Creating a deployment template for automated deployments</span></span>

<span data-ttu-id="45e7f-162">Once a solution has been developed, it can be captured and deployed via an Azure deployment template to any Azure region in the world.</span><span class="sxs-lookup"><span data-stu-id="45e7f-162">Once a solution has been developed, it can be captured and deployed via an Azure deployment template to any Azure region in the world.</span></span>  <span data-ttu-id="45e7f-163">This is useful for both modifying parameters for different versions of this workflow, but also for integrating this solution in a build and release pipeline.</span><span class="sxs-lookup"><span data-stu-id="45e7f-163">This is useful for both modifying parameters for different versions of this workflow, but also for integrating this solution in a build and release pipeline.</span></span>  <span data-ttu-id="45e7f-164">Details on creating a deployment template can be found [in this article](logic-apps-create-deploy-template.md).</span><span class="sxs-lookup"><span data-stu-id="45e7f-164">Details on creating a deployment template can be found [in this article](logic-apps-create-deploy-template.md).</span></span>

<span data-ttu-id="45e7f-165">Azure Functions can also be incorporated in the deployment template - so the entire solution with all dependencies can be managed as a single template.</span><span class="sxs-lookup"><span data-stu-id="45e7f-165">Azure Functions can also be incorporated in the deployment template - so the entire solution with all dependencies can be managed as a single template.</span></span>  <span data-ttu-id="45e7f-166">An example of a function deployment template can be found in the [Azure quickstart template repository](https://github.com/Azure/azure-quickstart-templates/tree/master/101-function-app-create-dynamic).</span><span class="sxs-lookup"><span data-stu-id="45e7f-166">An example of a function deployment template can be found in the [Azure quickstart template repository](https://github.com/Azure/azure-quickstart-templates/tree/master/101-function-app-create-dynamic).</span></span>

## <a name="next-steps"></a><span data-ttu-id="45e7f-167">Next steps</span><span class="sxs-lookup"><span data-stu-id="45e7f-167">Next steps</span></span>

* [<span data-ttu-id="45e7f-168">See other examples and scenarios for Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="45e7f-168">See other examples and scenarios for Azure Logic Apps</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="45e7f-169">Watch a video walkthrough on creating this solution end-to-end</span><span class="sxs-lookup"><span data-stu-id="45e7f-169">Watch a video walkthrough on creating this solution end-to-end</span></span>](http://aka.ms/logicappsdemo)
* [<span data-ttu-id="45e7f-170">Learn how to handle and catch exceptions within a logic app</span><span class="sxs-lookup"><span data-stu-id="45e7f-170">Learn how to handle and catch exceptions within a logic app</span></span>](logic-apps-exception-handling.md)

<!-- Image References -->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-scenario-social-serverless/twitter.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-scenario-social-serverless/function.png

