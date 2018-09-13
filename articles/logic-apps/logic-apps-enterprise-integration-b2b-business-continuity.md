---
title: Logic Apps B2B Integration Account Disaster Recovery - Azure Logic Apps | Microsoft Docs
description: Azure Logic Apps B2B Disaster Recovery
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: ''
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: padmavc
ms.openlocfilehash: e48b79eca23bc8e7440fd70bc651c22f58ea520b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660853"
---
# <a name="logic-apps-b2b-cross-region-disaster-recovery"></a><span data-ttu-id="2c434-103">Logic Apps B2B cross region disaster recovery</span><span class="sxs-lookup"><span data-stu-id="2c434-103">Logic Apps B2B cross region disaster recovery</span></span>
<span data-ttu-id="2c434-104">B2B workloads involve money transactions like orders, invoices.</span><span class="sxs-lookup"><span data-stu-id="2c434-104">B2B workloads involve money transactions like orders, invoices.</span></span>  <span data-ttu-id="2c434-105">For business, it is critical to quickly recover to meet business level SLAs as agreed with their partners during a disaster event.</span><span class="sxs-lookup"><span data-stu-id="2c434-105">For business, it is critical to quickly recover to meet business level SLAs as agreed with their partners during a disaster event.</span></span>  <span data-ttu-id="2c434-106">This topic demonstrates building a business continuity plan for B2B workloads.</span><span class="sxs-lookup"><span data-stu-id="2c434-106">This topic demonstrates building a business continuity plan for B2B workloads.</span></span>  <span data-ttu-id="2c434-107">It covers</span><span class="sxs-lookup"><span data-stu-id="2c434-107">It covers</span></span>

* <span data-ttu-id="2c434-108">Create an integration account in secondary region</span><span class="sxs-lookup"><span data-stu-id="2c434-108">Create an integration account in secondary region</span></span>
* <span data-ttu-id="2c434-109">Establish a connection from primary region to secondary region</span><span class="sxs-lookup"><span data-stu-id="2c434-109">Establish a connection from primary region to secondary region</span></span> 
* <span data-ttu-id="2c434-110">Fail over to secondary region during a disaster event</span><span class="sxs-lookup"><span data-stu-id="2c434-110">Fail over to secondary region during a disaster event</span></span>
* <span data-ttu-id="2c434-111">Fall back to primary region post-disaster event</span><span class="sxs-lookup"><span data-stu-id="2c434-111">Fall back to primary region post-disaster event</span></span>

## <a name="create-an-integration-account-in-secondary-region"></a><span data-ttu-id="2c434-112">Create an integration account in secondary region</span><span class="sxs-lookup"><span data-stu-id="2c434-112">Create an integration account in secondary region</span></span>
1. <span data-ttu-id="2c434-113">Select a secondary region and create an [integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).</span><span class="sxs-lookup"><span data-stu-id="2c434-113">Select a secondary region and create an [integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).</span></span>  

2. <span data-ttu-id="2c434-114">Add partners, schemas, and agreements for the required message flows where the run status needs to be replicated to secondary region integration account.</span><span class="sxs-lookup"><span data-stu-id="2c434-114">Add partners, schemas, and agreements for the required message flows where the run status needs to be replicated to secondary region integration account.</span></span>

    > [!Tip]
    > <span data-ttu-id="2c434-115">Make sure consistency in integration account artifacts naming convention across regions</span><span class="sxs-lookup"><span data-stu-id="2c434-115">Make sure consistency in integration account artifacts naming convention across regions</span></span> 
    > 
    > 

3. <span data-ttu-id="2c434-116">The recommendation is to deploy all primary region resources (for example SQL Azure or DocumentDB databases, or Service Bus / Event Hubs used for messaging, APIM, Logic Apps) in the secondary region as well.</span><span class="sxs-lookup"><span data-stu-id="2c434-116">The recommendation is to deploy all primary region resources (for example SQL Azure or DocumentDB databases, or Service Bus / Event Hubs used for messaging, APIM, Logic Apps) in the secondary region as well.</span></span>  

