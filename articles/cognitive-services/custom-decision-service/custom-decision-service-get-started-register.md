---
title: Register your application - Azure Cognitive Services | Microsoft Docs
description: A step-by-step guide how to register a new app with Azure Custom Decision Service
services: cognitive-services
author: slivkins
manager: slivkins
ms.service: cognitive-services
ms.topic: article
ms.date: 05/09/2018
ms.author: slivkins
ms.reviewer: marcozo;alekh;marossi
ms.openlocfilehash: 2aa8fbe77c11df4434eefa4c92d8529d5ca1d885
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864999"
---
# <a name="register-your-application"></a><span data-ttu-id="6b2b2-103">Register your application</span><span class="sxs-lookup"><span data-stu-id="6b2b2-103">Register your application</span></span>

<span data-ttu-id="6b2b2-104">To use Custom Decision Service for your application, register it on the portal.</span><span class="sxs-lookup"><span data-stu-id="6b2b2-104">To use Custom Decision Service for your application, register it on the portal.</span></span> <span data-ttu-id="6b2b2-105">This article explains how.</span><span class="sxs-lookup"><span data-stu-id="6b2b2-105">This article explains how.</span></span>

1. <span data-ttu-id="6b2b2-106">Go to the [front page](https://ds.microsoft.com/) of Custom Decision Service.</span><span class="sxs-lookup"><span data-stu-id="6b2b2-106">Go to the [front page](https://ds.microsoft.com/) of Custom Decision Service.</span></span> <span data-ttu-id="6b2b2-107">On the ribbon, click **My Portal**, as highlighted in the image:</span><span class="sxs-lookup"><span data-stu-id="6b2b2-107">On the ribbon, click **My Portal**, as highlighted in the image:</span></span>

    ![My Portal](./media/portal.png)

    <span data-ttu-id="6b2b2-109">If you are not already signed in, the portal prompts you to sign in with your [Microsoft account](https://account.microsoft.com/account).</span><span class="sxs-lookup"><span data-stu-id="6b2b2-109">If you are not already signed in, the portal prompts you to sign in with your [Microsoft account](https://account.microsoft.com/account).</span></span> <span data-ttu-id="6b2b2-110">After you have signed in, the portal displays your Microsoft account in the upper-right corner of the page.</span><span class="sxs-lookup"><span data-stu-id="6b2b2-110">After you have signed in, the portal displays your Microsoft account in the upper-right corner of the page.</span></span>

2. <span data-ttu-id="6b2b2-111">To register your application, click the **New App** button.</span><span class="sxs-lookup"><span data-stu-id="6b2b2-111">To register your application, click the **New App** button.</span></span>

3. <span data-ttu-id="6b2b2-112">In the dialog box, choose an App ID for your application.</span><span class="sxs-lookup"><span data-stu-id="6b2b2-112">In the dialog box, choose an App ID for your application.</span></span> <span data-ttu-id="6b2b2-113">Custom Decision Service requires a unique ID for each application.</span><span class="sxs-lookup"><span data-stu-id="6b2b2-113">Custom Decision Service requires a unique ID for each application.</span></span> <span data-ttu-id="6b2b2-114">If someone else has already taken this ID, the system asks you to pick a different one.</span><span class="sxs-lookup"><span data-stu-id="6b2b2-114">If someone else has already taken this ID, the system asks you to pick a different one.</span></span>

4. <span data-ttu-id="6b2b2-115">Specify an Action Set API.</span><span class="sxs-lookup"><span data-stu-id="6b2b2-115">Specify an Action Set API.</span></span> <span data-ttu-id="6b2b2-116">This setting is an RSS or Atom feed that communicates the available content for your application to Custom Decision Service.</span><span class="sxs-lookup"><span data-stu-id="6b2b2-116">This setting is an RSS or Atom feed that communicates the available content for your application to Custom Decision Service.</span></span> <span data-ttu-id="6b2b2-117">Enter a name for the feed, and enter the URL from which it is served.</span><span class="sxs-lookup"><span data-stu-id="6b2b2-117">Enter a name for the feed, and enter the URL from which it is served.</span></span> <span data-ttu-id="6b2b2-118">To do this step later, click the **Feeds** button and then click the **New feed** button.</span><span class="sxs-lookup"><span data-stu-id="6b2b2-118">To do this step later, click the **Feeds** button and then click the **New feed** button.</span></span> <span data-ttu-id="6b2b2-119">An example that creates an RSS feed is described later.</span><span class="sxs-lookup"><span data-stu-id="6b2b2-119">An example that creates an RSS feed is described later.</span></span>

5. <span data-ttu-id="6b2b2-120">To register your application, select the **Custom App** check box in the lower-left corner.</span><span class="sxs-lookup"><span data-stu-id="6b2b2-120">To register your application, select the **Custom App** check box in the lower-left corner.</span></span> <span data-ttu-id="6b2b2-121">Enter a [connection string](../../storage/common/storage-configure-connection-string.md) for the Azure storage account where your application data is logged.</span><span class="sxs-lookup"><span data-stu-id="6b2b2-121">Enter a [connection string](../../storage/common/storage-configure-connection-string.md) for the Azure storage account where your application data is logged.</span></span> <span data-ttu-id="6b2b2-122">For more information on how to create a storage account, see [How to create, manage, or delete a storage account](../../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="6b2b2-122">For more information on how to create a storage account, see [How to create, manage, or delete a storage account](../../storage/common/storage-create-storage-account.md).</span></span>

### <a name="next-steps"></a><span data-ttu-id="6b2b2-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="6b2b2-123">Next steps</span></span>

* <span data-ttu-id="6b2b2-124">Get started to optimize [a webpage](custom-decision-service-get-started-browser.md) or [a smartphone app](custom-decision-service-get-started-app.md).</span><span class="sxs-lookup"><span data-stu-id="6b2b2-124">Get started to optimize [a webpage](custom-decision-service-get-started-browser.md) or [a smartphone app](custom-decision-service-get-started-app.md).</span></span>
* <span data-ttu-id="6b2b2-125">Work through a [tutorial](custom-decision-service-tutorial-news.md) for a more in-depth example.</span><span class="sxs-lookup"><span data-stu-id="6b2b2-125">Work through a [tutorial](custom-decision-service-tutorial-news.md) for a more in-depth example.</span></span>
* <span data-ttu-id="6b2b2-126">Consult the [API reference](custom-decision-service-api-reference.md) to learn more about the provided functionality.</span><span class="sxs-lookup"><span data-stu-id="6b2b2-126">Consult the [API reference](custom-decision-service-api-reference.md) to learn more about the provided functionality.</span></span>