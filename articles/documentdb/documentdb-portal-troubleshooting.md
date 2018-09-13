---
title: Troubleshooting DocumentDB portal issues | Microsoft Docs
description: Find out to resolve issues in the DocumentDB Azure portal.
services: documentdb
documentationcenter: ''
author: mimig1
manager: jhubbard
editor: monicar
ms.assetid: 36ad9bf4-2617-4347-ba29-edebf62fc3ec
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/22/2016
ms.author: mimig
ms.openlocfilehash: 55ff7cab0c9528b7732198e219dd43198130424e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563570"
---
# <a name="azure-documentdb-portal-troubleshooting-tips"></a><span data-ttu-id="2eed3-103">Azure DocumentDB portal troubleshooting tips</span><span class="sxs-lookup"><span data-stu-id="2eed3-103">Azure DocumentDB portal troubleshooting tips</span></span>
<span data-ttu-id="2eed3-104">This article describes how to resolve DocumentDB issues in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2eed3-104">This article describes how to resolve DocumentDB issues in the Azure portal.</span></span> 

## <a name="resources-are-missing"></a><span data-ttu-id="2eed3-105">Resources are missing</span><span class="sxs-lookup"><span data-stu-id="2eed3-105">Resources are missing</span></span>
<span data-ttu-id="2eed3-106">**Symptom**: Databases or collections are missing from your portal blades.</span><span class="sxs-lookup"><span data-stu-id="2eed3-106">**Symptom**: Databases or collections are missing from your portal blades.</span></span>

<span data-ttu-id="2eed3-107">**Solution**: Lower application usage to operate under the maximum throughput quota for the collection.</span><span class="sxs-lookup"><span data-stu-id="2eed3-107">**Solution**: Lower application usage to operate under the maximum throughput quota for the collection.</span></span> 

