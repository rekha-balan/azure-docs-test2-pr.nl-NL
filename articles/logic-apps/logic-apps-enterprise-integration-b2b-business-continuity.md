---
title: Disaster recovery for B2B integration accounts - Azure Logic Apps | Microsoft Docs
description: Get ready for cross-region disaster recovery in Azure Logic Apps
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: divyaswarnkar
ms.author: divswa
ms.reviewer: jonfan, estfan, LADocs
ms.topic: article
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.date: 04/10/2017
ms.openlocfilehash: 3d465123f814887282bf2b29a5b6e0836601c243
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44771725"
---
# <a name="cross-region-disaster-recovery-for-b2b-integration-accounts-in-azure-logic-apps"></a><span data-ttu-id="c4d05-103">Cross-region disaster recovery for B2B integration accounts in Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="c4d05-103">Cross-region disaster recovery for B2B integration accounts in Azure Logic Apps</span></span>

<span data-ttu-id="c4d05-104">B2B workloads involve money transactions like orders and invoices.</span><span class="sxs-lookup"><span data-stu-id="c4d05-104">B2B workloads involve money transactions like orders and invoices.</span></span> <span data-ttu-id="c4d05-105">During a disaster event, it's critical for a business to quickly recover to meet the business-level SLAs agreed upon with their partners.</span><span class="sxs-lookup"><span data-stu-id="c4d05-105">During a disaster event, it's critical for a business to quickly recover to meet the business-level SLAs agreed upon with their partners.</span></span> <span data-ttu-id="c4d05-106">This article demonstrates how to build a business continuity plan for B2B workloads.</span><span class="sxs-lookup"><span data-stu-id="c4d05-106">This article demonstrates how to build a business continuity plan for B2B workloads.</span></span> 

* <span data-ttu-id="c4d05-107">Disaster Recovery readiness</span><span class="sxs-lookup"><span data-stu-id="c4d05-107">Disaster Recovery readiness</span></span> 
* <span data-ttu-id="c4d05-108">Fail over to secondary region during a disaster event</span><span class="sxs-lookup"><span data-stu-id="c4d05-108">Fail over to secondary region during a disaster event</span></span> 
* <span data-ttu-id="c4d05-109">Fall back to primary region after a disaster event</span><span class="sxs-lookup"><span data-stu-id="c4d05-109">Fall back to primary region after a disaster event</span></span>

## <a name="disaster-recovery-readiness"></a><span data-ttu-id="c4d05-110">Disaster Recovery readiness</span><span class="sxs-lookup"><span data-stu-id="c4d05-110">Disaster Recovery readiness</span></span>  

1. <span data-ttu-id="c4d05-111">Identify a secondary region and create an [integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) in the secondary region.</span><span class="sxs-lookup"><span data-stu-id="c4d05-111">Identify a secondary region and create an [integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) in the secondary region.</span></span>

2. <span data-ttu-id="c4d05-112">Add partners, schemas, and agreements for the required message flows where the run status needs to be replicated to secondary region integration account.</span><span class="sxs-lookup"><span data-stu-id="c4d05-112">Add partners, schemas, and agreements for the required message flows where the run status needs to be replicated to secondary region integration account.</span></span>

   > [!TIP]
   > <span data-ttu-id="c4d05-113">Make sure there's consistency in the integration account artifact's naming convention across regions.</span><span class="sxs-lookup"><span data-stu-id="c4d05-113">Make sure there's consistency in the integration account artifact's naming convention across regions.</span></span> 

