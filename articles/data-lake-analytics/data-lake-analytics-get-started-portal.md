---
title: Get Started with Azure Data Lake Analytics using Azure portal | Microsoft Docs
description: 'Learn how to use the Azure portal to create a Data Lake Analytics account, create a Data Lake Analytics job using U-SQL, and submit the job. '
services: data-lake-analytics
documentationcenter: ''
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: b1584d16-e0d2-4019-ad1f-f04be8c5b430
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/21/2017
ms.author: edmaca
ms.openlocfilehash: 98b521e9a77c14e5b7d63d3feac06332cf71d522
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554982"
---
# <a name="tutorial-get-started-with-azure-data-lake-analytics-using-azure-portal"></a><span data-ttu-id="4a70b-103">Tutorial: get started with Azure Data Lake Analytics using Azure portal</span><span class="sxs-lookup"><span data-stu-id="4a70b-103">Tutorial: get started with Azure Data Lake Analytics using Azure portal</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="4a70b-104">Learn how to use the Azure portal to create Azure Data Lake Analytics accounts, define jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs to the Data Lake Analytics service.</span><span class="sxs-lookup"><span data-stu-id="4a70b-104">Learn how to use the Azure portal to create Azure Data Lake Analytics accounts, define jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs to the Data Lake Analytics service.</span></span> <span data-ttu-id="4a70b-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4a70b-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

<span data-ttu-id="4a70b-106">In this tutorial, you will develop a job that reads a tab separated values (TSV) file and converts it into a comma separated values (CSV) file.</span><span class="sxs-lookup"><span data-stu-id="4a70b-106">In this tutorial, you will develop a job that reads a tab separated values (TSV) file and converts it into a comma separated values (CSV) file.</span></span> <span data-ttu-id="4a70b-107">To go through the same tutorial using other supported tools, click the tabs on the top of this section.</span><span class="sxs-lookup"><span data-stu-id="4a70b-107">To go through the same tutorial using other supported tools, click the tabs on the top of this section.</span></span> <span data-ttu-id="4a70b-108">Once your first job succeeds, you can start to write more complex data transformations with U-SQL.</span><span class="sxs-lookup"><span data-stu-id="4a70b-108">Once your first job succeeds, you can start to write more complex data transformations with U-SQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4a70b-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4a70b-109">Prerequisites</span></span>
<span data-ttu-id="4a70b-110">Before you begin this tutorial, you must have the following items:</span><span class="sxs-lookup"><span data-stu-id="4a70b-110">Before you begin this tutorial, you must have the following items:</span></span>

* <span data-ttu-id="4a70b-111">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="4a70b-111">**An Azure subscription**.</span></span> <span data-ttu-id="4a70b-112">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4a70b-112">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="create-data-lake-analytics-account"></a><span data-ttu-id="4a70b-113">Create Data Lake Analytics account</span><span class="sxs-lookup"><span data-stu-id="4a70b-113">Create Data Lake Analytics account</span></span>
<span data-ttu-id="4a70b-114">You must have a Data Lake Analytics account before you can run any jobs.</span><span class="sxs-lookup"><span data-stu-id="4a70b-114">You must have a Data Lake Analytics account before you can run any jobs.</span></span>

<span data-ttu-id="4a70b-115">Each Data Lake Analytics account has an Azure Data Lake Store account dependency.</span><span class="sxs-lookup"><span data-stu-id="4a70b-115">Each Data Lake Analytics account has an Azure Data Lake Store account dependency.</span></span>  <span data-ttu-id="4a70b-116">This account is referred as the default Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="4a70b-116">This account is referred as the default Data Lake Store account.</span></span>  <span data-ttu-id="4a70b-117">You can create the Data Lake Store account beforehand or when you create your Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="4a70b-117">You can create the Data Lake Store account beforehand or when you create your Data Lake Analytics account.</span></span> <span data-ttu-id="4a70b-118">In this tutorial, you will create the Data Lake Store account with the Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="4a70b-118">In this tutorial, you will create the Data Lake Store account with the Data Lake Analytics account.</span></span>

<span data-ttu-id="4a70b-119">**Create a Data Lake Analytics account**</span><span class="sxs-lookup"><span data-stu-id="4a70b-119">**Create a Data Lake Analytics account**</span></span>