## <a name="establish-a-connection-from-primary-to-secondary"></a><span data-ttu-id="2c434-117">Establish a connection from primary to secondary</span><span class="sxs-lookup"><span data-stu-id="2c434-117">Establish a connection from primary to secondary</span></span> 
<span data-ttu-id="2c434-118">To pull the run status from the primary region, create a Logic App in the secondary region.</span><span class="sxs-lookup"><span data-stu-id="2c434-118">To pull the run status from the primary region, create a Logic App in the secondary region.</span></span>  <span data-ttu-id="2c434-119">It should have a **trigger** and an **action**.</span><span class="sxs-lookup"><span data-stu-id="2c434-119">It should have a **trigger** and an **action**.</span></span>  <span data-ttu-id="2c434-120">The trigger should connect to primary region integration account and the action should connect to secondary region integration account.</span><span class="sxs-lookup"><span data-stu-id="2c434-120">The trigger should connect to primary region integration account and the action should connect to secondary region integration account.</span></span>  <span data-ttu-id="2c434-121">Based on the time interval, the trigger polls the primary region run status table pulls the new records if any and action updates them to secondary region integration account.</span><span class="sxs-lookup"><span data-stu-id="2c434-121">Based on the time interval, the trigger polls the primary region run status table pulls the new records if any and action updates them to secondary region integration account.</span></span> <span data-ttu-id="2c434-122">This helps to get incremental runtime status from primary region to secondary region.</span><span class="sxs-lookup"><span data-stu-id="2c434-122">This helps to get incremental runtime status from primary region to secondary region.</span></span>

<span data-ttu-id="2c434-123">Business continuity in Logic Apps integration account is designed to support based on B2B protocols - X12, AS2, and EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="2c434-123">Business continuity in Logic Apps integration account is designed to support based on B2B protocols - X12, AS2, and EDIFACT.</span></span>  <span data-ttu-id="2c434-124">To find detailed steps, select respective links.</span><span class="sxs-lookup"><span data-stu-id="2c434-124">To find detailed steps, select respective links.</span></span>

* [<span data-ttu-id="2c434-125">X12</span><span class="sxs-lookup"><span data-stu-id="2c434-125">X12</span></span>](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12)
* [<span data-ttu-id="2c434-126">AS2</span><span class="sxs-lookup"><span data-stu-id="2c434-126">AS2</span></span>](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2)
* <span data-ttu-id="2c434-127">EDIFACT (coming soon)</span><span class="sxs-lookup"><span data-stu-id="2c434-127">EDIFACT (coming soon)</span></span>

## <a name="fail-over-to-secondary-region-during-a-disaster-event"></a><span data-ttu-id="2c434-128">Fail over to secondary region during a disaster event</span><span class="sxs-lookup"><span data-stu-id="2c434-128">Fail over to secondary region during a disaster event</span></span>
<span data-ttu-id="2c434-129">During a disaster event, when the primary region is not available for business continuity, direct traffic to the secondary region.</span><span class="sxs-lookup"><span data-stu-id="2c434-129">During a disaster event, when the primary region is not available for business continuity, direct traffic to the secondary region.</span></span> <span data-ttu-id="2c434-130">Secondary region helps recover business functions quickly to meet recovery time/point objectives (RPO/RTO) as agreed with their partners.</span><span class="sxs-lookup"><span data-stu-id="2c434-130">Secondary region helps recover business functions quickly to meet recovery time/point objectives (RPO/RTO) as agreed with their partners.</span></span>  <span data-ttu-id="2c434-131">Also, minimizes efforts to fail over from one region to another region.</span><span class="sxs-lookup"><span data-stu-id="2c434-131">Also, minimizes efforts to fail over from one region to another region.</span></span> 

