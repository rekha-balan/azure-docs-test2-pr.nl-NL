---
title: 'Bing Custom Search: Site search | Microsoft Docs'
description: Describes how to configure hosted UI
services: cognitive-services
author: brapel
manager: ehansen
ms.service: cognitive-services
ms.component: bing-custom-search
ms.topic: article
ms.date: 09/28/2017
ms.author: v-brapel
ms.openlocfilehash: 7f2b97479ffcdb7ec8b3a1a635562d1fe68c3269
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866149"
---
# <a name="configure-your-hosted-ui-experience"></a><span data-ttu-id="28a73-103">Configure your hosted UI experience</span><span class="sxs-lookup"><span data-stu-id="28a73-103">Configure your hosted UI experience</span></span>
<span data-ttu-id="28a73-104">After configuring your custom search instance, you can call the Custom Search API to get the search results and display them in your app.</span><span class="sxs-lookup"><span data-stu-id="28a73-104">After configuring your custom search instance, you can call the Custom Search API to get the search results and display them in your app.</span></span> <span data-ttu-id="28a73-105">Or, if your app is a web app, you can use the hosted UI that Custom Search provides.</span><span class="sxs-lookup"><span data-stu-id="28a73-105">Or, if your app is a web app, you can use the hosted UI that Custom Search provides.</span></span>   

