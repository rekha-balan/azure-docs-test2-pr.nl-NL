---
title: Publish your LUIS app | Microsoft Docs
description: After you build and test your app by using Language Understanding Intelligent Services (LUIS), publish it as a web service on Azure.
services: cognitive-services
author: cahann
manager: hsalama
ms.service: cognitive-services
ms.technology: luis
ms.topic: article
ms.date: 03/01/2017
ms.author: cahann
ms.openlocfilehash: e13662536e95fad6a1f0b6c800f0a0465bbb9e0f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661499"
---
# <a name="publish-your-app"></a><span data-ttu-id="8853b-103">Publish your app</span><span class="sxs-lookup"><span data-stu-id="8853b-103">Publish your app</span></span>
<span data-ttu-id="8853b-104">When you finish building and testing your app, you can publish it as webservice on Azure and get an HTTP endpoint that can be integrated in any backend code.</span><span class="sxs-lookup"><span data-stu-id="8853b-104">When you finish building and testing your app, you can publish it as webservice on Azure and get an HTTP endpoint that can be integrated in any backend code.</span></span> 

<span data-ttu-id="8853b-105">Optionally, it would be better to test your app before publishing it.</span><span class="sxs-lookup"><span data-stu-id="8853b-105">Optionally, it would be better to test your app before publishing it.</span></span> <span data-ttu-id="8853b-106">For instructions, see [Train and test your app](Train-Test.md).</span><span class="sxs-lookup"><span data-stu-id="8853b-106">For instructions, see [Train and test your app](Train-Test.md).</span></span>

<span data-ttu-id="8853b-107">You can either publish your app directly to the **Production Slot** where end users can access and use your model, or you can publish to a **Staging Slot** to use as a development workstation where you can work on your app and go through trials and tests to validate any changes before publishing to the production slot.</span><span class="sxs-lookup"><span data-stu-id="8853b-107">You can either publish your app directly to the **Production Slot** where end users can access and use your model, or you can publish to a **Staging Slot** to use as a development workstation where you can work on your app and go through trials and tests to validate any changes before publishing to the production slot.</span></span> 

<span data-ttu-id="8853b-108">**To publish your app to an HTTP endpoint:**</span><span class="sxs-lookup"><span data-stu-id="8853b-108">**To publish your app to an HTTP endpoint:**</span></span>

1. <span data-ttu-id="8853b-109">Open your app (e.g. TravelAgent) by clicking its name on **My Apps** page, and then click **Publish App** in the left panel to access the **Publish App** page.</span><span class="sxs-lookup"><span data-stu-id="8853b-109">Open your app (e.g. TravelAgent) by clicking its name on **My Apps** page, and then click **Publish App** in the left panel to access the **Publish App** page.</span></span> <span data-ttu-id="8853b-110">The screenshot below shows the Publish page if you haven't published your app yet.</span><span class="sxs-lookup"><span data-stu-id="8853b-110">The screenshot below shows the Publish page if you haven't published your app yet.</span></span>

    ![Publish page-](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/PublishApp-FirstPublish.JPG)
 
    <span data-ttu-id="8853b-112">If you have previously published this app, this page will look like the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="8853b-112">If you have previously published this app, this page will look like the following screenshot:</span></span> 
 
    ![Publish page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/PublishApp-RePublish.JPG)
