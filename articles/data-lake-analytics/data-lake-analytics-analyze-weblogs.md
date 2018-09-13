---
title: Analyze Website logs using Azure Data Lake Analytics | Microsoft Docs
description: 'Learn how to analyze website logs using Data Lake Analytics. '
services: data-lake-analytics
documentationcenter: ''
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: 3a196735-d0d9-4deb-ba68-c4b3f3be8403
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: fc9a8b1d13c9499fd32d21b1f574eb4caef54aa9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549259"
---
# <a name="tutorial-analyze-website-logs-using-azure-data-lake-analytics"></a><span data-ttu-id="8fd6e-103">Tutorial: Analyze Website logs using Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="8fd6e-103">Tutorial: Analyze Website logs using Azure Data Lake Analytics</span></span>
<span data-ttu-id="8fd6e-104">Learn how to analyze website logs using Data Lake Analytics, especially on finding out which referrers ran into errors when they tried to visit the website.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-104">Learn how to analyze website logs using Data Lake Analytics, especially on finding out which referrers ran into errors when they tried to visit the website.</span></span>

> [!NOTE]
> <span data-ttu-id="8fd6e-105">If you just want to see the application working, it saves time to go through [Use Azure Data Lake Analytics interactive tutorials](data-lake-analytics-use-interactive-tutorials.md).</span><span class="sxs-lookup"><span data-stu-id="8fd6e-105">If you just want to see the application working, it saves time to go through [Use Azure Data Lake Analytics interactive tutorials](data-lake-analytics-use-interactive-tutorials.md).</span></span> <span data-ttu-id="8fd6e-106">This tutorial is based on the same scenario and the same code.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-106">This tutorial is based on the same scenario and the same code.</span></span> <span data-ttu-id="8fd6e-107">The purpose of this tutorial is to give developers the experience of creating and running a Data Lake Analytics application from end to end.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-107">The purpose of this tutorial is to give developers the experience of creating and running a Data Lake Analytics application from end to end.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="8fd6e-108">Prerequisites:</span><span class="sxs-lookup"><span data-stu-id="8fd6e-108">Prerequisites:</span></span>
* <span data-ttu-id="8fd6e-109">**Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012 with Visual C++ Installed**.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-109">**Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012 with Visual C++ Installed**.</span></span>
* <span data-ttu-id="8fd6e-110">**Microsoft Azure SDK for .NET version 2.5 or above**.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-110">**Microsoft Azure SDK for .NET version 2.5 or above**.</span></span>  <span data-ttu-id="8fd6e-111">Install it using the [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="8fd6e-111">Install it using the [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="8fd6e-112">**[Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs)**.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-112">**[Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs)**.</span></span>

    <span data-ttu-id="8fd6e-113">Once Data Lake Tools for Visual Studio is installed, you will see a **Data Lake** menu in Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="8fd6e-113">Once Data Lake Tools for Visual Studio is installed, you will see a **Data Lake** menu in Visual Studio:</span></span>

    ![U-SQL Visual Studio menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-menu.png)
