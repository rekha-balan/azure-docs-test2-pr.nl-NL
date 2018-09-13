---
title: How to write queries in Stream Analytics | Microsoft Docs
description: Write queries in Stream Analytics and query data | learning path segment.
keywords: how to write queries, query data, write a query, writing queries
documentationcenter: ''
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0e9cdadd-0ee0-4bee-b65b-4a06fb863c95
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 8d43ef1f281179ff5cdd8b60c32c094a54919c8e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549077"
---
# <a name="how-to-write-queries-in-stream-analytics"></a><span data-ttu-id="0ab7c-104">How to write queries in Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0ab7c-104">How to write queries in Stream Analytics</span></span>
<span data-ttu-id="0ab7c-105">Writing queries for stream processing logic in Azure Stream Analytics is implemented as a "standing query" that is defined before a job starts and executed on data as it reaches the job.</span><span class="sxs-lookup"><span data-stu-id="0ab7c-105">Writing queries for stream processing logic in Azure Stream Analytics is implemented as a "standing query" that is defined before a job starts and executed on data as it reaches the job.</span></span> <span data-ttu-id="0ab7c-106">The data transformation is expressed in a SQL-like query language, which is largely a subset of T-SQL with some added language extensions like [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) used to express temporal semantics.</span><span class="sxs-lookup"><span data-stu-id="0ab7c-106">The data transformation is expressed in a SQL-like query language, which is largely a subset of T-SQL with some added language extensions like [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) used to express temporal semantics.</span></span>

## <a name="writing-queries"></a><span data-ttu-id="0ab7c-107">Writing Queries:</span><span class="sxs-lookup"><span data-stu-id="0ab7c-107">Writing Queries:</span></span>
1. <span data-ttu-id="0ab7c-108">In your Stream Analytics Job in the Azure Management portal, click **Query**.</span><span class="sxs-lookup"><span data-stu-id="0ab7c-108">In your Stream Analytics Job in the Azure Management portal, click **Query**.</span></span>
   
    ![Select Query](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-write-queries/1-stream-analytics-write-queries.png)  
   
    <span data-ttu-id="0ab7c-110">In the Azure Portal, click **Query**.</span><span class="sxs-lookup"><span data-stu-id="0ab7c-110">In the Azure Portal, click **Query**.</span></span>
   
    ![Select Query Preview](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-write-queries/query-preview-portal.png)  
2. <span data-ttu-id="0ab7c-112">New jobs have a query template to help get you started.</span><span class="sxs-lookup"><span data-stu-id="0ab7c-112">New jobs have a query template to help get you started.</span></span> <span data-ttu-id="0ab7c-113">The query template performs a "pass-through" query that projects all fields from input events into the output.</span><span class="sxs-lookup"><span data-stu-id="0ab7c-113">The query template performs a "pass-through" query that projects all fields from input events into the output.</span></span>  
   
   * <span data-ttu-id="0ab7c-114">If you have defined at least one input and output for your job, you can replace the placeholder "[YourOutputAlias]" and "[YourInputAlias]" fields with the aliases of the input and output that you wish use first.</span><span class="sxs-lookup"><span data-stu-id="0ab7c-114">If you have defined at least one input and output for your job, you can replace the placeholder "[YourOutputAlias]" and "[YourInputAlias]" fields with the aliases of the input and output that you wish use first.</span></span> <span data-ttu-id="0ab7c-115">In addition, you can still author and test your query in the Azure Classic Portal without defining inputs and outputs on the job.</span><span class="sxs-lookup"><span data-stu-id="0ab7c-115">In addition, you can still author and test your query in the Azure Classic Portal without defining inputs and outputs on the job.</span></span>
   * <span data-ttu-id="0ab7c-116">If you wish to perform more processing than a simple pass-through, you can edit the query definition.</span><span class="sxs-lookup"><span data-stu-id="0ab7c-116">If you wish to perform more processing than a simple pass-through, you can edit the query definition.</span></span> <span data-ttu-id="0ab7c-117">To get started with query authoring, take a look at some common query patterns are captured [here](stream-analytics-stream-analytics-query-patterns.md).</span><span class="sxs-lookup"><span data-stu-id="0ab7c-117">To get started with query authoring, take a look at some common query patterns are captured [here](stream-analytics-stream-analytics-query-patterns.md).</span></span>  
   
   ![Query data Window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-write-queries/2-stream-analytics-write-queries.png)  