<span data-ttu-id="2c434-132">There is an expected latency while copying control numbers from primary to secondary region.</span><span class="sxs-lookup"><span data-stu-id="2c434-132">There is an expected latency while copying control numbers from primary to secondary region.</span></span>  <span data-ttu-id="2c434-133">To avoid sending duplicate generated control numbers to partners during a disaster event, it is recommended to bump up control numbers in the **secondary region agreements** using [PowerShell cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span><span class="sxs-lookup"><span data-stu-id="2c434-133">To avoid sending duplicate generated control numbers to partners during a disaster event, it is recommended to bump up control numbers in the **secondary region agreements** using [PowerShell cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span></span>

## <a name="fall-back-to-primary-region-post-disaster-event"></a><span data-ttu-id="2c434-134">Fall back to primary region post-disaster event</span><span class="sxs-lookup"><span data-stu-id="2c434-134">Fall back to primary region post-disaster event</span></span>
<span data-ttu-id="2c434-135">When primary region is available, to fall back to primary region follow below steps</span><span class="sxs-lookup"><span data-stu-id="2c434-135">When primary region is available, to fall back to primary region follow below steps</span></span>     
* <span data-ttu-id="2c434-136">Stop accepting messages from partners in the **secondary region**</span><span class="sxs-lookup"><span data-stu-id="2c434-136">Stop accepting messages from partners in the **secondary region**</span></span>   
* <span data-ttu-id="2c434-137">Bump up generated control numbers for all the **primary region agreements** using [PowerShell cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery)</span><span class="sxs-lookup"><span data-stu-id="2c434-137">Bump up generated control numbers for all the **primary region agreements** using [PowerShell cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery)</span></span>   
* <span data-ttu-id="2c434-138">Direct traffic from secondary to primary region</span><span class="sxs-lookup"><span data-stu-id="2c434-138">Direct traffic from secondary to primary region</span></span>   
* <span data-ttu-id="2c434-139">Check the Logic App created in the secondary region to pull run status from the primary is enabled</span><span class="sxs-lookup"><span data-stu-id="2c434-139">Check the Logic App created in the secondary region to pull run status from the primary is enabled</span></span>    

## <a name="x12"></a><span data-ttu-id="2c434-140">X12</span><span class="sxs-lookup"><span data-stu-id="2c434-140">X12</span></span> 
<span data-ttu-id="2c434-141">Business continuity for EDI X12 documents is designed based on control numbers</span><span class="sxs-lookup"><span data-stu-id="2c434-141">Business continuity for EDI X12 documents is designed based on control numbers</span></span>   
* <span data-ttu-id="2c434-142">Control numbers received (Inbound messages) from partners</span><span class="sxs-lookup"><span data-stu-id="2c434-142">Control numbers received (Inbound messages) from partners</span></span>  
* <span data-ttu-id="2c434-143">Control numbers generated (outbound messages) and send to partners</span><span class="sxs-lookup"><span data-stu-id="2c434-143">Control numbers generated (outbound messages) and send to partners</span></span>  
    
    > [!Tip]
    > <span data-ttu-id="2c434-144">You can also use [X12 quick start template](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/) to create Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="2c434-144">You can also use [X12 quick start template](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/) to create Logic Apps.</span></span>  <span data-ttu-id="2c434-145">Creating primary and secondary integration accounts are prerequisites to use the template.</span><span class="sxs-lookup"><span data-stu-id="2c434-145">Creating primary and secondary integration accounts are prerequisites to use the template.</span></span>  <span data-ttu-id="2c434-146">The template helps create 2 Logic Apps, one for received control number and another for generated control number.</span><span class="sxs-lookup"><span data-stu-id="2c434-146">The template helps create 2 Logic Apps, one for received control number and another for generated control number.</span></span>  <span data-ttu-id="2c434-147">Respective triggers and actions are created in the Logic Apps, connects the trigger to primary integration account and action to secondary integration account.</span><span class="sxs-lookup"><span data-stu-id="2c434-147">Respective triggers and actions are created in the Logic Apps, connects the trigger to primary integration account and action to secondary integration account.</span></span>
    > 
    >

### <a name="control-numbers-received-from-the-partners"></a><span data-ttu-id="2c434-148">Control numbers received from the partners</span><span class="sxs-lookup"><span data-stu-id="2c434-148">Control numbers received from the partners</span></span>
1. <span data-ttu-id="2c434-149">Create a [Logic App](../logic-apps/logic-apps-create-a-logic-app.md) in the secondary region</span><span class="sxs-lookup"><span data-stu-id="2c434-149">Create a [Logic App](../logic-apps/logic-apps-create-a-logic-app.md) in the secondary region</span></span>   

2. <span data-ttu-id="2c434-150">Search **X12** and select **X12 - When a received control number is modified**  </span><span class="sxs-lookup"><span data-stu-id="2c434-150">Search **X12** and select **X12 - When a received control number is modified**  </span></span>  
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/X12recevicedCN1.png)

3. <span data-ttu-id="2c434-151">Selecting the trigger prompts to establish a connection to integration account.</span><span class="sxs-lookup"><span data-stu-id="2c434-151">Selecting the trigger prompts to establish a connection to integration account.</span></span> <span data-ttu-id="2c434-152">Trigger to be connected to primary region integration account.</span><span class="sxs-lookup"><span data-stu-id="2c434-152">Trigger to be connected to primary region integration account.</span></span>  <span data-ttu-id="2c434-153">Give a connection name, select your **primary region integration account** from the list and click create.</span><span class="sxs-lookup"><span data-stu-id="2c434-153">Give a connection name, select your **primary region integration account** from the list and click create.</span></span>   
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/X12recevicedCN2.png)

