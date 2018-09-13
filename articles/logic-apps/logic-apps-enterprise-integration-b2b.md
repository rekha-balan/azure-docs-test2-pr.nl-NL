---
title: Create B2B solutions - Azure Logic Apps | Microsoft Docs
description: Receive data in logic apps by using the B2B features in the Enterprise Integration Pack
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 20fc3722-6f8b-402f-b391-b84e9df6fcff
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: estfan
ms.openlocfilehash: 5cc464323c7f0feb8cba9ffe21881c803e799ab2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552418"
---
# <a name="receive-data-in-logic-apps-with-the-b2b-features-in-the-enterprise-integration-pack"></a><span data-ttu-id="849ae-103">Receive data in logic apps with the B2B features in the Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="849ae-103">Receive data in logic apps with the B2B features in the Enterprise Integration Pack</span></span>

<span data-ttu-id="849ae-104">After you create an integration account that has partners and agreements, you are ready to create a business to business (B2B) workflow for your logic app with the [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="849ae-104">After you create an integration account that has partners and agreements, you are ready to create a business to business (B2B) workflow for your logic app with the [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="849ae-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="849ae-105">Prerequisites</span></span>

<span data-ttu-id="849ae-106">To use the AS2 and X12 actions, you must have an Enterprise Integration Account.</span><span class="sxs-lookup"><span data-stu-id="849ae-106">To use the AS2 and X12 actions, you must have an Enterprise Integration Account.</span></span> <span data-ttu-id="849ae-107">Learn [how to create an Enterprise Integration Account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="849ae-107">Learn [how to create an Enterprise Integration Account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span></span>

## <a name="create-a-logic-app-with-b2b-connectors"></a><span data-ttu-id="849ae-108">Create a logic app with B2B connectors</span><span class="sxs-lookup"><span data-stu-id="849ae-108">Create a logic app with B2B connectors</span></span>

<span data-ttu-id="849ae-109">Follow these steps to create a B2B logic app that uses the AS2 and X12 actions to receive data from a trading partner:</span><span class="sxs-lookup"><span data-stu-id="849ae-109">Follow these steps to create a B2B logic app that uses the AS2 and X12 actions to receive data from a trading partner:</span></span>

1. <span data-ttu-id="849ae-110">Create a logic app, then [link your app to your integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="849ae-110">Create a logic app, then [link your app to your integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span></span>

2. <span data-ttu-id="849ae-111">Add a **Request - When an HTTP request is received** trigger to your logic app.</span><span class="sxs-lookup"><span data-stu-id="849ae-111">Add a **Request - When an HTTP request is received** trigger to your logic app.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b/flatfile-1.png)

3. <span data-ttu-id="849ae-112">To add the **Decode AS2** action, select **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="849ae-112">To add the **Decode AS2** action, select **Add an action**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b/transform-2.png)

4. <span data-ttu-id="849ae-113">To filter all actions to the one that you want, enter the word **as2** in the search box.</span><span class="sxs-lookup"><span data-stu-id="849ae-113">To filter all actions to the one that you want, enter the word **as2** in the search box.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b/b2b-5.png)

5. <span data-ttu-id="849ae-114">Select the **AS2 - Decode AS2 message** action.</span><span class="sxs-lookup"><span data-stu-id="849ae-114">Select the **AS2 - Decode AS2 message** action.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b/b2b-6.png)

6. <span data-ttu-id="849ae-115">Add the **Body** that you want to use as input.</span><span class="sxs-lookup"><span data-stu-id="849ae-115">Add the **Body** that you want to use as input.</span></span> <span data-ttu-id="849ae-116">In this example, select the body of the HTTP request that triggers the logic app.</span><span class="sxs-lookup"><span data-stu-id="849ae-116">In this example, select the body of the HTTP request that triggers the logic app.</span></span> <span data-ttu-id="849ae-117">Or enter an expression that inputs the headers in the **HEADERS** field:</span><span class="sxs-lookup"><span data-stu-id="849ae-117">Or enter an expression that inputs the headers in the **HEADERS** field:</span></span>

    <span data-ttu-id="849ae-118">@triggerOutputs()['headers']</span><span class="sxs-lookup"><span data-stu-id="849ae-118">@triggerOutputs()['headers']</span></span>

7. <span data-ttu-id="849ae-119">Add the required **Headers** for AS2, which you can find in the HTTP request headers.</span><span class="sxs-lookup"><span data-stu-id="849ae-119">Add the required **Headers** for AS2, which you can find in the HTTP request headers.</span></span> <span data-ttu-id="849ae-120">In this example, select the headers of the HTTP request that trigger the logic app.</span><span class="sxs-lookup"><span data-stu-id="849ae-120">In this example, select the headers of the HTTP request that trigger the logic app.</span></span>

8. <span data-ttu-id="849ae-121">Now add the Decode X12 message action.</span><span class="sxs-lookup"><span data-stu-id="849ae-121">Now add the Decode X12 message action.</span></span> <span data-ttu-id="849ae-122">Select **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="849ae-122">Select **Add an action**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b/b2b-9.png)

9. <span data-ttu-id="849ae-123">To filter all actions to the one that you want, enter the word **x12** in the search box.</span><span class="sxs-lookup"><span data-stu-id="849ae-123">To filter all actions to the one that you want, enter the word **x12** in the search box.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b/b2b-10.png)

10. <span data-ttu-id="849ae-124">Select the **X12 - Decode X12 message** action.</span><span class="sxs-lookup"><span data-stu-id="849ae-124">Select the **X12 - Decode X12 message** action.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b/b2b-as2message.png)

