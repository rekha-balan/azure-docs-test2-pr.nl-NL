---
title: Import data into Machine Learning Studio | Microsoft Docs
description: How to import your data into Azure Machine Learning Studio from various data sources. Learn what data types and data formats are supported.
keywords: import data,data format,data types,data sources,training data
services: machine-learning
documentationcenter: ''
author: heatherbshapiro
ms.author: hshapiro
manager: hjerez
editor: cgronlun
ms.assetid: c194ee3b-838c-4efe-bb2a-c1d052326216
ms.service: machine-learning
ms.component: studio
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/29/2017
ms.openlocfilehash: a5750555802489b41b007831164767beb953ebc4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969111"
---
# <a name="import-your-training-data-into-azure-machine-learning-studio-from-various-data-sources"></a><span data-ttu-id="4378f-105">Import your training data into Azure Machine Learning Studio from various data sources</span><span class="sxs-lookup"><span data-stu-id="4378f-105">Import your training data into Azure Machine Learning Studio from various data sources</span></span>
<span data-ttu-id="4378f-106">To use your own data in Machine Learning Studio to develop and train a predictive analytics solution, you can:</span><span class="sxs-lookup"><span data-stu-id="4378f-106">To use your own data in Machine Learning Studio to develop and train a predictive analytics solution, you can:</span></span> 

* <span data-ttu-id="4378f-107">upload data from a **local file** ahead of time from your hard drive to create a dataset module in your workspace</span><span class="sxs-lookup"><span data-stu-id="4378f-107">upload data from a **local file** ahead of time from your hard drive to create a dataset module in your workspace</span></span>
* <span data-ttu-id="4378f-108">access data from one of several **online data sources** while your experiment is running using the [Import Data][import-data] module</span><span class="sxs-lookup"><span data-stu-id="4378f-108">access data from one of several **online data sources** while your experiment is running using the [Import Data][import-data] module</span></span> 
* <span data-ttu-id="4378f-109">use data from another Azure Machine learning **experiment** saved as a dataset</span><span class="sxs-lookup"><span data-stu-id="4378f-109">use data from another Azure Machine learning **experiment** saved as a dataset</span></span>
* <span data-ttu-id="4378f-110">use data from an on-premises **SQL Server database**</span><span class="sxs-lookup"><span data-stu-id="4378f-110">use data from an on-premises **SQL Server database**</span></span>

<span data-ttu-id="4378f-111">Each of these options is described in one of the topics on the menu below.</span><span class="sxs-lookup"><span data-stu-id="4378f-111">Each of these options is described in one of the topics on the menu below.</span></span> <span data-ttu-id="4378f-112">These topics show you how to import data from these various data sources to use in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="4378f-112">These topics show you how to import data from these various data sources to use in Machine Learning Studio.</span></span> 

[!INCLUDE [import-data-into-aml-studio-selector](../../../includes/machine-learning-import-data-into-aml-studio.md)]

> [!NOTE]
> <span data-ttu-id="4378f-113">There are a number of sample datasets available in Machine Learning Studio that you can use for training data.</span><span class="sxs-lookup"><span data-stu-id="4378f-113">There are a number of sample datasets available in Machine Learning Studio that you can use for training data.</span></span> <span data-ttu-id="4378f-114">For information on these, see [Use the sample datasets in Azure Machine Learning Studio](use-sample-datasets.md)).</span><span class="sxs-lookup"><span data-stu-id="4378f-114">For information on these, see [Use the sample datasets in Azure Machine Learning Studio](use-sample-datasets.md)).</span></span>
> 
> 

<span data-ttu-id="4378f-115">This introductory topic also discusses how to get data ready for use in Machine Learning Studio and describes which data formats and data types are supported.</span><span class="sxs-lookup"><span data-stu-id="4378f-115">This introductory topic also discusses how to get data ready for use in Machine Learning Studio and describes which data formats and data types are supported.</span></span> 

> [!INCLUDE [machine-learning-free-trial](../../../includes/machine-learning-free-trial.md)]
> 
> 

## <a name="get-data-ready-for-use-in-azure-machine-learning-studio"></a><span data-ttu-id="4378f-116">Get data ready for use in Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="4378f-116">Get data ready for use in Azure Machine Learning Studio</span></span>
<span data-ttu-id="4378f-117">Machine Learning Studio is designed to work with rectangular or tabular data, such as text data that's delimited or structured data from a database, though in some circumstances non-rectangular data may be used.</span><span class="sxs-lookup"><span data-stu-id="4378f-117">Machine Learning Studio is designed to work with rectangular or tabular data, such as text data that's delimited or structured data from a database, though in some circumstances non-rectangular data may be used.</span></span>

