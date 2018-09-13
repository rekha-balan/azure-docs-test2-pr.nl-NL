---
title: Use Azure Machine Learning with SQL Data Warehouse | Microsoft Docs
description: Tutorial for using Azure Machine Learning with Azure SQL Data Warehouse for developing solutions.
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: barbkess
editor: ''
ms.assetid: ac6bc731-6add-47a9-b3fe-68996e656f4d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: a4f5694f300652aed10a872d6df7c9f7e2a3149c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554860"
---
# <a name="use-azure-machine-learning-with-sql-data-warehouse"></a><span data-ttu-id="bf140-103">Use Azure Machine Learning with SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="bf140-103">Use Azure Machine Learning with SQL Data Warehouse</span></span>
<span data-ttu-id="bf140-104">Azure Machine Learning is a fully managed predictive analytics service that you can use to create predictive models against your data in SQL Data Warehouse, and then publish as ready-to-consume web services.</span><span class="sxs-lookup"><span data-stu-id="bf140-104">Azure Machine Learning is a fully managed predictive analytics service that you can use to create predictive models against your data in SQL Data Warehouse, and then publish as ready-to-consume web services.</span></span> <span data-ttu-id="bf140-105">You can learn the basics of predictive analytics and machine learning by reading [Introduction to Machine Learning on Azure][Introduction to Machine Learning on Azure].</span><span class="sxs-lookup"><span data-stu-id="bf140-105">You can learn the basics of predictive analytics and machine learning by reading [Introduction to Machine Learning on Azure][Introduction to Machine Learning on Azure].</span></span>  <span data-ttu-id="bf140-106">You can then learn how to create, train, score and test a machine learning model using the [Create experiment tutorial][Create experiment tutorial].</span><span class="sxs-lookup"><span data-stu-id="bf140-106">You can then learn how to create, train, score and test a machine learning model using the [Create experiment tutorial][Create experiment tutorial].</span></span>

<span data-ttu-id="bf140-107">In this article, you will learn how to do the following using the [Azure Machine Learning Studio][Azure Machine Learning Studio]:</span><span class="sxs-lookup"><span data-stu-id="bf140-107">In this article, you will learn how to do the following using the [Azure Machine Learning Studio][Azure Machine Learning Studio]:</span></span>

* <span data-ttu-id="bf140-108">Read data from your database to create, train and score a predictive model</span><span class="sxs-lookup"><span data-stu-id="bf140-108">Read data from your database to create, train and score a predictive model</span></span>
* <span data-ttu-id="bf140-109">Write data to your database</span><span class="sxs-lookup"><span data-stu-id="bf140-109">Write data to your database</span></span>

## <a name="read-data-from-sql-data-warehouse"></a><span data-ttu-id="bf140-110">Read data from SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="bf140-110">Read data from SQL Data Warehouse</span></span>
<span data-ttu-id="bf140-111">We will read data from Product table in the AdventureWorksDW database.</span><span class="sxs-lookup"><span data-stu-id="bf140-111">We will read data from Product table in the AdventureWorksDW database.</span></span>

### <a name="step-1"></a><span data-ttu-id="bf140-112">Step 1</span><span class="sxs-lookup"><span data-stu-id="bf140-112">Step 1</span></span>
<span data-ttu-id="bf140-113">Start a new experiment by clicking +NEW at the bottom of the Machine Learning Studio window, select EXPERIMENT, and then select Blank Experiment.</span><span class="sxs-lookup"><span data-stu-id="bf140-113">Start a new experiment by clicking +NEW at the bottom of the Machine Learning Studio window, select EXPERIMENT, and then select Blank Experiment.</span></span> <span data-ttu-id="bf140-114">Select the default experiment name at the top of the canvas and rename it to something meaningful, for example, Bicycle price prediction.</span><span class="sxs-lookup"><span data-stu-id="bf140-114">Select the default experiment name at the top of the canvas and rename it to something meaningful, for example, Bicycle price prediction.</span></span>