4. <span data-ttu-id="2c434-154">DateTime to start control number sync is optional.</span><span class="sxs-lookup"><span data-stu-id="2c434-154">DateTime to start control number sync is optional.</span></span>  <span data-ttu-id="2c434-155">Frequency can be set to **Day**, **Hour**, **Minute**, or **Second** with an interval.</span><span class="sxs-lookup"><span data-stu-id="2c434-155">Frequency can be set to **Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>    
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/X12recevicedCN3.png)

5. <span data-ttu-id="2c434-156">Click **New step** and **Add an action**  </span><span class="sxs-lookup"><span data-stu-id="2c434-156">Click **New step** and **Add an action**  </span></span>  
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/X12recevicedCN4.png)

6. <span data-ttu-id="2c434-157">Search **X12** and select **X12 - Add or update a received control number** </span><span class="sxs-lookup"><span data-stu-id="2c434-157">Search **X12** and select **X12 - Add or update a received control number** </span></span>  
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/X12recevicedCN5.png)

7. <span data-ttu-id="2c434-158">Action to be connected to secondary integration account.</span><span class="sxs-lookup"><span data-stu-id="2c434-158">Action to be connected to secondary integration account.</span></span>  <span data-ttu-id="2c434-159">Select **Change connection** and **Add new connection** lists the available integration accounts.</span><span class="sxs-lookup"><span data-stu-id="2c434-159">Select **Change connection** and **Add new connection** lists the available integration accounts.</span></span>  <span data-ttu-id="2c434-160">Give a connection name, select your **secondary region integration account** from the list and click create.</span><span class="sxs-lookup"><span data-stu-id="2c434-160">Give a connection name, select your **secondary region integration account** from the list and click create.</span></span>     
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/X12recevicedCN6.png)

8. <span data-ttu-id="2c434-161">Select the dynamic content and save the logic app</span><span class="sxs-lookup"><span data-stu-id="2c434-161">Select the dynamic content and save the logic app</span></span>   
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/X12recevicedCN7.png)

