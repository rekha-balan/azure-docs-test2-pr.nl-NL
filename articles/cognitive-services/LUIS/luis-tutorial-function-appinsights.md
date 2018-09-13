---
title: Add LUIS data to Application Insights using Node.js | Microsoft Docs
titleSuffix: Azure
description: Build a bot integrated with a LUIS application and Application Insights using Node.js.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 01/18/2018
ms.author: diberry
ms.openlocfilehash: 26806222015c78c791b36618f677a698914d1e45
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866373"
---
# <a name="add-luis-results-to-application-insights-from-a-web-app-bot"></a><span data-ttu-id="67624-103">Add LUIS results to Application Insights from a web app bot</span><span class="sxs-lookup"><span data-stu-id="67624-103">Add LUIS results to Application Insights from a web app bot</span></span>
<span data-ttu-id="67624-104">This tutorial adds LUIS request and response information to [Application Insights](https://azure.microsoft.com/services/application-insights/) telemetry data storage.</span><span class="sxs-lookup"><span data-stu-id="67624-104">This tutorial adds LUIS request and response information to [Application Insights](https://azure.microsoft.com/services/application-insights/) telemetry data storage.</span></span> <span data-ttu-id="67624-105">Once you have that data, you can query it with the Kusto language or PowerBi to analyze, aggregate, and report on intents, and entities of the utterance in real-time.</span><span class="sxs-lookup"><span data-stu-id="67624-105">Once you have that data, you can query it with the Kusto language or PowerBi to analyze, aggregate, and report on intents, and entities of the utterance in real-time.</span></span> <span data-ttu-id="67624-106">This analysis helps you determine if you should add or edit the intents and entities of your LUIS app.</span><span class="sxs-lookup"><span data-stu-id="67624-106">This analysis helps you determine if you should add or edit the intents and entities of your LUIS app.</span></span>

<span data-ttu-id="67624-107">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="67624-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
* <span data-ttu-id="67624-108">Add Application Insights library to a web app bot</span><span class="sxs-lookup"><span data-stu-id="67624-108">Add Application Insights library to a web app bot</span></span>
* <span data-ttu-id="67624-109">Capture and send LUIS query results to Application Insights</span><span class="sxs-lookup"><span data-stu-id="67624-109">Capture and send LUIS query results to Application Insights</span></span>
* <span data-ttu-id="67624-110">Query Application Insights for top intent, score, and utterance</span><span class="sxs-lookup"><span data-stu-id="67624-110">Query Application Insights for top intent, score, and utterance</span></span>

## <a name="prerequisites"></a><span data-ttu-id="67624-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="67624-111">Prerequisites</span></span>

* <span data-ttu-id="67624-112">Your LUIS web app bot from the **[previous tutorial](luis-nodejs-tutorial-build-bot-framework-sample.md)** with Application Insights turned on.</span><span class="sxs-lookup"><span data-stu-id="67624-112">Your LUIS web app bot from the **[previous tutorial](luis-nodejs-tutorial-build-bot-framework-sample.md)** with Application Insights turned on.</span></span> 

> [!Tip]
> <span data-ttu-id="67624-113">If you do not already have a subscription, you can register for a [free account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="67624-113">If you do not already have a subscription, you can register for a [free account](https://azure.microsoft.com/free/).</span></span>

<span data-ttu-id="67624-114">All of the code in this tutorial is available on the [LUIS-Samples github repository](https://github.com/Microsoft/LUIS-Samples/tree/master/documentation-samples/tutorial-web-app-bot-application-insights/nodejs) and each line associated with this tutorial is commented with `//APPINSIGHT:`.</span><span class="sxs-lookup"><span data-stu-id="67624-114">All of the code in this tutorial is available on the [LUIS-Samples github repository](https://github.com/Microsoft/LUIS-Samples/tree/master/documentation-samples/tutorial-web-app-bot-application-insights/nodejs) and each line associated with this tutorial is commented with `//APPINSIGHT:`.</span></span> 

## <a name="web-app-bot-with-luis"></a><span data-ttu-id="67624-115">Web app bot with LUIS</span><span class="sxs-lookup"><span data-stu-id="67624-115">Web app bot with LUIS</span></span>
<span data-ttu-id="67624-116">This tutorial assumes you have code that looks like the following or that you have completed the [other tutorial](luis-nodejs-tutorial-build-bot-framework-sample.md):</span><span class="sxs-lookup"><span data-stu-id="67624-116">This tutorial assumes you have code that looks like the following or that you have completed the [other tutorial](luis-nodejs-tutorial-build-bot-framework-sample.md):</span></span> 

   [!code-javascript[Web app bot with LUIS](~/samples-luis/documentation-samples/tutorial-web-app-bot/nodejs/app.js "Web app bot with LUIS")]

## <a name="add-application-insights-library-to-web-app-bot"></a><span data-ttu-id="67624-117">Add Application Insights library to web app bot</span><span class="sxs-lookup"><span data-stu-id="67624-117">Add Application Insights library to web app bot</span></span>
<span data-ttu-id="67624-118">Currently, the Application Insights service, used in this web app bot, collects general state telemetry for the bot.</span><span class="sxs-lookup"><span data-stu-id="67624-118">Currently, the Application Insights service, used in this web app bot, collects general state telemetry for the bot.</span></span> <span data-ttu-id="67624-119">It does not collect LUIS request and response information that you need to check and fix your intents and entities.</span><span class="sxs-lookup"><span data-stu-id="67624-119">It does not collect LUIS request and response information that you need to check and fix your intents and entities.</span></span> 

<span data-ttu-id="67624-120">In order to capture the LUIS request and response, the web app bot needs the **[Application Insights](https://www.npmjs.com/package/applicationinsights)** NPM package installed and configured in the **app.js** file.</span><span class="sxs-lookup"><span data-stu-id="67624-120">In order to capture the LUIS request and response, the web app bot needs the **[Application Insights](https://www.npmjs.com/package/applicationinsights)** NPM package installed and configured in the **app.js** file.</span></span> <span data-ttu-id="67624-121">Then the intent dialog handlers need to send the LUIS request and response information to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="67624-121">Then the intent dialog handlers need to send the LUIS request and response information to Application Insights.</span></span> 

1. <span data-ttu-id="67624-122">In the Azure portal, in the web app bot service, select **Build** under the **Bot Management** section.</span><span class="sxs-lookup"><span data-stu-id="67624-122">In the Azure portal, in the web app bot service, select **Build** under the **Bot Management** section.</span></span> 

    ![Search for app insights](./media/luis-tutorial-appinsights/build.png)

2. <span data-ttu-id="67624-124">A new browser tab opens with the App Service Editor.</span><span class="sxs-lookup"><span data-stu-id="67624-124">A new browser tab opens with the App Service Editor.</span></span> <span data-ttu-id="67624-125">Select the app name in the top bar, then select **Open Kudu Console**.</span><span class="sxs-lookup"><span data-stu-id="67624-125">Select the app name in the top bar, then select **Open Kudu Console**.</span></span> 

    ![Search for app insights](./media/luis-tutorial-appinsights/kudu-console.png)

3. <span data-ttu-id="67624-127">In the console, enter the following command to install Application Insights and the Underscore packages:</span><span class="sxs-lookup"><span data-stu-id="67624-127">In the console, enter the following command to install Application Insights and the Underscore packages:</span></span>

    ```
    cd site\wwwroot && npm install applicationinsights && npm install underscore
    ```

    ![Search for app insights](./media/luis-tutorial-appinsights/npm-install.png)

    <span data-ttu-id="67624-129">Wait for the packages to install:</span><span class="sxs-lookup"><span data-stu-id="67624-129">Wait for the packages to install:</span></span>

    ```
    luisbot@1.0.0 D:\home\site\wwwroot
    `-- applicationinsights@1.0.1 
      +-- diagnostic-channel@0.2.0 
      +-- diagnostic-channel-publishers@0.2.1 
      `-- zone.js@0.7.6 
    
    npm WARN luisbot@1.0.0 No repository field.
    luisbot@1.0.0 D:\home\site\wwwroot
    +-- botbuilder-azure@3.0.4
    | `-- azure-storage@1.4.0
    |   `-- underscore@1.4.4 
    `-- underscore@1.8.3 
    ```

    <span data-ttu-id="67624-130">You are done with the kudu console browser tab.</span><span class="sxs-lookup"><span data-stu-id="67624-130">You are done with the kudu console browser tab.</span></span>

## <a name="capture-and-send-luis-query-results-to-application-insights"></a><span data-ttu-id="67624-131">Capture and send LUIS query results to Application Insights</span><span class="sxs-lookup"><span data-stu-id="67624-131">Capture and send LUIS query results to Application Insights</span></span>
1. <span data-ttu-id="67624-132">In the App Service Editor browser tab, open the **app.js** file.</span><span class="sxs-lookup"><span data-stu-id="67624-132">In the App Service Editor browser tab, open the **app.js** file.</span></span>

2. <span data-ttu-id="67624-133">Add the following NPM libraries under the existing `requires` lines:</span><span class="sxs-lookup"><span data-stu-id="67624-133">Add the following NPM libraries under the existing `requires` lines:</span></span>

   [!code-javascript[Add NPM packages to app.js](~/samples-luis/documentation-samples/tutorial-web-app-bot-application-insights/nodejs/app.js?range=12-16 "Add NPM packages to app.js")]

3. <span data-ttu-id="67624-134">Create the Application Insights object and use the web app bot application setting **BotDevInsightsKey**:</span><span class="sxs-lookup"><span data-stu-id="67624-134">Create the Application Insights object and use the web app bot application setting **BotDevInsightsKey**:</span></span> 

   [!code-javascript[Create the Application Insights object](~/samples-luis/documentation-samples/tutorial-web-app-bot-application-insights/nodejs/app.js?range=68-80 "Create the Application Insights object")]

4. <span data-ttu-id="67624-135">Add the **appInsightsLog** function:</span><span class="sxs-lookup"><span data-stu-id="67624-135">Add the **appInsightsLog** function:</span></span>

   [!code-javascript[Add the appInsightsLog function](~/samples-luis/documentation-samples/tutorial-web-app-bot-application-insights/nodejs/app.js?range=82-109 "Add the appInsightsLog function")]

    <span data-ttu-id="67624-136">The last line of the function is where the data is added to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="67624-136">The last line of the function is where the data is added to Application Insights.</span></span> <span data-ttu-id="67624-137">The event's name is **LUIS-results**, a unique name apart from any other telemetry data collected by this web app bot.</span><span class="sxs-lookup"><span data-stu-id="67624-137">The event's name is **LUIS-results**, a unique name apart from any other telemetry data collected by this web app bot.</span></span> 

5. <span data-ttu-id="67624-138">Use the **appInsightsLog** function.</span><span class="sxs-lookup"><span data-stu-id="67624-138">Use the **appInsightsLog** function.</span></span> <span data-ttu-id="67624-139">You add it to every intent dialog:</span><span class="sxs-lookup"><span data-stu-id="67624-139">You add it to every intent dialog:</span></span>

   [!code-javascript[Use the appInsightsLog function](~/samples-luis/documentation-samples/tutorial-web-app-bot-application-insights/nodejs/app.js?range=117-118 "Use the appInsightsLog function")]

6. <span data-ttu-id="67624-140">To test your web app bot, use the **Test in Web Chat** feature.</span><span class="sxs-lookup"><span data-stu-id="67624-140">To test your web app bot, use the **Test in Web Chat** feature.</span></span> <span data-ttu-id="67624-141">You should see no difference because all the work is in Application Insights, not in the bot responses.</span><span class="sxs-lookup"><span data-stu-id="67624-141">You should see no difference because all the work is in Application Insights, not in the bot responses.</span></span>

## <a name="view-luis-entries-in-application-insights"></a><span data-ttu-id="67624-142">View LUIS entries in Application Insights</span><span class="sxs-lookup"><span data-stu-id="67624-142">View LUIS entries in Application Insights</span></span>
<span data-ttu-id="67624-143">Open Application Insights to see the LUIS entries.</span><span class="sxs-lookup"><span data-stu-id="67624-143">Open Application Insights to see the LUIS entries.</span></span> 

1. <span data-ttu-id="67624-144">In the portal, select **All resources** then filter by the web app bot name.</span><span class="sxs-lookup"><span data-stu-id="67624-144">In the portal, select **All resources** then filter by the web app bot name.</span></span> <span data-ttu-id="67624-145">Click on the resource with the type **Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="67624-145">Click on the resource with the type **Application Insights**.</span></span> <span data-ttu-id="67624-146">The icon for Application Insights is a light bulb.</span><span class="sxs-lookup"><span data-stu-id="67624-146">The icon for Application Insights is a light bulb.</span></span> 

    ![Search for app insights](./media/luis-tutorial-appinsights/search-for-app-insights.png)



2. <span data-ttu-id="67624-148">When the resource opens, click on the **Search** icon of the magnifying glass in the far right panel.</span><span class="sxs-lookup"><span data-stu-id="67624-148">When the resource opens, click on the **Search** icon of the magnifying glass in the far right panel.</span></span> <span data-ttu-id="67624-149">A new panel to the right displays.</span><span class="sxs-lookup"><span data-stu-id="67624-149">A new panel to the right displays.</span></span> <span data-ttu-id="67624-150">Depending on how much telemetry data is found, the panel may take a second to display.</span><span class="sxs-lookup"><span data-stu-id="67624-150">Depending on how much telemetry data is found, the panel may take a second to display.</span></span> <span data-ttu-id="67624-151">Search for `LUIS-results` and hit enter on the keyboard.</span><span class="sxs-lookup"><span data-stu-id="67624-151">Search for `LUIS-results` and hit enter on the keyboard.</span></span> <span data-ttu-id="67624-152">The list is narrowed to just LUIS query results added with this tutorial.</span><span class="sxs-lookup"><span data-stu-id="67624-152">The list is narrowed to just LUIS query results added with this tutorial.</span></span>

    ![Filter to dependencies](./media/luis-tutorial-appinsights/app-insights-filter.png)

3. <span data-ttu-id="67624-154">Select the top entry.</span><span class="sxs-lookup"><span data-stu-id="67624-154">Select the top entry.</span></span> <span data-ttu-id="67624-155">A new window displays more detailed data including the custom data for the LUIS query at the far-right.</span><span class="sxs-lookup"><span data-stu-id="67624-155">A new window displays more detailed data including the custom data for the LUIS query at the far-right.</span></span> <span data-ttu-id="67624-156">The data includes the top intent, and its score.</span><span class="sxs-lookup"><span data-stu-id="67624-156">The data includes the top intent, and its score.</span></span>

    ![Dependency details](./media/luis-tutorial-appinsights/app-insights-detail.png)

    <span data-ttu-id="67624-158">When you are done, select the far-right top **X** to return to the list of dependency items.</span><span class="sxs-lookup"><span data-stu-id="67624-158">When you are done, select the far-right top **X** to return to the list of dependency items.</span></span> 


> [!Tip]
> <span data-ttu-id="67624-159">If you want to save the dependency list and return to it later, click on **...More** and click **Save favorite**.</span><span class="sxs-lookup"><span data-stu-id="67624-159">If you want to save the dependency list and return to it later, click on **...More** and click **Save favorite**.</span></span>

## <a name="query-application-insights-for-intent-score-and-utterance"></a><span data-ttu-id="67624-160">Query Application Insights for intent, score, and utterance</span><span class="sxs-lookup"><span data-stu-id="67624-160">Query Application Insights for intent, score, and utterance</span></span>
<span data-ttu-id="67624-161">Application Insights gives you the power to query the data with the [Kusto](https://docs.microsoft.com/azure/application-insights/app-insights-analytics#query-data-in-analytics) language, as well as export it to [PowerBI](https://powerbi.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="67624-161">Application Insights gives you the power to query the data with the [Kusto](https://docs.microsoft.com/azure/application-insights/app-insights-analytics#query-data-in-analytics) language, as well as export it to [PowerBI](https://powerbi.microsoft.com).</span></span> 

1. <span data-ttu-id="67624-162">Click on **Analytics** at the top of the dependency listing, above the filter box.</span><span class="sxs-lookup"><span data-stu-id="67624-162">Click on **Analytics** at the top of the dependency listing, above the filter box.</span></span> 

    ![Analytics button](./media/luis-tutorial-appinsights/analytics-button.png)

2. <span data-ttu-id="67624-164">A new window opens with a query window at the top and a data table window below that.</span><span class="sxs-lookup"><span data-stu-id="67624-164">A new window opens with a query window at the top and a data table window below that.</span></span> <span data-ttu-id="67624-165">If you have used databases before, this arrangement is familiar.</span><span class="sxs-lookup"><span data-stu-id="67624-165">If you have used databases before, this arrangement is familiar.</span></span> <span data-ttu-id="67624-166">The query includes all items from the last 24 hours beginning with the name `LUIS-results`.</span><span class="sxs-lookup"><span data-stu-id="67624-166">The query includes all items from the last 24 hours beginning with the name `LUIS-results`.</span></span> <span data-ttu-id="67624-167">The **CustomDimensions** column has the LUIS query results as name/value pairs.</span><span class="sxs-lookup"><span data-stu-id="67624-167">The **CustomDimensions** column has the LUIS query results as name/value pairs.</span></span>

    ![Analytics query window](./media/luis-tutorial-appinsights/analytics-query-window.png)

3. <span data-ttu-id="67624-169">To pull out the top intent, score, and utterance, add the following just above the last line in the query window:</span><span class="sxs-lookup"><span data-stu-id="67624-169">To pull out the top intent, score, and utterance, add the following just above the last line in the query window:</span></span>

    ```SQL
    | extend topIntent = tostring(customDimensions.LUIS_intent_intent)
    | extend score = todouble(customDimensions.LUIS_intent_score)
    | extend utterance = tostring(customDimensions.LUIS_text)
    ```

4. <span data-ttu-id="67624-170">Run the query.</span><span class="sxs-lookup"><span data-stu-id="67624-170">Run the query.</span></span> <span data-ttu-id="67624-171">Scroll to the far right in the data table.</span><span class="sxs-lookup"><span data-stu-id="67624-171">Scroll to the far right in the data table.</span></span> <span data-ttu-id="67624-172">The new columns of topIntent, score, and utterance are available.</span><span class="sxs-lookup"><span data-stu-id="67624-172">The new columns of topIntent, score, and utterance are available.</span></span> <span data-ttu-id="67624-173">Click on the topIntent column to sort.</span><span class="sxs-lookup"><span data-stu-id="67624-173">Click on the topIntent column to sort.</span></span>

    ![Analytics top intent](./media/luis-tutorial-appinsights/app-insights-top-intent.png)


<span data-ttu-id="67624-175">Learn more about the [Kusto query language](https://docs.loganalytics.io/docs/Learn/Getting-Started/Getting-started-with-queries) or [export the data to PowerBi](https://docs.microsoft.com/azure/application-insights/app-insights-export-power-bi).</span><span class="sxs-lookup"><span data-stu-id="67624-175">Learn more about the [Kusto query language](https://docs.loganalytics.io/docs/Learn/Getting-Started/Getting-started-with-queries) or [export the data to PowerBi](https://docs.microsoft.com/azure/application-insights/app-insights-export-power-bi).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="67624-176">Next steps</span><span class="sxs-lookup"><span data-stu-id="67624-176">Next steps</span></span>

<span data-ttu-id="67624-177">Other information you may want to add to the application insights data includes app ID, version ID, last model change date, last train date, last publish date.</span><span class="sxs-lookup"><span data-stu-id="67624-177">Other information you may want to add to the application insights data includes app ID, version ID, last model change date, last train date, last publish date.</span></span> <span data-ttu-id="67624-178">These values can either be retrieved from the endpoint URL (app ID and version ID), or from an [authoring API](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/5890b47c39e2bb052c5b9c3d) call then set in the web app bot settings and pulled from there.</span><span class="sxs-lookup"><span data-stu-id="67624-178">These values can either be retrieved from the endpoint URL (app ID and version ID), or from an [authoring API](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/5890b47c39e2bb052c5b9c3d) call then set in the web app bot settings and pulled from there.</span></span>  

<span data-ttu-id="67624-179">If you are using the same endpoint subscription for more than one LUIS app, you should also include the subscription ID and a property stating that it is a shared key.</span><span class="sxs-lookup"><span data-stu-id="67624-179">If you are using the same endpoint subscription for more than one LUIS app, you should also include the subscription ID and a property stating that it is a shared key.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="67624-180">Learn more about example utterances</span><span class="sxs-lookup"><span data-stu-id="67624-180">Learn more about example utterances</span></span>](luis-how-to-add-example-utterances.md)