### <a name="step-2"></a><span data-ttu-id="bf140-115">Step 2</span><span class="sxs-lookup"><span data-stu-id="bf140-115">Step 2</span></span>
<span data-ttu-id="bf140-116">Look for the Reader module in the palette of datasets and modules on the left of the experiment canvas.</span><span class="sxs-lookup"><span data-stu-id="bf140-116">Look for the Reader module in the palette of datasets and modules on the left of the experiment canvas.</span></span> <span data-ttu-id="bf140-117">Drag the module to the experiment canvas.</span><span class="sxs-lookup"><span data-stu-id="bf140-117">Drag the module to the experiment canvas.</span></span>
![][drag_reader]

### <a name="step-3"></a><span data-ttu-id="bf140-118">Step 3</span><span class="sxs-lookup"><span data-stu-id="bf140-118">Step 3</span></span>
<span data-ttu-id="bf140-119">Select the Reader module and fill out the properties pane.</span><span class="sxs-lookup"><span data-stu-id="bf140-119">Select the Reader module and fill out the properties pane.</span></span>

1. <span data-ttu-id="bf140-120">Select Azure SQL Database as the Data Source.</span><span class="sxs-lookup"><span data-stu-id="bf140-120">Select Azure SQL Database as the Data Source.</span></span>
2. <span data-ttu-id="bf140-121">Database server name: Type the server name.</span><span class="sxs-lookup"><span data-stu-id="bf140-121">Database server name: Type the server name.</span></span> <span data-ttu-id="bf140-122">You can use the [Azure portal][Azure portal] to find this.</span><span class="sxs-lookup"><span data-stu-id="bf140-122">You can use the [Azure portal][Azure portal] to find this.</span></span>

![][server_name]

1. <span data-ttu-id="bf140-123">Database name: Type the name of a database on the server you just specified.</span><span class="sxs-lookup"><span data-stu-id="bf140-123">Database name: Type the name of a database on the server you just specified.</span></span>
2. <span data-ttu-id="bf140-124">Server user account name:  Type the user name of an account that has access permissions for the database.</span><span class="sxs-lookup"><span data-stu-id="bf140-124">Server user account name:  Type the user name of an account that has access permissions for the database.</span></span>
3. <span data-ttu-id="bf140-125">Server user account password: Provide the password for the specified user account.</span><span class="sxs-lookup"><span data-stu-id="bf140-125">Server user account password: Provide the password for the specified user account.</span></span>
4. <span data-ttu-id="bf140-126">Accept any server certificate: Use this option (less secure) if you want to skip reviewing the site certificate before you read your data.</span><span class="sxs-lookup"><span data-stu-id="bf140-126">Accept any server certificate: Use this option (less secure) if you want to skip reviewing the site certificate before you read your data.</span></span>
5. <span data-ttu-id="bf140-127">Database query: Enter a SQL statement that describes the data you want to read.</span><span class="sxs-lookup"><span data-stu-id="bf140-127">Database query: Enter a SQL statement that describes the data you want to read.</span></span> <span data-ttu-id="bf140-128">In this case, we will read data from Product table using the following query.</span><span class="sxs-lookup"><span data-stu-id="bf140-128">In this case, we will read data from Product table using the following query.</span></span>

```SQL
SELECT ProductKey, EnglishProductName, StandardCost,
        ListPrice, Size, Weight, DaysToManufacture,
        Class, Style, Color
FROM dbo.DimProduct;
```

![][reader_properties]

### <a name="step-4"></a><span data-ttu-id="bf140-129">Step 4</span><span class="sxs-lookup"><span data-stu-id="bf140-129">Step 4</span></span>
1. <span data-ttu-id="bf140-130">Run the experiment by clicking Run under the experiment canvas.</span><span class="sxs-lookup"><span data-stu-id="bf140-130">Run the experiment by clicking Run under the experiment canvas.</span></span>
2. <span data-ttu-id="bf140-131">When the experiment finishes, the Reader module will have a green check mark to indicate that it has completed successfully.</span><span class="sxs-lookup"><span data-stu-id="bf140-131">When the experiment finishes, the Reader module will have a green check mark to indicate that it has completed successfully.</span></span> <span data-ttu-id="bf140-132">Notice also the Finished running status in the upper-right corner.</span><span class="sxs-lookup"><span data-stu-id="bf140-132">Notice also the Finished running status in the upper-right corner.</span></span>

