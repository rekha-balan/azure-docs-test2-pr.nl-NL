---
title: Analyze Twitter data with Hadoop in HDInsight | Microsoft Docs
description: Learn how to use Hive to analyze Twitter data on Hadoop in HDInsight to find the usage frequency of a particular word.
services: hdinsight
documentationcenter: ''
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 78e4ea33-9714-424d-ac07-3d60ecaebf2e
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 159e41f3d1b43abc830b79e1ea0bed05e05505a2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550362"
---
# <a name="analyze-twitter-data-using-hive-in-hdinsight"></a><span data-ttu-id="7a5ba-103">Analyze Twitter data using Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="7a5ba-103">Analyze Twitter data using Hive in HDInsight</span></span>
<span data-ttu-id="7a5ba-104">Social websites are one of the major driving forces for big-data adoption.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-104">Social websites are one of the major driving forces for big-data adoption.</span></span> <span data-ttu-id="7a5ba-105">Public APIs provided by sites like Twitter are a useful source of data for analyzing and understanding popular trends.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-105">Public APIs provided by sites like Twitter are a useful source of data for analyzing and understanding popular trends.</span></span>
<span data-ttu-id="7a5ba-106">In this tutorial, you will get tweets by using a Twitter streaming API, and then use Apache Hive on Azure HDInsight to get a list of Twitter users who sent the most tweets that contained a certain word.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-106">In this tutorial, you will get tweets by using a Twitter streaming API, and then use Apache Hive on Azure HDInsight to get a list of Twitter users who sent the most tweets that contained a certain word.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7a5ba-107">The steps in this document require a Windows-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-107">The steps in this document require a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="7a5ba-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7a5ba-109">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="7a5ba-109">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span> <span data-ttu-id="7a5ba-110">For steps specific to a Linux-based cluster, see [Analyze Twitter data using Hive in HDInsight (Linux)](hdinsight-analyze-twitter-data-linux.md).</span><span class="sxs-lookup"><span data-stu-id="7a5ba-110">For steps specific to a Linux-based cluster, see [Analyze Twitter data using Hive in HDInsight (Linux)](hdinsight-analyze-twitter-data-linux.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a5ba-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7a5ba-111">Prerequisites</span></span>
<span data-ttu-id="7a5ba-112">Before you begin this tutorial, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="7a5ba-112">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="7a5ba-113">**A workstation** with Azure PowerShell installed and configured.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-113">**A workstation** with Azure PowerShell installed and configured.</span></span>

    <span data-ttu-id="7a5ba-114">To execute Windows PowerShell scripts, you must run Azure PowerShell as administrator and set the execution policy to *RemoteSigned*.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-114">To execute Windows PowerShell scripts, you must run Azure PowerShell as administrator and set the execution policy to *RemoteSigned*.</span></span> <span data-ttu-id="7a5ba-115">See [Run Windows PowerShell scripts][powershell-script].</span><span class="sxs-lookup"><span data-stu-id="7a5ba-115">See [Run Windows PowerShell scripts][powershell-script].</span></span>

    <span data-ttu-id="7a5ba-116">Before running Windows PowerShell scripts, make sure you are connected to your Azure subscription by using the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="7a5ba-116">Before running Windows PowerShell scripts, make sure you are connected to your Azure subscription by using the following cmdlet:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="7a5ba-117">If you have multiple Azure subscriptions, use the following cmdlet to set the current subscription:</span><span class="sxs-lookup"><span data-stu-id="7a5ba-117">If you have multiple Azure subscriptions, use the following cmdlet to set the current subscription:</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionID <Azure Subscription ID>
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="7a5ba-118">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and will be removed by January 1, 2017.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-118">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and will be removed by January 1, 2017.</span></span> <span data-ttu-id="7a5ba-119">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-119">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="7a5ba-120">Please follow the steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) to install the latest version of Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-120">Please follow the steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="7a5ba-121">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-121">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

* <span data-ttu-id="7a5ba-122">**An Azure HDInsight cluster**.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-122">**An Azure HDInsight cluster**.</span></span> <span data-ttu-id="7a5ba-123">For instructions on cluster provisioning, see [Get started using HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="7a5ba-123">For instructions on cluster provisioning, see [Get started using HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="7a5ba-124">You will need the cluster name later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-124">You will need the cluster name later in the tutorial.</span></span>

<span data-ttu-id="7a5ba-125">The following table lists the files used in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="7a5ba-125">The following table lists the files used in this tutorial:</span></span>

| <span data-ttu-id="7a5ba-126">Files</span><span class="sxs-lookup"><span data-stu-id="7a5ba-126">Files</span></span> | <span data-ttu-id="7a5ba-127">Description</span><span class="sxs-lookup"><span data-stu-id="7a5ba-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7a5ba-128">/tutorials/twitter/data/tweets.txt</span><span class="sxs-lookup"><span data-stu-id="7a5ba-128">/tutorials/twitter/data/tweets.txt</span></span> |<span data-ttu-id="7a5ba-129">The source data for the Hive job.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-129">The source data for the Hive job.</span></span> |
| <span data-ttu-id="7a5ba-130">/tutorials/twitter/output</span><span class="sxs-lookup"><span data-stu-id="7a5ba-130">/tutorials/twitter/output</span></span> |<span data-ttu-id="7a5ba-131">The output folder for the Hive job.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-131">The output folder for the Hive job.</span></span> <span data-ttu-id="7a5ba-132">The default Hive job output file name is **000000_0**.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-132">The default Hive job output file name is **000000_0**.</span></span> |
| <span data-ttu-id="7a5ba-133">tutorials/twitter/twitter.hql</span><span class="sxs-lookup"><span data-stu-id="7a5ba-133">tutorials/twitter/twitter.hql</span></span> |<span data-ttu-id="7a5ba-134">The HiveQL script file.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-134">The HiveQL script file.</span></span> |
| <span data-ttu-id="7a5ba-135">/tutorials/twitter/jobstatus</span><span class="sxs-lookup"><span data-stu-id="7a5ba-135">/tutorials/twitter/jobstatus</span></span> |<span data-ttu-id="7a5ba-136">The Hadoop job status.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-136">The Hadoop job status.</span></span> |

