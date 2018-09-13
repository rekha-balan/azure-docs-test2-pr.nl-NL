---
title: Azure Data Source Wizard for Azure Machine Learning | Microsoft Docs
description: Explains the data source wizard of AML workbench
services: machine-learning
author: cforbe
ms.author: cforbe
manager: mwinkle
ms.reviewer: jmartens, jasonwhowell, mldocs
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.topic: article
ms.date: 09/07/2017
ms.openlocfilehash: c74229504a43179673cc99ccff321b65e3f6ed4f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966428"
---
# <a name="data-source-wizard"></a><span data-ttu-id="7f677-103">Data Source Wizard</span><span class="sxs-lookup"><span data-stu-id="7f677-103">Data Source Wizard</span></span> #

<span data-ttu-id="7f677-104">The Data Source Wizard is a quick and easy way to bring a dataset into Azure ML Workbench without code.</span><span class="sxs-lookup"><span data-stu-id="7f677-104">The Data Source Wizard is a quick and easy way to bring a dataset into Azure ML Workbench without code.</span></span> <span data-ttu-id="7f677-105">It is where you can also select a sample strategy for the dataset and data types for each column.</span><span class="sxs-lookup"><span data-stu-id="7f677-105">It is where you can also select a sample strategy for the dataset and data types for each column.</span></span> 

## <a name="step-1-trigger-the-data-source-wizard"></a><span data-ttu-id="7f677-106">Step 1: Trigger the Data Source Wizard</span><span class="sxs-lookup"><span data-stu-id="7f677-106">Step 1: Trigger the Data Source Wizard</span></span> ## 

<span data-ttu-id="7f677-107">To bring data into a project using the data source wizard.</span><span class="sxs-lookup"><span data-stu-id="7f677-107">To bring data into a project using the data source wizard.</span></span> <span data-ttu-id="7f677-108">Select the **+** button next to the search box in the data view and choose Add Data Source.</span><span class="sxs-lookup"><span data-stu-id="7f677-108">Select the **+** button next to the search box in the data view and choose Add Data Source.</span></span> 

![add data source](media/data-source-wizard/add-data-source.png)

## <a name="step-2-select-where-data-is-stored"></a><span data-ttu-id="7f677-110">Step 2: Select where data is stored</span><span class="sxs-lookup"><span data-stu-id="7f677-110">Step 2: Select where data is stored</span></span> ##
<span data-ttu-id="7f677-111">First, specify how your data is currently in.</span><span class="sxs-lookup"><span data-stu-id="7f677-111">First, specify how your data is currently in.</span></span> <span data-ttu-id="7f677-112">It could be stored in a flat file or a directory, a parquet file, an Excel file, or a database.</span><span class="sxs-lookup"><span data-stu-id="7f677-112">It could be stored in a flat file or a directory, a parquet file, an Excel file, or a database.</span></span> <span data-ttu-id="7f677-113">For more information, see [Supported Data Sources](data-prep-appendix2-supported-data-sources.md).</span><span class="sxs-lookup"><span data-stu-id="7f677-113">For more information, see [Supported Data Sources](data-prep-appendix2-supported-data-sources.md).</span></span>

![step 1](media/data-source-wizard/step1.png)

## <a name="step-3-select-data-file"></a><span data-ttu-id="7f677-115">Step 3: Select data file</span><span class="sxs-lookup"><span data-stu-id="7f677-115">Step 3: Select data file</span></span> ##
<span data-ttu-id="7f677-116">For a file/directory, specify the file path.</span><span class="sxs-lookup"><span data-stu-id="7f677-116">For a file/directory, specify the file path.</span></span> <span data-ttu-id="7f677-117">Choose from the dropdown the location of the data – it could be a local file path or Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="7f677-117">Choose from the dropdown the location of the data – it could be a local file path or Azure Blob Storage.</span></span> 

