---
title: Upload data for Hadoop jobs in HDInsight | Microsoft Docs
description: Learn how to upload and access data for Hadoop jobs in HDInsight using the Azure CLI, Azure Storage Explorer, Azure PowerShell, the Hadoop command line, or Sqoop.
services: hdinsight,storage
documentationcenter: ''
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 56b913ee-0f9a-4e9f-9eaf-c571f8603dd6
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jgao
ms.openlocfilehash: 6f306f6032f9175b1c8b3a140c1b654408eb1ef2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661083"
---
# <a name="upload-data-for-hadoop-jobs-in-hdinsight"></a><span data-ttu-id="8afba-103">Upload data for Hadoop jobs in HDInsight</span><span class="sxs-lookup"><span data-stu-id="8afba-103">Upload data for Hadoop jobs in HDInsight</span></span>
<span data-ttu-id="8afba-104">Azure HDInsight provides a full-featured Hadoop distributed file system (HDFS) over Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="8afba-104">Azure HDInsight provides a full-featured Hadoop distributed file system (HDFS) over Azure Blob storage.</span></span> <span data-ttu-id="8afba-105">It is designed as an HDFS extension to provide a seamless experience to customers.</span><span class="sxs-lookup"><span data-stu-id="8afba-105">It is designed as an HDFS extension to provide a seamless experience to customers.</span></span> <span data-ttu-id="8afba-106">It enables the full set of components in the Hadoop ecosystem to operate directly on the data it manages.</span><span class="sxs-lookup"><span data-stu-id="8afba-106">It enables the full set of components in the Hadoop ecosystem to operate directly on the data it manages.</span></span> <span data-ttu-id="8afba-107">Azure Blob storage and HDFS are distinct file systems that are optimized for storage of data and computations on that data.</span><span class="sxs-lookup"><span data-stu-id="8afba-107">Azure Blob storage and HDFS are distinct file systems that are optimized for storage of data and computations on that data.</span></span> <span data-ttu-id="8afba-108">For information about the benefits of using Azure Blob storage, see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="8afba-108">For information about the benefits of using Azure Blob storage, see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="8afba-109">**Prerequisites**</span><span class="sxs-lookup"><span data-stu-id="8afba-109">**Prerequisites**</span></span>

<span data-ttu-id="8afba-110">Note the following requirement before you begin:</span><span class="sxs-lookup"><span data-stu-id="8afba-110">Note the following requirement before you begin:</span></span>

