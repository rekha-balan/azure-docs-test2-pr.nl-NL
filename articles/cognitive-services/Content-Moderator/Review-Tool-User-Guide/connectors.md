---
title: Use connectors in Azure Content Moderator to access other APIs | Microsoft Docs
description: Learn how to access other APIs for your Content Moderator workflows by using connectors.
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.component: content-moderator
ms.topic: article
ms.date: 06/22/2017
ms.author: sajagtap
ms.openlocfilehash: d8114457e7079ca8772cab830bd011dcddf372f5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967236"
---
# <a name="connectors"></a><span data-ttu-id="08b95-103">Connectors</span><span class="sxs-lookup"><span data-stu-id="08b95-103">Connectors</span></span>

<span data-ttu-id="08b95-104">Azure Content Moderator workflows can use other APIs, in addition to Content Moderator APIs.</span><span class="sxs-lookup"><span data-stu-id="08b95-104">Azure Content Moderator workflows can use other APIs, in addition to Content Moderator APIs.</span></span> <span data-ttu-id="08b95-105">You access other APIs by using a connector in Content Moderator.</span><span class="sxs-lookup"><span data-stu-id="08b95-105">You access other APIs by using a connector in Content Moderator.</span></span> <span data-ttu-id="08b95-106">The connector provides a link to the other APIs.</span><span class="sxs-lookup"><span data-stu-id="08b95-106">The connector provides a link to the other APIs.</span></span>

<span data-ttu-id="08b95-107">Content Moderator includes these default connectors:</span><span class="sxs-lookup"><span data-stu-id="08b95-107">Content Moderator includes these default connectors:</span></span>

* <span data-ttu-id="08b95-108">Emotion API</span><span class="sxs-lookup"><span data-stu-id="08b95-108">Emotion API</span></span>
* <span data-ttu-id="08b95-109">Face API</span><span class="sxs-lookup"><span data-stu-id="08b95-109">Face API</span></span>
* <span data-ttu-id="08b95-110">PhotoDNA Cloud Service</span><span class="sxs-lookup"><span data-stu-id="08b95-110">PhotoDNA Cloud Service</span></span>

![Content Moderator available connectors](images/connectors-1.png)

## <a name="verify-your-credentials"></a><span data-ttu-id="08b95-112">Verify your credentials</span><span class="sxs-lookup"><span data-stu-id="08b95-112">Verify your credentials</span></span> 

<span data-ttu-id="08b95-113">Before you define a workflow, ensure that you have valid credentials for the connector API that you want to use:</span><span class="sxs-lookup"><span data-stu-id="08b95-113">Before you define a workflow, ensure that you have valid credentials for the connector API that you want to use:</span></span>

1.  <span data-ttu-id="08b95-114">On the Review tool Dashboard, select **Settings** > **Connectors**.</span><span class="sxs-lookup"><span data-stu-id="08b95-114">On the Review tool Dashboard, select **Settings** > **Connectors**.</span></span>

  ![Content Moderator select Connectors](images/connectors-2.png)

2.  <span data-ttu-id="08b95-116">Select the **Edit** symbol next to the connector that you want to verify credentials for.</span><span class="sxs-lookup"><span data-stu-id="08b95-116">Select the **Edit** symbol next to the connector that you want to verify credentials for.</span></span>

  ![Content Moderator select the Edit symbol](images/connectors-3.png)

3.  <span data-ttu-id="08b95-118">The subscription key appears.</span><span class="sxs-lookup"><span data-stu-id="08b95-118">The subscription key appears.</span></span> <span data-ttu-id="08b95-119">If you make any edits, select **Save** when you are finished.</span><span class="sxs-lookup"><span data-stu-id="08b95-119">If you make any edits, select **Save** when you are finished.</span></span>

  ![Content Moderator Edit Connectors page](images/connectors-4-1.png)
 
## <a name="add-a-connector"></a><span data-ttu-id="08b95-121">Add a connector</span><span class="sxs-lookup"><span data-stu-id="08b95-121">Add a connector</span></span>

1.  <span data-ttu-id="08b95-122">Before you add a connector, you need a subscription key.</span><span class="sxs-lookup"><span data-stu-id="08b95-122">Before you add a connector, you need a subscription key.</span></span> <span data-ttu-id="08b95-123">On the Review tool Dashboard, select **Settings** > **Credentials**.</span><span class="sxs-lookup"><span data-stu-id="08b95-123">On the Review tool Dashboard, select **Settings** > **Credentials**.</span></span> <span data-ttu-id="08b95-124">Select and copy the value that's in the **Ocp-Admin-Subscription-Key** box.</span><span class="sxs-lookup"><span data-stu-id="08b95-124">Select and copy the value that's in the **Ocp-Admin-Subscription-Key** box.</span></span>

2.  <span data-ttu-id="08b95-125">Select **Connectors**.</span><span class="sxs-lookup"><span data-stu-id="08b95-125">Select **Connectors**.</span></span> <span data-ttu-id="08b95-126">Select one of the available connectors that are displayed on the Review tool Dashboard.</span><span class="sxs-lookup"><span data-stu-id="08b95-126">Select one of the available connectors that are displayed on the Review tool Dashboard.</span></span> <span data-ttu-id="08b95-127">Then, select **Connect**.</span><span class="sxs-lookup"><span data-stu-id="08b95-127">Then, select **Connect**.</span></span> 

  ![Content Moderator Add Connector page](images/connectors-5.png)

3.  <span data-ttu-id="08b95-129">In the **Ocp-Admin-Subscription-Key** box, paste the key that you copied.</span><span class="sxs-lookup"><span data-stu-id="08b95-129">In the **Ocp-Admin-Subscription-Key** box, paste the key that you copied.</span></span> <span data-ttu-id="08b95-130">Then, select **Save**.</span><span class="sxs-lookup"><span data-stu-id="08b95-130">Then, select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08b95-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="08b95-131">Next steps</span></span>

* <span data-ttu-id="08b95-132">Learn how to use connectors to [define custom workflows](workflows.md).</span><span class="sxs-lookup"><span data-stu-id="08b95-132">Learn how to use connectors to [define custom workflows](workflows.md).</span></span>
