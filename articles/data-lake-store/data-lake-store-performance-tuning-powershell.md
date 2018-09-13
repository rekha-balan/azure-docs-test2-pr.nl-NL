---
title: Performance tuning guidance for using Powershell with Data Lake Store | Microsoft Docs
description: Tips on how to improve performance when using Azure PowerShell with Data Lake Store
services: data-lake-store
documentationcenter: ''
author: stewu
manager: jhubbard
editor: cgronlun
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.date: 01/09/2018
ms.author: stewu
ms.openlocfilehash: 7b19972ed4a75ac899a4b78b28ab36ba305a5a64
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864587"
---
# <a name="performance-tuning-guidance-for-using-powershell-with-azure-data-lake-store"></a><span data-ttu-id="26164-103">Performance tuning guidance for using PowerShell with Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="26164-103">Performance tuning guidance for using PowerShell with Azure Data Lake Store</span></span>

<span data-ttu-id="26164-104">This article lists the properties that can be tuned to get a better performance while using PowerShell to work with Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="26164-104">This article lists the properties that can be tuned to get a better performance while using PowerShell to work with Data Lake Store:</span></span>

## <a name="performance-related-properties"></a><span data-ttu-id="26164-105">Performance-related properties</span><span class="sxs-lookup"><span data-stu-id="26164-105">Performance-related properties</span></span>

| <span data-ttu-id="26164-106">Property</span><span class="sxs-lookup"><span data-stu-id="26164-106">Property</span></span>            | <span data-ttu-id="26164-107">Default</span><span class="sxs-lookup"><span data-stu-id="26164-107">Default</span></span> | <span data-ttu-id="26164-108">Description</span><span class="sxs-lookup"><span data-stu-id="26164-108">Description</span></span> |
|---------------------|---------|-------------|
| <span data-ttu-id="26164-109">PerFileThreadCount</span><span class="sxs-lookup"><span data-stu-id="26164-109">PerFileThreadCount</span></span>  | <span data-ttu-id="26164-110">10</span><span class="sxs-lookup"><span data-stu-id="26164-110">10</span></span>      | <span data-ttu-id="26164-111">This parameter enables you to choose the number of parallel threads for uploading or downloading each file.</span><span class="sxs-lookup"><span data-stu-id="26164-111">This parameter enables you to choose the number of parallel threads for uploading or downloading each file.</span></span> <span data-ttu-id="26164-112">This number represents the max threads that can be allocated per file, but you may get fewer threads depending on your scenario (for example, if you are uploading a 1-KB file, you get one thread even if you ask for 20 threads).</span><span class="sxs-lookup"><span data-stu-id="26164-112">This number represents the max threads that can be allocated per file, but you may get fewer threads depending on your scenario (for example, if you are uploading a 1-KB file, you get one thread even if you ask for 20 threads).</span></span>  |
| <span data-ttu-id="26164-113">ConcurrentFileCount</span><span class="sxs-lookup"><span data-stu-id="26164-113">ConcurrentFileCount</span></span> | <span data-ttu-id="26164-114">10</span><span class="sxs-lookup"><span data-stu-id="26164-114">10</span></span>      | <span data-ttu-id="26164-115">This parameter is specifically for uploading or downloading folders.</span><span class="sxs-lookup"><span data-stu-id="26164-115">This parameter is specifically for uploading or downloading folders.</span></span> <span data-ttu-id="26164-116">This parameter determines the number of concurrent files that can be uploaded or downloaded.</span><span class="sxs-lookup"><span data-stu-id="26164-116">This parameter determines the number of concurrent files that can be uploaded or downloaded.</span></span> <span data-ttu-id="26164-117">This number represents the maximum number of concurrent files that can be uploaded or downloaded at one time, but you may get less concurrency depending on your scenario (for example, if you are uploading two files, you get two concurrent files uploads even if you ask for 15).</span><span class="sxs-lookup"><span data-stu-id="26164-117">This number represents the maximum number of concurrent files that can be uploaded or downloaded at one time, but you may get less concurrency depending on your scenario (for example, if you are uploading two files, you get two concurrent files uploads even if you ask for 15).</span></span> |

