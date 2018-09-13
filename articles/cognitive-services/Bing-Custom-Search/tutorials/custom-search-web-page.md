---
title: 'Bing Custom Search: Create a custom search web page | Microsoft Docs'
description: Describes how to configure a custom search instance and integrate it into a web page
services: cognitive-services
author: brapel
manager: ehansen
ms.service: cognitive-services
ms.component: bing-custom-search
ms.topic: article
ms.date: 10/16/2017
ms.author: v-brapel
ms.openlocfilehash: 1f9b689ac6127bc2f7d1e810356ae9a23b8e0996
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969195"
---
# <a name="build-a-custom-search-web-page"></a><span data-ttu-id="4b473-103">Build a Custom Search web page</span><span class="sxs-lookup"><span data-stu-id="4b473-103">Build a Custom Search web page</span></span>
<span data-ttu-id="4b473-104">Bing Custom Search enables you to create tailored search experiences for topics that you care about.</span><span class="sxs-lookup"><span data-stu-id="4b473-104">Bing Custom Search enables you to create tailored search experiences for topics that you care about.</span></span> <span data-ttu-id="4b473-105">For example, if you own a martial arts website that provides a search experience, you can specify the domains, subsites, and webpages that Bing searches.</span><span class="sxs-lookup"><span data-stu-id="4b473-105">For example, if you own a martial arts website that provides a search experience, you can specify the domains, subsites, and webpages that Bing searches.</span></span> <span data-ttu-id="4b473-106">Your users see search results tailored to the content they care about instead of paging through general search results that may contain irrelevant content.</span><span class="sxs-lookup"><span data-stu-id="4b473-106">Your users see search results tailored to the content they care about instead of paging through general search results that may contain irrelevant content.</span></span> 

<span data-ttu-id="4b473-107">This tutorial demonstrates how to configure a custom search instance and integrate it into a new web page.</span><span class="sxs-lookup"><span data-stu-id="4b473-107">This tutorial demonstrates how to configure a custom search instance and integrate it into a new web page.</span></span>

<span data-ttu-id="4b473-108">The tasks covered are:</span><span class="sxs-lookup"><span data-stu-id="4b473-108">The tasks covered are:</span></span>

