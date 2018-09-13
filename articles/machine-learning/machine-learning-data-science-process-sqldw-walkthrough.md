---
title: 'The Team Data Science Process in action: using SQL Data Warehouse | Microsoft Docs'
description: Advanced Analytics Process and Technology in Action
services: machine-learning
documentationcenter: ''
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 88ba8e28-0bd7-49fe-8320-5dfa83b65724
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;hangzh;weig
ms.openlocfilehash: 924b185b8dcec2b9d84a29d1a2722562c3408fee
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563379"
---
# <a name="the-team-data-science-process-in-action-using-sql-data-warehouse"></a><span data-ttu-id="86de4-103">The Team Data Science Process in action: using SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="86de4-103">The Team Data Science Process in action: using SQL Data Warehouse</span></span>
<span data-ttu-id="86de4-104">In this tutorial, we walk you through building and deploying a machine learning model using SQL Data Warehouse (SQL DW) for a publicly available dataset -- the [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset.</span><span class="sxs-lookup"><span data-stu-id="86de4-104">In this tutorial, we walk you through building and deploying a machine learning model using SQL Data Warehouse (SQL DW) for a publicly available dataset -- the [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset.</span></span> <span data-ttu-id="86de4-105">The binary classification model constructed predicts whether or not a tip is paid for a trip, and models for multiclass classification and regression are also discussed that predict the distribution for the tip amounts paid.</span><span class="sxs-lookup"><span data-stu-id="86de4-105">The binary classification model constructed predicts whether or not a tip is paid for a trip, and models for multiclass classification and regression are also discussed that predict the distribution for the tip amounts paid.</span></span>

<span data-ttu-id="86de4-106">The procedure follows the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) workflow.</span><span class="sxs-lookup"><span data-stu-id="86de4-106">The procedure follows the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) workflow.</span></span> <span data-ttu-id="86de4-107">We show how to setup a data science environment, how to load the data into SQL DW, and how use either SQL DW or an IPython Notebook to explore the data and engineer features to model.</span><span class="sxs-lookup"><span data-stu-id="86de4-107">We show how to setup a data science environment, how to load the data into SQL DW, and how use either SQL DW or an IPython Notebook to explore the data and engineer features to model.</span></span> <span data-ttu-id="86de4-108">We then show how to build and deploy a model with Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="86de4-108">We then show how to build and deploy a model with Azure Machine Learning.</span></span>

## <a name="dataset"></a><span data-ttu-id="86de4-109">The NYC Taxi Trips dataset</span><span class="sxs-lookup"><span data-stu-id="86de4-109">The NYC Taxi Trips dataset</span></span>
<span data-ttu-id="86de4-110">The NYC Taxi Trip data consists of about 20GB of compressed CSV files (~48GB uncompressed), recording more than 173 million individual trips and the fares paid for each trip.</span><span class="sxs-lookup"><span data-stu-id="86de4-110">The NYC Taxi Trip data consists of about 20GB of compressed CSV files (~48GB uncompressed), recording more than 173 million individual trips and the fares paid for each trip.</span></span> <span data-ttu-id="86de4-111">Each trip record includes the pickup and drop-off locations and times, anonymized hack (driver's) license number, and the medallion (taxi’s unique id) number.</span><span class="sxs-lookup"><span data-stu-id="86de4-111">Each trip record includes the pickup and drop-off locations and times, anonymized hack (driver's) license number, and the medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="86de4-112">The data covers all trips in the year 2013 and is provided in the following two datasets for each month:</span><span class="sxs-lookup"><span data-stu-id="86de4-112">The data covers all trips in the year 2013 and is provided in the following two datasets for each month:</span></span>

1. <span data-ttu-id="86de4-113">The **trip_data.csv** file contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span><span class="sxs-lookup"><span data-stu-id="86de4-113">The **trip_data.csv** file contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="86de4-114">Here are a few sample records:</span><span class="sxs-lookup"><span data-stu-id="86de4-114">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="86de4-115">The **trip_fare.csv** file contains details of the fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and the total amount paid.</span><span class="sxs-lookup"><span data-stu-id="86de4-115">The **trip_fare.csv** file contains details of the fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and the total amount paid.</span></span> <span data-ttu-id="86de4-116">Here are a few sample records:</span><span class="sxs-lookup"><span data-stu-id="86de4-116">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="86de4-117">The **unique key** used to join trip\_data and trip\_fare is composed of the following three fields:</span><span class="sxs-lookup"><span data-stu-id="86de4-117">The **unique key** used to join trip\_data and trip\_fare is composed of the following three fields:</span></span>

* <span data-ttu-id="86de4-118">medallion,</span><span class="sxs-lookup"><span data-stu-id="86de4-118">medallion,</span></span>
* <span data-ttu-id="86de4-119">hack\_license and</span><span class="sxs-lookup"><span data-stu-id="86de4-119">hack\_license and</span></span>
* <span data-ttu-id="86de4-120">pickup\_datetime.</span><span class="sxs-lookup"><span data-stu-id="86de4-120">pickup\_datetime.</span></span>

## <a name="mltasks"></a><span data-ttu-id="86de4-121">Address three types of prediction tasks</span><span class="sxs-lookup"><span data-stu-id="86de4-121">Address three types of prediction tasks</span></span>
<span data-ttu-id="86de4-122">We formulate three prediction problems based on the *tip\_amount* to illustrate three kinds of modeling tasks:</span><span class="sxs-lookup"><span data-stu-id="86de4-122">We formulate three prediction problems based on the *tip\_amount* to illustrate three kinds of modeling tasks:</span></span>

1. <span data-ttu-id="86de4-123">**Binary classification**: To predict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span><span class="sxs-lookup"><span data-stu-id="86de4-123">**Binary classification**: To predict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
2. <span data-ttu-id="86de4-124">**Multiclass classification**: To predict the range of tip paid for the trip.</span><span class="sxs-lookup"><span data-stu-id="86de4-124">**Multiclass classification**: To predict the range of tip paid for the trip.</span></span> <span data-ttu-id="86de4-125">We divide the *tip\_amount* into five bins or classes:</span><span class="sxs-lookup"><span data-stu-id="86de4-125">We divide the *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="86de4-126">**Regression task**: To predict the amount of tip paid for a trip.</span><span class="sxs-lookup"><span data-stu-id="86de4-126">**Regression task**: To predict the amount of tip paid for a trip.</span></span>  

## <a name="setup"></a><span data-ttu-id="86de4-127">Set up the Azure data science environment for advanced analytics</span><span class="sxs-lookup"><span data-stu-id="86de4-127">Set up the Azure data science environment for advanced analytics</span></span>
<span data-ttu-id="86de4-128">To set up your Azure Data Science environment, follow these steps.</span><span class="sxs-lookup"><span data-stu-id="86de4-128">To set up your Azure Data Science environment, follow these steps.</span></span>

<span data-ttu-id="86de4-129">**Create your own Azure blob storage account**</span><span class="sxs-lookup"><span data-stu-id="86de4-129">**Create your own Azure blob storage account**</span></span>