<span data-ttu-id="7f677-118">Specify the path by typing it in or clicking on the **Browse…**</span><span class="sxs-lookup"><span data-stu-id="7f677-118">Specify the path by typing it in or clicking on the **Browse…**</span></span> <span data-ttu-id="7f677-119">button to browse for it.</span><span class="sxs-lookup"><span data-stu-id="7f677-119">button to browse for it.</span></span> <span data-ttu-id="7f677-120">You can browse for a directory, or one or more files.</span><span class="sxs-lookup"><span data-stu-id="7f677-120">You can browse for a directory, or one or more files.</span></span>

<span data-ttu-id="7f677-121">Click **Finish** to accept the defaults for the rest of steps or Next to proceed to the next step.</span><span class="sxs-lookup"><span data-stu-id="7f677-121">Click **Finish** to accept the defaults for the rest of steps or Next to proceed to the next step.</span></span>


![step 4](media/data-source-wizard/step2.png)

## <a name="step-4-choose-file-parameters"></a><span data-ttu-id="7f677-123">Step 4: Choose file parameters</span><span class="sxs-lookup"><span data-stu-id="7f677-123">Step 4: Choose file parameters</span></span> ##

<span data-ttu-id="7f677-124">The Data Source Wizard can automatically detect the file type, separators, and encoding.</span><span class="sxs-lookup"><span data-stu-id="7f677-124">The Data Source Wizard can automatically detect the file type, separators, and encoding.</span></span> <span data-ttu-id="7f677-125">It would also show an example of what the data will look like.</span><span class="sxs-lookup"><span data-stu-id="7f677-125">It would also show an example of what the data will look like.</span></span> <span data-ttu-id="7f677-126">You can also change any of these parameters manually.</span><span class="sxs-lookup"><span data-stu-id="7f677-126">You can also change any of these parameters manually.</span></span> 

![step 5](media/data-source-wizard/step3.png)

## <a name="step-5-set-data-types-for-columns"></a><span data-ttu-id="7f677-128">Step 5: Set data types for columns</span><span class="sxs-lookup"><span data-stu-id="7f677-128">Step 5: Set data types for columns</span></span> ##

<span data-ttu-id="7f677-129">The Data Source Wizard automatically detects the data types of the dataset's columns.</span><span class="sxs-lookup"><span data-stu-id="7f677-129">The Data Source Wizard automatically detects the data types of the dataset's columns.</span></span> <span data-ttu-id="7f677-130">If it misses one, or you wish to enforce a data type, you can manually change the data type.</span><span class="sxs-lookup"><span data-stu-id="7f677-130">If it misses one, or you wish to enforce a data type, you can manually change the data type.</span></span> <span data-ttu-id="7f677-131">The **SAMPLE OUTPUT DATA** column shows you examples of what the data look like.</span><span class="sxs-lookup"><span data-stu-id="7f677-131">The **SAMPLE OUTPUT DATA** column shows you examples of what the data look like.</span></span>

<span data-ttu-id="7f677-132">For columns that Data Prep infers to contain dates, you may be prompted to select the order of month and day in the date format.</span><span class="sxs-lookup"><span data-stu-id="7f677-132">For columns that Data Prep infers to contain dates, you may be prompted to select the order of month and day in the date format.</span></span> <span data-ttu-id="7f677-133">For example, 1/2/2013 could represent January 2nd (for this, select *Day-Month*) or Feburary 1st (select *Month-Day*).</span><span class="sxs-lookup"><span data-stu-id="7f677-133">For example, 1/2/2013 could represent January 2nd (for this, select *Day-Month*) or Feburary 1st (select *Month-Day*).</span></span>

![step 6](media/data-source-wizard/step4.png)

## <a name="step-6-choose-sampling-strategy-for-data"></a><span data-ttu-id="7f677-135">Step 6: Choose sampling strategy for data</span><span class="sxs-lookup"><span data-stu-id="7f677-135">Step 6: Choose sampling strategy for data</span></span> ##