9. <span data-ttu-id="2c434-162">Based on the time interval, the trigger polls the primary region received control number table, pulls the new records, and actions updates them to secondary region integration account.</span><span class="sxs-lookup"><span data-stu-id="2c434-162">Based on the time interval, the trigger polls the primary region received control number table, pulls the new records, and actions updates them to secondary region integration account.</span></span>  <span data-ttu-id="2c434-163">If they are no updates, the trigger status shows as skipped.</span><span class="sxs-lookup"><span data-stu-id="2c434-163">If they are no updates, the trigger status shows as skipped.</span></span>
    
    > [!Tip]
    > <span data-ttu-id="2c434-164">Enabling duplicate check on the agreement receive settings keeps received control numbers runtime state and helps fire the triggers at regular intervals</span><span class="sxs-lookup"><span data-stu-id="2c434-164">Enabling duplicate check on the agreement receive settings keeps received control numbers runtime state and helps fire the triggers at regular intervals</span></span>
    > 
    >

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/X12recevicedCN8.png)


### <a name="control-numbers-generated-and-send-to-the-partners"></a><span data-ttu-id="2c434-165">Control numbers generated and send to the partners</span><span class="sxs-lookup"><span data-stu-id="2c434-165">Control numbers generated and send to the partners</span></span>
1. <span data-ttu-id="2c434-166">Create a [Logic App](../logic-apps/logic-apps-create-a-logic-app.md) in the secondary region</span><span class="sxs-lookup"><span data-stu-id="2c434-166">Create a [Logic App](../logic-apps/logic-apps-create-a-logic-app.md) in the secondary region</span></span>  

2. <span data-ttu-id="2c434-167">Search **X12** and select **X12 - When a generated control number is modified** </span><span class="sxs-lookup"><span data-stu-id="2c434-167">Search **X12** and select **X12 - When a generated control number is modified** </span></span>  
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/X12generatedCN1.png)

3. <span data-ttu-id="2c434-168">Selecting the trigger prompts to establish a connection to integration account.</span><span class="sxs-lookup"><span data-stu-id="2c434-168">Selecting the trigger prompts to establish a connection to integration account.</span></span> <span data-ttu-id="2c434-169">Trigger to be connected to primary region integration account.</span><span class="sxs-lookup"><span data-stu-id="2c434-169">Trigger to be connected to primary region integration account.</span></span>  <span data-ttu-id="2c434-170">Give a connection name, select your **primary region integration account** from the list and click create.</span><span class="sxs-lookup"><span data-stu-id="2c434-170">Give a connection name, select your **primary region integration account** from the list and click create.</span></span>   
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/X12generatedCN2.png) 

4. <span data-ttu-id="2c434-171">DateTime to start control number sync is optional.</span><span class="sxs-lookup"><span data-stu-id="2c434-171">DateTime to start control number sync is optional.</span></span>  <span data-ttu-id="2c434-172">Frequency can be set to **Day**, **Hour**, **Minute**, or **Second** with an interval.</span><span class="sxs-lookup"><span data-stu-id="2c434-172">Frequency can be set to **Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>   
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/X12generatedCN3.png)  

5. <span data-ttu-id="2c434-173">Click **New step** and **Add an action** </span><span class="sxs-lookup"><span data-stu-id="2c434-173">Click **New step** and **Add an action** </span></span>  
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/X12generatedCN4.png)

6. <span data-ttu-id="2c434-174">Search **X12** and select **X12 - Add or update a generated control number** </span><span class="sxs-lookup"><span data-stu-id="2c434-174">Search **X12** and select **X12 - Add or update a generated control number** </span></span>  
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/X12generatedCN5.png)

7. <span data-ttu-id="2c434-175">Action to be connected to secondary integration account.</span><span class="sxs-lookup"><span data-stu-id="2c434-175">Action to be connected to secondary integration account.</span></span>  <span data-ttu-id="2c434-176">Select **Change connection** and **Add new connection** lists the available integration accounts.</span><span class="sxs-lookup"><span data-stu-id="2c434-176">Select **Change connection** and **Add new connection** lists the available integration accounts.</span></span>  <span data-ttu-id="2c434-177">Give a connection name, select your **secondary region integration account** from the list and click create.</span><span class="sxs-lookup"><span data-stu-id="2c434-177">Give a connection name, select your **secondary region integration account** from the list and click create.</span></span>    
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/X12generatedCN6.png)