* <span data-ttu-id="86de4-130">When you provision your own Azure blob storage, choose a geo-location for your Azure blob storage in or as close as possible to **South Central US**, which is where the NYC Taxi data is stored.</span><span class="sxs-lookup"><span data-stu-id="86de4-130">When you provision your own Azure blob storage, choose a geo-location for your Azure blob storage in or as close as possible to **South Central US**, which is where the NYC Taxi data is stored.</span></span> <span data-ttu-id="86de4-131">The data will be copied using AzCopy from the public blob storage container to a container in your own storage account.</span><span class="sxs-lookup"><span data-stu-id="86de4-131">The data will be copied using AzCopy from the public blob storage container to a container in your own storage account.</span></span> <span data-ttu-id="86de4-132">The closer your Azure blob storage is to South Central US, the faster this task (Step 4) will be completed.</span><span class="sxs-lookup"><span data-stu-id="86de4-132">The closer your Azure blob storage is to South Central US, the faster this task (Step 4) will be completed.</span></span>
* <span data-ttu-id="86de4-133">To create your own Azure storage account, follow the steps outlined at [About Azure storage accounts](../storage/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="86de4-133">To create your own Azure storage account, follow the steps outlined at [About Azure storage accounts](../storage/storage-create-storage-account.md).</span></span> <span data-ttu-id="86de4-134">Be sure to make notes on the values for following storage account credentials as they will be needed later in this walkthrough.</span><span class="sxs-lookup"><span data-stu-id="86de4-134">Be sure to make notes on the values for following storage account credentials as they will be needed later in this walkthrough.</span></span>
  
  * <span data-ttu-id="86de4-135">**Storage Account Name**</span><span class="sxs-lookup"><span data-stu-id="86de4-135">**Storage Account Name**</span></span>
  * <span data-ttu-id="86de4-136">**Storage Account Key**</span><span class="sxs-lookup"><span data-stu-id="86de4-136">**Storage Account Key**</span></span>
  * <span data-ttu-id="86de4-137">**Container Name** (which you want the data to be stored in the Azure blob storage)</span><span class="sxs-lookup"><span data-stu-id="86de4-137">**Container Name** (which you want the data to be stored in the Azure blob storage)</span></span>

<span data-ttu-id="86de4-138">**Provision your Azure SQL DW instance.**</span><span class="sxs-lookup"><span data-stu-id="86de4-138">**Provision your Azure SQL DW instance.**</span></span>
<span data-ttu-id="86de4-139">Follow the documentation at [Create a SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) to provision a SQL Data Warehouse instance.</span><span class="sxs-lookup"><span data-stu-id="86de4-139">Follow the documentation at [Create a SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) to provision a SQL Data Warehouse instance.</span></span> <span data-ttu-id="86de4-140">Make sure that you make notations on the following SQL Data Warehouse credentials which will be used in later steps.</span><span class="sxs-lookup"><span data-stu-id="86de4-140">Make sure that you make notations on the following SQL Data Warehouse credentials which will be used in later steps.</span></span>

* <span data-ttu-id="86de4-141">**Server Name**: <server Name>.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="86de4-141">**Server Name**: <server Name>.database.windows.net</span></span>
* <span data-ttu-id="86de4-142">**SQLDW (Database) Name**</span><span class="sxs-lookup"><span data-stu-id="86de4-142">**SQLDW (Database) Name**</span></span>
* <span data-ttu-id="86de4-143">**Username**</span><span class="sxs-lookup"><span data-stu-id="86de4-143">**Username**</span></span>
* <span data-ttu-id="86de4-144">**Password**</span><span class="sxs-lookup"><span data-stu-id="86de4-144">**Password**</span></span>

<span data-ttu-id="86de4-145">**Install Visual Studio and SQL Server Data Tools.**</span><span class="sxs-lookup"><span data-stu-id="86de4-145">**Install Visual Studio and SQL Server Data Tools.**</span></span> <span data-ttu-id="86de4-146">For instructions, see [Install Visual Studio 2015 and/or SSDT (SQL Server Data Tools) for SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="86de4-146">For instructions, see [Install Visual Studio 2015 and/or SSDT (SQL Server Data Tools) for SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md).</span></span>

<span data-ttu-id="86de4-147">**Connect to your Azure SQL DW with Visual Studio.**</span><span class="sxs-lookup"><span data-stu-id="86de4-147">**Connect to your Azure SQL DW with Visual Studio.**</span></span> <span data-ttu-id="86de4-148">For instructions, see steps 1 & 2 in [Connect to Azure SQL Data Warehouse with Visual Studio](../sql-data-warehouse/sql-data-warehouse-connect-overview.md).</span><span class="sxs-lookup"><span data-stu-id="86de4-148">For instructions, see steps 1 & 2 in [Connect to Azure SQL Data Warehouse with Visual Studio](../sql-data-warehouse/sql-data-warehouse-connect-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="86de4-149">Run the following SQL query on the database you created in your SQL Data Warehouse (instead of the query provided in step 3 of the connect topic,) to **create a master key**.</span><span class="sxs-lookup"><span data-stu-id="86de4-149">Run the following SQL query on the database you created in your SQL Data Warehouse (instead of the query provided in step 3 of the connect topic,) to **create a master key**.</span></span>
> 
> 

    BEGIN TRY
           --Try to create the master key
        CREATE MASTER KEY
    END TRY
    BEGIN CATCH
           --If the master key exists, do nothing
    END CATCH;

<span data-ttu-id="86de4-150">**Create an Azure Machine Learning workspace under your Azure subscription.**</span><span class="sxs-lookup"><span data-stu-id="86de4-150">**Create an Azure Machine Learning workspace under your Azure subscription.**</span></span> <span data-ttu-id="86de4-151">For instructions, see [Create an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="86de4-151">For instructions, see [Create an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

## <a name="getdata"></a><span data-ttu-id="86de4-152">Load the data into SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="86de4-152">Load the data into SQL Data Warehouse</span></span>
<span data-ttu-id="86de4-153">Open a Windows PowerShell command console.</span><span class="sxs-lookup"><span data-stu-id="86de4-153">Open a Windows PowerShell command console.</span></span> <span data-ttu-id="86de4-154">Run the following PowerShell commands to download the example SQL script files that we share with you on GitHub to a local directory that you specify with the parameter *-DestDir*.</span><span class="sxs-lookup"><span data-stu-id="86de4-154">Run the following PowerShell commands to download the example SQL script files that we share with you on GitHub to a local directory that you specify with the parameter *-DestDir*.</span></span> <span data-ttu-id="86de4-155">You can change the value of parameter *-DestDir* to any local directory.</span><span class="sxs-lookup"><span data-stu-id="86de4-155">You can change the value of parameter *-DestDir* to any local directory.</span></span> <span data-ttu-id="86de4-156">If *-DestDir* does not exist, it will be created by the PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="86de4-156">If *-DestDir* does not exist, it will be created by the PowerShell script.</span></span>

> [!NOTE]
> <span data-ttu-id="86de4-157">You might need to **Run as Administrator** when executing the following PowerShell script if your *DestDir* directory needs Administrator privilege to create or to write to it.</span><span class="sxs-lookup"><span data-stu-id="86de4-157">You might need to **Run as Administrator** when executing the following PowerShell script if your *DestDir* directory needs Administrator privilege to create or to write to it.</span></span>
> 
> 

    $source = "https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/Download_Scripts_SQLDW_Walkthrough.ps1"
    $ps1_dest = "$pwd\Download_Scripts_SQLDW_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQLDW_Walkthrough.ps1 –DestDir 'C:\tempSQLDW'

<span data-ttu-id="86de4-158">After successful execution, your current working directory changes to *-DestDir*.</span><span class="sxs-lookup"><span data-stu-id="86de4-158">After successful execution, your current working directory changes to *-DestDir*.</span></span> <span data-ttu-id="86de4-159">You should be able to see screen like below:</span><span class="sxs-lookup"><span data-stu-id="86de4-159">You should be able to see screen like below:</span></span>

![][19]

<span data-ttu-id="86de4-160">In your *-DestDir*, execute the following PowerShell script in administrator mode:</span><span class="sxs-lookup"><span data-stu-id="86de4-160">In your *-DestDir*, execute the following PowerShell script in administrator mode:</span></span>

    ./SQLDW_Data_Import.ps1

<span data-ttu-id="86de4-161">When the PowerShell script runs for the first time, you will be asked to input the information from your Azure SQL DW and your Azure blob storage account.</span><span class="sxs-lookup"><span data-stu-id="86de4-161">When the PowerShell script runs for the first time, you will be asked to input the information from your Azure SQL DW and your Azure blob storage account.</span></span> <span data-ttu-id="86de4-162">When this PowerShell script completes running for the first time, the credentials you input will have been written to a configuration file SQLDW.conf in the present working directory.</span><span class="sxs-lookup"><span data-stu-id="86de4-162">When this PowerShell script completes running for the first time, the credentials you input will have been written to a configuration file SQLDW.conf in the present working directory.</span></span> <span data-ttu-id="86de4-163">The future run of this PowerShell script file has the option to read all needed parameters from this configuration file.</span><span class="sxs-lookup"><span data-stu-id="86de4-163">The future run of this PowerShell script file has the option to read all needed parameters from this configuration file.</span></span> <span data-ttu-id="86de4-164">If you need to change some parameters, you can choose to input the parameters on the screen upon prompt by deleting this configuration file and inputting the parameters values as prompted or to change the parameter values by editing the SQLDW.conf file in your *-DestDir* directory.</span><span class="sxs-lookup"><span data-stu-id="86de4-164">If you need to change some parameters, you can choose to input the parameters on the screen upon prompt by deleting this configuration file and inputting the parameters values as prompted or to change the parameter values by editing the SQLDW.conf file in your *-DestDir* directory.</span></span>

> [!NOTE]
> <span data-ttu-id="86de4-165">In order to avoid schema name conflicts with those that already exist in your Azure SQL DW, when reading parameters directly from the SQLDW.conf file, a 3-digit random number is added to the schema name from the SQLDW.conf file as the default schema name for each run.</span><span class="sxs-lookup"><span data-stu-id="86de4-165">In order to avoid schema name conflicts with those that already exist in your Azure SQL DW, when reading parameters directly from the SQLDW.conf file, a 3-digit random number is added to the schema name from the SQLDW.conf file as the default schema name for each run.</span></span> <span data-ttu-id="86de4-166">The PowerShell script may prompt you for a schema name: the name may be specified at user discretion.</span><span class="sxs-lookup"><span data-stu-id="86de4-166">The PowerShell script may prompt you for a schema name: the name may be specified at user discretion.</span></span>
> 
> 

<span data-ttu-id="86de4-167">This **PowerShell script** file completes the following tasks:</span><span class="sxs-lookup"><span data-stu-id="86de4-167">This **PowerShell script** file completes the following tasks:</span></span>

* <span data-ttu-id="86de4-168">**Downloads and installs AzCopy**, if AzCopy is not already installed</span><span class="sxs-lookup"><span data-stu-id="86de4-168">**Downloads and installs AzCopy**, if AzCopy is not already installed</span></span>
  
        $AzCopy_path = SearchAzCopy
        if ($AzCopy_path -eq $null){
               Write-Host "AzCopy.exe is not found in C:\Program Files*. Now, start installing AzCopy..." -ForegroundColor "Yellow"
            InstallAzCopy
            $AzCopy_path = SearchAzCopy
        }
            $env_path = $env:Path
            for ($i=0; $i -lt $AzCopy_path.count; $i++){
                if ($AzCopy_path.count -eq 1){
                    $AzCopy_path_i = $AzCopy_path
                } else {
                    $AzCopy_path_i = $AzCopy_path[$i]
                }
                if ($env_path -notlike '*' +$AzCopy_path_i+'*'){
                    Write-Host $AzCopy_path_i 'not in system path, add it...'
                    [Environment]::SetEnvironmentVariable("Path", "$AzCopy_path_i;$env_path", "Machine")
                    $env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine")
                    $env_path = $env:Path
                }
* <span data-ttu-id="86de4-169">**Copies data to your private blob storage account** from the public blob with AzCopy</span><span class="sxs-lookup"><span data-stu-id="86de4-169">**Copies data to your private blob storage account** from the public blob with AzCopy</span></span>
  
        Write-Host "AzCopy is copying data from public blob to yo storage account. It may take a while..." -ForegroundColor "Yellow"
        $start_time = Get-Date
        AzCopy.exe /Source:$Source /Dest:$DestURL /DestKey:$StorageAccountKey /S
        $end_time = Get-Date
        $time_span = $end_time - $start_time
        $total_seconds = [math]::Round($time_span.TotalSeconds,2)
        Write-Host "AzCopy finished copying data. Please check your storage account to verify." -ForegroundColor "Yellow"
        Write-Host "This step (copying data from public blob to your storage account) takes $total_seconds seconds." -ForegroundColor "Green"
* <span data-ttu-id="86de4-170">**Loads data using Polybase (by executing LoadDataToSQLDW.sql) to your Azure SQL DW** from your private blob storage account with the following commands.</span><span class="sxs-lookup"><span data-stu-id="86de4-170">**Loads data using Polybase (by executing LoadDataToSQLDW.sql) to your Azure SQL DW** from your private blob storage account with the following commands.</span></span>
  
  * <span data-ttu-id="86de4-171">Create a schema</span><span class="sxs-lookup"><span data-stu-id="86de4-171">Create a schema</span></span>
    
          EXEC (''CREATE SCHEMA {schemaname};'');
  * <span data-ttu-id="86de4-172">Create a database scoped credential</span><span class="sxs-lookup"><span data-stu-id="86de4-172">Create a database scoped credential</span></span>
    
          CREATE DATABASE SCOPED CREDENTIAL {KeyAlias}
          WITH IDENTITY = ''asbkey'' ,
          Secret = ''{StorageAccountKey}''
  * <span data-ttu-id="86de4-173">Create an external data source for an Azure storage blob</span><span class="sxs-lookup"><span data-stu-id="86de4-173">Create an external data source for an Azure storage blob</span></span>
    
          CREATE EXTERNAL DATA SOURCE {nyctaxi_trip_storage}
          WITH
          (
              TYPE = HADOOP,
              LOCATION =''wasbs://{ContainerName}@{StorageAccountName}.blob.core.windows.net'',
              CREDENTIAL = {KeyAlias}
          )
          ;
    
          CREATE EXTERNAL DATA SOURCE {nyctaxi_fare_storage}
          WITH
          (
              TYPE = HADOOP,
              LOCATION =''wasbs://{ContainerName}@{StorageAccountName}.blob.core.windows.net'',
              CREDENTIAL = {KeyAlias}
          )
          ;
  * <span data-ttu-id="86de4-174">Create an external file format for a csv file.</span><span class="sxs-lookup"><span data-stu-id="86de4-174">Create an external file format for a csv file.</span></span> <span data-ttu-id="86de4-175">Data is uncompressed and fields are separated with the pipe character.</span><span class="sxs-lookup"><span data-stu-id="86de4-175">Data is uncompressed and fields are separated with the pipe character.</span></span>
    
          CREATE EXTERNAL FILE FORMAT {csv_file_format}
          WITH
          (   
              FORMAT_TYPE = DELIMITEDTEXT,
              FORMAT_OPTIONS  
              (
                  FIELD_TERMINATOR ='','',
                  USE_TYPE_DEFAULT = TRUE
              )
          )
          ;
  * <span data-ttu-id="86de4-176">Create external fare and trip tables for NYC taxi dataset in Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="86de4-176">Create external fare and trip tables for NYC taxi dataset in Azure blob storage.</span></span>
    
          CREATE EXTERNAL TABLE {external_nyctaxi_fare}
          (
              medallion varchar(50) not null,
              hack_license varchar(50) not null,
              vendor_id char(3),
              pickup_datetime datetime not null,
              payment_type char(3),
              fare_amount float,
              surcharge float,
              mta_tax float,
              tip_amount float,
              tolls_amount float,
              total_amount float
          )
          with (
              LOCATION    = ''/nyctaxifare/'',
              DATA_SOURCE = {nyctaxi_fare_storage},
              FILE_FORMAT = {csv_file_format},
              REJECT_TYPE = VALUE,
              REJECT_VALUE = 12     
          )  

            CREATE EXTERNAL TABLE {external_nyctaxi_trip}
            (
                   medallion varchar(50) not null,
                   hack_license varchar(50)  not null,
                   vendor_id char(3),
                   rate_code char(3),
                   store_and_fwd_flag char(3),
                   pickup_datetime datetime  not null,
                   dropoff_datetime datetime,
                   passenger_count int,
                   trip_time_in_secs bigint,
                   trip_distance float,
                   pickup_longitude varchar(30),
                   pickup_latitude varchar(30),
                   dropoff_longitude varchar(30),
                   dropoff_latitude varchar(30)
            )
            with (
                LOCATION    = ''/nyctaxitrip/'',
                DATA_SOURCE = {nyctaxi_trip_storage},
                FILE_FORMAT = {csv_file_format},
                REJECT_TYPE = VALUE,
                REJECT_VALUE = 12         
            )

    - <span data-ttu-id="86de4-177">Load data from external tables in Azure blob storage to SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="86de4-177">Load data from external tables in Azure blob storage to SQL Data Warehouse</span></span>

            CREATE TABLE {schemaname}.{nyctaxi_fare}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            SELECT *
            FROM   {external_nyctaxi_fare}
            ;

            CREATE TABLE {schemaname}.{nyctaxi_trip}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            SELECT *
            FROM   {external_nyctaxi_trip}
            ;

    - <span data-ttu-id="86de4-178">Create a sample data table (NYCTaxi_Sample) and insert data to it from selecting SQL queries on the trip and fare tables.</span><span class="sxs-lookup"><span data-stu-id="86de4-178">Create a sample data table (NYCTaxi_Sample) and insert data to it from selecting SQL queries on the trip and fare tables.</span></span> <span data-ttu-id="86de4-179">(Some steps of this walkthrough needs to use this sample table.)</span><span class="sxs-lookup"><span data-stu-id="86de4-179">(Some steps of this walkthrough needs to use this sample table.)</span></span>

            CREATE TABLE {schemaname}.{nyctaxi_sample}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            (
                SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount, f.total_amount, f.tip_amount,
                tipped = CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END,
                tip_class = CASE
                        WHEN (tip_amount = 0) THEN 0
                        WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
                        WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
                        WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
                        ELSE 4
                    END
                FROM {schemaname}.{nyctaxi_trip} t, {schemaname}.{nyctaxi_fare} f
                WHERE datepart("mi",t.pickup_datetime) = 1
                AND t.medallion = f.medallion
                AND   t.hack_license = f.hack_license
                AND   t.pickup_datetime = f.pickup_datetime
                AND   pickup_longitude <> ''0''
                AND   dropoff_longitude <> ''0''
            )
            ;

<span data-ttu-id="86de4-180">The geographic location of your storage accounts affects load times.</span><span class="sxs-lookup"><span data-stu-id="86de4-180">The geographic location of your storage accounts affects load times.</span></span>

> [!NOTE]
> <span data-ttu-id="86de4-181">Depending on the geographical location of your private blob storage account, the process of copying data from a public blob to your private storage account can take about 15 minutes, or even longer,and the process of loading data from your storage account to your Azure SQL DW could take 20 minutes or longer.</span><span class="sxs-lookup"><span data-stu-id="86de4-181">Depending on the geographical location of your private blob storage account, the process of copying data from a public blob to your private storage account can take about 15 minutes, or even longer,and the process of loading data from your storage account to your Azure SQL DW could take 20 minutes or longer.</span></span>  
> 
> 

<span data-ttu-id="86de4-182">You will have to decide what do if you have duplicate source and destination files.</span><span class="sxs-lookup"><span data-stu-id="86de4-182">You will have to decide what do if you have duplicate source and destination files.</span></span>

> [!NOTE]
> <span data-ttu-id="86de4-183">If the .csv files to be copied from the public blob storage to your private blob storage account already exist in your private blob storage account, AzCopy will ask you whether you want to overwrite them.</span><span class="sxs-lookup"><span data-stu-id="86de4-183">If the .csv files to be copied from the public blob storage to your private blob storage account already exist in your private blob storage account, AzCopy will ask you whether you want to overwrite them.</span></span> <span data-ttu-id="86de4-184">If you do not want to overwrite them, input **n** when prompted.</span><span class="sxs-lookup"><span data-stu-id="86de4-184">If you do not want to overwrite them, input **n** when prompted.</span></span> <span data-ttu-id="86de4-185">If you want to overwrite **all** of them, input **a** when prompted.</span><span class="sxs-lookup"><span data-stu-id="86de4-185">If you want to overwrite **all** of them, input **a** when prompted.</span></span> <span data-ttu-id="86de4-186">You can also input **y** to overwrite .csv files individually.</span><span class="sxs-lookup"><span data-stu-id="86de4-186">You can also input **y** to overwrite .csv files individually.</span></span>
> 
> 

![Plot #21][21]

<span data-ttu-id="86de4-188">You can use your own data.</span><span class="sxs-lookup"><span data-stu-id="86de4-188">You can use your own data.</span></span> <span data-ttu-id="86de4-189">If your data is in your on-premise machine in your real life application, you can still use AzCopy to upload on-premise data to your private Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="86de4-189">If your data is in your on-premise machine in your real life application, you can still use AzCopy to upload on-premise data to your private Azure blob storage.</span></span> <span data-ttu-id="86de4-190">You only need to change the **Source** location, `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, in the AzCopy command of the PowerShell script file to the local directory that contains your data.</span><span class="sxs-lookup"><span data-stu-id="86de4-190">You only need to change the **Source** location, `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, in the AzCopy command of the PowerShell script file to the local directory that contains your data.</span></span>

> [!TIP]
> <span data-ttu-id="86de4-191">If your data is already in your private Azure blob storage in your real life application, you can skip the AzCopy step in the PowerShell script and directly upload the data to Azure SQL DW.</span><span class="sxs-lookup"><span data-stu-id="86de4-191">If your data is already in your private Azure blob storage in your real life application, you can skip the AzCopy step in the PowerShell script and directly upload the data to Azure SQL DW.</span></span> <span data-ttu-id="86de4-192">This will require additional edits of the script to tailor it to the format of your data.</span><span class="sxs-lookup"><span data-stu-id="86de4-192">This will require additional edits of the script to tailor it to the format of your data.</span></span>
> 
> 

<span data-ttu-id="86de4-193">This Powershell script also plugs in the Azure SQL DW information into the data exploration example files SQLDW_Explorations.sql, SQLDW_Explorations.ipynb, and SQLDW_Explorations_Scripts.py so that these three files are ready to be tried out instantly after the PowerShell script completes.</span><span class="sxs-lookup"><span data-stu-id="86de4-193">This Powershell script also plugs in the Azure SQL DW information into the data exploration example files SQLDW_Explorations.sql, SQLDW_Explorations.ipynb, and SQLDW_Explorations_Scripts.py so that these three files are ready to be tried out instantly after the PowerShell script completes.</span></span>

<span data-ttu-id="86de4-194">After a successful execution, you will see screen like below:</span><span class="sxs-lookup"><span data-stu-id="86de4-194">After a successful execution, you will see screen like below:</span></span>

![][20]

## <a name="dbexplore"></a><span data-ttu-id="86de4-195">Data exploration and feature engineering in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="86de4-195">Data exploration and feature engineering in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="86de4-196">In this section, we perform data exploration and feature generation by running SQL queries against Azure SQL DW directly using **Visual Studio Data Tools**.</span><span class="sxs-lookup"><span data-stu-id="86de4-196">In this section, we perform data exploration and feature generation by running SQL queries against Azure SQL DW directly using **Visual Studio Data Tools**.</span></span> <span data-ttu-id="86de4-197">All SQL queries used in this section can be found in the sample script named *SQLDW_Explorations.sql*.</span><span class="sxs-lookup"><span data-stu-id="86de4-197">All SQL queries used in this section can be found in the sample script named *SQLDW_Explorations.sql*.</span></span> <span data-ttu-id="86de4-198">This file has already been downloaded to your local directory by the PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="86de4-198">This file has already been downloaded to your local directory by the PowerShell script.</span></span> <span data-ttu-id="86de4-199">You can also retrieve it from [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql).</span><span class="sxs-lookup"><span data-stu-id="86de4-199">You can also retrieve it from [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql).</span></span> <span data-ttu-id="86de4-200">But the file in GitHub does not have the Azure SQL DW information plugged in.</span><span class="sxs-lookup"><span data-stu-id="86de4-200">But the file in GitHub does not have the Azure SQL DW information plugged in.</span></span>

<span data-ttu-id="86de4-201">Connect to your Azure SQL DW using Visual Studio with the SQL DW login name and password and open up the **SQL Object Explorer** to confirm the database and tables have been imported.</span><span class="sxs-lookup"><span data-stu-id="86de4-201">Connect to your Azure SQL DW using Visual Studio with the SQL DW login name and password and open up the **SQL Object Explorer** to confirm the database and tables have been imported.</span></span> <span data-ttu-id="86de4-202">Retrieve the *SQLDW_Explorations.sql* file.</span><span class="sxs-lookup"><span data-stu-id="86de4-202">Retrieve the *SQLDW_Explorations.sql* file.</span></span>

> [!NOTE]
> <span data-ttu-id="86de4-203">To open a Parallel Data Warehouse (PDW) query editor, use the **New Query** command while your PDW is selected in the **SQL Object Explorer**.</span><span class="sxs-lookup"><span data-stu-id="86de4-203">To open a Parallel Data Warehouse (PDW) query editor, use the **New Query** command while your PDW is selected in the **SQL Object Explorer**.</span></span> <span data-ttu-id="86de4-204">The standard SQL query editor is not supported by PDW.</span><span class="sxs-lookup"><span data-stu-id="86de4-204">The standard SQL query editor is not supported by PDW.</span></span>
> 
> 

<span data-ttu-id="86de4-205">Here are the type of data exploration and feature generation tasks performed in this section:</span><span class="sxs-lookup"><span data-stu-id="86de4-205">Here are the type of data exploration and feature generation tasks performed in this section:</span></span>

* <span data-ttu-id="86de4-206">Explore data distributions of a few fields in varying time windows.</span><span class="sxs-lookup"><span data-stu-id="86de4-206">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="86de4-207">Investigate data quality of the longitude and latitude fields.</span><span class="sxs-lookup"><span data-stu-id="86de4-207">Investigate data quality of the longitude and latitude fields.</span></span>
* <span data-ttu-id="86de4-208">Generate binary and multiclass classification labels based on the **tip\_amount**.</span><span class="sxs-lookup"><span data-stu-id="86de4-208">Generate binary and multiclass classification labels based on the **tip\_amount**.</span></span>
* <span data-ttu-id="86de4-209">Generate features and compute/compare trip distances.</span><span class="sxs-lookup"><span data-stu-id="86de4-209">Generate features and compute/compare trip distances.</span></span>
* <span data-ttu-id="86de4-210">Join the two tables and extract a random sample that will be used to build models.</span><span class="sxs-lookup"><span data-stu-id="86de4-210">Join the two tables and extract a random sample that will be used to build models.</span></span>

### <a name="data-import-verification"></a><span data-ttu-id="86de4-211">Data import verification</span><span class="sxs-lookup"><span data-stu-id="86de4-211">Data import verification</span></span>
<span data-ttu-id="86de4-212">These queries provide a quick verification of the number of rows and columns in the tables populated earlier using Polybase's parallel bulk import,</span><span class="sxs-lookup"><span data-stu-id="86de4-212">These queries provide a quick verification of the number of rows and columns in the tables populated earlier using Polybase's parallel bulk import,</span></span>

    -- Report number of rows in table <nyctaxi_trip> without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')

    -- Report number of columns in table <nyctaxi_trip>
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = '<nyctaxi_trip>' AND table_schema = '<schemaname>'

<span data-ttu-id="86de4-213">**Output:** You should get 173,179,759 rows and 14 columns.</span><span class="sxs-lookup"><span data-stu-id="86de4-213">**Output:** You should get 173,179,759 rows and 14 columns.</span></span>

### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="86de4-214">Exploration: Trip distribution by medallion</span><span class="sxs-lookup"><span data-stu-id="86de4-214">Exploration: Trip distribution by medallion</span></span>
<span data-ttu-id="86de4-215">This example query identifies the medallions (taxi numbers) that completed more than 100 trips within a specified time period.</span><span class="sxs-lookup"><span data-stu-id="86de4-215">This example query identifies the medallions (taxi numbers) that completed more than 100 trips within a specified time period.</span></span> <span data-ttu-id="86de4-216">The query would benefit from the partitioned table access since it is conditioned by the partition scheme of **pickup\_datetime**.</span><span class="sxs-lookup"><span data-stu-id="86de4-216">The query would benefit from the partitioned table access since it is conditioned by the partition scheme of **pickup\_datetime**.</span></span> <span data-ttu-id="86de4-217">Querying the full dataset will also make use of the partitioned table and/or index scan.</span><span class="sxs-lookup"><span data-stu-id="86de4-217">Querying the full dataset will also make use of the partitioned table and/or index scan.</span></span>

    SELECT medallion, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

<span data-ttu-id="86de4-218">**Output:** The query should return a table with rows specifying the 13,369 medallions (taxis) and the number of trip completed by them in 2013.</span><span class="sxs-lookup"><span data-stu-id="86de4-218">**Output:** The query should return a table with rows specifying the 13,369 medallions (taxis) and the number of trip completed by them in 2013.</span></span> <span data-ttu-id="86de4-219">The last column contains the count of the number of trips completed.</span><span class="sxs-lookup"><span data-stu-id="86de4-219">The last column contains the count of the number of trips completed.</span></span>

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="86de4-220">Exploration: Trip distribution by medallion and hack_license</span><span class="sxs-lookup"><span data-stu-id="86de4-220">Exploration: Trip distribution by medallion and hack_license</span></span>
<span data-ttu-id="86de4-221">This example identifies the medallions (taxi numbers) and hack_license numbers (drivers) that completed more than 100 trips within a specified time period.</span><span class="sxs-lookup"><span data-stu-id="86de4-221">This example identifies the medallions (taxi numbers) and hack_license numbers (drivers) that completed more than 100 trips within a specified time period.</span></span>

    SELECT medallion, hack_license, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

<span data-ttu-id="86de4-222">**Output:** The query should return a table with 13,369 rows specifying the 13,369 car/driver IDs that have completed more that 100 trips in 2013.</span><span class="sxs-lookup"><span data-stu-id="86de4-222">**Output:** The query should return a table with 13,369 rows specifying the 13,369 car/driver IDs that have completed more that 100 trips in 2013.</span></span> <span data-ttu-id="86de4-223">The last column contains the count of the number of trips completed.</span><span class="sxs-lookup"><span data-stu-id="86de4-223">The last column contains the count of the number of trips completed.</span></span>

### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a><span data-ttu-id="86de4-224">Data quality assessment: Verify records with incorrect longitude and/or latitude</span><span class="sxs-lookup"><span data-stu-id="86de4-224">Data quality assessment: Verify records with incorrect longitude and/or latitude</span></span>
<span data-ttu-id="86de4-225">This example investigates if any of the longitude and/or latitude fields either contain an invalid value (radian degrees should be between -90 and 90), or have (0, 0) coordinates.</span><span class="sxs-lookup"><span data-stu-id="86de4-225">This example investigates if any of the longitude and/or latitude fields either contain an invalid value (radian degrees should be between -90 and 90), or have (0, 0) coordinates.</span></span>

    SELECT COUNT(*) FROM <schemaname>.<nyctaxi_trip>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

<span data-ttu-id="86de4-226">**Output:** The query returns 837,467 trips that have invalid longitude and/or latitude fields.</span><span class="sxs-lookup"><span data-stu-id="86de4-226">**Output:** The query returns 837,467 trips that have invalid longitude and/or latitude fields.</span></span>

### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a><span data-ttu-id="86de4-227">Exploration: Tipped vs. not tipped trips distribution</span><span class="sxs-lookup"><span data-stu-id="86de4-227">Exploration: Tipped vs. not tipped trips distribution</span></span>
<span data-ttu-id="86de4-228">This example finds the number of trips that were tipped vs. the number that were not tipped in a specified time period (or in the full dataset if covering the full year as it is set up here).</span><span class="sxs-lookup"><span data-stu-id="86de4-228">This example finds the number of trips that were tipped vs. the number that were not tipped in a specified time period (or in the full dataset if covering the full year as it is set up here).</span></span> <span data-ttu-id="86de4-229">This distribution reflects the binary label distribution to be later used for binary classification modeling.</span><span class="sxs-lookup"><span data-stu-id="86de4-229">This distribution reflects the binary label distribution to be later used for binary classification modeling.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM <schemaname>.<nyctaxi_fare>
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

<span data-ttu-id="86de4-230">**Output:** The query should return the following tip frequencies for the year 2013: 90,447,622 tipped and 82,264,709 not-tipped.</span><span class="sxs-lookup"><span data-stu-id="86de4-230">**Output:** The query should return the following tip frequencies for the year 2013: 90,447,622 tipped and 82,264,709 not-tipped.</span></span>

### <a name="exploration-tip-classrange-distribution"></a><span data-ttu-id="86de4-231">Exploration: Tip class/range distribution</span><span class="sxs-lookup"><span data-stu-id="86de4-231">Exploration: Tip class/range distribution</span></span>
<span data-ttu-id="86de4-232">This example computes the distribution of tip ranges in a given time period (or in the full dataset if covering the full year).</span><span class="sxs-lookup"><span data-stu-id="86de4-232">This example computes the distribution of tip ranges in a given time period (or in the full dataset if covering the full year).</span></span> <span data-ttu-id="86de4-233">This is the distribution of the label classes that will be used later for multiclass classification modeling.</span><span class="sxs-lookup"><span data-stu-id="86de4-233">This is the distribution of the label classes that will be used later for multiclass classification modeling.</span></span>

    SELECT tip_class, COUNT(*) AS tip_freq FROM (
        SELECT CASE
            WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tip_class

<span data-ttu-id="86de4-234">**Output:**</span><span class="sxs-lookup"><span data-stu-id="86de4-234">**Output:**</span></span>

| <span data-ttu-id="86de4-235">tip_class</span><span class="sxs-lookup"><span data-stu-id="86de4-235">tip_class</span></span> | <span data-ttu-id="86de4-236">tip_freq</span><span class="sxs-lookup"><span data-stu-id="86de4-236">tip_freq</span></span> |
| --- | --- |
| <span data-ttu-id="86de4-237">1</span><span class="sxs-lookup"><span data-stu-id="86de4-237">1</span></span> |<span data-ttu-id="86de4-238">82230915</span><span class="sxs-lookup"><span data-stu-id="86de4-238">82230915</span></span> |
| <span data-ttu-id="86de4-239">2</span><span class="sxs-lookup"><span data-stu-id="86de4-239">2</span></span> |<span data-ttu-id="86de4-240">6198803</span><span class="sxs-lookup"><span data-stu-id="86de4-240">6198803</span></span> |
| <span data-ttu-id="86de4-241">3</span><span class="sxs-lookup"><span data-stu-id="86de4-241">3</span></span> |<span data-ttu-id="86de4-242">1932223</span><span class="sxs-lookup"><span data-stu-id="86de4-242">1932223</span></span> |
| <span data-ttu-id="86de4-243">0</span><span class="sxs-lookup"><span data-stu-id="86de4-243">0</span></span> |<span data-ttu-id="86de4-244">82264625</span><span class="sxs-lookup"><span data-stu-id="86de4-244">82264625</span></span> |
| <span data-ttu-id="86de4-245">4</span><span class="sxs-lookup"><span data-stu-id="86de4-245">4</span></span> |<span data-ttu-id="86de4-246">85765</span><span class="sxs-lookup"><span data-stu-id="86de4-246">85765</span></span> |

### <a name="exploration-compute-and-compare-trip-distance"></a><span data-ttu-id="86de4-247">Exploration: Compute and compare trip distance</span><span class="sxs-lookup"><span data-stu-id="86de4-247">Exploration: Compute and compare trip distance</span></span>
<span data-ttu-id="86de4-248">This example converts the pickup and drop-off longitude and latitude to SQL geography points, computes the trip distance using SQL geography points difference, and returns a random sample of the results for comparison.</span><span class="sxs-lookup"><span data-stu-id="86de4-248">This example converts the pickup and drop-off longitude and latitude to SQL geography points, computes the trip distance using SQL geography points difference, and returns a random sample of the results for comparison.</span></span> <span data-ttu-id="86de4-249">The example limits the results to valid coordinates only using the data quality assessment query covered earlier.</span><span class="sxs-lookup"><span data-stu-id="86de4-249">The example limits the results to valid coordinates only using the data quality assessment query covered earlier.</span></span>

    /****** Object:  UserDefinedFunction [dbo].[fnCalculateDistance] ******/
    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function to calculate the direct distance  in mile between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert to radians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert to miles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

### <a name="feature-engineering-using-sql-functions"></a><span data-ttu-id="86de4-250">Feature engineering using SQL functions</span><span class="sxs-lookup"><span data-stu-id="86de4-250">Feature engineering using SQL functions</span></span>
<span data-ttu-id="86de4-251">Sometimes SQL functions can be an efficient option for feature engineering.</span><span class="sxs-lookup"><span data-stu-id="86de4-251">Sometimes SQL functions can be an efficient option for feature engineering.</span></span> <span data-ttu-id="86de4-252">In this walkthrough, we defined a SQL function to calculate the direct distance between the pickup and dropoff locations.</span><span class="sxs-lookup"><span data-stu-id="86de4-252">In this walkthrough, we defined a SQL function to calculate the direct distance between the pickup and dropoff locations.</span></span> <span data-ttu-id="86de4-253">You can run the following SQL scripts in **Visual Studio Data Tools**.</span><span class="sxs-lookup"><span data-stu-id="86de4-253">You can run the following SQL scripts in **Visual Studio Data Tools**.</span></span>

<span data-ttu-id="86de4-254">Here is the SQL script that defines the distance function.</span><span class="sxs-lookup"><span data-stu-id="86de4-254">Here is the SQL script that defines the distance function.</span></span>

    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function calculate the direct distance between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert to radians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert to miles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

<span data-ttu-id="86de4-255">Here is an example to call this function to generate features in your SQL query:</span><span class="sxs-lookup"><span data-stu-id="86de4-255">Here is an example to call this function to generate features in your SQL query:</span></span>

    -- Sample query to call the function to create features
    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

<span data-ttu-id="86de4-256">**Output:** This query generates a table (with 2,803,538 rows) with pickup and dropoff latitudes and longitudes and the corresponding direct distances in miles.</span><span class="sxs-lookup"><span data-stu-id="86de4-256">**Output:** This query generates a table (with 2,803,538 rows) with pickup and dropoff latitudes and longitudes and the corresponding direct distances in miles.</span></span> <span data-ttu-id="86de4-257">Here are the results for first 3 rows:</span><span class="sxs-lookup"><span data-stu-id="86de4-257">Here are the results for first 3 rows:</span></span>

|  | <span data-ttu-id="86de4-258">pickup_latitude</span><span class="sxs-lookup"><span data-stu-id="86de4-258">pickup_latitude</span></span> | <span data-ttu-id="86de4-259">pickup_longitude</span><span class="sxs-lookup"><span data-stu-id="86de4-259">pickup_longitude</span></span> | <span data-ttu-id="86de4-260">dropoff_latitude</span><span class="sxs-lookup"><span data-stu-id="86de4-260">dropoff_latitude</span></span> | <span data-ttu-id="86de4-261">dropoff_longitude</span><span class="sxs-lookup"><span data-stu-id="86de4-261">dropoff_longitude</span></span> | <span data-ttu-id="86de4-262">DirectDistance</span><span class="sxs-lookup"><span data-stu-id="86de4-262">DirectDistance</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="86de4-263">1</span><span class="sxs-lookup"><span data-stu-id="86de4-263">1</span></span> |<span data-ttu-id="86de4-264">40.731804</span><span class="sxs-lookup"><span data-stu-id="86de4-264">40.731804</span></span> |<span data-ttu-id="86de4-265">-74.001083</span><span class="sxs-lookup"><span data-stu-id="86de4-265">-74.001083</span></span> |<span data-ttu-id="86de4-266">40.736622</span><span class="sxs-lookup"><span data-stu-id="86de4-266">40.736622</span></span> |<span data-ttu-id="86de4-267">-73.988953</span><span class="sxs-lookup"><span data-stu-id="86de4-267">-73.988953</span></span> |<span data-ttu-id="86de4-268">.7169601222</span><span class="sxs-lookup"><span data-stu-id="86de4-268">.7169601222</span></span> |
| <span data-ttu-id="86de4-269">2</span><span class="sxs-lookup"><span data-stu-id="86de4-269">2</span></span> |<span data-ttu-id="86de4-270">40.715794</span><span class="sxs-lookup"><span data-stu-id="86de4-270">40.715794</span></span> |<span data-ttu-id="86de4-271">-74,010635</span><span class="sxs-lookup"><span data-stu-id="86de4-271">-74,010635</span></span> |<span data-ttu-id="86de4-272">40.725338</span><span class="sxs-lookup"><span data-stu-id="86de4-272">40.725338</span></span> |<span data-ttu-id="86de4-273">-74.00399</span><span class="sxs-lookup"><span data-stu-id="86de4-273">-74.00399</span></span> |<span data-ttu-id="86de4-274">.7448343721</span><span class="sxs-lookup"><span data-stu-id="86de4-274">.7448343721</span></span> |
| <span data-ttu-id="86de4-275">3</span><span class="sxs-lookup"><span data-stu-id="86de4-275">3</span></span> |<span data-ttu-id="86de4-276">40.761456</span><span class="sxs-lookup"><span data-stu-id="86de4-276">40.761456</span></span> |<span data-ttu-id="86de4-277">-73.999886</span><span class="sxs-lookup"><span data-stu-id="86de4-277">-73.999886</span></span> |<span data-ttu-id="86de4-278">40.766544</span><span class="sxs-lookup"><span data-stu-id="86de4-278">40.766544</span></span> |<span data-ttu-id="86de4-279">-73.988228</span><span class="sxs-lookup"><span data-stu-id="86de4-279">-73.988228</span></span> |<span data-ttu-id="86de4-280">0.7037227967</span><span class="sxs-lookup"><span data-stu-id="86de4-280">0.7037227967</span></span> |

### <a name="prepare-data-for-model-building"></a><span data-ttu-id="86de4-281">Prepare data for model building</span><span class="sxs-lookup"><span data-stu-id="86de4-281">Prepare data for model building</span></span>
<span data-ttu-id="86de4-282">The following query joins the **nyctaxi\_trip** and **nyctaxi\_fare** tables, generates a binary classification label **tipped**, a multi-class classification label **tip\_class**, and extracts a sample from the full joined dataset.</span><span class="sxs-lookup"><span data-stu-id="86de4-282">The following query joins the **nyctaxi\_trip** and **nyctaxi\_fare** tables, generates a binary classification label **tipped**, a multi-class classification label **tip\_class**, and extracts a sample from the full joined dataset.</span></span> <span data-ttu-id="86de4-283">The sampling is done by retrieving a subset of the trips based on pickup time.</span><span class="sxs-lookup"><span data-stu-id="86de4-283">The sampling is done by retrieving a subset of the trips based on pickup time.</span></span>  <span data-ttu-id="86de4-284">This query can be copied then pasted directly in the [Azure Machine Learning Studio](https://studio.azureml.net) [Import Data][import-data] module for direct data ingestion from the SQL database instance in Azure.</span><span class="sxs-lookup"><span data-stu-id="86de4-284">This query can be copied then pasted directly in the [Azure Machine Learning Studio](https://studio.azureml.net) [Import Data][import-data] module for direct data ingestion from the SQL database instance in Azure.</span></span> <span data-ttu-id="86de4-285">The query excludes records with incorrect (0, 0) coordinates.</span><span class="sxs-lookup"><span data-stu-id="86de4-285">The query excludes records with incorrect (0, 0) coordinates.</span></span>

    SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,     f.total_amount, f.tip_amount,
        CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped,
        CASE WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM <schemaname>.<nyctaxi_trip> t, <schemaname>.<nyctaxi_fare> f
    WHERE datepart("mi",t.pickup_datetime) = 1
    AND   t.medallion = f.medallion
    AND   t.hack_license = f.hack_license
    AND   t.pickup_datetime = f.pickup_datetime
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'

<span data-ttu-id="86de4-286">When you are ready to proceed to Azure Machine Learning, you may either:</span><span class="sxs-lookup"><span data-stu-id="86de4-286">When you are ready to proceed to Azure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="86de4-287">Save the final SQL query to extract and sample the data and copy-paste the query directly into a [Import Data][import-data] module in Azure Machine Learning, or</span><span class="sxs-lookup"><span data-stu-id="86de4-287">Save the final SQL query to extract and sample the data and copy-paste the query directly into a [Import Data][import-data] module in Azure Machine Learning, or</span></span>
2. <span data-ttu-id="86de4-288">Persist the sampled and engineered data you plan to use for model building in a new SQL DW table and use the new table in the [Import Data][import-data] module in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="86de4-288">Persist the sampled and engineered data you plan to use for model building in a new SQL DW table and use the new table in the [Import Data][import-data] module in Azure Machine Learning.</span></span> <span data-ttu-id="86de4-289">The PowerShell script in earlier step has done this for you.</span><span class="sxs-lookup"><span data-stu-id="86de4-289">The PowerShell script in earlier step has done this for you.</span></span> <span data-ttu-id="86de4-290">You can read directly from this table in the Import Data module.</span><span class="sxs-lookup"><span data-stu-id="86de4-290">You can read directly from this table in the Import Data module.</span></span>

## <a name="ipnb"></a><span data-ttu-id="86de4-291">Data exploration and feature engineering in IPython notebook</span><span class="sxs-lookup"><span data-stu-id="86de4-291">Data exploration and feature engineering in IPython notebook</span></span>
<span data-ttu-id="86de4-292">In this section, we will perform data exploration and feature generation using both Python and SQL queries against the SQL DW created earlier.</span><span class="sxs-lookup"><span data-stu-id="86de4-292">In this section, we will perform data exploration and feature generation using both Python and SQL queries against the SQL DW created earlier.</span></span> <span data-ttu-id="86de4-293">A sample IPython notebook named **SQLDW_Explorations.ipynb** and a Python script file **SQLDW_Explorations_Scripts.py** have been downloaded to your local directory.</span><span class="sxs-lookup"><span data-stu-id="86de4-293">A sample IPython notebook named **SQLDW_Explorations.ipynb** and a Python script file **SQLDW_Explorations_Scripts.py** have been downloaded to your local directory.</span></span> <span data-ttu-id="86de4-294">They are also available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW).</span><span class="sxs-lookup"><span data-stu-id="86de4-294">They are also available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW).</span></span> <span data-ttu-id="86de4-295">These two files are identical in Python scripts.</span><span class="sxs-lookup"><span data-stu-id="86de4-295">These two files are identical in Python scripts.</span></span> <span data-ttu-id="86de4-296">The Python script file is provided to you in case you do not have an IPython Notebook server.</span><span class="sxs-lookup"><span data-stu-id="86de4-296">The Python script file is provided to you in case you do not have an IPython Notebook server.</span></span> <span data-ttu-id="86de4-297">These two sample Python files are designed under **Python 2.7**.</span><span class="sxs-lookup"><span data-stu-id="86de4-297">These two sample Python files are designed under **Python 2.7**.</span></span>

<span data-ttu-id="86de4-298">The needed Azure SQL DW information in the sample IPython Notebook and the Python script file downloaded to your local machine has been plugged in by the PowerShell script previously.</span><span class="sxs-lookup"><span data-stu-id="86de4-298">The needed Azure SQL DW information in the sample IPython Notebook and the Python script file downloaded to your local machine has been plugged in by the PowerShell script previously.</span></span> <span data-ttu-id="86de4-299">They are executable without any modification.</span><span class="sxs-lookup"><span data-stu-id="86de4-299">They are executable without any modification.</span></span>

<span data-ttu-id="86de4-300">If you have already set up an AzureML workspace, you can directly upload the sample IPython Notebook to the AzureML IPython Notebook service and start running it.</span><span class="sxs-lookup"><span data-stu-id="86de4-300">If you have already set up an AzureML workspace, you can directly upload the sample IPython Notebook to the AzureML IPython Notebook service and start running it.</span></span> <span data-ttu-id="86de4-301">Here are the steps to upload to AzureML IPython Notebook service:</span><span class="sxs-lookup"><span data-stu-id="86de4-301">Here are the steps to upload to AzureML IPython Notebook service:</span></span>

1. <span data-ttu-id="86de4-302">Log in to your AzureML workspace, click "Studio" at the top, and click "NOTEBOOKS" on the left side of the web page.</span><span class="sxs-lookup"><span data-stu-id="86de4-302">Log in to your AzureML workspace, click "Studio" at the top, and click "NOTEBOOKS" on the left side of the web page.</span></span>
   
    ![Plot #22][22]
2. <span data-ttu-id="86de4-304">Click "NEW" on the left bottom corner of the web page, and select "Python 2".</span><span class="sxs-lookup"><span data-stu-id="86de4-304">Click "NEW" on the left bottom corner of the web page, and select "Python 2".</span></span> <span data-ttu-id="86de4-305">Then, provide a name to the notebook and click the check mark to create the new blank IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="86de4-305">Then, provide a name to the notebook and click the check mark to create the new blank IPython Notebook.</span></span>
   
    ![Plot #23][23]
3. <span data-ttu-id="86de4-307">Click the "Jupyter" symbol on the left top corner of the new IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="86de4-307">Click the "Jupyter" symbol on the left top corner of the new IPython Notebook.</span></span>
   
    ![Plot #24][24]
4. <span data-ttu-id="86de4-309">Drag and drop the sample IPython Notebook to the **tree** page of your AzureML IPython Notebook service, and click **Upload**.</span><span class="sxs-lookup"><span data-stu-id="86de4-309">Drag and drop the sample IPython Notebook to the **tree** page of your AzureML IPython Notebook service, and click **Upload**.</span></span> <span data-ttu-id="86de4-310">Then, the sample IPython Notebook will be uploaded to the AzureML IPython Notebook service.</span><span class="sxs-lookup"><span data-stu-id="86de4-310">Then, the sample IPython Notebook will be uploaded to the AzureML IPython Notebook service.</span></span>
   
    ![Plot #25][25]

<span data-ttu-id="86de4-312">In order to run the sample IPython Notebook or the Python script file, the following Python packages are needed.</span><span class="sxs-lookup"><span data-stu-id="86de4-312">In order to run the sample IPython Notebook or the Python script file, the following Python packages are needed.</span></span> <span data-ttu-id="86de4-313">If you are using the AzureML IPython Notebook service, these packages have been pre-installed.</span><span class="sxs-lookup"><span data-stu-id="86de4-313">If you are using the AzureML IPython Notebook service, these packages have been pre-installed.</span></span>

    - <span data-ttu-id="86de4-314">pandas</span><span class="sxs-lookup"><span data-stu-id="86de4-314">pandas</span></span>
    - <span data-ttu-id="86de4-315">numpy</span><span class="sxs-lookup"><span data-stu-id="86de4-315">numpy</span></span>
    - <span data-ttu-id="86de4-316">matplotlib</span><span class="sxs-lookup"><span data-stu-id="86de4-316">matplotlib</span></span>
    - <span data-ttu-id="86de4-317">pyodbc</span><span class="sxs-lookup"><span data-stu-id="86de4-317">pyodbc</span></span>
    - <span data-ttu-id="86de4-318">PyTables</span><span class="sxs-lookup"><span data-stu-id="86de4-318">PyTables</span></span>

<span data-ttu-id="86de4-319">The recommended sequence when building advanced analytical solutions on AzureML with large data is the following:</span><span class="sxs-lookup"><span data-stu-id="86de4-319">The recommended sequence when building advanced analytical solutions on AzureML with large data is the following:</span></span>

* <span data-ttu-id="86de4-320">Read in a small sample of the data into an in-memory data frame.</span><span class="sxs-lookup"><span data-stu-id="86de4-320">Read in a small sample of the data into an in-memory data frame.</span></span>
* <span data-ttu-id="86de4-321">Perform some visualizations and explorations using the sampled data.</span><span class="sxs-lookup"><span data-stu-id="86de4-321">Perform some visualizations and explorations using the sampled data.</span></span>
* <span data-ttu-id="86de4-322">Experiment with feature engineering using the sampled data.</span><span class="sxs-lookup"><span data-stu-id="86de4-322">Experiment with feature engineering using the sampled data.</span></span>
* <span data-ttu-id="86de4-323">For larger data exploration, data manipulation and feature engineering, use Python to issue SQL Queries directly against the SQL DW.</span><span class="sxs-lookup"><span data-stu-id="86de4-323">For larger data exploration, data manipulation and feature engineering, use Python to issue SQL Queries directly against the SQL DW.</span></span>
* <span data-ttu-id="86de4-324">Decide the sample size to be suitable for Azure Machine Learning model building.</span><span class="sxs-lookup"><span data-stu-id="86de4-324">Decide the sample size to be suitable for Azure Machine Learning model building.</span></span>

<span data-ttu-id="86de4-325">The followings are a few data exploration, data visualization, and feature engineering examples.</span><span class="sxs-lookup"><span data-stu-id="86de4-325">The followings are a few data exploration, data visualization, and feature engineering examples.</span></span> <span data-ttu-id="86de4-326">More data explorations can be found in the sample IPython Notebook and the sample Python script file.</span><span class="sxs-lookup"><span data-stu-id="86de4-326">More data explorations can be found in the sample IPython Notebook and the sample Python script file.</span></span>

### <a name="initialize-database-credentials"></a><span data-ttu-id="86de4-327">Initialize database credentials</span><span class="sxs-lookup"><span data-stu-id="86de4-327">Initialize database credentials</span></span>
<span data-ttu-id="86de4-328">Initialize your database connection settings in the following variables:</span><span class="sxs-lookup"><span data-stu-id="86de4-328">Initialize your database connection settings in the following variables:</span></span>

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database driver>

### <a name="create-database-connection"></a><span data-ttu-id="86de4-329">Create database connection</span><span class="sxs-lookup"><span data-stu-id="86de4-329">Create database connection</span></span>
<span data-ttu-id="86de4-330">Here is the connection string that creates the connection to the database.</span><span class="sxs-lookup"><span data-stu-id="86de4-330">Here is the connection string that creates the connection to the database.</span></span>

    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a><span data-ttu-id="86de4-331">Report number of rows and columns in table <nyctaxi_trip></span><span class="sxs-lookup"><span data-stu-id="86de4-331">Report number of rows and columns in table <nyctaxi_trip></span></span>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('<nyctaxi_trip>') AND table_schema = ('<schemaname>')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* <span data-ttu-id="86de4-332">Total number of rows = 173179759</span><span class="sxs-lookup"><span data-stu-id="86de4-332">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="86de4-333">Total number of columns = 14</span><span class="sxs-lookup"><span data-stu-id="86de4-333">Total number of columns = 14</span></span>

### <a name="report-number-of-rows-and-columns-in-table-nyctaxifare"></a><span data-ttu-id="86de4-334">Report number of rows and columns in table <nyctaxi_fare></span><span class="sxs-lookup"><span data-stu-id="86de4-334">Report number of rows and columns in table <nyctaxi_fare></span></span>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_fare>')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('<nyctaxi_fare>') AND table_schema = ('<schemaname>')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* <span data-ttu-id="86de4-335">Total number of rows = 173179759</span><span class="sxs-lookup"><span data-stu-id="86de4-335">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="86de4-336">Total number of columns = 11</span><span class="sxs-lookup"><span data-stu-id="86de4-336">Total number of columns = 11</span></span>

### <a name="read-in-a-small-data-sample-from-the-sql-data-warehouse-database"></a><span data-ttu-id="86de4-337">Read-in a small data sample from the SQL Data Warehouse Database</span><span class="sxs-lookup"><span data-stu-id="86de4-337">Read-in a small data sample from the SQL Data Warehouse Database</span></span>
    t0 = time.time()

    query = '''
        SELECT TOP 10000 t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax,
            f.tolls_amount, f.total_amount, f.tip_amount
        FROM <schemaname>.<nyctaxi_trip> t, <schemaname>.<nyctaxi_fare> f
        WHERE datepart("mi",t.pickup_datetime) = 1
        AND   t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
    '''

    df1 = pd.read_sql(query, conn)

    t1 = time.time()
    print 'Time to read the sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

<span data-ttu-id="86de4-338">Time to read the sample table is 14.096495 seconds.</span><span class="sxs-lookup"><span data-stu-id="86de4-338">Time to read the sample table is 14.096495 seconds.</span></span>  
<span data-ttu-id="86de4-339">Number of rows and columns retrieved = (1000, 21).</span><span class="sxs-lookup"><span data-stu-id="86de4-339">Number of rows and columns retrieved = (1000, 21).</span></span>

### <a name="descriptive-statistics"></a><span data-ttu-id="86de4-340">Descriptive statistics</span><span class="sxs-lookup"><span data-stu-id="86de4-340">Descriptive statistics</span></span>
<span data-ttu-id="86de4-341">Now you are ready to explore the sampled data.</span><span class="sxs-lookup"><span data-stu-id="86de4-341">Now you are ready to explore the sampled data.</span></span> <span data-ttu-id="86de4-342">We start with looking at some descriptive statistics for the **trip\_distance** (or any other fields you choose to specify).</span><span class="sxs-lookup"><span data-stu-id="86de4-342">We start with looking at some descriptive statistics for the **trip\_distance** (or any other fields you choose to specify).</span></span>

    df1['trip_distance'].describe()

### <a name="visualization-box-plot-example"></a><span data-ttu-id="86de4-343">Visualization: Box plot example</span><span class="sxs-lookup"><span data-stu-id="86de4-343">Visualization: Box plot example</span></span>
<span data-ttu-id="86de4-344">Next we look at the box plot for the trip distance to visualize the quantiles.</span><span class="sxs-lookup"><span data-stu-id="86de4-344">Next we look at the box plot for the trip distance to visualize the quantiles.</span></span>

    df1.boxplot(column='trip_distance',return_type='dict')

![Plot #1][1]

### <a name="visualization-distribution-plot-example"></a><span data-ttu-id="86de4-346">Visualization: Distribution plot example</span><span class="sxs-lookup"><span data-stu-id="86de4-346">Visualization: Distribution plot example</span></span>
<span data-ttu-id="86de4-347">Plots that visualize the distribution and a histogram for the sampled trip distances.</span><span class="sxs-lookup"><span data-stu-id="86de4-347">Plots that visualize the distribution and a histogram for the sampled trip distances.</span></span>

    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![Plot #2][2]

### <a name="visualization-bar-and-line-plots"></a><span data-ttu-id="86de4-349">Visualization: Bar and line plots</span><span class="sxs-lookup"><span data-stu-id="86de4-349">Visualization: Bar and line plots</span></span>
<span data-ttu-id="86de4-350">In this example, we bin the trip distance into five bins and visualize the binning results.</span><span class="sxs-lookup"><span data-stu-id="86de4-350">In this example, we bin the trip distance into five bins and visualize the binning results.</span></span>

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

<span data-ttu-id="86de4-351">We can plot the above bin distribution in a bar or line plot with:</span><span class="sxs-lookup"><span data-stu-id="86de4-351">We can plot the above bin distribution in a bar or line plot with:</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![Plot #3][3]

<span data-ttu-id="86de4-353">and</span><span class="sxs-lookup"><span data-stu-id="86de4-353">and</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![Plot #4][4]

### <a name="visualization-scatterplot-examples"></a><span data-ttu-id="86de4-355">Visualization: Scatterplot examples</span><span class="sxs-lookup"><span data-stu-id="86de4-355">Visualization: Scatterplot examples</span></span>
<span data-ttu-id="86de4-356">We show scatter plot between **trip\_time\_in\_secs** and **trip\_distance** to see if there is any correlation</span><span class="sxs-lookup"><span data-stu-id="86de4-356">We show scatter plot between **trip\_time\_in\_secs** and **trip\_distance** to see if there is any correlation</span></span>

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![Plot #6][6]

<span data-ttu-id="86de4-358">Similarly we can check the relationship between **rate\_code** and **trip\_distance**.</span><span class="sxs-lookup"><span data-stu-id="86de4-358">Similarly we can check the relationship between **rate\_code** and **trip\_distance**.</span></span>

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![Plot #8][8]

### <a name="data-exploration-on-sampled-data-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="86de4-360">Data exploration on sampled data using SQL queries in IPython notebook</span><span class="sxs-lookup"><span data-stu-id="86de4-360">Data exploration on sampled data using SQL queries in IPython notebook</span></span>
<span data-ttu-id="86de4-361">In this section, we explore data distributions using the sampled data which is persisted in the new table we created above.</span><span class="sxs-lookup"><span data-stu-id="86de4-361">In this section, we explore data distributions using the sampled data which is persisted in the new table we created above.</span></span> <span data-ttu-id="86de4-362">Note that similar explorations can be performed using the original tables.</span><span class="sxs-lookup"><span data-stu-id="86de4-362">Note that similar explorations can be performed using the original tables.</span></span>

#### <a name="exploration-report-number-of-rows-and-columns-in-the-sampled-table"></a><span data-ttu-id="86de4-363">Exploration: Report number of rows and columns in the sampled table</span><span class="sxs-lookup"><span data-stu-id="86de4-363">Exploration: Report number of rows and columns in the sampled table</span></span>
    nrows = pd.read_sql('''SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_sample>')''', conn)
    print 'Number of rows in sample = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''SELECT count(*) FROM information_schema.columns WHERE table_name = ('<nyctaxi_sample>') AND table_schema = '<schemaname>'''', conn)
    print 'Number of columns in sample = %d' % ncols.iloc[0,0]

#### <a name="exploration-tippednot-tripped-distribution"></a><span data-ttu-id="86de4-364">Exploration: Tipped/not tripped Distribution</span><span class="sxs-lookup"><span data-stu-id="86de4-364">Exploration: Tipped/not tripped Distribution</span></span>
    query = '''
        SELECT tipped, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tipped
        '''

    pd.read_sql(query, conn)

#### <a name="exploration-tip-class-distribution"></a><span data-ttu-id="86de4-365">Exploration: Tip class distribution</span><span class="sxs-lookup"><span data-stu-id="86de4-365">Exploration: Tip class distribution</span></span>
    query = '''
        SELECT tip_class, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tip_class
    '''

    tip_class_dist = pd.read_sql(query, conn)

#### <a name="exploration-plot-the-tip-distribution-by-class"></a><span data-ttu-id="86de4-366">Exploration: Plot the tip distribution by class</span><span class="sxs-lookup"><span data-stu-id="86de4-366">Exploration: Plot the tip distribution by class</span></span>
    tip_class_dist['tip_freq'].plot(kind='bar')

![Plot #26][26]

#### <a name="exploration-daily-distribution-of-trips"></a><span data-ttu-id="86de4-368">Exploration: Daily distribution of trips</span><span class="sxs-lookup"><span data-stu-id="86de4-368">Exploration: Daily distribution of trips</span></span>
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a><span data-ttu-id="86de4-369">Exploration: Trip distribution per medallion</span><span class="sxs-lookup"><span data-stu-id="86de4-369">Exploration: Trip distribution per medallion</span></span>
    query = '''
        SELECT medallion,count(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-by-medallion-and-hack-license"></a><span data-ttu-id="86de4-370">Exploration: Trip distribution by medallion and hack license</span><span class="sxs-lookup"><span data-stu-id="86de4-370">Exploration: Trip distribution by medallion and hack license</span></span>
    query = '''select medallion, hack_license,count(*) from <schemaname>.<nyctaxi_sample> group by medallion, hack_license'''
    pd.read_sql(query,conn)


#### <a name="exploration-trip-time-distribution"></a><span data-ttu-id="86de4-371">Exploration: Trip time distribution</span><span class="sxs-lookup"><span data-stu-id="86de4-371">Exploration: Trip time distribution</span></span>
    query = '''select trip_time_in_secs, count(*) from <schemaname>.<nyctaxi_sample> group by trip_time_in_secs order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-trip-distance-distribution"></a><span data-ttu-id="86de4-372">Exploration: Trip distance distribution</span><span class="sxs-lookup"><span data-stu-id="86de4-372">Exploration: Trip distance distribution</span></span>
    query = '''select floor(trip_distance/5)*5 as tripbin, count(*) from <schemaname>.<nyctaxi_sample> group by floor(trip_distance/5)*5 order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-payment-type-distribution"></a><span data-ttu-id="86de4-373">Exploration: Payment type distribution</span><span class="sxs-lookup"><span data-stu-id="86de4-373">Exploration: Payment type distribution</span></span>
    query = '''select payment_type,count(*) from <schemaname>.<nyctaxi_sample> group by payment_type'''
    pd.read_sql(query,conn)

#### <a name="verify-the-final-form-of-the-featurized-table"></a><span data-ttu-id="86de4-374">Verify the final form of the featurized table</span><span class="sxs-lookup"><span data-stu-id="86de4-374">Verify the final form of the featurized table</span></span>
    query = '''SELECT TOP 100 * FROM <schemaname>.<nyctaxi_sample>'''
    pd.read_sql(query,conn)

## <a name="mlmodel"></a><span data-ttu-id="86de4-375">Build models in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="86de4-375">Build models in Azure Machine Learning</span></span>
<span data-ttu-id="86de4-376">We are now ready to proceed to model building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="86de4-376">We are now ready to proceed to model building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="86de4-377">The data is ready to be used in any of the prediction problems identified earlier, namely:</span><span class="sxs-lookup"><span data-stu-id="86de4-377">The data is ready to be used in any of the prediction problems identified earlier, namely:</span></span>

1. <span data-ttu-id="86de4-378">**Binary classification**: To predict whether or not a tip was paid for a trip.</span><span class="sxs-lookup"><span data-stu-id="86de4-378">**Binary classification**: To predict whether or not a tip was paid for a trip.</span></span>
2. <span data-ttu-id="86de4-379">**Multiclass classification**: To predict the range of tip paid, according to the previously defined classes.</span><span class="sxs-lookup"><span data-stu-id="86de4-379">**Multiclass classification**: To predict the range of tip paid, according to the previously defined classes.</span></span>
3. <span data-ttu-id="86de4-380">**Regression task**: To predict the amount of tip paid for a trip.</span><span class="sxs-lookup"><span data-stu-id="86de4-380">**Regression task**: To predict the amount of tip paid for a trip.</span></span>  

<span data-ttu-id="86de4-381">To begin the modeling exercise, log in to your **Azure Machine Learning** workspace.</span><span class="sxs-lookup"><span data-stu-id="86de4-381">To begin the modeling exercise, log in to your **Azure Machine Learning** workspace.</span></span> <span data-ttu-id="86de4-382">If you have not yet created a machine learning workspace, see [Create an Azure ML workspace](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="86de4-382">If you have not yet created a machine learning workspace, see [Create an Azure ML workspace](machine-learning-create-workspace.md).</span></span>

1. <span data-ttu-id="86de4-383">To get started with Azure Machine Learning, see [What is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span><span class="sxs-lookup"><span data-stu-id="86de4-383">To get started with Azure Machine Learning, see [What is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span></span>
2. <span data-ttu-id="86de4-384">Log in to [Azure Machine Learning Studio](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="86de4-384">Log in to [Azure Machine Learning Studio](https://studio.azureml.net).</span></span>
3. <span data-ttu-id="86de4-385">The Studio Home page provides a wealth of information, videos, tutorials, links to the Modules Reference, and other resources.</span><span class="sxs-lookup"><span data-stu-id="86de4-385">The Studio Home page provides a wealth of information, videos, tutorials, links to the Modules Reference, and other resources.</span></span> <span data-ttu-id="86de4-386">For more information about Azure Machine Learning, consult the [Azure Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="86de4-386">For more information about Azure Machine Learning, consult the [Azure Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

<span data-ttu-id="86de4-387">A typical training experiment consists of the following steps:</span><span class="sxs-lookup"><span data-stu-id="86de4-387">A typical training experiment consists of the following steps:</span></span>

1. <span data-ttu-id="86de4-388">Create a **+NEW** experiment.</span><span class="sxs-lookup"><span data-stu-id="86de4-388">Create a **+NEW** experiment.</span></span>
2. <span data-ttu-id="86de4-389">Get the data into Azure ML.</span><span class="sxs-lookup"><span data-stu-id="86de4-389">Get the data into Azure ML.</span></span>
3. <span data-ttu-id="86de4-390">Pre-process, transform and manipulate the data as needed.</span><span class="sxs-lookup"><span data-stu-id="86de4-390">Pre-process, transform and manipulate the data as needed.</span></span>
4. <span data-ttu-id="86de4-391">Generate features as needed.</span><span class="sxs-lookup"><span data-stu-id="86de4-391">Generate features as needed.</span></span>
5. <span data-ttu-id="86de4-392">Split the data into training/validation/testing datasets(or have separate datasets for each).</span><span class="sxs-lookup"><span data-stu-id="86de4-392">Split the data into training/validation/testing datasets(or have separate datasets for each).</span></span>
6. <span data-ttu-id="86de4-393">Select one or more machine learning algorithms depending on the learning problem to solve.</span><span class="sxs-lookup"><span data-stu-id="86de4-393">Select one or more machine learning algorithms depending on the learning problem to solve.</span></span> <span data-ttu-id="86de4-394">E.g., binary classification, multiclass classification, regression.</span><span class="sxs-lookup"><span data-stu-id="86de4-394">E.g., binary classification, multiclass classification, regression.</span></span>
7. <span data-ttu-id="86de4-395">Train one or more models using the training dataset.</span><span class="sxs-lookup"><span data-stu-id="86de4-395">Train one or more models using the training dataset.</span></span>
8. <span data-ttu-id="86de4-396">Score the validation dataset using the trained model(s).</span><span class="sxs-lookup"><span data-stu-id="86de4-396">Score the validation dataset using the trained model(s).</span></span>
9. <span data-ttu-id="86de4-397">Evaluate the model(s) to compute the relevant metrics for the learning problem.</span><span class="sxs-lookup"><span data-stu-id="86de4-397">Evaluate the model(s) to compute the relevant metrics for the learning problem.</span></span>
10. <span data-ttu-id="86de4-398">Fine tune the model(s) and select the best model to deploy.</span><span class="sxs-lookup"><span data-stu-id="86de4-398">Fine tune the model(s) and select the best model to deploy.</span></span>

<span data-ttu-id="86de4-399">In this exercise, we have already explored and engineered the data in SQL Data Warehouse, and decided on the sample size to ingest in Azure ML.</span><span class="sxs-lookup"><span data-stu-id="86de4-399">In this exercise, we have already explored and engineered the data in SQL Data Warehouse, and decided on the sample size to ingest in Azure ML.</span></span> <span data-ttu-id="86de4-400">Here is the procedure to build one or more of the prediction models:</span><span class="sxs-lookup"><span data-stu-id="86de4-400">Here is the procedure to build one or more of the prediction models:</span></span>

1. <span data-ttu-id="86de4-401">Get the data into Azure ML using the [Import Data][import-data] module, available in the **Data Input and Output** section.</span><span class="sxs-lookup"><span data-stu-id="86de4-401">Get the data into Azure ML using the [Import Data][import-data] module, available in the **Data Input and Output** section.</span></span> <span data-ttu-id="86de4-402">For more information, see the [Import Data][import-data] module reference page.</span><span class="sxs-lookup"><span data-stu-id="86de4-402">For more information, see the [Import Data][import-data] module reference page.</span></span>
   
    ![Azure ML Import Data][17]
2. <span data-ttu-id="86de4-404">Select **Azure SQL Database** as the **Data source** in the **Properties** panel.</span><span class="sxs-lookup"><span data-stu-id="86de4-404">Select **Azure SQL Database** as the **Data source** in the **Properties** panel.</span></span>
3. <span data-ttu-id="86de4-405">Enter the database DNS name in the **Database server name** field.</span><span class="sxs-lookup"><span data-stu-id="86de4-405">Enter the database DNS name in the **Database server name** field.</span></span> <span data-ttu-id="86de4-406">Format: `tcp:<your_virtual_machine_DNS_name>,1433`</span><span class="sxs-lookup"><span data-stu-id="86de4-406">Format: `tcp:<your_virtual_machine_DNS_name>,1433`</span></span>
4. <span data-ttu-id="86de4-407">Enter the **Database name** in the corresponding field.</span><span class="sxs-lookup"><span data-stu-id="86de4-407">Enter the **Database name** in the corresponding field.</span></span>
5. <span data-ttu-id="86de4-408">Enter the *SQL user name* in the **Server user account name**, and the *password* in the **Server user account password**.</span><span class="sxs-lookup"><span data-stu-id="86de4-408">Enter the *SQL user name* in the **Server user account name**, and the *password* in the **Server user account password**.</span></span>
6. <span data-ttu-id="86de4-409">Check the **Accept any server certificate** option.</span><span class="sxs-lookup"><span data-stu-id="86de4-409">Check the **Accept any server certificate** option.</span></span>
7. <span data-ttu-id="86de4-410">In the **Database query** edit text area, paste the query which extracts the necessary database fields (including any computed fields such as the labels) and down samples the data to the desired sample size.</span><span class="sxs-lookup"><span data-stu-id="86de4-410">In the **Database query** edit text area, paste the query which extracts the necessary database fields (including any computed fields such as the labels) and down samples the data to the desired sample size.</span></span>

<span data-ttu-id="86de4-411">An example of a binary classification experiment reading data directly from the SQL Data Warehouse database is in the figure below (remember to replace the table names nyctaxi_trip and nyctaxi_fare by the schema name and the table names you used in your walkthrough).</span><span class="sxs-lookup"><span data-stu-id="86de4-411">An example of a binary classification experiment reading data directly from the SQL Data Warehouse database is in the figure below (remember to replace the table names nyctaxi_trip and nyctaxi_fare by the schema name and the table names you used in your walkthrough).</span></span> <span data-ttu-id="86de4-412">Similar experiments can be constructed for multiclass classification and regression problems.</span><span class="sxs-lookup"><span data-stu-id="86de4-412">Similar experiments can be constructed for multiclass classification and regression problems.</span></span>

![Azure ML Train][10]

> [!IMPORTANT]
> <span data-ttu-id="86de4-414">In the modeling data extraction and sampling query examples provided in previous sections, **all labels for the three modeling exercises are included in the query**.</span><span class="sxs-lookup"><span data-stu-id="86de4-414">In the modeling data extraction and sampling query examples provided in previous sections, **all labels for the three modeling exercises are included in the query**.</span></span> <span data-ttu-id="86de4-415">An important (required) step in each of the modeling exercises is to **exclude** the unnecessary labels for the other two problems, and any other **target leaks**.</span><span class="sxs-lookup"><span data-stu-id="86de4-415">An important (required) step in each of the modeling exercises is to **exclude** the unnecessary labels for the other two problems, and any other **target leaks**.</span></span> <span data-ttu-id="86de4-416">For example, when using binary classification, use the label **tipped** and exclude the fields **tip\_class**, **tip\_amount**, and **total\_amount**.</span><span class="sxs-lookup"><span data-stu-id="86de4-416">For example, when using binary classification, use the label **tipped** and exclude the fields **tip\_class**, **tip\_amount**, and **total\_amount**.</span></span> <span data-ttu-id="86de4-417">The latter are target leaks since they imply the tip paid.</span><span class="sxs-lookup"><span data-stu-id="86de4-417">The latter are target leaks since they imply the tip paid.</span></span>
> 
> <span data-ttu-id="86de4-418">To exclude any unnecessary columns or target leaks, you may use the [Select Columns in Dataset][select-columns] module or the [Edit Metadata][edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="86de4-418">To exclude any unnecessary columns or target leaks, you may use the [Select Columns in Dataset][select-columns] module or the [Edit Metadata][edit-metadata].</span></span> <span data-ttu-id="86de4-419">For more information, see [Select Columns in Dataset][select-columns] and [Edit Metadata][edit-metadata] reference pages.</span><span class="sxs-lookup"><span data-stu-id="86de4-419">For more information, see [Select Columns in Dataset][select-columns] and [Edit Metadata][edit-metadata] reference pages.</span></span>
> 
> 

## <a name="mldeploy"></a><span data-ttu-id="86de4-420">Deploy models in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="86de4-420">Deploy models in Azure Machine Learning</span></span>
<span data-ttu-id="86de4-421">When your model is ready, you can easily deploy it as a web service directly from the experiment.</span><span class="sxs-lookup"><span data-stu-id="86de4-421">When your model is ready, you can easily deploy it as a web service directly from the experiment.</span></span> <span data-ttu-id="86de4-422">For more information about deploying Azure ML web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="86de4-422">For more information about deploying Azure ML web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="86de4-423">To deploy a new web service, you need to:</span><span class="sxs-lookup"><span data-stu-id="86de4-423">To deploy a new web service, you need to:</span></span>

1. <span data-ttu-id="86de4-424">Create a scoring experiment.</span><span class="sxs-lookup"><span data-stu-id="86de4-424">Create a scoring experiment.</span></span>
2. <span data-ttu-id="86de4-425">Deploy the web service.</span><span class="sxs-lookup"><span data-stu-id="86de4-425">Deploy the web service.</span></span>

<span data-ttu-id="86de4-426">To create a scoring experiment from a **Finished** training experiment, click **CREATE SCORING EXPERIMENT** in the lower action bar.</span><span class="sxs-lookup"><span data-stu-id="86de4-426">To create a scoring experiment from a **Finished** training experiment, click **CREATE SCORING EXPERIMENT** in the lower action bar.</span></span>

![Azure Scoring][18]

<span data-ttu-id="86de4-428">Azure Machine Learning will attempt to create a scoring experiment based on the components of the training experiment.</span><span class="sxs-lookup"><span data-stu-id="86de4-428">Azure Machine Learning will attempt to create a scoring experiment based on the components of the training experiment.</span></span> <span data-ttu-id="86de4-429">In particular, it will:</span><span class="sxs-lookup"><span data-stu-id="86de4-429">In particular, it will:</span></span>

1. <span data-ttu-id="86de4-430">Save the trained model and remove the model training modules.</span><span class="sxs-lookup"><span data-stu-id="86de4-430">Save the trained model and remove the model training modules.</span></span>
2. <span data-ttu-id="86de4-431">Identify a logical **input port** to represent the expected input data schema.</span><span class="sxs-lookup"><span data-stu-id="86de4-431">Identify a logical **input port** to represent the expected input data schema.</span></span>
3. <span data-ttu-id="86de4-432">Identify a logical **output port** to represent the expected web service output schema.</span><span class="sxs-lookup"><span data-stu-id="86de4-432">Identify a logical **output port** to represent the expected web service output schema.</span></span>

<span data-ttu-id="86de4-433">When the scoring experiment is created, review it and make adjust as needed.</span><span class="sxs-lookup"><span data-stu-id="86de4-433">When the scoring experiment is created, review it and make adjust as needed.</span></span> <span data-ttu-id="86de4-434">A typical adjustment is to replace the input dataset and/or query with one which excludes label fields, as these will not be available when the service is called.</span><span class="sxs-lookup"><span data-stu-id="86de4-434">A typical adjustment is to replace the input dataset and/or query with one which excludes label fields, as these will not be available when the service is called.</span></span> <span data-ttu-id="86de4-435">It is also a good practice to reduce the size of the input dataset and/or query to a few records, just enough to indicate the input schema.</span><span class="sxs-lookup"><span data-stu-id="86de4-435">It is also a good practice to reduce the size of the input dataset and/or query to a few records, just enough to indicate the input schema.</span></span> <span data-ttu-id="86de4-436">For the output port, it is common to exclude all input fields and only include the **Scored Labels** and **Scored Probabilities** in the output using the [Select Columns in Dataset][select-columns] module.</span><span class="sxs-lookup"><span data-stu-id="86de4-436">For the output port, it is common to exclude all input fields and only include the **Scored Labels** and **Scored Probabilities** in the output using the [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="86de4-437">A sample scoring experiment is provided in the figure below.</span><span class="sxs-lookup"><span data-stu-id="86de4-437">A sample scoring experiment is provided in the figure below.</span></span> <span data-ttu-id="86de4-438">When ready to deploy, click the **PUBLISH WEB SERVICE** button in the lower action bar.</span><span class="sxs-lookup"><span data-stu-id="86de4-438">When ready to deploy, click the **PUBLISH WEB SERVICE** button in the lower action bar.</span></span>

![Azure ML Publish][11]

## <a name="summary"></a><span data-ttu-id="86de4-440">Summary</span><span class="sxs-lookup"><span data-stu-id="86de4-440">Summary</span></span>
<span data-ttu-id="86de4-441">To recap what we have done in this walkthrough tutorial, you have created an Azure data science environment, worked with a large public dataset, taking it through the Team Data Science Process, all the way from data acquisition to model training, and then to the deployment of an Azure Machine Learning web service.</span><span class="sxs-lookup"><span data-stu-id="86de4-441">To recap what we have done in this walkthrough tutorial, you have created an Azure data science environment, worked with a large public dataset, taking it through the Team Data Science Process, all the way from data acquisition to model training, and then to the deployment of an Azure Machine Learning web service.</span></span>

### <a name="license-information"></a><span data-ttu-id="86de4-442">License information</span><span class="sxs-lookup"><span data-stu-id="86de4-442">License information</span></span>
<span data-ttu-id="86de4-443">This sample walkthrough and its accompanying scripts and IPython notebook(s) are shared by Microsoft under the MIT license.</span><span class="sxs-lookup"><span data-stu-id="86de4-443">This sample walkthrough and its accompanying scripts and IPython notebook(s) are shared by Microsoft under the MIT license.</span></span> <span data-ttu-id="86de4-444">Please check the LICENSE.txt file in in the directory of the sample code on GitHub for more details.</span><span class="sxs-lookup"><span data-stu-id="86de4-444">Please check the LICENSE.txt file in in the directory of the sample code on GitHub for more details.</span></span>

## <a name="references"></a><span data-ttu-id="86de4-445">References</span><span class="sxs-lookup"><span data-stu-id="86de4-445">References</span></span>
<span data-ttu-id="86de4-446">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="86de4-446">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="86de4-447">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="86de4-447">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="86de4-448">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="86de4-448">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_26_1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_28_1.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_35_1.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_36_1.png
[5]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_39_1.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_42_1.png
[7]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_44_1.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_46_1.png
[9]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_71_1.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-sqldw-walkthrough/azuremltrain.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-sqldw-walkthrough/azuremlpublish.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-sqldw-walkthrough/ssmsconnect.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-sqldw-walkthrough/executescript.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-sqldw-walkthrough/sqlserverproperties.png
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-sqldw-walkthrough/sqldefaultdirs.png
[16]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-sqldw-walkthrough/bulkimport.png
[17]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-sqldw-walkthrough/amlreader.png
[18]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-sqldw-walkthrough/amlscoring.png
[19]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-sqldw-walkthrough/ps_download_scripts.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-sqldw-walkthrough/ps_load_data.png
[21]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-sqldw-walkthrough/azcopy-overwrite.png
[22]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-1.png
[23]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-2.png
[24]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-3.png
[25]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-4.png
[26]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-sqldw-walkthrough/tip_class_hist_1.png


<!-- Module References -->
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/






