* <span data-ttu-id="8fd6e-115">**Basic knowledge of Data Lake Analytics and the Data Lake Tools for Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-115">**Basic knowledge of Data Lake Analytics and the Data Lake Tools for Visual Studio**.</span></span> <span data-ttu-id="8fd6e-116">To get started, see:</span><span class="sxs-lookup"><span data-stu-id="8fd6e-116">To get started, see:</span></span>

  * <span data-ttu-id="8fd6e-117">[Get Started with Azure Data Lake Analytics using Azure Portal](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8fd6e-117">[Get Started with Azure Data Lake Analytics using Azure Portal](data-lake-analytics-get-started-portal.md).</span></span>
  * <span data-ttu-id="8fd6e-118">[Develop U-SQL script using Data Lake tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8fd6e-118">[Develop U-SQL script using Data Lake tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="8fd6e-119">**A Data Lake Analytics account.**</span><span class="sxs-lookup"><span data-stu-id="8fd6e-119">**A Data Lake Analytics account.**</span></span>  <span data-ttu-id="8fd6e-120">See [Create an Azure Data Lake Analytics account](data-lake-analytics-get-started-portal.md#create-data-lake-analytics-account).</span><span class="sxs-lookup"><span data-stu-id="8fd6e-120">See [Create an Azure Data Lake Analytics account](data-lake-analytics-get-started-portal.md#create-data-lake-analytics-account).</span></span>

    <span data-ttu-id="8fd6e-121">The Data Lake Tools doesn't support creating Data Lake Analytics accounts.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-121">The Data Lake Tools doesn't support creating Data Lake Analytics accounts.</span></span>  <span data-ttu-id="8fd6e-122">So you have to create it using the Azure Portal, Azure PowerShell, .NET SDK or Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-122">So you have to create it using the Azure Portal, Azure PowerShell, .NET SDK or Azure CLI.</span></span>
* <span data-ttu-id="8fd6e-123">**Upload the sample data to the Data Lake Analytics account.**</span><span class="sxs-lookup"><span data-stu-id="8fd6e-123">**Upload the sample data to the Data Lake Analytics account.**</span></span> <span data-ttu-id="8fd6e-124">See [To copy sample data files](data-lake-analytics-get-started-portal.md#prepare-source-data).</span><span class="sxs-lookup"><span data-stu-id="8fd6e-124">See [To copy sample data files](data-lake-analytics-get-started-portal.md#prepare-source-data).</span></span>

    <span data-ttu-id="8fd6e-125">To run a Data Lake Analytics job, you will need some data.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-125">To run a Data Lake Analytics job, you will need some data.</span></span> <span data-ttu-id="8fd6e-126">Even though the Data Lake Tools supports uploading data, you will use the portal to upload the sample data to make this tutorial easier to follow.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-126">Even though the Data Lake Tools supports uploading data, you will use the portal to upload the sample data to make this tutorial easier to follow.</span></span>

## <a name="connect-to-azure"></a><span data-ttu-id="8fd6e-127">Connect to Azure</span><span class="sxs-lookup"><span data-stu-id="8fd6e-127">Connect to Azure</span></span>
<span data-ttu-id="8fd6e-128">Before you can build and test any U-SQL scripts, you must first connect to Azure.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-128">Before you can build and test any U-SQL scripts, you must first connect to Azure.</span></span>

<span data-ttu-id="8fd6e-129">**To connect to Data Lake Analytics**</span><span class="sxs-lookup"><span data-stu-id="8fd6e-129">**To connect to Data Lake Analytics**</span></span>

1. <span data-ttu-id="8fd6e-130">Open Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-130">Open Visual Studio.</span></span>
2. <span data-ttu-id="8fd6e-131">From the **Data Lake** menu, click **Options and Settings**.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-131">From the **Data Lake** menu, click **Options and Settings**.</span></span>
3. <span data-ttu-id="8fd6e-132">Click **Sign In**, or **Change User** if someone has signed in, and follow the instructions.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-132">Click **Sign In**, or **Change User** if someone has signed in, and follow the instructions.</span></span>
4. <span data-ttu-id="8fd6e-133">Click **OK** to close the Options and Settings dialog.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-133">Click **OK** to close the Options and Settings dialog.</span></span>

<span data-ttu-id="8fd6e-134">**To browse your Data Lake Analytics accounts**</span><span class="sxs-lookup"><span data-stu-id="8fd6e-134">**To browse your Data Lake Analytics accounts**</span></span>

1. <span data-ttu-id="8fd6e-135">From Visual Studio, open **Server Explorer** by press **CTRL+ALT+S**.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-135">From Visual Studio, open **Server Explorer** by press **CTRL+ALT+S**.</span></span>
2. <span data-ttu-id="8fd6e-136">From **Server Explorer**, expand **Azure**, and then expand **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-136">From **Server Explorer**, expand **Azure**, and then expand **Data Lake Analytics**.</span></span> <span data-ttu-id="8fd6e-137">You shall see a list of your Data Lake Analytics accounts if there are any.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-137">You shall see a list of your Data Lake Analytics accounts if there are any.</span></span> <span data-ttu-id="8fd6e-138">You cannot create Data Lake Analytics accounts from the studio.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-138">You cannot create Data Lake Analytics accounts from the studio.</span></span> <span data-ttu-id="8fd6e-139">To create an account, see [Get Started with Azure Data Lake Analytics using Azure Portal](data-lake-analytics-get-started-portal.md) or [Get Started with Azure Data Lake Analytics using Azure PowerShell](data-lake-analytics-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="8fd6e-139">To create an account, see [Get Started with Azure Data Lake Analytics using Azure Portal](data-lake-analytics-get-started-portal.md) or [Get Started with Azure Data Lake Analytics using Azure PowerShell](data-lake-analytics-get-started-powershell.md).</span></span>

## <a name="develop-u-sql-application"></a><span data-ttu-id="8fd6e-140">Develop U-SQL application</span><span class="sxs-lookup"><span data-stu-id="8fd6e-140">Develop U-SQL application</span></span>
<span data-ttu-id="8fd6e-141">A U-SQL application is mostly a U-SQL script.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-141">A U-SQL application is mostly a U-SQL script.</span></span> <span data-ttu-id="8fd6e-142">To learn more about U-SQL, see [Get started with U-SQL](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8fd6e-142">To learn more about U-SQL, see [Get started with U-SQL](data-lake-analytics-u-sql-get-started.md).</span></span>

<span data-ttu-id="8fd6e-143">You can add addition user-defined operators to the application.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-143">You can add addition user-defined operators to the application.</span></span>  <span data-ttu-id="8fd6e-144">For more information, see [Develop U-SQL user defined operators for Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-user-defined-operators.md).</span><span class="sxs-lookup"><span data-stu-id="8fd6e-144">For more information, see [Develop U-SQL user defined operators for Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-user-defined-operators.md).</span></span>

<span data-ttu-id="8fd6e-145">**To create and submit a Data Lake Analytics job**</span><span class="sxs-lookup"><span data-stu-id="8fd6e-145">**To create and submit a Data Lake Analytics job**</span></span>

1. <span data-ttu-id="8fd6e-146">From the **File** menu, click **New**, and then click **Project**.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-146">From the **File** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="8fd6e-147">Select the U-SQL Project type.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-147">Select the U-SQL Project type.</span></span>

    ![new U-SQL Visual Studio project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-new-project.png)
3. <span data-ttu-id="8fd6e-149">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-149">Click **OK**.</span></span> <span data-ttu-id="8fd6e-150">Visual studio creates a solution with a Script.usql file.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-150">Visual studio creates a solution with a Script.usql file.</span></span>
4. <span data-ttu-id="8fd6e-151">Enter the following script into the Script.usql file:</span><span class="sxs-lookup"><span data-stu-id="8fd6e-151">Enter the following script into the Script.usql file:</span></span>

        // Create a database for easy reuse, so you don't need to read from a file every time.
        CREATE DATABASE IF NOT EXISTS SampleDBTutorials;

        // Create a Table valued function. TVF ensures that your jobs fetch data from the weblog file with the correct schema.
        DROP FUNCTION IF EXISTS SampleDBTutorials.dbo.WeblogsView;
        CREATE FUNCTION SampleDBTutorials.dbo.WeblogsView()
        RETURNS @result TABLE
        (
            s_date DateTime,
            s_time string,
            s_sitename string,
            cs_method string,
            cs_uristem string,
            cs_uriquery string,
            s_port int,
            cs_username string,
            c_ip string,
            cs_useragent string,
            cs_cookie string,
            cs_referer string,
            cs_host string,
            sc_status int,
            sc_substatus int,
            sc_win32status int,
            sc_bytes int,
            cs_bytes int,
            s_timetaken int
        )
        AS
        BEGIN

            @result = EXTRACT
                s_date DateTime,
                s_time string,
                s_sitename string,
                cs_method string,
                cs_uristem string,
                cs_uriquery string,
                s_port int,
                cs_username string,
                c_ip string,
                cs_useragent string,
                cs_cookie string,
                cs_referer string,
                cs_host string,
                sc_status int,
                sc_substatus int,
                sc_win32status int,
                sc_bytes int,
                cs_bytes int,
                s_timetaken int
            FROM @"/Samples/Data/WebLog.log"
            USING Extractors.Text(delimiter:' ');
            RETURN;
        END;

        // Create a table for storing referrers and status
        DROP TABLE IF EXISTS SampleDBTutorials.dbo.ReferrersPerDay;
        @weblog = SampleDBTutorials.dbo.WeblogsView();
        CREATE TABLE SampleDBTutorials.dbo.ReferrersPerDay
        (
            INDEX idx1
            CLUSTERED(Year ASC)
            PARTITIONED BY HASH(Year)
        ) AS

        SELECT s_date.Year AS Year,
            s_date.Month AS Month,
            s_date.Day AS Day,
            cs_referer,
            sc_status,
            COUNT(DISTINCT c_ip) AS cnt
        FROM @weblog
        GROUP BY s_date,
                cs_referer,
                sc_status;

    <span data-ttu-id="8fd6e-152">To understand the U-SQL, see [Get started with Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8fd6e-152">To understand the U-SQL, see [Get started with Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>    
5. <span data-ttu-id="8fd6e-153">Add a new U-SQL script to your project and enter the following:</span><span class="sxs-lookup"><span data-stu-id="8fd6e-153">Add a new U-SQL script to your project and enter the following:</span></span>

        // Query the referrers that ran into errors
        @content =
            SELECT *
            FROM SampleDBTutorials.dbo.ReferrersPerDay
            WHERE sc_status >=400 AND sc_status < 500;

        OUTPUT @content
        TO @"/Samples/Outputs/UnsuccessfulResponses.log"
        USING Outputters.Tsv();
6. <span data-ttu-id="8fd6e-154">Switch back to the first U-SQL script and next to the **Submit** button, specify your Analytics account.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-154">Switch back to the first U-SQL script and next to the **Submit** button, specify your Analytics account.</span></span>
7. <span data-ttu-id="8fd6e-155">From **Solution Explorer**, right click **Script.usql**, and then click **Build Script**.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-155">From **Solution Explorer**, right click **Script.usql**, and then click **Build Script**.</span></span> <span data-ttu-id="8fd6e-156">Verify the results in the Output pane.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-156">Verify the results in the Output pane.</span></span>
8. <span data-ttu-id="8fd6e-157">From **Solution Explorer**, right click **Script.usql**, and then click **Submit Script**.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-157">From **Solution Explorer**, right click **Script.usql**, and then click **Submit Script**.</span></span>
9. <span data-ttu-id="8fd6e-158">Verify the **Analytics Account** is the one where you want to run the job, and then click **Submit**.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-158">Verify the **Analytics Account** is the one where you want to run the job, and then click **Submit**.</span></span> <span data-ttu-id="8fd6e-159">Submission results and job link are available in the Data Lake Tools for Visual Studio Results window when the submission is completed.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-159">Submission results and job link are available in the Data Lake Tools for Visual Studio Results window when the submission is completed.</span></span>
10. <span data-ttu-id="8fd6e-160">Wait until the job is completed successfully.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-160">Wait until the job is completed successfully.</span></span>  <span data-ttu-id="8fd6e-161">If the job failed, it is most likely missing the source file.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-161">If the job failed, it is most likely missing the source file.</span></span>  <span data-ttu-id="8fd6e-162">Please see the Prerequisite section of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-162">Please see the Prerequisite section of this tutorial.</span></span> <span data-ttu-id="8fd6e-163">For additional troubleshooting information, see [Monitor and troubleshoot Azure Data Lake Analytics jobs](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="8fd6e-163">For additional troubleshooting information, see [Monitor and troubleshoot Azure Data Lake Analytics jobs](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span></span>

    <span data-ttu-id="8fd6e-164">When the job is completed, you shall see the following screen:</span><span class="sxs-lookup"><span data-stu-id="8fd6e-164">When the job is completed, you shall see the following screen:</span></span>

    ![data lake analytics analyze weblogs website logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-analyze-weblogs/data-lake-analytics-analyze-weblogs-job-completed.png)
11. <span data-ttu-id="8fd6e-166">Now repeat steps 7- 10 for **Script1.usql**.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-166">Now repeat steps 7- 10 for **Script1.usql**.</span></span>

> [!NOTE]
> <span data-ttu-id="8fd6e-167">You can't read from or write to a U-SQL table that has been created or modified in the same script.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-167">You can't read from or write to a U-SQL table that has been created or modified in the same script.</span></span>  <span data-ttu-id="8fd6e-168">That's why use use two scripts for this example.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-168">That's why use use two scripts for this example.</span></span>
>
>

<span data-ttu-id="8fd6e-169">**To see the job output**</span><span class="sxs-lookup"><span data-stu-id="8fd6e-169">**To see the job output**</span></span>

1. <span data-ttu-id="8fd6e-170">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**, right-click the default Data Lake Storage account, and then click **Explorer**.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-170">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**, right-click the default Data Lake Storage account, and then click **Explorer**.</span></span>
2. <span data-ttu-id="8fd6e-171">Double-click **Samples** to open the folder, and then double-click **Outputs**.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-171">Double-click **Samples** to open the folder, and then double-click **Outputs**.</span></span>
3. <span data-ttu-id="8fd6e-172">Double-click **UnsuccessfulResponsees.log**.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-172">Double-click **UnsuccessfulResponsees.log**.</span></span>
4. <span data-ttu-id="8fd6e-173">You can also double-click the output file inside the graph view of the job in order to navigate directly to the output.</span><span class="sxs-lookup"><span data-stu-id="8fd6e-173">You can also double-click the output file inside the graph view of the job in order to navigate directly to the output.</span></span>

## <a name="see-also"></a><span data-ttu-id="8fd6e-174">See also</span><span class="sxs-lookup"><span data-stu-id="8fd6e-174">See also</span></span>
<span data-ttu-id="8fd6e-175">To get started with Data Lake Analytics using different tools, see:</span><span class="sxs-lookup"><span data-stu-id="8fd6e-175">To get started with Data Lake Analytics using different tools, see:</span></span>

* [<span data-ttu-id="8fd6e-176">Get started with Data Lake Analytics using Azure Portal</span><span class="sxs-lookup"><span data-stu-id="8fd6e-176">Get started with Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="8fd6e-177">Get started with Data Lake Analytics using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8fd6e-177">Get started with Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="8fd6e-178">Get started with Data Lake Analytics using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="8fd6e-178">Get started with Data Lake Analytics using .NET SDK</span></span>](data-lake-analytics-get-started-net-sdk.md)

<span data-ttu-id="8fd6e-179">To see more development topics:</span><span class="sxs-lookup"><span data-stu-id="8fd6e-179">To see more development topics:</span></span>

* [<span data-ttu-id="8fd6e-180">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8fd6e-180">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="8fd6e-181">Get started with Azure Data Lake Analytics U-SQL language</span><span class="sxs-lookup"><span data-stu-id="8fd6e-181">Get started with Azure Data Lake Analytics U-SQL language</span></span>](data-lake-analytics-u-sql-get-started.md)
* [<span data-ttu-id="8fd6e-182">Develop U-SQL user defined operators for Data Lake Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="8fd6e-182">Develop U-SQL user defined operators for Data Lake Analytics jobs</span></span>](data-lake-analytics-u-sql-develop-user-defined-operators.md)