8. <span data-ttu-id="2c434-178">Select the dynamic content and save the logic app</span><span class="sxs-lookup"><span data-stu-id="2c434-178">Select the dynamic content and save the logic app</span></span>   
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/X12generatedCN7.png)

9. <span data-ttu-id="2c434-179">Based on the time interval, the trigger polls the primary region received control number table, pulls the new records, and actions updates them to secondary region integration account.</span><span class="sxs-lookup"><span data-stu-id="2c434-179">Based on the time interval, the trigger polls the primary region received control number table, pulls the new records, and actions updates them to secondary region integration account.</span></span>  <span data-ttu-id="2c434-180">If they are no updates, the trigger status shows as skipped.</span><span class="sxs-lookup"><span data-stu-id="2c434-180">If they are no updates, the trigger status shows as skipped.</span></span>  
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/X12generatedCN8.png)

<span data-ttu-id="2c434-181">Based on the time interval, the incremental runtime status replicates from primary region to secondary region.</span><span class="sxs-lookup"><span data-stu-id="2c434-181">Based on the time interval, the incremental runtime status replicates from primary region to secondary region.</span></span>  <span data-ttu-id="2c434-182">During a disaster event, when the primary region is not available, direct traffic to the secondary region for business continuity.</span><span class="sxs-lookup"><span data-stu-id="2c434-182">During a disaster event, when the primary region is not available, direct traffic to the secondary region for business continuity.</span></span> 

## <a name="as2"></a><span data-ttu-id="2c434-183">AS2</span><span class="sxs-lookup"><span data-stu-id="2c434-183">AS2</span></span> 
<span data-ttu-id="2c434-184">Business continuity for documents that use AS2 protocol is designed based on message id and MIC value</span><span class="sxs-lookup"><span data-stu-id="2c434-184">Business continuity for documents that use AS2 protocol is designed based on message id and MIC value</span></span>

> [!Tip]
    > <span data-ttu-id="2c434-185">You can also use [AS2 quick start template](https://github.com/Azure/azure-quickstart-templates/pull/3302) to create Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="2c434-185">You can also use [AS2 quick start template](https://github.com/Azure/azure-quickstart-templates/pull/3302) to create Logic Apps.</span></span>  <span data-ttu-id="2c434-186">Creating primary and secondary integration accounts are prerequisites to use the template.</span><span class="sxs-lookup"><span data-stu-id="2c434-186">Creating primary and secondary integration accounts are prerequisites to use the template.</span></span>  <span data-ttu-id="2c434-187">The template helps create a Logic App, having a trigger and an action.</span><span class="sxs-lookup"><span data-stu-id="2c434-187">The template helps create a Logic App, having a trigger and an action.</span></span>  <span data-ttu-id="2c434-188">Creates a connection from trigger to primary integration account and action to secondary integration account.</span><span class="sxs-lookup"><span data-stu-id="2c434-188">Creates a connection from trigger to primary integration account and action to secondary integration account.</span></span>
    > 
    >

1. <span data-ttu-id="2c434-189">Create a [Logic App](../logic-apps/logic-apps-create-a-logic-app.md) in the secondary region</span><span class="sxs-lookup"><span data-stu-id="2c434-189">Create a [Logic App](../logic-apps/logic-apps-create-a-logic-app.md) in the secondary region</span></span>  

2. <span data-ttu-id="2c434-190">Search **AS2** and select **AS2 - When a MIC value is created** </span><span class="sxs-lookup"><span data-stu-id="2c434-190">Search **AS2** and select **AS2 - When a MIC value is created** </span></span>  
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/AS2messageid1.png)

