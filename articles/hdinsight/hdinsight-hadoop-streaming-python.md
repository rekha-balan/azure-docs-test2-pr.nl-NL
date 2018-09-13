---
title: Develop Python MapReduce jobs with HDInsight | Microsoft Docs
description: Learn how to create and run Python MapReduce jobs on Linux-based HDInsight clusters.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7631d8d9-98ae-42ec-b9ec-ee3cf7e57fb3
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/06/2017
ms.author: larryfr
ms.openlocfilehash: d41c7786c35b2639893defd2116120e176482f9a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550300"
---
# <a name="develop-python-streaming-programs-for-hdinsight"></a><span data-ttu-id="cf3c0-103">Develop Python streaming programs for HDInsight</span><span class="sxs-lookup"><span data-stu-id="cf3c0-103">Develop Python streaming programs for HDInsight</span></span>

<span data-ttu-id="cf3c0-104">Hadoop provides a streaming API for MapReduce that enables you to write map and reduce functions in languages other than Java.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-104">Hadoop provides a streaming API for MapReduce that enables you to write map and reduce functions in languages other than Java.</span></span> <span data-ttu-id="cf3c0-105">In this article, you will learn how to use Python to perform MapReduce operations.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-105">In this article, you will learn how to use Python to perform MapReduce operations.</span></span>

