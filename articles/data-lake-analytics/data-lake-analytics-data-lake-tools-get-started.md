---
title: Develop U-SQL scripts using Data Lake Tools for Visual Studio | Microsoft Docs
description: 'Learn how to install Data Lake Tools for Visual Studio, how to develop and test U-SQL scripts. '
services: data-lake-analytics
documentationcenter: ''
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: ad8a6992-02c7-47d4-a108-62fc5a0777a3
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/06/2017
ms.author: edmaca, yanacai
ms.openlocfilehash: 55c665dc50fda800168270d167f7d94694989bfb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662831"
---
# <a name="tutorial-develop-u-sql-scripts-using-data-lake-tools-for-visual-studio"></a><span data-ttu-id="21bc2-103">Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="21bc2-103">Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="21bc2-104">Write and test U-SQL scripts using Data Lake Tools for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="21bc2-104">Write and test U-SQL scripts using Data Lake Tools for Visual Studio.</span></span>

<span data-ttu-id="21bc2-105">U-SQL is a hyper-scalable, highly extensible language for preparing, transforming and analyzing all data in the data lake and beyond.</span><span class="sxs-lookup"><span data-stu-id="21bc2-105">U-SQL is a hyper-scalable, highly extensible language for preparing, transforming and analyzing all data in the data lake and beyond.</span></span> <span data-ttu-id="21bc2-106">For more information, see [U-SQL Reference](http://go.microsoft.com/fwlink/p/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="21bc2-106">For more information, see [U-SQL Reference](http://go.microsoft.com/fwlink/p/?LinkId=691348).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="21bc2-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="21bc2-107">Prerequisites</span></span>
* <span data-ttu-id="21bc2-108">**Visual Studio 2017 (under data storage and processing workload), Visual Studio 2015 update 3, Visual Studio 2013 update 4, or Visual Studio 2012. Enterprise (Ultimate/Premium), Professional, Community editions are supported; Express edition is not supported.**</span><span class="sxs-lookup"><span data-stu-id="21bc2-108">**Visual Studio 2017 (under data storage and processing workload), Visual Studio 2015 update 3, Visual Studio 2013 update 4, or Visual Studio 2012. Enterprise (Ultimate/Premium), Professional, Community editions are supported; Express edition is not supported.**</span></span>
* <span data-ttu-id="21bc2-109">**Microsoft Azure SDK for .NET version 2.7.1 or above**.</span><span class="sxs-lookup"><span data-stu-id="21bc2-109">**Microsoft Azure SDK for .NET version 2.7.1 or above**.</span></span>  <span data-ttu-id="21bc2-110">Install it using the [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="21bc2-110">Install it using the [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="21bc2-111">**[Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs)**.</span><span class="sxs-lookup"><span data-stu-id="21bc2-111">**[Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs)**.</span></span>

    <span data-ttu-id="21bc2-112">Once Data Lake Tools for Visual Studio is installed, you will see a "Data Lake Analytics" node in Server Explorer under the "Azure" node (Open Server Explorer by pressing Ctrl+Alt+S).</span><span class="sxs-lookup"><span data-stu-id="21bc2-112">Once Data Lake Tools for Visual Studio is installed, you will see a "Data Lake Analytics" node in Server Explorer under the "Azure" node (Open Server Explorer by pressing Ctrl+Alt+S).</span></span>

* <span data-ttu-id="21bc2-113">**Data Lake Analytics account and sample data** The Data Lake Tools do not support creating Data Lake Analytics accounts.</span><span class="sxs-lookup"><span data-stu-id="21bc2-113">**Data Lake Analytics account and sample data** The Data Lake Tools do not support creating Data Lake Analytics accounts.</span></span> <span data-ttu-id="21bc2-114">Create an account using the Azure portal, Azure PowerShell, .NET SDK or Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="21bc2-114">Create an account using the Azure portal, Azure PowerShell, .NET SDK or Azure CLI.</span></span>
<span data-ttu-id="21bc2-115">For your convenience, a PowerShell script for creating a Data Lake Analytics service and uploading the source data file can be found in [Appx-A PowerShell sample for preparing the tutorial](data-lake-analytics-data-lake-tools-get-started.md#appx-a-powershell-sample-for-preparing-the-tutorial).</span><span class="sxs-lookup"><span data-stu-id="21bc2-115">For your convenience, a PowerShell script for creating a Data Lake Analytics service and uploading the source data file can be found in [Appx-A PowerShell sample for preparing the tutorial](data-lake-analytics-data-lake-tools-get-started.md#appx-a-powershell-sample-for-preparing-the-tutorial).</span></span>

    <span data-ttu-id="21bc2-116">Optionally, you can go through the following two sections in [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md) to create your account and upload data manually:</span><span class="sxs-lookup"><span data-stu-id="21bc2-116">Optionally, you can go through the following two sections in [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md) to create your account and upload data manually:</span></span>

    1. <span data-ttu-id="21bc2-117">[Create an Azure Data Lake Analytics account](data-lake-analytics-get-started-portal.md#create-data-lake-analytics-account).</span><span class="sxs-lookup"><span data-stu-id="21bc2-117">[Create an Azure Data Lake Analytics account](data-lake-analytics-get-started-portal.md#create-data-lake-analytics-account).</span></span>
    2. <span data-ttu-id="21bc2-118">[Upload SearchLog.tsv to the default Data Lake Storage account](data-lake-analytics-get-started-portal.md#prepare-source-data).</span><span class="sxs-lookup"><span data-stu-id="21bc2-118">[Upload SearchLog.tsv to the default Data Lake Storage account](data-lake-analytics-get-started-portal.md#prepare-source-data).</span></span>

## <a name="connect-to-azure"></a><span data-ttu-id="21bc2-119">Connect to Azure</span><span class="sxs-lookup"><span data-stu-id="21bc2-119">Connect to Azure</span></span>
<span data-ttu-id="21bc2-120">**Connect to Data Lake Analytics**</span><span class="sxs-lookup"><span data-stu-id="21bc2-120">**Connect to Data Lake Analytics**</span></span>

1. <span data-ttu-id="21bc2-121">Open Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="21bc2-121">Open Visual Studio.</span></span>
2. <span data-ttu-id="21bc2-122">From the **View** menu, click **Server Explorer** to open Server Explorer.</span><span class="sxs-lookup"><span data-stu-id="21bc2-122">From the **View** menu, click **Server Explorer** to open Server Explorer.</span></span> <span data-ttu-id="21bc2-123">Or press **[CTRL]+[ALT]+S**.</span><span class="sxs-lookup"><span data-stu-id="21bc2-123">Or press **[CTRL]+[ALT]+S**.</span></span>
3. <span data-ttu-id="21bc2-124">Right-click **Azure**, click "Connect to Microsoft Azure Subscription", and then follow instructions.</span><span class="sxs-lookup"><span data-stu-id="21bc2-124">Right-click **Azure**, click "Connect to Microsoft Azure Subscription", and then follow instructions.</span></span>
4. <span data-ttu-id="21bc2-125">From **Server Explorer**, expand **Azure**, and then expand **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="21bc2-125">From **Server Explorer**, expand **Azure**, and then expand **Data Lake Analytics**.</span></span> <span data-ttu-id="21bc2-126">You shall see a list of your Data Lake Analytics accounts if there are any.</span><span class="sxs-lookup"><span data-stu-id="21bc2-126">You shall see a list of your Data Lake Analytics accounts if there are any.</span></span> <span data-ttu-id="21bc2-127">You cannot create Data Lake Analytics accounts from Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="21bc2-127">You cannot create Data Lake Analytics accounts from Visual Studio.</span></span> <span data-ttu-id="21bc2-128">To create an account, see [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md) or [Get Started with Azure Data Lake Analytics using Azure PowerShell](data-lake-analytics-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="21bc2-128">To create an account, see [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md) or [Get Started with Azure Data Lake Analytics using Azure PowerShell](data-lake-analytics-get-started-powershell.md).</span></span>

## <a name="upload-source-data-files"></a><span data-ttu-id="21bc2-129">Upload source data files</span><span class="sxs-lookup"><span data-stu-id="21bc2-129">Upload source data files</span></span>
<span data-ttu-id="21bc2-130">You have uploaded some data in the **Prerequisite** section earlier in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="21bc2-130">You have uploaded some data in the **Prerequisite** section earlier in the tutorial.</span></span>  

<span data-ttu-id="21bc2-131">To use your own data, follow these steps for uploading data from the Data Lake Tools.</span><span class="sxs-lookup"><span data-stu-id="21bc2-131">To use your own data, follow these steps for uploading data from the Data Lake Tools.</span></span>

<span data-ttu-id="21bc2-132">**Upload files to the dependent Azure Data Lake account**</span><span class="sxs-lookup"><span data-stu-id="21bc2-132">**Upload files to the dependent Azure Data Lake account**</span></span>

1. <span data-ttu-id="21bc2-133">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**.</span><span class="sxs-lookup"><span data-stu-id="21bc2-133">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**.</span></span> <span data-ttu-id="21bc2-134">You shall see the default Data Lake Storage account, and the linked Data Lake Storage accounts, and the linked Azure Storage accounts.</span><span class="sxs-lookup"><span data-stu-id="21bc2-134">You shall see the default Data Lake Storage account, and the linked Data Lake Storage accounts, and the linked Azure Storage accounts.</span></span> <span data-ttu-id="21bc2-135">The default Data Lake account has a label "Default Storage Account".</span><span class="sxs-lookup"><span data-stu-id="21bc2-135">The default Data Lake account has a label "Default Storage Account".</span></span>
2. <span data-ttu-id="21bc2-136">Right-click the default Data Lake Storage account, and then click **Explorer**.</span><span class="sxs-lookup"><span data-stu-id="21bc2-136">Right-click the default Data Lake Storage account, and then click **Explorer**.</span></span>  <span data-ttu-id="21bc2-137">It opens the Data Lake Tools for Visual Studio Explorer pane.</span><span class="sxs-lookup"><span data-stu-id="21bc2-137">It opens the Data Lake Tools for Visual Studio Explorer pane.</span></span>  <span data-ttu-id="21bc2-138">In the left, it shows a tree view, the content view is on the right.</span><span class="sxs-lookup"><span data-stu-id="21bc2-138">In the left, it shows a tree view, the content view is on the right.</span></span>
3. <span data-ttu-id="21bc2-139">Browse to the folder where you want to upload files,</span><span class="sxs-lookup"><span data-stu-id="21bc2-139">Browse to the folder where you want to upload files,</span></span>
4. <span data-ttu-id="21bc2-140">Right-click any blank space, and then click **Upload**.</span><span class="sxs-lookup"><span data-stu-id="21bc2-140">Right-click any blank space, and then click **Upload**.</span></span>

    ![U-SQL Visual Studio project U-SQL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-upload-files.png)

<span data-ttu-id="21bc2-142">**Upload files to a linked Azure Blob storage account**</span><span class="sxs-lookup"><span data-stu-id="21bc2-142">**Upload files to a linked Azure Blob storage account**</span></span>

1. <span data-ttu-id="21bc2-143">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**.</span><span class="sxs-lookup"><span data-stu-id="21bc2-143">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**.</span></span> <span data-ttu-id="21bc2-144">You shall see the default Data Lake Storage account, and the linked Data Lake Storage accounts, and the linked Azure Storage accounts.</span><span class="sxs-lookup"><span data-stu-id="21bc2-144">You shall see the default Data Lake Storage account, and the linked Data Lake Storage accounts, and the linked Azure Storage accounts.</span></span>
2. <span data-ttu-id="21bc2-145">Expand the Azure Storage Account.</span><span class="sxs-lookup"><span data-stu-id="21bc2-145">Expand the Azure Storage Account.</span></span>
3. <span data-ttu-id="21bc2-146">Right-click the container where you want to upload files, and then click **Explorer**.</span><span class="sxs-lookup"><span data-stu-id="21bc2-146">Right-click the container where you want to upload files, and then click **Explorer**.</span></span> <span data-ttu-id="21bc2-147">If you don't have a container, you must first create one using the Azure portal, Azure PowerShell, or other tools.</span><span class="sxs-lookup"><span data-stu-id="21bc2-147">If you don't have a container, you must first create one using the Azure portal, Azure PowerShell, or other tools.</span></span>
4. <span data-ttu-id="21bc2-148">Browse to the folder where you want to upload files,</span><span class="sxs-lookup"><span data-stu-id="21bc2-148">Browse to the folder where you want to upload files,</span></span>
5. <span data-ttu-id="21bc2-149">Right-click any blank space, and then click **Upload**.</span><span class="sxs-lookup"><span data-stu-id="21bc2-149">Right-click any blank space, and then click **Upload**.</span></span>

## <a name="develop-u-sql-scripts"></a><span data-ttu-id="21bc2-150">Develop U-SQL scripts</span><span class="sxs-lookup"><span data-stu-id="21bc2-150">Develop U-SQL scripts</span></span>
<span data-ttu-id="21bc2-151">The Data Lake Analytics jobs are written in the U-SQL language.</span><span class="sxs-lookup"><span data-stu-id="21bc2-151">The Data Lake Analytics jobs are written in the U-SQL language.</span></span> <span data-ttu-id="21bc2-152">To learn more about U-SQL, see [Get started with U-SQL language](data-lake-analytics-u-sql-get-started.md) and [U-SQL language reference](http://go.microsoft.com/fwlink/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="21bc2-152">To learn more about U-SQL, see [Get started with U-SQL language](data-lake-analytics-u-sql-get-started.md) and [U-SQL language reference](http://go.microsoft.com/fwlink/?LinkId=691348).</span></span>

<span data-ttu-id="21bc2-153">**Create and submit a Data Lake Analytics job**</span><span class="sxs-lookup"><span data-stu-id="21bc2-153">**Create and submit a Data Lake Analytics job**</span></span>

1. <span data-ttu-id="21bc2-154">From the **File** menu, click **New**, and then click **Project**.</span><span class="sxs-lookup"><span data-stu-id="21bc2-154">From the **File** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="21bc2-155">Select the **U-SQL Project** type.</span><span class="sxs-lookup"><span data-stu-id="21bc2-155">Select the **U-SQL Project** type.</span></span>

    ![new U-SQL Visual Studio project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-new-project.png)
3. <span data-ttu-id="21bc2-157">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="21bc2-157">Click **OK**.</span></span> <span data-ttu-id="21bc2-158">Visual studio creates a solution with a **Script.usql** file.</span><span class="sxs-lookup"><span data-stu-id="21bc2-158">Visual studio creates a solution with a **Script.usql** file.</span></span>
4. <span data-ttu-id="21bc2-159">Enter the following script into **Script.usql**:</span><span class="sxs-lookup"><span data-stu-id="21bc2-159">Enter the following script into **Script.usql**:</span></span>

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

        @res =
            SELECT *
            FROM @searchlog;        

        OUTPUT @res   
            TO "/Output/SearchLog-from-Data-Lake.csv"
        USING Outputters.Csv();

    <span data-ttu-id="21bc2-160">This U-SQL script reads the source data file using **Extractors.Tsv()**, and then creates a csv file using **Outputters.Csv()**.</span><span class="sxs-lookup"><span data-stu-id="21bc2-160">This U-SQL script reads the source data file using **Extractors.Tsv()**, and then creates a csv file using **Outputters.Csv()**.</span></span>

    <span data-ttu-id="21bc2-161">Don't modify the two paths unless you copied the source file into a different location.</span><span class="sxs-lookup"><span data-stu-id="21bc2-161">Don't modify the two paths unless you copied the source file into a different location.</span></span>  <span data-ttu-id="21bc2-162">Data Lake Analytics will create the output folder if it doesn't exist.</span><span class="sxs-lookup"><span data-stu-id="21bc2-162">Data Lake Analytics will create the output folder if it doesn't exist.</span></span>

    <span data-ttu-id="21bc2-163">It is simpler to use relative paths for files stored in default data Lake accounts.</span><span class="sxs-lookup"><span data-stu-id="21bc2-163">It is simpler to use relative paths for files stored in default data Lake accounts.</span></span> <span data-ttu-id="21bc2-164">You can also use absolute paths.</span><span class="sxs-lookup"><span data-stu-id="21bc2-164">You can also use absolute paths.</span></span>  <span data-ttu-id="21bc2-165">For example</span><span class="sxs-lookup"><span data-stu-id="21bc2-165">For example</span></span>

        adl://<Data LakeStorageAccountName>.azuredatalakestore.net:443/Samples/Data/SearchLog.tsv

    <span data-ttu-id="21bc2-166">You must use absolute paths to access  files in  linked Storage accounts.</span><span class="sxs-lookup"><span data-stu-id="21bc2-166">You must use absolute paths to access  files in  linked Storage accounts.</span></span>  <span data-ttu-id="21bc2-167">The syntax for files stored in linked Azure Storage account is:</span><span class="sxs-lookup"><span data-stu-id="21bc2-167">The syntax for files stored in linked Azure Storage account is:</span></span>

        wasb://<BlobContainerName>@<StorageAccountName>.blob.core.windows.net/Samples/Data/SearchLog.tsv

   > [!NOTE]
   > <span data-ttu-id="21bc2-168">Azure Blob container with public blobs or public containers access permissions are not currently supported.</span><span class="sxs-lookup"><span data-stu-id="21bc2-168">Azure Blob container with public blobs or public containers access permissions are not currently supported.</span></span>  
   >
   >

    <span data-ttu-id="21bc2-169">Notice the following features:</span><span class="sxs-lookup"><span data-stu-id="21bc2-169">Notice the following features:</span></span>

   * <span data-ttu-id="21bc2-170">**IntelliSense**</span><span class="sxs-lookup"><span data-stu-id="21bc2-170">**IntelliSense**</span></span>

       <span data-ttu-id="21bc2-171">Name auto completed and the members will be shown for Rowset, Classes, Databases, Schemas and User Defined Objects (UDOs).</span><span class="sxs-lookup"><span data-stu-id="21bc2-171">Name auto completed and the members will be shown for Rowset, Classes, Databases, Schemas and User Defined Objects (UDOs).</span></span>

       <span data-ttu-id="21bc2-172">IntelliSense for catalog entities (Databases, Schemas, Tables, UDOs etc.) is related to your compute account.</span><span class="sxs-lookup"><span data-stu-id="21bc2-172">IntelliSense for catalog entities (Databases, Schemas, Tables, UDOs etc.) is related to your compute account.</span></span> <span data-ttu-id="21bc2-173">You can check the current active compute account, database and schema in the top toolbar, and switch them through the dropdown lists.</span><span class="sxs-lookup"><span data-stu-id="21bc2-173">You can check the current active compute account, database and schema in the top toolbar, and switch them through the dropdown lists.</span></span>
   * <span data-ttu-id="21bc2-174">**Expand \* columns**</span><span class="sxs-lookup"><span data-stu-id="21bc2-174">**Expand \* columns**</span></span>

       <span data-ttu-id="21bc2-175">Click the right of \*, you shall see a blue underline beneath the \*.</span><span class="sxs-lookup"><span data-stu-id="21bc2-175">Click the right of \*, you shall see a blue underline beneath the \*.</span></span> <span data-ttu-id="21bc2-176">Hover your mouse cursor on the blue underline, and then click the down arrow.</span><span class="sxs-lookup"><span data-stu-id="21bc2-176">Hover your mouse cursor on the blue underline, and then click the down arrow.</span></span>
       <span data-ttu-id="21bc2-177">![Data Lake visual studio tools expand *](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-expand-asterisk.png)</span><span class="sxs-lookup"><span data-stu-id="21bc2-177">![Data Lake visual studio tools expand *](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-expand-asterisk.png)</span></span>

       <span data-ttu-id="21bc2-178">Click **Expand Columns**, the tool will replace the \* with the column names.</span><span class="sxs-lookup"><span data-stu-id="21bc2-178">Click **Expand Columns**, the tool will replace the \* with the column names.</span></span>
   * <span data-ttu-id="21bc2-179">**Auto Format**</span><span class="sxs-lookup"><span data-stu-id="21bc2-179">**Auto Format**</span></span>

       <span data-ttu-id="21bc2-180">Users can change the indentation of the U-SQL script based on the code structure under Edit->Advanced:</span><span class="sxs-lookup"><span data-stu-id="21bc2-180">Users can change the indentation of the U-SQL script based on the code structure under Edit->Advanced:</span></span>

     * <span data-ttu-id="21bc2-181">Format Document (Ctrl+E, D) : Formats the whole document</span><span class="sxs-lookup"><span data-stu-id="21bc2-181">Format Document (Ctrl+E, D) : Formats the whole document</span></span>   
     * <span data-ttu-id="21bc2-182">Format Selection (Ctrl+K, Ctrl+F): Formats the selection.</span><span class="sxs-lookup"><span data-stu-id="21bc2-182">Format Selection (Ctrl+K, Ctrl+F): Formats the selection.</span></span> <span data-ttu-id="21bc2-183">If no selection has been made, this shortcut formats the line the cursor is in.</span><span class="sxs-lookup"><span data-stu-id="21bc2-183">If no selection has been made, this shortcut formats the line the cursor is in.</span></span>  

       <span data-ttu-id="21bc2-184">All the formatting rules are configurable under Tools->Options->Text Editor->SIP->Formatting.</span><span class="sxs-lookup"><span data-stu-id="21bc2-184">All the formatting rules are configurable under Tools->Options->Text Editor->SIP->Formatting.</span></span>  
   * <span data-ttu-id="21bc2-185">**Smart Indent**</span><span class="sxs-lookup"><span data-stu-id="21bc2-185">**Smart Indent**</span></span>

       <span data-ttu-id="21bc2-186">Data Lake Tools for Visual Studio is able to indent expressions automatically while you are writing scripts.</span><span class="sxs-lookup"><span data-stu-id="21bc2-186">Data Lake Tools for Visual Studio is able to indent expressions automatically while you are writing scripts.</span></span> <span data-ttu-id="21bc2-187">This feature is disabled by default, users need to enable it through checking U-SQL->Options and Settings ->Switches->Enable Smart Indent.</span><span class="sxs-lookup"><span data-stu-id="21bc2-187">This feature is disabled by default, users need to enable it through checking U-SQL->Options and Settings ->Switches->Enable Smart Indent.</span></span>
   * <span data-ttu-id="21bc2-188">**Go To Definition and Find All References**</span><span class="sxs-lookup"><span data-stu-id="21bc2-188">**Go To Definition and Find All References**</span></span>

       <span data-ttu-id="21bc2-189">Right-clicking the name of a RowSet/parameter/column/UDO etc. and clicking Go To Definition (F12) allows you to navigate to its definition.</span><span class="sxs-lookup"><span data-stu-id="21bc2-189">Right-clicking the name of a RowSet/parameter/column/UDO etc. and clicking Go To Definition (F12) allows you to navigate to its definition.</span></span> <span data-ttu-id="21bc2-190">By clicking Find All References (Shift+F12), will show all the references.</span><span class="sxs-lookup"><span data-stu-id="21bc2-190">By clicking Find All References (Shift+F12), will show all the references.</span></span>
   * <span data-ttu-id="21bc2-191">**Insert Azure Path**</span><span class="sxs-lookup"><span data-stu-id="21bc2-191">**Insert Azure Path**</span></span>

       <span data-ttu-id="21bc2-192">Rather than remembering Azure file path and type it manually when writing script, Data Lake Tools for Visual Studio provides an easy way: right-click in the editor, click Insert Azure Path.</span><span class="sxs-lookup"><span data-stu-id="21bc2-192">Rather than remembering Azure file path and type it manually when writing script, Data Lake Tools for Visual Studio provides an easy way: right-click in the editor, click Insert Azure Path.</span></span> <span data-ttu-id="21bc2-193">Navigate to the file in the Azure Blob Browser dialog.</span><span class="sxs-lookup"><span data-stu-id="21bc2-193">Navigate to the file in the Azure Blob Browser dialog.</span></span> <span data-ttu-id="21bc2-194">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="21bc2-194">Click **OK**.</span></span> <span data-ttu-id="21bc2-195">the file path will be inserted to your code.</span><span class="sxs-lookup"><span data-stu-id="21bc2-195">the file path will be inserted to your code.</span></span>
5. <span data-ttu-id="21bc2-196">Specify the Data Lake Analytics account, Database, and Schema.</span><span class="sxs-lookup"><span data-stu-id="21bc2-196">Specify the Data Lake Analytics account, Database, and Schema.</span></span> <span data-ttu-id="21bc2-197">You can select **(local)** to run the script locally for the testing purpose.</span><span class="sxs-lookup"><span data-stu-id="21bc2-197">You can select **(local)** to run the script locally for the testing purpose.</span></span> <span data-ttu-id="21bc2-198">For more information, see [Run U-SQL locally](#run-u-sql-locally).</span><span class="sxs-lookup"><span data-stu-id="21bc2-198">For more information, see [Run U-SQL locally](#run-u-sql-locally).</span></span>

    ![Submit U-SQL Visual Studio project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job.png)

    <span data-ttu-id="21bc2-200">For more information, see [Use U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="21bc2-200">For more information, see [Use U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>
6. <span data-ttu-id="21bc2-201">From **Solution Explorer**, right-click **Script.usql**, and then click **Build Script**.</span><span class="sxs-lookup"><span data-stu-id="21bc2-201">From **Solution Explorer**, right-click **Script.usql**, and then click **Build Script**.</span></span> <span data-ttu-id="21bc2-202">Verify the result in the Output pane.</span><span class="sxs-lookup"><span data-stu-id="21bc2-202">Verify the result in the Output pane.</span></span>
7. <span data-ttu-id="21bc2-203">From **Solution Explorer**, right-click **Script.usql**, and then click **Submit Script**.</span><span class="sxs-lookup"><span data-stu-id="21bc2-203">From **Solution Explorer**, right-click **Script.usql**, and then click **Submit Script**.</span></span> <span data-ttu-id="21bc2-204">Optionally, you can also click **Submit** from Script.usql pane.</span><span class="sxs-lookup"><span data-stu-id="21bc2-204">Optionally, you can also click **Submit** from Script.usql pane.</span></span>  <span data-ttu-id="21bc2-205">See the previous screenshot.</span><span class="sxs-lookup"><span data-stu-id="21bc2-205">See the previous screenshot.</span></span>  <span data-ttu-id="21bc2-206">Click the down arrow next to the Submit button to submit using the advance options:</span><span class="sxs-lookup"><span data-stu-id="21bc2-206">Click the down arrow next to the Submit button to submit using the advance options:</span></span>
8. <span data-ttu-id="21bc2-207">Specify **Job Name**, verify the **Analytics Account**, and then click **Submit**.</span><span class="sxs-lookup"><span data-stu-id="21bc2-207">Specify **Job Name**, verify the **Analytics Account**, and then click **Submit**.</span></span> <span data-ttu-id="21bc2-208">Submission results and job link are available in the Data Lake Tools for Visual Studio Results window when the submission is completed.</span><span class="sxs-lookup"><span data-stu-id="21bc2-208">Submission results and job link are available in the Data Lake Tools for Visual Studio Results window when the submission is completed.</span></span>

    ![Submit U-SQL Visual Studio project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job-advanced.png)
9. <span data-ttu-id="21bc2-210">You must click the Refresh button to see the latest job status and refresh the screen.</span><span class="sxs-lookup"><span data-stu-id="21bc2-210">You must click the Refresh button to see the latest job status and refresh the screen.</span></span> <span data-ttu-id="21bc2-211">When the job successes, it will show you the **Job Graph**, **Meta Data Operations**, **State History**, **Diagnostics**:</span><span class="sxs-lookup"><span data-stu-id="21bc2-211">When the job successes, it will show you the **Job Graph**, **Meta Data Operations**, **State History**, **Diagnostics**:</span></span>

    ![U-SQL Visual Studio Data Lake Analytics job performance graph](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-performance-graph.png)

   * <span data-ttu-id="21bc2-213">Job Summary.</span><span class="sxs-lookup"><span data-stu-id="21bc2-213">Job Summary.</span></span> <span data-ttu-id="21bc2-214">Show the summary information of current job, e.g.: State, Progress, Execution Time, Runtime Name, Submitter etc.</span><span class="sxs-lookup"><span data-stu-id="21bc2-214">Show the summary information of current job, e.g.: State, Progress, Execution Time, Runtime Name, Submitter etc.</span></span>   
   * <span data-ttu-id="21bc2-215">Job Details.</span><span class="sxs-lookup"><span data-stu-id="21bc2-215">Job Details.</span></span> <span data-ttu-id="21bc2-216">Detailed information on this job is provided, including script, resource, Vertex Execution View.</span><span class="sxs-lookup"><span data-stu-id="21bc2-216">Detailed information on this job is provided, including script, resource, Vertex Execution View.</span></span>
   * <span data-ttu-id="21bc2-217">Job Graph.</span><span class="sxs-lookup"><span data-stu-id="21bc2-217">Job Graph.</span></span> <span data-ttu-id="21bc2-218">Four graphs are provided to visualize the job’s information: Progress, Data Read, Data Written, Execution Time, Average Execution Time Per Node, Input Throughput, Output Throughput.</span><span class="sxs-lookup"><span data-stu-id="21bc2-218">Four graphs are provided to visualize the job’s information: Progress, Data Read, Data Written, Execution Time, Average Execution Time Per Node, Input Throughput, Output Throughput.</span></span>
   * <span data-ttu-id="21bc2-219">Metadata Operations.</span><span class="sxs-lookup"><span data-stu-id="21bc2-219">Metadata Operations.</span></span> <span data-ttu-id="21bc2-220">It shows all the metadata operations.</span><span class="sxs-lookup"><span data-stu-id="21bc2-220">It shows all the metadata operations.</span></span>
   * <span data-ttu-id="21bc2-221">State History.</span><span class="sxs-lookup"><span data-stu-id="21bc2-221">State History.</span></span>
   * <span data-ttu-id="21bc2-222">Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="21bc2-222">Diagnostics.</span></span> <span data-ttu-id="21bc2-223">Data Lake Tools for Visual Studio will diagnose job execution automatically.</span><span class="sxs-lookup"><span data-stu-id="21bc2-223">Data Lake Tools for Visual Studio will diagnose job execution automatically.</span></span> <span data-ttu-id="21bc2-224">You will receive alerts when there are some errors or performance issues in their jobs.</span><span class="sxs-lookup"><span data-stu-id="21bc2-224">You will receive alerts when there are some errors or performance issues in their jobs.</span></span> <span data-ttu-id="21bc2-225">See Job Diagnostics (link TBD) part for more information.</span><span class="sxs-lookup"><span data-stu-id="21bc2-225">See Job Diagnostics (link TBD) part for more information.</span></span>

<span data-ttu-id="21bc2-226">**To check job state**</span><span class="sxs-lookup"><span data-stu-id="21bc2-226">**To check job state**</span></span>

1. <span data-ttu-id="21bc2-227">From Server Explorer, expand **Azure**, expand **Data Lake Analytics**, expand the Data Lake Analytics account name</span><span class="sxs-lookup"><span data-stu-id="21bc2-227">From Server Explorer, expand **Azure**, expand **Data Lake Analytics**, expand the Data Lake Analytics account name</span></span>
2. <span data-ttu-id="21bc2-228">Double-click **Jobs** to list the jobs.</span><span class="sxs-lookup"><span data-stu-id="21bc2-228">Double-click **Jobs** to list the jobs.</span></span>
3. <span data-ttu-id="21bc2-229">Click a job to see the status.</span><span class="sxs-lookup"><span data-stu-id="21bc2-229">Click a job to see the status.</span></span>

<span data-ttu-id="21bc2-230">**To see the job output**</span><span class="sxs-lookup"><span data-stu-id="21bc2-230">**To see the job output**</span></span>

1. <span data-ttu-id="21bc2-231">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**, right-click the default Data Lake Storage account, and then click **Explorer**.</span><span class="sxs-lookup"><span data-stu-id="21bc2-231">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**, right-click the default Data Lake Storage account, and then click **Explorer**.</span></span>
2. <span data-ttu-id="21bc2-232">Double-click **output** to open the folder</span><span class="sxs-lookup"><span data-stu-id="21bc2-232">Double-click **output** to open the folder</span></span>
3. <span data-ttu-id="21bc2-233">Double-click **SearchLog-From-adltools.csv**.</span><span class="sxs-lookup"><span data-stu-id="21bc2-233">Double-click **SearchLog-From-adltools.csv**.</span></span>

### <a name="job-playback"></a><span data-ttu-id="21bc2-234">Job Playback</span><span class="sxs-lookup"><span data-stu-id="21bc2-234">Job Playback</span></span>
<span data-ttu-id="21bc2-235">Job playback enables you to watch job execution progress and visually detect out performance anomalies and bottlenecks.</span><span class="sxs-lookup"><span data-stu-id="21bc2-235">Job playback enables you to watch job execution progress and visually detect out performance anomalies and bottlenecks.</span></span> <span data-ttu-id="21bc2-236">This feature can be used before the job completes execution (i.e. during the time the job is actively running) as well as after the execution has completed.</span><span class="sxs-lookup"><span data-stu-id="21bc2-236">This feature can be used before the job completes execution (i.e. during the time the job is actively running) as well as after the execution has completed.</span></span> <span data-ttu-id="21bc2-237">Doing playback during job execution will allow the user to play back the progress up to the current time.</span><span class="sxs-lookup"><span data-stu-id="21bc2-237">Doing playback during job execution will allow the user to play back the progress up to the current time.</span></span>

<span data-ttu-id="21bc2-238">**To view job execution progress**</span><span class="sxs-lookup"><span data-stu-id="21bc2-238">**To view job execution progress**</span></span>  

1. <span data-ttu-id="21bc2-239">Click **Load Profile** on the upper right corner.</span><span class="sxs-lookup"><span data-stu-id="21bc2-239">Click **Load Profile** on the upper right corner.</span></span> <span data-ttu-id="21bc2-240">See the previous screen shot.</span><span class="sxs-lookup"><span data-stu-id="21bc2-240">See the previous screen shot.</span></span>
2. <span data-ttu-id="21bc2-241">Click on the Play button on the bottom left corner to review the job execution progress.</span><span class="sxs-lookup"><span data-stu-id="21bc2-241">Click on the Play button on the bottom left corner to review the job execution progress.</span></span>
3. <span data-ttu-id="21bc2-242">During the playback, click **Pause** to stop it or directly drag the progress bar to specific positions.</span><span class="sxs-lookup"><span data-stu-id="21bc2-242">During the playback, click **Pause** to stop it or directly drag the progress bar to specific positions.</span></span>

### <a name="heat-map"></a><span data-ttu-id="21bc2-243">Heat Map</span><span class="sxs-lookup"><span data-stu-id="21bc2-243">Heat Map</span></span>
<span data-ttu-id="21bc2-244">Data Lake Tools for Visual Studio provides user-selectable color-overlays on job view to indicate progress, data I/O, execution time, I/O throughput of each stage.</span><span class="sxs-lookup"><span data-stu-id="21bc2-244">Data Lake Tools for Visual Studio provides user-selectable color-overlays on job view to indicate progress, data I/O, execution time, I/O throughput of each stage.</span></span> <span data-ttu-id="21bc2-245">Through this, users can figure out potential issues and distribution of job properties directly and intuitively.</span><span class="sxs-lookup"><span data-stu-id="21bc2-245">Through this, users can figure out potential issues and distribution of job properties directly and intuitively.</span></span> <span data-ttu-id="21bc2-246">You can choose a data source to display from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="21bc2-246">You can choose a data source to display from the drop-down list.</span></span>  

## <a name="run-u-sql-locally"></a><span data-ttu-id="21bc2-247">Run U-SQL locally</span><span class="sxs-lookup"><span data-stu-id="21bc2-247">Run U-SQL locally</span></span>

<span data-ttu-id="21bc2-248">You can use Azure Data Lake Tools for Visual Studio and the Azure Data Lake U-SQL SDK to run U-SQL jobs on your workstation, just as you can in the Azure Data Lake service.</span><span class="sxs-lookup"><span data-stu-id="21bc2-248">You can use Azure Data Lake Tools for Visual Studio and the Azure Data Lake U-SQL SDK to run U-SQL jobs on your workstation, just as you can in the Azure Data Lake service.</span></span> <span data-ttu-id="21bc2-249">These two local-run features save you time in testing and debugging your U-SQL jobs.</span><span class="sxs-lookup"><span data-stu-id="21bc2-249">These two local-run features save you time in testing and debugging your U-SQL jobs.</span></span> 

* [<span data-ttu-id="21bc2-250">Test and debug U-SQL jobs by using local run and the Azure Data Lake U-SQL SDK</span><span class="sxs-lookup"><span data-stu-id="21bc2-250">Test and debug U-SQL jobs by using local run and the Azure Data Lake U-SQL SDK</span></span>](data-lake-analytics-data-lake-tools-local-run.md)


## <a name="see-also"></a><span data-ttu-id="21bc2-251">See also</span><span class="sxs-lookup"><span data-stu-id="21bc2-251">See also</span></span>
<span data-ttu-id="21bc2-252">To get started with Data Lake Analytics using different tools, see:</span><span class="sxs-lookup"><span data-stu-id="21bc2-252">To get started with Data Lake Analytics using different tools, see:</span></span>

* [<span data-ttu-id="21bc2-253">Get started with Data Lake Analytics using Azure portal</span><span class="sxs-lookup"><span data-stu-id="21bc2-253">Get started with Data Lake Analytics using Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="21bc2-254">Get started with Data Lake Analytics using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="21bc2-254">Get started with Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="21bc2-255">Get started with Data Lake Analytics using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="21bc2-255">Get started with Data Lake Analytics using .NET SDK</span></span>](data-lake-analytics-get-started-net-sdk.md)
* [<span data-ttu-id="21bc2-256">Debug C# code in U-SQL jobs</span><span class="sxs-lookup"><span data-stu-id="21bc2-256">Debug C# code in U-SQL jobs</span></span>](data-lake-analytics-debug-u-sql-jobs.md)

<span data-ttu-id="21bc2-257">To learn Data Lake Tools for Visual Studio code, see [Use the Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="21bc2-257">To learn Data Lake Tools for Visual Studio code, see [Use the Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>

<span data-ttu-id="21bc2-258">To see more development topics:</span><span class="sxs-lookup"><span data-stu-id="21bc2-258">To see more development topics:</span></span>

* [<span data-ttu-id="21bc2-259">Analyze weblogs using Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="21bc2-259">Analyze weblogs using Data Lake Analytics</span></span>](data-lake-analytics-analyze-weblogs.md)
* [<span data-ttu-id="21bc2-260">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="21bc2-260">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="21bc2-261">Get started with Azure Data Lake Analytics U-SQL language</span><span class="sxs-lookup"><span data-stu-id="21bc2-261">Get started with Azure Data Lake Analytics U-SQL language</span></span>](data-lake-analytics-u-sql-get-started.md)
* [<span data-ttu-id="21bc2-262">Develop U-SQL user defined operators for Data Lake Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="21bc2-262">Develop U-SQL user defined operators for Data Lake Analytics jobs</span></span>](data-lake-analytics-u-sql-develop-user-defined-operators.md)

## <a name="appx-a-powershell-sample-for-preparing-the-tutorial"></a><span data-ttu-id="21bc2-263">Appx-A PowerShell sample for preparing the tutorial</span><span class="sxs-lookup"><span data-stu-id="21bc2-263">Appx-A PowerShell sample for preparing the tutorial</span></span>
<span data-ttu-id="21bc2-264">The following PowerShell script prepares an Azure Data Lake Analytics account and the source data for you, So you can skip to [Develop U-SQL scripts](data-lake-analytics-data-lake-tools-get-started.md#develop-u-sql-scripts).</span><span class="sxs-lookup"><span data-stu-id="21bc2-264">The following PowerShell script prepares an Azure Data Lake Analytics account and the source data for you, So you can skip to [Develop U-SQL scripts](data-lake-analytics-data-lake-tools-get-started.md#develop-u-sql-scripts).</span></span>

    #region - used for creating Azure service names
    $nameToken = "<Enter an alias>"
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")
    #endregion

    #region - service names
    $resourceGroupName = $namePrefix + "rg"
    $dataLakeStoreName = $namePrefix + "adas"
    $dataLakeAnalyticsName = $namePrefix + "adla"
    $location = "East US 2"
    #endregion


    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #endregion

    #region - Create an Azure Data Lake Analytics service account
    Write-Host "Create a resource group ..." -ForegroundColor Green
    New-AzureRmResourceGroup `
        -Name  $resourceGroupName `
        -Location $location

    Write-Host "Create a Data Lake account ..."  -ForegroundColor Green
    New-AzureRmDataLakeStoreAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $dataLakeStoreName `
        -Location $location

    Write-Host "Create a Data Lake Analytics account ..."  -ForegroundColor Green
    New-AzureRmDataLakeAnalyticsAccount `
        -Name $dataLakeAnalyticsName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -DefaultDataLake $dataLakeStoreName

    Write-Host "The newly created Data Lake Analytics account ..."  -ForegroundColor Green
    Get-AzureRmDataLakeAnalyticsAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $dataLakeAnalyticsName  
    #endregion

    #region - prepare the source data
    Write-Host "Import the source data ..."  -ForegroundColor Green
    $localFolder = "C:\Tutorials\Downloads\" # A temp location for the file.
    $storageAccount = "adltutorials"  # Don't modify this value.
    $container = "adls-sample-data"  #Don't modify this value.

    # Create the temp location  
    New-Item -Path $localFolder -ItemType Directory -Force

    # Download the sample file from Azure Blob storage
    $context = New-AzureStorageContext -StorageAccountName $storageAccount -Anonymous
    $blobs = Azure\Get-AzureStorageBlob -Container $container -Context $context
    $blobs | Get-AzureStorageBlobContent -Context $context -Destination $localFolder

    # Upload the file to the default Data Lake Store account    
    Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $localFolder"SearchLog.tsv" -Destination "/Samples/Data/SearchLog.tsv"

    Write-Host "List the source data ..."  -ForegroundColor Green
    Get-AzureRmDataLakeStoreChildItem -Account $dataLakeStoreName -Path  "/Samples/Data/"
    #endregion






