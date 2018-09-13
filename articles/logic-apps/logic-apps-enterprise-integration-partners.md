---
title: Create partners for business-to-business (B2B) messages - Azure Logic Apps | Microsoft Docs
description: Learn how to add partners to your integration account with the Enterprise Integration Pack and Logic Apps
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: ''
ms.assetid: b179325c-a511-4c1b-9796-f7484b4f6873
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: estfan
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 93b3d778d52c8d842b69d30c89853bf038189f04
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563037"
---
# <a name="add-or-update-partners-in-business-to-business-agreements-in-your-workflow"></a><span data-ttu-id="d554a-103">Add or update partners in business-to-business agreements in your workflow</span><span class="sxs-lookup"><span data-stu-id="d554a-103">Add or update partners in business-to-business agreements in your workflow</span></span>

<span data-ttu-id="d554a-104">Partners are entities that participate in business-to-business (B2B) transactions and exchange messages between each other.</span><span class="sxs-lookup"><span data-stu-id="d554a-104">Partners are entities that participate in business-to-business (B2B) transactions and exchange messages between each other.</span></span> <span data-ttu-id="d554a-105">Before you can create partners that represent you and another organization in these transactions, you must both share information that identifies and validates messages sent by each other.</span><span class="sxs-lookup"><span data-stu-id="d554a-105">Before you can create partners that represent you and another organization in these transactions, you must both share information that identifies and validates messages sent by each other.</span></span> <span data-ttu-id="d554a-106">After you discuss these details and are ready to start your business relationship, you can create partners in your integration account to represent you both.</span><span class="sxs-lookup"><span data-stu-id="d554a-106">After you discuss these details and are ready to start your business relationship, you can create partners in your integration account to represent you both.</span></span>

## <a name="what-roles-do-partners-have-in-your-integration-account"></a><span data-ttu-id="d554a-107">What roles do partners have in your integration account?</span><span class="sxs-lookup"><span data-stu-id="d554a-107">What roles do partners have in your integration account?</span></span>

<span data-ttu-id="d554a-108">To define details about the messages exchanged between partners, you create agreements between those partners.</span><span class="sxs-lookup"><span data-stu-id="d554a-108">To define details about the messages exchanged between partners, you create agreements between those partners.</span></span> <span data-ttu-id="d554a-109">However, before you can create an agreement, you must have added at least two partners to your integration account.</span><span class="sxs-lookup"><span data-stu-id="d554a-109">However, before you can create an agreement, you must have added at least two partners to your integration account.</span></span> <span data-ttu-id="d554a-110">Your organization must be part of the agreement as the **host partner**.</span><span class="sxs-lookup"><span data-stu-id="d554a-110">Your organization must be part of the agreement as the **host partner**.</span></span> <span data-ttu-id="d554a-111">The other partner, or **guest partner** represents the organization that exchanges messages with your organization.</span><span class="sxs-lookup"><span data-stu-id="d554a-111">The other partner, or **guest partner** represents the organization that exchanges messages with your organization.</span></span> <span data-ttu-id="d554a-112">The guest partner can be another company, or even a department in your own organization.</span><span class="sxs-lookup"><span data-stu-id="d554a-112">The guest partner can be another company, or even a department in your own organization.</span></span>

<span data-ttu-id="d554a-113">After you add these partners, you can create an agreement.</span><span class="sxs-lookup"><span data-stu-id="d554a-113">After you add these partners, you can create an agreement.</span></span>

<span data-ttu-id="d554a-114">Receive and Send settings are oriented from the point of view of the Hosted Partner.</span><span class="sxs-lookup"><span data-stu-id="d554a-114">Receive and Send settings are oriented from the point of view of the Hosted Partner.</span></span> <span data-ttu-id="d554a-115">For example, the receive settings in an agreement determine how the hosted partner receives messages sent from a guest partner.</span><span class="sxs-lookup"><span data-stu-id="d554a-115">For example, the receive settings in an agreement determine how the hosted partner receives messages sent from a guest partner.</span></span> <span data-ttu-id="d554a-116">Likewise, the send settings on the agreement indicate how the hosted partner sends messages to the guest partner.</span><span class="sxs-lookup"><span data-stu-id="d554a-116">Likewise, the send settings on the agreement indicate how the hosted partner sends messages to the guest partner.</span></span>

## <a name="how-to-create-a-partner"></a><span data-ttu-id="d554a-117">How to create a partner?</span><span class="sxs-lookup"><span data-stu-id="d554a-117">How to create a partner?</span></span>

1. <span data-ttu-id="d554a-118">In the Azure portal, select **Browse**.</span><span class="sxs-lookup"><span data-stu-id="d554a-118">In the Azure portal, select **Browse**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-overview/overview-1.png)