<span data-ttu-id="cf3c0-106">This article is based on information and examples published by Michael Noll at [Writing an Hadoop MapReduce Program in Python](http://www.michael-noll.com/tutorials/writing-an-hadoop-mapreduce-program-in-python/).</span><span class="sxs-lookup"><span data-stu-id="cf3c0-106">This article is based on information and examples published by Michael Noll at [Writing an Hadoop MapReduce Program in Python](http://www.michael-noll.com/tutorials/writing-an-hadoop-mapreduce-program-in-python/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cf3c0-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="cf3c0-107">Prerequisites</span></span>

<span data-ttu-id="cf3c0-108">To complete the steps in this article, you will need the following:</span><span class="sxs-lookup"><span data-stu-id="cf3c0-108">To complete the steps in this article, you will need the following:</span></span>

* <span data-ttu-id="cf3c0-109">A Linux-based Hadoop on HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="cf3c0-109">A Linux-based Hadoop on HDInsight cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="cf3c0-110">The steps in this document require an HDInsight cluster that uses Linux.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-110">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="cf3c0-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="cf3c0-112">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="cf3c0-112">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

* <span data-ttu-id="cf3c0-113">A text editor</span><span class="sxs-lookup"><span data-stu-id="cf3c0-113">A text editor</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="cf3c0-114">The text editor must use LF as the line ending.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-114">The text editor must use LF as the line ending.</span></span> <span data-ttu-id="cf3c0-115">If it uses CRLF, this will cause errors when running the MapReduce job on Linux-based HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-115">If it uses CRLF, this will cause errors when running the MapReduce job on Linux-based HDInsight clusters.</span></span> <span data-ttu-id="cf3c0-116">If you are not sure, use the optional step in the [Run MapReduce](#run-mapreduce) section to convert any CRLF to LF.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-116">If you are not sure, use the optional step in the [Run MapReduce](#run-mapreduce) section to convert any CRLF to LF.</span></span>

* <span data-ttu-id="cf3c0-117">**Familiarity with SSH and SCP**.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-117">**Familiarity with SSH and SCP**.</span></span> <span data-ttu-id="cf3c0-118">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="cf3c0-118">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="word-count"></a><span data-ttu-id="cf3c0-119">Word count</span><span class="sxs-lookup"><span data-stu-id="cf3c0-119">Word count</span></span>

<span data-ttu-id="cf3c0-120">For this example, you implement a basic word count by using a mapper and reducer.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-120">For this example, you implement a basic word count by using a mapper and reducer.</span></span> <span data-ttu-id="cf3c0-121">The mapper breaks sentences into individual words, and the reducer aggregates the words and counts to produce the output.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-121">The mapper breaks sentences into individual words, and the reducer aggregates the words and counts to produce the output.</span></span>

<span data-ttu-id="cf3c0-122">The following flowchart illustrates what happens during the map and reduce phases.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-122">The following flowchart illustrates what happens during the map and reduce phases.</span></span>

![illustration of map reduce](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-streaming-python/HDI.WordCountDiagram.png)

## <a name="why-python"></a><span data-ttu-id="cf3c0-124">Why Python?</span><span class="sxs-lookup"><span data-stu-id="cf3c0-124">Why Python?</span></span>

<span data-ttu-id="cf3c0-125">Python is a general-purpose, high-level programming language that allows you to express concepts in fewer lines of code than many other languages.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-125">Python is a general-purpose, high-level programming language that allows you to express concepts in fewer lines of code than many other languages.</span></span> <span data-ttu-id="cf3c0-126">It has recently became popular with data scientists as a prototyping language because its interpreted nature, dynamic typing, and elegant syntax make it suitable for rapid application development.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-126">It has recently became popular with data scientists as a prototyping language because its interpreted nature, dynamic typing, and elegant syntax make it suitable for rapid application development.</span></span>

<span data-ttu-id="cf3c0-127">Python is installed on all HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-127">Python is installed on all HDInsight clusters.</span></span>

## <a name="streaming-mapreduce"></a><span data-ttu-id="cf3c0-128">Streaming MapReduce</span><span class="sxs-lookup"><span data-stu-id="cf3c0-128">Streaming MapReduce</span></span>

<span data-ttu-id="cf3c0-129">Hadoop allows you to specify a file that contains the map and reduce logic that is used by a job.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-129">Hadoop allows you to specify a file that contains the map and reduce logic that is used by a job.</span></span> <span data-ttu-id="cf3c0-130">The specific requirements for the map and reduce logic are:</span><span class="sxs-lookup"><span data-stu-id="cf3c0-130">The specific requirements for the map and reduce logic are:</span></span>

* <span data-ttu-id="cf3c0-131">**Input**: The map and reduce components must read input data from STDIN.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-131">**Input**: The map and reduce components must read input data from STDIN.</span></span>
* <span data-ttu-id="cf3c0-132">**Output**: The map and reduce components must write output data to STDOUT.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-132">**Output**: The map and reduce components must write output data to STDOUT.</span></span>
* <span data-ttu-id="cf3c0-133">**Data format**: The data consumed and produced must be a key/value pair, separated by a tab character.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-133">**Data format**: The data consumed and produced must be a key/value pair, separated by a tab character.</span></span>

<span data-ttu-id="cf3c0-134">Python can easily handle these requirements by using the **sys** module to read from STDIN and using **print** to print to STDOUT.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-134">Python can easily handle these requirements by using the **sys** module to read from STDIN and using **print** to print to STDOUT.</span></span> <span data-ttu-id="cf3c0-135">The remaining task is simply formatting the data with a tab (`\t`) character between the key and value.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-135">The remaining task is simply formatting the data with a tab (`\t`) character between the key and value.</span></span>

## <a name="create-the-mapper-and-reducer"></a><span data-ttu-id="cf3c0-136">Create the mapper and reducer</span><span class="sxs-lookup"><span data-stu-id="cf3c0-136">Create the mapper and reducer</span></span>

<span data-ttu-id="cf3c0-137">The mapper and reducer are text files, in this case **mapper.py** and **reducer.py** (to make it clear which does what).</span><span class="sxs-lookup"><span data-stu-id="cf3c0-137">The mapper and reducer are text files, in this case **mapper.py** and **reducer.py** (to make it clear which does what).</span></span> <span data-ttu-id="cf3c0-138">You can create these by using the editor of your choice.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-138">You can create these by using the editor of your choice.</span></span>

### <a name="mapperpy"></a><span data-ttu-id="cf3c0-139">Mapper.py</span><span class="sxs-lookup"><span data-stu-id="cf3c0-139">Mapper.py</span></span>

<span data-ttu-id="cf3c0-140">Create a new file named **mapper.py** and use the following code as the content:</span><span class="sxs-lookup"><span data-stu-id="cf3c0-140">Create a new file named **mapper.py** and use the following code as the content:</span></span>

```python
#!/usr/bin/env python

# Use the sys module
import sys

# 'file' in this case is STDIN
def read_input(file):
    # Split each line into words
    for line in file:
        yield line.split()

def main(separator='\t'):
    # Read the data using read_input
    data = read_input(sys.stdin)
    # Process each words returned from read_input
    for words in data:
        # Process each word
        for word in words:
            # Write to STDOUT
            print '%s%s%d' % (word, separator, 1)

if __name__ == "__main__":
    main()
```

<span data-ttu-id="cf3c0-141">Take a moment to read through the code so you can understand what it does.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-141">Take a moment to read through the code so you can understand what it does.</span></span>

### <a name="reducerpy"></a><span data-ttu-id="cf3c0-142">Reducer.py</span><span class="sxs-lookup"><span data-stu-id="cf3c0-142">Reducer.py</span></span>

<span data-ttu-id="cf3c0-143">Create a new file named **reducer.py** and use the following code as the content:</span><span class="sxs-lookup"><span data-stu-id="cf3c0-143">Create a new file named **reducer.py** and use the following code as the content:</span></span>

```python
#!/usr/bin/env python

# import modules
from itertools import groupby
from operator import itemgetter
import sys

# 'file' in this case is STDIN
def read_mapper_output(file, separator='\t'):
    # Go through each line
    for line in file:
        # Strip out the separator character
        yield line.rstrip().split(separator, 1)

def main(separator='\t'):
    # Read the data using read_mapper_output
    data = read_mapper_output(sys.stdin, separator=separator)
    # Group words and counts into 'group'
    #   Since MapReduce is a distributed process, each word
    #   may have multiple counts. 'group' will have all counts
    #   which can be retrieved using the word as the key.
    for current_word, group in groupby(data, itemgetter(0)):
        try:
            # For each word, pull the count(s) for the word
            #   from 'group' and create a total count
            total_count = sum(int(count) for current_word, count in group)
            # Write to stdout
            print "%s%s%d" % (current_word, separator, total_count)
        except ValueError:
            # Count was not a number, so do nothing
            pass

if __name__ == "__main__":
    main()
```

## <a name="upload-the-files"></a><span data-ttu-id="cf3c0-144">Upload the files</span><span class="sxs-lookup"><span data-stu-id="cf3c0-144">Upload the files</span></span>

<span data-ttu-id="cf3c0-145">Both **mapper.py** and **reducer.py** must be on the head node of the cluster before we can run them.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-145">Both **mapper.py** and **reducer.py** must be on the head node of the cluster before we can run them.</span></span> <span data-ttu-id="cf3c0-146">This section provides an example `scp` command, and an Azure PowerShell script that can be used to upload the files to the cluster.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-146">This section provides an example `scp` command, and an Azure PowerShell script that can be used to upload the files to the cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cf3c0-147">There is an important difference between using `scp` and PowerShell to upload the files:</span><span class="sxs-lookup"><span data-stu-id="cf3c0-147">There is an important difference between using `scp` and PowerShell to upload the files:</span></span>
>
> * <span data-ttu-id="cf3c0-148">Using `scp` places the files on the primary head node of the cluster.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-148">Using `scp` places the files on the primary head node of the cluster.</span></span> <span data-ttu-id="cf3c0-149">This assumes that you will later connect to the head node and run the job from an SSH session.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-149">This assumes that you will later connect to the head node and run the job from an SSH session.</span></span>
> * <span data-ttu-id="cf3c0-150">Using the PowerShell script places the files into the default storage for the cluster.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-150">Using the PowerShell script places the files into the default storage for the cluster.</span></span> <span data-ttu-id="cf3c0-151">This assumes that you will later use a PowerShell script to run the job from a remote client.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-151">This assumes that you will later use a PowerShell script to run the job from a remote client.</span></span>

### <a name="upload-using-scp"></a><span data-ttu-id="cf3c0-152">Upload using scp</span><span class="sxs-lookup"><span data-stu-id="cf3c0-152">Upload using scp</span></span>

<span data-ttu-id="cf3c0-153">From your development environment, in the same directory as **mapper.py** and **reducer.py**, use the following command.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-153">From your development environment, in the same directory as **mapper.py** and **reducer.py**, use the following command.</span></span> <span data-ttu-id="cf3c0-154">Replace **username** with the SSH user name for your cluster, and **clustername** with the name of your cluster.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-154">Replace **username** with the SSH user name for your cluster, and **clustername** with the name of your cluster.</span></span>

`scp mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`

<span data-ttu-id="cf3c0-155">This copies the files from the local system to the head node.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-155">This copies the files from the local system to the head node.</span></span>

> [!NOTE]
> <span data-ttu-id="cf3c0-156">If you used a password to secure your SSH account, you will be prompted for the password.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-156">If you used a password to secure your SSH account, you will be prompted for the password.</span></span> <span data-ttu-id="cf3c0-157">If you used an SSH key, you may have to use the `-i` parameter and the path to the private key, for example, `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-157">If you used an SSH key, you may have to use the `-i` parameter and the path to the private key, for example, `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.</span></span>

### <a name="upload-using-powershell"></a><span data-ttu-id="cf3c0-158">Upload using PowerShell</span><span class="sxs-lookup"><span data-stu-id="cf3c0-158">Upload using PowerShell</span></span>

1. <span data-ttu-id="cf3c0-159">From your development environment, create a new file named `Put-FilesInHDInsight.ps1` and use the following as the contents of the file:</span><span class="sxs-lookup"><span data-stu-id="cf3c0-159">From your development environment, create a new file named `Put-FilesInHDInsight.ps1` and use the following as the contents of the file:</span></span>

    ```PowerShell
    param(
        [Parameter(Mandatory = $true)]
        [String]$clusterName,
        [Parameter(Mandatory = $true)]
        [String]$source,
        [Parameter(Mandatory = $true)]
        [String]$destination
    )
    # Login to your Azure subscription
    # Is there an active Azure subscription?
    $sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
    if(-not($sub))
    {
        Add-AzureRmAccount
    }

    # Get the cluster info
    $clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $storageInfo = $clusterInfo.DefaultStorageAccount.split('.')

    # What type of default storage are we using?
    switch ($storageInfo[1])
    {
        "blob" {
            # Get the blob storage information for the cluster
            $resourceGroup = $clusterInfo.ResourceGroup
            $storageAccountName=$storageInfo[0]
            $storageContainer=$clusterInfo.DefaultStorageContainer
            $storageAccountKey=(Get-AzureRmStorageAccountKey `
                -Name $storageAccountName `
                -ResourceGroupName $resourceGroup)[0].Value
            # Create a storage context and upload the file
            $context = New-AzureStorageContext `
                -StorageAccountName $storageAccountName `
                -StorageAccountKey $storageAccountKey
            # Upload the file
            Set-AzureStorageBlobContent `
                -File $source `
                -Blob $destination `
                -Container $storageContainer `
                -Context $context
        }
        "azuredatalakestore" {
            # Get the Data Lake Store name
            $dataLakeStoreName=$storageInfo[0]
            # Get the root of the HDInsight cluster azuredatalakestore
            $clusterRoot=$clusterInfo.DefaultStorageRootPath
            # Upload the file. Prepend the destination with the cluster root
            Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $source -Destination "$clusterRoot$destination"
        }
        default {
            Throw "Unknown storage type: $storageInfo[1]"
        }
    }
    ```

2. <span data-ttu-id="cf3c0-160">To use this script to upload a file, use the following from an Azure PowerShell prompt:</span><span class="sxs-lookup"><span data-stu-id="cf3c0-160">To use this script to upload a file, use the following from an Azure PowerShell prompt:</span></span>

    `.\Put-FilesInHDInsight.ps1 -clusterName <your HDInsight cluster name> -source mapper.py -destination mapper.py`

    <span data-ttu-id="cf3c0-161">When prompted, enter the HTTPS login credentials for your cluster.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-161">When prompted, enter the HTTPS login credentials for your cluster.</span></span>

3. <span data-ttu-id="cf3c0-162">Repeat the command, replacing `mapper.py` with `reducer.py`.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-162">Repeat the command, replacing `mapper.py` with `reducer.py`.</span></span> <span data-ttu-id="cf3c0-163">This will upload both mapper and reducer files to the default storage for the cluster.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-163">This will upload both mapper and reducer files to the default storage for the cluster.</span></span>

## <a name="run-mapreduce-ssh"></a><span data-ttu-id="cf3c0-164">Run MapReduce (SSH)</span><span class="sxs-lookup"><span data-stu-id="cf3c0-164">Run MapReduce (SSH)</span></span>

<span data-ttu-id="cf3c0-165">Use the following steps to connect to the cluster and run the streaming MapReduce job from an SSH session.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-165">Use the following steps to connect to the cluster and run the streaming MapReduce job from an SSH session.</span></span>

1. <span data-ttu-id="cf3c0-166">Connect to the cluster by using SSH:</span><span class="sxs-lookup"><span data-stu-id="cf3c0-166">Connect to the cluster by using SSH:</span></span>

   `ssh username@clustername-ssh.azurehdinsight.net`

   > [!NOTE]
   > <span data-ttu-id="cf3c0-167">If you used a password to secure your SSH account, you will be prompted for the password.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-167">If you used a password to secure your SSH account, you will be prompted for the password.</span></span> <span data-ttu-id="cf3c0-168">If you used an SSH key, you may have to use the `-i` parameter and the path to the private key, for example, `ssh -i /path/to/private/key username@clustername-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-168">If you used an SSH key, you may have to use the `-i` parameter and the path to the private key, for example, `ssh -i /path/to/private/key username@clustername-ssh.azurehdinsight.net`.</span></span>

2. <span data-ttu-id="cf3c0-169">(Optional) If you used a text editor that uses CRLF as the line ending when creating the mapper.py and reducer.py files, or do not know what line-ending your editor uses, use the following commands to convert occurrences of CRLF in mapper.py and reducer.py to LF.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-169">(Optional) If you used a text editor that uses CRLF as the line ending when creating the mapper.py and reducer.py files, or do not know what line-ending your editor uses, use the following commands to convert occurrences of CRLF in mapper.py and reducer.py to LF.</span></span>

    <span data-ttu-id="cf3c0-170">`perl -pi -e 's/\r\n/\n/g' mappery.py` `perl -pi -e 's/\r\n/\n/g' reducer.py`</span><span class="sxs-lookup"><span data-stu-id="cf3c0-170">`perl -pi -e 's/\r\n/\n/g' mappery.py` `perl -pi -e 's/\r\n/\n/g' reducer.py`</span></span>

3. <span data-ttu-id="cf3c0-171">Use the following command to start the MapReduce job.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-171">Use the following command to start the MapReduce job.</span></span>

    `yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files mapper.py,reducer.py -mapper mapper.py -reducer reducer.py -input /example/data/gutenberg/davinci.txt -output /example/wordcountout`

    <span data-ttu-id="cf3c0-172">This command has the following parts:</span><span class="sxs-lookup"><span data-stu-id="cf3c0-172">This command has the following parts:</span></span>

   * <span data-ttu-id="cf3c0-173">**hadoop-streaming.jar**: Used when performing streaming MapReduce operations.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-173">**hadoop-streaming.jar**: Used when performing streaming MapReduce operations.</span></span> <span data-ttu-id="cf3c0-174">It interfaces Hadoop with the external MapReduce code you provide.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-174">It interfaces Hadoop with the external MapReduce code you provide.</span></span>

   * <span data-ttu-id="cf3c0-175">**-files**: Tells Hadoop that the specified files are needed for this MapReduce job, and they should be copied to all the worker nodes.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-175">**-files**: Tells Hadoop that the specified files are needed for this MapReduce job, and they should be copied to all the worker nodes.</span></span>

   * <span data-ttu-id="cf3c0-176">**-mapper**: Tells Hadoop which file to use as the mapper.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-176">**-mapper**: Tells Hadoop which file to use as the mapper.</span></span>

   * <span data-ttu-id="cf3c0-177">**-reducer**: Tells Hadoop which file to use as the reducer.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-177">**-reducer**: Tells Hadoop which file to use as the reducer.</span></span>

   * <span data-ttu-id="cf3c0-178">**-input**: The input file that we should count words from.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-178">**-input**: The input file that we should count words from.</span></span>

   * <span data-ttu-id="cf3c0-179">**-output**: The directory that the output will be written to.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-179">**-output**: The directory that the output will be written to.</span></span>

     > [!NOTE]
     > <span data-ttu-id="cf3c0-180">This directory will be created by the job.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-180">This directory will be created by the job.</span></span>

<span data-ttu-id="cf3c0-181">You should see a bunch of **INFO** statements as the job starts, and finally see the **map** and **reduce** operation displayed as percentages.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-181">You should see a bunch of **INFO** statements as the job starts, and finally see the **map** and **reduce** operation displayed as percentages.</span></span>

    15/02/05 19:01:04 INFO mapreduce.Job:  map 0% reduce 0%
    15/02/05 19:01:16 INFO mapreduce.Job:  map 100% reduce 0%
    15/02/05 19:01:27 INFO mapreduce.Job:  map 100% reduce 100%

<span data-ttu-id="cf3c0-182">You will receive status information about the job when it completes.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-182">You will receive status information about the job when it completes.</span></span>

## <a name="run-mapreduce-powershell"></a><span data-ttu-id="cf3c0-183">Run MapReduce (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="cf3c0-183">Run MapReduce (PowerShell)</span></span>

<span data-ttu-id="cf3c0-184">Use the following steps to run the streaming MapReduce from PowerShell on your development environment.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-184">Use the following steps to run the streaming MapReduce from PowerShell on your development environment.</span></span> <span data-ttu-id="cf3c0-185">The PowerShell script runs the job by connecting to the HDInsight cluster using WebHCat.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-185">The PowerShell script runs the job by connecting to the HDInsight cluster using WebHCat.</span></span>

1. <span data-ttu-id="cf3c0-186">Create a new file named `Start-HDInsightStreamingPythonJob` and use the following as the contents of the file:</span><span class="sxs-lookup"><span data-stu-id="cf3c0-186">Create a new file named `Start-HDInsightStreamingPythonJob` and use the following as the contents of the file:</span></span>

    ```PowerShell
    param(
        [Parameter(Mandatory = $true)]
        [String]$clusterName,
        [Parameter(Mandatory = $true)]
        [String]$inputPath,
        [Parameter(Mandatory = $true)]
        [String]$outputPath
    )
    # Login to your Azure subscription
    # Is there an active Azure subscription?
    $sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
    if(-not($sub))
    {
        Add-AzureRmAccount
    }

    # Get the login (HTTPS) credentials for the cluster
    $creds=Get-Credential -Message "Enter the login for the cluster" -UserName "admin"

    # Create the streaming job definition
    # Note: This assumes that the mapper.py and reducer.py
    #       are in the root of default storage. If you put them in a
    #       subdirectory, change the -Files parameter to the correct path.
    $jobDefinition = New-AzureRmHDInsightStreamingMapReduceJobDefinition `
        -Files "/mapper.py", "/reducer.py" `
        -Mapper "mapper.py" `
        -Reducer "reducer.py" `
        -InputPath $inputPath `
        -OutputPath $outputPath

    # Start the job
    $job = Start-AzureRmHDInsightJob `
        -ClusterName $clusterName `
        -JobDefinition $jobDefinition `
        -HttpCredential $creds

    # Wait for the job to complete
    Wait-AzureRmHDInsightJob `
        -JobId $job.JobId `
        -ClusterName $clusterName `
        -HttpCredential $creds
    ```

2. <span data-ttu-id="cf3c0-187">Use the following from an Azure PowerShell prompt to run the job:</span><span class="sxs-lookup"><span data-stu-id="cf3c0-187">Use the following from an Azure PowerShell prompt to run the job:</span></span>

    `.\Start-HDInsightStreamingPythonJob.ps1 -clusterName <your HDInsight cluster name> -inputPath "/example/data/gutenberg/davinci.txt" -outputPath "/example/wordcountout"`

    <span data-ttu-id="cf3c0-188">This will use the `mapper.py` and `reducer.py` files previous uploaded to the cluster to count the words in the `davinci.txt` file.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-188">This will use the `mapper.py` and `reducer.py` files previous uploaded to the cluster to count the words in the `davinci.txt` file.</span></span> <span data-ttu-id="cf3c0-189">The output is stored in the `/example/wordcount` folder on the cluster's default storage.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-189">The output is stored in the `/example/wordcount` folder on the cluster's default storage.</span></span>

    <span data-ttu-id="cf3c0-190">Information similar to the following is displayed when the job completes:</span><span class="sxs-lookup"><span data-stu-id="cf3c0-190">Information similar to the following is displayed when the job completes:</span></span>

    ```
    Cluster         : myhdicluster
    HttpEndpoint    : myhdicluster.azurehdinsight.net
    State           : SUCCEEDED
    JobId           : job_1486046226168_0004
    ParentId        :
    PercentComplete : map 100% reduce 100%
    ExitValue       : 0
    User            : admin
    Callback        :
    Completed       : done
    StatusFolder    : 2017-02-06T19-14-28-a3dda3ca-f489-4287-afc9-b5e16e2e7c7a
    ```

## <a name="view-the-output"></a><span data-ttu-id="cf3c0-191">View the output</span><span class="sxs-lookup"><span data-stu-id="cf3c0-191">View the output</span></span>

<span data-ttu-id="cf3c0-192">The output of the job is stored in the `/example/wordcountout` directory.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-192">The output of the job is stored in the `/example/wordcountout` directory.</span></span> <span data-ttu-id="cf3c0-193">You can view this from either an SSH session, or download it locally and view it from PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-193">You can view this from either an SSH session, or download it locally and view it from PowerShell.</span></span>

<span data-ttu-id="cf3c0-194">To view the data from an SSH session to the cluster, use the following command:</span><span class="sxs-lookup"><span data-stu-id="cf3c0-194">To view the data from an SSH session to the cluster, use the following command:</span></span>

`hdfs dfs -text /example/wordcountout/part-00000`

<span data-ttu-id="cf3c0-195">This displays a list of words and how many times the word occurred.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-195">This displays a list of words and how many times the word occurred.</span></span> <span data-ttu-id="cf3c0-196">The following is an sample of the output data:</span><span class="sxs-lookup"><span data-stu-id="cf3c0-196">The following is an sample of the output data:</span></span>

```
wrenching       1
wretched        6
wriggling       1
wrinkled,       1
wrinkles        2
wrinkling       2
```

<span data-ttu-id="cf3c0-197">To view the output from your development environment using PowerShell, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="cf3c0-197">To view the output from your development environment using PowerShell, use the following steps:</span></span>

1. <span data-ttu-id="cf3c0-198">Create a new file named `Get-FilesInHDInsight.ps1` and use the following as the file contents:</span><span class="sxs-lookup"><span data-stu-id="cf3c0-198">Create a new file named `Get-FilesInHDInsight.ps1` and use the following as the file contents:</span></span>

    ```PowerShell
    param(
        [Parameter(Mandatory = $true)]
        [String]$clusterName,
        [Parameter(Mandatory = $true)]
        [String]$source
    )
    # Login to your Azure subscription
    # Is there an active Azure subscription?
    $sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
    if(-not($sub))
    {
        Add-AzureRmAccount
    }

    # Get the cluster info
    $clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $storageInfo = $clusterInfo.DefaultStorageAccount.split('.')

    # What type of default storage are we using?
    switch ($storageInfo[1])
    {
        "blob" {
            # Get the blob storage information for the cluster
            $resourceGroup = $clusterInfo.ResourceGroup
            $storageAccountName=$storageInfo[0]
            $storageContainer=$clusterInfo.DefaultStorageContainer
            $storageAccountKey=(Get-AzureRmStorageAccountKey `
                -Name $storageAccountName `
                -ResourceGroupName $resourceGroup)[0].Value
            # Create a storage context and download the file
            $context = New-AzureStorageContext `
                -StorageAccountName $storageAccountName `
                -StorageAccountKey $storageAccountKey
            # Download the file
            Get-AzureStorageBlobContent `
                -Container $storageContainer `
                -Blob $source `
                -Context $context `
                -Destination "./output.txt"
            # Display the output
            Get-Content "./output.txt"
        }
        "azuredatalakestore" {
            # Get the Data Lake Store name
            $dataLakeStoreName=$storageInfo[0]
            # Get the root of the HDInsight cluster azuredatalakestore
            $clusterRoot=$clusterInfo.DefaultStorageRootPath
            # Download the file. Prepend the destination with the cluster root
            # NOTE: Unlike getting a blob, this just gets the content and no
            #       file is created locally.
            Get-AzureRmDataLakeStoreItemContent -Account $dataLakeStoreName -Path $clusterRoot$source -Confirm
        }
        default {
            Throw "Unknown storage type: $storageInfo[1]"
        }
    }
    ```

2. <span data-ttu-id="cf3c0-199">From an Azure PowerShell prompt, use the following to run the script and view the output:</span><span class="sxs-lookup"><span data-stu-id="cf3c0-199">From an Azure PowerShell prompt, use the following to run the script and view the output:</span></span>

    `Get-FilesInHDInsight.ps1 -clusterName <your HDInsight cluster name> -source "example/wordcountout/part-00000"`

    <span data-ttu-id="cf3c0-200">This displays a list of words and how many times the word occurred.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-200">This displays a list of words and how many times the word occurred.</span></span> <span data-ttu-id="cf3c0-201">The following is an sample of the output data:</span><span class="sxs-lookup"><span data-stu-id="cf3c0-201">The following is an sample of the output data:</span></span>

    ```
    wrenching       1
    wretched        6
    wriggling       1
    wrinkled,       1
    wrinkles        2
    wrinkling       2
    ```

## <a name="next-steps"></a><span data-ttu-id="cf3c0-202">Next steps</span><span class="sxs-lookup"><span data-stu-id="cf3c0-202">Next steps</span></span>

<span data-ttu-id="cf3c0-203">Now that you have learned how to use streaming MapRedcue jobs with HDInsight, use the following links to explore other ways to work with Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cf3c0-203">Now that you have learned how to use streaming MapRedcue jobs with HDInsight, use the following links to explore other ways to work with Azure HDInsight.</span></span>

* [<span data-ttu-id="cf3c0-204">Use Hive with HDInsight</span><span class="sxs-lookup"><span data-stu-id="cf3c0-204">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="cf3c0-205">Use Pig with HDInsight</span><span class="sxs-lookup"><span data-stu-id="cf3c0-205">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="cf3c0-206">Use MapReduce jobs with HDInsight</span><span class="sxs-lookup"><span data-stu-id="cf3c0-206">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)