<span data-ttu-id="4378f-118">It's best if your data is relatively clean.</span><span class="sxs-lookup"><span data-stu-id="4378f-118">It's best if your data is relatively clean.</span></span> <span data-ttu-id="4378f-119">That is, you'll want to take care of issues such as unquoted strings before you upload the data into your experiment.</span><span class="sxs-lookup"><span data-stu-id="4378f-119">That is, you'll want to take care of issues such as unquoted strings before you upload the data into your experiment.</span></span>

<span data-ttu-id="4378f-120">However, there are modules available in Machine Learning Studio that enable some manipulation of data within your experiment.</span><span class="sxs-lookup"><span data-stu-id="4378f-120">However, there are modules available in Machine Learning Studio that enable some manipulation of data within your experiment.</span></span> <span data-ttu-id="4378f-121">Depending on the machine learning algorithms you'll be using, you may need to decide how you'll handle data structural issues such as missing values and sparse data, and there are modules that can help with that.</span><span class="sxs-lookup"><span data-stu-id="4378f-121">Depending on the machine learning algorithms you'll be using, you may need to decide how you'll handle data structural issues such as missing values and sparse data, and there are modules that can help with that.</span></span> <span data-ttu-id="4378f-122">Look in the **Data Transformation** section of the module palette for modules that perform these functions.</span><span class="sxs-lookup"><span data-stu-id="4378f-122">Look in the **Data Transformation** section of the module palette for modules that perform these functions.</span></span>

<span data-ttu-id="4378f-123">At any point in your experiment you can view or download the data that's produced by a module by clicking the output port.</span><span class="sxs-lookup"><span data-stu-id="4378f-123">At any point in your experiment you can view or download the data that's produced by a module by clicking the output port.</span></span> <span data-ttu-id="4378f-124">Depending on the module, there may be different download options available, or you may be able to visualize the data within your web browser in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="4378f-124">Depending on the module, there may be different download options available, or you may be able to visualize the data within your web browser in Machine Learning Studio.</span></span>

## <a name="data-formats-and-data-types-supported"></a><span data-ttu-id="4378f-125">Data formats and data types supported</span><span class="sxs-lookup"><span data-stu-id="4378f-125">Data formats and data types supported</span></span>
<span data-ttu-id="4378f-126">You can import a number of data types into your experiment, depending on what mechanism you use to import data and where it's coming from:</span><span class="sxs-lookup"><span data-stu-id="4378f-126">You can import a number of data types into your experiment, depending on what mechanism you use to import data and where it's coming from:</span></span>

