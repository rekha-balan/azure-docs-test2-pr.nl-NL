---
title: Track AS2, X12, EDIFACT messages using a query - Azure logic apps  | Microsoft Docs
description: Use queries to track business-to-business messages in the Operations Management Suite portal
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
ms.date: 01/27/2017
ms.author: padmavc
ms.openlocfilehash: a4c6ea3f43ba7ed2d4b3b0104b3ec7dd43b8b0fe
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670354"
---
# <a name="track-b2b-messages-in-the-operations-management-suite-portal-by-using-a-query"></a><span data-ttu-id="80091-103">Track B2B messages in the Operations Management Suite portal by using a query</span><span class="sxs-lookup"><span data-stu-id="80091-103">Track B2B messages in the Operations Management Suite portal by using a query</span></span>
<span data-ttu-id="80091-104">To track business-to-business (B2B) messages in the Operations Management Suite portal, you can create a query that filters data for a specific interchange control number.</span><span class="sxs-lookup"><span data-stu-id="80091-104">To track business-to-business (B2B) messages in the Operations Management Suite portal, you can create a query that filters data for a specific interchange control number.</span></span>

## <a name="prereqs"></a><span data-ttu-id="80091-105">Prereqs</span><span class="sxs-lookup"><span data-stu-id="80091-105">Prereqs</span></span>

<span data-ttu-id="80091-106">For debugging and for more detailed diagnostics information, turn on diagnostics in your [integration account](logic-apps-monitor-b2b-message.md) for your [logic apps](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics-and-alerts) that have X12 connectors.</span><span class="sxs-lookup"><span data-stu-id="80091-106">For debugging and for more detailed diagnostics information, turn on diagnostics in your [integration account](logic-apps-monitor-b2b-message.md) for your [logic apps](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics-and-alerts) that have X12 connectors.</span></span> <span data-ttu-id="80091-107">Then, do the steps to [publish diagnostic data](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) to the Operations Management Suite portal.</span><span class="sxs-lookup"><span data-stu-id="80091-107">Then, do the steps to [publish diagnostic data](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) to the Operations Management Suite portal.</span></span>

## <a name="search-for-an-interchange-control-number"></a><span data-ttu-id="80091-108">Search for an interchange control number</span><span class="sxs-lookup"><span data-stu-id="80091-108">Search for an interchange control number</span></span>

1. <span data-ttu-id="80091-109">On the start page, select **Log Search**.</span><span class="sxs-lookup"><span data-stu-id="80091-109">On the start page, select **Log Search**.</span></span>  
<span data-ttu-id="80091-110">![Select log search](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)</span><span class="sxs-lookup"><span data-stu-id="80091-110">![Select log search](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)</span></span>

2. <span data-ttu-id="80091-111">In the search box, type **Type="AzureDiagnostics"**.</span><span class="sxs-lookup"><span data-stu-id="80091-111">In the search box, type **Type="AzureDiagnostics"**.</span></span> <span data-ttu-id="80091-112">To filter data, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="80091-112">To filter data, select **Add**.</span></span>  
<span data-ttu-id="80091-113">![Select query](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query1.png)</span><span class="sxs-lookup"><span data-stu-id="80091-113">![Select query](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query1.png)</span></span>

3. <span data-ttu-id="80091-114">Type **interchange**, select **event_record_messageProperties_interchangeControlNumber_s**, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="80091-114">Type **interchange**, select **event_record_messageProperties_interchangeControlNumber_s**, and then select **Add**.</span></span>  
<span data-ttu-id="80091-115">![Add filter](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query2.png)</span><span class="sxs-lookup"><span data-stu-id="80091-115">![Add filter](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query2.png)</span></span>

4. <span data-ttu-id="80091-116">Select the control number that you want to filter data for, and then select **Apply**.</span><span class="sxs-lookup"><span data-stu-id="80091-116">Select the control number that you want to filter data for, and then select **Apply**.</span></span>  
<span data-ttu-id="80091-117">![Search on the control number](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query3.png)</span><span class="sxs-lookup"><span data-stu-id="80091-117">![Search on the control number](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query3.png)</span></span>

5. <span data-ttu-id="80091-118">Find the query that you created to filter data for the selected control number.</span><span class="sxs-lookup"><span data-stu-id="80091-118">Find the query that you created to filter data for the selected control number.</span></span>   
![Find the query](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query4.png)

6. <span data-ttu-id="80091-120">Type a name for the query, and then save it.</span><span class="sxs-lookup"><span data-stu-id="80091-120">Type a name for the query, and then save it.</span></span>   
![Save the query](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query5.png)

7. <span data-ttu-id="80091-122">To view the query, and to use it in future searches, select **Favorites**.</span><span class="sxs-lookup"><span data-stu-id="80091-122">To view the query, and to use it in future searches, select **Favorites**.</span></span>  
<span data-ttu-id="80091-123">![View the query](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query7.png)</span><span class="sxs-lookup"><span data-stu-id="80091-123">![View the query](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query7.png)</span></span>

8. <span data-ttu-id="80091-124">You can update the query to search for a new interchange control number.</span><span class="sxs-lookup"><span data-stu-id="80091-124">You can update the query to search for a new interchange control number.</span></span>  
![Update the query](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query6.png)


## <a name="next-steps"></a><span data-ttu-id="80091-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="80091-126">Next steps</span></span>
* <span data-ttu-id="80091-127">Learn more about [custom tracking schemas](logic-apps-track-integration-account-custom-tracking-schema.md).</span><span class="sxs-lookup"><span data-stu-id="80091-127">Learn more about [custom tracking schemas](logic-apps-track-integration-account-custom-tracking-schema.md).</span></span>   
* <span data-ttu-id="80091-128">Learn more about [AS2 tracking schemas](logic-apps-track-integration-account-as2-tracking-schemas.md).</span><span class="sxs-lookup"><span data-stu-id="80091-128">Learn more about [AS2 tracking schemas](logic-apps-track-integration-account-as2-tracking-schemas.md).</span></span>    
* <span data-ttu-id="80091-129">Learn more about [X12 tracking schemas](logic-apps-track-integration-account-x12-tracking-schema.md).</span><span class="sxs-lookup"><span data-stu-id="80091-129">Learn more about [X12 tracking schemas](logic-apps-track-integration-account-x12-tracking-schema.md).</span></span>  
* <span data-ttu-id="80091-130">Learn more about the [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="80091-130">Learn more about the [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span>