* <span data-ttu-id="8afba-111">An Azure HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="8afba-111">An Azure HDInsight cluster.</span></span> <span data-ttu-id="8afba-112">For instructions, see [Get started with Azure HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="8afba-112">For instructions, see [Get started with Azure HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span>

## <a name="why-blob-storage"></a><span data-ttu-id="8afba-113">Why blob storage?</span><span class="sxs-lookup"><span data-stu-id="8afba-113">Why blob storage?</span></span>
<span data-ttu-id="8afba-114">Azure HDInsight clusters are typically deployed to run MapReduce jobs, and the clusters are dropped after these jobs complete.</span><span class="sxs-lookup"><span data-stu-id="8afba-114">Azure HDInsight clusters are typically deployed to run MapReduce jobs, and the clusters are dropped after these jobs complete.</span></span> <span data-ttu-id="8afba-115">Keeping the data in the HDFS clusters after computations are complete would be an expensive way to store this data.</span><span class="sxs-lookup"><span data-stu-id="8afba-115">Keeping the data in the HDFS clusters after computations are complete would be an expensive way to store this data.</span></span> <span data-ttu-id="8afba-116">Azure Blob storage is a highly available, highly scalable, high capacity, low cost, and shareable storage option for data that is to be processed using HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8afba-116">Azure Blob storage is a highly available, highly scalable, high capacity, low cost, and shareable storage option for data that is to be processed using HDInsight.</span></span> <span data-ttu-id="8afba-117">Storing data in a blob enables the HDInsight clusters that are used for computation to be safely released without losing data.</span><span class="sxs-lookup"><span data-stu-id="8afba-117">Storing data in a blob enables the HDInsight clusters that are used for computation to be safely released without losing data.</span></span>

### <a name="directories"></a><span data-ttu-id="8afba-118">Directories</span><span class="sxs-lookup"><span data-stu-id="8afba-118">Directories</span></span>
<span data-ttu-id="8afba-119">Azure Blob storage containers store data as key/value pairs, and there is no directory hierarchy.</span><span class="sxs-lookup"><span data-stu-id="8afba-119">Azure Blob storage containers store data as key/value pairs, and there is no directory hierarchy.</span></span> <span data-ttu-id="8afba-120">However the "/" character can be used within the key name to make it appear as if a file is stored within a directory structure.</span><span class="sxs-lookup"><span data-stu-id="8afba-120">However the "/" character can be used within the key name to make it appear as if a file is stored within a directory structure.</span></span> <span data-ttu-id="8afba-121">HDInsight sees these as if they are actual directories.</span><span class="sxs-lookup"><span data-stu-id="8afba-121">HDInsight sees these as if they are actual directories.</span></span>

<span data-ttu-id="8afba-122">For example, a blob's key may be *input/log1.txt*.</span><span class="sxs-lookup"><span data-stu-id="8afba-122">For example, a blob's key may be *input/log1.txt*.</span></span> <span data-ttu-id="8afba-123">No actual "input" directory exists, but due to the presence of the "/" character in the key name, it has the appearance of a file path.</span><span class="sxs-lookup"><span data-stu-id="8afba-123">No actual "input" directory exists, but due to the presence of the "/" character in the key name, it has the appearance of a file path.</span></span>

<span data-ttu-id="8afba-124">Because of this, if you use Azure Explorer tools you may notice some 0 byte files.</span><span class="sxs-lookup"><span data-stu-id="8afba-124">Because of this, if you use Azure Explorer tools you may notice some 0 byte files.</span></span> <span data-ttu-id="8afba-125">These files serve two purposes:</span><span class="sxs-lookup"><span data-stu-id="8afba-125">These files serve two purposes:</span></span>

* <span data-ttu-id="8afba-126">If there are empty folders, they mark of the existence of the folder.</span><span class="sxs-lookup"><span data-stu-id="8afba-126">If there are empty folders, they mark of the existence of the folder.</span></span> <span data-ttu-id="8afba-127">Azure Blob storage is clever enough to know that if a blob called foo/bar exists, there is a folder called **foo**.</span><span class="sxs-lookup"><span data-stu-id="8afba-127">Azure Blob storage is clever enough to know that if a blob called foo/bar exists, there is a folder called **foo**.</span></span> <span data-ttu-id="8afba-128">But the only way to signify an empty folder called **foo** is by having this special 0 byte file in place.</span><span class="sxs-lookup"><span data-stu-id="8afba-128">But the only way to signify an empty folder called **foo** is by having this special 0 byte file in place.</span></span>
* <span data-ttu-id="8afba-129">They hold special metadata that is needed by the Hadoop file system, notably the permissions and owners for the folders.</span><span class="sxs-lookup"><span data-stu-id="8afba-129">They hold special metadata that is needed by the Hadoop file system, notably the permissions and owners for the folders.</span></span>

## <a name="command-line-utilities"></a><span data-ttu-id="8afba-130">Command-line utilities</span><span class="sxs-lookup"><span data-stu-id="8afba-130">Command-line utilities</span></span>
<span data-ttu-id="8afba-131">Microsoft provides the following utilities to work with Azure Blob storage:</span><span class="sxs-lookup"><span data-stu-id="8afba-131">Microsoft provides the following utilities to work with Azure Blob storage:</span></span>

| <span data-ttu-id="8afba-132">Tool</span><span class="sxs-lookup"><span data-stu-id="8afba-132">Tool</span></span> | <span data-ttu-id="8afba-133">Linux</span><span class="sxs-lookup"><span data-stu-id="8afba-133">Linux</span></span> | <span data-ttu-id="8afba-134">OS X</span><span class="sxs-lookup"><span data-stu-id="8afba-134">OS X</span></span> | <span data-ttu-id="8afba-135">Windows</span><span class="sxs-lookup"><span data-stu-id="8afba-135">Windows</span></span> |
| --- |:---:|:---:|:---:|
| <span data-ttu-id="8afba-136">[Azure Command-Line Interface][azurecli]</span><span class="sxs-lookup"><span data-stu-id="8afba-136">[Azure Command-Line Interface][azurecli]</span></span> |<span data-ttu-id="8afba-137">✔</span><span class="sxs-lookup"><span data-stu-id="8afba-137">✔</span></span> |<span data-ttu-id="8afba-138">✔</span><span class="sxs-lookup"><span data-stu-id="8afba-138">✔</span></span> |<span data-ttu-id="8afba-139">✔</span><span class="sxs-lookup"><span data-stu-id="8afba-139">✔</span></span> |
| <span data-ttu-id="8afba-140">[Azure PowerShell][azure-powershell]</span><span class="sxs-lookup"><span data-stu-id="8afba-140">[Azure PowerShell][azure-powershell]</span></span> | | |<span data-ttu-id="8afba-141">✔</span><span class="sxs-lookup"><span data-stu-id="8afba-141">✔</span></span> |
| <span data-ttu-id="8afba-142">[AzCopy][azure-azcopy]</span><span class="sxs-lookup"><span data-stu-id="8afba-142">[AzCopy][azure-azcopy]</span></span> | | |<span data-ttu-id="8afba-143">✔</span><span class="sxs-lookup"><span data-stu-id="8afba-143">✔</span></span> |
| [<span data-ttu-id="8afba-144">Hadoop command</span><span class="sxs-lookup"><span data-stu-id="8afba-144">Hadoop command</span></span>](#commandline) |<span data-ttu-id="8afba-145">✔</span><span class="sxs-lookup"><span data-stu-id="8afba-145">✔</span></span> |<span data-ttu-id="8afba-146">✔</span><span class="sxs-lookup"><span data-stu-id="8afba-146">✔</span></span> |<span data-ttu-id="8afba-147">✔</span><span class="sxs-lookup"><span data-stu-id="8afba-147">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="8afba-148">While the Azure CLI, Azure PowerShell, and AzCopy can all be used from outside Azure, the Hadoop command is only available on the HDInsight cluster and only allows loading data from the local file system into Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="8afba-148">While the Azure CLI, Azure PowerShell, and AzCopy can all be used from outside Azure, the Hadoop command is only available on the HDInsight cluster and only allows loading data from the local file system into Azure Blob storage.</span></span>
>
>

### <a id="xplatcli"></a><span data-ttu-id="8afba-149">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8afba-149">Azure CLI</span></span>
<span data-ttu-id="8afba-150">The Azure CLI is a cross-platform tool that allows you to manage Azure services.</span><span class="sxs-lookup"><span data-stu-id="8afba-150">The Azure CLI is a cross-platform tool that allows you to manage Azure services.</span></span> <span data-ttu-id="8afba-151">Use the following steps to upload data to Azure Blob storage:</span><span class="sxs-lookup"><span data-stu-id="8afba-151">Use the following steps to upload data to Azure Blob storage:</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. <span data-ttu-id="8afba-152">[Install and configure the Azure CLI for Mac, Linux and Windows](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="8afba-152">[Install and configure the Azure CLI for Mac, Linux and Windows](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="8afba-153">Open a command prompt, bash, or other shell, and use the following to authenticate to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="8afba-153">Open a command prompt, bash, or other shell, and use the following to authenticate to your Azure subscription.</span></span>

        azure login

    <span data-ttu-id="8afba-154">When prompted, enter the user name and password for your subscription.</span><span class="sxs-lookup"><span data-stu-id="8afba-154">When prompted, enter the user name and password for your subscription.</span></span>
3. <span data-ttu-id="8afba-155">Enter the following command to list the storage accounts for your subscription:</span><span class="sxs-lookup"><span data-stu-id="8afba-155">Enter the following command to list the storage accounts for your subscription:</span></span>

        azure storage account list
4. <span data-ttu-id="8afba-156">Select the storage account that contains the blob you want to work with, then use the following command to retrieve the key for this account:</span><span class="sxs-lookup"><span data-stu-id="8afba-156">Select the storage account that contains the blob you want to work with, then use the following command to retrieve the key for this account:</span></span>

        azure storage account keys list <storage-account-name>

    <span data-ttu-id="8afba-157">This should return **Primary** and **Secondary** keys.</span><span class="sxs-lookup"><span data-stu-id="8afba-157">This should return **Primary** and **Secondary** keys.</span></span> <span data-ttu-id="8afba-158">Copy the **Primary** key value because it will be used in the next steps.</span><span class="sxs-lookup"><span data-stu-id="8afba-158">Copy the **Primary** key value because it will be used in the next steps.</span></span>
5. <span data-ttu-id="8afba-159">Use the following command to retrieve a list of blob containers within the storage account:</span><span class="sxs-lookup"><span data-stu-id="8afba-159">Use the following command to retrieve a list of blob containers within the storage account:</span></span>

        azure storage container list -a <storage-account-name> -k <primary-key>
6. <span data-ttu-id="8afba-160">Use the following commands to upload and download files to the blob:</span><span class="sxs-lookup"><span data-stu-id="8afba-160">Use the following commands to upload and download files to the blob:</span></span>

   * <span data-ttu-id="8afba-161">To upload a file:</span><span class="sxs-lookup"><span data-stu-id="8afba-161">To upload a file:</span></span>

           azure storage blob upload -a <storage-account-name> -k <primary-key> <source-file> <container-name> <blob-name>
   * <span data-ttu-id="8afba-162">To download a file:</span><span class="sxs-lookup"><span data-stu-id="8afba-162">To download a file:</span></span>

           azure storage blob download -a <storage-account-name> -k <primary-key> <container-name> <blob-name> <destination-file>

> [!NOTE]
> <span data-ttu-id="8afba-163">If you will always be working with the same storage account, you can set the following environment variables instead of specifying the account and key for every command:</span><span class="sxs-lookup"><span data-stu-id="8afba-163">If you will always be working with the same storage account, you can set the following environment variables instead of specifying the account and key for every command:</span></span>
>
> * <span data-ttu-id="8afba-164">**AZURE\_STORAGE\_ACCOUNT**: The storage account name</span><span class="sxs-lookup"><span data-stu-id="8afba-164">**AZURE\_STORAGE\_ACCOUNT**: The storage account name</span></span>
> * <span data-ttu-id="8afba-165">**AZURE\_STORAGE\_ACCESS\_KEY**: The storage account key</span><span class="sxs-lookup"><span data-stu-id="8afba-165">**AZURE\_STORAGE\_ACCESS\_KEY**: The storage account key</span></span>
>
>

### <a id="powershell"></a><span data-ttu-id="8afba-166">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8afba-166">Azure PowerShell</span></span>
<span data-ttu-id="8afba-167">Azure PowerShell is a scripting environment that you can use to control and automate the deployment and management of your workloads in Azure.</span><span class="sxs-lookup"><span data-stu-id="8afba-167">Azure PowerShell is a scripting environment that you can use to control and automate the deployment and management of your workloads in Azure.</span></span> <span data-ttu-id="8afba-168">For information about configuring your workstation to run Azure PowerShell, see [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="8afba-168">For information about configuring your workstation to run Azure PowerShell, see [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="8afba-169">**To upload a local file to Azure Blob storage**</span><span class="sxs-lookup"><span data-stu-id="8afba-169">**To upload a local file to Azure Blob storage**</span></span>

1. <span data-ttu-id="8afba-170">Open the Azure PowerShell console as instructed in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="8afba-170">Open the Azure PowerShell console as instructed in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>
2. <span data-ttu-id="8afba-171">Set the values of the first five variables in the following script:</span><span class="sxs-lookup"><span data-stu-id="8afba-171">Set the values of the first five variables in the following script:</span></span>

        $resourceGroupName = "<AzureResourceGroupName>"
        $storageAccountName = "<StorageAccountName>"
        $containerName = "<ContainerName>"

        $fileName ="<LocalFileName>"
        $blobName = "<BlobName>"

        # Get the storage account key
        $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
        # Create the storage context object
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

        # Copy the file from local workstation to the Blob container
        Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob $blobName -context $destContext
3. <span data-ttu-id="8afba-172">Paste the script into the Azure PowerShell console to run it to copy the file.</span><span class="sxs-lookup"><span data-stu-id="8afba-172">Paste the script into the Azure PowerShell console to run it to copy the file.</span></span>

<span data-ttu-id="8afba-173">For example PowerShell scripts created to work with HDInsight, see [HDInsight tools](https://github.com/blackmist/hdinsight-tools).</span><span class="sxs-lookup"><span data-stu-id="8afba-173">For example PowerShell scripts created to work with HDInsight, see [HDInsight tools](https://github.com/blackmist/hdinsight-tools).</span></span>

### <a id="azcopy"></a><span data-ttu-id="8afba-174">AzCopy</span><span class="sxs-lookup"><span data-stu-id="8afba-174">AzCopy</span></span>
<span data-ttu-id="8afba-175">AzCopy is a command-line tool that is designed to simplify the task of transferring data into and out of an Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="8afba-175">AzCopy is a command-line tool that is designed to simplify the task of transferring data into and out of an Azure Storage account.</span></span> <span data-ttu-id="8afba-176">You can use it as a standalone tool or incorporate this tool in an existing application.</span><span class="sxs-lookup"><span data-stu-id="8afba-176">You can use it as a standalone tool or incorporate this tool in an existing application.</span></span> <span data-ttu-id="8afba-177">[Download AzCopy][azure-azcopy-download].</span><span class="sxs-lookup"><span data-stu-id="8afba-177">[Download AzCopy][azure-azcopy-download].</span></span>

<span data-ttu-id="8afba-178">The AzCopy syntax is:</span><span class="sxs-lookup"><span data-stu-id="8afba-178">The AzCopy syntax is:</span></span>

    AzCopy <Source> <Destination> [filePattern [filePattern...]] [Options]

<span data-ttu-id="8afba-179">For more information, see [AzCopy - Uploading/Downloading files for Azure Blobs][azure-azcopy].</span><span class="sxs-lookup"><span data-stu-id="8afba-179">For more information, see [AzCopy - Uploading/Downloading files for Azure Blobs][azure-azcopy].</span></span>

### <a id="commandline"></a><span data-ttu-id="8afba-180">Hadoop command line</span><span class="sxs-lookup"><span data-stu-id="8afba-180">Hadoop command line</span></span>
<span data-ttu-id="8afba-181">The Hadoop command line is only useful for storing data into blob storage when the data is already present on the cluster head node.</span><span class="sxs-lookup"><span data-stu-id="8afba-181">The Hadoop command line is only useful for storing data into blob storage when the data is already present on the cluster head node.</span></span>

<span data-ttu-id="8afba-182">In order to use the Hadoop command, you must first connect to the headnode using one of the following methods:</span><span class="sxs-lookup"><span data-stu-id="8afba-182">In order to use the Hadoop command, you must first connect to the headnode using one of the following methods:</span></span>

* <span data-ttu-id="8afba-183">**Windows-based HDInsight**: [Connect using Remote Desktop](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span><span class="sxs-lookup"><span data-stu-id="8afba-183">**Windows-based HDInsight**: [Connect using Remote Desktop](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span></span>
* <span data-ttu-id="8afba-184">**Linux-based HDInsight**: Connect using SSH ([the SSH command](hdinsight-hadoop-linux-use-ssh-unix.md) or [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))</span><span class="sxs-lookup"><span data-stu-id="8afba-184">**Linux-based HDInsight**: Connect using SSH ([the SSH command](hdinsight-hadoop-linux-use-ssh-unix.md) or [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))</span></span>

<span data-ttu-id="8afba-185">Once connected, you can use the following syntax to upload a file to storage.</span><span class="sxs-lookup"><span data-stu-id="8afba-185">Once connected, you can use the following syntax to upload a file to storage.</span></span>

    hadoop -copyFromLocal <localFilePath> <storageFilePath>

<span data-ttu-id="8afba-186">For example, `hadoop fs -copyFromLocal data.txt /example/data/data.txt`</span><span class="sxs-lookup"><span data-stu-id="8afba-186">For example, `hadoop fs -copyFromLocal data.txt /example/data/data.txt`</span></span>

<span data-ttu-id="8afba-187">Because the default file system for HDInsight is in Azure Blob storage, /example/data.txt is actually in Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="8afba-187">Because the default file system for HDInsight is in Azure Blob storage, /example/data.txt is actually in Azure Blob storage.</span></span> <span data-ttu-id="8afba-188">You can also refer to the file as:</span><span class="sxs-lookup"><span data-stu-id="8afba-188">You can also refer to the file as:</span></span>

    wasbs:///example/data/data.txt

<span data-ttu-id="8afba-189">or</span><span class="sxs-lookup"><span data-stu-id="8afba-189">or</span></span>

    wasbs://<ContainerName>@<StorageAccountName>.blob.core.windows.net/example/data/davinci.txt

<span data-ttu-id="8afba-190">For a list of other Hadoop commands that work with files, see [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)</span><span class="sxs-lookup"><span data-stu-id="8afba-190">For a list of other Hadoop commands that work with files, see [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)</span></span>

> [!WARNING]
> <span data-ttu-id="8afba-191">On HBase clusters, the default block size used when writing data is 256KB.</span><span class="sxs-lookup"><span data-stu-id="8afba-191">On HBase clusters, the default block size used when writing data is 256KB.</span></span> <span data-ttu-id="8afba-192">While this works fine when using HBase APIs or REST APIs, using the `hadoop` or `hdfs dfs` commands to write data larger than ~12GB results in an error.</span><span class="sxs-lookup"><span data-stu-id="8afba-192">While this works fine when using HBase APIs or REST APIs, using the `hadoop` or `hdfs dfs` commands to write data larger than ~12GB results in an error.</span></span> <span data-ttu-id="8afba-193">See the [storage exception for write on blob](#storageexception) section below for more information.</span><span class="sxs-lookup"><span data-stu-id="8afba-193">See the [storage exception for write on blob](#storageexception) section below for more information.</span></span>
>
>

## <a name="graphical-clients"></a><span data-ttu-id="8afba-194">Graphical clients</span><span class="sxs-lookup"><span data-stu-id="8afba-194">Graphical clients</span></span>
<span data-ttu-id="8afba-195">There are also several applications that provide a graphical interface for working with Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="8afba-195">There are also several applications that provide a graphical interface for working with Azure Storage.</span></span> <span data-ttu-id="8afba-196">The following is a list of a few of these applications:</span><span class="sxs-lookup"><span data-stu-id="8afba-196">The following is a list of a few of these applications:</span></span>

| <span data-ttu-id="8afba-197">Client</span><span class="sxs-lookup"><span data-stu-id="8afba-197">Client</span></span> | <span data-ttu-id="8afba-198">Linux</span><span class="sxs-lookup"><span data-stu-id="8afba-198">Linux</span></span> | <span data-ttu-id="8afba-199">OS X</span><span class="sxs-lookup"><span data-stu-id="8afba-199">OS X</span></span> | <span data-ttu-id="8afba-200">Windows</span><span class="sxs-lookup"><span data-stu-id="8afba-200">Windows</span></span> |
| --- |:---:|:---:|:---:|
| [<span data-ttu-id="8afba-201">Microsoft Visual Studio Tools for HDInsight</span><span class="sxs-lookup"><span data-stu-id="8afba-201">Microsoft Visual Studio Tools for HDInsight</span></span>](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources) |<span data-ttu-id="8afba-202">✔</span><span class="sxs-lookup"><span data-stu-id="8afba-202">✔</span></span> |<span data-ttu-id="8afba-203">✔</span><span class="sxs-lookup"><span data-stu-id="8afba-203">✔</span></span> |<span data-ttu-id="8afba-204">✔</span><span class="sxs-lookup"><span data-stu-id="8afba-204">✔</span></span> |
| [<span data-ttu-id="8afba-205">Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="8afba-205">Azure Storage Explorer</span></span>](http://storageexplorer.com/) |<span data-ttu-id="8afba-206">✔</span><span class="sxs-lookup"><span data-stu-id="8afba-206">✔</span></span> |<span data-ttu-id="8afba-207">✔</span><span class="sxs-lookup"><span data-stu-id="8afba-207">✔</span></span> |<span data-ttu-id="8afba-208">✔</span><span class="sxs-lookup"><span data-stu-id="8afba-208">✔</span></span> |
| [<span data-ttu-id="8afba-209">Cloud Storage Studio 2</span><span class="sxs-lookup"><span data-stu-id="8afba-209">Cloud Storage Studio 2</span></span>](http://www.cerebrata.com/Products/CloudStorageStudio/) | | |<span data-ttu-id="8afba-210">✔</span><span class="sxs-lookup"><span data-stu-id="8afba-210">✔</span></span> |
| [<span data-ttu-id="8afba-211">CloudXplorer</span><span class="sxs-lookup"><span data-stu-id="8afba-211">CloudXplorer</span></span>](http://clumsyleaf.com/products/cloudxplorer) | | |<span data-ttu-id="8afba-212">✔</span><span class="sxs-lookup"><span data-stu-id="8afba-212">✔</span></span> |
| [<span data-ttu-id="8afba-213">Azure Explorer</span><span class="sxs-lookup"><span data-stu-id="8afba-213">Azure Explorer</span></span>](http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx) | | |<span data-ttu-id="8afba-214">✔</span><span class="sxs-lookup"><span data-stu-id="8afba-214">✔</span></span> |
| [<span data-ttu-id="8afba-215">Cyberduck</span><span class="sxs-lookup"><span data-stu-id="8afba-215">Cyberduck</span></span>](https://cyberduck.io/) | |<span data-ttu-id="8afba-216">✔</span><span class="sxs-lookup"><span data-stu-id="8afba-216">✔</span></span> |<span data-ttu-id="8afba-217">✔</span><span class="sxs-lookup"><span data-stu-id="8afba-217">✔</span></span> |

### <a name="visual-studio-tools-for-hdinsight"></a><span data-ttu-id="8afba-218">Visual Studio Tools for HDInsight</span><span class="sxs-lookup"><span data-stu-id="8afba-218">Visual Studio Tools for HDInsight</span></span>
<span data-ttu-id="8afba-219">For more information, see [Navigate the linked resources](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).</span><span class="sxs-lookup"><span data-stu-id="8afba-219">For more information, see [Navigate the linked resources](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).</span></span>

### <a id="storageexplorer"></a><span data-ttu-id="8afba-220">Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="8afba-220">Azure Storage Explorer</span></span>
<span data-ttu-id="8afba-221">*Azure Storage Explorer* is a useful tool for inspecting and altering the data in blobs.</span><span class="sxs-lookup"><span data-stu-id="8afba-221">*Azure Storage Explorer* is a useful tool for inspecting and altering the data in blobs.</span></span> <span data-ttu-id="8afba-222">It is a free, open source tool that can be downloaded from [http://storageexplorer.com/](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="8afba-222">It is a free, open source tool that can be downloaded from [http://storageexplorer.com/](http://storageexplorer.com/).</span></span> <span data-ttu-id="8afba-223">The source code is available from this link as well.</span><span class="sxs-lookup"><span data-stu-id="8afba-223">The source code is available from this link as well.</span></span>

<span data-ttu-id="8afba-224">Before using the tool, you must know your Azure storage account name and account key.</span><span class="sxs-lookup"><span data-stu-id="8afba-224">Before using the tool, you must know your Azure storage account name and account key.</span></span> <span data-ttu-id="8afba-225">For instructions about getting this information, see the "How to: View, copy and regenerate storage access keys" section of [Create, manage, or delete a storage account][azure-create-storage-account].</span><span class="sxs-lookup"><span data-stu-id="8afba-225">For instructions about getting this information, see the "How to: View, copy and regenerate storage access keys" section of [Create, manage, or delete a storage account][azure-create-storage-account].</span></span>

1. <span data-ttu-id="8afba-226">Run Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="8afba-226">Run Azure Storage Explorer.</span></span> <span data-ttu-id="8afba-227">If this is the first time you have run the Storage Explorer, you will be prompted for the **_Storage account name** and **Storage account key**.</span><span class="sxs-lookup"><span data-stu-id="8afba-227">If this is the first time you have run the Storage Explorer, you will be prompted for the **_Storage account name** and **Storage account key**.</span></span> <span data-ttu-id="8afba-228">If you have run it before, use the **Add** button to add a new storage account name and key.</span><span class="sxs-lookup"><span data-stu-id="8afba-228">If you have run it before, use the **Add** button to add a new storage account name and key.</span></span>

    <span data-ttu-id="8afba-229">Enter the name and key for the storage account used by your HDinsight cluster and then select **SAVE & OPEN**.</span><span class="sxs-lookup"><span data-stu-id="8afba-229">Enter the name and key for the storage account used by your HDinsight cluster and then select **SAVE & OPEN**.</span></span>

    ![HDI.AzureStorageExplorer][image-azure-storage-explorer]
2. <span data-ttu-id="8afba-231">In the list of containers to the left of the interface, click the name of the container that is associated with your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="8afba-231">In the list of containers to the left of the interface, click the name of the container that is associated with your HDInsight cluster.</span></span> <span data-ttu-id="8afba-232">By default, this is the name of the HDInsight cluster, but may be different if you entered a specific name when creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="8afba-232">By default, this is the name of the HDInsight cluster, but may be different if you entered a specific name when creating the cluster.</span></span>
3. <span data-ttu-id="8afba-233">From the tool bar, select the upload icon.</span><span class="sxs-lookup"><span data-stu-id="8afba-233">From the tool bar, select the upload icon.</span></span>

    ![Tool bar with upload icon highlighted](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-upload-data/toolbar.png)
4. <span data-ttu-id="8afba-235">Specify a file to upload, and then click **Open**.</span><span class="sxs-lookup"><span data-stu-id="8afba-235">Specify a file to upload, and then click **Open**.</span></span> <span data-ttu-id="8afba-236">When prompted, select **Upload** to upload the file to the root of the storage container.</span><span class="sxs-lookup"><span data-stu-id="8afba-236">When prompted, select **Upload** to upload the file to the root of the storage container.</span></span> <span data-ttu-id="8afba-237">If you want to upload the file to a specific path, enter the path in the **Destination** field and then select **Upload**.</span><span class="sxs-lookup"><span data-stu-id="8afba-237">If you want to upload the file to a specific path, enter the path in the **Destination** field and then select **Upload**.</span></span>

    ![File upload dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-upload-data/fileupload.png)

    <span data-ttu-id="8afba-239">Once the file has finished uploading, you can use it from jobs on the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="8afba-239">Once the file has finished uploading, you can use it from jobs on the HDInsight cluster.</span></span>

## <a name="mount-azure-blob-storage-as-local-drive"></a><span data-ttu-id="8afba-240">Mount Azure Blob Storage as Local Drive</span><span class="sxs-lookup"><span data-stu-id="8afba-240">Mount Azure Blob Storage as Local Drive</span></span>
<span data-ttu-id="8afba-241">See [Mount Azure Blob Storage as Local Drive](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).</span><span class="sxs-lookup"><span data-stu-id="8afba-241">See [Mount Azure Blob Storage as Local Drive](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).</span></span>

## <a name="services"></a><span data-ttu-id="8afba-242">Services</span><span class="sxs-lookup"><span data-stu-id="8afba-242">Services</span></span>
### <a name="azure-data-factory"></a><span data-ttu-id="8afba-243">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="8afba-243">Azure Data Factory</span></span>
<span data-ttu-id="8afba-244">The Azure Data Factory service is a fully managed service for composing data storage, data processing, and data movement services into streamlined, scalable, and reliable data production pipelines.</span><span class="sxs-lookup"><span data-stu-id="8afba-244">The Azure Data Factory service is a fully managed service for composing data storage, data processing, and data movement services into streamlined, scalable, and reliable data production pipelines.</span></span>

<span data-ttu-id="8afba-245">Azure Data Factory can be used to move data into Azure Blob storage, or to create data pipelines that directly use HDInsight features such as Hive and Pig.</span><span class="sxs-lookup"><span data-stu-id="8afba-245">Azure Data Factory can be used to move data into Azure Blob storage, or to create data pipelines that directly use HDInsight features such as Hive and Pig.</span></span>

<span data-ttu-id="8afba-246">For more information, see the [Azure Data Factory documentation](https://azure.microsoft.com/documentation/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="8afba-246">For more information, see the [Azure Data Factory documentation](https://azure.microsoft.com/documentation/services/data-factory/).</span></span>

### <a id="sqoop"></a><span data-ttu-id="8afba-247">Apache Sqoop</span><span class="sxs-lookup"><span data-stu-id="8afba-247">Apache Sqoop</span></span>
<span data-ttu-id="8afba-248">Sqoop is a tool designed to transfer data between Hadoop and relational databases.</span><span class="sxs-lookup"><span data-stu-id="8afba-248">Sqoop is a tool designed to transfer data between Hadoop and relational databases.</span></span> <span data-ttu-id="8afba-249">You can use it to import data from a relational database management system (RDBMS), such as SQL Server, MySQL, or Oracle into the Hadoop distributed file system (HDFS), transform the data in Hadoop with MapReduce or Hive, and then export the data back into an RDBMS.</span><span class="sxs-lookup"><span data-stu-id="8afba-249">You can use it to import data from a relational database management system (RDBMS), such as SQL Server, MySQL, or Oracle into the Hadoop distributed file system (HDFS), transform the data in Hadoop with MapReduce or Hive, and then export the data back into an RDBMS.</span></span>

<span data-ttu-id="8afba-250">For more information, see [Use Sqoop with HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="8afba-250">For more information, see [Use Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

## <a name="development-sdks"></a><span data-ttu-id="8afba-251">Development SDKs</span><span class="sxs-lookup"><span data-stu-id="8afba-251">Development SDKs</span></span>
<span data-ttu-id="8afba-252">Azure Blob storage can also be accessed using an Azure SDK from the following programming languages:</span><span class="sxs-lookup"><span data-stu-id="8afba-252">Azure Blob storage can also be accessed using an Azure SDK from the following programming languages:</span></span>

* <span data-ttu-id="8afba-253">.NET</span><span class="sxs-lookup"><span data-stu-id="8afba-253">.NET</span></span>
* <span data-ttu-id="8afba-254">Java</span><span class="sxs-lookup"><span data-stu-id="8afba-254">Java</span></span>
* <span data-ttu-id="8afba-255">Node.js</span><span class="sxs-lookup"><span data-stu-id="8afba-255">Node.js</span></span>
* <span data-ttu-id="8afba-256">PHP</span><span class="sxs-lookup"><span data-stu-id="8afba-256">PHP</span></span>
* <span data-ttu-id="8afba-257">Python</span><span class="sxs-lookup"><span data-stu-id="8afba-257">Python</span></span>
* <span data-ttu-id="8afba-258">Ruby</span><span class="sxs-lookup"><span data-stu-id="8afba-258">Ruby</span></span>

<span data-ttu-id="8afba-259">For more information on installing the Azure SDKs, see [Azure downloads](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="8afba-259">For more information on installing the Azure SDKs, see [Azure downloads](https://azure.microsoft.com/downloads/)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="8afba-260">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="8afba-260">Troubleshooting</span></span>
### <a id="storageexception"></a><span data-ttu-id="8afba-261">Storage exception for write on blob</span><span class="sxs-lookup"><span data-stu-id="8afba-261">Storage exception for write on blob</span></span>
<span data-ttu-id="8afba-262">**Symptoms**: When using the `hadoop` or `hdfs dfs` commands to write files that are ~12GB or larger on an HBase cluster, you may encounter the following error:</span><span class="sxs-lookup"><span data-stu-id="8afba-262">**Symptoms**: When using the `hadoop` or `hdfs dfs` commands to write files that are ~12GB or larger on an HBase cluster, you may encounter the following error:</span></span>

    ERROR azure.NativeAzureFileSystem: Encountered Storage Exception for write on Blob : example/test_large_file.bin._COPYING_ Exception details: null Error Code : RequestBodyTooLarge
    copyFromLocal: java.io.IOException
            at com.microsoft.azure.storage.core.Utility.initIOException(Utility.java:661)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:366)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:350)
            at java.util.concurrent.FutureTask.run(FutureTask.java:262)
            at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:471)
            at java.util.concurrent.FutureTask.run(FutureTask.java:262)
            at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1145)
            at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:615)
            at java.lang.Thread.run(Thread.java:745)
    Caused by: com.microsoft.azure.storage.StorageException: The request body is too large and exceeds the maximum permissible limit.
            at com.microsoft.azure.storage.StorageException.translateException(StorageException.java:89)
            at com.microsoft.azure.storage.core.StorageRequest.materializeException(StorageRequest.java:307)
            at com.microsoft.azure.storage.core.ExecutionEngine.executeWithRetry(ExecutionEngine.java:182)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlockInternal(CloudBlockBlob.java:816)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlock(CloudBlockBlob.java:788)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:354)
            ... 7 more

<span data-ttu-id="8afba-263">**Cause**: HBase on HDInsight clusters default to a block size of 256KB when writing to Azure storage.</span><span class="sxs-lookup"><span data-stu-id="8afba-263">**Cause**: HBase on HDInsight clusters default to a block size of 256KB when writing to Azure storage.</span></span> <span data-ttu-id="8afba-264">While this works for HBase APIs or REST APIs, it will result in an error when using the `hadoop` or `hdfs dfs` command-line utilities.</span><span class="sxs-lookup"><span data-stu-id="8afba-264">While this works for HBase APIs or REST APIs, it will result in an error when using the `hadoop` or `hdfs dfs` command-line utilities.</span></span>

<span data-ttu-id="8afba-265">**Resolution**: Use `fs.azure.write.request.size` to specify a larger block size.</span><span class="sxs-lookup"><span data-stu-id="8afba-265">**Resolution**: Use `fs.azure.write.request.size` to specify a larger block size.</span></span> <span data-ttu-id="8afba-266">You can do this on a per-use basis by using the `-D` parameter.</span><span class="sxs-lookup"><span data-stu-id="8afba-266">You can do this on a per-use basis by using the `-D` parameter.</span></span> <span data-ttu-id="8afba-267">The following is an example using this parameter with the `hadoop` command:</span><span class="sxs-lookup"><span data-stu-id="8afba-267">The following is an example using this parameter with the `hadoop` command:</span></span>

    hadoop -fs -D fs.azure.write.request.size=4194304 -copyFromLocal test_large_file.bin /example/data

<span data-ttu-id="8afba-268">You can also increase the value of `fs.azure.write.request.size` globally by using Ambari.</span><span class="sxs-lookup"><span data-stu-id="8afba-268">You can also increase the value of `fs.azure.write.request.size` globally by using Ambari.</span></span> <span data-ttu-id="8afba-269">The following steps can be used to change the value in the Ambari Web UI:</span><span class="sxs-lookup"><span data-stu-id="8afba-269">The following steps can be used to change the value in the Ambari Web UI:</span></span>

1. <span data-ttu-id="8afba-270">In your browser, go to the Ambari Web UI for your cluster.</span><span class="sxs-lookup"><span data-stu-id="8afba-270">In your browser, go to the Ambari Web UI for your cluster.</span></span> <span data-ttu-id="8afba-271">This is https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of your cluster.</span><span class="sxs-lookup"><span data-stu-id="8afba-271">This is https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of your cluster.</span></span>

    <span data-ttu-id="8afba-272">When prompted, enter the admin name and password for the cluster.</span><span class="sxs-lookup"><span data-stu-id="8afba-272">When prompted, enter the admin name and password for the cluster.</span></span>
2. <span data-ttu-id="8afba-273">From the left side of the screen, select **HDFS**, and then select the **Configs** tab.</span><span class="sxs-lookup"><span data-stu-id="8afba-273">From the left side of the screen, select **HDFS**, and then select the **Configs** tab.</span></span>
3. <span data-ttu-id="8afba-274">In the **Filter...** field, enter `fs.azure.write.request.size`.</span><span class="sxs-lookup"><span data-stu-id="8afba-274">In the **Filter...** field, enter `fs.azure.write.request.size`.</span></span> <span data-ttu-id="8afba-275">This will display the field and current value in the middle of the page.</span><span class="sxs-lookup"><span data-stu-id="8afba-275">This will display the field and current value in the middle of the page.</span></span>
4. <span data-ttu-id="8afba-276">Change the value from 262144 (256KB) to the new value.</span><span class="sxs-lookup"><span data-stu-id="8afba-276">Change the value from 262144 (256KB) to the new value.</span></span> <span data-ttu-id="8afba-277">For example, 4194304 (4MB).</span><span class="sxs-lookup"><span data-stu-id="8afba-277">For example, 4194304 (4MB).</span></span>

![Image of changing the value through Ambari Web UI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-upload-data/hbase-change-block-write-size.png)

<span data-ttu-id="8afba-279">For more information on using Ambari, see [Manage HDInsight clusters using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="8afba-279">For more information on using Ambari, see [Manage HDInsight clusters using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8afba-280">Next steps</span><span class="sxs-lookup"><span data-stu-id="8afba-280">Next steps</span></span>
<span data-ttu-id="8afba-281">Now that you understand how to get data into HDInsight, read the following articles to learn how to perform analysis:</span><span class="sxs-lookup"><span data-stu-id="8afba-281">Now that you understand how to get data into HDInsight, read the following articles to learn how to perform analysis:</span></span>

* <span data-ttu-id="8afba-282">[Get started with Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="8afba-282">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="8afba-283">[Submit Hadoop jobs programmatically][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="8afba-283">[Submit Hadoop jobs programmatically][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="8afba-284">[Use Hive with HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="8afba-284">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="8afba-285">[Use Pig with HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="8afba-285">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>

[azure-management-portal]: https://porta.azure.com
[azure-powershell]: http://msdn.microsoft.com/library/windowsazure/jj152841.aspx

[azure-storage-client-library]: /develop/net/how-to-guides/blob-storage/
[azure-create-storage-account]: ../storage/storage-create-storage-account.md
[azure-azcopy-download]: ../storage/storage-use-azcopy.md
[azure-azcopy]: ../storage/storage-use-azcopy.md

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md

[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-provision]: hdinsight-provision-clusters.md

[sqldatabase-create-configure]: ../sql-database-create-configure.md

[apache-sqoop-guide]: http://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs

[azurecli]: ../cli-install-nodejs.md


[image-azure-storage-explorer]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-upload-data/HDI.AzureStorageExplorer.png
[image-ase-addaccount]: ./media/hdinsight-upload-data/HDI.ASEAddAccount.png
[image-ase-blob]: ./media/hdinsight-upload-data/HDI.ASEBlob.png