<span data-ttu-id="26164-118">**Example**</span><span class="sxs-lookup"><span data-stu-id="26164-118">**Example**</span></span>

<span data-ttu-id="26164-119">This command downloads files from Azure Data Lake Store to the user's local drive using 20 threads per file and 100 concurrent files.</span><span class="sxs-lookup"><span data-stu-id="26164-119">This command downloads files from Azure Data Lake Store to the user's local drive using 20 threads per file and 100 concurrent files.</span></span>

    Export-AzureRmDataLakeStoreItem -AccountName <Data Lake Store account name> -PerFileThreadCount 20-ConcurrentFileCount 100 -Path /Powershell/100GB/ -Destination C:\Performance\ -Force -Recurse

## <a name="how-do-i-determine-the-value-for-these-properties"></a><span data-ttu-id="26164-120">How do I determine the value for these properties?</span><span class="sxs-lookup"><span data-stu-id="26164-120">How do I determine the value for these properties?</span></span>

<span data-ttu-id="26164-121">The next question you might have is how to determine what value to provide for the performance-related properties.</span><span class="sxs-lookup"><span data-stu-id="26164-121">The next question you might have is how to determine what value to provide for the performance-related properties.</span></span> <span data-ttu-id="26164-122">Here's some guidance that you can use.</span><span class="sxs-lookup"><span data-stu-id="26164-122">Here's some guidance that you can use.</span></span>

* <span data-ttu-id="26164-123">**Step 1: Determine the total thread count** - You should start by calculating the total thread count to use.</span><span class="sxs-lookup"><span data-stu-id="26164-123">**Step 1: Determine the total thread count** - You should start by calculating the total thread count to use.</span></span> <span data-ttu-id="26164-124">As a general guideline, you should use six threads for each physical core.</span><span class="sxs-lookup"><span data-stu-id="26164-124">As a general guideline, you should use six threads for each physical core.</span></span>

        Total thread count = total physical cores * 6

    <span data-ttu-id="26164-125">**Example**</span><span class="sxs-lookup"><span data-stu-id="26164-125">**Example**</span></span>

    <span data-ttu-id="26164-126">Assuming you are running the PowerShell commands from a D14 VM that has 16 cores</span><span class="sxs-lookup"><span data-stu-id="26164-126">Assuming you are running the PowerShell commands from a D14 VM that has 16 cores</span></span>

        Total thread count = 16 cores * 6 = 96 threads


