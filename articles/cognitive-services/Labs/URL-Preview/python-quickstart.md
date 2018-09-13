---
title: Python quickstart for Project URL Preview - Microsoft Cognitive Services | Microsoft Docs
description: Script sample to quickly get started using the Project URL Preview in Microsoft Cognitive Services on Azure.
services: cognitive-services
author: mikedodaro
ms.service: cognitive-services
ms.technology: project-url-preview
ms.topic: article
ms.date: 03/29/2018
ms.author: rosh, v-gedod
ms.openlocfilehash: 78b2d83b02aa9ea32509029c7456e04e420b8572
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856093"
---
# <a name="url-preview-python-quickstart"></a><span data-ttu-id="eb8db-103">URL Preview Python quickstart</span><span class="sxs-lookup"><span data-stu-id="eb8db-103">URL Preview Python quickstart</span></span>

<span data-ttu-id="eb8db-104">The following Python example creates a Url Preview for the SwiftKey Web site: https://swiftkey.com/en.</span><span class="sxs-lookup"><span data-stu-id="eb8db-104">The following Python example creates a Url Preview for the SwiftKey Web site: https://swiftkey.com/en.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eb8db-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="eb8db-105">Prerequisites</span></span>

<span data-ttu-id="eb8db-106">Get an access key for the free trial [Cognitive Services Labs](https://aka.ms/answersearchsubscription)</span><span class="sxs-lookup"><span data-stu-id="eb8db-106">Get an access key for the free trial [Cognitive Services Labs](https://aka.ms/answersearchsubscription)</span></span>

<span data-ttu-id="eb8db-107">This example uses Python 3.6.</span><span class="sxs-lookup"><span data-stu-id="eb8db-107">This example uses Python 3.6.</span></span>

## <a name="code-scenario"></a><span data-ttu-id="eb8db-108">Code scenario</span><span class="sxs-lookup"><span data-stu-id="eb8db-108">Code scenario</span></span> 

<span data-ttu-id="eb8db-109">The following code creates a URL Preview.</span><span class="sxs-lookup"><span data-stu-id="eb8db-109">The following code creates a URL Preview.</span></span>
<span data-ttu-id="eb8db-110">It is implemented in the following steps:</span><span class="sxs-lookup"><span data-stu-id="eb8db-110">It is implemented in the following steps:</span></span>
1. <span data-ttu-id="eb8db-111">Declare variables to specify the endpoint by host and path.</span><span class="sxs-lookup"><span data-stu-id="eb8db-111">Declare variables to specify the endpoint by host and path.</span></span>
2. <span data-ttu-id="eb8db-112">Specify the query URL to preview, and add the query parameter.</span><span class="sxs-lookup"><span data-stu-id="eb8db-112">Specify the query URL to preview, and add the query parameter.</span></span>  
3. <span data-ttu-id="eb8db-113">Set the query parameter.</span><span class="sxs-lookup"><span data-stu-id="eb8db-113">Set the query parameter.</span></span>
4. <span data-ttu-id="eb8db-114">Define the Search function that creates the request and adds the *Ocp-Apim-Subscription-Key* header.</span><span class="sxs-lookup"><span data-stu-id="eb8db-114">Define the Search function that creates the request and adds the *Ocp-Apim-Subscription-Key* header.</span></span>
5. <span data-ttu-id="eb8db-115">Set the *Ocp-Apim-Subscription-Key* header.</span><span class="sxs-lookup"><span data-stu-id="eb8db-115">Set the *Ocp-Apim-Subscription-Key* header.</span></span> 
6. <span data-ttu-id="eb8db-116">Make the connection, and send the request.</span><span class="sxs-lookup"><span data-stu-id="eb8db-116">Make the connection, and send the request.</span></span>
7. <span data-ttu-id="eb8db-117">Print the JSON results.</span><span class="sxs-lookup"><span data-stu-id="eb8db-117">Print the JSON results.</span></span>

<span data-ttu-id="eb8db-118">The complete code for this demo follows:</span><span class="sxs-lookup"><span data-stu-id="eb8db-118">The complete code for this demo follows:</span></span>

````
import http.client, urllib.parse
import json

# Replace the subscriptionKey string value with your valid subscription key.
subscriptionKey = 'your-subscription-key'

host = 'api.labs.cognitive.microsoft.com'
path = '/urlpreview/v7.0/search'

query = 'https://SwiftKey.com'

params = '?q=' + urllib.parse.quote (query)

def get_preview ():
    headers = {'Ocp-Apim-Subscription-Key': subscriptionKey}
    conn = http.client.HTTPSConnection (host)
    conn.request ("GET", path + params, None, headers)
    response = conn.getresponse ()
    return response.read ()

result = get_preview ()
print (json.dumps(json.loads(result), indent=4))
````
## <a name="next-steps"></a><span data-ttu-id="eb8db-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="eb8db-119">Next steps</span></span>
- [<span data-ttu-id="eb8db-120">C# quickstart</span><span class="sxs-lookup"><span data-stu-id="eb8db-120">C# quickstart</span></span>](csharp.md)
- [<span data-ttu-id="eb8db-121">Java quickstart</span><span class="sxs-lookup"><span data-stu-id="eb8db-121">Java quickstart</span></span>](java-quickstart.md)
- [<span data-ttu-id="eb8db-122">JavaScript quickstart</span><span class="sxs-lookup"><span data-stu-id="eb8db-122">JavaScript quickstart</span></span>](javascript.md)
- [<span data-ttu-id="eb8db-123">Node URL quickstart</span><span class="sxs-lookup"><span data-stu-id="eb8db-123">Node URL quickstart</span></span>](node-quickstart.md)