2. <span data-ttu-id="8853b-114">From the **Endpoint Key** list, select an existing endpoint key to assign to the app, or click **Add a new key to your account** to add a new one.</span><span class="sxs-lookup"><span data-stu-id="8853b-114">From the **Endpoint Key** list, select an existing endpoint key to assign to the app, or click **Add a new key to your account** to add a new one.</span></span> <span data-ttu-id="8853b-115">For more information on how to create and add endpoint keys to your account, see [Manage your keys](Manage-Keys.md).</span><span class="sxs-lookup"><span data-stu-id="8853b-115">For more information on how to create and add endpoint keys to your account, see [Manage your keys](Manage-Keys.md).</span></span>
3. <span data-ttu-id="8853b-116">Choose whether to publish to **Production** or to **Staging** slot by selecting the corresponding value from the **Endpoint Slot** list.</span><span class="sxs-lookup"><span data-stu-id="8853b-116">Choose whether to publish to **Production** or to **Staging** slot by selecting the corresponding value from the **Endpoint Slot** list.</span></span> 
4. <span data-ttu-id="8853b-117">If you will use an external service with your LUIS app (e.g. Bing Spell Check):</span><span class="sxs-lookup"><span data-stu-id="8853b-117">If you will use an external service with your LUIS app (e.g. Bing Spell Check):</span></span>
    - <span data-ttu-id="8853b-118">Click **Add Key Association** to assign the external service key to the app by selecting the key type and key value in the following dialog box.</span><span class="sxs-lookup"><span data-stu-id="8853b-118">Click **Add Key Association** to assign the external service key to the app by selecting the key type and key value in the following dialog box.</span></span>
    - <span data-ttu-id="8853b-119">Click **Enable Bing Spell Checker** check box.</span><span class="sxs-lookup"><span data-stu-id="8853b-119">Click **Enable Bing Spell Checker** check box.</span></span> 
    
        ![Assign External Key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/PublishApp-KeyAssociation.JPG)
5. <span data-ttu-id="8853b-121">If you want the JSON response of your published app to include all intents defined in your app and their prediction scores, click **Add Verbose Flag** checkbox.</span><span class="sxs-lookup"><span data-stu-id="8853b-121">If you want the JSON response of your published app to include all intents defined in your app and their prediction scores, click **Add Verbose Flag** checkbox.</span></span> <span data-ttu-id="8853b-122">Otherwise, it will include only the top scoring intent.</span><span class="sxs-lookup"><span data-stu-id="8853b-122">Otherwise, it will include only the top scoring intent.</span></span>
6. <span data-ttu-id="8853b-123">Click **Train** if the app wasn't trained already.</span><span class="sxs-lookup"><span data-stu-id="8853b-123">Click **Train** if the app wasn't trained already.</span></span>  

7. <span data-ttu-id="8853b-124">Click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="8853b-124">Click **Publish**.</span></span> <span data-ttu-id="8853b-125">The endpoint URL of your published app is displayed.</span><span class="sxs-lookup"><span data-stu-id="8853b-125">The endpoint URL of your published app is displayed.</span></span> 

    ![HTTP endpoint URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/PublishApp-URL.JPG)

    >[!NOTE]
    ><span data-ttu-id="8853b-127">If the **Publish** button is disabled, then either your app does not have an assigned an endpoint key, or you have not trained your app yet.</span><span class="sxs-lookup"><span data-stu-id="8853b-127">If the **Publish** button is disabled, then either your app does not have an assigned an endpoint key, or you have not trained your app yet.</span></span>


<span data-ttu-id="8853b-128">To test how your published app works, you can access the test console by clicking **Train & Test** in the left panel.</span><span class="sxs-lookup"><span data-stu-id="8853b-128">To test how your published app works, you can access the test console by clicking **Train & Test** in the left panel.</span></span> <span data-ttu-id="8853b-129">For instructions on how to test your app using the test console, see [Train and test your app](Train-Test.md).</span><span class="sxs-lookup"><span data-stu-id="8853b-129">For instructions on how to test your app using the test console, see [Train and test your app](Train-Test.md).</span></span>

<span data-ttu-id="8853b-130">If you want to test your published endpoint in a browser using the generated URL, you can click the URL to open it in your browser, then set the URL parameter "&q" to your test query (for example: "&q=Book me a flight to Boston on May 4"), and then press Enter.</span><span class="sxs-lookup"><span data-stu-id="8853b-130">If you want to test your published endpoint in a browser using the generated URL, you can click the URL to open it in your browser, then set the URL parameter "&q" to your test query (for example: "&q=Book me a flight to Boston on May 4"), and then press Enter.</span></span> <span data-ttu-id="8853b-131">You will get the JSON response of your HTTP endpoint.</span><span class="sxs-lookup"><span data-stu-id="8853b-131">You will get the JSON response of your HTTP endpoint.</span></span> 

![JSON response of published HTTP endpoint](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/PublishApp-JSONresponse.JPG)