<span data-ttu-id="2eed3-108">**Explanation**: The portal is an application like any other, making calls to your DocumentDB database and collection.</span><span class="sxs-lookup"><span data-stu-id="2eed3-108">**Explanation**: The portal is an application like any other, making calls to your DocumentDB database and collection.</span></span> <span data-ttu-id="2eed3-109">If your requests are currently being throttled due to calls being made from a separate application, the portal may also be throttled, causing resources not to appear in the portal.</span><span class="sxs-lookup"><span data-stu-id="2eed3-109">If your requests are currently being throttled due to calls being made from a separate application, the portal may also be throttled, causing resources not to appear in the portal.</span></span> <span data-ttu-id="2eed3-110">To resolve the issue, address the cause of the high throughput usage, and then refresh the portal blade.</span><span class="sxs-lookup"><span data-stu-id="2eed3-110">To resolve the issue, address the cause of the high throughput usage, and then refresh the portal blade.</span></span> <span data-ttu-id="2eed3-111">Information on how to measure and lower throughput usage can be found in the [Throughput](documentdb-performance-tips.md#throughput) section of the [Performance tips](documentdb-performance-tips.md) article.</span><span class="sxs-lookup"><span data-stu-id="2eed3-111">Information on how to measure and lower throughput usage can be found in the [Throughput](documentdb-performance-tips.md#throughput) section of the [Performance tips](documentdb-performance-tips.md) article.</span></span>

## <a name="pages-or-blades-wont-load"></a><span data-ttu-id="2eed3-112">Pages or blades won't load</span><span class="sxs-lookup"><span data-stu-id="2eed3-112">Pages or blades won't load</span></span>
<span data-ttu-id="2eed3-113">**Symptom**: Pages and blades in the portal do not display.</span><span class="sxs-lookup"><span data-stu-id="2eed3-113">**Symptom**: Pages and blades in the portal do not display.</span></span>

<span data-ttu-id="2eed3-114">**Solution**: Lower application usage to operate under the maximum throughput quota for the collection.</span><span class="sxs-lookup"><span data-stu-id="2eed3-114">**Solution**: Lower application usage to operate under the maximum throughput quota for the collection.</span></span> 

<span data-ttu-id="2eed3-115">**Explanation**: The portal is an application like any other, making calls to your DocumentDB database and collection.</span><span class="sxs-lookup"><span data-stu-id="2eed3-115">**Explanation**: The portal is an application like any other, making calls to your DocumentDB database and collection.</span></span> <span data-ttu-id="2eed3-116">If your requests are currently being throttled due to calls being made from a separate application, the portal may also be throttled, causing resources not to appear in the portal.</span><span class="sxs-lookup"><span data-stu-id="2eed3-116">If your requests are currently being throttled due to calls being made from a separate application, the portal may also be throttled, causing resources not to appear in the portal.</span></span> <span data-ttu-id="2eed3-117">To resolve the issue, address the cause of the high throughput usage, and then refresh the portal blade.</span><span class="sxs-lookup"><span data-stu-id="2eed3-117">To resolve the issue, address the cause of the high throughput usage, and then refresh the portal blade.</span></span> <span data-ttu-id="2eed3-118">Information on how to measure and lower throughput usage can be found in the [Throughput](documentdb-performance-tips.md#throughput) section of the [Performance tips](documentdb-performance-tips.md) article.</span><span class="sxs-lookup"><span data-stu-id="2eed3-118">Information on how to measure and lower throughput usage can be found in the [Throughput](documentdb-performance-tips.md#throughput) section of the [Performance tips](documentdb-performance-tips.md) article.</span></span>

## <a name="add-collection-button-is-disabled"></a><span data-ttu-id="2eed3-119">Add Collection button is disabled</span><span class="sxs-lookup"><span data-stu-id="2eed3-119">Add Collection button is disabled</span></span>
<span data-ttu-id="2eed3-120">**Symptom**: On the Database blade, the **Add Collection** button is disabled.</span><span class="sxs-lookup"><span data-stu-id="2eed3-120">**Symptom**: On the Database blade, the **Add Collection** button is disabled.</span></span>

<span data-ttu-id="2eed3-121">**Explanation**: If your Azure subscription is associated with benefit credits, such as free credits offered from an MSDN subscription, and you have used all of your credits for the month, you are unable to create any additional collections in DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="2eed3-121">**Explanation**: If your Azure subscription is associated with benefit credits, such as free credits offered from an MSDN subscription, and you have used all of your credits for the month, you are unable to create any additional collections in DocumentDB.</span></span>

<span data-ttu-id="2eed3-122">**Solution**: Remove the spending limit from your account.</span><span class="sxs-lookup"><span data-stu-id="2eed3-122">**Solution**: Remove the spending limit from your account.</span></span>

1. <span data-ttu-id="2eed3-123">In the Azure portal, in the Jumpbar, click **Subscriptions**, click the subscription associated with the DocumentDB database, and then in the **Subscription** blade, click **Manage**.</span><span class="sxs-lookup"><span data-stu-id="2eed3-123">In the Azure portal, in the Jumpbar, click **Subscriptions**, click the subscription associated with the DocumentDB database, and then in the **Subscription** blade, click **Manage**.</span></span> 
    <span data-ttu-id="2eed3-124">![DocumentDB offers multiple, well defined (relaxed) consistency models to choose from](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-portal-troubleshooting/documentdb-change-billing.png)</span><span class="sxs-lookup"><span data-stu-id="2eed3-124">![DocumentDB offers multiple, well defined (relaxed) consistency models to choose from](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-portal-troubleshooting/documentdb-change-billing.png)</span></span>
2. <span data-ttu-id="2eed3-125">In the new browser window, you'll see that you have no credits remaining.</span><span class="sxs-lookup"><span data-stu-id="2eed3-125">In the new browser window, you'll see that you have no credits remaining.</span></span> <span data-ttu-id="2eed3-126">Click the **Remove spending limit** button to remove the spending for only the current billing period or indefinitely.</span><span class="sxs-lookup"><span data-stu-id="2eed3-126">Click the **Remove spending limit** button to remove the spending for only the current billing period or indefinitely.</span></span> <span data-ttu-id="2eed3-127">Then complete the wizard to add or confirm your credit card information.</span><span class="sxs-lookup"><span data-stu-id="2eed3-127">Then complete the wizard to add or confirm your credit card information.</span></span> 
    <span data-ttu-id="2eed3-128">![DocumentDB offers multiple, well defined (relaxed) consistency models to choose from](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-portal-troubleshooting/documentdb-remove-spending-limit.png)</span><span class="sxs-lookup"><span data-stu-id="2eed3-128">![DocumentDB offers multiple, well defined (relaxed) consistency models to choose from](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-portal-troubleshooting/documentdb-remove-spending-limit.png)</span></span>

## <a name="query-explorer-completes-with-errors"></a><span data-ttu-id="2eed3-129">Query Explorer completes with errors</span><span class="sxs-lookup"><span data-stu-id="2eed3-129">Query Explorer completes with errors</span></span>
<span data-ttu-id="2eed3-130">See [Troubleshoot Query Explorer](documentdb-query-collections-query-explorer.md#troubleshoot).</span><span class="sxs-lookup"><span data-stu-id="2eed3-130">See [Troubleshoot Query Explorer](documentdb-query-collections-query-explorer.md#troubleshoot).</span></span>

## <a name="no-data-available-in-monitoring-tiles"></a><span data-ttu-id="2eed3-131">No data available in monitoring tiles</span><span class="sxs-lookup"><span data-stu-id="2eed3-131">No data available in monitoring tiles</span></span>
<span data-ttu-id="2eed3-132">See [Troubleshoot monitoring tiles](documentdb-monitor-accounts.md#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="2eed3-132">See [Troubleshoot monitoring tiles](documentdb-monitor-accounts.md#troubleshooting).</span></span>

## <a name="no-documents-returned-in-document-explorer"></a><span data-ttu-id="2eed3-133">No documents returned in Document Explorer</span><span class="sxs-lookup"><span data-stu-id="2eed3-133">No documents returned in Document Explorer</span></span>
<span data-ttu-id="2eed3-134">See [Troubleshooting Document Explorer](documentdb-view-json-document-explorer.md#troubleshoot).</span><span class="sxs-lookup"><span data-stu-id="2eed3-134">See [Troubleshooting Document Explorer](documentdb-view-json-document-explorer.md#troubleshoot).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2eed3-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="2eed3-135">Next steps</span></span>
<span data-ttu-id="2eed3-136">If you are still experiencing issues in the portal, please email [askdocdb@microsoft.com](mailto:askdocdb@microsoft.com) for assistance, or file a support request in the portal by clicking **Browse**, **Help + support**, and then clicking **Create support request**.</span><span class="sxs-lookup"><span data-stu-id="2eed3-136">If you are still experiencing issues in the portal, please email [askdocdb@microsoft.com](mailto:askdocdb@microsoft.com) for assistance, or file a support request in the portal by clicking **Browse**, **Help + support**, and then clicking **Create support request**.</span></span>