## <a name="get-twitter-feed"></a><span data-ttu-id="7a5ba-137">Get Twitter feed</span><span class="sxs-lookup"><span data-stu-id="7a5ba-137">Get Twitter feed</span></span>
<span data-ttu-id="7a5ba-138">In this tutorial, you will use the [Twitter streaming APIs][twitter-streaming-api].</span><span class="sxs-lookup"><span data-stu-id="7a5ba-138">In this tutorial, you will use the [Twitter streaming APIs][twitter-streaming-api].</span></span> <span data-ttu-id="7a5ba-139">The specific Twitter streaming API you will use is [statuses/filter][twitter-statuses-filter].</span><span class="sxs-lookup"><span data-stu-id="7a5ba-139">The specific Twitter streaming API you will use is [statuses/filter][twitter-statuses-filter].</span></span>

> [!NOTE]
> <span data-ttu-id="7a5ba-140">A file containing 10,000 tweets and the Hive script file (covered in the next section) have been uploaded in a public Blob container.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-140">A file containing 10,000 tweets and the Hive script file (covered in the next section) have been uploaded in a public Blob container.</span></span> <span data-ttu-id="7a5ba-141">You can skip this section if you want to use the uploaded files.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-141">You can skip this section if you want to use the uploaded files.</span></span>