3. <span data-ttu-id="2c434-191">Selecting the trigger prompts to establish a connection to integration account.</span><span class="sxs-lookup"><span data-stu-id="2c434-191">Selecting the trigger prompts to establish a connection to integration account.</span></span> <span data-ttu-id="2c434-192">Trigger to be connected to primary region integration account.</span><span class="sxs-lookup"><span data-stu-id="2c434-192">Trigger to be connected to primary region integration account.</span></span>  <span data-ttu-id="2c434-193">Give a connection name, select your **primary region integration account** from the list and click create.</span><span class="sxs-lookup"><span data-stu-id="2c434-193">Give a connection name, select your **primary region integration account** from the list and click create.</span></span>   
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/AS2messageid2.png)

4. <span data-ttu-id="2c434-194">DateTime to start MIC value sync is optional.</span><span class="sxs-lookup"><span data-stu-id="2c434-194">DateTime to start MIC value sync is optional.</span></span>  <span data-ttu-id="2c434-195">Frequency can be set to **Day**, **Hour**, **Minute**, or **Second** with an interval.</span><span class="sxs-lookup"><span data-stu-id="2c434-195">Frequency can be set to **Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>   
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/AS2messageid3.png)

5. <span data-ttu-id="2c434-196">Click **New step** and **Add an action** </span><span class="sxs-lookup"><span data-stu-id="2c434-196">Click **New step** and **Add an action** </span></span>  
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/AS2messageid4.png)

6. <span data-ttu-id="2c434-197">Search **AS2** and select **AS2 - Add or update a MIC** </span><span class="sxs-lookup"><span data-stu-id="2c434-197">Search **AS2** and select **AS2 - Add or update a MIC** </span></span>  
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/AS2messageid5.png)

7. <span data-ttu-id="2c434-198">Action to be connected to secondary integration account.</span><span class="sxs-lookup"><span data-stu-id="2c434-198">Action to be connected to secondary integration account.</span></span>  <span data-ttu-id="2c434-199">Select **Change connection** and **Add new connection** lists the available integration accounts.</span><span class="sxs-lookup"><span data-stu-id="2c434-199">Select **Change connection** and **Add new connection** lists the available integration accounts.</span></span>  <span data-ttu-id="2c434-200">Give a connection name, select your **secondary region integration account** from the list and click create.</span><span class="sxs-lookup"><span data-stu-id="2c434-200">Give a connection name, select your **secondary region integration account** from the list and click create.</span></span>    
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/AS2messageid6.png)

8. <span data-ttu-id="2c434-201">Select the dynamic content and save the logic app</span><span class="sxs-lookup"><span data-stu-id="2c434-201">Select the dynamic content and save the logic app</span></span>   
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/AS2messageid7.png)

9. <span data-ttu-id="2c434-202">Based on the time interval, the trigger polls the primary region table, pulls the new records, and actions updates them to secondary region integration account.</span><span class="sxs-lookup"><span data-stu-id="2c434-202">Based on the time interval, the trigger polls the primary region table, pulls the new records, and actions updates them to secondary region integration account.</span></span>  <span data-ttu-id="2c434-203">If they are no updates, the trigger status shows as skipped.</span><span class="sxs-lookup"><span data-stu-id="2c434-203">If they are no updates, the trigger status shows as skipped.</span></span>  
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/AS2messageid8.png)

<span data-ttu-id="2c434-204">Based on the time interval, the incremental runtime status replicates from primary region to secondary region.</span><span class="sxs-lookup"><span data-stu-id="2c434-204">Based on the time interval, the incremental runtime status replicates from primary region to secondary region.</span></span>  <span data-ttu-id="2c434-205">During a disaster event, when the primary region is not available, direct traffic to the secondary region for business continuity.</span><span class="sxs-lookup"><span data-stu-id="2c434-205">During a disaster event, when the primary region is not available, direct traffic to the secondary region for business continuity.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="2c434-206">Next Steps</span><span class="sxs-lookup"><span data-stu-id="2c434-206">Next Steps</span></span>
* <span data-ttu-id="2c434-207">Learn more about [monitoring B2B messages](logic-apps-monitor-b2b-message.md).</span><span class="sxs-lookup"><span data-stu-id="2c434-207">Learn more about [monitoring B2B messages](logic-apps-monitor-b2b-message.md).</span></span>   























