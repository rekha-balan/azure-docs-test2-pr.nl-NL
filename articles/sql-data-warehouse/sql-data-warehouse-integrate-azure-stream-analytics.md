---
title: Use Azure Stream Analytics with SQL Data Warehouse | Microsoft Docs
description: Tips for using Azure Stream Analytics with Azure SQL Data Warehouse for developing solutions.
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: barbkess
editor: ''
ms.assetid: 8aeb2247-20c5-4a29-b327-30a8ce09dfdc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: 99adddc04c5c0826fc4e57ded81729c3ed127d9d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563586"
---
# <a name="use-azure-stream-analytics-with-sql-data-warehouse"></a><span data-ttu-id="fc95f-103">Use Azure Stream Analytics with SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="fc95f-103">Use Azure Stream Analytics with SQL Data Warehouse</span></span>
<span data-ttu-id="fc95f-104">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable complex event processing over streaming data in the cloud.</span><span class="sxs-lookup"><span data-stu-id="fc95f-104">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable complex event processing over streaming data in the cloud.</span></span> <span data-ttu-id="fc95f-105">You can learn the basics by reading [Introduction to Azure Stream Analytics][Introduction to Azure Stream Analytics].</span><span class="sxs-lookup"><span data-stu-id="fc95f-105">You can learn the basics by reading [Introduction to Azure Stream Analytics][Introduction to Azure Stream Analytics].</span></span> <span data-ttu-id="fc95f-106">You can then learn how to create an end-to-end solution with Stream Analytics by following the [Get started using Azure Stream Analytics][Get started using Azure Stream Analytics] tutorial.</span><span class="sxs-lookup"><span data-stu-id="fc95f-106">You can then learn how to create an end-to-end solution with Stream Analytics by following the [Get started using Azure Stream Analytics][Get started using Azure Stream Analytics] tutorial.</span></span>

<span data-ttu-id="fc95f-107">In this article, you will learn how to use your Azure SQL Data Warehouse database as an output sink for your Steam Analytics jobs.</span><span class="sxs-lookup"><span data-stu-id="fc95f-107">In this article, you will learn how to use your Azure SQL Data Warehouse database as an output sink for your Steam Analytics jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fc95f-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="fc95f-108">Prerequisites</span></span>
<span data-ttu-id="fc95f-109">First, run through the following steps in the [Get started using Azure Stream Analytics][Get started using Azure Stream Analytics] tutorial.</span><span class="sxs-lookup"><span data-stu-id="fc95f-109">First, run through the following steps in the [Get started using Azure Stream Analytics][Get started using Azure Stream Analytics] tutorial.</span></span>  

1. <span data-ttu-id="fc95f-110">Create an Event Hub input</span><span class="sxs-lookup"><span data-stu-id="fc95f-110">Create an Event Hub input</span></span>
2. <span data-ttu-id="fc95f-111">Configure and start event generator application</span><span class="sxs-lookup"><span data-stu-id="fc95f-111">Configure and start event generator application</span></span>
3. <span data-ttu-id="fc95f-112">Provision a Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="fc95f-112">Provision a Stream Analytics job</span></span>
4. <span data-ttu-id="fc95f-113">Specify job input and query</span><span class="sxs-lookup"><span data-stu-id="fc95f-113">Specify job input and query</span></span>

<span data-ttu-id="fc95f-114">Then, create an Azure SQL Data Warehouse database</span><span class="sxs-lookup"><span data-stu-id="fc95f-114">Then, create an Azure SQL Data Warehouse database</span></span>

## <a name="specify-job-output-azure-sql-data-warehouse-database"></a><span data-ttu-id="fc95f-115">Specify job output: Azure SQL Data Warehouse database</span><span class="sxs-lookup"><span data-stu-id="fc95f-115">Specify job output: Azure SQL Data Warehouse database</span></span>
### <a name="step-1"></a><span data-ttu-id="fc95f-116">Step 1</span><span class="sxs-lookup"><span data-stu-id="fc95f-116">Step 1</span></span>
<span data-ttu-id="fc95f-117">In your Stream Analytics job click **OUTPUT** from the top of the page, and then click **ADD OUTPUT**.</span><span class="sxs-lookup"><span data-stu-id="fc95f-117">In your Stream Analytics job click **OUTPUT** from the top of the page, and then click **ADD OUTPUT**.</span></span>

### <a name="step-2"></a><span data-ttu-id="fc95f-118">Step 2</span><span class="sxs-lookup"><span data-stu-id="fc95f-118">Step 2</span></span>
<span data-ttu-id="fc95f-119">Select SQL Database and click next.</span><span class="sxs-lookup"><span data-stu-id="fc95f-119">Select SQL Database and click next.</span></span>

![][add-output]

