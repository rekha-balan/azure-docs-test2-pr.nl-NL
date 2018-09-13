---
title: Azure Government Intelligence + Analytics | Microsoft Docs
description: This provides a comparision of features and guidance on developing applications for Azure Government
services: azure-government
cloud: gov
documentationcenter: ''
author: MeganYount
manager: zakramer
ms.assetid: 4b7720c1-699e-432b-9246-6e49fb77f497
ms.service: azure-government
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: azure-government
ms.date: 12/06/2016
ms.author: MeganYount
ms.openlocfilehash: 0233aa66bc4f4f135456ec15bd09756e63192b14
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553611"
---
# <a name="azure-government-intelligence--analytics"></a><span data-ttu-id="47d1c-103">Azure Government Intelligence + Analytics</span><span class="sxs-lookup"><span data-stu-id="47d1c-103">Azure Government Intelligence + Analytics</span></span>
<span data-ttu-id="47d1c-104">This article outlines the intelligence and analytics services, variations, and considerations for the Azure Government environment.</span><span class="sxs-lookup"><span data-stu-id="47d1c-104">This article outlines the intelligence and analytics services, variations, and considerations for the Azure Government environment.</span></span>

## <a name="hdinsight"></a><span data-ttu-id="47d1c-105">HDInsight</span><span class="sxs-lookup"><span data-stu-id="47d1c-105">HDInsight</span></span>
<span data-ttu-id="47d1c-106">HDInsight on Linux Standard is generally available in Azure Government.</span><span class="sxs-lookup"><span data-stu-id="47d1c-106">HDInsight on Linux Standard is generally available in Azure Government.</span></span> <span data-ttu-id="47d1c-107">You can see a demo on how to build data-centric solutions on Azure Government using HDInsight <a href=https://channel9.msdn.com/Blogs/Azure/Cognitive-Services-HDInsight-and-Power-BI-on-Azure-Government/>here</a>.</span><span class="sxs-lookup"><span data-stu-id="47d1c-107">You can see a demo on how to build data-centric solutions on Azure Government using HDInsight <a href=https://channel9.msdn.com/Blogs/Azure/Cognitive-Services-HDInsight-and-Power-BI-on-Azure-Government/>here</a>.</span></span>

<span data-ttu-id="47d1c-108">HDInsight on Linux Premium is coming soon.</span><span class="sxs-lookup"><span data-stu-id="47d1c-108">HDInsight on Linux Premium is coming soon.</span></span>

### <a name="variations"></a><span data-ttu-id="47d1c-109">Variations</span><span class="sxs-lookup"><span data-stu-id="47d1c-109">Variations</span></span>
<span data-ttu-id="47d1c-110">The following HDInsight features are not currently available in Azure Government.</span><span class="sxs-lookup"><span data-stu-id="47d1c-110">The following HDInsight features are not currently available in Azure Government.</span></span>

* <span data-ttu-id="47d1c-111">HDInsight is not available on Windows.</span><span class="sxs-lookup"><span data-stu-id="47d1c-111">HDInsight is not available on Windows.</span></span>
* <span data-ttu-id="47d1c-112">Azure Data Lake Store is not currently available in Azure Government.</span><span class="sxs-lookup"><span data-stu-id="47d1c-112">Azure Data Lake Store is not currently available in Azure Government.</span></span> <span data-ttu-id="47d1c-113">Azure Blob Storage is the only available storage option currently.</span><span class="sxs-lookup"><span data-stu-id="47d1c-113">Azure Blob Storage is the only available storage option currently.</span></span>

<span data-ttu-id="47d1c-114">The URLs for Log Analytics are different in Azure Government:</span><span class="sxs-lookup"><span data-stu-id="47d1c-114">The URLs for Log Analytics are different in Azure Government:</span></span>

| <span data-ttu-id="47d1c-115">Service Type</span><span class="sxs-lookup"><span data-stu-id="47d1c-115">Service Type</span></span> | <span data-ttu-id="47d1c-116">Azure Public</span><span class="sxs-lookup"><span data-stu-id="47d1c-116">Azure Public</span></span> | <span data-ttu-id="47d1c-117">Azure Government</span><span class="sxs-lookup"><span data-stu-id="47d1c-117">Azure Government</span></span> |
| --- | --- | --- |
| <span data-ttu-id="47d1c-118">HDInsight Cluster</span><span class="sxs-lookup"><span data-stu-id="47d1c-118">HDInsight Cluster</span></span> | <span data-ttu-id="47d1c-119">\*.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="47d1c-119">\*.azurehdinsight.net</span></span> | <span data-ttu-id="47d1c-120">\*.azurehdinsight.us</span><span class="sxs-lookup"><span data-stu-id="47d1c-120">\*.azurehdinsight.us</span></span> |