* <span data-ttu-id="4378f-127">Plain text (.txt)</span><span class="sxs-lookup"><span data-stu-id="4378f-127">Plain text (.txt)</span></span>
* <span data-ttu-id="4378f-128">Comma-separated values (CSV) with a header (.csv) or without (.nh.csv)</span><span class="sxs-lookup"><span data-stu-id="4378f-128">Comma-separated values (CSV) with a header (.csv) or without (.nh.csv)</span></span>
* <span data-ttu-id="4378f-129">Tab-separated values (TSV) with a header (.tsv) or without (.nh.tsv)</span><span class="sxs-lookup"><span data-stu-id="4378f-129">Tab-separated values (TSV) with a header (.tsv) or without (.nh.tsv)</span></span>
* <span data-ttu-id="4378f-130">Excel file</span><span class="sxs-lookup"><span data-stu-id="4378f-130">Excel file</span></span>
* <span data-ttu-id="4378f-131">Azure table</span><span class="sxs-lookup"><span data-stu-id="4378f-131">Azure table</span></span>
* <span data-ttu-id="4378f-132">Hive table</span><span class="sxs-lookup"><span data-stu-id="4378f-132">Hive table</span></span>
* <span data-ttu-id="4378f-133">SQL database table</span><span class="sxs-lookup"><span data-stu-id="4378f-133">SQL database table</span></span>
* <span data-ttu-id="4378f-134">OData values</span><span class="sxs-lookup"><span data-stu-id="4378f-134">OData values</span></span>
* <span data-ttu-id="4378f-135">SVMLight data (.svmlight) (see the [SVMLight definition](http://svmlight.joachims.org/) for format information)</span><span class="sxs-lookup"><span data-stu-id="4378f-135">SVMLight data (.svmlight) (see the [SVMLight definition](http://svmlight.joachims.org/) for format information)</span></span>
* <span data-ttu-id="4378f-136">Attribute Relation File Format (ARFF) data (.arff) (see the [ARFF definition](http://weka.wikispaces.com/ARFF) for format information)</span><span class="sxs-lookup"><span data-stu-id="4378f-136">Attribute Relation File Format (ARFF) data (.arff) (see the [ARFF definition](http://weka.wikispaces.com/ARFF) for format information)</span></span>
* <span data-ttu-id="4378f-137">Zip file (.zip)</span><span class="sxs-lookup"><span data-stu-id="4378f-137">Zip file (.zip)</span></span>
* <span data-ttu-id="4378f-138">R object or workspace file (.RData)</span><span class="sxs-lookup"><span data-stu-id="4378f-138">R object or workspace file (.RData)</span></span>

<span data-ttu-id="4378f-139">If you import data in a format such as ARFF that includes metadata, Machine Learning Studio uses this metadata to define the heading and data type of each column.</span><span class="sxs-lookup"><span data-stu-id="4378f-139">If you import data in a format such as ARFF that includes metadata, Machine Learning Studio uses this metadata to define the heading and data type of each column.</span></span>

<span data-ttu-id="4378f-140">If you import data such as TSV or CSV format that doesn't include this metadata, Machine Learning Studio infers the data type for each column by sampling the data.</span><span class="sxs-lookup"><span data-stu-id="4378f-140">If you import data such as TSV or CSV format that doesn't include this metadata, Machine Learning Studio infers the data type for each column by sampling the data.</span></span> <span data-ttu-id="4378f-141">If the data also doesn't have column headings, Machine Learning Studio provides default names.</span><span class="sxs-lookup"><span data-stu-id="4378f-141">If the data also doesn't have column headings, Machine Learning Studio provides default names.</span></span>

<span data-ttu-id="4378f-142">You can explicitly specify or change the headings and data types for columns using the [Edit Metadata][edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="4378f-142">You can explicitly specify or change the headings and data types for columns using the [Edit Metadata][edit-metadata].</span></span>

<span data-ttu-id="4378f-143">The following **data types** are recognized by Machine Learning Studio:</span><span class="sxs-lookup"><span data-stu-id="4378f-143">The following **data types** are recognized by Machine Learning Studio:</span></span>

* <span data-ttu-id="4378f-144">String</span><span class="sxs-lookup"><span data-stu-id="4378f-144">String</span></span>
* <span data-ttu-id="4378f-145">Integer</span><span class="sxs-lookup"><span data-stu-id="4378f-145">Integer</span></span>
* <span data-ttu-id="4378f-146">Double</span><span class="sxs-lookup"><span data-stu-id="4378f-146">Double</span></span>
* <span data-ttu-id="4378f-147">Boolean</span><span class="sxs-lookup"><span data-stu-id="4378f-147">Boolean</span></span>
* <span data-ttu-id="4378f-148">DateTime</span><span class="sxs-lookup"><span data-stu-id="4378f-148">DateTime</span></span>
* <span data-ttu-id="4378f-149">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="4378f-149">TimeSpan</span></span>

<span data-ttu-id="4378f-150">Machine Learning Studio uses an internal data type called ***Data Table*** to pass data between modules.</span><span class="sxs-lookup"><span data-stu-id="4378f-150">Machine Learning Studio uses an internal data type called ***Data Table*** to pass data between modules.</span></span> <span data-ttu-id="4378f-151">You can explicitly convert your data into Data Table format using the [Convert to Dataset][convert-to-dataset] module.</span><span class="sxs-lookup"><span data-stu-id="4378f-151">You can explicitly convert your data into Data Table format using the [Convert to Dataset][convert-to-dataset] module.</span></span>

<span data-ttu-id="4378f-152">Any module that accepts formats other than Data Table will convert the data to Data Table silently before passing it to the next module.</span><span class="sxs-lookup"><span data-stu-id="4378f-152">Any module that accepts formats other than Data Table will convert the data to Data Table silently before passing it to the next module.</span></span>

<span data-ttu-id="4378f-153">If necessary, you can convert Data Table format back into CSV, TSV, ARFF, or SVMLight format using other conversion modules.</span><span class="sxs-lookup"><span data-stu-id="4378f-153">If necessary, you can convert Data Table format back into CSV, TSV, ARFF, or SVMLight format using other conversion modules.</span></span>
<span data-ttu-id="4378f-154">Look in the **Data Format Conversions** section of the module palette for modules that perform these functions.</span><span class="sxs-lookup"><span data-stu-id="4378f-154">Look in the **Data Format Conversions** section of the module palette for modules that perform these functions.</span></span>

<!-- Module References -->
[convert-to-dataset]: https://msdn.microsoft.com/library/azure/72bf58e0-fc87-4bb1-9704-f1805003b975/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