## <a name="configure-custom-hosted-ui"></a><span data-ttu-id="28a73-106">Configure custom hosted UI</span><span class="sxs-lookup"><span data-stu-id="28a73-106">Configure custom hosted UI</span></span>
<span data-ttu-id="28a73-107">Use the following instructions to configure a hosted UI to include in your web app.</span><span class="sxs-lookup"><span data-stu-id="28a73-107">Use the following instructions to configure a hosted UI to include in your web app.</span></span>
1.  <span data-ttu-id="28a73-108">Sign in to Custom Search [portal](https://customsearch.ai).</span><span class="sxs-lookup"><span data-stu-id="28a73-108">Sign in to Custom Search [portal](https://customsearch.ai).</span></span>
2.  <span data-ttu-id="28a73-109">Click a Custom Search instance.</span><span class="sxs-lookup"><span data-stu-id="28a73-109">Click a Custom Search instance.</span></span> <span data-ttu-id="28a73-110">To create an instance, see [Create your first Bing Custom Search instance](quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="28a73-110">To create an instance, see [Create your first Bing Custom Search instance](quick-start.md).</span></span>
3.  <span data-ttu-id="28a73-111">Click the **Hosted UI** tab.</span><span class="sxs-lookup"><span data-stu-id="28a73-111">Click the **Hosted UI** tab.</span></span>
4.  <span data-ttu-id="28a73-112">Select a layout.</span><span class="sxs-lookup"><span data-stu-id="28a73-112">Select a layout.</span></span>
    - <span data-ttu-id="28a73-113">Search bar and results (default) &mdash; Display a search box and search results</span><span class="sxs-lookup"><span data-stu-id="28a73-113">Search bar and results (default) &mdash; Display a search box and search results</span></span>
    - <span data-ttu-id="28a73-114">Results only &mdash; Don't display a search box, show only results</span><span class="sxs-lookup"><span data-stu-id="28a73-114">Results only &mdash; Don't display a search box, show only results</span></span>
    - <span data-ttu-id="28a73-115">Pop-over &mdash; Don't display a search box, show only results in a sliding overlay</span><span class="sxs-lookup"><span data-stu-id="28a73-115">Pop-over &mdash; Don't display a search box, show only results in a sliding overlay</span></span>
    
   > [!IMPORTANT]
   > <span data-ttu-id="28a73-116">Be sure to include the customConfig query parameter when selecting the **Results only** layout, see [Query parameters](https://docs.microsoft.com/rest/api/cognitiveservices/bing-custom-search-api-v7-reference#query-parameters).</span><span class="sxs-lookup"><span data-stu-id="28a73-116">Be sure to include the customConfig query parameter when selecting the **Results only** layout, see [Query parameters](https://docs.microsoft.com/rest/api/cognitiveservices/bing-custom-search-api-v7-reference#query-parameters).</span></span>

5.  <span data-ttu-id="28a73-117">Under **Additional Configurations**, provide values as appropriate for your app.</span><span class="sxs-lookup"><span data-stu-id="28a73-117">Under **Additional Configurations**, provide values as appropriate for your app.</span></span> <span data-ttu-id="28a73-118">These settings are optional.</span><span class="sxs-lookup"><span data-stu-id="28a73-118">These settings are optional.</span></span> <span data-ttu-id="28a73-119">To see the effect of applying or removing them, see the preview pane on the right.</span><span class="sxs-lookup"><span data-stu-id="28a73-119">To see the effect of applying or removing them, see the preview pane on the right.</span></span>  <span data-ttu-id="28a73-120">Available configuration options are:</span><span class="sxs-lookup"><span data-stu-id="28a73-120">Available configuration options are:</span></span>
    - <span data-ttu-id="28a73-121">Web search configurations:</span><span class="sxs-lookup"><span data-stu-id="28a73-121">Web search configurations:</span></span>
        - <span data-ttu-id="28a73-122">Web results enabled &mdash; Determines if web search results are returned</span><span class="sxs-lookup"><span data-stu-id="28a73-122">Web results enabled &mdash; Determines if web search results are returned</span></span>
        - <span data-ttu-id="28a73-123">Enable autosuggest &mdash; Determines if custom autosuggest is enabled</span><span class="sxs-lookup"><span data-stu-id="28a73-123">Enable autosuggest &mdash; Determines if custom autosuggest is enabled</span></span>
        - <span data-ttu-id="28a73-124">Web results per page &mdash; Number of web search results to display at a time</span><span class="sxs-lookup"><span data-stu-id="28a73-124">Web results per page &mdash; Number of web search results to display at a time</span></span>
        - <span data-ttu-id="28a73-125">Image caption &mdash; Determines if images are displayed with search results</span><span class="sxs-lookup"><span data-stu-id="28a73-125">Image caption &mdash; Determines if images are displayed with search results</span></span>
        - <span data-ttu-id="28a73-126">Highlight words &mdash; Determines if results are displayed with search terms in bold</span><span class="sxs-lookup"><span data-stu-id="28a73-126">Highlight words &mdash; Determines if results are displayed with search terms in bold</span></span>
    - <span data-ttu-id="28a73-127">Image search configurations:</span><span class="sxs-lookup"><span data-stu-id="28a73-127">Image search configurations:</span></span>
        - <span data-ttu-id="28a73-128">Image results enabled &mdash; Determines if image search results are returned</span><span class="sxs-lookup"><span data-stu-id="28a73-128">Image results enabled &mdash; Determines if image search results are returned</span></span>
    - <span data-ttu-id="28a73-129">Miscellaneous configurations:</span><span class="sxs-lookup"><span data-stu-id="28a73-129">Miscellaneous configurations:</span></span>
        - <span data-ttu-id="28a73-130">Page title &mdash;  Text displayed in the page title area</span><span class="sxs-lookup"><span data-stu-id="28a73-130">Page title &mdash;  Text displayed in the page title area</span></span>
        - <span data-ttu-id="28a73-131">Toolbar theme &mdash; Determines the background color of the page title area</span><span class="sxs-lookup"><span data-stu-id="28a73-131">Toolbar theme &mdash; Determines the background color of the page title area</span></span>
        - <span data-ttu-id="28a73-132">Search box text placeholder &mdash; Text displayed in the search box prior to input</span><span class="sxs-lookup"><span data-stu-id="28a73-132">Search box text placeholder &mdash; Text displayed in the search box prior to input</span></span>
        - <span data-ttu-id="28a73-133">Title link url &mdash;  Target for the title link</span><span class="sxs-lookup"><span data-stu-id="28a73-133">Title link url &mdash;  Target for the title link</span></span>
        - <span data-ttu-id="28a73-134">Logo url &mdash; Image displayed next to the title</span><span class="sxs-lookup"><span data-stu-id="28a73-134">Logo url &mdash; Image displayed next to the title</span></span> 
        - <span data-ttu-id="28a73-135">Favicon url &mdash; Icon displayed in the browser title bar</span><span class="sxs-lookup"><span data-stu-id="28a73-135">Favicon url &mdash; Icon displayed in the browser title bar</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="28a73-136">At least one of Image search or Web search must be enabled.</span><span class="sxs-lookup"><span data-stu-id="28a73-136">At least one of Image search or Web search must be enabled.</span></span>

6.  <span data-ttu-id="28a73-137">Enter the search subscription key, or choose one from the drop-down.</span><span class="sxs-lookup"><span data-stu-id="28a73-137">Enter the search subscription key, or choose one from the drop-down.</span></span> <span data-ttu-id="28a73-138">The drop-down is populated with keys from your account's Azure subscriptions.</span><span class="sxs-lookup"><span data-stu-id="28a73-138">The drop-down is populated with keys from your account's Azure subscriptions.</span></span> <span data-ttu-id="28a73-139">See [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account).</span><span class="sxs-lookup"><span data-stu-id="28a73-139">See [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account).</span></span>
7.  <span data-ttu-id="28a73-140">If you enabled autosuggest, enter the autosuggest subscription key, or choose one from the drop-down.</span><span class="sxs-lookup"><span data-stu-id="28a73-140">If you enabled autosuggest, enter the autosuggest subscription key, or choose one from the drop-down.</span></span> <span data-ttu-id="28a73-141">The drop-down is populated with keys from your account's Azure subscriptions.</span><span class="sxs-lookup"><span data-stu-id="28a73-141">The drop-down is populated with keys from your account's Azure subscriptions.</span></span> <span data-ttu-id="28a73-142">Custom Autosuggest requires a specifiec subscription tier, see the [pricing pages](https://azure.microsoft.com/pricing/details/cognitive-services/bing-custom-search/).</span><span class="sxs-lookup"><span data-stu-id="28a73-142">Custom Autosuggest requires a specifiec subscription tier, see the [pricing pages](https://azure.microsoft.com/pricing/details/cognitive-services/bing-custom-search/).</span></span>

> [!NOTE]
> <span data-ttu-id="28a73-143">As you make changes to the custom hosted UI configuration, the pane on the right provides a visual reference for the changes made.</span><span class="sxs-lookup"><span data-stu-id="28a73-143">As you make changes to the custom hosted UI configuration, the pane on the right provides a visual reference for the changes made.</span></span> <span data-ttu-id="28a73-144">The displayed search results are not actual results for your instance</span><span class="sxs-lookup"><span data-stu-id="28a73-144">The displayed search results are not actual results for your instance</span></span>

[!INCLUDE [publish or revert](./includes/publish-revert.md)]

## <a name="consume-custom-ui"></a><span data-ttu-id="28a73-145">Consume custom UI</span><span class="sxs-lookup"><span data-stu-id="28a73-145">Consume custom UI</span></span>
<span data-ttu-id="28a73-146">To consume the hosted UI, either:</span><span class="sxs-lookup"><span data-stu-id="28a73-146">To consume the hosted UI, either:</span></span> 

- <span data-ttu-id="28a73-147">Include the script in your web page</span><span class="sxs-lookup"><span data-stu-id="28a73-147">Include the script in your web page</span></span>
    ``` html
    <html>
        <body>
            <script type="text/javascript"
                id="bcs_js_snippet"            
                src="https://ui.customsearch.ai/api/ux/render?customConfig=<YOUR-CUSTOM-CONFIG-ID>&market=en-US&safeSearch=Moderate">            
            </script>
        </body>    
    </html>
    ```

- <span data-ttu-id="28a73-148">Use the URL provided `https://ui.customsearch.ai/hosted?customConfig=YOUR-CUSTOM-CONFIG-ID`</span><span class="sxs-lookup"><span data-stu-id="28a73-148">Use the URL provided `https://ui.customsearch.ai/hosted?customConfig=YOUR-CUSTOM-CONFIG-ID`</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="28a73-149">The page cannot display your privacy statement or other notices and terms.</span><span class="sxs-lookup"><span data-stu-id="28a73-149">The page cannot display your privacy statement or other notices and terms.</span></span> <span data-ttu-id="28a73-150">Suitability for your use may vary.</span><span class="sxs-lookup"><span data-stu-id="28a73-150">Suitability for your use may vary.</span></span>  

<span data-ttu-id="28a73-151">For additional information, including your Custom Configuration ID, go to **Endpoints** under the **Production** tab.</span><span class="sxs-lookup"><span data-stu-id="28a73-151">For additional information, including your Custom Configuration ID, go to **Endpoints** under the **Production** tab.</span></span>

## <a name="next-steps"></a><span data-ttu-id="28a73-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="28a73-152">Next steps</span></span>
- [<span data-ttu-id="28a73-153">Use decoration markers to highlight text</span><span class="sxs-lookup"><span data-stu-id="28a73-153">Use decoration markers to highlight text</span></span>](./hit-highlighting.md)
- [<span data-ttu-id="28a73-154">Page webpages</span><span class="sxs-lookup"><span data-stu-id="28a73-154">Page webpages</span></span>](./page-webpages.md)