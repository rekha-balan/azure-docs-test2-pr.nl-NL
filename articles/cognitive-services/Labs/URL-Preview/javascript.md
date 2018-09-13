---
title: JavaScript quickstart for Project URL Preview - Microsoft Cognitive Services | Microsoft Docs
description: Script sample to quickly get started using the Bing URL Preview API in Microsoft Cognitive Services on Azure.
services: cognitive-services
author: mikedodaro
ms.service: cognitive-services
ms.technology: project-url-preview
ms.topic: article
ms.date: 03/16/2018
ms.author: rosh, v-gedod
ms.openlocfilehash: dda6f7c105dfbadc3c22f0c008aa8759fe12fa03
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857099"
---
# <a name="url-preview-in-javascript"></a><span data-ttu-id="33e7b-103">URL Preview in JavaScript</span><span class="sxs-lookup"><span data-stu-id="33e7b-103">URL Preview in JavaScript</span></span> 

<span data-ttu-id="33e7b-104">The following single-page application uses JavaScript to create a URL Preview for the SwiftKey site: https://swiftkey.com/en.</span><span class="sxs-lookup"><span data-stu-id="33e7b-104">The following single-page application uses JavaScript to create a URL Preview for the SwiftKey site: https://swiftkey.com/en.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="33e7b-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="33e7b-105">Prerequisites</span></span>