## <a name="to-validate-query-data-is-working"></a><span data-ttu-id="0ab7c-119">To validate query data is working:</span><span class="sxs-lookup"><span data-stu-id="0ab7c-119">To validate query data is working:</span></span>
<span data-ttu-id="0ab7c-120">You can test that your query behaves as expected by running it in the browser over one or more local JSON files containing test data.</span><span class="sxs-lookup"><span data-stu-id="0ab7c-120">You can test that your query behaves as expected by running it in the browser over one or more local JSON files containing test data.</span></span> <span data-ttu-id="0ab7c-121">This will not start the job or have any billing implications.</span><span class="sxs-lookup"><span data-stu-id="0ab7c-121">This will not start the job or have any billing implications.</span></span>

> [!NOTE]
> <span data-ttu-id="0ab7c-122">Currently in-browser query testing is not supported in the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="0ab7c-122">Currently in-browser query testing is not supported in the Azure Portal.</span></span>  
> 
> 

1. <span data-ttu-id="0ab7c-123">Make sure that there are no errors in the query (otherwise the Test button will be disabled) and then click the Test button.</span><span class="sxs-lookup"><span data-stu-id="0ab7c-123">Make sure that there are no errors in the query (otherwise the Test button will be disabled) and then click the Test button.</span></span>  
   
   ![Query data Test](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-write-queries/3-stream-analytics-write-queries.png)  
2. <span data-ttu-id="0ab7c-125">You will be prompted to specify files for each of the inputs referenced in the query.</span><span class="sxs-lookup"><span data-stu-id="0ab7c-125">You will be prompted to specify files for each of the inputs referenced in the query.</span></span> <span data-ttu-id="0ab7c-126">In this example, the template query is left as-is, so the dialog is prompting for an input named "yourinputalias".</span><span class="sxs-lookup"><span data-stu-id="0ab7c-126">In this example, the template query is left as-is, so the dialog is prompting for an input named "yourinputalias".</span></span>  
   
   ![Test Data query](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-write-queries/4-stream-analytics-write-queries.png)  
3. <span data-ttu-id="0ab7c-128">Browse to a test file.</span><span class="sxs-lookup"><span data-stu-id="0ab7c-128">Browse to a test file.</span></span> <span data-ttu-id="0ab7c-129">Several sample files are available on [github](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) and you can also retrieve sample data from your own data stream inputs via the Sample Data function on the inputs tab.</span><span class="sxs-lookup"><span data-stu-id="0ab7c-129">Several sample files are available on [github](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) and you can also retrieve sample data from your own data stream inputs via the Sample Data function on the inputs tab.</span></span>  
   
   ![Query Input](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-write-queries/5-stream-analytics-write-queries.png)  
4. <span data-ttu-id="0ab7c-131">After closing the dialog, your query will be run over the test data and you will see the results at the bottom of the Query page.</span><span class="sxs-lookup"><span data-stu-id="0ab7c-131">After closing the dialog, your query will be run over the test data and you will see the results at the bottom of the Query page.</span></span>  
   
   ![Query Summary](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-write-queries/6-stream-analytics-write-queries.png)  

## <a name="get-help"></a><span data-ttu-id="0ab7c-133">Get help</span><span class="sxs-lookup"><span data-stu-id="0ab7c-133">Get help</span></span>
<span data-ttu-id="0ab7c-134">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="0ab7c-134">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ab7c-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="0ab7c-135">Next steps</span></span>
* [<span data-ttu-id="0ab7c-136">Introduction to Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0ab7c-136">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="0ab7c-137">Get started using Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0ab7c-137">Get started using Azure Stream Analytics</span></span>](stream-analytics-get-started.md)
* [<span data-ttu-id="0ab7c-138">Scale Azure Stream Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="0ab7c-138">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="0ab7c-139">Azure Stream Analytics Query Language Reference</span><span class="sxs-lookup"><span data-stu-id="0ab7c-139">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="0ab7c-140">Azure Stream Analytics Management REST API Reference</span><span class="sxs-lookup"><span data-stu-id="0ab7c-140">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)








