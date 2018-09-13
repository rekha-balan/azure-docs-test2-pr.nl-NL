---
title: Generate recommendations using Mahout HDInsight from PowerShell | Microsoft Docs
description: Learn how to use the Apache Mahout machine learning library to generate movie recommendations with HDInsight (Hadoop) from a PowerShell script running on your client.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 07b57208-32aa-4e59-900a-6c934fa1b7a7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/14/2017
ms.author: larryfr
ms.openlocfilehash: f6983fe8a1d5620c30baf61f7c77785df37e498a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548889"
---
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-hadoop-in-hdinsight-powershell"></a><span data-ttu-id="5da99-103">Generate movie recommendations by using Apache Mahout with Hadoop in HDInsight (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="5da99-103">Generate movie recommendations by using Apache Mahout with Hadoop in HDInsight (PowerShell)</span></span>

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

<span data-ttu-id="5da99-104">Learn how to use the [Apache Mahout](http://mahout.apache.org) machine learning library with Azure HDInsight to generate movie recommendations.</span><span class="sxs-lookup"><span data-stu-id="5da99-104">Learn how to use the [Apache Mahout](http://mahout.apache.org) machine learning library with Azure HDInsight to generate movie recommendations.</span></span> <span data-ttu-id="5da99-105">The example in this document uses Azure PowerShell to run Mahout jobs.</span><span class="sxs-lookup"><span data-stu-id="5da99-105">The example in this document uses Azure PowerShell to run Mahout jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5da99-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5da99-106">Prerequisites</span></span>

* <span data-ttu-id="5da99-107">A Linux-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="5da99-107">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="5da99-108">For information about creating one, see [Get started using Linux-based Hadoop in HDInsight][getstarted].</span><span class="sxs-lookup"><span data-stu-id="5da99-108">For information about creating one, see [Get started using Linux-based Hadoop in HDInsight][getstarted].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5da99-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="5da99-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5da99-110">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="5da99-110">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

* [<span data-ttu-id="5da99-111">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5da99-111">Azure PowerShell</span></span>](https://docs.microsoft.com/powershell/azure/overview)

## <a name="recommendations"></a><span data-ttu-id="5da99-112">Generate recommendations by using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5da99-112">Generate recommendations by using Azure PowerShell</span></span>

> [!WARNING]
> <span data-ttu-id="5da99-113">The job in this section works by using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5da99-113">The job in this section works by using Azure PowerShell.</span></span> <span data-ttu-id="5da99-114">Many of the classes provided with Mahout do not currently work with Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5da99-114">Many of the classes provided with Mahout do not currently work with Azure PowerShell.</span></span> <span data-ttu-id="5da99-115">For a list of classes that do not work with Azure PowerShell, see the [Troubleshooting](#troubleshooting) section.</span><span class="sxs-lookup"><span data-stu-id="5da99-115">For a list of classes that do not work with Azure PowerShell, see the [Troubleshooting](#troubleshooting) section.</span></span>
>
> <span data-ttu-id="5da99-116">For an example of using SSH to connect to HDInsight and run Mahout examples directly on the cluster, see [Generate movie recommendations using Mahout and HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="5da99-116">For an example of using SSH to connect to HDInsight and run Mahout examples directly on the cluster, see [Generate movie recommendations using Mahout and HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span></span>

<span data-ttu-id="5da99-117">One of the functions that is provided by Mahout is a recommendation engine.</span><span class="sxs-lookup"><span data-stu-id="5da99-117">One of the functions that is provided by Mahout is a recommendation engine.</span></span> <span data-ttu-id="5da99-118">This engine accepts data in the format of `userID`, `itemId`, and `prefValue` (the users preference for the item).</span><span class="sxs-lookup"><span data-stu-id="5da99-118">This engine accepts data in the format of `userID`, `itemId`, and `prefValue` (the users preference for the item).</span></span> <span data-ttu-id="5da99-119">Mahout uses the data to determine users with like-item preferences, which can be used to make recommendations.</span><span class="sxs-lookup"><span data-stu-id="5da99-119">Mahout uses the data to determine users with like-item preferences, which can be used to make recommendations.</span></span>

<span data-ttu-id="5da99-120">The following example is a simplified walk-through of how the recommendation process works:</span><span class="sxs-lookup"><span data-stu-id="5da99-120">The following example is a simplified walk-through of how the recommendation process works:</span></span>

* <span data-ttu-id="5da99-121">**co-occurrence**: Joe, Alice, and Bob all liked *Star Wars*, *The Empire Strikes Back*, and *Return of the Jedi*.</span><span class="sxs-lookup"><span data-stu-id="5da99-121">**co-occurrence**: Joe, Alice, and Bob all liked *Star Wars*, *The Empire Strikes Back*, and *Return of the Jedi*.</span></span> <span data-ttu-id="5da99-122">Mahout determines that users who like any one of these movies also like the other two.</span><span class="sxs-lookup"><span data-stu-id="5da99-122">Mahout determines that users who like any one of these movies also like the other two.</span></span>

* <span data-ttu-id="5da99-123">**co-occurrence**: Bob and Alice also liked *The Phantom Menace*, *Attack of the Clones*, and *Revenge of the Sith*.</span><span class="sxs-lookup"><span data-stu-id="5da99-123">**co-occurrence**: Bob and Alice also liked *The Phantom Menace*, *Attack of the Clones*, and *Revenge of the Sith*.</span></span> <span data-ttu-id="5da99-124">Mahout determines that users who liked the previous three movies also like these movies.</span><span class="sxs-lookup"><span data-stu-id="5da99-124">Mahout determines that users who liked the previous three movies also like these movies.</span></span>

* <span data-ttu-id="5da99-125">**Similarity recommendation**: Because Joe liked the first three movies, Mahout looks at movies that others with similar preferences liked, but Joe has not watched (liked/rated).</span><span class="sxs-lookup"><span data-stu-id="5da99-125">**Similarity recommendation**: Because Joe liked the first three movies, Mahout looks at movies that others with similar preferences liked, but Joe has not watched (liked/rated).</span></span> <span data-ttu-id="5da99-126">In this case, Mahout recommends *The Phantom Menace*, *Attack of the Clones*, and *Revenge of the Sith*.</span><span class="sxs-lookup"><span data-stu-id="5da99-126">In this case, Mahout recommends *The Phantom Menace*, *Attack of the Clones*, and *Revenge of the Sith*.</span></span>

### <a name="understanding-the-data"></a><span data-ttu-id="5da99-127">Understanding the data</span><span class="sxs-lookup"><span data-stu-id="5da99-127">Understanding the data</span></span>

<span data-ttu-id="5da99-128">[GroupLens Research][movielens] provides rating data for movies in a format that is compatible with Mahout.</span><span class="sxs-lookup"><span data-stu-id="5da99-128">[GroupLens Research][movielens] provides rating data for movies in a format that is compatible with Mahout.</span></span> <span data-ttu-id="5da99-129">This data is available on the default storage for your cluster at `/HdiSamples//HdiSamples/MahoutMovieData`.</span><span class="sxs-lookup"><span data-stu-id="5da99-129">This data is available on the default storage for your cluster at `/HdiSamples//HdiSamples/MahoutMovieData`.</span></span>

<span data-ttu-id="5da99-130">There are two files, `moviedb.txt` (information about the movies) and `user-ratings.txt`.</span><span class="sxs-lookup"><span data-stu-id="5da99-130">There are two files, `moviedb.txt` (information about the movies) and `user-ratings.txt`.</span></span> <span data-ttu-id="5da99-131">The `user-ratings.txt` file is used during analysis.</span><span class="sxs-lookup"><span data-stu-id="5da99-131">The `user-ratings.txt` file is used during analysis.</span></span> <span data-ttu-id="5da99-132">The `moviedb.txt` file is used to provide user-friendly text when displaying the results of the analysis.</span><span class="sxs-lookup"><span data-stu-id="5da99-132">The `moviedb.txt` file is used to provide user-friendly text when displaying the results of the analysis.</span></span>

<span data-ttu-id="5da99-133">The data contained in user-ratings.txt has a structure of `userID`, `movieID`, `userRating`, and `timestamp`, which tells us how highly each user rated a movie.</span><span class="sxs-lookup"><span data-stu-id="5da99-133">The data contained in user-ratings.txt has a structure of `userID`, `movieID`, `userRating`, and `timestamp`, which tells us how highly each user rated a movie.</span></span> <span data-ttu-id="5da99-134">Here is an example of the data:</span><span class="sxs-lookup"><span data-stu-id="5da99-134">Here is an example of the data:</span></span>

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

### <a name="run-the-job"></a><span data-ttu-id="5da99-135">Run the job</span><span class="sxs-lookup"><span data-stu-id="5da99-135">Run the job</span></span>

<span data-ttu-id="5da99-136">Use the following Windows PowerShell script to run a job that uses the Mahout recommendation engine with the movie data:</span><span class="sxs-lookup"><span data-stu-id="5da99-136">Use the following Windows PowerShell script to run a job that uses the Mahout recommendation engine with the movie data:</span></span>

> [!NOTE]
> <span data-ttu-id="5da99-137">This file prompts you for information that is used to connect to your HDInsight cluster and run jobs.</span><span class="sxs-lookup"><span data-stu-id="5da99-137">This file prompts you for information that is used to connect to your HDInsight cluster and run jobs.</span></span> <span data-ttu-id="5da99-138">It may take several minutes for the jobs to complete and download the output.txt file.</span><span class="sxs-lookup"><span data-stu-id="5da99-138">It may take several minutes for the jobs to complete and download the output.txt file.</span></span>

```powershell
# Login to your Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter the HDInsight cluster name"
$creds=Get-Credential -UserName "admin" -Message "Enter the login for the cluster"

#Get the cluster info so we can get the resource group, storage, etc.
$clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroup = $clusterInfo.ResourceGroup
$storageAccountName = $clusterInfo.DefaultStorageAccount.split('.')[0]
$container = $clusterInfo.DefaultStorageContainer
$storageAccountKey = (Get-AzureRmStorageAccountKey `
    -Name $storageAccountName `
-ResourceGroupName $resourceGroup)[0].Value

#Create a storage context and upload the file
$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey $storageAccountKey

#Use Hive to figure out the path to the mahout examples
#Because the file name/path has a version number in it that changes
$queryString = "!ls /usr/hdp/current/mahout-client"
$hiveJobDefinition = New-AzureRmHDInsightHiveJobDefinition -Query $queryString
$hiveJob=Start-AzureRmHDInsightJob -ClusterName $clusterName -JobDefinition $hiveJobDefinition -HttpCredential $creds
wait-azurermhdinsightjob -ClusterName $clusterName -JobId $hiveJob.JobId -HttpCredential $creds > $null
#Get the files returned from Hive
$files=get-azurermhdinsightjoboutput -clustername $clusterName -JobId $hiveJob.JobId -DefaultContainer $container -DefaultStorageAccountName $storageAccountName -DefaultStorageAccountKey $storageAccountKey -HttpCredential $creds
#Find the file that starts with mahout-examples and ends in job.jar
$jarFile = $files | select-string "mahout-examples.+job\.jar" | % {$_.Matches.Value}
#Add the full path
$jarFile = "file:///usr/hdp/current/mahout-client/$jarFile"

# The arguments for the mahout job
# * input - the path to the data uploaded to HDInsight
# * output - the path to store output data
# * tempDir - the directory for temp files
$jobArguments = "-s", "SIMILARITY_COOCCURRENCE", `
                "--input", "/HdiSamples/HdiSamples/MahoutMovieData/user-ratings.txt",
                "--output", "/example/out",
                "--tempDir", "/example/temp"

# Create the job definition
$jobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
    -JarFile $jarFile `
    -ClassName "org.apache.mahout.cf.taste.hadoop.item.RecommenderJob" `
    -Arguments $jobArguments

# Start the job
$job = Start-AzureRmHDInsightJob `
    -ClusterName $clusterName `
    -JobDefinition $jobDefinition `
    -HttpCredential $creds

# Wait on the job to complete
Write-Host "Wait for the job to complete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
        -ClusterName $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds

# Write out any error information
Write-Host "STDERR"
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError

# Download the output
Get-AzureStorageBlobContent `
        -Blob example/out/part-r-00000 `
        -Container $container `
        -Destination output.txt `
        -Context $context
#Download movie and user files for use in displaying results
Get-AzureStorageBlobContent -blob "HdiSamples/HdiSamples/MahoutMovieData/moviedb.txt" `
        -Container $container `
        -Destination moviedb.txt `
        -Context $context
Get-AzureStorageBlobContent -blob "HdiSamples/HdiSamples/MahoutMovieData/user-ratings.txt" `
        -Container $container `
        -Destination user-ratings.txt `
        -Context $context
```

> [!NOTE]
> <span data-ttu-id="5da99-139">Mahout jobs do not remove temporary data that is created while processing the job.</span><span class="sxs-lookup"><span data-stu-id="5da99-139">Mahout jobs do not remove temporary data that is created while processing the job.</span></span> <span data-ttu-id="5da99-140">The `--tempDir` parameter is specified in the example job to isolate the temporary files into a specific directory.</span><span class="sxs-lookup"><span data-stu-id="5da99-140">The `--tempDir` parameter is specified in the example job to isolate the temporary files into a specific directory.</span></span>

<span data-ttu-id="5da99-141">The Mahout job does not return the output to STDOUT.</span><span class="sxs-lookup"><span data-stu-id="5da99-141">The Mahout job does not return the output to STDOUT.</span></span> <span data-ttu-id="5da99-142">Instead, it stores it in the specified output directory as **part-r-00000**.</span><span class="sxs-lookup"><span data-stu-id="5da99-142">Instead, it stores it in the specified output directory as **part-r-00000**.</span></span> <span data-ttu-id="5da99-143">The script downloads this file to **output.txt** in the current directory on your workstation.</span><span class="sxs-lookup"><span data-stu-id="5da99-143">The script downloads this file to **output.txt** in the current directory on your workstation.</span></span>

<span data-ttu-id="5da99-144">The following text is an example of the content of this file:</span><span class="sxs-lookup"><span data-stu-id="5da99-144">The following text is an example of the content of this file:</span></span>

    1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
    2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
    3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
    4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

<span data-ttu-id="5da99-145">The first column is the `userID`.</span><span class="sxs-lookup"><span data-stu-id="5da99-145">The first column is the `userID`.</span></span> <span data-ttu-id="5da99-146">The values contained in '[' and ']' are `movieId`:`recommendationScore`.</span><span class="sxs-lookup"><span data-stu-id="5da99-146">The values contained in '[' and ']' are `movieId`:`recommendationScore`.</span></span>

<span data-ttu-id="5da99-147">The script also downloads the `moviedb.txt` and `user-ratings.txt` files, which are needed to format the output to be more readable.</span><span class="sxs-lookup"><span data-stu-id="5da99-147">The script also downloads the `moviedb.txt` and `user-ratings.txt` files, which are needed to format the output to be more readable.</span></span>

### <a name="view-the-output"></a><span data-ttu-id="5da99-148">View the output</span><span class="sxs-lookup"><span data-stu-id="5da99-148">View the output</span></span>

<span data-ttu-id="5da99-149">Although the generated output might be OK for use in an application, it's not user-friendly.</span><span class="sxs-lookup"><span data-stu-id="5da99-149">Although the generated output might be OK for use in an application, it's not user-friendly.</span></span> <span data-ttu-id="5da99-150">The `moviedb.txt` from the server can be used to resolve the `movieId` to a movie name.</span><span class="sxs-lookup"><span data-stu-id="5da99-150">The `moviedb.txt` from the server can be used to resolve the `movieId` to a movie name.</span></span> <span data-ttu-id="5da99-151">Use the following PowerShell script to display recommendations with movie names:</span><span class="sxs-lookup"><span data-stu-id="5da99-151">Use the following PowerShell script to display recommendations with movie names:</span></span>

```powershell
<#
.SYNOPSIS
    Displays recommendations for movies.
.DESCRIPTION
    Displays recommendations generated by Mahout
    with HDInsight example in a human readable format.
.EXAMPLE
    .\Show-Recommendation -userId 4
        -userDataFile "user-ratings.txt"
        -movieFile "moviedb.txt"
        -recommendationFile "output.txt"
#>

[CmdletBinding(SupportsShouldProcess = $true)]
param(
    #The user ID
    [Parameter(Mandatory = $true)]
    [String]$userId,

    [Parameter(Mandatory = $true)]
    [String]$userDataFile,

    [Parameter(Mandatory = $true)]
    [String]$movieFile,

    [Parameter(Mandatory = $true)]
    [String]$recommendationFile
)
# Read movie ID & description into hash table
Write-Host "Reading movies descriptions" -ForegroundColor Green
$movieById = @{}
foreach($line in Get-Content $movieFile)
{
    $tokens = $line.Split("|")
    $movieById[$tokens[0]] = $tokens[1]
}
# Load movies user has already seen (rated)
# into a hash table
Write-Host "Reading rated movies" -ForegroundColor Green
$ratedMovieIds = @{}
foreach($line in Get-Content $userDataFile)
{
    $tokens = $line.Split("`t")
    if($tokens[0] -eq $userId)
    {
        # Resolve the ID to the movie name
        $ratedMovieIds[$movieById[$tokens[1]]] = $tokens[2]
    }
}
# Read recommendations generated by Mahout
Write-Host "Reading recommendations" -ForegroundColor Green
$recommendations = @{}
foreach($line in get-content $recommendationFile)
{
    $tokens = $line.Split("`t")
    if($tokens[0] -eq $userId)
    {
        #Trim leading/treailing [] and split at ,
        $movieIdAndScores = $tokens[1].TrimStart("[").TrimEnd("]").Split(",")
        foreach($movieIdAndScore in $movieIdAndScores)
        {
            #Split at : and store title and score in a hash table
            $idAndScore = $movieIdAndScore.Split(":")
            $recommendations[$movieById[$idAndScore[0]]] = $idAndScore[1]
        }
        break
    }
}

Write-Host "Rated movies" -ForegroundColor Green
Write-Host "---------------------------" -ForegroundColor Green
$ratedFormat = @{Expression={$_.Name};Label="Movie";Width=40}, `
                @{Expression={$_.Value};Label="Rating"}
$ratedMovieIds | format-table $ratedFormat
Write-Host "---------------------------" -ForegroundColor Green

write-host "Recommended movies" -ForegroundColor Green
Write-Host "---------------------------" -ForegroundColor Green
$recommendationFormat = @{Expression={$_.Name};Label="Movie";Width=40}, `
                        @{Expression={$_.Value};Label="Score"}
$recommendations | format-table $recommendationFormat
```

<span data-ttu-id="5da99-152">Use the following command to display the recommendations in a user-friendly format:</span><span class="sxs-lookup"><span data-stu-id="5da99-152">Use the following command to display the recommendations in a user-friendly format:</span></span> 

```powershell
.\show-recommendation.ps1 -userId 4 -userDataFile .\user-ratings.txt -movieFile .\moviedb.txt -recommendationFile .\output.txt
```

<span data-ttu-id="5da99-153">The output is similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="5da99-153">The output is similar to the following text:</span></span>

    Reading movies descriptions
    Reading rated movies
    Reading recommendations
    Rated movies
    ---------------------------
    Movie                                    Rating
    -----                                    ------
    Devil's Own, The (1997)                  1
    Alien: Resurrection (1997)               3
    187 (1997)                               2
    (lines ommitted)

    ---------------------------
    Recommended movies
    ---------------------------

    Movie                                    Score
    -----                                    -----
    Good Will Hunting (1997)                 4.6504064
    Swingers (1996)                          4.6862745
    Wings of the Dove, The (1997)            4.6666665
    People vs. Larry Flynt, The (1996)       4.834559
    Everyone Says I Love You (1996)          4.707071
    Secrets & Lies (1996)                    4.818182
    That Thing You Do! (1996)                4.75
    Grosse Pointe Blank (1997)               4.8235292
    Donnie Brasco (1997)                     4.6792455
    Lone Star (1996)                         4.7099237

## <a name="troubleshooting"></a><span data-ttu-id="5da99-154">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="5da99-154">Troubleshooting</span></span>

### <a name="cannot-overwrite-files"></a><span data-ttu-id="5da99-155">Cannot overwrite files</span><span class="sxs-lookup"><span data-stu-id="5da99-155">Cannot overwrite files</span></span>

<span data-ttu-id="5da99-156">Mahout jobs do not clean up temporary files that were created during processing.</span><span class="sxs-lookup"><span data-stu-id="5da99-156">Mahout jobs do not clean up temporary files that were created during processing.</span></span> <span data-ttu-id="5da99-157">In addition, the jobs do not overwrite existing output file.</span><span class="sxs-lookup"><span data-stu-id="5da99-157">In addition, the jobs do not overwrite existing output file.</span></span>

<span data-ttu-id="5da99-158">To avoid errors when running Mahout jobs, delete temporary and output files between runs.</span><span class="sxs-lookup"><span data-stu-id="5da99-158">To avoid errors when running Mahout jobs, delete temporary and output files between runs.</span></span> <span data-ttu-id="5da99-159">To remove the files created by the earlier scripts in this document, use the following PowerShell script:</span><span class="sxs-lookup"><span data-stu-id="5da99-159">To remove the files created by the earlier scripts in this document, use the following PowerShell script:</span></span>

```powershell
# Login to your Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter the HDInsight cluster name"
$creds=Get-Credential -Message "Enter the login for the cluster"

#Get the cluster info so we can get the resource group, storage, etc.
$clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroup = $clusterInfo.ResourceGroup
$storageAccountName = $clusterInfo.DefaultStorageAccount.split('.')[0]
$container = $clusterInfo.DefaultStorageContainer
$storageAccountKey = (Get-AzureRmStorageAccountKey `
    -Name $storageAccountName `
-ResourceGroupName $resourceGroup)[0].Value

#Create a storage context and upload the file
$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey $storageAccountKey

#Azure PowerShell can't delete blobs using wildcard,
#so have to get a list and delete one at a time
# Start with the output
$blobs = Get-AzureStorageBlob -Container $container -Context $context -Prefix "example/out"
foreach($blob in $blobs)
{
    Remove-AzureStorageBlob -Blob $blob.Name -Container $container -context $context
}
# Next the temp files
$blobs = Get-AzureStorageBlob -Container $container -Context $context -Prefix "example/temp"
foreach($blob in $blobs)
{
    Remove-AzureStorageBlob -Blob $blob.Name -Container $container -context $context
}
```

### <a name="nopowershell"></a><span data-ttu-id="5da99-160">Classes that do not work with Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5da99-160">Classes that do not work with Azure PowerShell</span></span>

<span data-ttu-id="5da99-161">Mahout jobs that use the following classes return various error messages when used from Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5da99-161">Mahout jobs that use the following classes return various error messages when used from Windows PowerShell:</span></span>

* <span data-ttu-id="5da99-162">org.apache.mahout.utils.clustering.ClusterDumper</span><span class="sxs-lookup"><span data-stu-id="5da99-162">org.apache.mahout.utils.clustering.ClusterDumper</span></span>
* <span data-ttu-id="5da99-163">org.apache.mahout.utils.SequenceFileDumper</span><span class="sxs-lookup"><span data-stu-id="5da99-163">org.apache.mahout.utils.SequenceFileDumper</span></span>
* <span data-ttu-id="5da99-164">org.apache.mahout.utils.vectors.lucene.Driver</span><span class="sxs-lookup"><span data-stu-id="5da99-164">org.apache.mahout.utils.vectors.lucene.Driver</span></span>
* <span data-ttu-id="5da99-165">org.apache.mahout.utils.vectors.arff.Driver</span><span class="sxs-lookup"><span data-stu-id="5da99-165">org.apache.mahout.utils.vectors.arff.Driver</span></span>
* <span data-ttu-id="5da99-166">org.apache.mahout.text.WikipediaToSequenceFile</span><span class="sxs-lookup"><span data-stu-id="5da99-166">org.apache.mahout.text.WikipediaToSequenceFile</span></span>
* <span data-ttu-id="5da99-167">org.apache.mahout.clustering.streaming.tools.ResplitSequenceFiles</span><span class="sxs-lookup"><span data-stu-id="5da99-167">org.apache.mahout.clustering.streaming.tools.ResplitSequenceFiles</span></span>
* <span data-ttu-id="5da99-168">org.apache.mahout.clustering.streaming.tools.ClusterQualitySummarizer</span><span class="sxs-lookup"><span data-stu-id="5da99-168">org.apache.mahout.clustering.streaming.tools.ClusterQualitySummarizer</span></span>
* <span data-ttu-id="5da99-169">org.apache.mahout.classifier.sgd.TrainLogistic</span><span class="sxs-lookup"><span data-stu-id="5da99-169">org.apache.mahout.classifier.sgd.TrainLogistic</span></span>
* <span data-ttu-id="5da99-170">org.apache.mahout.classifier.sgd.RunLogistic</span><span class="sxs-lookup"><span data-stu-id="5da99-170">org.apache.mahout.classifier.sgd.RunLogistic</span></span>
* <span data-ttu-id="5da99-171">org.apache.mahout.classifier.sgd.TrainAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="5da99-171">org.apache.mahout.classifier.sgd.TrainAdaptiveLogistic</span></span>
* <span data-ttu-id="5da99-172">org.apache.mahout.classifier.sgd.ValidateAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="5da99-172">org.apache.mahout.classifier.sgd.ValidateAdaptiveLogistic</span></span>
* <span data-ttu-id="5da99-173">org.apache.mahout.classifier.sgd.RunAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="5da99-173">org.apache.mahout.classifier.sgd.RunAdaptiveLogistic</span></span>
* <span data-ttu-id="5da99-174">org.apache.mahout.classifier.sequencelearning.hmm.BaumWelchTrainer</span><span class="sxs-lookup"><span data-stu-id="5da99-174">org.apache.mahout.classifier.sequencelearning.hmm.BaumWelchTrainer</span></span>
* <span data-ttu-id="5da99-175">org.apache.mahout.classifier.sequencelearning.hmm.ViterbiEvaluator</span><span class="sxs-lookup"><span data-stu-id="5da99-175">org.apache.mahout.classifier.sequencelearning.hmm.ViterbiEvaluator</span></span>
* <span data-ttu-id="5da99-176">org.apache.mahout.classifier.sequencelearning.hmm.RandomSequenceGenerator</span><span class="sxs-lookup"><span data-stu-id="5da99-176">org.apache.mahout.classifier.sequencelearning.hmm.RandomSequenceGenerator</span></span>
* <span data-ttu-id="5da99-177">org.apache.mahout.classifier.df.tools.Describe</span><span class="sxs-lookup"><span data-stu-id="5da99-177">org.apache.mahout.classifier.df.tools.Describe</span></span>

<span data-ttu-id="5da99-178">To run jobs that use these classes, connect to the HDInsight cluster using SSH and run the jobs from the command line.</span><span class="sxs-lookup"><span data-stu-id="5da99-178">To run jobs that use these classes, connect to the HDInsight cluster using SSH and run the jobs from the command line.</span></span> <span data-ttu-id="5da99-179">For an example of using SSH to run Mahout jobs, see [Generate movie recommendations using Mahout and HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="5da99-179">For an example of using SSH to run Mahout jobs, see [Generate movie recommendations using Mahout and HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5da99-180">Next steps</span><span class="sxs-lookup"><span data-stu-id="5da99-180">Next steps</span></span>

<span data-ttu-id="5da99-181">Now that you have learned how to use Mahout, discover other ways of working with data on HDInsight:</span><span class="sxs-lookup"><span data-stu-id="5da99-181">Now that you have learned how to use Mahout, discover other ways of working with data on HDInsight:</span></span>

* [<span data-ttu-id="5da99-182">Hive with HDInsight</span><span class="sxs-lookup"><span data-stu-id="5da99-182">Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="5da99-183">Pig with HDInsight</span><span class="sxs-lookup"><span data-stu-id="5da99-183">Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="5da99-184">MapReduce with HDInsight</span><span class="sxs-lookup"><span data-stu-id="5da99-184">MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

[build]: http://mahout.apache.org/developers/buildingmahout.html
[aps]: /powershell/azureps-cmdlets-docs
[movielens]: http://grouplens.org/datasets/movielens/
[100k]: http://files.grouplens.org/datasets/movielens/ml-100k.zip
[getstarted]: hdinsight-hadoop-linux-tutorial-get-started.md
[upload]: hdinsight-upload-data.md
[ml]: http://en.wikipedia.org/wiki/Machine_learning
[forest]: http://en.wikipedia.org/wiki/Random_forest
[management]: https://manage.windowsazure.com/
[enableremote]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-mahout/enableremote.png
[connect]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-mahout/connect.png
[hadoopcli]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-mahout/hadoopcli.png
[tools]: https://github.com/Blackmist/hdinsight-tools