### <a name="step-3"></a><span data-ttu-id="fc95f-120">Step 3</span><span class="sxs-lookup"><span data-stu-id="fc95f-120">Step 3</span></span>
<span data-ttu-id="fc95f-121">Enter the following values on the next page:</span><span class="sxs-lookup"><span data-stu-id="fc95f-121">Enter the following values on the next page:</span></span>

* <span data-ttu-id="fc95f-122">*Output Alias*: Enter a friendly name for this job output.</span><span class="sxs-lookup"><span data-stu-id="fc95f-122">*Output Alias*: Enter a friendly name for this job output.</span></span>
* <span data-ttu-id="fc95f-123">*Subscription*:</span><span class="sxs-lookup"><span data-stu-id="fc95f-123">*Subscription*:</span></span>
  * <span data-ttu-id="fc95f-124">If your SQL Data Warehouse database is in the same subscription as the Stream Analytics job, select Use SQL Database from Current Subscription.</span><span class="sxs-lookup"><span data-stu-id="fc95f-124">If your SQL Data Warehouse database is in the same subscription as the Stream Analytics job, select Use SQL Database from Current Subscription.</span></span>
  * <span data-ttu-id="fc95f-125">If your database is in a different subscription, select Use SQL Database from Another Subscription.</span><span class="sxs-lookup"><span data-stu-id="fc95f-125">If your database is in a different subscription, select Use SQL Database from Another Subscription.</span></span>
* <span data-ttu-id="fc95f-126">*Database*: Specify the name of a destination database.</span><span class="sxs-lookup"><span data-stu-id="fc95f-126">*Database*: Specify the name of a destination database.</span></span>
* <span data-ttu-id="fc95f-127">*Server Name*: Specify the server name for the database you just specified.</span><span class="sxs-lookup"><span data-stu-id="fc95f-127">*Server Name*: Specify the server name for the database you just specified.</span></span> <span data-ttu-id="fc95f-128">You can use the Azure Classic Portal to find this.</span><span class="sxs-lookup"><span data-stu-id="fc95f-128">You can use the Azure Classic Portal to find this.</span></span>

![][server-name]

* <span data-ttu-id="fc95f-129">*User Name*: Specify the user name of an account that has write permissions for the database.</span><span class="sxs-lookup"><span data-stu-id="fc95f-129">*User Name*: Specify the user name of an account that has write permissions for the database.</span></span>
* <span data-ttu-id="fc95f-130">*Password*: Provide the password for the specified user account.</span><span class="sxs-lookup"><span data-stu-id="fc95f-130">*Password*: Provide the password for the specified user account.</span></span>
* <span data-ttu-id="fc95f-131">*Table*: Specify the name of the target table in the database.</span><span class="sxs-lookup"><span data-stu-id="fc95f-131">*Table*: Specify the name of the target table in the database.</span></span>

![][add-database]

### <a name="step-4"></a><span data-ttu-id="fc95f-132">Step 4</span><span class="sxs-lookup"><span data-stu-id="fc95f-132">Step 4</span></span>
<span data-ttu-id="fc95f-133">Click the check button to add this job output and to verify that Stream Analytics can successfully connect to the database.</span><span class="sxs-lookup"><span data-stu-id="fc95f-133">Click the check button to add this job output and to verify that Stream Analytics can successfully connect to the database.</span></span>

![][test-connection]

<span data-ttu-id="fc95f-134">When the connection to the database succeeds, you will see a notification at the bottom of the portal.</span><span class="sxs-lookup"><span data-stu-id="fc95f-134">When the connection to the database succeeds, you will see a notification at the bottom of the portal.</span></span> <span data-ttu-id="fc95f-135">You can click Test Connection at the bottom to test the connection to the database.</span><span class="sxs-lookup"><span data-stu-id="fc95f-135">You can click Test Connection at the bottom to test the connection to the database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fc95f-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="fc95f-136">Next steps</span></span>
<span data-ttu-id="fc95f-137">For an overview of integration, see [SQL Data Warehouse integration overview][SQL Data Warehouse integration overview].</span><span class="sxs-lookup"><span data-stu-id="fc95f-137">For an overview of integration, see [SQL Data Warehouse integration overview][SQL Data Warehouse integration overview].</span></span>

<span data-ttu-id="fc95f-138">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="fc95f-138">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

[add-output]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-integrate-azure-stream-analytics/add-output.png
[server-name]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-integrate-azure-stream-analytics/dw-server-name.png
[add-database]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-integrate-azure-stream-analytics/add-database.png
[test-connection]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-integrate-azure-stream-analytics/test-connection.png

<!--Article references-->

[Introduction to Azure Stream Analytics]: ../stream-analytics/stream-analytics-introduction.md
[Get started using Azure Stream Analytics]: ../stream-analytics/stream-analytics-get-started.md
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Stream Analytics documentation]: http://azure.microsoft.com/documentation/services/stream-analytics/