3. <span data-ttu-id="c4d05-114">To pull the run status from the primary region, create a logic app in the secondary region.</span><span class="sxs-lookup"><span data-stu-id="c4d05-114">To pull the run status from the primary region, create a logic app in the secondary region.</span></span> 

   <span data-ttu-id="c4d05-115">This logic app should have a *trigger* and an *action*.</span><span class="sxs-lookup"><span data-stu-id="c4d05-115">This logic app should have a *trigger* and an *action*.</span></span> 
   <span data-ttu-id="c4d05-116">The trigger should connect to primary region integration account, and the action should connect to secondary region integration account.</span><span class="sxs-lookup"><span data-stu-id="c4d05-116">The trigger should connect to primary region integration account, and the action should connect to secondary region integration account.</span></span> 
   <span data-ttu-id="c4d05-117">Based on the time interval, the trigger polls the primary region run status table and pulls the new records, if any.</span><span class="sxs-lookup"><span data-stu-id="c4d05-117">Based on the time interval, the trigger polls the primary region run status table and pulls the new records, if any.</span></span> <span data-ttu-id="c4d05-118">The action updates them to secondary region integration account.</span><span class="sxs-lookup"><span data-stu-id="c4d05-118">The action updates them to secondary region integration account.</span></span> 
   <span data-ttu-id="c4d05-119">This helps to get incremental runtime status from primary region to secondary region.</span><span class="sxs-lookup"><span data-stu-id="c4d05-119">This helps to get incremental runtime status from primary region to secondary region.</span></span>

4. <span data-ttu-id="c4d05-120">Business continuity in Logic Apps integration account is designed to support based on B2B protocols - X12, AS2, and EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="c4d05-120">Business continuity in Logic Apps integration account is designed to support based on B2B protocols - X12, AS2, and EDIFACT.</span></span> <span data-ttu-id="c4d05-121">To find detailed steps, select the respective links.</span><span class="sxs-lookup"><span data-stu-id="c4d05-121">To find detailed steps, select the respective links.</span></span>

5. <span data-ttu-id="c4d05-122">The recommendation is to deploy all primary region resources in a secondary region too.</span><span class="sxs-lookup"><span data-stu-id="c4d05-122">The recommendation is to deploy all primary region resources in a secondary region too.</span></span> 

   <span data-ttu-id="c4d05-123">Primary region resources include Azure SQL Database or Azure Cosmos DB, Azure Service Bus and Azure Event Hubs used for messaging, Azure API Management, and the Azure Logic Apps feature in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="c4d05-123">Primary region resources include Azure SQL Database or Azure Cosmos DB, Azure Service Bus and Azure Event Hubs used for messaging, Azure API Management, and the Azure Logic Apps feature in Azure App Service.</span></span>   

6. <span data-ttu-id="c4d05-124">Establish a connection from a primary region to a secondary region.</span><span class="sxs-lookup"><span data-stu-id="c4d05-124">Establish a connection from a primary region to a secondary region.</span></span> <span data-ttu-id="c4d05-125">To pull the run status from a primary region, create a logic app in a secondary region.</span><span class="sxs-lookup"><span data-stu-id="c4d05-125">To pull the run status from a primary region, create a logic app in a secondary region.</span></span> 

   <span data-ttu-id="c4d05-126">The logic app should have a trigger and an action.</span><span class="sxs-lookup"><span data-stu-id="c4d05-126">The logic app should have a trigger and an action.</span></span> 
   <span data-ttu-id="c4d05-127">The trigger should connect to a primary region integration account.</span><span class="sxs-lookup"><span data-stu-id="c4d05-127">The trigger should connect to a primary region integration account.</span></span> 
   <span data-ttu-id="c4d05-128">The action should connect to a secondary region integration account.</span><span class="sxs-lookup"><span data-stu-id="c4d05-128">The action should connect to a secondary region integration account.</span></span> 
   <span data-ttu-id="c4d05-129">Based on the time interval, the trigger polls the primary region run status table and pulls the new records, if any.</span><span class="sxs-lookup"><span data-stu-id="c4d05-129">Based on the time interval, the trigger polls the primary region run status table and pulls the new records, if any.</span></span> 
   <span data-ttu-id="c4d05-130">The action updates them to a secondary region integration account.</span><span class="sxs-lookup"><span data-stu-id="c4d05-130">The action updates them to a secondary region integration account.</span></span> 
   <span data-ttu-id="c4d05-131">This process helps to get incremental runtime status from the primary region to the secondary region.</span><span class="sxs-lookup"><span data-stu-id="c4d05-131">This process helps to get incremental runtime status from the primary region to the secondary region.</span></span>

