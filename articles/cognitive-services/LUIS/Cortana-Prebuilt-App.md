---
title: Use Cortana pre-built app from LUIS | Microsoft Docs
description: Use Cortana personal assistant, a pre-built application from Language Understanding Intelligent Services (LUIS).
services: cognitive-services
author: cahann
manager: hsalama
ms.service: cognitive-services
ms.technology: luis
ms.topic: article
ms.date: 03/31/2017
ms.author: cahann
ms.openlocfilehash: dc99cd2c290fb67ae81276dd5fe603e77c5824de
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552368"
---
# <a name="cortana-prebuilt-app"></a><span data-ttu-id="3dc55-103">Cortana Prebuilt App</span><span class="sxs-lookup"><span data-stu-id="3dc55-103">Cortana Prebuilt App</span></span>

<span data-ttu-id="3dc55-104">In addition to allowing you to build your own applications, LUIS also provides selected models from Microsoft Cortana personal assistant as a pre-built application.</span><span class="sxs-lookup"><span data-stu-id="3dc55-104">In addition to allowing you to build your own applications, LUIS also provides selected models from Microsoft Cortana personal assistant as a pre-built application.</span></span> <span data-ttu-id="3dc55-105">This is an "as-is" application; the intents and entities in this application cannot be edited or integrated into other LUIS applications.</span><span class="sxs-lookup"><span data-stu-id="3dc55-105">This is an "as-is" application; the intents and entities in this application cannot be edited or integrated into other LUIS applications.</span></span> <span data-ttu-id="3dc55-106">If you’d like your client to have access to both this pre-built application and your own LUIS application, then your client will have to make two separate HTTP calls.</span><span class="sxs-lookup"><span data-stu-id="3dc55-106">If you’d like your client to have access to both this pre-built application and your own LUIS application, then your client will have to make two separate HTTP calls.</span></span>

<span data-ttu-id="3dc55-107">The pre-built personal assistant application is available in these cultures (locales): English, French, Italian, Spanish and Chinese.</span><span class="sxs-lookup"><span data-stu-id="3dc55-107">The pre-built personal assistant application is available in these cultures (locales): English, French, Italian, Spanish and Chinese.</span></span>

<span data-ttu-id="3dc55-108">**To use Cortana Prebuilt App:**</span><span class="sxs-lookup"><span data-stu-id="3dc55-108">**To use Cortana Prebuilt App:**</span></span>

1. <span data-ttu-id="3dc55-109">On **My Apps** page, click **Cortana prebuilt apps** and select your language, English for example.</span><span class="sxs-lookup"><span data-stu-id="3dc55-109">On **My Apps** page, click **Cortana prebuilt apps** and select your language, English for example.</span></span> <span data-ttu-id="3dc55-110">The following dialog box appears:</span><span class="sxs-lookup"><span data-stu-id="3dc55-110">The following dialog box appears:</span></span>

    ![Use Cortana prebuilt app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Use-Cortana.jpg)
2. <span data-ttu-id="3dc55-112">In **Query**, type the utterance you want to interpret.</span><span class="sxs-lookup"><span data-stu-id="3dc55-112">In **Query**, type the utterance you want to interpret.</span></span> <span data-ttu-id="3dc55-113">For example, type "set up an appointment at 2:00 pm tomorrow for 90 minutes called discuss budget"</span><span class="sxs-lookup"><span data-stu-id="3dc55-113">For example, type "set up an appointment at 2:00 pm tomorrow for 90 minutes called discuss budget"</span></span>
3. <span data-ttu-id="3dc55-114">From the **Subscription Key** list, select the subscription key to be used for this endpoint hit to Cortana app.</span><span class="sxs-lookup"><span data-stu-id="3dc55-114">From the **Subscription Key** list, select the subscription key to be used for this endpoint hit to Cortana app.</span></span> 
4. <span data-ttu-id="3dc55-115">Click the generated endpoint URL to access the endpoint and get the result of the query.</span><span class="sxs-lookup"><span data-stu-id="3dc55-115">Click the generated endpoint URL to access the endpoint and get the result of the query.</span></span> <span data-ttu-id="3dc55-116">The screenshot below shows the result returned in JSON format for the example utterance: "set up an appointment at 2:00 pm tomorrow for 90 minutes called discuss budget"</span><span class="sxs-lookup"><span data-stu-id="3dc55-116">The screenshot below shows the result returned in JSON format for the example utterance: "set up an appointment at 2:00 pm tomorrow for 90 minutes called discuss budget"</span></span>

    ![Cortana Query Result](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Cortana-JSON-Result.jpg)


