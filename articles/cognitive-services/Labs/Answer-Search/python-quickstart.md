---
title: Python quickstart for Microsoft Cognitive Services, Project Answer Search | Microsoft Docs
description: Python example get started using Project Answer Search, Microsoft Cognitive Services on Azure.
services: cognitive-services
author: mikedodaro
ms.service: cognitive-services
ms.technology: project-answer-search
ms.topic: article
ms.date: 04/13/2018
ms.author: rosh, v-gedod
ms.openlocfilehash: 9cb5406c616ed8e96d73c00c788a0d20f66dcabd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871661"
---
# <a name="project-answer-search-python-quickstart"></a><span data-ttu-id="c8329-103">Project Answer Search Python quickstart</span><span class="sxs-lookup"><span data-stu-id="c8329-103">Project Answer Search Python quickstart</span></span>

<span data-ttu-id="c8329-104">The following Python example creates and sends a request for information about "Rock of Gibraltar".</span><span class="sxs-lookup"><span data-stu-id="c8329-104">The following Python example creates and sends a request for information about "Rock of Gibraltar".</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c8329-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c8329-105">Prerequisites</span></span>

<span data-ttu-id="c8329-106">Get an access key for the free trial [Cognitive Services Labs](https://aka.ms/answersearchsubscription)</span><span class="sxs-lookup"><span data-stu-id="c8329-106">Get an access key for the free trial [Cognitive Services Labs](https://aka.ms/answersearchsubscription)</span></span>

<span data-ttu-id="c8329-107">This example uses Python 3.6.4</span><span class="sxs-lookup"><span data-stu-id="c8329-107">This example uses Python 3.6.4</span></span>

## <a name="code-scenario"></a><span data-ttu-id="c8329-108">Code scenario</span><span class="sxs-lookup"><span data-stu-id="c8329-108">Code scenario</span></span> 

<span data-ttu-id="c8329-109">The following code creates a URL Preview.</span><span class="sxs-lookup"><span data-stu-id="c8329-109">The following code creates a URL Preview.</span></span>
<span data-ttu-id="c8329-110">It is implemented in the following steps:</span><span class="sxs-lookup"><span data-stu-id="c8329-110">It is implemented in the following steps:</span></span>
1. <span data-ttu-id="c8329-111">Declare variables to specify the endpoint by host and path.</span><span class="sxs-lookup"><span data-stu-id="c8329-111">Declare variables to specify the endpoint by host and path.</span></span>
2. <span data-ttu-id="c8329-112">Specify the query URL to preview, and add the query parameter.</span><span class="sxs-lookup"><span data-stu-id="c8329-112">Specify the query URL to preview, and add the query parameter.</span></span>  
3. <span data-ttu-id="c8329-113">Set the query parameter.</span><span class="sxs-lookup"><span data-stu-id="c8329-113">Set the query parameter.</span></span>
4. <span data-ttu-id="c8329-114">Define the Search function that creates the request and adds the *Ocp-Apim-Subscription-Key* header.</span><span class="sxs-lookup"><span data-stu-id="c8329-114">Define the Search function that creates the request and adds the *Ocp-Apim-Subscription-Key* header.</span></span>
5. <span data-ttu-id="c8329-115">Set the *Ocp-Apim-Subscription-Key* header.</span><span class="sxs-lookup"><span data-stu-id="c8329-115">Set the *Ocp-Apim-Subscription-Key* header.</span></span> 
6. <span data-ttu-id="c8329-116">Make the connection, and send the request.</span><span class="sxs-lookup"><span data-stu-id="c8329-116">Make the connection, and send the request.</span></span>
7. <span data-ttu-id="c8329-117">Print the JSON results.</span><span class="sxs-lookup"><span data-stu-id="c8329-117">Print the JSON results.</span></span>

<span data-ttu-id="c8329-118">The complete code for this demo follows:</span><span class="sxs-lookup"><span data-stu-id="c8329-118">The complete code for this demo follows:</span></span>

````
import http.client, urllib.parse
import json

# Replace the subscriptionKey string value with your valid subscription key.
subscriptionKey = 'YOUR-SUBSCRIPTION-KEY'

host = 'https://api.labs.cognitive.microsoft.com'
path = '/answerSearch/v7.0/search '

query = 'Rock of Gibraltar'

params = '?q=' + urllib.parse.quote (query) + '&mkt=en-us'

def get_local():
    headers = {'Ocp-Apim-Subscription-Key': subscriptionKey}
    conn = http.client.HTTPSConnection (host)
    conn.request ("GET", path + params, None, headers)
    response = conn.getresponse ()
    return response.read ()

result = get_local()
print (json.dumps(json.loads(result), indent=4))

````
## <a name="next-steps"></a><span data-ttu-id="c8329-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="c8329-119">Next steps</span></span>
- [<span data-ttu-id="c8329-120">C# quickstart</span><span class="sxs-lookup"><span data-stu-id="c8329-120">C# quickstart</span></span>](c-sharp-quickstart.md)
- [<span data-ttu-id="c8329-121">Java quickstart</span><span class="sxs-lookup"><span data-stu-id="c8329-121">Java quickstart</span></span>](java-quickstart.md)
- [<span data-ttu-id="c8329-122">Node quickstart</span><span class="sxs-lookup"><span data-stu-id="c8329-122">Node quickstart</span></span>](node-quickstart.md)