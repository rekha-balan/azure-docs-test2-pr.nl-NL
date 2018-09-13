---
title: Add LUIS data to Application Insights using C# | Microsoft Docs
titleSuffix: Azure
description: Build a bot integrated with a LUIS application and Application Insights using C#.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 03/07/2018
ms.author: diberry
ms.openlocfilehash: f1efe305f5659bfab50cee13ac30d56531cc6093
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856642"
---
# <a name="add-luis-results-to-application-insights-from-a-web-app-bot"></a><span data-ttu-id="e83cf-103">Add LUIS results to Application Insights from a web app bot</span><span class="sxs-lookup"><span data-stu-id="e83cf-103">Add LUIS results to Application Insights from a web app bot</span></span>
<span data-ttu-id="e83cf-104">This tutorial adds LUIS response information to [Application Insights](https://azure.microsoft.com/services/application-insights/) telemetry data storage.</span><span class="sxs-lookup"><span data-stu-id="e83cf-104">This tutorial adds LUIS response information to [Application Insights](https://azure.microsoft.com/services/application-insights/) telemetry data storage.</span></span> <span data-ttu-id="e83cf-105">Once you have that data, you can query it with the Kusto language or PowerBi to analyze, aggregate, and report on intents, and entities of the utterance in real-time.</span><span class="sxs-lookup"><span data-stu-id="e83cf-105">Once you have that data, you can query it with the Kusto language or PowerBi to analyze, aggregate, and report on intents, and entities of the utterance in real-time.</span></span> <span data-ttu-id="e83cf-106">This analysis helps you determine if you should add or edit the intents and entities of your LUIS app.</span><span class="sxs-lookup"><span data-stu-id="e83cf-106">This analysis helps you determine if you should add or edit the intents and entities of your LUIS app.</span></span>

<span data-ttu-id="e83cf-107">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="e83cf-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
* <span data-ttu-id="e83cf-108">Add Application Insights to a web app bot</span><span class="sxs-lookup"><span data-stu-id="e83cf-108">Add Application Insights to a web app bot</span></span>
* <span data-ttu-id="e83cf-109">Capture and send LUIS query results to Application Insights</span><span class="sxs-lookup"><span data-stu-id="e83cf-109">Capture and send LUIS query results to Application Insights</span></span>
* <span data-ttu-id="e83cf-110">Query Application Insights for top intent, score, and utterance</span><span class="sxs-lookup"><span data-stu-id="e83cf-110">Query Application Insights for top intent, score, and utterance</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e83cf-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e83cf-111">Prerequisites</span></span>

* <span data-ttu-id="e83cf-112">Your LUIS web app bot from the **[previous tutorial](luis-csharp-tutorial-build-bot-framework-sample.md)** with Application Insights turned on.</span><span class="sxs-lookup"><span data-stu-id="e83cf-112">Your LUIS web app bot from the **[previous tutorial](luis-csharp-tutorial-build-bot-framework-sample.md)** with Application Insights turned on.</span></span> 
* <span data-ttu-id="e83cf-113">[Visual Studio 2017](https://www.visualstudio.com/downloads/) installed locally on  your computer.</span><span class="sxs-lookup"><span data-stu-id="e83cf-113">[Visual Studio 2017](https://www.visualstudio.com/downloads/) installed locally on  your computer.</span></span>

> [!Tip]
> <span data-ttu-id="e83cf-114">If you do not already have a subscription, you can register for a [free account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="e83cf-114">If you do not already have a subscription, you can register for a [free account](https://azure.microsoft.com/free/).</span></span>

<span data-ttu-id="e83cf-115">All of the code in this tutorial is available on the [LUIS-Samples github repository](https://github.com/Microsoft/LUIS-Samples/tree/master/documentation-samples/tutorial-web-app-bot-application-insights/csharp) and each line associated with this tutorial is commented with `//LUIS Tutorial:`.</span><span class="sxs-lookup"><span data-stu-id="e83cf-115">All of the code in this tutorial is available on the [LUIS-Samples github repository](https://github.com/Microsoft/LUIS-Samples/tree/master/documentation-samples/tutorial-web-app-bot-application-insights/csharp) and each line associated with this tutorial is commented with `//LUIS Tutorial:`.</span></span> 

## <a name="review-luis-web-app-bot"></a><span data-ttu-id="e83cf-116">Review LUIS web app bot</span><span class="sxs-lookup"><span data-stu-id="e83cf-116">Review LUIS web app bot</span></span>
<span data-ttu-id="e83cf-117">This tutorial assumes you have code that looks like the following or that you have completed the [other tutorial](luis-csharp-tutorial-build-bot-framework-sample.md):</span><span class="sxs-lookup"><span data-stu-id="e83cf-117">This tutorial assumes you have code that looks like the following or that you have completed the [other tutorial](luis-csharp-tutorial-build-bot-framework-sample.md):</span></span> 

   [!code-csharp[Web app bot with LUIS](~/samples-luis/documentation-samples/tutorial-web-app-bot/csharp/BasicLuisDialog.cs "Web app bot with LUIS")]

## <a name="application-insights-in-web-app-bot"></a><span data-ttu-id="e83cf-118">Application Insights in web app bot</span><span class="sxs-lookup"><span data-stu-id="e83cf-118">Application Insights in web app bot</span></span>
<span data-ttu-id="e83cf-119">Currently, the Application Insights service, added as part of the web app bot service creation, collects general state telemetry for the bot.</span><span class="sxs-lookup"><span data-stu-id="e83cf-119">Currently, the Application Insights service, added as part of the web app bot service creation, collects general state telemetry for the bot.</span></span> <span data-ttu-id="e83cf-120">It does not collect LUIS response information.</span><span class="sxs-lookup"><span data-stu-id="e83cf-120">It does not collect LUIS response information.</span></span> <span data-ttu-id="e83cf-121">In order to analyze and improve LUIS, you need the LUIS response information.</span><span class="sxs-lookup"><span data-stu-id="e83cf-121">In order to analyze and improve LUIS, you need the LUIS response information.</span></span>  

<span data-ttu-id="e83cf-122">In order to capture the LUIS response, the web app bot needs **[Application Insights](https://www.nuget.org/packages/Microsoft.ApplicationInsights/)** installed and configured for the project.</span><span class="sxs-lookup"><span data-stu-id="e83cf-122">In order to capture the LUIS response, the web app bot needs **[Application Insights](https://www.nuget.org/packages/Microsoft.ApplicationInsights/)** installed and configured for the project.</span></span> 

## <a name="download-web-app-bot"></a><span data-ttu-id="e83cf-123">Download web app bot</span><span class="sxs-lookup"><span data-stu-id="e83cf-123">Download web app bot</span></span>
<span data-ttu-id="e83cf-124">Use [Visual Studio 2017](https://www.visualstudio.com/downloads/) to add and configure Application Insights for the web app bot.</span><span class="sxs-lookup"><span data-stu-id="e83cf-124">Use [Visual Studio 2017](https://www.visualstudio.com/downloads/) to add and configure Application Insights for the web app bot.</span></span> <span data-ttu-id="e83cf-125">In order to use the web app bot in Visual Studio, download the web app bot code.</span><span class="sxs-lookup"><span data-stu-id="e83cf-125">In order to use the web app bot in Visual Studio, download the web app bot code.</span></span>

1. <span data-ttu-id="e83cf-126">In the Azure portal, for the web app bot, select **Build**.</span><span class="sxs-lookup"><span data-stu-id="e83cf-126">In the Azure portal, for the web app bot, select **Build**.</span></span>

    ![Select Build in portal](./media/luis-tutorial-bot-csharp-appinsights/download-build-menu.png)

2. <span data-ttu-id="e83cf-128">Select **Download zip file** and wait until the file is prepared.</span><span class="sxs-lookup"><span data-stu-id="e83cf-128">Select **Download zip file** and wait until the file is prepared.</span></span>

    ![Download zip file](./media/luis-tutorial-bot-csharp-appinsights/download-link.png)

3. <span data-ttu-id="e83cf-130">Select **Download zip file** in the pop-up window.</span><span class="sxs-lookup"><span data-stu-id="e83cf-130">Select **Download zip file** in the pop-up window.</span></span> <span data-ttu-id="e83cf-131">Remember the location on your computer, you will need it in the next section.</span><span class="sxs-lookup"><span data-stu-id="e83cf-131">Remember the location on your computer, you will need it in the next section.</span></span>

    ![Download zip file popup](./media/luis-tutorial-bot-csharp-appinsights/download-popup.png)

## <a name="open-solution-in-visual-studio-2017"></a><span data-ttu-id="e83cf-133">Open solution in Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="e83cf-133">Open solution in Visual Studio 2017</span></span>

1. <span data-ttu-id="e83cf-134">Extract the file into a folder.</span><span class="sxs-lookup"><span data-stu-id="e83cf-134">Extract the file into a folder.</span></span> 

2. <span data-ttu-id="e83cf-135">Open Visual Studio 2017 and open the solution file, `Microsoft.Bot.Sample.LuisBot.sln`.</span><span class="sxs-lookup"><span data-stu-id="e83cf-135">Open Visual Studio 2017 and open the solution file, `Microsoft.Bot.Sample.LuisBot.sln`.</span></span> <span data-ttu-id="e83cf-136">If the security warning pops up, select "OK".</span><span class="sxs-lookup"><span data-stu-id="e83cf-136">If the security warning pops up, select "OK".</span></span>

    ![Open solution in Visual Studio 2017](./media/luis-tutorial-bot-csharp-appinsights/vs-2017-security-warning.png)

3. <span data-ttu-id="e83cf-138">Visual Studio needs to add dependencies to the solution.</span><span class="sxs-lookup"><span data-stu-id="e83cf-138">Visual Studio needs to add dependencies to the solution.</span></span> <span data-ttu-id="e83cf-139">In the **Solution Explorer**, right-click on **References**, and select **Manage NuGet Packages...**.</span><span class="sxs-lookup"><span data-stu-id="e83cf-139">In the **Solution Explorer**, right-click on **References**, and select **Manage NuGet Packages...**.</span></span> 

    ![Manage NuGet packages](./media/luis-tutorial-bot-csharp-appinsights/vs-2017-manage-nuget-packages.png)

4. <span data-ttu-id="e83cf-141">The NuGet Package manager shows a list of installed packages.</span><span class="sxs-lookup"><span data-stu-id="e83cf-141">The NuGet Package manager shows a list of installed packages.</span></span> <span data-ttu-id="e83cf-142">Select **Restore** in the yellow bar.</span><span class="sxs-lookup"><span data-stu-id="e83cf-142">Select **Restore** in the yellow bar.</span></span> <span data-ttu-id="e83cf-143">Wait for the Restore process to finish.</span><span class="sxs-lookup"><span data-stu-id="e83cf-143">Wait for the Restore process to finish.</span></span>

    ![Restore NuGet packages](./media/luis-tutorial-bot-csharp-appinsights/vs-2017-restore-packages.png)

## <a name="add-application-insights-to-the-project"></a><span data-ttu-id="e83cf-145">Add Application Insights to the project</span><span class="sxs-lookup"><span data-stu-id="e83cf-145">Add Application Insights to the project</span></span>
<span data-ttu-id="e83cf-146">Install and configure Application Insights in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e83cf-146">Install and configure Application Insights in Visual Studio.</span></span> 

1. <span data-ttu-id="e83cf-147">In Visual Studio 2017, on the top menu, select **Project**, then select **Add Application Insights Telemetry...**.</span><span class="sxs-lookup"><span data-stu-id="e83cf-147">In Visual Studio 2017, on the top menu, select **Project**, then select **Add Application Insights Telemetry...**.</span></span>

2. <span data-ttu-id="e83cf-148">In the **Application Insights Configuration** window, select **Start Free**</span><span class="sxs-lookup"><span data-stu-id="e83cf-148">In the **Application Insights Configuration** window, select **Start Free**</span></span>

    ![Start configuring Application Insights](./media/luis-tutorial-bot-csharp-appinsights/vs-2017-configure-app-insights.png)

3. <span data-ttu-id="e83cf-150">Register your app with Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e83cf-150">Register your app with Application Insights.</span></span> <span data-ttu-id="e83cf-151">You may have to enter your Azure portal credentials.</span><span class="sxs-lookup"><span data-stu-id="e83cf-151">You may have to enter your Azure portal credentials.</span></span> 

4. <span data-ttu-id="e83cf-152">Visual Studio adds Application Insights to the project, displaying status as it does this.</span><span class="sxs-lookup"><span data-stu-id="e83cf-152">Visual Studio adds Application Insights to the project, displaying status as it does this.</span></span> 

    ![Application Insights status](./media/luis-tutorial-bot-csharp-appinsights/vs-2017-adding-application-insights-to-project.png)

    <span data-ttu-id="e83cf-154">When the process completes, the **Application Insights Configuration** shows the progress status.</span><span class="sxs-lookup"><span data-stu-id="e83cf-154">When the process completes, the **Application Insights Configuration** shows the progress status.</span></span> 

    ![Application Insights progress status](./media/luis-tutorial-bot-csharp-appinsights/vs-2017-configured-application-insights-to-project.png)

    <span data-ttu-id="e83cf-156">The **Enable trace collection** is red, meaning it is not enabled.</span><span class="sxs-lookup"><span data-stu-id="e83cf-156">The **Enable trace collection** is red, meaning it is not enabled.</span></span> <span data-ttu-id="e83cf-157">This tutorial doesn't use the feature.</span><span class="sxs-lookup"><span data-stu-id="e83cf-157">This tutorial doesn't use the feature.</span></span> 

## <a name="build-and-resolve-errors"></a><span data-ttu-id="e83cf-158">Build and resolve errors</span><span class="sxs-lookup"><span data-stu-id="e83cf-158">Build and resolve errors</span></span>

1. <span data-ttu-id="e83cf-159">Build the solution by selecting the **Build** menu, then select **Rebuild Solution**.</span><span class="sxs-lookup"><span data-stu-id="e83cf-159">Build the solution by selecting the **Build** menu, then select **Rebuild Solution**.</span></span> <span data-ttu-id="e83cf-160">Wait for the build to finish.</span><span class="sxs-lookup"><span data-stu-id="e83cf-160">Wait for the build to finish.</span></span> 

2. <span data-ttu-id="e83cf-161">If the build fails with `CS0104` errors, you need to fix them.</span><span class="sxs-lookup"><span data-stu-id="e83cf-161">If the build fails with `CS0104` errors, you need to fix them.</span></span> <span data-ttu-id="e83cf-162">In the `Controllers` folder, in the `MessagesController.cs file`, fix the ambiguous usage of `Activity` type by prefixing the Activity type with the Connector type.</span><span class="sxs-lookup"><span data-stu-id="e83cf-162">In the `Controllers` folder, in the `MessagesController.cs file`, fix the ambiguous usage of `Activity` type by prefixing the Activity type with the Connector type.</span></span> <span data-ttu-id="e83cf-163">To do this, change the name `Activity` on lines 22 and 36 from `Activity` to `Connector.Activity`.</span><span class="sxs-lookup"><span data-stu-id="e83cf-163">To do this, change the name `Activity` on lines 22 and 36 from `Activity` to `Connector.Activity`.</span></span> <span data-ttu-id="e83cf-164">Build the solution again.</span><span class="sxs-lookup"><span data-stu-id="e83cf-164">Build the solution again.</span></span> <span data-ttu-id="e83cf-165">There should be no more build errors.</span><span class="sxs-lookup"><span data-stu-id="e83cf-165">There should be no more build errors.</span></span>

    <span data-ttu-id="e83cf-166">The full source of that file is:</span><span class="sxs-lookup"><span data-stu-id="e83cf-166">The full source of that file is:</span></span>

    [!code-csharp[MessagesController.cs file](~/samples-luis/documentation-samples/tutorial-web-app-bot-application-insights/csharp/MessagesController.cs "MessagesController.cs file")]

## <a name="publish-project-to-azure"></a><span data-ttu-id="e83cf-167">Publish project to Azure</span><span class="sxs-lookup"><span data-stu-id="e83cf-167">Publish project to Azure</span></span>
<span data-ttu-id="e83cf-168">The **Application Insights** package is now in the project and configured correctly for your credentials in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e83cf-168">The **Application Insights** package is now in the project and configured correctly for your credentials in the Azure portal.</span></span> <span data-ttu-id="e83cf-169">The changes for the project need to be published back to Azure.</span><span class="sxs-lookup"><span data-stu-id="e83cf-169">The changes for the project need to be published back to Azure.</span></span>

1. <span data-ttu-id="e83cf-170">In the **Solution Explorer**, right-click the project name, then select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="e83cf-170">In the **Solution Explorer**, right-click the project name, then select **Publish**.</span></span>

    ![Publish project to portal](./media/luis-tutorial-bot-csharp-appinsights/vs-2017-publish.png)

2. <span data-ttu-id="e83cf-172">In the **Publish** window, select **Create new profile**.</span><span class="sxs-lookup"><span data-stu-id="e83cf-172">In the **Publish** window, select **Create new profile**.</span></span>

    ![Publish project to portal](./media/luis-tutorial-bot-csharp-appinsights/vs-2017-publish-1.png)

3. <span data-ttu-id="e83cf-174">Select **Import profile**, and select **OK**.</span><span class="sxs-lookup"><span data-stu-id="e83cf-174">Select **Import profile**, and select **OK**.</span></span>

    ![Publish project to portal](./media/luis-tutorial-bot-csharp-appinsights/vs-2017-publish-2.png)

4. <span data-ttu-id="e83cf-176">In the **Import Publish Settings File** windows, navigate to your project folder, navigate to the `PostDeployScripts` folder, select the file that ends in `.PublishSettings`, and select `Open`.</span><span class="sxs-lookup"><span data-stu-id="e83cf-176">In the **Import Publish Settings File** windows, navigate to your project folder, navigate to the `PostDeployScripts` folder, select the file that ends in `.PublishSettings`, and select `Open`.</span></span> <span data-ttu-id="e83cf-177">You have now configured publishing for this project.</span><span class="sxs-lookup"><span data-stu-id="e83cf-177">You have now configured publishing for this project.</span></span> 

5. <span data-ttu-id="e83cf-178">Publish your local source code to Bot Service by selecting the **Publish** button.</span><span class="sxs-lookup"><span data-stu-id="e83cf-178">Publish your local source code to Bot Service by selecting the **Publish** button.</span></span> <span data-ttu-id="e83cf-179">The **Output** window shows status.</span><span class="sxs-lookup"><span data-stu-id="e83cf-179">The **Output** window shows status.</span></span> <span data-ttu-id="e83cf-180">The rest of the tutorial is completed in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e83cf-180">The rest of the tutorial is completed in the Azure portal.</span></span> <span data-ttu-id="e83cf-181">Close Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="e83cf-181">Close Visual Studio 2017.</span></span> 

## <a name="open-three-browser-tabs"></a><span data-ttu-id="e83cf-182">Open three browser tabs</span><span class="sxs-lookup"><span data-stu-id="e83cf-182">Open three browser tabs</span></span>
<span data-ttu-id="e83cf-183">In the Azure portal, find the web app bot and open it.</span><span class="sxs-lookup"><span data-stu-id="e83cf-183">In the Azure portal, find the web app bot and open it.</span></span> <span data-ttu-id="e83cf-184">The following steps use three different views of the web app bot.</span><span class="sxs-lookup"><span data-stu-id="e83cf-184">The following steps use three different views of the web app bot.</span></span> <span data-ttu-id="e83cf-185">It may be easier to have three separate tabs open in the browser:</span><span class="sxs-lookup"><span data-stu-id="e83cf-185">It may be easier to have three separate tabs open in the browser:</span></span> 
  
>  * <span data-ttu-id="e83cf-186">Test in Web Chat</span><span class="sxs-lookup"><span data-stu-id="e83cf-186">Test in Web Chat</span></span>
>  * <span data-ttu-id="e83cf-187">Build/Open online code editor -> App Service Editor</span><span class="sxs-lookup"><span data-stu-id="e83cf-187">Build/Open online code editor -> App Service Editor</span></span>
>  * <span data-ttu-id="e83cf-188">App Service Editor/Open Kudu console -> Diagnostic Console</span><span class="sxs-lookup"><span data-stu-id="e83cf-188">App Service Editor/Open Kudu console -> Diagnostic Console</span></span>

## <a name="modify-basicluisdialogcs-code"></a><span data-ttu-id="e83cf-189">Modify BasicLuisDialog.cs code</span><span class="sxs-lookup"><span data-stu-id="e83cf-189">Modify BasicLuisDialog.cs code</span></span>

1. <span data-ttu-id="e83cf-190">In the **App Service Editor** browser tab, open the `BasicLuisDialog.cs` file.</span><span class="sxs-lookup"><span data-stu-id="e83cf-190">In the **App Service Editor** browser tab, open the `BasicLuisDialog.cs` file.</span></span>

2. <span data-ttu-id="e83cf-191">Add the following NuGet dependency under the existing `using` lines:</span><span class="sxs-lookup"><span data-stu-id="e83cf-191">Add the following NuGet dependency under the existing `using` lines:</span></span>

   [!code-csharp[Add using statement](~/samples-luis/documentation-samples/tutorial-web-app-bot-application-insights/csharp/BasicLuisDialog.cs?range=11-12 "Add using statement")]

3. <span data-ttu-id="e83cf-192">Add the `LogToApplicationInsights` function:</span><span class="sxs-lookup"><span data-stu-id="e83cf-192">Add the `LogToApplicationInsights` function:</span></span>

   [!code-csharp[Add the LogToApplicationInsights function](~/samples-luis/documentation-samples/tutorial-web-app-bot-application-insights/csharp/BasicLuisDialog.cs?range=61-92 "Add the LogToApplicationInsights function")]

    <span data-ttu-id="e83cf-193">The Application Insights instrumentation key is already in the web app bot's application setting named `BotDevInsightsKey`.</span><span class="sxs-lookup"><span data-stu-id="e83cf-193">The Application Insights instrumentation key is already in the web app bot's application setting named `BotDevInsightsKey`.</span></span> 

    <span data-ttu-id="e83cf-194">The last line of the function adds the data to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e83cf-194">The last line of the function adds the data to Application Insights.</span></span> <span data-ttu-id="e83cf-195">The trace's name is `LUIS`, a unique name apart from any other telemetry data collected by this web app bot.</span><span class="sxs-lookup"><span data-stu-id="e83cf-195">The trace's name is `LUIS`, a unique name apart from any other telemetry data collected by this web app bot.</span></span> <span data-ttu-id="e83cf-196">All the properties are also prefixed with `LUIS_` so you can see what data this tutorial adds compared to information that is given by the web app bot.</span><span class="sxs-lookup"><span data-stu-id="e83cf-196">All the properties are also prefixed with `LUIS_` so you can see what data this tutorial adds compared to information that is given by the web app bot.</span></span>

4. <span data-ttu-id="e83cf-197">Call the `LogToApplicationInsights` function at the top of the `ShowLuisResult` function:</span><span class="sxs-lookup"><span data-stu-id="e83cf-197">Call the `LogToApplicationInsights` function at the top of the `ShowLuisResult` function:</span></span>

   [!code-csharp[Use the LogToApplicationInsights function](~/samples-luis/documentation-samples/tutorial-web-app-bot-application-insights/csharp/BasicLuisDialog.cs?range=114-115 "Use the LogToApplicationInsights function")]

## <a name="build-web-app-bot"></a><span data-ttu-id="e83cf-198">Build web app bot</span><span class="sxs-lookup"><span data-stu-id="e83cf-198">Build web app bot</span></span>
1. <span data-ttu-id="e83cf-199">Build the web app bot in one of two ways.</span><span class="sxs-lookup"><span data-stu-id="e83cf-199">Build the web app bot in one of two ways.</span></span> <span data-ttu-id="e83cf-200">The first method is to right-click on `build.cmd` in the **App Service Editor**, then select **Run from Console**.</span><span class="sxs-lookup"><span data-stu-id="e83cf-200">The first method is to right-click on `build.cmd` in the **App Service Editor**, then select **Run from Console**.</span></span> <span data-ttu-id="e83cf-201">The output of the console displays and completes with `Finished successfully.`</span><span class="sxs-lookup"><span data-stu-id="e83cf-201">The output of the console displays and completes with `Finished successfully.`</span></span>

2. <span data-ttu-id="e83cf-202">If this doesn't complete successfully, you need to open the console, navigate to the  script, and run it using the following steps.</span><span class="sxs-lookup"><span data-stu-id="e83cf-202">If this doesn't complete successfully, you need to open the console, navigate to the  script, and run it using the following steps.</span></span> <span data-ttu-id="e83cf-203">In the **App Service Editor**, on the top blue bar, select the name of your bot, then select **Open Kudu Console** in the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="e83cf-203">In the **App Service Editor**, on the top blue bar, select the name of your bot, then select **Open Kudu Console** in the drop-down list.</span></span>

    ![Open Kudu Console](./media/luis-tutorial-bot-csharp-appinsights/open-kudu-console.png)

3. <span data-ttu-id="e83cf-205">In the console window, enter the following command:</span><span class="sxs-lookup"><span data-stu-id="e83cf-205">In the console window, enter the following command:</span></span>

    ```
    cd site\wwwroot && build.cmd
    ```

    <span data-ttu-id="e83cf-206">Wait for the build to complete with `Finished successfully.`</span><span class="sxs-lookup"><span data-stu-id="e83cf-206">Wait for the build to complete with `Finished successfully.`</span></span>

## <a name="test-the-web-app-bot"></a><span data-ttu-id="e83cf-207">Test the web app bot</span><span class="sxs-lookup"><span data-stu-id="e83cf-207">Test the web app bot</span></span>

1. <span data-ttu-id="e83cf-208">To test your web app bot, open the **Test in Web Chat** feature in the portal.</span><span class="sxs-lookup"><span data-stu-id="e83cf-208">To test your web app bot, open the **Test in Web Chat** feature in the portal.</span></span> 

2. <span data-ttu-id="e83cf-209">Enter the phrase `Coffee bar on please`.</span><span class="sxs-lookup"><span data-stu-id="e83cf-209">Enter the phrase `Coffee bar on please`.</span></span>  

    ![Test web app bot in chat](./media/luis-tutorial-bot-csharp-appinsights/test-in-web-chat.png)

3. <span data-ttu-id="e83cf-211">You should see no difference in the chatbot response.</span><span class="sxs-lookup"><span data-stu-id="e83cf-211">You should see no difference in the chatbot response.</span></span> <span data-ttu-id="e83cf-212">The change is sending data to Application Insights, not in the bot responses.</span><span class="sxs-lookup"><span data-stu-id="e83cf-212">The change is sending data to Application Insights, not in the bot responses.</span></span> <span data-ttu-id="e83cf-213">Enter a few more utterances so there is a little more data in Application Insights:</span><span class="sxs-lookup"><span data-stu-id="e83cf-213">Enter a few more utterances so there is a little more data in Application Insights:</span></span>

```
Please deliver a pizza
Turn off all the lights
Turn on the hall light
```

## <a name="view-luis-entries-in-application-insights"></a><span data-ttu-id="e83cf-214">View LUIS entries in Application Insights</span><span class="sxs-lookup"><span data-stu-id="e83cf-214">View LUIS entries in Application Insights</span></span>
<span data-ttu-id="e83cf-215">Open Application Insights to see the LUIS entries.</span><span class="sxs-lookup"><span data-stu-id="e83cf-215">Open Application Insights to see the LUIS entries.</span></span> 

1. <span data-ttu-id="e83cf-216">In the portal, select **All resources** then filter by the web app bot name.</span><span class="sxs-lookup"><span data-stu-id="e83cf-216">In the portal, select **All resources** then filter by the web app bot name.</span></span> <span data-ttu-id="e83cf-217">Click on the resource with the type **Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="e83cf-217">Click on the resource with the type **Application Insights**.</span></span> <span data-ttu-id="e83cf-218">The icon for Application Insights is a light bulb.</span><span class="sxs-lookup"><span data-stu-id="e83cf-218">The icon for Application Insights is a light bulb.</span></span> 

    ![Search for app insights](./media/luis-tutorial-bot-csharp-appinsights/portal-service-list-app-insights.png)

2. <span data-ttu-id="e83cf-220">When the resource opens, click on the **Search** icon of the magnifying glass in the far right panel.</span><span class="sxs-lookup"><span data-stu-id="e83cf-220">When the resource opens, click on the **Search** icon of the magnifying glass in the far right panel.</span></span> <span data-ttu-id="e83cf-221">A new panel to the right displays.</span><span class="sxs-lookup"><span data-stu-id="e83cf-221">A new panel to the right displays.</span></span> <span data-ttu-id="e83cf-222">Depending on how much telemetry data is found, the panel may take a second to display.</span><span class="sxs-lookup"><span data-stu-id="e83cf-222">Depending on how much telemetry data is found, the panel may take a second to display.</span></span> <span data-ttu-id="e83cf-223">Search for `LUIS`.</span><span class="sxs-lookup"><span data-stu-id="e83cf-223">Search for `LUIS`.</span></span> <span data-ttu-id="e83cf-224">The list is narrowed to just LUIS query results added with this tutorial.</span><span class="sxs-lookup"><span data-stu-id="e83cf-224">The list is narrowed to just LUIS query results added with this tutorial.</span></span>

    ![Search for traces](./media/luis-tutorial-bot-csharp-appinsights/portal-service-list-app-insights-search-luis-trace.png)

3. <span data-ttu-id="e83cf-226">Select the top entry.</span><span class="sxs-lookup"><span data-stu-id="e83cf-226">Select the top entry.</span></span> <span data-ttu-id="e83cf-227">A new window displays more detailed data including the custom data for the LUIS query at the far-right.</span><span class="sxs-lookup"><span data-stu-id="e83cf-227">A new window displays more detailed data including the custom data for the LUIS query at the far-right.</span></span> <span data-ttu-id="e83cf-228">The data includes the top intent, and its score.</span><span class="sxs-lookup"><span data-stu-id="e83cf-228">The data includes the top intent, and its score.</span></span>

    ![Review trace item](./media/luis-tutorial-bot-csharp-appinsights/portal-service-list-app-insights-search-luis-trace-item.png)

    <span data-ttu-id="e83cf-230">When you are done, select the far-right top **X** to return to the list of dependency items.</span><span class="sxs-lookup"><span data-stu-id="e83cf-230">When you are done, select the far-right top **X** to return to the list of dependency items.</span></span> 


> [!Tip]
> <span data-ttu-id="e83cf-231">If you want to save the dependency list and return to it later, click on **...More** and click **Save favorite**.</span><span class="sxs-lookup"><span data-stu-id="e83cf-231">If you want to save the dependency list and return to it later, click on **...More** and click **Save favorite**.</span></span>

## <a name="query-application-insights-for-intent-score-and-utterance"></a><span data-ttu-id="e83cf-232">Query Application Insights for intent, score, and utterance</span><span class="sxs-lookup"><span data-stu-id="e83cf-232">Query Application Insights for intent, score, and utterance</span></span>
<span data-ttu-id="e83cf-233">Application Insights gives you the power to query the data with the [Kusto](https://docs.microsoft.com/azure/application-insights/app-insights-analytics#query-data-in-analytics) language, as well as export it to [PowerBI](https://powerbi.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="e83cf-233">Application Insights gives you the power to query the data with the [Kusto](https://docs.microsoft.com/azure/application-insights/app-insights-analytics#query-data-in-analytics) language, as well as export it to [PowerBI](https://powerbi.microsoft.com).</span></span> 

1. <span data-ttu-id="e83cf-234">Click on **Analytics** at the top of the dependency listing, above the filter box.</span><span class="sxs-lookup"><span data-stu-id="e83cf-234">Click on **Analytics** at the top of the dependency listing, above the filter box.</span></span> 

    ![Analytics button](./media/luis-tutorial-bot-csharp-appinsights/portal-service-list-app-insights-search-luis-analytics-button.png)

2. <span data-ttu-id="e83cf-236">A new window opens with a query window at the top and a data table window below that.</span><span class="sxs-lookup"><span data-stu-id="e83cf-236">A new window opens with a query window at the top and a data table window below that.</span></span> <span data-ttu-id="e83cf-237">If you have used databases before, this arrangement is familiar.</span><span class="sxs-lookup"><span data-stu-id="e83cf-237">If you have used databases before, this arrangement is familiar.</span></span> <span data-ttu-id="e83cf-238">The query includes all items from the last 24 hours beginning with the name `LUIS`.</span><span class="sxs-lookup"><span data-stu-id="e83cf-238">The query includes all items from the last 24 hours beginning with the name `LUIS`.</span></span> <span data-ttu-id="e83cf-239">The **CustomDimensions** column has the LUIS query results as name/value pairs.</span><span class="sxs-lookup"><span data-stu-id="e83cf-239">The **CustomDimensions** column has the LUIS query results as name/value pairs.</span></span>

    ![Default analytics report](./media/luis-tutorial-bot-csharp-appinsights/analytics-query-1.png)

3. <span data-ttu-id="e83cf-241">To pull out the top intent, score, and utterance, add the following just above the last line in the query window:</span><span class="sxs-lookup"><span data-stu-id="e83cf-241">To pull out the top intent, score, and utterance, add the following just above the last line in the query window:</span></span>

    ```SQL
    | extend topIntent = tostring(customDimensions.LUIS_topScoringIntent)
    | extend score = todouble(customDimensions.LUIS_topScoringIntentScore)
    | extend utterance = tostring(customDimensions.LUIS_query)
    ```

4. <span data-ttu-id="e83cf-242">Run the query.</span><span class="sxs-lookup"><span data-stu-id="e83cf-242">Run the query.</span></span> <span data-ttu-id="e83cf-243">Scroll to the far right in the data table.</span><span class="sxs-lookup"><span data-stu-id="e83cf-243">Scroll to the far right in the data table.</span></span> <span data-ttu-id="e83cf-244">The new columns of topIntent, score, and utterance are available.</span><span class="sxs-lookup"><span data-stu-id="e83cf-244">The new columns of topIntent, score, and utterance are available.</span></span> <span data-ttu-id="e83cf-245">Click on the topIntent column to sort.</span><span class="sxs-lookup"><span data-stu-id="e83cf-245">Click on the topIntent column to sort.</span></span>

    ![Custom analytics report](./media/luis-tutorial-bot-csharp-appinsights/analytics-query-2.png)


<span data-ttu-id="e83cf-247">Learn more about the [Kusto query language](https://docs.loganalytics.io/docs/Learn/Getting-Started/Getting-started-with-queries) or [export the data to PowerBi](https://docs.microsoft.com/azure/application-insights/app-insights-export-power-bi).</span><span class="sxs-lookup"><span data-stu-id="e83cf-247">Learn more about the [Kusto query language](https://docs.loganalytics.io/docs/Learn/Getting-Started/Getting-started-with-queries) or [export the data to PowerBi](https://docs.microsoft.com/azure/application-insights/app-insights-export-power-bi).</span></span> 


## <a name="learn-more-about-bot-framework"></a><span data-ttu-id="e83cf-248">Learn more about Bot Framework</span><span class="sxs-lookup"><span data-stu-id="e83cf-248">Learn more about Bot Framework</span></span>
<span data-ttu-id="e83cf-249">Learn more about [Bot Framework](https://dev.botframework.com/).</span><span class="sxs-lookup"><span data-stu-id="e83cf-249">Learn more about [Bot Framework](https://dev.botframework.com/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e83cf-250">Next steps</span><span class="sxs-lookup"><span data-stu-id="e83cf-250">Next steps</span></span>

<span data-ttu-id="e83cf-251">Other information you may want to add to the application insights data includes app ID, version ID, last model change date, last train date, last publish date.</span><span class="sxs-lookup"><span data-stu-id="e83cf-251">Other information you may want to add to the application insights data includes app ID, version ID, last model change date, last train date, last publish date.</span></span> <span data-ttu-id="e83cf-252">These values can either be retrieved from the endpoint URL (app ID and version ID), or from an [authoring API](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/5890b47c39e2bb052c5b9c3d) call then set in the web app bot settings and pulled from there.</span><span class="sxs-lookup"><span data-stu-id="e83cf-252">These values can either be retrieved from the endpoint URL (app ID and version ID), or from an [authoring API](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/5890b47c39e2bb052c5b9c3d) call then set in the web app bot settings and pulled from there.</span></span>  

<span data-ttu-id="e83cf-253">If you are using the same endpoint subscription for more than one LUIS app, you should also include the subscription ID and a property stating that it is a shared key.</span><span class="sxs-lookup"><span data-stu-id="e83cf-253">If you are using the same endpoint subscription for more than one LUIS app, you should also include the subscription ID and a property stating that it is a shared key.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="e83cf-254">Learn more about example utterances</span><span class="sxs-lookup"><span data-stu-id="e83cf-254">Learn more about example utterances</span></span>](luis-how-to-add-example-utterances.md)