<span data-ttu-id="47d1c-121">For more information, see [HDInsight public documentation](../hdinsight/hdinsight-hadoop-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="47d1c-121">For more information, see [HDInsight public documentation](../hdinsight/hdinsight-hadoop-introduction.md).</span></span>

## <a name="power-bi"></a><span data-ttu-id="47d1c-122">Power BI</span><span class="sxs-lookup"><span data-stu-id="47d1c-122">Power BI</span></span>
<span data-ttu-id="47d1c-123">Power BI US Government is generally available as part of the Office 365 US Government Community subscriptions.</span><span class="sxs-lookup"><span data-stu-id="47d1c-123">Power BI US Government is generally available as part of the Office 365 US Government Community subscriptions.</span></span> <span data-ttu-id="47d1c-124">You can learn about Power BI US Government <a href=https://powerbi.microsoft.com/en-us/documentation/powerbi-service-govus-overview/>here</a>.</span><span class="sxs-lookup"><span data-stu-id="47d1c-124">You can learn about Power BI US Government <a href=https://powerbi.microsoft.com/en-us/documentation/powerbi-service-govus-overview/>here</a>.</span></span> <span data-ttu-id="47d1c-125">You can see a demo on how to build data-centric solutions on Azure Government using Power BI <a href=https://channel9.msdn.com/Blogs/Azure/Cognitive-Services-HDInsight-and-Power-BI-on-Azure-Government/>here</a>.</span><span class="sxs-lookup"><span data-stu-id="47d1c-125">You can see a demo on how to build data-centric solutions on Azure Government using Power BI <a href=https://channel9.msdn.com/Blogs/Azure/Cognitive-Services-HDInsight-and-Power-BI-on-Azure-Government/>here</a>.</span></span>

<span data-ttu-id="47d1c-126">Power BI Embedded is coming soon.</span><span class="sxs-lookup"><span data-stu-id="47d1c-126">Power BI Embedded is coming soon.</span></span>

### <a name="variations"></a><span data-ttu-id="47d1c-127">Variations</span><span class="sxs-lookup"><span data-stu-id="47d1c-127">Variations</span></span>

<span data-ttu-id="47d1c-128">The URLs for Power BI are different in US Government:</span><span class="sxs-lookup"><span data-stu-id="47d1c-128">The URLs for Power BI are different in US Government:</span></span>

| <span data-ttu-id="47d1c-129">Service Type</span><span class="sxs-lookup"><span data-stu-id="47d1c-129">Service Type</span></span> | <span data-ttu-id="47d1c-130">Power BI Commercial</span><span class="sxs-lookup"><span data-stu-id="47d1c-130">Power BI Commercial</span></span> | <span data-ttu-id="47d1c-131">Power BI US Government</span><span class="sxs-lookup"><span data-stu-id="47d1c-131">Power BI US Government</span></span> |
| --- | --- | --- |
| <span data-ttu-id="47d1c-132">Power BI URL</span><span class="sxs-lookup"><span data-stu-id="47d1c-132">Power BI URL</span></span> | <span data-ttu-id="47d1c-133">app.powerbi.com</span><span class="sxs-lookup"><span data-stu-id="47d1c-133">app.powerbi.com</span></span> | <span data-ttu-id="47d1c-134">app.powerbigov.us</span><span class="sxs-lookup"><span data-stu-id="47d1c-134">app.powerbigov.us</span></span> |

## <a name="next-steps"></a><span data-ttu-id="47d1c-135">Next Steps</span><span class="sxs-lookup"><span data-stu-id="47d1c-135">Next Steps</span></span>
<span data-ttu-id="47d1c-136">For supplemental information and updates, subscribe to the <a href="https://blogs.msdn.microsoft.com/azuregov/">Microsoft Azure Government Blog. </a></span><span class="sxs-lookup"><span data-stu-id="47d1c-136">For supplemental information and updates, subscribe to the <a href="https://blogs.msdn.microsoft.com/azuregov/">Microsoft Azure Government Blog. </a></span></span>