![][run]

1. <span data-ttu-id="bf140-133">To see the imported data, click the output port at the bottom of the automobile dataset and select Visualize.</span><span class="sxs-lookup"><span data-stu-id="bf140-133">To see the imported data, click the output port at the bottom of the automobile dataset and select Visualize.</span></span>

## <a name="create-train-and-score-a-model"></a><span data-ttu-id="bf140-134">Create, train and score a model</span><span class="sxs-lookup"><span data-stu-id="bf140-134">Create, train and score a model</span></span>
<span data-ttu-id="bf140-135">Now you can use this dataset to:</span><span class="sxs-lookup"><span data-stu-id="bf140-135">Now you can use this dataset to:</span></span>

* <span data-ttu-id="bf140-136">Create a Model: Process data and define features</span><span class="sxs-lookup"><span data-stu-id="bf140-136">Create a Model: Process data and define features</span></span>
* <span data-ttu-id="bf140-137">Train the model: Choose and apply a learning algorithm</span><span class="sxs-lookup"><span data-stu-id="bf140-137">Train the model: Choose and apply a learning algorithm</span></span>
* <span data-ttu-id="bf140-138">Score and test the model: Predict new bicycle price</span><span class="sxs-lookup"><span data-stu-id="bf140-138">Score and test the model: Predict new bicycle price</span></span>

![][model]

<span data-ttu-id="bf140-139">To learn more about how to create, train, score and test a machine learning model use the [Create experiment tutorial][Create experiment tutorial].</span><span class="sxs-lookup"><span data-stu-id="bf140-139">To learn more about how to create, train, score and test a machine learning model use the [Create experiment tutorial][Create experiment tutorial].</span></span>

## <a name="write-data-to-azure-sql-data-warehouse"></a><span data-ttu-id="bf140-140">Write data to Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="bf140-140">Write data to Azure SQL Data Warehouse</span></span>
<span data-ttu-id="bf140-141">We will write the result set to ProductPriceForecast table in the AdventureWorksDW database.</span><span class="sxs-lookup"><span data-stu-id="bf140-141">We will write the result set to ProductPriceForecast table in the AdventureWorksDW database.</span></span>

### <a name="step-1"></a><span data-ttu-id="bf140-142">Step 1</span><span class="sxs-lookup"><span data-stu-id="bf140-142">Step 1</span></span>
<span data-ttu-id="bf140-143">Look for the Writer module in the palette of datasets and modules on the left of the experiment canvas.</span><span class="sxs-lookup"><span data-stu-id="bf140-143">Look for the Writer module in the palette of datasets and modules on the left of the experiment canvas.</span></span> <span data-ttu-id="bf140-144">Drag the module to the experiment canvas.</span><span class="sxs-lookup"><span data-stu-id="bf140-144">Drag the module to the experiment canvas.</span></span>

![][drag_writer]

### <a name="step-2"></a><span data-ttu-id="bf140-145">Step 2</span><span class="sxs-lookup"><span data-stu-id="bf140-145">Step 2</span></span>
<span data-ttu-id="bf140-146">Select the Writer module and fill out the properties pane.</span><span class="sxs-lookup"><span data-stu-id="bf140-146">Select the Writer module and fill out the properties pane.</span></span>

