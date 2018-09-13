---
title: Bing Image Search single-page Web app | Microsoft Docs
titleSuffix: Bing Web Search APIs - Cognitive Services
description: Shows how to use the Bing Image Search API in a single-page Web application.
services: cognitive-services
author: brapel
manager: ehansen
ms.service: cognitive-services
ms.component: bing-image-search
ms.topic: article
ms.date: 10/04/2017
ms.author: v-brapel
ms.openlocfilehash: 303d7745167d2ea25fda083ed99881ac4e0a7ec7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870914"
---
# <a name="tutorial-visual-search-single-page-web-app"></a><span data-ttu-id="8548c-103">Tutorial: Visual Search Single-page Web app</span><span class="sxs-lookup"><span data-stu-id="8548c-103">Tutorial: Visual Search Single-page Web app</span></span>

<span data-ttu-id="8548c-104">Bing Visual Search API provides an experience similar to the image details shown on Bing.com/images.</span><span class="sxs-lookup"><span data-stu-id="8548c-104">Bing Visual Search API provides an experience similar to the image details shown on Bing.com/images.</span></span> <span data-ttu-id="8548c-105">With Visual Search, you can specify an image and get back insights about the image such as visually similar images, shopping sources, webpages that include the image, and more.</span><span class="sxs-lookup"><span data-stu-id="8548c-105">With Visual Search, you can specify an image and get back insights about the image such as visually similar images, shopping sources, webpages that include the image, and more.</span></span> 

<span data-ttu-id="8548c-106">This tutorial extends the single page web app from the Bing Image Search tutorial (see [Single-page Web app](../Bing-Image-Search/tutorial-bing-image-search-single-page-app.md)).</span><span class="sxs-lookup"><span data-stu-id="8548c-106">This tutorial extends the single page web app from the Bing Image Search tutorial (see [Single-page Web app](../Bing-Image-Search/tutorial-bing-image-search-single-page-app.md)).</span></span> <span data-ttu-id="8548c-107">For full source code to start this tutorial, see [Single-page Web app (source code)](../Bing-Image-Search/tutorial-bing-image-search-single-page-app-source.md).</span><span class="sxs-lookup"><span data-stu-id="8548c-107">For full source code to start this tutorial, see [Single-page Web app (source code)](../Bing-Image-Search/tutorial-bing-image-search-single-page-app-source.md).</span></span> <span data-ttu-id="8548c-108">For the final source code of this tutorial, see [Visual Search Single-page Web app](tutorial-bing-visual-search-single-page-app-source.md).</span><span class="sxs-lookup"><span data-stu-id="8548c-108">For the final source code of this tutorial, see [Visual Search Single-page Web app](tutorial-bing-visual-search-single-page-app-source.md).</span></span>

<span data-ttu-id="8548c-109">The tasks covered are:</span><span class="sxs-lookup"><span data-stu-id="8548c-109">The tasks covered are:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8548c-110">Call Bing Visual Search API with an image insights token</span><span class="sxs-lookup"><span data-stu-id="8548c-110">Call Bing Visual Search API with an image insights token</span></span>
> * <span data-ttu-id="8548c-111">Display similar images</span><span class="sxs-lookup"><span data-stu-id="8548c-111">Display similar images</span></span>

## <a name="call-bing-visual-search"></a><span data-ttu-id="8548c-112">Call Bing Visual Search</span><span class="sxs-lookup"><span data-stu-id="8548c-112">Call Bing Visual Search</span></span>
<span data-ttu-id="8548c-113">Edit the Bing Image Search tutorial and add the following code to the end of the script element at line 409.</span><span class="sxs-lookup"><span data-stu-id="8548c-113">Edit the Bing Image Search tutorial and add the following code to the end of the script element at line 409.</span></span> <span data-ttu-id="8548c-114">This code calls the Bing Visual Search API and displays the results.</span><span class="sxs-lookup"><span data-stu-id="8548c-114">This code calls the Bing Visual Search API and displays the results.</span></span>