<span data-ttu-id="7f677-136">You can specify one or more sampling strategies for the dataset, and choose one as the active strategy.</span><span class="sxs-lookup"><span data-stu-id="7f677-136">You can specify one or more sampling strategies for the dataset, and choose one as the active strategy.</span></span> <span data-ttu-id="7f677-137">The default is to load the Top 10000 rows.</span><span class="sxs-lookup"><span data-stu-id="7f677-137">The default is to load the Top 10000 rows.</span></span> <span data-ttu-id="7f677-138">You can edit this sample by clicking on the **Edit** button in the toolbar or add a new strategy by clicking on +New.</span><span class="sxs-lookup"><span data-stu-id="7f677-138">You can edit this sample by clicking on the **Edit** button in the toolbar or add a new strategy by clicking on +New.</span></span> <span data-ttu-id="7f677-139">The strategies that are currently support are</span><span class="sxs-lookup"><span data-stu-id="7f677-139">The strategies that are currently support are</span></span>

-     <span data-ttu-id="7f677-140">Top number of rows</span><span class="sxs-lookup"><span data-stu-id="7f677-140">Top number of rows</span></span>
-     <span data-ttu-id="7f677-141">Random number of rows</span><span class="sxs-lookup"><span data-stu-id="7f677-141">Random number of rows</span></span>
-     <span data-ttu-id="7f677-142">Random percentage of rows</span><span class="sxs-lookup"><span data-stu-id="7f677-142">Random percentage of rows</span></span>
-     <span data-ttu-id="7f677-143">Full file</span><span class="sxs-lookup"><span data-stu-id="7f677-143">Full file</span></span>

<span data-ttu-id="7f677-144">You can specify as many sampling strategies as you want, but there is only one that can be set to active when preparing your data.</span><span class="sxs-lookup"><span data-stu-id="7f677-144">You can specify as many sampling strategies as you want, but there is only one that can be set to active when preparing your data.</span></span> <span data-ttu-id="7f677-145">You can set any strategy to be the active by selecting the strategy and click Set as Active  in the toolbar.</span><span class="sxs-lookup"><span data-stu-id="7f677-145">You can set any strategy to be the active by selecting the strategy and click Set as Active  in the toolbar.</span></span>

<span data-ttu-id="7f677-146">Depending on where the data comes from, some sample strategies may not be supported.</span><span class="sxs-lookup"><span data-stu-id="7f677-146">Depending on where the data comes from, some sample strategies may not be supported.</span></span> <span data-ttu-id="7f677-147">For more information about sampling, look at the sampling section in [this document](data-prep-user-guide.md)</span><span class="sxs-lookup"><span data-stu-id="7f677-147">For more information about sampling, look at the sampling section in [this document](data-prep-user-guide.md)</span></span> 

![step 6](media/data-source-wizard/step5.png)

## <a name="step-7-path-column-handling"></a><span data-ttu-id="7f677-149">Step 7: Path column handling</span><span class="sxs-lookup"><span data-stu-id="7f677-149">Step 7: Path column handling</span></span> ##

<span data-ttu-id="7f677-150">If the file path includes important data, you can choose to include it as the first column in the dataset.</span><span class="sxs-lookup"><span data-stu-id="7f677-150">If the file path includes important data, you can choose to include it as the first column in the dataset.</span></span> <span data-ttu-id="7f677-151">This option would be helpful if you are bringing in multiple files.</span><span class="sxs-lookup"><span data-stu-id="7f677-151">This option would be helpful if you are bringing in multiple files.</span></span> <span data-ttu-id="7f677-152">Otherwise, you can choose to not include it.</span><span class="sxs-lookup"><span data-stu-id="7f677-152">Otherwise, you can choose to not include it.</span></span>

![step 7](media/data-source-wizard/step6.png)

<span data-ttu-id="7f677-154">After clicking Finish, a new data source will be added to the project.</span><span class="sxs-lookup"><span data-stu-id="7f677-154">After clicking Finish, a new data source will be added to the project.</span></span> <span data-ttu-id="7f677-155">You can find it under the Data Sources group in the Data View, or as a dsource file in the **File View**.</span><span class="sxs-lookup"><span data-stu-id="7f677-155">You can find it under the Data Sources group in the Data View, or as a dsource file in the **File View**.</span></span>