1. <span data-ttu-id="4a70b-120">Sign on to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4a70b-120">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4a70b-121">Click **New**, click **Intelligence + analytics**, and then click **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="4a70b-121">Click **New**, click **Intelligence + analytics**, and then click **Data Lake Analytics**.</span></span>
3. <span data-ttu-id="4a70b-122">Type or select the following values:</span><span class="sxs-lookup"><span data-stu-id="4a70b-122">Type or select the following values:</span></span>

    ![Azure Data Lake Analytics portal blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-get-started-portal/data-lake-analytics-portal-create-adla.png)

   * <span data-ttu-id="4a70b-124">**Name**: Name your Data Lake Analytics account (Only lower case letters and numbers allowed).</span><span class="sxs-lookup"><span data-stu-id="4a70b-124">**Name**: Name your Data Lake Analytics account (Only lower case letters and numbers allowed).</span></span>
   * <span data-ttu-id="4a70b-125">**Subscription**: Choose the Azure subscription used for the Analytics account.</span><span class="sxs-lookup"><span data-stu-id="4a70b-125">**Subscription**: Choose the Azure subscription used for the Analytics account.</span></span>
   * <span data-ttu-id="4a70b-126">**Resource Group**.</span><span class="sxs-lookup"><span data-stu-id="4a70b-126">**Resource Group**.</span></span> <span data-ttu-id="4a70b-127">Select an existing Azure Resource Group or create a new one.</span><span class="sxs-lookup"><span data-stu-id="4a70b-127">Select an existing Azure Resource Group or create a new one.</span></span> <span data-ttu-id="4a70b-128">Azure Resource Manager enables you to work with the resources in your application as a group.</span><span class="sxs-lookup"><span data-stu-id="4a70b-128">Azure Resource Manager enables you to work with the resources in your application as a group.</span></span> <span data-ttu-id="4a70b-129">For more information, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4a70b-129">For more information, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>
   * <span data-ttu-id="4a70b-130">**Location**.</span><span class="sxs-lookup"><span data-stu-id="4a70b-130">**Location**.</span></span> <span data-ttu-id="4a70b-131">Select an Azure data center for the Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="4a70b-131">Select an Azure data center for the Data Lake Analytics account.</span></span>
   * <span data-ttu-id="4a70b-132">**Data Lake Store**: Click *Configure required settings*.</span><span class="sxs-lookup"><span data-stu-id="4a70b-132">**Data Lake Store**: Click *Configure required settings*.</span></span> <span data-ttu-id="4a70b-133">Follow the instruction to create a new Data Lake Store account, or select an existing one.</span><span class="sxs-lookup"><span data-stu-id="4a70b-133">Follow the instruction to create a new Data Lake Store account, or select an existing one.</span></span> <span data-ttu-id="4a70b-134">Each Data Lake Analytics account has a dependent Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="4a70b-134">Each Data Lake Analytics account has a dependent Data Lake Store account.</span></span> <span data-ttu-id="4a70b-135">The Data Lake Analytics account and the dependent Data Lake Store account must be located in the same Azure data center.</span><span class="sxs-lookup"><span data-stu-id="4a70b-135">The Data Lake Analytics account and the dependent Data Lake Store account must be located in the same Azure data center.</span></span>
4. <span data-ttu-id="4a70b-136">Select your Pricing Tier</span><span class="sxs-lookup"><span data-stu-id="4a70b-136">Select your Pricing Tier</span></span>  
5. <span data-ttu-id="4a70b-137">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="4a70b-137">Click **Create**.</span></span> <span data-ttu-id="4a70b-138">It returns you to your portal home screen where a new tile appears, showing "Deploying Azure Data Lake Analytics".</span><span class="sxs-lookup"><span data-stu-id="4a70b-138">It returns you to your portal home screen where a new tile appears, showing "Deploying Azure Data Lake Analytics".</span></span> <span data-ttu-id="4a70b-139">The deploy process will take several minutes to create a Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="4a70b-139">The deploy process will take several minutes to create a Data Lake Analytics account.</span></span> <span data-ttu-id="4a70b-140">When the account is created, the portal opens the account on a new blade.</span><span class="sxs-lookup"><span data-stu-id="4a70b-140">When the account is created, the portal opens the account on a new blade.</span></span>