``` javascript
function handleVisualSearchResponse(){
    if(this.status !== 200){
        console.log(this.responseText);
        return;
    }
    let json = this.responseText;
    let response = JSON.parse(json);
    for (let i =0; i < response.tags.length; i++) {
        let tag = response.tags[i];
        if (tag.displayName === '') {
            for (let j = 0; j < tag.actions.length; j++) {
                let action = tag.actions[j];
                if (action.actionType === 'VisualSearch') {
                    let html = '';
                    for (let k = 0; k < action.data.value.length; k++) {
                        let item = action.data.value[k];
                        let height = 120;
                        let width = Math.max(Math.round(height * item.thumbnail.width / item.thumbnail.height), 120);
                        html += "<img src='"+ item.thumbnailUrl + "&h=" + height + "&w=" + width + "' height=" + height + " width=" + width + "'>";
                    }
                    showDiv("insights", html);
                    window.scrollTo({top: document.getElementById("insights").getBoundingClientRect().top, behavior: "smooth"});
                }
            }
        }
    }
}

function bingVisualSearch(insightsToken){
    let visualSearchBaseURL = 'https://api.cognitive.microsoft.com/bing/v7.0/images/visualsearch',
        boundary = 'boundary_ABC123DEF456',
        startBoundary = '--' + boundary,
        endBoundary = '--' + boundary + '--',
        newLine = "\r\n",
        bodyHeader = 'Content-Disposition: form-data; name="knowledgeRequest"' + newLine + newLine;

    let postBody = {
        imageInfo: {
            imageInsightsToken: insightsToken
        }
    }
    let requestBody = startBoundary + newLine;
    requestBody += bodyHeader;
    requestBody += JSON.stringify(postBody) + newLine + newLine;
    requestBody += endBoundary + newLine;       
    
    let request = new XMLHttpRequest();

    try {
        request.open("POST", visualSearchBaseURL);
    } 
    catch (e) {
        renderErrorMessage("Error performing visual search: " + e.message);
    }
    request.setRequestHeader("Ocp-Apim-Subscription-Key", getSubscriptionKey());
    request.setRequestHeader("Content-Type", "multipart/form-data; boundary=" + boundary);
    request.addEventListener("load", handleVisualSearchResponse);
    request.send(requestBody);
}
```

## <a name="capture-insights-token"></a><span data-ttu-id="8548c-115">Capture insights token</span><span class="sxs-lookup"><span data-stu-id="8548c-115">Capture insights token</span></span>
<span data-ttu-id="8548c-116">Add the following code into the `searchItemsRenderer` object at line 151.</span><span class="sxs-lookup"><span data-stu-id="8548c-116">Add the following code into the `searchItemsRenderer` object at line 151.</span></span> <span data-ttu-id="8548c-117">This code adds a **find similar** link that calls the `bingVisualSearch` function when clicked.</span><span class="sxs-lookup"><span data-stu-id="8548c-117">This code adds a **find similar** link that calls the `bingVisualSearch` function when clicked.</span></span> <span data-ttu-id="8548c-118">The function receives the imageInsightsToken as an argument.</span><span class="sxs-lookup"><span data-stu-id="8548c-118">The function receives the imageInsightsToken as an argument.</span></span>

``` javascript
html.push("<a href='javascript:bingVisualSearch(\"" + item.imageInsightsToken + "\");'>find similar</a><br>");
```

## <a name="display-similar-images"></a><span data-ttu-id="8548c-119">Display similar images</span><span class="sxs-lookup"><span data-stu-id="8548c-119">Display similar images</span></span>
<span data-ttu-id="8548c-120">Add the following HTML code at line 601.</span><span class="sxs-lookup"><span data-stu-id="8548c-120">Add the following HTML code at line 601.</span></span> <span data-ttu-id="8548c-121">This markup code adds an element used to display the results of the Bing Visual Search API call.</span><span class="sxs-lookup"><span data-stu-id="8548c-121">This markup code adds an element used to display the results of the Bing Visual Search API call.</span></span>

``` html
<div id="insights">
    <h3><a href="#" onclick="return toggleDisplay('_insights')">Similar</a></h3>
    <div id="_insights" style="display: none"></div>
</div>
```

<span data-ttu-id="8548c-122">With all the new JavaScript code and HTML elements in place, search results are displayed with a **find similar** link.</span><span class="sxs-lookup"><span data-stu-id="8548c-122">With all the new JavaScript code and HTML elements in place, search results are displayed with a **find similar** link.</span></span> <span data-ttu-id="8548c-123">Click the link to populate the **Similar** section with images similar to the one you picked.</span><span class="sxs-lookup"><span data-stu-id="8548c-123">Click the link to populate the **Similar** section with images similar to the one you picked.</span></span> <span data-ttu-id="8548c-124">You may have to expand the **Similar** section to show the images.</span><span class="sxs-lookup"><span data-stu-id="8548c-124">You may have to expand the **Similar** section to show the images.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8548c-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="8548c-125">Next steps</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="8548c-126">[Visual Search Single-page Web app source](tutorial-bing-visual-search-single-page-app-source.md)
> [Bing Visual Search API reference](https://aka.ms/bingvisualsearchreferencedoc)</span><span class="sxs-lookup"><span data-stu-id="8548c-126">[Visual Search Single-page Web app source](tutorial-bing-visual-search-single-page-app-source.md)
[Bing Visual Search API reference](https://aka.ms/bingvisualsearchreferencedoc)</span></span>