> [!div class="checklist"]
> - <span data-ttu-id="4b473-109">Create a custom search instance</span><span class="sxs-lookup"><span data-stu-id="4b473-109">Create a custom search instance</span></span>
> - <span data-ttu-id="4b473-110">Add active entries</span><span class="sxs-lookup"><span data-stu-id="4b473-110">Add active entries</span></span>
> - <span data-ttu-id="4b473-111">Add blocked entries</span><span class="sxs-lookup"><span data-stu-id="4b473-111">Add blocked entries</span></span>
> - <span data-ttu-id="4b473-112">Add pinned entries</span><span class="sxs-lookup"><span data-stu-id="4b473-112">Add pinned entries</span></span>
> - <span data-ttu-id="4b473-113">Integrate custom search into a web page</span><span class="sxs-lookup"><span data-stu-id="4b473-113">Integrate custom search into a web page</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b473-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4b473-114">Prerequisites</span></span>
- <span data-ttu-id="4b473-115">To follow along with the tutorial, you need a subscription key for the Bing Custom Search API.</span><span class="sxs-lookup"><span data-stu-id="4b473-115">To follow along with the tutorial, you need a subscription key for the Bing Custom Search API.</span></span>  <span data-ttu-id="4b473-116">To get a key, see [Try Cognitive Services](https://azure.microsoft.com/try/cognitive-services/?api=bing-custom-search).</span><span class="sxs-lookup"><span data-stu-id="4b473-116">To get a key, see [Try Cognitive Services](https://azure.microsoft.com/try/cognitive-services/?api=bing-custom-search).</span></span>
- <span data-ttu-id="4b473-117">If you don’t already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="4b473-117">If you don’t already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span>

## <a name="create-a-custom-search-instance"></a><span data-ttu-id="4b473-118">Create a custom search instance</span><span class="sxs-lookup"><span data-stu-id="4b473-118">Create a custom search instance</span></span>
<span data-ttu-id="4b473-119">To create a Bing Custom Search instance:</span><span class="sxs-lookup"><span data-stu-id="4b473-119">To create a Bing Custom Search instance:</span></span>

1.  <span data-ttu-id="4b473-120">Open an internet browser.</span><span class="sxs-lookup"><span data-stu-id="4b473-120">Open an internet browser.</span></span>
2.  <span data-ttu-id="4b473-121">Navigate to the custom search [portal](https://customsearch.ai).</span><span class="sxs-lookup"><span data-stu-id="4b473-121">Navigate to the custom search [portal](https://customsearch.ai).</span></span>
3.  <span data-ttu-id="4b473-122">Sign in to the portal using a Microsoft account (MSA).</span><span class="sxs-lookup"><span data-stu-id="4b473-122">Sign in to the portal using a Microsoft account (MSA).</span></span> <span data-ttu-id="4b473-123">If you don’t have an MSA, click **Create a Microsoft account**.</span><span class="sxs-lookup"><span data-stu-id="4b473-123">If you don’t have an MSA, click **Create a Microsoft account**.</span></span> <span data-ttu-id="4b473-124">If it’s your first time using the portal, it will ask for permissions to access your data.</span><span class="sxs-lookup"><span data-stu-id="4b473-124">If it’s your first time using the portal, it will ask for permissions to access your data.</span></span> <span data-ttu-id="4b473-125">Click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="4b473-125">Click **Yes**.</span></span>
4.  <span data-ttu-id="4b473-126">After signing in, click **New custom search**.</span><span class="sxs-lookup"><span data-stu-id="4b473-126">After signing in, click **New custom search**.</span></span> <span data-ttu-id="4b473-127">In the **Create a new custom search instance** window, enter a name that’s meaningful and describes the type of content the search returns.</span><span class="sxs-lookup"><span data-stu-id="4b473-127">In the **Create a new custom search instance** window, enter a name that’s meaningful and describes the type of content the search returns.</span></span> <span data-ttu-id="4b473-128">You can change the name at any time.</span><span class="sxs-lookup"><span data-stu-id="4b473-128">You can change the name at any time.</span></span>
 
    ![Screen shot of the Create a new custom search instance box](../media/newCustomSrch.png)

5.  <span data-ttu-id="4b473-130">Click OK, specify a URL and whether to include subpages of the base page:</span><span class="sxs-lookup"><span data-stu-id="4b473-130">Click OK, specify a URL and whether to include subpages of the base page:</span></span>

    ![Screen shot of URL definition page](../media/newCustomSrch1-a.png)

## <a name="add-active-entries"></a><span data-ttu-id="4b473-132">Add active entries</span><span class="sxs-lookup"><span data-stu-id="4b473-132">Add active entries</span></span>
<span data-ttu-id="4b473-133">To include results from specific sites or URLs, add them to the **Active** tab.</span><span class="sxs-lookup"><span data-stu-id="4b473-133">To include results from specific sites or URLs, add them to the **Active** tab.</span></span>

1.  <span data-ttu-id="4b473-134">In the **Definition Editor**, click the **Active** tab and enter the URL of one or more sites you want to include in your search.</span><span class="sxs-lookup"><span data-stu-id="4b473-134">In the **Definition Editor**, click the **Active** tab and enter the URL of one or more sites you want to include in your search.</span></span>

    ![Screen shot of the Definition Editor active tab](../media/customSrchEditor.png)

2.  <span data-ttu-id="4b473-136">To confirm that your instance returns results, enter a query in the preview pane on the right.</span><span class="sxs-lookup"><span data-stu-id="4b473-136">To confirm that your instance returns results, enter a query in the preview pane on the right.</span></span> <span data-ttu-id="4b473-137">Bing returns results only for public sites that it has indexed.</span><span class="sxs-lookup"><span data-stu-id="4b473-137">Bing returns results only for public sites that it has indexed.</span></span>

## <a name="add-blocked-entries"></a><span data-ttu-id="4b473-138">Add blocked entries</span><span class="sxs-lookup"><span data-stu-id="4b473-138">Add blocked entries</span></span>
<span data-ttu-id="4b473-139">To exclude results from specific sites or URLs, add them to the **Blocked** tab.</span><span class="sxs-lookup"><span data-stu-id="4b473-139">To exclude results from specific sites or URLs, add them to the **Blocked** tab.</span></span>

1. <span data-ttu-id="4b473-140">In the **Definition Editor**, click the **Blocked** tab and enter the URL of one or more sites you want to exclude from your search.</span><span class="sxs-lookup"><span data-stu-id="4b473-140">In the **Definition Editor**, click the **Blocked** tab and enter the URL of one or more sites you want to exclude from your search.</span></span>

    ![Screen shot of the Definition Editor blocked tab](../media/blockedCustomSrch.png)


2. <span data-ttu-id="4b473-142">To confirm that your instance doesn't return results from the blocked sites, enter a query in the preview pane on the right.</span><span class="sxs-lookup"><span data-stu-id="4b473-142">To confirm that your instance doesn't return results from the blocked sites, enter a query in the preview pane on the right.</span></span> 

## <a name="add-pinned-entries"></a><span data-ttu-id="4b473-143">Add pinned entries</span><span class="sxs-lookup"><span data-stu-id="4b473-143">Add pinned entries</span></span>
<span data-ttu-id="4b473-144">To pin a specific webpage to the top of the search results, add the webpage and query term to the **Pinned** tab.  The **Pinned** tab contains a list of webpage and query term pairs that specify the webpage that appears as the top result for a specific query.</span><span class="sxs-lookup"><span data-stu-id="4b473-144">To pin a specific webpage to the top of the search results, add the webpage and query term to the **Pinned** tab.  The **Pinned** tab contains a list of webpage and query term pairs that specify the webpage that appears as the top result for a specific query.</span></span> <span data-ttu-id="4b473-145">The user’s query term must exactly match the pinned query term for the webpage to be pinned to the top.</span><span class="sxs-lookup"><span data-stu-id="4b473-145">The user’s query term must exactly match the pinned query term for the webpage to be pinned to the top.</span></span>

1. <span data-ttu-id="4b473-146">In the **Definition Editor**, click the **Pinned** tab and enter the webpage and query term of the webpage that should return as the top result.</span><span class="sxs-lookup"><span data-stu-id="4b473-146">In the **Definition Editor**, click the **Pinned** tab and enter the webpage and query term of the webpage that should return as the top result.</span></span>

    ![Screen shot of the Definition Editor pinned tab](../media/pinnedCustomSrch.png)

2. <span data-ttu-id="4b473-148">To confirm that your instance returns the specified webpage as the top result, enter the query term you pinned in the preview pane on the right.</span><span class="sxs-lookup"><span data-stu-id="4b473-148">To confirm that your instance returns the specified webpage as the top result, enter the query term you pinned in the preview pane on the right.</span></span>

## <a name="configure-hosted-ui"></a><span data-ttu-id="4b473-149">Configure Hosted UI</span><span class="sxs-lookup"><span data-stu-id="4b473-149">Configure Hosted UI</span></span>
<span data-ttu-id="4b473-150">Custom Search provides a hosted UI to render the JSON response of your custom search instance.</span><span class="sxs-lookup"><span data-stu-id="4b473-150">Custom Search provides a hosted UI to render the JSON response of your custom search instance.</span></span>  <span data-ttu-id="4b473-151">To define your UI experience:</span><span class="sxs-lookup"><span data-stu-id="4b473-151">To define your UI experience:</span></span>

1. <span data-ttu-id="4b473-152">Click the **Hosted UI** tab.</span><span class="sxs-lookup"><span data-stu-id="4b473-152">Click the **Hosted UI** tab.</span></span>
2. <span data-ttu-id="4b473-153">Select a layout.</span><span class="sxs-lookup"><span data-stu-id="4b473-153">Select a layout.</span></span>

    ![Screen shot of the Hosted UI select layout step](./media/custom-search-hosted-ui-select-layout.png)

3. <span data-ttu-id="4b473-155">Select a color theme.</span><span class="sxs-lookup"><span data-stu-id="4b473-155">Select a color theme.</span></span>

    ![Screen shot of the Hosted UI select layout step](./media/custom-search-hosted-ui-select-color-theme.png)

4. <span data-ttu-id="4b473-157">Specify additional configuration options.</span><span class="sxs-lookup"><span data-stu-id="4b473-157">Specify additional configuration options.</span></span>

    ![Screen shot of the Hosted UI additional configurations step](./media/custom-search-hosted-ui-additional-configurations.png)

5. <span data-ttu-id="4b473-159">Paste your **Subscription key**.</span><span class="sxs-lookup"><span data-stu-id="4b473-159">Paste your **Subscription key**.</span></span> <span data-ttu-id="4b473-160">See [Try Cognitive Services](https://azure.microsoft.com/try/cognitive-services/?api=bing-custom-search-api).</span><span class="sxs-lookup"><span data-stu-id="4b473-160">See [Try Cognitive Services](https://azure.microsoft.com/try/cognitive-services/?api=bing-custom-search-api).</span></span>

    ![Screen shot of the Hosted UI additional configurations step](./media/custom-search-hosted-ui-subscription-key.png)

[!INCLUDE [publish or revert](../includes/publish-revert.md)]

<a name="consuminghostedui"></a>
## <a name="consuming-hosted-ui"></a><span data-ttu-id="4b473-162">Consuming Hosted UI</span><span class="sxs-lookup"><span data-stu-id="4b473-162">Consuming Hosted UI</span></span>
<span data-ttu-id="4b473-163">There are two ways to consume the hosted UI.</span><span class="sxs-lookup"><span data-stu-id="4b473-163">There are two ways to consume the hosted UI.</span></span>  

- <span data-ttu-id="4b473-164">Option 1: Integrate the provided JavaScript snippet into your application.</span><span class="sxs-lookup"><span data-stu-id="4b473-164">Option 1: Integrate the provided JavaScript snippet into your application.</span></span>
- <span data-ttu-id="4b473-165">Option 2: Use the HTML Endpoint provided.</span><span class="sxs-lookup"><span data-stu-id="4b473-165">Option 2: Use the HTML Endpoint provided.</span></span>

<span data-ttu-id="4b473-166">The remainder of this tutorial illustrates **Option 1: Javascript snippet**.</span><span class="sxs-lookup"><span data-stu-id="4b473-166">The remainder of this tutorial illustrates **Option 1: Javascript snippet**.</span></span>  

## <a name="set-up-your-visual-studio-solution"></a><span data-ttu-id="4b473-167">Set up your Visual Studio solution</span><span class="sxs-lookup"><span data-stu-id="4b473-167">Set up your Visual Studio solution</span></span>
1. <span data-ttu-id="4b473-168">Open **Visual Studio** on your computer.</span><span class="sxs-lookup"><span data-stu-id="4b473-168">Open **Visual Studio** on your computer.</span></span>
2. <span data-ttu-id="4b473-169">On the **File** menu, select **New**, and then choose **Project**.</span><span class="sxs-lookup"><span data-stu-id="4b473-169">On the **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="4b473-170">In the **New Project** window, select **Visual C# / Web / ASP.NET Core Web Application**, name your project, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="4b473-170">In the **New Project** window, select **Visual C# / Web / ASP.NET Core Web Application**, name your project, and then click **OK**.</span></span>
   
    ![Screen shot of new project window](./media/custom-search-new-project.png)

4. <span data-ttu-id="4b473-172">In the **New ASP.NET Core Web Application** window, select **Web Application** and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="4b473-172">In the **New ASP.NET Core Web Application** window, select **Web Application** and click **OK**.</span></span>
    
    ![Screen shot of new project window](./media/custom-search-new-webapp.png)

## <a name="edit-indexcshtml"></a><span data-ttu-id="4b473-174">Edit index.cshtml</span><span class="sxs-lookup"><span data-stu-id="4b473-174">Edit index.cshtml</span></span>
1. <span data-ttu-id="4b473-175">In the **Solution Explorer**, expand **Pages** and double-click **index.cshtml** to open the file.</span><span class="sxs-lookup"><span data-stu-id="4b473-175">In the **Solution Explorer**, expand **Pages** and double-click **index.cshtml** to open the file.</span></span>

    ![Screen shot of solution explorer with pages expanded and index.cshtml selected](./media/custom-search-visual-studio-webapp-solution-explorer-index.png)

2. <span data-ttu-id="4b473-177">In index.cshtml, delete everything starting from line 7 and below.</span><span class="sxs-lookup"><span data-stu-id="4b473-177">In index.cshtml, delete everything starting from line 7 and below.</span></span>
    
    ``` razor
    @page
    @model IndexModel
    @{
        ViewData["Title"] = "Home page";
    }    
    ```

3. <span data-ttu-id="4b473-178">Add a line break element and a div to act as a container.</span><span class="sxs-lookup"><span data-stu-id="4b473-178">Add a line break element and a div to act as a container.</span></span>

    ``` html
    @page
    @model IndexModel
    @{
        ViewData["Title"] = "Home page";
    }
    <br />
    <div id="customSearch"></div>
    ```

4. <span data-ttu-id="4b473-179">From the **Hosted UI** tab, scroll down to the section titled **Consuming the UI**.</span><span class="sxs-lookup"><span data-stu-id="4b473-179">From the **Hosted UI** tab, scroll down to the section titled **Consuming the UI**.</span></span> <span data-ttu-id="4b473-180">Copy the JavaScript snippet.</span><span class="sxs-lookup"><span data-stu-id="4b473-180">Copy the JavaScript snippet.</span></span>

    ![Screen shot of the Hosted UI save button](./media/custom-search-hosted-ui-consuming-ui.png)

5. <span data-ttu-id="4b473-182">Paste the script element into the container you added.</span><span class="sxs-lookup"><span data-stu-id="4b473-182">Paste the script element into the container you added.</span></span>

    ``` html
    @page
    @model IndexModel
    @{
        ViewData["Title"] = "Home page";
    }
    <br />
    <div id="customSearch">
        <script type="text/javascript"
                id="bcs_js_snippet"
                src="https://ui.customsearch.ai/api/ux/render?customConfig=<YOUR-CUSTOM-CONFIG-ID>&market=en-US&safeSearch=Moderate">
        </script>
    </div>
    ```

6. <span data-ttu-id="4b473-183">In the **Solution Explorer**, right click on **wwwroot** and click **View in Browser**.</span><span class="sxs-lookup"><span data-stu-id="4b473-183">In the **Solution Explorer**, right click on **wwwroot** and click **View in Browser**.</span></span>

    ![Screen shot of solution explorer selecting View in Browser from the wwwroot context menu](./media/custom-search-webapp-view-in-browser.png)

<span data-ttu-id="4b473-185">Your new custom search web page should look similar to this:</span><span class="sxs-lookup"><span data-stu-id="4b473-185">Your new custom search web page should look similar to this:</span></span>

![Screen shot of custom search web page](./media/custom-search-webapp-browse-index.png)

<span data-ttu-id="4b473-187">Performing a search renders results like this.</span><span class="sxs-lookup"><span data-stu-id="4b473-187">Performing a search renders results like this.</span></span>

![Screen shot of custom search results](./media/custom-search-webapp-results.png)

## <a name="next-steps"></a><span data-ttu-id="4b473-189">Next steps</span><span class="sxs-lookup"><span data-stu-id="4b473-189">Next steps</span></span>
<span data-ttu-id="4b473-190">In this tutorial, you've done the following:</span><span class="sxs-lookup"><span data-stu-id="4b473-190">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> - <span data-ttu-id="4b473-191">Created a custom search instance</span><span class="sxs-lookup"><span data-stu-id="4b473-191">Created a custom search instance</span></span>
> - <span data-ttu-id="4b473-192">Added active entries</span><span class="sxs-lookup"><span data-stu-id="4b473-192">Added active entries</span></span>
> - <span data-ttu-id="4b473-193">Added blocked entries</span><span class="sxs-lookup"><span data-stu-id="4b473-193">Added blocked entries</span></span>
> - <span data-ttu-id="4b473-194">Added pinned entries</span><span class="sxs-lookup"><span data-stu-id="4b473-194">Added pinned entries</span></span>
> - <span data-ttu-id="4b473-195">Integrated custom search into a web page</span><span class="sxs-lookup"><span data-stu-id="4b473-195">Integrated custom search into a web page</span></span>

<span data-ttu-id="4b473-196">You can now proceed to calling Bing Custom Search endpoints programmatically.</span><span class="sxs-lookup"><span data-stu-id="4b473-196">You can now proceed to calling Bing Custom Search endpoints programmatically.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4b473-197">Call Bing Custom Search endpoint (C#)</span><span class="sxs-lookup"><span data-stu-id="4b473-197">Call Bing Custom Search endpoint (C#)</span></span>](../call-endpoint-csharp.md)