---
title: Install Azure Data Lake Tools for Visual Studio
description: This article describes how to install Azure Data Lake Tools for Visual Studio.
services: data-lake-analytics
ms.service: data-lake-analytics
author: saveenr
ms.author: saveenr
ms.reviewer: jasonwhowell
ms.assetid: ad8a6992-02c7-47d4-a108-62fc5a0777a3
ms.topic: conceptual
ms.date: 05/03/2018
ms.openlocfilehash: e731f28ab416de7da30f41fe8a154108b8097b89
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868901"
---
# <a name="install-data-lake-tools-for-visual-studio"></a><span data-ttu-id="3b134-103">Install Data Lake Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3b134-103">Install Data Lake Tools for Visual Studio</span></span>

<span data-ttu-id="3b134-104">Learn how to use Visual Studio to create Azure Data Lake Analytics accounts, define jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs to the Data Lake Analytics service.</span><span class="sxs-lookup"><span data-stu-id="3b134-104">Learn how to use Visual Studio to create Azure Data Lake Analytics accounts, define jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs to the Data Lake Analytics service.</span></span> <span data-ttu-id="3b134-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3b134-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b134-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3b134-106">Prerequisites</span></span>

* <span data-ttu-id="3b134-107">**Visual Studio**: All editions except Express are supported.</span><span class="sxs-lookup"><span data-stu-id="3b134-107">**Visual Studio**: All editions except Express are supported.</span></span>
    * <span data-ttu-id="3b134-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="3b134-108">Visual Studio 2017</span></span>
    * <span data-ttu-id="3b134-109">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="3b134-109">Visual Studio 2015</span></span>
    * <span data-ttu-id="3b134-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="3b134-110">Visual Studio 2013</span></span>
* <span data-ttu-id="3b134-111">**Microsoft Azure SDK for .NET** version 2.7.1 or later.</span><span class="sxs-lookup"><span data-stu-id="3b134-111">**Microsoft Azure SDK for .NET** version 2.7.1 or later.</span></span>  <span data-ttu-id="3b134-112">Install it by using the [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="3b134-112">Install it by using the [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="3b134-113">A **Data Lake Analytics** account.</span><span class="sxs-lookup"><span data-stu-id="3b134-113">A **Data Lake Analytics** account.</span></span> <span data-ttu-id="3b134-114">To create an account, see [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3b134-114">To create an account, see [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span></span>

## <a name="install-azure-data-lake-tools-for-visual-studio-2017"></a><span data-ttu-id="3b134-115">Install Azure Data Lake Tools for Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="3b134-115">Install Azure Data Lake Tools for Visual Studio 2017</span></span>

<span data-ttu-id="3b134-116">Azure Data Lake Tools for Visual Studio is supported in Visual Studio 2017 15.3 or above.</span><span class="sxs-lookup"><span data-stu-id="3b134-116">Azure Data Lake Tools for Visual Studio is supported in Visual Studio 2017 15.3 or above.</span></span> <span data-ttu-id="3b134-117">The tool is part of the **Data storage and processing** and **Azure Development** workloads in Visual Studio Installer.</span><span class="sxs-lookup"><span data-stu-id="3b134-117">The tool is part of the **Data storage and processing** and **Azure Development** workloads in Visual Studio Installer.</span></span> <span data-ttu-id="3b134-118">Enable either one of these two workloads as part of your Visual Studio installation.</span><span class="sxs-lookup"><span data-stu-id="3b134-118">Enable either one of these two workloads as part of your Visual Studio installation.</span></span>  

<span data-ttu-id="3b134-119">Enable the **Data storage and processing** workload as shown: ![Enable Data storage and processing workload](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-tools-for-vs-2017-install-01.png)</span><span class="sxs-lookup"><span data-stu-id="3b134-119">Enable the **Data storage and processing** workload as shown: ![Enable Data storage and processing workload](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-tools-for-vs-2017-install-01.png)</span></span>

<span data-ttu-id="3b134-120">Enable the **Azure development** workload as shown: ![Enable Azure development workload](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-tools-for-vs-2017-install-02.png)</span><span class="sxs-lookup"><span data-stu-id="3b134-120">Enable the **Azure development** workload as shown: ![Enable Azure development workload](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-tools-for-vs-2017-install-02.png)</span></span>

## <a name="install-azure-data-lake-tools-for-visual-studio-2013-and-2015"></a><span data-ttu-id="3b134-121">Install Azure Data Lake Tools for Visual Studio 2013 and 2015</span><span class="sxs-lookup"><span data-stu-id="3b134-121">Install Azure Data Lake Tools for Visual Studio 2013 and 2015</span></span>

<span data-ttu-id="3b134-122">Download and install Azure Data Lake Tools for Visual Studio [from the Download Center](http://aka.ms/adltoolsvs).</span><span class="sxs-lookup"><span data-stu-id="3b134-122">Download and install Azure Data Lake Tools for Visual Studio [from the Download Center](http://aka.ms/adltoolsvs).</span></span> <span data-ttu-id="3b134-123">After installation, note that:</span><span class="sxs-lookup"><span data-stu-id="3b134-123">After installation, note that:</span></span>
* <span data-ttu-id="3b134-124">The **Server Explorer** > **Azure** node contains a **Data Lake Analytics** node.</span><span class="sxs-lookup"><span data-stu-id="3b134-124">The **Server Explorer** > **Azure** node contains a **Data Lake Analytics** node.</span></span> 
* <span data-ttu-id="3b134-125">The **Tools** menu has a **Data Lake** item.</span><span class="sxs-lookup"><span data-stu-id="3b134-125">The **Tools** menu has a **Data Lake** item.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3b134-126">Next Steps</span><span class="sxs-lookup"><span data-stu-id="3b134-126">Next Steps</span></span>
* <span data-ttu-id="3b134-127">To log diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md)</span><span class="sxs-lookup"><span data-stu-id="3b134-127">To log diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md)</span></span>
* <span data-ttu-id="3b134-128">To see a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="3b134-128">To see a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="3b134-129">To use the vertex execution view, see [Use the Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md)</span><span class="sxs-lookup"><span data-stu-id="3b134-129">To use the vertex execution view, see [Use the Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md)</span></span>