* <span data-ttu-id="26164-127">**Step 2: Calculate PerFileThreadCount**  - We calculate our PerFileThreadCount based on the size of the files.</span><span class="sxs-lookup"><span data-stu-id="26164-127">**Step 2: Calculate PerFileThreadCount**  - We calculate our PerFileThreadCount based on the size of the files.</span></span> <span data-ttu-id="26164-128">For files smaller than 2.5 GB, there is no need to change this parameter because the default of 10 is sufficient.</span><span class="sxs-lookup"><span data-stu-id="26164-128">For files smaller than 2.5 GB, there is no need to change this parameter because the default of 10 is sufficient.</span></span> <span data-ttu-id="26164-129">For files larger than 2.5 GB, you should use 10 threads as the base for the first 2.5 GB and add 1 thread for each additional 256-MB increase in file size.</span><span class="sxs-lookup"><span data-stu-id="26164-129">For files larger than 2.5 GB, you should use 10 threads as the base for the first 2.5 GB and add 1 thread for each additional 256-MB increase in file size.</span></span> <span data-ttu-id="26164-130">If you are copying a folder with a large range of file sizes, consider grouping them into similar file sizes.</span><span class="sxs-lookup"><span data-stu-id="26164-130">If you are copying a folder with a large range of file sizes, consider grouping them into similar file sizes.</span></span> <span data-ttu-id="26164-131">Having dissimilar file sizes may cause non-optimal performance.</span><span class="sxs-lookup"><span data-stu-id="26164-131">Having dissimilar file sizes may cause non-optimal performance.</span></span> <span data-ttu-id="26164-132">If that's not possible to group similar file sizes, you should set PerFileThreadCount based on the largest file size.</span><span class="sxs-lookup"><span data-stu-id="26164-132">If that's not possible to group similar file sizes, you should set PerFileThreadCount based on the largest file size.</span></span>

        PerFileThreadCount = 10 threads for the first 2.5 GB + 1 thread for each additional 256 MB increase in file size

    <span data-ttu-id="26164-133">**Example**</span><span class="sxs-lookup"><span data-stu-id="26164-133">**Example**</span></span>

    <span data-ttu-id="26164-134">Assuming you have 100 files ranging from 1 GB to 10 GB, we use the 10 GB as the largest file size for equation, which would read like the following.</span><span class="sxs-lookup"><span data-stu-id="26164-134">Assuming you have 100 files ranging from 1 GB to 10 GB, we use the 10 GB as the largest file size for equation, which would read like the following.</span></span>

        PerFileThreadCount = 10 + ((10 GB - 2.5 GB) / 256 MB) = 40 threads

* <span data-ttu-id="26164-135">**Step 3: Calculate ConcurrentFilecount** - Use the total thread count and PerFileThreadCount to calculate ConcurrentFileCount based on the following equation:</span><span class="sxs-lookup"><span data-stu-id="26164-135">**Step 3: Calculate ConcurrentFilecount** - Use the total thread count and PerFileThreadCount to calculate ConcurrentFileCount based on the following equation:</span></span>

        Total thread count = PerFileThreadCount * ConcurrentFileCount

    <span data-ttu-id="26164-136">**Example**</span><span class="sxs-lookup"><span data-stu-id="26164-136">**Example**</span></span>

    <span data-ttu-id="26164-137">Based on the example values we have been using</span><span class="sxs-lookup"><span data-stu-id="26164-137">Based on the example values we have been using</span></span>

        96 = 40 * ConcurrentFileCount

    <span data-ttu-id="26164-138">So, **ConcurrentFileCount** is **2.4**, which we can round off to **2**.</span><span class="sxs-lookup"><span data-stu-id="26164-138">So, **ConcurrentFileCount** is **2.4**, which we can round off to **2**.</span></span>

## <a name="further-tuning"></a><span data-ttu-id="26164-139">Further tuning</span><span class="sxs-lookup"><span data-stu-id="26164-139">Further tuning</span></span>

<span data-ttu-id="26164-140">You might require further tuning because there is a range of file sizes to work with.</span><span class="sxs-lookup"><span data-stu-id="26164-140">You might require further tuning because there is a range of file sizes to work with.</span></span> <span data-ttu-id="26164-141">The preceding calculation works well if all or most of the files are larger and closer to the 10-GB range.</span><span class="sxs-lookup"><span data-stu-id="26164-141">The preceding calculation works well if all or most of the files are larger and closer to the 10-GB range.</span></span> <span data-ttu-id="26164-142">If instead, there are many different files sizes with many files being smaller, then you could reduce PerFileThreadCount.</span><span class="sxs-lookup"><span data-stu-id="26164-142">If instead, there are many different files sizes with many files being smaller, then you could reduce PerFileThreadCount.</span></span> <span data-ttu-id="26164-143">By reducing the PerFileThreadCount, we can increase ConcurrentFileCount.</span><span class="sxs-lookup"><span data-stu-id="26164-143">By reducing the PerFileThreadCount, we can increase ConcurrentFileCount.</span></span> <span data-ttu-id="26164-144">So, if we assume that most of our files are smaller in the 5-GB range, we can redo our calculation:</span><span class="sxs-lookup"><span data-stu-id="26164-144">So, if we assume that most of our files are smaller in the 5-GB range, we can redo our calculation:</span></span>

    PerFileThreadCount = 10 + ((5 GB - 2.5 GB) / 256 MB) = 20