1. <span data-ttu-id="bf140-147">Select Azure SQL Database as the Data Destination.</span><span class="sxs-lookup"><span data-stu-id="bf140-147">Select Azure SQL Database as the Data Destination.</span></span>
2. <span data-ttu-id="bf140-148">Database server name: Type the server name.</span><span class="sxs-lookup"><span data-stu-id="bf140-148">Database server name: Type the server name.</span></span> <span data-ttu-id="bf140-149">You can use the [Azure portal][Azure portal] to find this.</span><span class="sxs-lookup"><span data-stu-id="bf140-149">You can use the [Azure portal][Azure portal] to find this.</span></span>
3. <span data-ttu-id="bf140-150">Database name: Type the name of a database on the server you just specified.</span><span class="sxs-lookup"><span data-stu-id="bf140-150">Database name: Type the name of a database on the server you just specified.</span></span>
4. <span data-ttu-id="bf140-151">Server user account name:  Type the user name of an account that has write permissions for the database.</span><span class="sxs-lookup"><span data-stu-id="bf140-151">Server user account name:  Type the user name of an account that has write permissions for the database.</span></span>
5. <span data-ttu-id="bf140-152">Server user account password: Provide the password for the specified user account.</span><span class="sxs-lookup"><span data-stu-id="bf140-152">Server user account password: Provide the password for the specified user account.</span></span>
6. <span data-ttu-id="bf140-153">Accept any server certificate (insecure): Select this option if you don’t want to view the certificate.</span><span class="sxs-lookup"><span data-stu-id="bf140-153">Accept any server certificate (insecure): Select this option if you don’t want to view the certificate.</span></span>
7. <span data-ttu-id="bf140-154">Comma-separated list of columns to be saved: Provide a list of the dataset or result columns that you want to output.</span><span class="sxs-lookup"><span data-stu-id="bf140-154">Comma-separated list of columns to be saved: Provide a list of the dataset or result columns that you want to output.</span></span>
8. <span data-ttu-id="bf140-155">Data table name: Specify the name of the data table.</span><span class="sxs-lookup"><span data-stu-id="bf140-155">Data table name: Specify the name of the data table.</span></span>
9. <span data-ttu-id="bf140-156">Comma-separated list of datatable columns:  Specify the column names to use in the new table.</span><span class="sxs-lookup"><span data-stu-id="bf140-156">Comma-separated list of datatable columns:  Specify the column names to use in the new table.</span></span> <span data-ttu-id="bf140-157">The column names can be different from the ones in the source dataset, but you must list the same number of columns here that you define for the output table.</span><span class="sxs-lookup"><span data-stu-id="bf140-157">The column names can be different from the ones in the source dataset, but you must list the same number of columns here that you define for the output table.</span></span>
10. <span data-ttu-id="bf140-158">Number of rows written per SQL Azure operation: You can configure the number of rows that are written to a SQL database in one operation.</span><span class="sxs-lookup"><span data-stu-id="bf140-158">Number of rows written per SQL Azure operation: You can configure the number of rows that are written to a SQL database in one operation.</span></span>

![][writer_properties]

### <a name="step-3"></a><span data-ttu-id="bf140-159">Step 3</span><span class="sxs-lookup"><span data-stu-id="bf140-159">Step 3</span></span>
1. <span data-ttu-id="bf140-160">Run the experiment by clicking Run under the experiment canvas.</span><span class="sxs-lookup"><span data-stu-id="bf140-160">Run the experiment by clicking Run under the experiment canvas.</span></span>
2. <span data-ttu-id="bf140-161">When the experiment finishes, all modules will have a green check mark to indicate that they completed successfully.</span><span class="sxs-lookup"><span data-stu-id="bf140-161">When the experiment finishes, all modules will have a green check mark to indicate that they completed successfully.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf140-162">Next steps</span><span class="sxs-lookup"><span data-stu-id="bf140-162">Next steps</span></span>
<span data-ttu-id="bf140-163">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="bf140-163">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

[drag_reader]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-reader.png
[server_name]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-integrate-azure-machine-learning/dw-server-name.png
[reader_properties]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-integrate-azure-machine-learning/ml-reader-properties.png
[run]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-integrate-azure-machine-learning/ml-finished-running.png
[model]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-integrate-azure-machine-learning/ml-create-train-score-model.png
[drag_writer]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-writer.png
[writer_properties]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-integrate-azure-machine-learning/ml-writer-properties.png

<!--Article references-->

[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Create experiment tutorial]: https://azure.microsoft.com/documentation/articles/machine-learning-create-experiment/
[Introduction to machine learning on Azure]: https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[Azure Machine Learning Studio]: https://studio.azureml.net/Home
[Azure portal]: https://portal.azure.com/

<!--MSDN references-->

<!--Other Web references-->

[Azure Machine Learning documentation]: http://azure.microsoft.com/documentation/services/machine-learning/







