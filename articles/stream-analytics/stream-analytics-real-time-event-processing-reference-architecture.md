---
title: Real-time event processing using Azure Stream Analytics event processing
description: This article describes the reference architecture to acheive real-time event processing and analytics using Azure Stream Analytics.
services: stream-analytics
author: jseb225
ms.author: jeanb
manager: kfile
ms.reviewer: jasonh
ms.service: stream-analytics
ms.topic: conceptual
ms.date: 01/24/2017
ms.openlocfilehash: 8a5d426d67916e010c7fff048eebdc77b93c5c38
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44826878"
---
# <a name="reference-architecture-real-time-event-processing-with-microsoft-azure-stream-analytics"></a><span data-ttu-id="1e50c-103">Reference architecture: Real-time event processing with Microsoft Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1e50c-103">Reference architecture: Real-time event processing with Microsoft Azure Stream Analytics</span></span>
<span data-ttu-id="1e50c-104">The reference architecture for real-time event processing with Azure Stream Analytics is intended to provide a generic blueprint for deploying a real-time platform as a service (PaaS) stream-processing solution with Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="1e50c-104">The reference architecture for real-time event processing with Azure Stream Analytics is intended to provide a generic blueprint for deploying a real-time platform as a service (PaaS) stream-processing solution with Microsoft Azure.</span></span>

## <a name="summary"></a><span data-ttu-id="1e50c-105">Summary</span><span class="sxs-lookup"><span data-stu-id="1e50c-105">Summary</span></span>
<span data-ttu-id="1e50c-106">Traditionally, analytics solutions have been based on capabilities such as ETL (extract, transform, load) and data warehousing, where data is stored prior to analysis.</span><span class="sxs-lookup"><span data-stu-id="1e50c-106">Traditionally, analytics solutions have been based on capabilities such as ETL (extract, transform, load) and data warehousing, where data is stored prior to analysis.</span></span> <span data-ttu-id="1e50c-107">Changing requirements, including more rapidly arriving data, are pushing this existing model to the limit.</span><span class="sxs-lookup"><span data-stu-id="1e50c-107">Changing requirements, including more rapidly arriving data, are pushing this existing model to the limit.</span></span> <span data-ttu-id="1e50c-108">The ability to analyze data within moving streams prior to storage is one solution, and while it is not a new capability, the approach has not been widely adopted across all industry verticals.</span><span class="sxs-lookup"><span data-stu-id="1e50c-108">The ability to analyze data within moving streams prior to storage is one solution, and while it is not a new capability, the approach has not been widely adopted across all industry verticals.</span></span> 

<span data-ttu-id="1e50c-109">Microsoft Azure provides an extensive catalog of analytics technologies that are capable of supporting an array of different solution scenarios and requirements.</span><span class="sxs-lookup"><span data-stu-id="1e50c-109">Microsoft Azure provides an extensive catalog of analytics technologies that are capable of supporting an array of different solution scenarios and requirements.</span></span> <span data-ttu-id="1e50c-110">Selecting which Azure services to deploy for an end-to-end solution can be a challenge given the breadth of offerings.</span><span class="sxs-lookup"><span data-stu-id="1e50c-110">Selecting which Azure services to deploy for an end-to-end solution can be a challenge given the breadth of offerings.</span></span> <span data-ttu-id="1e50c-111">This paper is designed to describe the capabilities and interoperation of the various Azure services that support an event-streaming solution.</span><span class="sxs-lookup"><span data-stu-id="1e50c-111">This paper is designed to describe the capabilities and interoperation of the various Azure services that support an event-streaming solution.</span></span> <span data-ttu-id="1e50c-112">It also explains some of the scenarios in which customers can benefit from this type of approach.</span><span class="sxs-lookup"><span data-stu-id="1e50c-112">It also explains some of the scenarios in which customers can benefit from this type of approach.</span></span>