<span data-ttu-id="26164-145">So, **ConcurrentFileCount** becomes 96/20, which is 4.8, rounded off to **4**.</span><span class="sxs-lookup"><span data-stu-id="26164-145">So, **ConcurrentFileCount** becomes 96/20, which is 4.8, rounded off to **4**.</span></span>

<span data-ttu-id="26164-146">You can continue to tune these settings by changing the **PerFileThreadCount** up and down depending on the distribution of your file sizes.</span><span class="sxs-lookup"><span data-stu-id="26164-146">You can continue to tune these settings by changing the **PerFileThreadCount** up and down depending on the distribution of your file sizes.</span></span>

### <a name="limitation"></a><span data-ttu-id="26164-147">Limitation</span><span class="sxs-lookup"><span data-stu-id="26164-147">Limitation</span></span>

* <span data-ttu-id="26164-148">**Number of files is less than ConcurrentFileCount**: If the number of files you are uploading is smaller than the **ConcurrentFileCount** that you calculated, then you should reduce **ConcurrentFileCount** to be equal to the number of files.</span><span class="sxs-lookup"><span data-stu-id="26164-148">**Number of files is less than ConcurrentFileCount**: If the number of files you are uploading is smaller than the **ConcurrentFileCount** that you calculated, then you should reduce **ConcurrentFileCount** to be equal to the number of files.</span></span> <span data-ttu-id="26164-149">You can use any remaining threads to increase **PerFileThreadCount**.</span><span class="sxs-lookup"><span data-stu-id="26164-149">You can use any remaining threads to increase **PerFileThreadCount**.</span></span>

* <span data-ttu-id="26164-150">**Too many threads**: If you increase thread count too much without increasing your cluster size, you run the risk of degraded performance.</span><span class="sxs-lookup"><span data-stu-id="26164-150">**Too many threads**: If you increase thread count too much without increasing your cluster size, you run the risk of degraded performance.</span></span> <span data-ttu-id="26164-151">There can be contention issues when context-switching on the CPU.</span><span class="sxs-lookup"><span data-stu-id="26164-151">There can be contention issues when context-switching on the CPU.</span></span>

* <span data-ttu-id="26164-152">**Insufficient concurrency**: If the concurrency is not sufficient, then your cluster may be too small.</span><span class="sxs-lookup"><span data-stu-id="26164-152">**Insufficient concurrency**: If the concurrency is not sufficient, then your cluster may be too small.</span></span> <span data-ttu-id="26164-153">You can increase the number of nodes in your cluster, which gives you more concurrency.</span><span class="sxs-lookup"><span data-stu-id="26164-153">You can increase the number of nodes in your cluster, which gives you more concurrency.</span></span>

* <span data-ttu-id="26164-154">**Throttling errors**: You may see throttling errors if your concurrency is too high.</span><span class="sxs-lookup"><span data-stu-id="26164-154">**Throttling errors**: You may see throttling errors if your concurrency is too high.</span></span> <span data-ttu-id="26164-155">If you are seeing throttling errors, you should either reduce the concurrency or contact us.</span><span class="sxs-lookup"><span data-stu-id="26164-155">If you are seeing throttling errors, you should either reduce the concurrency or contact us.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26164-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="26164-156">Next steps</span></span>
* [<span data-ttu-id="26164-157">Use Azure Data Lake Store for big data requirements</span><span class="sxs-lookup"><span data-stu-id="26164-157">Use Azure Data Lake Store for big data requirements</span></span>](data-lake-store-data-scenarios.md) 
* [<span data-ttu-id="26164-158">Secure data in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="26164-158">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="26164-159">Use Azure Data Lake Analytics with Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="26164-159">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="26164-160">Use Azure HDInsight with Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="26164-160">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