<span data-ttu-id="7a5ba-142">[Tweets data](https://dev.twitter.com/docs/platform-objects/tweets) is stored in the JavaScript Object Notation (JSON) format that contains a complex nested structure.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-142">[Tweets data](https://dev.twitter.com/docs/platform-objects/tweets) is stored in the JavaScript Object Notation (JSON) format that contains a complex nested structure.</span></span> <span data-ttu-id="7a5ba-143">Instead of writing many lines of code by using a conventional programming language, you can transform this nested structure into a Hive table, so that it can be queried by a Structured Query Language (SQL)-like language called HiveQL.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-143">Instead of writing many lines of code by using a conventional programming language, you can transform this nested structure into a Hive table, so that it can be queried by a Structured Query Language (SQL)-like language called HiveQL.</span></span>

<span data-ttu-id="7a5ba-144">Twitter uses OAuth to provide authorized access to its API.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-144">Twitter uses OAuth to provide authorized access to its API.</span></span> <span data-ttu-id="7a5ba-145">OAuth is an authentication protocol that allows users to approve applications to act on their behalf without sharing their password.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-145">OAuth is an authentication protocol that allows users to approve applications to act on their behalf without sharing their password.</span></span> <span data-ttu-id="7a5ba-146">More information can be found at [oauth.net](http://oauth.net/) or in the excellent [Beginner's Guide to OAuth](http://hueniverse.com/oauth/) from Hueniverse.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-146">More information can be found at [oauth.net](http://oauth.net/) or in the excellent [Beginner's Guide to OAuth](http://hueniverse.com/oauth/) from Hueniverse.</span></span>

<span data-ttu-id="7a5ba-147">The first step to use OAuth is to create a new application on the Twitter Developer site.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-147">The first step to use OAuth is to create a new application on the Twitter Developer site.</span></span>

<span data-ttu-id="7a5ba-148">**To create a Twitter application**</span><span class="sxs-lookup"><span data-stu-id="7a5ba-148">**To create a Twitter application**</span></span>

1. <span data-ttu-id="7a5ba-149">Sign in to [https://apps.twitter.com/](https://apps.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="7a5ba-149">Sign in to [https://apps.twitter.com/](https://apps.twitter.com/).</span></span> <span data-ttu-id="7a5ba-150">Click the **Sign up now** link if you don't have a Twitter account.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-150">Click the **Sign up now** link if you don't have a Twitter account.</span></span>
2. <span data-ttu-id="7a5ba-151">Click **Create New App**.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-151">Click **Create New App**.</span></span>
3. <span data-ttu-id="7a5ba-152">Enter **Name**, **Description**, **Website**.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-152">Enter **Name**, **Description**, **Website**.</span></span> <span data-ttu-id="7a5ba-153">You can make up a URL for the **Website** field.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-153">You can make up a URL for the **Website** field.</span></span> <span data-ttu-id="7a5ba-154">The following table shows some sample values to use:</span><span class="sxs-lookup"><span data-stu-id="7a5ba-154">The following table shows some sample values to use:</span></span>

   | <span data-ttu-id="7a5ba-155">Field</span><span class="sxs-lookup"><span data-stu-id="7a5ba-155">Field</span></span> | <span data-ttu-id="7a5ba-156">Value</span><span class="sxs-lookup"><span data-stu-id="7a5ba-156">Value</span></span> |
   | --- | --- |
   |  <span data-ttu-id="7a5ba-157">Name</span><span class="sxs-lookup"><span data-stu-id="7a5ba-157">Name</span></span> |<span data-ttu-id="7a5ba-158">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="7a5ba-158">MyHDInsightApp</span></span> |
   |  <span data-ttu-id="7a5ba-159">Description</span><span class="sxs-lookup"><span data-stu-id="7a5ba-159">Description</span></span> |<span data-ttu-id="7a5ba-160">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="7a5ba-160">MyHDInsightApp</span></span> |
   |  <span data-ttu-id="7a5ba-161">Website</span><span class="sxs-lookup"><span data-stu-id="7a5ba-161">Website</span></span> |http://www.myhdinsightapp.com |
4. <span data-ttu-id="7a5ba-162">Check **Yes, I agree**, and then click **Create your Twitter application**.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-162">Check **Yes, I agree**, and then click **Create your Twitter application**.</span></span>
5. <span data-ttu-id="7a5ba-163">Click the **Permissions** tab. The default permission is **Read only**.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-163">Click the **Permissions** tab. The default permission is **Read only**.</span></span> <span data-ttu-id="7a5ba-164">This is sufficient for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-164">This is sufficient for this tutorial.</span></span>
6. <span data-ttu-id="7a5ba-165">Click the **Keys and Access Tokens** tab.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-165">Click the **Keys and Access Tokens** tab.</span></span>
7. <span data-ttu-id="7a5ba-166">Click **Create my access token**.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-166">Click **Create my access token**.</span></span>
8. <span data-ttu-id="7a5ba-167">Click **Test OAuth** in the upper-right corner of the page.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-167">Click **Test OAuth** in the upper-right corner of the page.</span></span>
9. <span data-ttu-id="7a5ba-168">Write down **consumer key**, **Consumer secret**, **Access token**, and **Access token secret**.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-168">Write down **consumer key**, **Consumer secret**, **Access token**, and **Access token secret**.</span></span> <span data-ttu-id="7a5ba-169">You will need the values later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-169">You will need the values later in the tutorial.</span></span>

<span data-ttu-id="7a5ba-170">In this tutorial, you will use Windows PowerShell to make the web service call.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-170">In this tutorial, you will use Windows PowerShell to make the web service call.</span></span> <span data-ttu-id="7a5ba-171">For a .NET C# sample, see [Analyze real-time Twitter sentiment with HBase in HDInsight][hdinsight-hbase-twitter-sentiment].</span><span class="sxs-lookup"><span data-stu-id="7a5ba-171">For a .NET C# sample, see [Analyze real-time Twitter sentiment with HBase in HDInsight][hdinsight-hbase-twitter-sentiment].</span></span> <span data-ttu-id="7a5ba-172">The other popular tool to make web service calls is [*Curl*][curl].</span><span class="sxs-lookup"><span data-stu-id="7a5ba-172">The other popular tool to make web service calls is [*Curl*][curl].</span></span> <span data-ttu-id="7a5ba-173">Curl can be downloaded from [here][curl-download].</span><span class="sxs-lookup"><span data-stu-id="7a5ba-173">Curl can be downloaded from [here][curl-download].</span></span>

> [!NOTE]
> <span data-ttu-id="7a5ba-174">When you use the curl command in Windows, use double quotes instead of single quotes for the option values.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-174">When you use the curl command in Windows, use double quotes instead of single quotes for the option values.</span></span>

<span data-ttu-id="7a5ba-175">**To get tweets**</span><span class="sxs-lookup"><span data-stu-id="7a5ba-175">**To get tweets**</span></span>

1. <span data-ttu-id="7a5ba-176">Open the Windows PowerShell Integrated Scripting Environment (ISE).</span><span class="sxs-lookup"><span data-stu-id="7a5ba-176">Open the Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="7a5ba-177">(On the Windows 8 Start screen, type **PowerShell_ISE** and then click **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-177">(On the Windows 8 Start screen, type **PowerShell_ISE** and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="7a5ba-178">See [Start Windows PowerShell on Windows 8 and Windows][powershell-start].)</span><span class="sxs-lookup"><span data-stu-id="7a5ba-178">See [Start Windows PowerShell on Windows 8 and Windows][powershell-start].)</span></span>
2. <span data-ttu-id="7a5ba-179">Copy the following script into the script pane:</span><span class="sxs-lookup"><span data-stu-id="7a5ba-179">Copy the following script into the script pane:</span></span>

    ```powershell
    #region - variables and constants
    $clusterName = "<HDInsightClusterName>" # Enter the HDInsight cluster name

    # Enter the OAuth information for your Twitter application
    $oauth_consumer_key = "<TwitterAppConsumerKey>";
    $oauth_consumer_secret = "<TwitterAppConsumerSecret>";
    $oauth_token = "<TwitterAppAccessToken>";
    $oauth_token_secret = "<TwitterAppAccessTokenSecret>";

    $destBlobName = "tutorials/twitter/data/tweets.txt" # This script saves the tweets into this blob.

    $trackString = "Azure, Cloud, HDInsight" # This script gets the tweets containing these keywords.
    $track = [System.Uri]::EscapeDataString($trackString);
    $lineMax = 10000  # The script will get this number of tweets. It is about 3 minutes every 100 lines.
    #endregion

    #region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
    Login-AzureRmAccount
    #endregion

    #region - Create a block blob object for writing tweets into Blob storage
    Write-Host "Get the default storage account name and Blob container name using the cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -Name $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $storageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $containerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $storageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $containerName." -ForegroundColor Yellow

    Write-Host "Define the Azure storage connection string ..." -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$storageAccountName;AccountKey=$storageAccountKey"
    Write-Host "`tThe connection string is $storageConnectionString." -ForegroundColor Yellow

    Write-Host "Create block blob object ..." -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($containerName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)
    #end region

    # region - Format OAuth strings
    Write-Host "Format oauth strings ..." -ForegroundColor Green
    $oauth_nonce = [System.Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes([System.DateTime]::Now.Ticks.ToString()));
    $ts = [System.DateTime]::UtcNow - [System.DateTime]::ParseExact("01/01/1970", "dd/MM/yyyy", $null)
    $oauth_timestamp = [System.Convert]::ToInt64($ts.TotalSeconds).ToString();

    $signature = "POST&";
    $signature += [System.Uri]::EscapeDataString("https://stream.twitter.com/1.1/statuses/filter.json") + "&";
    $signature += [System.Uri]::EscapeDataString("oauth_consumer_key=" + $oauth_consumer_key + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_nonce=" + $oauth_nonce + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_signature_method=HMAC-SHA1&");
    $signature += [System.Uri]::EscapeDataString("oauth_timestamp=" + $oauth_timestamp + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_token=" + $oauth_token + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_version=1.0&");
    $signature += [System.Uri]::EscapeDataString("track=" + $track);

    $signature_key = [System.Uri]::EscapeDataString($oauth_consumer_secret) + "&" + [System.Uri]::EscapeDataString($oauth_token_secret);

    $hmacsha1 = new-object System.Security.Cryptography.HMACSHA1;
    $hmacsha1.Key = [System.Text.Encoding]::ASCII.GetBytes($signature_key);
    $oauth_signature = [System.Convert]::ToBase64String($hmacsha1.ComputeHash([System.Text.Encoding]::ASCII.GetBytes($signature)));

    $oauth_authorization = 'OAuth ';
    $oauth_authorization += 'oauth_consumer_key="' + [System.Uri]::EscapeDataString($oauth_consumer_key) + '",';
    $oauth_authorization += 'oauth_nonce="' + [System.Uri]::EscapeDataString($oauth_nonce) + '",';
    $oauth_authorization += 'oauth_signature="' + [System.Uri]::EscapeDataString($oauth_signature) + '",';
    $oauth_authorization += 'oauth_signature_method="HMAC-SHA1",'
    $oauth_authorization += 'oauth_timestamp="' + [System.Uri]::EscapeDataString($oauth_timestamp) + '",'
    $oauth_authorization += 'oauth_token="' + [System.Uri]::EscapeDataString($oauth_token) + '",';
    $oauth_authorization += 'oauth_version="1.0"';

    $post_body = [System.Text.Encoding]::ASCII.GetBytes("track=" + $track);
    #endregion

    #region - Read tweets
    Write-Host "Create HTTP web request ..." -ForegroundColor Green
    [System.Net.HttpWebRequest] $request = [System.Net.WebRequest]::Create("https://stream.twitter.com/1.1/statuses/filter.json");
    $request.Method = "POST";
    $request.Headers.Add("Authorization", $oauth_authorization);
    $request.ContentType = "application/x-www-form-urlencoded";
    $body = $request.GetRequestStream();

    $body.write($post_body, 0, $post_body.length);
    $body.flush();
    $body.close();
    $response = $request.GetResponse() ;

    Write-Host "Start stream reading ..." -ForegroundColor Green

    Write-Host "Define a MemoryStream and a StreamWriter for writing ..." -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    $sReader = New-Object System.IO.StreamReader($response.GetResponseStream())

    $inrec = $sReader.ReadLine()
    $count = 0
    while (($inrec -ne $null) -and ($count -le $lineMax))
    {
        if ($inrec -ne "")
        {
            Write-Host "`n`t $count tweets received." -ForegroundColor Yellow

            $writeStream.WriteLine($inrec)
            $count ++
        }

        $inrec=$sReader.ReadLine()
    }
    #endregion

    #region - Write tweets to Blob storage
    Write-Host "Write to the destination blob ..." -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    $sReader.close()
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. <span data-ttu-id="7a5ba-180">Set the first five to eight variables in the script:</span><span class="sxs-lookup"><span data-stu-id="7a5ba-180">Set the first five to eight variables in the script:</span></span>

    <span data-ttu-id="7a5ba-181">Variable</span><span class="sxs-lookup"><span data-stu-id="7a5ba-181">Variable</span></span>|<span data-ttu-id="7a5ba-182">Description</span><span class="sxs-lookup"><span data-stu-id="7a5ba-182">Description</span></span>
    ---|---
    <span data-ttu-id="7a5ba-183">$clusterName</span><span class="sxs-lookup"><span data-stu-id="7a5ba-183">$clusterName</span></span>|<span data-ttu-id="7a5ba-184">This is the name of the HDInsight cluster where you want to run the application.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-184">This is the name of the HDInsight cluster where you want to run the application.</span></span>
    <span data-ttu-id="7a5ba-185">$oauth_consumer_key</span><span class="sxs-lookup"><span data-stu-id="7a5ba-185">$oauth_consumer_key</span></span>|<span data-ttu-id="7a5ba-186">This is the Twitter application **consumer key** you wrote down earlier when you created the Twitter application.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-186">This is the Twitter application **consumer key** you wrote down earlier when you created the Twitter application.</span></span>
    <span data-ttu-id="7a5ba-187">$oauth_consumer_secret</span><span class="sxs-lookup"><span data-stu-id="7a5ba-187">$oauth_consumer_secret</span></span>|<span data-ttu-id="7a5ba-188">This is the Twitter application **consumer secret** you wrote down earlier.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-188">This is the Twitter application **consumer secret** you wrote down earlier.</span></span>
    <span data-ttu-id="7a5ba-189">$oauth_token</span><span class="sxs-lookup"><span data-stu-id="7a5ba-189">$oauth_token</span></span>|<span data-ttu-id="7a5ba-190">This is the Twitter application **access token** you wrote down earlier.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-190">This is the Twitter application **access token** you wrote down earlier.</span></span>
    <span data-ttu-id="7a5ba-191">$oauth_token_secret</span><span class="sxs-lookup"><span data-stu-id="7a5ba-191">$oauth_token_secret</span></span>|<span data-ttu-id="7a5ba-192">This is the Twitter application **access token secret** you wrote down earlier.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-192">This is the Twitter application **access token secret** you wrote down earlier.</span></span>
    <span data-ttu-id="7a5ba-193">$destBlobName</span><span class="sxs-lookup"><span data-stu-id="7a5ba-193">$destBlobName</span></span>|<span data-ttu-id="7a5ba-194">This is the output blob name.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-194">This is the output blob name.</span></span> <span data-ttu-id="7a5ba-195">The default value is **tutorials/twitter/data/tweets.txt**.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-195">The default value is **tutorials/twitter/data/tweets.txt**.</span></span> <span data-ttu-id="7a5ba-196">If you change the default value, you will need to update the Windows PowerShell scripts accordingly.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-196">If you change the default value, you will need to update the Windows PowerShell scripts accordingly.</span></span>
    <span data-ttu-id="7a5ba-197">$trackString</span><span class="sxs-lookup"><span data-stu-id="7a5ba-197">$trackString</span></span>|<span data-ttu-id="7a5ba-198">The web service will return tweets related to these keywords.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-198">The web service will return tweets related to these keywords.</span></span> <span data-ttu-id="7a5ba-199">The default value is **Azure, Cloud, HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-199">The default value is **Azure, Cloud, HDInsight**.</span></span> <span data-ttu-id="7a5ba-200">If you change the default value, you will update the Windows PowerShell scripts accordingly.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-200">If you change the default value, you will update the Windows PowerShell scripts accordingly.</span></span>
    <span data-ttu-id="7a5ba-201">$lineMax</span><span class="sxs-lookup"><span data-stu-id="7a5ba-201">$lineMax</span></span>|<span data-ttu-id="7a5ba-202">The value determines how many tweets the script will read.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-202">The value determines how many tweets the script will read.</span></span> <span data-ttu-id="7a5ba-203">It takes about three minutes to read 100 tweets.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-203">It takes about three minutes to read 100 tweets.</span></span> <span data-ttu-id="7a5ba-204">You can set a larger number, but it will take more time to download.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-204">You can set a larger number, but it will take more time to download.</span></span>

1. <span data-ttu-id="7a5ba-205">Press **F5** to run the script.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-205">Press **F5** to run the script.</span></span> <span data-ttu-id="7a5ba-206">If you run into problems, as a workaround, select all the lines, and then press **F8**.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-206">If you run into problems, as a workaround, select all the lines, and then press **F8**.</span></span>
2. <span data-ttu-id="7a5ba-207">You shall see "Complete!"</span><span class="sxs-lookup"><span data-stu-id="7a5ba-207">You shall see "Complete!"</span></span> <span data-ttu-id="7a5ba-208">at the end of the output.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-208">at the end of the output.</span></span> <span data-ttu-id="7a5ba-209">Any error messages will be displayed in red.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-209">Any error messages will be displayed in red.</span></span>

<span data-ttu-id="7a5ba-210">As a validation procedure, you can check the output file, **/tutorials/twitter/data/tweets.txt**, on your Azure Blob storage by using an Azure storage explorer or Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-210">As a validation procedure, you can check the output file, **/tutorials/twitter/data/tweets.txt**, on your Azure Blob storage by using an Azure storage explorer or Azure PowerShell.</span></span> <span data-ttu-id="7a5ba-211">For a sample Windows PowerShell script for listing files, see [Use Blob storage with HDInsight][hdinsight-storage-powershell].</span><span class="sxs-lookup"><span data-stu-id="7a5ba-211">For a sample Windows PowerShell script for listing files, see [Use Blob storage with HDInsight][hdinsight-storage-powershell].</span></span>

## <a name="create-hiveql-script"></a><span data-ttu-id="7a5ba-212">Create HiveQL script</span><span class="sxs-lookup"><span data-stu-id="7a5ba-212">Create HiveQL script</span></span>
<span data-ttu-id="7a5ba-213">Using Azure PowerShell, you can run multiple HiveQL statements one at a time, or package the HiveQL statement into a script file.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-213">Using Azure PowerShell, you can run multiple HiveQL statements one at a time, or package the HiveQL statement into a script file.</span></span> <span data-ttu-id="7a5ba-214">In this tutorial, you will create a HiveQL script.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-214">In this tutorial, you will create a HiveQL script.</span></span> <span data-ttu-id="7a5ba-215">The script file must be uploaded to Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-215">The script file must be uploaded to Azure Blob storage.</span></span> <span data-ttu-id="7a5ba-216">In the next section, you will run the script file by using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-216">In the next section, you will run the script file by using Azure PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="7a5ba-217">The Hive script file and a file containing 10,000 tweets have been uploaded in a public Blob container.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-217">The Hive script file and a file containing 10,000 tweets have been uploaded in a public Blob container.</span></span> <span data-ttu-id="7a5ba-218">You can skip this section if you want to use the uploaded files.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-218">You can skip this section if you want to use the uploaded files.</span></span>

<span data-ttu-id="7a5ba-219">The HiveQL script will perform the following:</span><span class="sxs-lookup"><span data-stu-id="7a5ba-219">The HiveQL script will perform the following:</span></span>

1. <span data-ttu-id="7a5ba-220">**Drop the tweets_raw table** in case the table already exists.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-220">**Drop the tweets_raw table** in case the table already exists.</span></span>
2. <span data-ttu-id="7a5ba-221">**Create the tweets_raw Hive table**.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-221">**Create the tweets_raw Hive table**.</span></span> <span data-ttu-id="7a5ba-222">This temporary Hive structured table holds the data for further extract, transform, and load (ETL) processing.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-222">This temporary Hive structured table holds the data for further extract, transform, and load (ETL) processing.</span></span> <span data-ttu-id="7a5ba-223">For information on partitions, see [Hive tutorial][apache-hive-tutorial].</span><span class="sxs-lookup"><span data-stu-id="7a5ba-223">For information on partitions, see [Hive tutorial][apache-hive-tutorial].</span></span>
3. <span data-ttu-id="7a5ba-224">**Load data** from the source folder, /tutorials/twitter/data.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-224">**Load data** from the source folder, /tutorials/twitter/data.</span></span> <span data-ttu-id="7a5ba-225">The large tweets dataset in nested JSON format has now been transformed into a temporary Hive table structure.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-225">The large tweets dataset in nested JSON format has now been transformed into a temporary Hive table structure.</span></span>
4. <span data-ttu-id="7a5ba-226">**Drop the tweets table** in case the table already exists.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-226">**Drop the tweets table** in case the table already exists.</span></span>
5. <span data-ttu-id="7a5ba-227">**Create the tweets table**.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-227">**Create the tweets table**.</span></span> <span data-ttu-id="7a5ba-228">Before you can query against the tweets dataset by using Hive, you need to run another ETL process.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-228">Before you can query against the tweets dataset by using Hive, you need to run another ETL process.</span></span> <span data-ttu-id="7a5ba-229">This ETL process defines a more detailed table schema for the data that you have stored in the "twitter_raw" table.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-229">This ETL process defines a more detailed table schema for the data that you have stored in the "twitter_raw" table.</span></span>
6. <span data-ttu-id="7a5ba-230">**Insert overwrite table**.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-230">**Insert overwrite table**.</span></span> <span data-ttu-id="7a5ba-231">This complex Hive script will kick off a set of long MapReduce jobs by the Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-231">This complex Hive script will kick off a set of long MapReduce jobs by the Hadoop cluster.</span></span> <span data-ttu-id="7a5ba-232">Depending on your dataset and the size of your cluster, this could take about 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-232">Depending on your dataset and the size of your cluster, this could take about 10 minutes.</span></span>
7. <span data-ttu-id="7a5ba-233">**Insert overwrite directory**.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-233">**Insert overwrite directory**.</span></span> <span data-ttu-id="7a5ba-234">Run a query and output the dataset to a file.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-234">Run a query and output the dataset to a file.</span></span> <span data-ttu-id="7a5ba-235">This query will return a list of Twitter users who sent most tweets that contained the word "Azure".</span><span class="sxs-lookup"><span data-stu-id="7a5ba-235">This query will return a list of Twitter users who sent most tweets that contained the word "Azure".</span></span>

<span data-ttu-id="7a5ba-236">**To create a Hive script and upload it to Azure**</span><span class="sxs-lookup"><span data-stu-id="7a5ba-236">**To create a Hive script and upload it to Azure**</span></span>

1. <span data-ttu-id="7a5ba-237">Open Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-237">Open Windows PowerShell ISE.</span></span>
2. <span data-ttu-id="7a5ba-238">Copy the following script into the script pane:</span><span class="sxs-lookup"><span data-stu-id="7a5ba-238">Copy the following script into the script pane:</span></span>

    ```powershell
    #region - variables and constants
    $clusterName = "<Existing HDInsight Cluster Name>" # Enter your HDInsight cluster name
    $subscriptionID = "<Azure Subscription ID>"

    $sourceDataPath = "/tutorials/twitter/data"
    $outputPath = "/tutorials/twitter/output"
    $hqlScriptFile = "tutorials/twitter/twitter.hql"

    $hqlStatements = @"
    set hive.exec.dynamic.partition = true;
    set hive.exec.dynamic.partition.mode = nonstrict;

    DROP TABLE tweets_raw;
    CREATE EXTERNAL TABLE tweets_raw (
        json_response STRING
    )
    STORED AS TEXTFILE LOCATION '$sourceDataPath';

    DROP TABLE tweets;
    CREATE TABLE tweets
    (
        id BIGINT,
        created_at STRING,
        created_at_date STRING,
        created_at_year STRING,
        created_at_month STRING,
        created_at_day STRING,
        created_at_time STRING,
        in_reply_to_user_id_str STRING,
        text STRING,
        contributors STRING,
        retweeted STRING,
        truncated STRING,
        coordinates STRING,
        source STRING,
        retweet_count INT,
        url STRING,
        hashtags array<STRING>,
        user_mentions array<STRING>,
        first_hashtag STRING,
        first_user_mention STRING,
        screen_name STRING,
        name STRING,
        followers_count INT,
        listed_count INT,
        friends_count INT,
        lang STRING,
        user_location STRING,
        time_zone STRING,
        profile_image_url STRING,
        json_response STRING
    );

    FROM tweets_raw
    INSERT OVERWRITE TABLE tweets
    SELECT
        cast(get_json_object(json_response, '$.id_str') as BIGINT),
        get_json_object(json_response, '$.created_at'),
        concat(substr (get_json_object(json_response, '$.created_at'),1,10),' ',
        substr (get_json_object(json_response, '$.created_at'),27,4)),
        substr (get_json_object(json_response, '$.created_at'),27,4),
        case substr (get_json_object(json_response, '$.created_at'),5,3)
            when "Jan" then "01"
            when "Feb" then "02"
            when "Mar" then "03"
            when "Apr" then "04"
            when "May" then "05"
            when "Jun" then "06"
            when "Jul" then "07"
            when "Aug" then "08"
            when "Sep" then "09"
            when "Oct" then "10"
            when "Nov" then "11"
            when "Dec" then "12" end,
        substr (get_json_object(json_response, '$.created_at'),9,2),
        substr (get_json_object(json_response, '$.created_at'),12,8),
        get_json_object(json_response, '$.in_reply_to_user_id_str'),
        get_json_object(json_response, '$.text'),
        get_json_object(json_response, '$.contributors'),
        get_json_object(json_response, '$.retweeted'),
        get_json_object(json_response, '$.truncated'),
        get_json_object(json_response, '$.coordinates'),
        get_json_object(json_response, '$.source'),
        cast (get_json_object(json_response, '$.retweet_count') as INT),
        get_json_object(json_response, '$.entities.display_url'),
        array(
            trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[1].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[2].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[3].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[4].text')))),
        array(
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[1].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[2].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[3].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[4].screen_name')))),
        trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
        trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
        get_json_object(json_response, '$.user.screen_name'),
        get_json_object(json_response, '$.user.name'),
        cast (get_json_object(json_response, '$.user.followers_count') as INT),
        cast (get_json_object(json_response, '$.user.listed_count') as INT),
        cast (get_json_object(json_response, '$.user.friends_count') as INT),
        get_json_object(json_response, '$.user.lang'),
        get_json_object(json_response, '$.user.location'),
        get_json_object(json_response, '$.user.time_zone'),
        get_json_object(json_response, '$.user.profile_image_url'),
        json_response
    WHERE (length(json_response) > 500);

    INSERT OVERWRITE DIRECTORY '$outputPath'
    SELECT name, screen_name, count(1) as cc
        FROM tweets
        WHERE text like "%Azure%"
        GROUP BY name,screen_name
        ORDER BY cc DESC LIMIT 10;
    "@
    #endregion

    #region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #endregion

    #region - Create a block blob object for writing the Hive script file
    Write-Host "Get the default storage account name and container name based on the cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

    Write-Host "Define the connection string ..." -ForegroundColor Green
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    Write-Host "Create block blob objects referencing the hql script file" -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $hqlScriptBlob = $storageContainer.GetBlockBlobReference($hqlScriptFile)

    Write-Host "Define a MemoryStream and a StreamWriter for writing ... " -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream
    $writeStream.Writeline($hqlStatements)
    #endregion

    #region - Write the Hive script file to Blob storage
    Write-Host "Write to the destination blob ... " -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $hqlScriptBlob.UploadFromStream($memStream)
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. <span data-ttu-id="7a5ba-239">Set the first two variables in the script:</span><span class="sxs-lookup"><span data-stu-id="7a5ba-239">Set the first two variables in the script:</span></span>

   | <span data-ttu-id="7a5ba-240">Variable</span><span class="sxs-lookup"><span data-stu-id="7a5ba-240">Variable</span></span> | <span data-ttu-id="7a5ba-241">Description</span><span class="sxs-lookup"><span data-stu-id="7a5ba-241">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="7a5ba-242">$clusterName</span><span class="sxs-lookup"><span data-stu-id="7a5ba-242">$clusterName</span></span> |<span data-ttu-id="7a5ba-243">Enter the HDInsight cluster name where you want to run the application.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-243">Enter the HDInsight cluster name where you want to run the application.</span></span> |
   |  <span data-ttu-id="7a5ba-244">$subscriptionID</span><span class="sxs-lookup"><span data-stu-id="7a5ba-244">$subscriptionID</span></span> |<span data-ttu-id="7a5ba-245">Enter your Azure subscription ID.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-245">Enter your Azure subscription ID.</span></span> |
   |  <span data-ttu-id="7a5ba-246">$sourceDataPath</span><span class="sxs-lookup"><span data-stu-id="7a5ba-246">$sourceDataPath</span></span> |<span data-ttu-id="7a5ba-247">The Azure Blob storage location where the Hive queries will read the data from.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-247">The Azure Blob storage location where the Hive queries will read the data from.</span></span> <span data-ttu-id="7a5ba-248">You don't need to change this variable.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-248">You don't need to change this variable.</span></span> |
   |  <span data-ttu-id="7a5ba-249">$outputPath</span><span class="sxs-lookup"><span data-stu-id="7a5ba-249">$outputPath</span></span> |<span data-ttu-id="7a5ba-250">The Azure Blob storage location where the Hive queries will output the results.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-250">The Azure Blob storage location where the Hive queries will output the results.</span></span> <span data-ttu-id="7a5ba-251">You don't need to change this variable.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-251">You don't need to change this variable.</span></span> |
   |  <span data-ttu-id="7a5ba-252">$hqlScriptFile</span><span class="sxs-lookup"><span data-stu-id="7a5ba-252">$hqlScriptFile</span></span> |<span data-ttu-id="7a5ba-253">The location and the file name of the HiveQL script file.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-253">The location and the file name of the HiveQL script file.</span></span> <span data-ttu-id="7a5ba-254">You don't need to change this variable.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-254">You don't need to change this variable.</span></span> |
4. <span data-ttu-id="7a5ba-255">Press **F5** to run the script.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-255">Press **F5** to run the script.</span></span> <span data-ttu-id="7a5ba-256">If you run into problems, as a workaround, select all the lines, and then press **F8**.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-256">If you run into problems, as a workaround, select all the lines, and then press **F8**.</span></span>
5. <span data-ttu-id="7a5ba-257">You shall see "Complete!"</span><span class="sxs-lookup"><span data-stu-id="7a5ba-257">You shall see "Complete!"</span></span> <span data-ttu-id="7a5ba-258">at the end of the output.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-258">at the end of the output.</span></span> <span data-ttu-id="7a5ba-259">Any error messages will be displayed in red.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-259">Any error messages will be displayed in red.</span></span>

<span data-ttu-id="7a5ba-260">As a validation procedure, you can check the output file, **/tutorials/twitter/twitter.hql**, on your Azure Blob storage by using an Azure storage explorer or Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-260">As a validation procedure, you can check the output file, **/tutorials/twitter/twitter.hql**, on your Azure Blob storage by using an Azure storage explorer or Azure PowerShell.</span></span> <span data-ttu-id="7a5ba-261">For a sample Windows PowerShell script for listing files, see [Use Blob storage with HDInsight][hdinsight-storage-powershell].</span><span class="sxs-lookup"><span data-stu-id="7a5ba-261">For a sample Windows PowerShell script for listing files, see [Use Blob storage with HDInsight][hdinsight-storage-powershell].</span></span>

## <a name="process-twitter-data-by-using-hive"></a><span data-ttu-id="7a5ba-262">Process Twitter data by using Hive</span><span class="sxs-lookup"><span data-stu-id="7a5ba-262">Process Twitter data by using Hive</span></span>
<span data-ttu-id="7a5ba-263">You have finished all the preparation work.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-263">You have finished all the preparation work.</span></span> <span data-ttu-id="7a5ba-264">Now, you can invoke the Hive script and check the results.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-264">Now, you can invoke the Hive script and check the results.</span></span>

### <a name="submit-a-hive-job"></a><span data-ttu-id="7a5ba-265">Submit a Hive job</span><span class="sxs-lookup"><span data-stu-id="7a5ba-265">Submit a Hive job</span></span>
<span data-ttu-id="7a5ba-266">Use the following Windows PowerShell script to run the Hive script.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-266">Use the following Windows PowerShell script to run the Hive script.</span></span> <span data-ttu-id="7a5ba-267">You will need to set the first variable.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-267">You will need to set the first variable.</span></span>

> [!NOTE]
> <span data-ttu-id="7a5ba-268">To use the tweets and the HiveQL script you uploaded in the last two sections, set $hqlScriptFile to "/tutorials/twitter/twitter.hql".</span><span class="sxs-lookup"><span data-stu-id="7a5ba-268">To use the tweets and the HiveQL script you uploaded in the last two sections, set $hqlScriptFile to "/tutorials/twitter/twitter.hql".</span></span> <span data-ttu-id="7a5ba-269">To use the ones that have been uploaded to a public blob for you, set $hqlScriptFile to "wasbs://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql".</span><span class="sxs-lookup"><span data-stu-id="7a5ba-269">To use the ones that have been uploaded to a public blob for you, set $hqlScriptFile to "wasbs://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql".</span></span>

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"
$httpUserName = "admin"
$httpUserPassword = "<HDInsight Cluster HTTP User Password>"

#use one of the following
$hqlScriptFile = "wasbs://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql"
$hqlScriptFile = "/tutorials/twitter/twitter.hql"

$statusFolder = "/tutorials/twitter/jobstatus"
#endregion

$myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroupName = $myCluster.ResourceGroup
$defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
$defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value

$defaultBlobContainerName = $myCluster.DefaultStorageContainer

#region - Invoke Hive
Write-Host "Invoke Hive ... " -ForegroundColor Green

# Create the HDInsight cluster
$pw = ConvertTo-SecureString -String $httpUserPassword -AsPlainText -Force
$httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

Use-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName -HttpCredential $httpCredential
$response = Invoke-AzureRmHDInsightHiveJob -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -file $hqlScriptFile -StatusFolder $statusFolder #-OutVariable $outVariable

Write-Host "Display the standard error log ... " -ForegroundColor Green
$jobID = ($response | Select-String job_ | Select-Object -First 1) -replace ‘\s*$’ -replace ‘.*\s’
Get-AzureRmHDInsightJobOutput -ClusterName $clusterName -JobId $jobID -DefaultContainer $defaultBlobContainerName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -HttpCredential $httpCredential
#endregion
```

### <a name="check-the-results"></a><span data-ttu-id="7a5ba-270">Check the results</span><span class="sxs-lookup"><span data-stu-id="7a5ba-270">Check the results</span></span>
<span data-ttu-id="7a5ba-271">Use the following Windows PowerShell script to check the Hive job output.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-271">Use the following Windows PowerShell script to check the Hive job output.</span></span> <span data-ttu-id="7a5ba-272">You will need to set the first two variables.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-272">You will need to set the first two variables.</span></span>

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"

$blob = "tutorials/twitter/output/000000_0" # The name of the blob to be downloaded.
#endregion

#region - Create an Azure storage context object
Write-Host "Get the default storage account name and container name based on the cluster name ..." -ForegroundColor Green
$myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroupName = $myCluster.ResourceGroup
$defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
$defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
$defaultBlobContainerName = $myCluster.DefaultStorageContainer

Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

Write-Host "Create a context object ... " -ForegroundColor Green
$storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
#endregion

#region - Download blob and display blob
Write-Host "Download the blob ..." -ForegroundColor Green
cd $HOME
Get-AzureStorageBlobContent -Container $defaultBlobContainerName -Blob $blob -Context $storageContext -Force

Write-Host "Display the output ..." -ForegroundColor Green
Write-Host "==================================" -ForegroundColor Green
cat "./$blob"
Write-Host "==================================" -ForegroundColor Green
#end region
```

> [!NOTE]
> The Hive table uses \001 as the field delimiter. <span data-ttu-id="7a5ba-274">The delimiter is not visible in the output.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-274">The delimiter is not visible in the output.</span></span>

<span data-ttu-id="7a5ba-275">After the analysis results have been placed in Azure Blob storage, you can export the data to an Azure SQL database/SQL server, export the data to Excel by using Power Query, or connect your application to the data by using the Hive ODBC Driver.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-275">After the analysis results have been placed in Azure Blob storage, you can export the data to an Azure SQL database/SQL server, export the data to Excel by using Power Query, or connect your application to the data by using the Hive ODBC Driver.</span></span> <span data-ttu-id="7a5ba-276">For more information, see [Use Sqoop with HDInsight][hdinsight-use-sqoop], [Analyze flight delay data using HDInsight][hdinsight-analyze-flight-delay-data], [Connect Excel to HDInsight with Power Query][hdinsight-power-query], and [Connect Excel to HDInsight with the Microsoft Hive ODBC Driver][hdinsight-hive-odbc].</span><span class="sxs-lookup"><span data-stu-id="7a5ba-276">For more information, see [Use Sqoop with HDInsight][hdinsight-use-sqoop], [Analyze flight delay data using HDInsight][hdinsight-analyze-flight-delay-data], [Connect Excel to HDInsight with Power Query][hdinsight-power-query], and [Connect Excel to HDInsight with the Microsoft Hive ODBC Driver][hdinsight-hive-odbc].</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a5ba-277">Next steps</span><span class="sxs-lookup"><span data-stu-id="7a5ba-277">Next steps</span></span>
<span data-ttu-id="7a5ba-278">In this tutorial we have seen how to transform an unstructured JSON dataset into a structured Hive table to query, explore, and analyze data from Twitter by using HDInsight on Azure.</span><span class="sxs-lookup"><span data-stu-id="7a5ba-278">In this tutorial we have seen how to transform an unstructured JSON dataset into a structured Hive table to query, explore, and analyze data from Twitter by using HDInsight on Azure.</span></span> <span data-ttu-id="7a5ba-279">To learn more, see:</span><span class="sxs-lookup"><span data-stu-id="7a5ba-279">To learn more, see:</span></span>

* <span data-ttu-id="7a5ba-280">[Get started with HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="7a5ba-280">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="7a5ba-281">[Analyze real-time Twitter sentiment with HBase in HDInsight][hdinsight-hbase-twitter-sentiment]</span><span class="sxs-lookup"><span data-stu-id="7a5ba-281">[Analyze real-time Twitter sentiment with HBase in HDInsight][hdinsight-hbase-twitter-sentiment]</span></span>
* <span data-ttu-id="7a5ba-282">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-delay-data]</span><span class="sxs-lookup"><span data-stu-id="7a5ba-282">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-delay-data]</span></span>
* <span data-ttu-id="7a5ba-283">[Connect Excel to HDInsight with Power Query][hdinsight-power-query]</span><span class="sxs-lookup"><span data-stu-id="7a5ba-283">[Connect Excel to HDInsight with Power Query][hdinsight-power-query]</span></span>
* <span data-ttu-id="7a5ba-284">[Connect Excel to HDInsight with the Microsoft Hive ODBC Driver][hdinsight-hive-odbc]</span><span class="sxs-lookup"><span data-stu-id="7a5ba-284">[Connect Excel to HDInsight with the Microsoft Hive ODBC Driver][hdinsight-hive-odbc]</span></span>
* <span data-ttu-id="7a5ba-285">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="7a5ba-285">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176961.aspx

[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]:hdinsight-hadoop-use-blob-storage.md#access-blobs-using-azure-powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-odbc-driver.md
[hdinsight-hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