<span data-ttu-id="4a70b-141">After a Data Lake Analytics account is created, you can add additional Data Lake Store accounts and Azure Storage accounts.</span><span class="sxs-lookup"><span data-stu-id="4a70b-141">After a Data Lake Analytics account is created, you can add additional Data Lake Store accounts and Azure Storage accounts.</span></span> <span data-ttu-id="4a70b-142">For instructions, see [Manage Data lake Analytics account data sources](data-lake-analytics-manage-use-portal.md#manage-account-data-sources).</span><span class="sxs-lookup"><span data-stu-id="4a70b-142">For instructions, see [Manage Data lake Analytics account data sources](data-lake-analytics-manage-use-portal.md#manage-account-data-sources).</span></span>

## <a name="prepare-source-data"></a><span data-ttu-id="4a70b-143">Prepare source data</span><span class="sxs-lookup"><span data-stu-id="4a70b-143">Prepare source data</span></span>
<span data-ttu-id="4a70b-144">In this tutorial, you will process search logs.</span><span class="sxs-lookup"><span data-stu-id="4a70b-144">In this tutorial, you will process search logs.</span></span>  <span data-ttu-id="4a70b-145">The search log can be stored in either dData Lake store or Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="4a70b-145">The search log can be stored in either dData Lake store or Azure Blob storage.</span></span>

<span data-ttu-id="4a70b-146">The Azure portal provides a user interface for copying sample data files to the default Data Lake Store account, which include a search log file.</span><span class="sxs-lookup"><span data-stu-id="4a70b-146">The Azure portal provides a user interface for copying sample data files to the default Data Lake Store account, which include a search log file.</span></span>

<span data-ttu-id="4a70b-147">**Copy sample data files**</span><span class="sxs-lookup"><span data-stu-id="4a70b-147">**Copy sample data files**</span></span>

1. <span data-ttu-id="4a70b-148">From the [Azure portal](https://portal.azure.com), open your Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="4a70b-148">From the [Azure portal](https://portal.azure.com), open your Data Lake Analytics account.</span></span>  <span data-ttu-id="4a70b-149">See [Manage Data Lake Analytics accounts](data-lake-analytics-get-started-portal.md#create-data-lake-analytics-account) to create one and open the account in the portal.</span><span class="sxs-lookup"><span data-stu-id="4a70b-149">See [Manage Data Lake Analytics accounts](data-lake-analytics-get-started-portal.md#create-data-lake-analytics-account) to create one and open the account in the portal.</span></span>
2. <span data-ttu-id="4a70b-150">Expand the **Essentials** pane, and then click **Explore sample scripts**.</span><span class="sxs-lookup"><span data-stu-id="4a70b-150">Expand the **Essentials** pane, and then click **Explore sample scripts**.</span></span> <span data-ttu-id="4a70b-151">It opens another blade called **Sample Scripts**.</span><span class="sxs-lookup"><span data-stu-id="4a70b-151">It opens another blade called **Sample Scripts**.</span></span>

    ![Azure Data Lake Analytics portal sample script](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-get-started-portal/data-lake-analytics-portal-sample-scripts.png)
3. <span data-ttu-id="4a70b-153">Click **Sample Data Missing** to copy the sample data files.</span><span class="sxs-lookup"><span data-stu-id="4a70b-153">Click **Sample Data Missing** to copy the sample data files.</span></span> <span data-ttu-id="4a70b-154">When it is done, the portal shows **Sample data updated successfully**.</span><span class="sxs-lookup"><span data-stu-id="4a70b-154">When it is done, the portal shows **Sample data updated successfully**.</span></span>
4. <span data-ttu-id="4a70b-155">From the Data Lake analytics account blade, click **Data Explorer** on the top.</span><span class="sxs-lookup"><span data-stu-id="4a70b-155">From the Data Lake analytics account blade, click **Data Explorer** on the top.</span></span>

    ![Azure Data Lake Analytics data explorer button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-get-started-portal/data-lake-analytics-data-explorer-button.png)

    <span data-ttu-id="4a70b-157">It opens two blades.</span><span class="sxs-lookup"><span data-stu-id="4a70b-157">It opens two blades.</span></span> <span data-ttu-id="4a70b-158">One is **Data Explorer**, and the other is the default Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="4a70b-158">One is **Data Explorer**, and the other is the default Data Lake Store account.</span></span>
5. <span data-ttu-id="4a70b-159">In the default Data Lake Store account blade, click **Samples** to expand the folder, and the click **Data** to expand the folder.</span><span class="sxs-lookup"><span data-stu-id="4a70b-159">In the default Data Lake Store account blade, click **Samples** to expand the folder, and the click **Data** to expand the folder.</span></span> <span data-ttu-id="4a70b-160">You shall see the following files and folders:</span><span class="sxs-lookup"><span data-stu-id="4a70b-160">You shall see the following files and folders:</span></span>

   * <span data-ttu-id="4a70b-161">AmbulanceData/</span><span class="sxs-lookup"><span data-stu-id="4a70b-161">AmbulanceData/</span></span>
   * <span data-ttu-id="4a70b-162">AdsLog.tsv</span><span class="sxs-lookup"><span data-stu-id="4a70b-162">AdsLog.tsv</span></span>
   * <span data-ttu-id="4a70b-163">SearchLog.tsv</span><span class="sxs-lookup"><span data-stu-id="4a70b-163">SearchLog.tsv</span></span>
   * <span data-ttu-id="4a70b-164">version.txt</span><span class="sxs-lookup"><span data-stu-id="4a70b-164">version.txt</span></span>
   * <span data-ttu-id="4a70b-165">WebLog.log</span><span class="sxs-lookup"><span data-stu-id="4a70b-165">WebLog.log</span></span>

     <span data-ttu-id="4a70b-166">In this tutorial, you use SearchLog.tsv.</span><span class="sxs-lookup"><span data-stu-id="4a70b-166">In this tutorial, you use SearchLog.tsv.</span></span>

<span data-ttu-id="4a70b-167">In practice, you either program your applications to write data into a linked storage accounts or upload data.</span><span class="sxs-lookup"><span data-stu-id="4a70b-167">In practice, you either program your applications to write data into a linked storage accounts or upload data.</span></span> <span data-ttu-id="4a70b-168">For uploading files, see [Upload data to Data Lake Store](data-lake-analytics-manage-use-portal.md#upload-data-to-adls) or [Upload data to Blob storage](data-lake-analytics-manage-use-portal.md#upload-data-to-wasb).</span><span class="sxs-lookup"><span data-stu-id="4a70b-168">For uploading files, see [Upload data to Data Lake Store](data-lake-analytics-manage-use-portal.md#upload-data-to-adls) or [Upload data to Blob storage](data-lake-analytics-manage-use-portal.md#upload-data-to-wasb).</span></span>

## <a name="create-and-submit-data-lake-analytics-jobs"></a><span data-ttu-id="4a70b-169">Create and submit Data Lake Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="4a70b-169">Create and submit Data Lake Analytics jobs</span></span>
<span data-ttu-id="4a70b-170">After you have prepared the source data, you can start developing a U-SQL script.</span><span class="sxs-lookup"><span data-stu-id="4a70b-170">After you have prepared the source data, you can start developing a U-SQL script.</span></span>  

<span data-ttu-id="4a70b-171">**To submit a job**</span><span class="sxs-lookup"><span data-stu-id="4a70b-171">**To submit a job**</span></span>

1. <span data-ttu-id="4a70b-172">From the Data Lake analytics account blade on the portal, click **New Job**.</span><span class="sxs-lookup"><span data-stu-id="4a70b-172">From the Data Lake analytics account blade on the portal, click **New Job**.</span></span>

    ![Azure Data Lake Analytics new job button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-get-started-portal/data-lake-analytics-new-job-button.png)

    <span data-ttu-id="4a70b-174">If you don't see the blade, see [Open a Data Lake Analytics account from portal](data-lake-analytics-manage-use-portal.md#access-adla-account).</span><span class="sxs-lookup"><span data-stu-id="4a70b-174">If you don't see the blade, see [Open a Data Lake Analytics account from portal](data-lake-analytics-manage-use-portal.md#access-adla-account).</span></span>
2. <span data-ttu-id="4a70b-175">Enter **Job Name**, and the following U-SQL script:</span><span class="sxs-lookup"><span data-stu-id="4a70b-175">Enter **Job Name**, and the following U-SQL script:</span></span>

        @searchlog =
            EXTRACT UserId          int,
                    Start           DateTime,
                    Region          string,
                    Query           string,
                    Duration        int?,
                    Urls            string,
                    ClickedUrls     string
            FROM "/Samples/Data/SearchLog.tsv"
            USING Extractors.Tsv();

        OUTPUT @searchlog   
            TO "/Output/SearchLog-from-Data-Lake.csv"
        USING Outputters.Csv();

    ![create Azure Data Lake Analytics U-SQL jobs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-get-started-portal/data-lake-analytics-new-job.png)

    <span data-ttu-id="4a70b-177">This U-SQL script reads the source data file using **Extractors.Tsv()**, and then creates a csv file using **Outputters.Csv()**.</span><span class="sxs-lookup"><span data-stu-id="4a70b-177">This U-SQL script reads the source data file using **Extractors.Tsv()**, and then creates a csv file using **Outputters.Csv()**.</span></span>

    <span data-ttu-id="4a70b-178">Don't modify the two paths unless you copy the source file into a different location.</span><span class="sxs-lookup"><span data-stu-id="4a70b-178">Don't modify the two paths unless you copy the source file into a different location.</span></span>  <span data-ttu-id="4a70b-179">Data Lake Analytics creates the output folder if it doesn't exist.</span><span class="sxs-lookup"><span data-stu-id="4a70b-179">Data Lake Analytics creates the output folder if it doesn't exist.</span></span>  <span data-ttu-id="4a70b-180">In this case, we are using simple, relative paths.</span><span class="sxs-lookup"><span data-stu-id="4a70b-180">In this case, we are using simple, relative paths.</span></span>  

    <span data-ttu-id="4a70b-181">It is simpler to use relative paths for files stored in default Data Lake accounts.</span><span class="sxs-lookup"><span data-stu-id="4a70b-181">It is simpler to use relative paths for files stored in default Data Lake accounts.</span></span> <span data-ttu-id="4a70b-182">You can also use absolute paths.</span><span class="sxs-lookup"><span data-stu-id="4a70b-182">You can also use absolute paths.</span></span>  <span data-ttu-id="4a70b-183">For example</span><span class="sxs-lookup"><span data-stu-id="4a70b-183">For example</span></span>

        adl://<Data LakeStorageAccountName>.azuredatalakestore.net:443/Samples/Data/SearchLog.tsv

    <span data-ttu-id="4a70b-184">For more about U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md) and [U-SQL language reference](http://go.microsoft.com/fwlink/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="4a70b-184">For more about U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md) and [U-SQL language reference](http://go.microsoft.com/fwlink/?LinkId=691348).</span></span>

1. <span data-ttu-id="4a70b-185">Click **Submit Job** from the top.</span><span class="sxs-lookup"><span data-stu-id="4a70b-185">Click **Submit Job** from the top.</span></span>   
2. <span data-ttu-id="4a70b-186">Wait until the job status is changed to **Succeeded**.</span><span class="sxs-lookup"><span data-stu-id="4a70b-186">Wait until the job status is changed to **Succeeded**.</span></span> <span data-ttu-id="4a70b-187">You can see the job took about one minute to complete.</span><span class="sxs-lookup"><span data-stu-id="4a70b-187">You can see the job took about one minute to complete.</span></span>

    <span data-ttu-id="4a70b-188">In case the job failed, see [Monitor and troubleshoot Data Lake Analytics jobs](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="4a70b-188">In case the job failed, see [Monitor and troubleshoot Data Lake Analytics jobs](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span></span>
3. <span data-ttu-id="4a70b-189">At the bottom of the blade, click the **Output** tab, and then click **SearchLog-from-Data-Lake.csv**.</span><span class="sxs-lookup"><span data-stu-id="4a70b-189">At the bottom of the blade, click the **Output** tab, and then click **SearchLog-from-Data-Lake.csv**.</span></span> <span data-ttu-id="4a70b-190">You can preview, download, rename, and delete the output file.</span><span class="sxs-lookup"><span data-stu-id="4a70b-190">You can preview, download, rename, and delete the output file.</span></span>

    ![Azure Data Lake Analytics job output file properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-get-started-portal/data-lake-analytics-output-file-properties.png)

## <a name="see-also"></a><span data-ttu-id="4a70b-192">See also</span><span class="sxs-lookup"><span data-stu-id="4a70b-192">See also</span></span>
* <span data-ttu-id="4a70b-193">To see a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="4a70b-193">To see a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="4a70b-194">To get started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4a70b-194">To get started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="4a70b-195">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4a70b-195">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="4a70b-196">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4a70b-196">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
* <span data-ttu-id="4a70b-197">To get an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4a70b-197">To get an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>
* <span data-ttu-id="4a70b-198">To see the same tutorial using other tools, click the tab selectors on the top of the page.</span><span class="sxs-lookup"><span data-stu-id="4a70b-198">To see the same tutorial using other tools, click the tab selectors on the top of the page.</span></span>
* <span data-ttu-id="4a70b-199">To log diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md)</span><span class="sxs-lookup"><span data-stu-id="4a70b-199">To log diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md)</span></span>






