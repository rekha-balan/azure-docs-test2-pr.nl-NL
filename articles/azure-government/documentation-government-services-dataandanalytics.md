---
title: Azure Government Data + Analytics
description: This provides a comparision of features and guidance on developing applications for Azure Government
services: azure-government
cloud: gov
author: jglixon
ms.author: jglixon
manager: zakramer
ms.assetid: 4b7720c1-699e-432b-9246-6e49fb77f497
ms.service: azure-government
ms.topic: article
ms.workload: azure-government
ms.date: 07/30/2018
ms.openlocfilehash: 5389be06d27755f28deb8bda5bbff8fb98a95e4e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871432"
---
# <a name="azure-government-data--analytics"></a><span data-ttu-id="316a9-103">Azure Government Data + Analytics</span><span class="sxs-lookup"><span data-stu-id="316a9-103">Azure Government Data + Analytics</span></span>
<span data-ttu-id="316a9-104">This article outlines the data and analytics services, variations, and considerations for the Azure Government environment.</span><span class="sxs-lookup"><span data-stu-id="316a9-104">This article outlines the data and analytics services, variations, and considerations for the Azure Government environment.</span></span>

## <a name="hdinsight"></a><span data-ttu-id="316a9-105">HDInsight</span><span class="sxs-lookup"><span data-stu-id="316a9-105">HDInsight</span></span>
<span data-ttu-id="316a9-106">HDInsight on Linux Standard is generally available in Azure Government.</span><span class="sxs-lookup"><span data-stu-id="316a9-106">HDInsight on Linux Standard is generally available in Azure Government.</span></span> <span data-ttu-id="316a9-107">You can see a demo on how to build data-centric solutions on Azure Government using [HDInsight](https://channel9.msdn.com/Blogs/Azure/Cognitive-Services-HDInsight-and-Power-BI-on-Azure-Government).</span><span class="sxs-lookup"><span data-stu-id="316a9-107">You can see a demo on how to build data-centric solutions on Azure Government using [HDInsight](https://channel9.msdn.com/Blogs/Azure/Cognitive-Services-HDInsight-and-Power-BI-on-Azure-Government).</span></span>

### <a name="variations"></a><span data-ttu-id="316a9-108">Variations</span><span class="sxs-lookup"><span data-stu-id="316a9-108">Variations</span></span>
<span data-ttu-id="316a9-109">The following HDInsight features are not currently available in Azure Government.</span><span class="sxs-lookup"><span data-stu-id="316a9-109">The following HDInsight features are not currently available in Azure Government.</span></span>

* <span data-ttu-id="316a9-110">HDInsight is not available on Windows.</span><span class="sxs-lookup"><span data-stu-id="316a9-110">HDInsight is not available on Windows.</span></span>
* <span data-ttu-id="316a9-111">Azure Data Lake Store is not currently available in Azure Government.</span><span class="sxs-lookup"><span data-stu-id="316a9-111">Azure Data Lake Store is not currently available in Azure Government.</span></span> <span data-ttu-id="316a9-112">Azure Blob Storage is the only available storage option currently.</span><span class="sxs-lookup"><span data-stu-id="316a9-112">Azure Blob Storage is the only available storage option currently.</span></span>

<span data-ttu-id="316a9-113">The URLs for Log Analytics are different in Azure Government:</span><span class="sxs-lookup"><span data-stu-id="316a9-113">The URLs for Log Analytics are different in Azure Government:</span></span>

| <span data-ttu-id="316a9-114">Service Type</span><span class="sxs-lookup"><span data-stu-id="316a9-114">Service Type</span></span> | <span data-ttu-id="316a9-115">Azure Public</span><span class="sxs-lookup"><span data-stu-id="316a9-115">Azure Public</span></span> | <span data-ttu-id="316a9-116">Azure Government</span><span class="sxs-lookup"><span data-stu-id="316a9-116">Azure Government</span></span> |
| --- | --- | --- |
| <span data-ttu-id="316a9-117">HDInsight Cluster</span><span class="sxs-lookup"><span data-stu-id="316a9-117">HDInsight Cluster</span></span> | <span data-ttu-id="316a9-118">\*.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="316a9-118">\*.azurehdinsight.net</span></span> | <span data-ttu-id="316a9-119">\*.azurehdinsight.us</span><span class="sxs-lookup"><span data-stu-id="316a9-119">\*.azurehdinsight.us</span></span> |

<span data-ttu-id="316a9-120">For secured virtual networks, you will want to allow Network Security Groups (NSGs) access to certain IP addresses and ports.</span><span class="sxs-lookup"><span data-stu-id="316a9-120">For secured virtual networks, you will want to allow Network Security Groups (NSGs) access to certain IP addresses and ports.</span></span> <span data-ttu-id="316a9-121">For Azure Government, you should allow the follow IP addresses (all with an Allowed port of 443):</span><span class="sxs-lookup"><span data-stu-id="316a9-121">For Azure Government, you should allow the follow IP addresses (all with an Allowed port of 443):</span></span>

| <span data-ttu-id="316a9-122">Region</span><span class="sxs-lookup"><span data-stu-id="316a9-122">Region</span></span> | <span data-ttu-id="316a9-123">Allowed IP addresses</span><span class="sxs-lookup"><span data-stu-id="316a9-123">Allowed IP addresses</span></span> | <span data-ttu-id="316a9-124">Allowed port</span><span class="sxs-lookup"><span data-stu-id="316a9-124">Allowed port</span></span> |
| ---- | ---- | ---- | ---- |
| <span data-ttu-id="316a9-125">USGov Iowa</span><span class="sxs-lookup"><span data-stu-id="316a9-125">USGov Iowa</span></span> | <span data-ttu-id="316a9-126">13.72.184.124</span><span class="sxs-lookup"><span data-stu-id="316a9-126">13.72.184.124</span></span></br><span data-ttu-id="316a9-127">13.72.190.110</span><span class="sxs-lookup"><span data-stu-id="316a9-127">13.72.190.110</span></span> | <span data-ttu-id="316a9-128">443</span><span class="sxs-lookup"><span data-stu-id="316a9-128">443</span></span> |
| <span data-ttu-id="316a9-129">USGov Virginia</span><span class="sxs-lookup"><span data-stu-id="316a9-129">USGov Virginia</span></span> | <span data-ttu-id="316a9-130">13.72.49.126</span><span class="sxs-lookup"><span data-stu-id="316a9-130">13.72.49.126</span></span></br><span data-ttu-id="316a9-131">13.72.55.55</span><span class="sxs-lookup"><span data-stu-id="316a9-131">13.72.55.55</span></span> | <span data-ttu-id="316a9-132">443</span><span class="sxs-lookup"><span data-stu-id="316a9-132">443</span></span> |

<span data-ttu-id="316a9-133">For more information, see [HDInsight public documentation](../hdinsight/hadoop/apache-hadoop-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="316a9-133">For more information, see [HDInsight public documentation](../hdinsight/hadoop/apache-hadoop-introduction.md).</span></span>

## <a name="power-bi"></a><span data-ttu-id="316a9-134">Power BI</span><span class="sxs-lookup"><span data-stu-id="316a9-134">Power BI</span></span>
<span data-ttu-id="316a9-135">Power BI US Government is generally available as part of the Office 365 US Government Community subscriptions.</span><span class="sxs-lookup"><span data-stu-id="316a9-135">Power BI US Government is generally available as part of the Office 365 US Government Community subscriptions.</span></span> <span data-ttu-id="316a9-136">You can learn about [Power BI US Government here](https://powerbi.microsoft.com/en-us/documentation/powerbi-service-govus-overview/).</span><span class="sxs-lookup"><span data-stu-id="316a9-136">You can learn about [Power BI US Government here](https://powerbi.microsoft.com/en-us/documentation/powerbi-service-govus-overview/).</span></span>

<span data-ttu-id="316a9-137">You can see a demo on [how to build data-centric solutions on Azure Government using Power BI](https://channel9.msdn.com/Blogs/Azure/Cognitive-Services-HDInsight-and-Power-BI-on-Azure-Government/)</span><span class="sxs-lookup"><span data-stu-id="316a9-137">You can see a demo on [how to build data-centric solutions on Azure Government using Power BI](https://channel9.msdn.com/Blogs/Azure/Cognitive-Services-HDInsight-and-Power-BI-on-Azure-Government/)</span></span>

### <a name="variations"></a><span data-ttu-id="316a9-138">Variations</span><span class="sxs-lookup"><span data-stu-id="316a9-138">Variations</span></span>

<span data-ttu-id="316a9-139">Power BI does not yet have Portal support in the Azure Government Portal.</span><span class="sxs-lookup"><span data-stu-id="316a9-139">Power BI does not yet have Portal support in the Azure Government Portal.</span></span> 

<span data-ttu-id="316a9-140">The URLs for Power BI are different in US Government:</span><span class="sxs-lookup"><span data-stu-id="316a9-140">The URLs for Power BI are different in US Government:</span></span>

| <span data-ttu-id="316a9-141">Service Type</span><span class="sxs-lookup"><span data-stu-id="316a9-141">Service Type</span></span> | <span data-ttu-id="316a9-142">Power BI Commercial</span><span class="sxs-lookup"><span data-stu-id="316a9-142">Power BI Commercial</span></span> | <span data-ttu-id="316a9-143">Power BI US Government</span><span class="sxs-lookup"><span data-stu-id="316a9-143">Power BI US Government</span></span> |
| --- | --- | --- |
| <span data-ttu-id="316a9-144">Power BI URL</span><span class="sxs-lookup"><span data-stu-id="316a9-144">Power BI URL</span></span> | <span data-ttu-id="316a9-145">app.powerbi.com</span><span class="sxs-lookup"><span data-stu-id="316a9-145">app.powerbi.com</span></span> | <span data-ttu-id="316a9-146">app.powerbigov.us</span><span class="sxs-lookup"><span data-stu-id="316a9-146">app.powerbigov.us</span></span> |

## <a name="power-bi-embedded"></a><span data-ttu-id="316a9-147">Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="316a9-147">Power BI Embedded</span></span> 
<span data-ttu-id="316a9-148">For details on this service and how to use it, see [Azure Power BI Embedded Documentation](../power-bi-embedded/index.md).</span><span class="sxs-lookup"><span data-stu-id="316a9-148">For details on this service and how to use it, see [Azure Power BI Embedded Documentation](../power-bi-embedded/index.md).</span></span>

### <a name="variations"></a><span data-ttu-id="316a9-149">Variations</span><span class="sxs-lookup"><span data-stu-id="316a9-149">Variations</span></span>
<span data-ttu-id="316a9-150">Power BI Embedded does not yet have Portal support in the Azure Government Portal.</span><span class="sxs-lookup"><span data-stu-id="316a9-150">Power BI Embedded does not yet have Portal support in the Azure Government Portal.</span></span> 

## <a name="azure-analysis-services"></a><span data-ttu-id="316a9-151">Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="316a9-151">Azure Analysis Services</span></span>

<span data-ttu-id="316a9-152">For information on this service and how to use it, see [Azure Analysis Services Documentation](../analysis-services/index.md).</span><span class="sxs-lookup"><span data-stu-id="316a9-152">For information on this service and how to use it, see [Azure Analysis Services Documentation](../analysis-services/index.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="316a9-153">Next Steps</span><span class="sxs-lookup"><span data-stu-id="316a9-153">Next Steps</span></span>
<span data-ttu-id="316a9-154">For supplemental information and updates, subscribe to the <a href="https://blogs.msdn.microsoft.com/azuregov/">Microsoft Azure Government Blog. </a></span><span class="sxs-lookup"><span data-stu-id="316a9-154">For supplemental information and updates, subscribe to the <a href="https://blogs.msdn.microsoft.com/azuregov/">Microsoft Azure Government Blog. </a></span></span>
