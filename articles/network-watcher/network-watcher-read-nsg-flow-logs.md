---
title: Read NSG flow logs | Microsoft Docs
description: This article shows how to parse NSG flow logs
services: network-watcher
documentationcenter: na
author: jimdial
manager: timlt
editor: ''
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: jdial
ms.openlocfilehash: 63407382762a814ded4529caa109d76e987c9505
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870956"
---
# <a name="read-nsg-flow-logs"></a><span data-ttu-id="0f7a3-103">Read NSG flow logs</span><span class="sxs-lookup"><span data-stu-id="0f7a3-103">Read NSG flow logs</span></span>

<span data-ttu-id="0f7a3-104">Learn how to read NSG flow logs entries with PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0f7a3-104">Learn how to read NSG flow logs entries with PowerShell.</span></span>

<span data-ttu-id="0f7a3-105">NSG flow logs are stored in a storage account in [block blobs](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs).</span><span class="sxs-lookup"><span data-stu-id="0f7a3-105">NSG flow logs are stored in a storage account in [block blobs](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs).</span></span> <span data-ttu-id="0f7a3-106">Block blobs are made up of smaller blocks.</span><span class="sxs-lookup"><span data-stu-id="0f7a3-106">Block blobs are made up of smaller blocks.</span></span> <span data-ttu-id="0f7a3-107">Each log is a separate block blob that is generated every hour.</span><span class="sxs-lookup"><span data-stu-id="0f7a3-107">Each log is a separate block blob that is generated every hour.</span></span> <span data-ttu-id="0f7a3-108">New logs are generated every hour, the logs are updated with new entries every few minutes with the latest data.</span><span class="sxs-lookup"><span data-stu-id="0f7a3-108">New logs are generated every hour, the logs are updated with new entries every few minutes with the latest data.</span></span> <span data-ttu-id="0f7a3-109">In this article you learn how to read portions of the flow logs.</span><span class="sxs-lookup"><span data-stu-id="0f7a3-109">In this article you learn how to read portions of the flow logs.</span></span>

## <a name="scenario"></a><span data-ttu-id="0f7a3-110">Scenario</span><span class="sxs-lookup"><span data-stu-id="0f7a3-110">Scenario</span></span>

<span data-ttu-id="0f7a3-111">In the following scenario, you have an example flow log that is stored in a storage account.</span><span class="sxs-lookup"><span data-stu-id="0f7a3-111">In the following scenario, you have an example flow log that is stored in a storage account.</span></span> <span data-ttu-id="0f7a3-112">You learn how to selectively read the latest events in NSG flow logs.</span><span class="sxs-lookup"><span data-stu-id="0f7a3-112">You learn how to selectively read the latest events in NSG flow logs.</span></span> <span data-ttu-id="0f7a3-113">In this article you use PowerShell, however, the concepts discussed in the article are not limited to the programming language, and are applicable to all languages supported by the Azure Storage APIs.</span><span class="sxs-lookup"><span data-stu-id="0f7a3-113">In this article you use PowerShell, however, the concepts discussed in the article are not limited to the programming language, and are applicable to all languages supported by the Azure Storage APIs.</span></span>

## <a name="setup"></a><span data-ttu-id="0f7a3-114">Setup</span><span class="sxs-lookup"><span data-stu-id="0f7a3-114">Setup</span></span>