2. <span data-ttu-id="d554a-119">In the filter search box, enter **integration**, then select **Integration Accounts** in the results list.</span><span class="sxs-lookup"><span data-stu-id="d554a-119">In the filter search box, enter **integration**, then select **Integration Accounts** in the results list.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-overview/overview-2.png)

3. <span data-ttu-id="d554a-120">Select the integration account where you want to add your partners.</span><span class="sxs-lookup"><span data-stu-id="d554a-120">Select the integration account where you want to add your partners.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="d554a-121">Select the **Partners** tile.</span><span class="sxs-lookup"><span data-stu-id="d554a-121">Select the **Partners** tile.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-partners/partner-1.png)

5. <span data-ttu-id="d554a-122">In the Partners blade, choose **Add**.</span><span class="sxs-lookup"><span data-stu-id="d554a-122">In the Partners blade, choose **Add**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-partners/partner-2.png)

6. <span data-ttu-id="d554a-123">Enter a name for your partner, then select a **Qualifier**.</span><span class="sxs-lookup"><span data-stu-id="d554a-123">Enter a name for your partner, then select a **Qualifier**.</span></span> <span data-ttu-id="d554a-124">Finally, enter a **Value** to help identify documents that come into your apps.</span><span class="sxs-lookup"><span data-stu-id="d554a-124">Finally, enter a **Value** to help identify documents that come into your apps.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-partners/partner-3.png)

7. <span data-ttu-id="d554a-125">To see the progress for your partner creation process, select the *bell* notification icon.</span><span class="sxs-lookup"><span data-stu-id="d554a-125">To see the progress for your partner creation process, select the *bell* notification icon.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-partners/partner-4.png)

8. <span data-ttu-id="d554a-126">To confirm that your new partners were successfully added, select the **Partners** tile.</span><span class="sxs-lookup"><span data-stu-id="d554a-126">To confirm that your new partners were successfully added, select the **Partners** tile.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-partners/partner-5.png)

    <span data-ttu-id="d554a-127">After you select the Partners tile, you'll also see  newly added partners in the Partners blade.</span><span class="sxs-lookup"><span data-stu-id="d554a-127">After you select the Partners tile, you'll also see  newly added partners in the Partners blade.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-partners/partner-6.png)

## <a name="how-to-edit-existing-partners-in-your-integration-account"></a><span data-ttu-id="d554a-128">How to edit existing partners in your integration account</span><span class="sxs-lookup"><span data-stu-id="d554a-128">How to edit existing partners in your integration account</span></span>

1. <span data-ttu-id="d554a-129">Select the **Partners** tile.</span><span class="sxs-lookup"><span data-stu-id="d554a-129">Select the **Partners** tile.</span></span>
2. <span data-ttu-id="d554a-130">After the Partners blade opens, select the partner you want to edit.</span><span class="sxs-lookup"><span data-stu-id="d554a-130">After the Partners blade opens, select the partner you want to edit.</span></span>
3. <span data-ttu-id="d554a-131">On the **Update Partner** tile, make your changes.</span><span class="sxs-lookup"><span data-stu-id="d554a-131">On the **Update Partner** tile, make your changes.</span></span>
4. <span data-ttu-id="d554a-132">After you're done, choose **Save**, or to cancel your changes, select **Discard**.</span><span class="sxs-lookup"><span data-stu-id="d554a-132">After you're done, choose **Save**, or to cancel your changes, select **Discard**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-partners/edit-1.png)

## <a name="how-to-delete-a-partner"></a><span data-ttu-id="d554a-133">How to delete a partner</span><span class="sxs-lookup"><span data-stu-id="d554a-133">How to delete a partner</span></span>

1. <span data-ttu-id="d554a-134">Select the **Partners** tile.</span><span class="sxs-lookup"><span data-stu-id="d554a-134">Select the **Partners** tile.</span></span>
2. <span data-ttu-id="d554a-135">After the Partner blade opens, select the partner that you want to delete.</span><span class="sxs-lookup"><span data-stu-id="d554a-135">After the Partner blade opens, select the partner that you want to delete.</span></span>
3. <span data-ttu-id="d554a-136">Choose **Delete**.</span><span class="sxs-lookup"><span data-stu-id="d554a-136">Choose **Delete**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-partners/delete-1.png)

## <a name="next-steps"></a><span data-ttu-id="d554a-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="d554a-137">Next steps</span></span>
* [<span data-ttu-id="d554a-138">Learn more about agreements</span><span class="sxs-lookup"><span data-stu-id="d554a-138">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Learn about enterprise integration agreements")  