11. <span data-ttu-id="849ae-125">Now you must specify the input to this action.</span><span class="sxs-lookup"><span data-stu-id="849ae-125">Now you must specify the input to this action.</span></span> <span data-ttu-id="849ae-126">This input is the output from the previous AS2 action.</span><span class="sxs-lookup"><span data-stu-id="849ae-126">This input is the output from the previous AS2 action.</span></span>

    <span data-ttu-id="849ae-127">The actual message content is in a JSON object and is base64 encoded, so you must specify an expression as the input.</span><span class="sxs-lookup"><span data-stu-id="849ae-127">The actual message content is in a JSON object and is base64 encoded, so you must specify an expression as the input.</span></span> 
    <span data-ttu-id="849ae-128">Enter the following expression in the **X12 FLAT FILE MESSAGE TO DECODE** input field:</span><span class="sxs-lookup"><span data-stu-id="849ae-128">Enter the following expression in the **X12 FLAT FILE MESSAGE TO DECODE** input field:</span></span>
    
    <span data-ttu-id="849ae-129">@base64ToString(body('Decode_AS2_message')?['AS2Message']?['Content'])</span><span class="sxs-lookup"><span data-stu-id="849ae-129">@base64ToString(body('Decode_AS2_message')?['AS2Message']?['Content'])</span></span>

    <span data-ttu-id="849ae-130">Now add steps to decode the X12 data received from the trading partner and output items in a JSON object.</span><span class="sxs-lookup"><span data-stu-id="849ae-130">Now add steps to decode the X12 data received from the trading partner and output items in a JSON object.</span></span> 
    <span data-ttu-id="849ae-131">To notify the partner that the data was received, you can send back a response containing the AS2 Message Disposition Notification (MDN) in an HTTP Response Action.</span><span class="sxs-lookup"><span data-stu-id="849ae-131">To notify the partner that the data was received, you can send back a response containing the AS2 Message Disposition Notification (MDN) in an HTTP Response Action.</span></span>

12. <span data-ttu-id="849ae-132">To add the **Response** action, choose **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="849ae-132">To add the **Response** action, choose **Add an action**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b/b2b-14.png)

13. <span data-ttu-id="849ae-133">To filter all actions to the one that you want, enter the word **response** in the search box.</span><span class="sxs-lookup"><span data-stu-id="849ae-133">To filter all actions to the one that you want, enter the word **response** in the search box.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b/b2b-15.png)

14. <span data-ttu-id="849ae-134">Select the **Response** action.</span><span class="sxs-lookup"><span data-stu-id="849ae-134">Select the **Response** action.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b/b2b-16.png)

15. <span data-ttu-id="849ae-135">To access the MDN from the output of the **Decode X12 message** action, set the response **BODY** field with this expression:</span><span class="sxs-lookup"><span data-stu-id="849ae-135">To access the MDN from the output of the **Decode X12 message** action, set the response **BODY** field with this expression:</span></span>

    <span data-ttu-id="849ae-136">@base64ToString(body('Decode_AS2_message')?['OutgoingMdn']?['Content'])</span><span class="sxs-lookup"><span data-stu-id="849ae-136">@base64ToString(body('Decode_AS2_message')?['OutgoingMdn']?['Content'])</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b/b2b-17.png)  

16. <span data-ttu-id="849ae-137">Save your work.</span><span class="sxs-lookup"><span data-stu-id="849ae-137">Save your work.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b/transform-5.png)  

<span data-ttu-id="849ae-138">You are now done setting up your B2B logic app.</span><span class="sxs-lookup"><span data-stu-id="849ae-138">You are now done setting up your B2B logic app.</span></span> <span data-ttu-id="849ae-139">In a real world application, you might want to store the decoded X12 data in a line-of-business (LOB) app or data store.</span><span class="sxs-lookup"><span data-stu-id="849ae-139">In a real world application, you might want to store the decoded X12 data in a line-of-business (LOB) app or data store.</span></span> <span data-ttu-id="849ae-140">To connect your own LOB apps and use these APIs in your logic app, you can add further actions or write custom APIs.</span><span class="sxs-lookup"><span data-stu-id="849ae-140">To connect your own LOB apps and use these APIs in your logic app, you can add further actions or write custom APIs.</span></span>

## <a name="features-and-use-cases"></a><span data-ttu-id="849ae-141">Features and use cases</span><span class="sxs-lookup"><span data-stu-id="849ae-141">Features and use cases</span></span>

* <span data-ttu-id="849ae-142">The AS2 and X12 decode and encode actions let you exchange data between trading partners by using industry standard protocols in logic apps.</span><span class="sxs-lookup"><span data-stu-id="849ae-142">The AS2 and X12 decode and encode actions let you exchange data between trading partners by using industry standard protocols in logic apps.</span></span>
* <span data-ttu-id="849ae-143">To exchange data with trading partners, you can use AS2 and X12 with or without each other.</span><span class="sxs-lookup"><span data-stu-id="849ae-143">To exchange data with trading partners, you can use AS2 and X12 with or without each other.</span></span>
* <span data-ttu-id="849ae-144">The B2B actions help you create partners and agreements easily in your integration account and consume them in a logic app.</span><span class="sxs-lookup"><span data-stu-id="849ae-144">The B2B actions help you create partners and agreements easily in your integration account and consume them in a logic app.</span></span>
* <span data-ttu-id="849ae-145">When you extend your logic app with other actions, you can send and receive data between other apps and services like SalesForce.</span><span class="sxs-lookup"><span data-stu-id="849ae-145">When you extend your logic app with other actions, you can send and receive data between other apps and services like SalesForce.</span></span>

## <a name="learn-more"></a><span data-ttu-id="849ae-146">Learn more</span><span class="sxs-lookup"><span data-stu-id="849ae-146">Learn more</span></span>
[<span data-ttu-id="849ae-147">Learn more about the Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="849ae-147">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md)