<span data-ttu-id="0f7a3-115">Before you begin, you must have Network Security Group Flow Logging enabled on one or many Network Security Groups in your account.</span><span class="sxs-lookup"><span data-stu-id="0f7a3-115">Before you begin, you must have Network Security Group Flow Logging enabled on one or many Network Security Groups in your account.</span></span> <span data-ttu-id="0f7a3-116">For instructions on enabling Network Security flow logs, refer to the following article: [Introduction to flow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0f7a3-116">For instructions on enabling Network Security flow logs, refer to the following article: [Introduction to flow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>

## <a name="retrieve-the-block-list"></a><span data-ttu-id="0f7a3-117">Retrieve the block list</span><span class="sxs-lookup"><span data-stu-id="0f7a3-117">Retrieve the block list</span></span>

<span data-ttu-id="0f7a3-118">The following PowerShell sets up the variables needed to query the NSG flow log blob and list the blocks within the [CloudBlockBlob](https://docs.microsoft.com/dotnet/api/microsoft.windowsazure.storage.blob.cloudblockblob?view=azurestorage-8.1.3) block blob.</span><span class="sxs-lookup"><span data-stu-id="0f7a3-118">The following PowerShell sets up the variables needed to query the NSG flow log blob and list the blocks within the [CloudBlockBlob](https://docs.microsoft.com/dotnet/api/microsoft.windowsazure.storage.blob.cloudblockblob?view=azurestorage-8.1.3) block blob.</span></span> <span data-ttu-id="0f7a3-119">Update the script to contain valid values for your environment.</span><span class="sxs-lookup"><span data-stu-id="0f7a3-119">Update the script to contain valid values for your environment.</span></span>

```powershell
function Get-NSGFlowLogBlockList {
    [CmdletBinding()]
    param (
        [string] [Parameter(Mandatory=$true)] $subscriptionId,
        [string] [Parameter(Mandatory=$true)] $NSGResourceGroupName,
        [string] [Parameter(Mandatory=$true)] $NSGName,
        [string] [Parameter(Mandatory=$true)] $storageAccountName,
        [string] [Parameter(Mandatory=$true)] $storageAccountResourceGroup,
        [string] [Parameter(Mandatory=$true)] $macAddress,
        [datetime] [Parameter(Mandatory=$true)] $logTime
    )

    process {
        # Retrieve the primary storage account key to access the NSG logs
        $StorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccountResourceGroup -Name $storageAccountName).Value[0]

        # Setup a new storage context to be used to query the logs
        $ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

        # Container name used by NSG flow logs
        $ContainerName = "insights-logs-networksecuritygroupflowevent"

        # Name of the blob that contains the NSG flow log
        $BlobName = "resourceId=/SUBSCRIPTIONS/${subscriptionId}/RESOURCEGROUPS/${NSGResourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/${NSGName}/y=$($logTime.Year)/m=$(($logTime).ToString("MM"))/d=$(($logTime).ToString("dd"))/h=$(($logTime).ToString("HH"))/m=00/macAddress=$($macAddress)/PT1H.json"

        # Gets the storage blog
        $Blob = Get-AzureStorageBlob -Context $ctx -Container $ContainerName -Blob $BlobName

        # Gets the block blog of type 'Microsoft.WindowsAzure.Storage.Blob.CloudBlob' from the storage blob
        $CloudBlockBlob = [Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob] $Blob.ICloudBlob

        # Stores the block list in a variable from the block blob.
        $blockList = $CloudBlockBlob.DownloadBlockList()

        # Return the Block List
        $blockList
    }
}
$blockList = Get-NSGFlowLogBlockList -subscriptionId "00000000-0000-0000-0000-000000000000" -NSGResourceGroupName "resourcegroupname" -storageAccountName "storageaccountname" -storageAccountResourceGroup "sa-rg" -macAddress "000D3AF8196E" -logTime "03/07/2018 22:00"
```

<span data-ttu-id="0f7a3-120">The `$blockList` variable returns a list of the blocks in the blob.</span><span class="sxs-lookup"><span data-stu-id="0f7a3-120">The `$blockList` variable returns a list of the blocks in the blob.</span></span> <span data-ttu-id="0f7a3-121">Each block blob contains at least two blocks.</span><span class="sxs-lookup"><span data-stu-id="0f7a3-121">Each block blob contains at least two blocks.</span></span>  <span data-ttu-id="0f7a3-122">The first block has a length of `21` bytes, this block contains the opening brackets of the json log.</span><span class="sxs-lookup"><span data-stu-id="0f7a3-122">The first block has a length of `21` bytes, this block contains the opening brackets of the json log.</span></span> <span data-ttu-id="0f7a3-123">The other block is the closing brackets and has a length of `9` bytes.</span><span class="sxs-lookup"><span data-stu-id="0f7a3-123">The other block is the closing brackets and has a length of `9` bytes.</span></span>  <span data-ttu-id="0f7a3-124">As you can see the following example log has seven entries in it, each being an individual entry.</span><span class="sxs-lookup"><span data-stu-id="0f7a3-124">As you can see the following example log has seven entries in it, each being an individual entry.</span></span> <span data-ttu-id="0f7a3-125">All new entries in the log are added to the end right before the final block.</span><span class="sxs-lookup"><span data-stu-id="0f7a3-125">All new entries in the log are added to the end right before the final block.</span></span>

```
Name                                         Length Committed
----                                         ------ ---------
ZDk5MTk5N2FkNGE0MmY5MTk5ZWViYjA0YmZhODRhYzY=     12      True
NzQxNDA5MTRhNDUzMGI2M2Y1MDMyOWZlN2QwNDZiYzQ=   2685      True
ODdjM2UyMWY3NzFhZTU3MmVlMmU5MDNlOWEwNWE3YWY=   2586      True
ZDU2MjA3OGQ2ZDU3MjczMWQ4MTRmYWNhYjAzOGJkMTg=   2688      True
ZmM3ZWJjMGQ0ZDA1ODJlOWMyODhlOWE3MDI1MGJhMTc=   2775      True
ZGVkYTc4MzQzNjEyMzlmZWE5MmRiNjc1OWE5OTc0OTQ=   2676      True
ZmY2MjUzYTIwYWIyOGU1OTA2ZDY1OWYzNmY2NmU4ZTY=   2777      True
Mzk1YzQwM2U0ZWY1ZDRhOWFlMTNhYjQ3OGVhYmUzNjk=   2675      True
ZjAyZTliYWE3OTI1YWZmYjFmMWI0MjJhNzMxZTI4MDM=      2      True
```

## <a name="read-the-block-blob"></a><span data-ttu-id="0f7a3-126">Read the block blob</span><span class="sxs-lookup"><span data-stu-id="0f7a3-126">Read the block blob</span></span>

<span data-ttu-id="0f7a3-127">Next you need to read the `$blocklist` variable to retrieve the data.</span><span class="sxs-lookup"><span data-stu-id="0f7a3-127">Next you need to read the `$blocklist` variable to retrieve the data.</span></span> <span data-ttu-id="0f7a3-128">In this example we iterate through the blocklist, read the bytes from each block and story them in an array.</span><span class="sxs-lookup"><span data-stu-id="0f7a3-128">In this example we iterate through the blocklist, read the bytes from each block and story them in an array.</span></span> <span data-ttu-id="0f7a3-129">Use the [DownloadRangeToByteArray](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob.downloadrangetobytearray?view=azurestorage-8.1.3#Microsoft_WindowsAzure_Storage_Blob_CloudBlob_DownloadRangeToByteArray_System_Byte___System_Int32_System_Nullable_System_Int64__System_Nullable_System_Int64__Microsoft_WindowsAzure_Storage_AccessCondition_Microsoft_WindowsAzure_Storage_Blob_BlobRequestOptions_Microsoft_WindowsAzure_Storage_OperationContext_) method to retrieve the data.</span><span class="sxs-lookup"><span data-stu-id="0f7a3-129">Use the [DownloadRangeToByteArray](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob.downloadrangetobytearray?view=azurestorage-8.1.3#Microsoft_WindowsAzure_Storage_Blob_CloudBlob_DownloadRangeToByteArray_System_Byte___System_Int32_System_Nullable_System_Int64__System_Nullable_System_Int64__Microsoft_WindowsAzure_Storage_AccessCondition_Microsoft_WindowsAzure_Storage_Blob_BlobRequestOptions_Microsoft_WindowsAzure_Storage_OperationContext_) method to retrieve the data.</span></span>

```powershell
# Set the size of the byte array to the largest block
$maxvalue = ($blocklist | measure Length -Maximum).Maximum

# Create an array to store values in
$valuearray = @()

# Define the starting index to track the current block being read
$index = 0

# Loop through each block in the block list
for($i=0; $i -lt $blocklist.count; $i++)
{

# Create a byte array object to story the bytes from the block
$downloadArray = New-Object -TypeName byte[] -ArgumentList $maxvalue

# Download the data into the ByteArray, starting with the current index, for the number of bytes in the current block. Index is increased by 3 when reading to remove preceding comma.
$CloudBlockBlob.DownloadRangeToByteArray($downloadArray,0,$index+3,$($blockList[$i].Length-1)) | Out-Null

# Increment the index by adding the current block length to the previous index
$index = $index + $blockList[$i].Length

# Retrieve the string from the byte array

$value = [System.Text.Encoding]::ASCII.GetString($downloadArray)

# Add the log entry to the value array
$valuearray += $value
}
```

<span data-ttu-id="0f7a3-130">Now the `$valuearray` array contains the string value of each block.</span><span class="sxs-lookup"><span data-stu-id="0f7a3-130">Now the `$valuearray` array contains the string value of each block.</span></span> <span data-ttu-id="0f7a3-131">To verify the entry, get the second to the last value from the array by running `$valuearray[$valuearray.Length-2]`.</span><span class="sxs-lookup"><span data-stu-id="0f7a3-131">To verify the entry, get the second to the last value from the array by running `$valuearray[$valuearray.Length-2]`.</span></span> <span data-ttu-id="0f7a3-132">You do not want the last value, because it is the closing bracket.</span><span class="sxs-lookup"><span data-stu-id="0f7a3-132">You do not want the last value, because it is the closing bracket.</span></span>

<span data-ttu-id="0f7a3-133">The results of this value are shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="0f7a3-133">The results of this value are shown in the following example:</span></span>

```json
        {
             "time": "2017-06-16T20:59:43.7340000Z",
             "systemId": "5f4d02d3-a7d0-4ed4-9ce8-c0ae9377951c",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/CONTOSORG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/CONTOSONSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_AllowInternetOutBound","flows":[{"mac":"000D3A18077E","flowTuples":["1497646722,10.0.0.4,168.62.32.14,44904,443,T,O,A","1497646722,10.0.0.4,52.240.48.24,45218,443,T,O,A","1497646725,10.
0.0.4,168.62.32.14,44910,443,T,O,A","1497646725,10.0.0.4,52.240.48.24,45224,443,T,O,A","1497646728,10.0.0.4,168.62.32.14,44916,443,T,O,A","1497646728,10.0.0.4,52.240.48.24,45230,443,T,O,A","1497646732,10.0.0.4,168.62.32.14,44922,443,T,O,A","14976
46732,10.0.0.4,52.240.48.24,45236,443,T,O,A","1497646735,10.0.0.4,168.62.32.14,44928,443,T,O,A","1497646735,10.0.0.4,52.240.48.24,45242,443,T,O,A","1497646738,10.0.0.4,168.62.32.14,44934,443,T,O,A","1497646738,10.0.0.4,52.240.48.24,45248,443,T,O,
A","1497646742,10.0.0.4,168.62.32.14,44942,443,T,O,A","1497646742,10.0.0.4,52.240.48.24,45256,443,T,O,A","1497646745,10.0.0.4,168.62.32.14,44948,443,T,O,A","1497646745,10.0.0.4,52.240.48.24,45262,443,T,O,A","1497646749,10.0.0.4,168.62.32.14,44954
,443,T,O,A","1497646749,10.0.0.4,52.240.48.24,45268,443,T,O,A","1497646753,10.0.0.4,168.62.32.14,44960,443,T,O,A","1497646753,10.0.0.4,52.240.48.24,45274,443,T,O,A","1497646756,10.0.0.4,168.62.32.14,44966,443,T,O,A","1497646756,10.0.0.4,52.240.48
.24,45280,443,T,O,A","1497646759,10.0.0.4,168.62.32.14,44972,443,T,O,A","1497646759,10.0.0.4,52.240.48.24,45286,443,T,O,A","1497646763,10.0.0.4,168.62.32.14,44978,443,T,O,A","1497646763,10.0.0.4,52.240.48.24,45292,443,T,O,A","1497646766,10.0.0.4,
168.62.32.14,44984,443,T,O,A","1497646766,10.0.0.4,52.240.48.24,45298,443,T,O,A","1497646769,10.0.0.4,168.62.32.14,44990,443,T,O,A","1497646769,10.0.0.4,52.240.48.24,45304,443,T,O,A","1497646773,10.0.0.4,168.62.32.14,44996,443,T,O,A","1497646773,
10.0.0.4,52.240.48.24,45310,443,T,O,A","1497646776,10.0.0.4,168.62.32.14,45002,443,T,O,A","1497646776,10.0.0.4,52.240.48.24,45316,443,T,O,A","1497646779,10.0.0.4,168.62.32.14,45008,443,T,O,A","1497646779,10.0.0.4,52.240.48.24,45322,443,T,O,A"]}]}
,{"rule":"DefaultRule_DenyAllInBound","flows":[]},{"rule":"UserRule_ssh-rule","flows":[]},{"rule":"UserRule_web-rule","flows":[{"mac":"000D3A18077E","flowTuples":["1497646738,13.82.225.93,10.0.0.4,1180,80,T,I,A","1497646750,13.82.225.93,10.0.0.4,
1184,80,T,I,A","1497646768,13.82.225.93,10.0.0.4,1181,80,T,I,A","1497646780,13.82.225.93,10.0.0.4,1336,80,T,I,A"]}]}]}
        }
```

<span data-ttu-id="0f7a3-134">This scenario is an example of how to read entries in NSG flow logs without having to parse the entire log.</span><span class="sxs-lookup"><span data-stu-id="0f7a3-134">This scenario is an example of how to read entries in NSG flow logs without having to parse the entire log.</span></span> <span data-ttu-id="0f7a3-135">You can read new entries in the log as they are written by using the block ID or by tracking the length of blocks stored in the block blob.</span><span class="sxs-lookup"><span data-stu-id="0f7a3-135">You can read new entries in the log as they are written by using the block ID or by tracking the length of blocks stored in the block blob.</span></span> <span data-ttu-id="0f7a3-136">This allows you to read only the new entries.</span><span class="sxs-lookup"><span data-stu-id="0f7a3-136">This allows you to read only the new entries.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f7a3-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="0f7a3-137">Next steps</span></span>

<span data-ttu-id="0f7a3-138">Visit [visualize Azure Network Watcher NSG flow logs using open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md) to learn more about other ways to view NSG flow logs.</span><span class="sxs-lookup"><span data-stu-id="0f7a3-138">Visit [visualize Azure Network Watcher NSG flow logs using open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md) to learn more about other ways to view NSG flow logs.</span></span>

<span data-ttu-id="0f7a3-139">To learn more about storage blobs visit: [Azure Functions Blob storage bindings](../azure-functions/functions-bindings-storage-blob.md)</span><span class="sxs-lookup"><span data-stu-id="0f7a3-139">To learn more about storage blobs visit: [Azure Functions Blob storage bindings](../azure-functions/functions-bindings-storage-blob.md)</span></span>