## <a name="contents"></a><span data-ttu-id="1e50c-113">Contents</span><span class="sxs-lookup"><span data-stu-id="1e50c-113">Contents</span></span>
* <span data-ttu-id="1e50c-114">Executive Summary</span><span class="sxs-lookup"><span data-stu-id="1e50c-114">Executive Summary</span></span>
* <span data-ttu-id="1e50c-115">Introduction to Real-Time Analytics</span><span class="sxs-lookup"><span data-stu-id="1e50c-115">Introduction to Real-Time Analytics</span></span>
* <span data-ttu-id="1e50c-116">Value Proposition of Real-Time Data in Azure</span><span class="sxs-lookup"><span data-stu-id="1e50c-116">Value Proposition of Real-Time Data in Azure</span></span>
* <span data-ttu-id="1e50c-117">Common Scenarios for Real-Time Analytics</span><span class="sxs-lookup"><span data-stu-id="1e50c-117">Common Scenarios for Real-Time Analytics</span></span>
* <span data-ttu-id="1e50c-118">Architecture and Components</span><span class="sxs-lookup"><span data-stu-id="1e50c-118">Architecture and Components</span></span>
  * <span data-ttu-id="1e50c-119">Data Sources</span><span class="sxs-lookup"><span data-stu-id="1e50c-119">Data Sources</span></span>
  * <span data-ttu-id="1e50c-120">Data-Integration Layer</span><span class="sxs-lookup"><span data-stu-id="1e50c-120">Data-Integration Layer</span></span>
  * <span data-ttu-id="1e50c-121">Real-time Analytics Layer</span><span class="sxs-lookup"><span data-stu-id="1e50c-121">Real-time Analytics Layer</span></span>
  * <span data-ttu-id="1e50c-122">Data Storage Layer</span><span class="sxs-lookup"><span data-stu-id="1e50c-122">Data Storage Layer</span></span>
  * <span data-ttu-id="1e50c-123">Presentation / Consumption Layer</span><span class="sxs-lookup"><span data-stu-id="1e50c-123">Presentation / Consumption Layer</span></span>
* <span data-ttu-id="1e50c-124">Conclusion</span><span class="sxs-lookup"><span data-stu-id="1e50c-124">Conclusion</span></span>

<span data-ttu-id="1e50c-125">**Author:** Charles Feddersen, Solution Architect, Data Insights Center of Excellence, Microsoft Corporation</span><span class="sxs-lookup"><span data-stu-id="1e50c-125">**Author:** Charles Feddersen, Solution Architect, Data Insights Center of Excellence, Microsoft Corporation</span></span>

<span data-ttu-id="1e50c-126">**Published:** January 2015</span><span class="sxs-lookup"><span data-stu-id="1e50c-126">**Published:** January 2015</span></span>

<span data-ttu-id="1e50c-127">**Revision:** 1.0</span><span class="sxs-lookup"><span data-stu-id="1e50c-127">**Revision:** 1.0</span></span>

<span data-ttu-id="1e50c-128">**Download:** [Real-Time Event Processing with Microsoft Azure Stream Analytics](http://download.microsoft.com/download/6/2/3/623924DE-B083-4561-9624-C1AB62B5F82B/real-time-event-processing-with-microsoft-azure-stream-analytics.pdf)</span><span class="sxs-lookup"><span data-stu-id="1e50c-128">**Download:** [Real-Time Event Processing with Microsoft Azure Stream Analytics](http://download.microsoft.com/download/6/2/3/623924DE-B083-4561-9624-C1AB62B5F82B/real-time-event-processing-with-microsoft-azure-stream-analytics.pdf)</span></span>

## <a name="get-help"></a><span data-ttu-id="1e50c-129">Get help</span><span class="sxs-lookup"><span data-stu-id="1e50c-129">Get help</span></span>
<span data-ttu-id="1e50c-130">For further assistance, try the [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="1e50c-130">For further assistance, try the [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e50c-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="1e50c-131">Next steps</span></span>
* [<span data-ttu-id="1e50c-132">Introduction to Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1e50c-132">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="1e50c-133">Get started using Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1e50c-133">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="1e50c-134">Scale Azure Stream Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="1e50c-134">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="1e50c-135">Azure Stream Analytics Query Language Reference</span><span class="sxs-lookup"><span data-stu-id="1e50c-135">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="1e50c-136">Azure Stream Analytics Management REST API Reference</span><span class="sxs-lookup"><span data-stu-id="1e50c-136">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

