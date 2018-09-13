---
title: Encode AS2 messages - Azure Logic Apps | Microsoft Docs
description: How to use the AS2 encoder in the Enterprise Integration Pack for Azure Logic Apps
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: ''
ms.assetid: 332fb9e3-576c-4683-bd10-d177a0ebe9a3
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: padmavc
ms.openlocfilehash: 2fc3337cb11d84d20d1a5f63034fcf49ea44fc7b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549171"
---
# <a name="encode-as2-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="1b2fb-103">Encode AS2 messages for Azure Logic Apps with the Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="1b2fb-103">Encode AS2 messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="1b2fb-104">To establish security and reliability while transmitting messages, use the Encode AS2 message connector.</span><span class="sxs-lookup"><span data-stu-id="1b2fb-104">To establish security and reliability while transmitting messages, use the Encode AS2 message connector.</span></span> <span data-ttu-id="1b2fb-105">This connector provides digital signing, encryption, and acknowledgements through Message Disposition Notifications (MDN), which also leads to support for Non-Repudiation.</span><span class="sxs-lookup"><span data-stu-id="1b2fb-105">This connector provides digital signing, encryption, and acknowledgements through Message Disposition Notifications (MDN), which also leads to support for Non-Repudiation.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="1b2fb-106">Before you start</span><span class="sxs-lookup"><span data-stu-id="1b2fb-106">Before you start</span></span>

<span data-ttu-id="1b2fb-107">Here's the items you need:</span><span class="sxs-lookup"><span data-stu-id="1b2fb-107">Here's the items you need:</span></span>

* <span data-ttu-id="1b2fb-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="1b2fb-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="1b2fb-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="1b2fb-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="1b2fb-110">You must have an integration account to use the Encode AS2 message connector.</span><span class="sxs-lookup"><span data-stu-id="1b2fb-110">You must have an integration account to use the Encode AS2 message connector.</span></span>
* <span data-ttu-id="1b2fb-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span><span class="sxs-lookup"><span data-stu-id="1b2fb-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="1b2fb-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span><span class="sxs-lookup"><span data-stu-id="1b2fb-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span></span>

## <a name="encode-as2-messages"></a><span data-ttu-id="1b2fb-113">Encode AS2 messages</span><span class="sxs-lookup"><span data-stu-id="1b2fb-113">Encode AS2 messages</span></span>

1. <span data-ttu-id="1b2fb-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="1b2fb-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="1b2fb-115">The Encode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span><span class="sxs-lookup"><span data-stu-id="1b2fb-115">The Encode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="1b2fb-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span><span class="sxs-lookup"><span data-stu-id="1b2fb-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="1b2fb-117">In the search box, enter "AS2" for your filter.</span><span class="sxs-lookup"><span data-stu-id="1b2fb-117">In the search box, enter "AS2" for your filter.</span></span> <span data-ttu-id="1b2fb-118">Select **AS2 - Encode AS2 message**.</span><span class="sxs-lookup"><span data-stu-id="1b2fb-118">Select **AS2 - Encode AS2 message**.</span></span>
   
    ![Search for "AS2"](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-as2-encode/as2decodeimage1.png)

4. <span data-ttu-id="1b2fb-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span><span class="sxs-lookup"><span data-stu-id="1b2fb-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="1b2fb-121">Name your connection, and select the integration account that you want to connect.</span><span class="sxs-lookup"><span data-stu-id="1b2fb-121">Name your connection, and select the integration account that you want to connect.</span></span> 
   
    ![create connection to integration account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-as2-encode/as2encodeimage1.png)  

    <span data-ttu-id="1b2fb-123">Properties with an asterisk are required.</span><span class="sxs-lookup"><span data-stu-id="1b2fb-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="1b2fb-124">Property</span><span class="sxs-lookup"><span data-stu-id="1b2fb-124">Property</span></span> | <span data-ttu-id="1b2fb-125">Details</span><span class="sxs-lookup"><span data-stu-id="1b2fb-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="1b2fb-126">Connection Name \*</span><span class="sxs-lookup"><span data-stu-id="1b2fb-126">Connection Name \*</span></span> |<span data-ttu-id="1b2fb-127">Enter any name for your connection.</span><span class="sxs-lookup"><span data-stu-id="1b2fb-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="1b2fb-128">Integration Account \*</span><span class="sxs-lookup"><span data-stu-id="1b2fb-128">Integration Account \*</span></span> |<span data-ttu-id="1b2fb-129">Enter a name for your integration account.</span><span class="sxs-lookup"><span data-stu-id="1b2fb-129">Enter a name for your integration account.</span></span> <span data-ttu-id="1b2fb-130">Make sure that your integration account and logic app are in the same Azure location.</span><span class="sxs-lookup"><span data-stu-id="1b2fb-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="1b2fb-131">When you're done, your connection details should look similar to this example.</span><span class="sxs-lookup"><span data-stu-id="1b2fb-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="1b2fb-132">To finish creating your connection, choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="1b2fb-132">To finish creating your connection, choose **Create**.</span></span>
   
    ![integration connection details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-as2-encode/as2encodeimage2.png)

6. <span data-ttu-id="1b2fb-134">After your connection is created, as shown in this example, provide details for **AS2-From**, **AS2-To identifiers** as configured in your agreement, and **Body**, which is the message payload.</span><span class="sxs-lookup"><span data-stu-id="1b2fb-134">After your connection is created, as shown in this example, provide details for **AS2-From**, **AS2-To identifiers** as configured in your agreement, and **Body**, which is the message payload.</span></span>
   
    ![provide mandatory fields](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-as2-encode/as2encodeimage3.png)

## <a name="as2-encoder-details"></a><span data-ttu-id="1b2fb-136">AS2 encoder details</span><span class="sxs-lookup"><span data-stu-id="1b2fb-136">AS2 encoder details</span></span>

<span data-ttu-id="1b2fb-137">The Encode AS2 connector performs these tasks:</span><span class="sxs-lookup"><span data-stu-id="1b2fb-137">The Encode AS2 connector performs these tasks:</span></span> 

* <span data-ttu-id="1b2fb-138">Applies AS2/HTTP headers</span><span class="sxs-lookup"><span data-stu-id="1b2fb-138">Applies AS2/HTTP headers</span></span>
* <span data-ttu-id="1b2fb-139">Signs outgoing messages (if configured)</span><span class="sxs-lookup"><span data-stu-id="1b2fb-139">Signs outgoing messages (if configured)</span></span>
* <span data-ttu-id="1b2fb-140">Encrypts outgoing messages (if configured)</span><span class="sxs-lookup"><span data-stu-id="1b2fb-140">Encrypts outgoing messages (if configured)</span></span>
* <span data-ttu-id="1b2fb-141">Compresses the message (if configured)</span><span class="sxs-lookup"><span data-stu-id="1b2fb-141">Compresses the message (if configured)</span></span>

## <a name="try-this-sample"></a><span data-ttu-id="1b2fb-142">Try this sample</span><span class="sxs-lookup"><span data-stu-id="1b2fb-142">Try this sample</span></span>

<span data-ttu-id="1b2fb-143">To try deploying a fully operational logic app and sample AS2 scenario, see the [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span><span class="sxs-lookup"><span data-stu-id="1b2fb-143">To try deploying a fully operational logic app and sample AS2 scenario, see the [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b2fb-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="1b2fb-144">Next steps</span></span>
[<span data-ttu-id="1b2fb-145">Learn more about the Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="1b2fb-145">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Learn about Enterprise Integration Pack") 