<span data-ttu-id="33e7b-106">Get an access key for the free trial [Cognitive Services Labs](https://labs.cognitive.microsoft.com/en-us/project-url-preview)</span><span class="sxs-lookup"><span data-stu-id="33e7b-106">Get an access key for the free trial [Cognitive Services Labs](https://labs.cognitive.microsoft.com/en-us/project-url-preview)</span></span>

## <a name="code-scenario"></a><span data-ttu-id="33e7b-107">Code scenario</span><span class="sxs-lookup"><span data-stu-id="33e7b-107">Code scenario</span></span>
<span data-ttu-id="33e7b-108">The following javascript example includes a textbox input object where the user enters the URL to preview.</span><span class="sxs-lookup"><span data-stu-id="33e7b-108">The following javascript example includes a textbox input object where the user enters the URL to preview.</span></span>  <span data-ttu-id="33e7b-109">When the user clicks the **Preview** button, the onclick method routes to `getPreview` where code generates a Web request to the **UrlPreview** endpoint.</span><span class="sxs-lookup"><span data-stu-id="33e7b-109">When the user clicks the **Preview** button, the onclick method routes to `getPreview` where code generates a Web request to the **UrlPreview** endpoint.</span></span>

<span data-ttu-id="33e7b-110">The code creates an *XMLHttpRequest*, adds the *Ocp-Apim-Subscription-Key* header and key, and sends the request.</span><span class="sxs-lookup"><span data-stu-id="33e7b-110">The code creates an *XMLHttpRequest*, adds the *Ocp-Apim-Subscription-Key* header and key, and sends the request.</span></span>  <span data-ttu-id="33e7b-111">It adds an asynchronous event handler to process the response.</span><span class="sxs-lookup"><span data-stu-id="33e7b-111">It adds an asynchronous event handler to process the response.</span></span>

<span data-ttu-id="33e7b-112">If the response returns successfully, the handler assigns the JSON text of the response to the `demo` paragraph on the page.</span><span class="sxs-lookup"><span data-stu-id="33e7b-112">If the response returns successfully, the handler assigns the JSON text of the response to the `demo` paragraph on the page.</span></span> <span data-ttu-id="33e7b-113">Other response elements are set to the following paragraphs for display.</span><span class="sxs-lookup"><span data-stu-id="33e7b-113">Other response elements are set to the following paragraphs for display.</span></span>

<span data-ttu-id="33e7b-114">**Raw JSON response**</span><span class="sxs-lookup"><span data-stu-id="33e7b-114">**Raw JSON response**</span></span>

````
{
  "_type": "WebPage",
  "name": "SwiftKey - Smart prediction technology for easier mobile typing",
  "url": "https://swiftkey.com/en",
  "description": "Discover the best Android and iPhone and iPad apps for faster, easier typing with emoji, colorful themes and more - download SwiftKey Keyboard free today.",
  "isFamilyFriendly": true,
  "primaryImageOfPage": {
    "contentUrl": "https://swiftkey.com/images/og/default.jpg"
  }
}

````

<span data-ttu-id="33e7b-115">**The running demo**</span><span class="sxs-lookup"><span data-stu-id="33e7b-115">**The running demo**</span></span>

![JavaScript Url Preview example](./media/java-script-demo.png)

## <a name="running-the-application"></a><span data-ttu-id="33e7b-117">Running the application</span><span class="sxs-lookup"><span data-stu-id="33e7b-117">Running the application</span></span>

<span data-ttu-id="33e7b-118">To run the application:</span><span class="sxs-lookup"><span data-stu-id="33e7b-118">To run the application:</span></span>

1. <span data-ttu-id="33e7b-119">Replace the `YOUR-SUBSCRIPTION-KEY` value with a valid access key for your subscription.</span><span class="sxs-lookup"><span data-stu-id="33e7b-119">Replace the `YOUR-SUBSCRIPTION-KEY` value with a valid access key for your subscription.</span></span>
2. <span data-ttu-id="33e7b-120">Save the HTML and script to a file with .html extension.</span><span class="sxs-lookup"><span data-stu-id="33e7b-120">Save the HTML and script to a file with .html extension.</span></span>
3. <span data-ttu-id="33e7b-121">Run the Web page in a browser.</span><span class="sxs-lookup"><span data-stu-id="33e7b-121">Run the Web page in a browser.</span></span>
4. <span data-ttu-id="33e7b-122">Use the existing URL, or enter another in the textbox.</span><span class="sxs-lookup"><span data-stu-id="33e7b-122">Use the existing URL, or enter another in the textbox.</span></span>
5. <span data-ttu-id="33e7b-123">Click the **Preview** button.</span><span class="sxs-lookup"><span data-stu-id="33e7b-123">Click the **Preview** button.</span></span>

<span data-ttu-id="33e7b-124">**Source code:**</span><span class="sxs-lookup"><span data-stu-id="33e7b-124">**Source code:**</span></span>

```
<!DOCTYPE html>

<html lang="en" xmlns="http://www.w3.org/1999/xhtml">
<head>
    <meta charset="utf-8" />
    <title>urlPreview Demo</title>
</head>
<body>
    <h3>URL Preview Demo</h3>

    Page to preview: <input type="url" id="myURL" value="https://swiftkey.com/en">
    <button onclick="getPreview()">Preview</button>

    <p id="demo"></p>
    <br />
    <p id="jsonDesc"></p>
    <p><a id="familyFriendly"></a></p>
    <a id="contentUrl"></a>
    <p />
    <img id="jsonImage" />

    <script>

        var BING_ENDPOINT = "https://api.labs.cognitive.microsoft.com/urlpreview/v7.0/search"; 
        var key = "YOUR-SUBSCRIPTION-KEY";
        var xhr;

        function getPreview() {
            xhr = new XMLHttpRequest();

            var queryUrl = BING_ENDPOINT + "?q=" +
                encodeURIComponent(document.getElementById("myURL").value);
            xhr.open('GET', queryUrl, true);
            xhr.setRequestHeader("Ocp-Apim-Subscription-Key", key);

            xhr.send();

            xhr.addEventListener("readystatechange", processRequest, false);
        }

        function processRequest(e) {

            if (xhr.readyState == 4 && xhr.status == 200) {
                document.getElementById("demo").innerHTML = xhr.responseText;
                var obj = JSON.parse(xhr.responseText);
                document.getElementById("jsonDesc").innerHTML = obj.description;
                document.getElementById("familyFriendly").innerHTML = "Family Friendly: " + obj.isFamilyFriendly;
                document.getElementById("contentUrl").innerHTML = obj.url;
                document.getElementById("contentUrl").href = obj.url;
                document.getElementById("jsonImage").width = 350;
                document.getElementById("jsonImage").src = obj.primaryImageOfPage.contentUrl;

            }

        }

    </script>

</body>
</html>

```

## <a name="next-steps"></a><span data-ttu-id="33e7b-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="33e7b-125">Next steps</span></span>
- [<span data-ttu-id="33e7b-126">C# quickstart</span><span class="sxs-lookup"><span data-stu-id="33e7b-126">C# quickstart</span></span>](csharp.md)
- [<span data-ttu-id="33e7b-127">Java quickstart</span><span class="sxs-lookup"><span data-stu-id="33e7b-127">Java quickstart</span></span>](java-quickstart.md)
- [<span data-ttu-id="33e7b-128">Node quickstart</span><span class="sxs-lookup"><span data-stu-id="33e7b-128">Node quickstart</span></span>](node-quickstart.md)
- [<span data-ttu-id="33e7b-129">Python quickstart</span><span class="sxs-lookup"><span data-stu-id="33e7b-129">Python quickstart</span></span>](python-quickstart.md)
