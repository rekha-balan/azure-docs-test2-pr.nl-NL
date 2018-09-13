---
title: Manage integration account artifact metadata - Azure Logic Apps | Microsoft Docs
description: Add or retrieve artifact metadata from integration accounts for Azure Logic Apps
author: padmavc
manager: anneta
editor: ''
services: logic-apps
documentationcenter: ''
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 11/21/2016
ms.author: padmavc
ms.openlocfilehash: 25623fe8585b696e2c88cb564c60cd442c150f3c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660977"
---
# <a name="manage-artifact-metadata-in-integration-accounts-for-logic-apps"></a><span data-ttu-id="304ea-103">Manage artifact metadata in integration accounts for logic apps</span><span class="sxs-lookup"><span data-stu-id="304ea-103">Manage artifact metadata in integration accounts for logic apps</span></span>

<span data-ttu-id="304ea-104">You can define custom metadata for artifacts in integration accounts and retrieve that metadata during runtime for your logic app.</span><span class="sxs-lookup"><span data-stu-id="304ea-104">You can define custom metadata for artifacts in integration accounts and retrieve that metadata during runtime for your logic app.</span></span> <span data-ttu-id="304ea-105">For example, you can specify metadata for artifacts like partners, agreements, schemas, and maps - all store metadata using key-value pairs.</span><span class="sxs-lookup"><span data-stu-id="304ea-105">For example, you can specify metadata for artifacts like partners, agreements, schemas, and maps - all store metadata using key-value pairs.</span></span> <span data-ttu-id="304ea-106">Currently, artifacts can't create metadata through UI, but you can use REST APIs to create metadata.</span><span class="sxs-lookup"><span data-stu-id="304ea-106">Currently, artifacts can't create metadata through UI, but you can use REST APIs to create metadata.</span></span> <span data-ttu-id="304ea-107">To add metadata when you create or select a partner, agreement, or schema in the Azure portal, choose **Edit as JSON**.</span><span class="sxs-lookup"><span data-stu-id="304ea-107">To add metadata when you create or select a partner, agreement, or schema in the Azure portal, choose **Edit as JSON**.</span></span> <span data-ttu-id="304ea-108">To retrieve artifact metadata in logic apps, you can use the Integration Account Artifact Lookup feature.</span><span class="sxs-lookup"><span data-stu-id="304ea-108">To retrieve artifact metadata in logic apps, you can use the Integration Account Artifact Lookup feature.</span></span>

## <a name="add-metadata-to-artifacts-in-integration-accounts"></a><span data-ttu-id="304ea-109">Add metadata to artifacts in integration accounts</span><span class="sxs-lookup"><span data-stu-id="304ea-109">Add metadata to artifacts in integration accounts</span></span>

1. <span data-ttu-id="304ea-110">Create an [integration account](logic-apps-enterprise-integration-create-integration-account.md).</span><span class="sxs-lookup"><span data-stu-id="304ea-110">Create an [integration account](logic-apps-enterprise-integration-create-integration-account.md).</span></span>

2. <span data-ttu-id="304ea-111">Add an artifact to your integration account, for example, a [partner](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), [agreement](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements), or [schema](logic-apps-enterprise-integration-schemas.md).</span><span class="sxs-lookup"><span data-stu-id="304ea-111">Add an artifact to your integration account, for example, a [partner](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), [agreement](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements), or [schema](logic-apps-enterprise-integration-schemas.md).</span></span>

3.  <span data-ttu-id="304ea-112">Select the artifact, choose **Edit as JSON**, and enter metadata details.</span><span class="sxs-lookup"><span data-stu-id="304ea-112">Select the artifact, choose **Edit as JSON**, and enter metadata details.</span></span>

    ![Enter metadata](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-metadata/image1.png)

## <a name="retrieve-metadata-from-artifacts-for-logic-apps"></a><span data-ttu-id="304ea-114">Retrieve metadata from artifacts for logic apps</span><span class="sxs-lookup"><span data-stu-id="304ea-114">Retrieve metadata from artifacts for logic apps</span></span>

1. <span data-ttu-id="304ea-115">Create a [logic app](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="304ea-115">Create a [logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="304ea-116">Create a [link from your logic app to your integration account](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app).</span><span class="sxs-lookup"><span data-stu-id="304ea-116">Create a [link from your logic app to your integration account](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app).</span></span> 

3. <span data-ttu-id="304ea-117">In Logic App Designer, add a trigger like *Request* or *HTTP* to your logic app.</span><span class="sxs-lookup"><span data-stu-id="304ea-117">In Logic App Designer, add a trigger like *Request* or *HTTP* to your logic app.</span></span>

4.  <span data-ttu-id="304ea-118">Choose **Next Step** > **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="304ea-118">Choose **Next Step** > **Add an action**.</span></span> <span data-ttu-id="304ea-119">Search for *integration* so you can find and then select **Integration Account - Integration Account Artifact Lookup**.</span><span class="sxs-lookup"><span data-stu-id="304ea-119">Search for *integration* so you can find and then select **Integration Account - Integration Account Artifact Lookup**.</span></span>

    ![Select Integration Account Artifact Lookup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-metadata/image2.png)

5. <span data-ttu-id="304ea-121">Select the **Artifact Type**, and provide the **Artifact Name**.</span><span class="sxs-lookup"><span data-stu-id="304ea-121">Select the **Artifact Type**, and provide the **Artifact Name**.</span></span>

    ![Select artifact type and specify artifact name](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-metadata/image3.png)

## <a name="example-retrieve-partner-metadata"></a><span data-ttu-id="304ea-123">Example: Retrieve partner metadata</span><span class="sxs-lookup"><span data-stu-id="304ea-123">Example: Retrieve partner metadata</span></span>

<span data-ttu-id="304ea-124">Partner metadata has these `routingUrl` details:</span><span class="sxs-lookup"><span data-stu-id="304ea-124">Partner metadata has these `routingUrl` details:</span></span>

![Find partner "routingURL" metadata](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-metadata/image6.png)

1. <span data-ttu-id="304ea-126">In your logic app, add your trigger, an **Integration Account - Integration Account Artifact Lookup** action for your partner, and an **HTTP**.</span><span class="sxs-lookup"><span data-stu-id="304ea-126">In your logic app, add your trigger, an **Integration Account - Integration Account Artifact Lookup** action for your partner, and an **HTTP**.</span></span>

    ![Add trigger, artifact lookup, and "HTTP" to your logic app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-metadata/image4.png)

2. <span data-ttu-id="304ea-128">To retrieve the URI, go to Code View for your logic app.</span><span class="sxs-lookup"><span data-stu-id="304ea-128">To retrieve the URI, go to Code View for your logic app.</span></span> <span data-ttu-id="304ea-129">Your logic app definition should look like this example:</span><span class="sxs-lookup"><span data-stu-id="304ea-129">Your logic app definition should look like this example:</span></span>

    ![Search lookup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-metadata/image5.png)


## <a name="next-steps"></a><span data-ttu-id="304ea-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="304ea-131">Next steps</span></span>
* [<span data-ttu-id="304ea-132">Learn more about agreements</span><span class="sxs-lookup"><span data-stu-id="304ea-132">Learn more about agreements</span></span>](logic-apps-enterprise-integration-agreements.md "Learn about enterprise integration agreements")  