<span data-ttu-id="c4d05-132">Business continuity in a Logic Apps integration account provides support based on the B2B protocols X12, AS2, and EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="c4d05-132">Business continuity in a Logic Apps integration account provides support based on the B2B protocols X12, AS2, and EDIFACT.</span></span> <span data-ttu-id="c4d05-133">For detailed steps on using X12 and AS2, see [X12](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) and [AS2](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2) in this article.</span><span class="sxs-lookup"><span data-stu-id="c4d05-133">For detailed steps on using X12 and AS2, see [X12](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) and [AS2](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2) in this article.</span></span>

## <a name="fail-over-to-a-secondary-region-during-a-disaster-event"></a><span data-ttu-id="c4d05-134">Fail over to a secondary region during a disaster event</span><span class="sxs-lookup"><span data-stu-id="c4d05-134">Fail over to a secondary region during a disaster event</span></span>

<span data-ttu-id="c4d05-135">During a disaster event, when the primary region is not available for business continuity, direct traffic to the secondary region.</span><span class="sxs-lookup"><span data-stu-id="c4d05-135">During a disaster event, when the primary region is not available for business continuity, direct traffic to the secondary region.</span></span> <span data-ttu-id="c4d05-136">A secondary region helps a business to recover functions quickly to meet the RPO/RTO agreed upon by their partners.</span><span class="sxs-lookup"><span data-stu-id="c4d05-136">A secondary region helps a business to recover functions quickly to meet the RPO/RTO agreed upon by their partners.</span></span> <span data-ttu-id="c4d05-137">It also minimizes efforts to fail over from one region to another region.</span><span class="sxs-lookup"><span data-stu-id="c4d05-137">It also minimizes efforts to fail over from one region to another region.</span></span> 

<span data-ttu-id="c4d05-138">There is an expected latency while copying control numbers from a primary region to a secondary region.</span><span class="sxs-lookup"><span data-stu-id="c4d05-138">There is an expected latency while copying control numbers from a primary region to a secondary region.</span></span> <span data-ttu-id="c4d05-139">To avoid sending duplicate generated control numbers to partners during a disaster event, the recommendation is to increment the control numbers in the secondary region agreements by using [PowerShell cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span><span class="sxs-lookup"><span data-stu-id="c4d05-139">To avoid sending duplicate generated control numbers to partners during a disaster event, the recommendation is to increment the control numbers in the secondary region agreements by using [PowerShell cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span></span>

## <a name="fall-back-to-a-primary-region-post-disaster-event"></a><span data-ttu-id="c4d05-140">Fall back to a primary region post-disaster event</span><span class="sxs-lookup"><span data-stu-id="c4d05-140">Fall back to a primary region post-disaster event</span></span>

<span data-ttu-id="c4d05-141">To fall back to a primary region when it is available, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="c4d05-141">To fall back to a primary region when it is available, follow these steps:</span></span>

1. <span data-ttu-id="c4d05-142">Stop accepting messages from partners in the secondary region.</span><span class="sxs-lookup"><span data-stu-id="c4d05-142">Stop accepting messages from partners in the secondary region.</span></span>  

2. <span data-ttu-id="c4d05-143">Increment the generated control numbers for all the primary region agreements by using [PowerShell cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span><span class="sxs-lookup"><span data-stu-id="c4d05-143">Increment the generated control numbers for all the primary region agreements by using [PowerShell cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span></span>  

3. <span data-ttu-id="c4d05-144">Direct traffic from the secondary region to the primary region.</span><span class="sxs-lookup"><span data-stu-id="c4d05-144">Direct traffic from the secondary region to the primary region.</span></span>

4. <span data-ttu-id="c4d05-145">Check that the logic app created in the secondary region for pulling run status from the primary region is enabled.</span><span class="sxs-lookup"><span data-stu-id="c4d05-145">Check that the logic app created in the secondary region for pulling run status from the primary region is enabled.</span></span>

## <a name="x12"></a><span data-ttu-id="c4d05-146">X12</span><span class="sxs-lookup"><span data-stu-id="c4d05-146">X12</span></span> 

<span data-ttu-id="c4d05-147">Business continuity for EDI X12 documents is based on control numbers:</span><span class="sxs-lookup"><span data-stu-id="c4d05-147">Business continuity for EDI X12 documents is based on control numbers:</span></span>

> [!TIP]
> <span data-ttu-id="c4d05-148">You can also use the [X12 quick start template](https://azure.microsoft.com/resources/templates/201-logic-app-b2b-disaster-recovery-replication/) to create logic apps.</span><span class="sxs-lookup"><span data-stu-id="c4d05-148">You can also use the [X12 quick start template](https://azure.microsoft.com/resources/templates/201-logic-app-b2b-disaster-recovery-replication/) to create logic apps.</span></span> <span data-ttu-id="c4d05-149">Creating primary and secondary integration accounts are prerequisites to use the template.</span><span class="sxs-lookup"><span data-stu-id="c4d05-149">Creating primary and secondary integration accounts are prerequisites to use the template.</span></span> <span data-ttu-id="c4d05-150">The template helps to create two logic apps, one for received control numbers and another for generated control numbers.</span><span class="sxs-lookup"><span data-stu-id="c4d05-150">The template helps to create two logic apps, one for received control numbers and another for generated control numbers.</span></span> <span data-ttu-id="c4d05-151">Respective triggers and actions are created in the logic apps, connecting the trigger to the primary integration account and the action to the secondary integration account.</span><span class="sxs-lookup"><span data-stu-id="c4d05-151">Respective triggers and actions are created in the logic apps, connecting the trigger to the primary integration account and the action to the secondary integration account.</span></span>

<span data-ttu-id="c4d05-152">**Prerequisites**</span><span class="sxs-lookup"><span data-stu-id="c4d05-152">**Prerequisites**</span></span>

<span data-ttu-id="c4d05-153">To enable disaster recovery for inbound messages, select the duplicate check settings in the X12 agreement's Receive Settings.</span><span class="sxs-lookup"><span data-stu-id="c4d05-153">To enable disaster recovery for inbound messages, select the duplicate check settings in the X12 agreement's Receive Settings.</span></span>

![Select duplicate check settings](./media/logic-apps-enterprise-integration-b2b-business-continuity/dupcheck.png)  

1. <span data-ttu-id="c4d05-155">Create a [logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md) in a secondary region.</span><span class="sxs-lookup"><span data-stu-id="c4d05-155">Create a [logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md) in a secondary region.</span></span>    

2. <span data-ttu-id="c4d05-156">Search on **X12**, and select **X12 - When a control number is modified**.</span><span class="sxs-lookup"><span data-stu-id="c4d05-156">Search on **X12**, and select **X12 - When a control number is modified**.</span></span>   

   ![Search for X12](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn1.png)

   <span data-ttu-id="c4d05-158">The trigger prompts you to establish a connection to an integration account.</span><span class="sxs-lookup"><span data-stu-id="c4d05-158">The trigger prompts you to establish a connection to an integration account.</span></span> 
   <span data-ttu-id="c4d05-159">The trigger should be connected to a primary region integration account.</span><span class="sxs-lookup"><span data-stu-id="c4d05-159">The trigger should be connected to a primary region integration account.</span></span>

3. <span data-ttu-id="c4d05-160">Enter a connection name, select your *primary region integration account* from the list, and choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="c4d05-160">Enter a connection name, select your *primary region integration account* from the list, and choose **Create**.</span></span>   

   ![Primary region integration account name](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn2.png)

4. <span data-ttu-id="c4d05-162">The **DateTime to start control number sync** setting is optional.</span><span class="sxs-lookup"><span data-stu-id="c4d05-162">The **DateTime to start control number sync** setting is optional.</span></span> <span data-ttu-id="c4d05-163">The **Frequency** can be set to **Day**, **Hour**, **Minute**, or **Second** with an interval.</span><span class="sxs-lookup"><span data-stu-id="c4d05-163">The **Frequency** can be set to **Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>   

   ![DateTime and Frequency](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

5. <span data-ttu-id="c4d05-165">Select **New step** > **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="c4d05-165">Select **New step** > **Add an action**.</span></span>

   ![New step, Add an action](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

6. <span data-ttu-id="c4d05-167">Search on **X12**, and select **X12 - Add or update control numbers**.</span><span class="sxs-lookup"><span data-stu-id="c4d05-167">Search on **X12**, and select **X12 - Add or update control numbers**.</span></span>   

   ![Add or update control numbers](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn5.png)

7. <span data-ttu-id="c4d05-169">To connect an action to a secondary region integration account, select **Change connection** > **Add new connection** for a list of the available integration accounts.</span><span class="sxs-lookup"><span data-stu-id="c4d05-169">To connect an action to a secondary region integration account, select **Change connection** > **Add new connection** for a list of the available integration accounts.</span></span> <span data-ttu-id="c4d05-170">Enter a connection name, select your *secondary region integration account* from the list, and choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="c4d05-170">Enter a connection name, select your *secondary region integration account* from the list, and choose **Create**.</span></span> 

   ![Secondary region integration account name](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

8. <span data-ttu-id="c4d05-172">Switch to raw inputs by clicking on the icon in upper right corner.</span><span class="sxs-lookup"><span data-stu-id="c4d05-172">Switch to raw inputs by clicking on the icon in upper right corner.</span></span>

   ![Switch to raw inputs](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12rawinputs.png)

9. <span data-ttu-id="c4d05-174">Select Body from the dynamic content picker, and save the logic app.</span><span class="sxs-lookup"><span data-stu-id="c4d05-174">Select Body from the dynamic content picker, and save the logic app.</span></span>

   ![Dynamic content fields](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn7.png)

   <span data-ttu-id="c4d05-176">Based on the time interval, the trigger polls the primary region received control number table and pulls the new records.</span><span class="sxs-lookup"><span data-stu-id="c4d05-176">Based on the time interval, the trigger polls the primary region received control number table and pulls the new records.</span></span> 
   <span data-ttu-id="c4d05-177">The action updates the records in the secondary region integration account.</span><span class="sxs-lookup"><span data-stu-id="c4d05-177">The action updates the records in the secondary region integration account.</span></span> 
   <span data-ttu-id="c4d05-178">If there are no updates, the trigger status appears as **Skipped**.</span><span class="sxs-lookup"><span data-stu-id="c4d05-178">If there are no updates, the trigger status appears as **Skipped**.</span></span>   

   ![Control number table](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

<span data-ttu-id="c4d05-180">Based on the time interval, the incremental runtime status replicates from a primary region to a secondary region.</span><span class="sxs-lookup"><span data-stu-id="c4d05-180">Based on the time interval, the incremental runtime status replicates from a primary region to a secondary region.</span></span> <span data-ttu-id="c4d05-181">During a disaster event, when the primary region is not available, direct traffic to the secondary region for business continuity.</span><span class="sxs-lookup"><span data-stu-id="c4d05-181">During a disaster event, when the primary region is not available, direct traffic to the secondary region for business continuity.</span></span> 

## <a name="edifact"></a><span data-ttu-id="c4d05-182">EDIFACT</span><span class="sxs-lookup"><span data-stu-id="c4d05-182">EDIFACT</span></span> 

<span data-ttu-id="c4d05-183">Business continuity for EDI EDIFACT documents is based on control numbers.</span><span class="sxs-lookup"><span data-stu-id="c4d05-183">Business continuity for EDI EDIFACT documents is based on control numbers.</span></span>

<span data-ttu-id="c4d05-184">**Prerequisites**</span><span class="sxs-lookup"><span data-stu-id="c4d05-184">**Prerequisites**</span></span>

<span data-ttu-id="c4d05-185">To enable disaster recovery for inbound messages, select the duplicate check settings in your EDIFACT agreement's Receive Settings.</span><span class="sxs-lookup"><span data-stu-id="c4d05-185">To enable disaster recovery for inbound messages, select the duplicate check settings in your EDIFACT agreement's Receive Settings.</span></span>

![Select duplicate check settings](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactdupcheck.png)  

1. <span data-ttu-id="c4d05-187">Create a [logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md) in a secondary region.</span><span class="sxs-lookup"><span data-stu-id="c4d05-187">Create a [logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md) in a secondary region.</span></span>    

2. <span data-ttu-id="c4d05-188">Search on **EDIFACT**, and select **EDIFACT - When a control number is modified**.</span><span class="sxs-lookup"><span data-stu-id="c4d05-188">Search on **EDIFACT**, and select **EDIFACT - When a control number is modified**.</span></span>

   ![Search for EDIFACT](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactcn1.png)

   <span data-ttu-id="c4d05-190">The trigger prompts you to establish a connection to an integration account.</span><span class="sxs-lookup"><span data-stu-id="c4d05-190">The trigger prompts you to establish a connection to an integration account.</span></span> 
   <span data-ttu-id="c4d05-191">The trigger should be connected to a primary region integration account.</span><span class="sxs-lookup"><span data-stu-id="c4d05-191">The trigger should be connected to a primary region integration account.</span></span> 

3. <span data-ttu-id="c4d05-192">Enter a connection name, select your *primary region integration account* from the list, and choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="c4d05-192">Enter a connection name, select your *primary region integration account* from the list, and choose **Create**.</span></span>    

   ![Primary region integration account name](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN2.png)

4. <span data-ttu-id="c4d05-194">The **DateTime to start control number sync** setting is optional.</span><span class="sxs-lookup"><span data-stu-id="c4d05-194">The **DateTime to start control number sync** setting is optional.</span></span> <span data-ttu-id="c4d05-195">The **Frequency** can be set to **Day**, **Hour**, **Minute**, or **Second** with an interval.</span><span class="sxs-lookup"><span data-stu-id="c4d05-195">The **Frequency** can be set to **Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>    

   ![DateTime and Frequency](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

6. <span data-ttu-id="c4d05-197">Select **New step** > **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="c4d05-197">Select **New step** > **Add an action**.</span></span>    

   ![New step, Add an action](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

7. <span data-ttu-id="c4d05-199">Search on **EDIFACT**, and select **EDIFACT - Add or update control numbers**.</span><span class="sxs-lookup"><span data-stu-id="c4d05-199">Search on **EDIFACT**, and select **EDIFACT - Add or update control numbers**.</span></span>   

   ![Add or update control numbers](./media/logic-apps-enterprise-integration-b2b-business-continuity/EdifactChooseAction.png)

8. <span data-ttu-id="c4d05-201">To connect an action to a secondary region integration account, select **Change connection** > **Add new connection** for a list of the available integration accounts.</span><span class="sxs-lookup"><span data-stu-id="c4d05-201">To connect an action to a secondary region integration account, select **Change connection** > **Add new connection** for a list of the available integration accounts.</span></span> <span data-ttu-id="c4d05-202">Enter a connection name, select your *secondary region integration account* from the list, and choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="c4d05-202">Enter a connection name, select your *secondary region integration account* from the list, and choose **Create**.</span></span>

   ![Secondary region integration account name](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

9. <span data-ttu-id="c4d05-204">Switch to raw inputs by clicking on the icon in upper right corner.</span><span class="sxs-lookup"><span data-stu-id="c4d05-204">Switch to raw inputs by clicking on the icon in upper right corner.</span></span>

   ![Switch to raw inputs](./media/logic-apps-enterprise-integration-b2b-business-continuity/Edifactrawinputs.png)

10. <span data-ttu-id="c4d05-206">Select Body from the dynamic content picker, and save the logic app.</span><span class="sxs-lookup"><span data-stu-id="c4d05-206">Select Body from the dynamic content picker, and save the logic app.</span></span>   

   ![Dynamic content fields](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN7.png)

   <span data-ttu-id="c4d05-208">Based on the time interval, the trigger polls the primary region received control number table and pulls the new records.</span><span class="sxs-lookup"><span data-stu-id="c4d05-208">Based on the time interval, the trigger polls the primary region received control number table and pulls the new records.</span></span>
   <span data-ttu-id="c4d05-209">The action updates the records to the secondary region integration account.</span><span class="sxs-lookup"><span data-stu-id="c4d05-209">The action updates the records to the secondary region integration account.</span></span> 
   <span data-ttu-id="c4d05-210">If there are no updates, the trigger status appears as **Skipped**.</span><span class="sxs-lookup"><span data-stu-id="c4d05-210">If there are no updates, the trigger status appears as **Skipped**.</span></span>

   ![Control number table](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

<span data-ttu-id="c4d05-212">Based on the time interval, the incremental runtime status replicates from a primary region to a secondary region.</span><span class="sxs-lookup"><span data-stu-id="c4d05-212">Based on the time interval, the incremental runtime status replicates from a primary region to a secondary region.</span></span> <span data-ttu-id="c4d05-213">During a disaster event, when the primary region is not available, direct traffic to the secondary region for business continuity.</span><span class="sxs-lookup"><span data-stu-id="c4d05-213">During a disaster event, when the primary region is not available, direct traffic to the secondary region for business continuity.</span></span> 

## <a name="as2"></a><span data-ttu-id="c4d05-214">AS2</span><span class="sxs-lookup"><span data-stu-id="c4d05-214">AS2</span></span> 

<span data-ttu-id="c4d05-215">Business continuity for documents that use the AS2 protocol is based on the message ID and the MIC value.</span><span class="sxs-lookup"><span data-stu-id="c4d05-215">Business continuity for documents that use the AS2 protocol is based on the message ID and the MIC value.</span></span>

> [!TIP]
> <span data-ttu-id="c4d05-216">You can also use the [AS2 quick start template](https://github.com/Azure/azure-quickstart-templates/pull/3302) to create logic apps.</span><span class="sxs-lookup"><span data-stu-id="c4d05-216">You can also use the [AS2 quick start template](https://github.com/Azure/azure-quickstart-templates/pull/3302) to create logic apps.</span></span> <span data-ttu-id="c4d05-217">Creating primary and secondary integration accounts are prerequisites to use the template.</span><span class="sxs-lookup"><span data-stu-id="c4d05-217">Creating primary and secondary integration accounts are prerequisites to use the template.</span></span> <span data-ttu-id="c4d05-218">The template helps create a logic app that has a trigger and an action.</span><span class="sxs-lookup"><span data-stu-id="c4d05-218">The template helps create a logic app that has a trigger and an action.</span></span> <span data-ttu-id="c4d05-219">The logic app creates a connection from a trigger to a primary integration account and an action to a secondary integration account.</span><span class="sxs-lookup"><span data-stu-id="c4d05-219">The logic app creates a connection from a trigger to a primary integration account and an action to a secondary integration account.</span></span>

1. <span data-ttu-id="c4d05-220">Create a [logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md) in the secondary region.</span><span class="sxs-lookup"><span data-stu-id="c4d05-220">Create a [logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md) in the secondary region.</span></span>  

2. <span data-ttu-id="c4d05-221">Search on **AS2**, and select **AS2 - When a MIC value is created**.</span><span class="sxs-lookup"><span data-stu-id="c4d05-221">Search on **AS2**, and select **AS2 - When a MIC value is created**.</span></span>   

   ![Search for AS2](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid1.png)

   <span data-ttu-id="c4d05-223">A trigger prompts you to establish a connection to an integration account.</span><span class="sxs-lookup"><span data-stu-id="c4d05-223">A trigger prompts you to establish a connection to an integration account.</span></span> 
   <span data-ttu-id="c4d05-224">The trigger should be connected to a primary region integration account.</span><span class="sxs-lookup"><span data-stu-id="c4d05-224">The trigger should be connected to a primary region integration account.</span></span> 
   
3. <span data-ttu-id="c4d05-225">Enter a connection name, select your *primary region integration account* from the list, and choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="c4d05-225">Enter a connection name, select your *primary region integration account* from the list, and choose **Create**.</span></span>

   ![Primary region integration account name](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid2.png)

4. <span data-ttu-id="c4d05-227">The **DateTime to start MIC value sync** setting is optional.</span><span class="sxs-lookup"><span data-stu-id="c4d05-227">The **DateTime to start MIC value sync** setting is optional.</span></span> <span data-ttu-id="c4d05-228">The **Frequency** can be set to **Day**, **Hour**, **Minute**, or **Second** with an interval.</span><span class="sxs-lookup"><span data-stu-id="c4d05-228">The **Frequency** can be set to **Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>   

   ![DateTime and Frequency](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid3.png)

5. <span data-ttu-id="c4d05-230">Select **New step** > **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="c4d05-230">Select **New step** > **Add an action**.</span></span>  

   ![New step, Add an action](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid4.png)

6. <span data-ttu-id="c4d05-232">Search on **AS2**, and select **AS2 - Add or update MIC contents**.</span><span class="sxs-lookup"><span data-stu-id="c4d05-232">Search on **AS2**, and select **AS2 - Add or update MIC contents**.</span></span>  

   ![MIC addition or update](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid5.png)

7. <span data-ttu-id="c4d05-234">To connect an action to a secondary integration account, select **Change connection** > **Add new connection** for a list of the available integration accounts.</span><span class="sxs-lookup"><span data-stu-id="c4d05-234">To connect an action to a secondary integration account, select **Change connection** > **Add new connection** for a list of the available integration accounts.</span></span> <span data-ttu-id="c4d05-235">Enter a connection name, select your *secondary region integration account* from the list, and choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="c4d05-235">Enter a connection name, select your *secondary region integration account* from the list, and choose **Create**.</span></span>

   ![Secondary region integration account name](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid6.png)

8. <span data-ttu-id="c4d05-237">Switch to raw inputs by clicking on the icon in upper right corner.</span><span class="sxs-lookup"><span data-stu-id="c4d05-237">Switch to raw inputs by clicking on the icon in upper right corner.</span></span>

   ![Switch to raw inputs](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2rawinputs.png)

9. <span data-ttu-id="c4d05-239">Select Body from the dynamic content picker, and save the logic app.</span><span class="sxs-lookup"><span data-stu-id="c4d05-239">Select Body from the dynamic content picker, and save the logic app.</span></span>   

   ![Dynamic content](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid7.png)

   <span data-ttu-id="c4d05-241">Based on the time interval, the trigger polls the primary region table and pulls the new records.</span><span class="sxs-lookup"><span data-stu-id="c4d05-241">Based on the time interval, the trigger polls the primary region table and pulls the new records.</span></span> <span data-ttu-id="c4d05-242">The action updates them to the secondary region integration account.</span><span class="sxs-lookup"><span data-stu-id="c4d05-242">The action updates them to the secondary region integration account.</span></span> 
   <span data-ttu-id="c4d05-243">If there are no updates, the trigger status appears as **Skipped**.</span><span class="sxs-lookup"><span data-stu-id="c4d05-243">If there are no updates, the trigger status appears as **Skipped**.</span></span>  

   ![Primary region table](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid8.png)

<span data-ttu-id="c4d05-245">Based on the time interval, the incremental runtime status replicates from the primary region to the secondary region.</span><span class="sxs-lookup"><span data-stu-id="c4d05-245">Based on the time interval, the incremental runtime status replicates from the primary region to the secondary region.</span></span> <span data-ttu-id="c4d05-246">During a disaster event, when the primary region is not available, direct traffic to the secondary region for business continuity.</span><span class="sxs-lookup"><span data-stu-id="c4d05-246">During a disaster event, when the primary region is not available, direct traffic to the secondary region for business continuity.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c4d05-247">Next steps</span><span class="sxs-lookup"><span data-stu-id="c4d05-247">Next steps</span></span>

[<span data-ttu-id="c4d05-248">Monitor B2B messages</span><span class="sxs-lookup"><span data-stu-id="c4d05-248">Monitor B2B messages</span></span>](logic-apps-monitor-b2b-message.md)

