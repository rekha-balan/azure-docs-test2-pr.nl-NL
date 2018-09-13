---
title: 'Quickstart: Submit a workflow using multiple inputs | Microsoft Docs'
titleSuffix: Azure
description: The quickstart assumes you have the msgen client installed and have successfully run the sample data through the service.
services: microsoft-genomics
author: grhuynh
manager: jhubbard
editor: jasonwhowell
ms.author: grhuynh
ms.service: microsoft-genomics
ms.workload: genomics
ms.topic: quickstart
ms.date: 02/05/2018
ms.openlocfilehash: 7aeb4d5ad939cefcf8300b78b4afcc9d91ca0624
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966512"
---
# <a name="submit-a-workflow-using-multiple-inputs-from-the-same-sample"></a><span data-ttu-id="95e19-103">Submit a workflow using multiple inputs from the same sample</span><span class="sxs-lookup"><span data-stu-id="95e19-103">Submit a workflow using multiple inputs from the same sample</span></span>

<span data-ttu-id="95e19-104">This quickstart demonstrates how to submit a workflow to the Microsoft Genomics service if your input file is multiple FASTQ or BAM files **coming from the same sample**.</span><span class="sxs-lookup"><span data-stu-id="95e19-104">This quickstart demonstrates how to submit a workflow to the Microsoft Genomics service if your input file is multiple FASTQ or BAM files **coming from the same sample**.</span></span> <span data-ttu-id="95e19-105">For example, if you ran the **same sample** in multiple lanes on the sequencer, the sequencer could output a pair of FASTQ files for each lane.</span><span class="sxs-lookup"><span data-stu-id="95e19-105">For example, if you ran the **same sample** in multiple lanes on the sequencer, the sequencer could output a pair of FASTQ files for each lane.</span></span> <span data-ttu-id="95e19-106">Rather than concatenating these FASTQ files prior to alignment and variant calling, you can directly submit all of these inputs to the `msgen` client.</span><span class="sxs-lookup"><span data-stu-id="95e19-106">Rather than concatenating these FASTQ files prior to alignment and variant calling, you can directly submit all of these inputs to the `msgen` client.</span></span> <span data-ttu-id="95e19-107">The output from the `msgen` client would be a **single set** of files, including a .bam, .bai, .vcf file.</span><span class="sxs-lookup"><span data-stu-id="95e19-107">The output from the `msgen` client would be a **single set** of files, including a .bam, .bai, .vcf file.</span></span> 

<span data-ttu-id="95e19-108">Keep in mind, however, that you **cannot** mix FASTQ and BAM files in the same submission.</span><span class="sxs-lookup"><span data-stu-id="95e19-108">Keep in mind, however, that you **cannot** mix FASTQ and BAM files in the same submission.</span></span> <span data-ttu-id="95e19-109">Further, you **cannot** submit multiple FASTQ or BAM files from multiple individuals.</span><span class="sxs-lookup"><span data-stu-id="95e19-109">Further, you **cannot** submit multiple FASTQ or BAM files from multiple individuals.</span></span> 

<span data-ttu-id="95e19-110">This article assumes you have already installed and run the `msgen` client, and are familiar with how to use Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="95e19-110">This article assumes you have already installed and run the `msgen` client, and are familiar with how to use Azure Storage.</span></span> <span data-ttu-id="95e19-111">If you have successfully submitted a workflow using the provided sample data, you are ready to proceed with this quickstart.</span><span class="sxs-lookup"><span data-stu-id="95e19-111">If you have successfully submitted a workflow using the provided sample data, you are ready to proceed with this quickstart.</span></span> 


## <a name="multiple-bam-files"></a><span data-ttu-id="95e19-112">Multiple BAM files</span><span class="sxs-lookup"><span data-stu-id="95e19-112">Multiple BAM files</span></span>

### <a name="upload-your-input-files-to-azure-storage"></a><span data-ttu-id="95e19-113">Upload your input files to Azure storage</span><span class="sxs-lookup"><span data-stu-id="95e19-113">Upload your input files to Azure storage</span></span>
<span data-ttu-id="95e19-114">Let’s assume you have multiple BAM files as input, *reads.bam*, *additional_reads.bam*, and *yet_more_reads.bam*, and you have uploaded them to your storage account *myaccount* in Azure.</span><span class="sxs-lookup"><span data-stu-id="95e19-114">Let’s assume you have multiple BAM files as input, *reads.bam*, *additional_reads.bam*, and *yet_more_reads.bam*, and you have uploaded them to your storage account *myaccount* in Azure.</span></span> <span data-ttu-id="95e19-115">You have the API URL and your access key.</span><span class="sxs-lookup"><span data-stu-id="95e19-115">You have the API URL and your access key.</span></span> <span data-ttu-id="95e19-116">You want to have outputs in **https://<span></span>myaccount.blob.core<span></span>.windows<span></span>.net<span></span>/outputs<span></span>**.</span><span class="sxs-lookup"><span data-stu-id="95e19-116">You want to have outputs in **https://<span></span>myaccount.blob.core<span></span>.windows<span></span>.net<span></span>/outputs<span></span>**.</span></span>


### <a name="submit-your-job-to-the-msgen-client"></a><span data-ttu-id="95e19-117">Submit your job to the `msgen` client</span><span class="sxs-lookup"><span data-stu-id="95e19-117">Submit your job to the `msgen` client</span></span> 

<span data-ttu-id="95e19-118">You can submit multiple BAM files by passing all their names to the --input-blob-name-1 argument.</span><span class="sxs-lookup"><span data-stu-id="95e19-118">You can submit multiple BAM files by passing all their names to the --input-blob-name-1 argument.</span></span> <span data-ttu-id="95e19-119">Note that all files should come from the same sample, but their order is not important.</span><span class="sxs-lookup"><span data-stu-id="95e19-119">Note that all files should come from the same sample, but their order is not important.</span></span> <span data-ttu-id="95e19-120">The following section details example submissions from a command line in Windows, in Unix, and using a configuration file.</span><span class="sxs-lookup"><span data-stu-id="95e19-120">The following section details example submissions from a command line in Windows, in Unix, and using a configuration file.</span></span> <span data-ttu-id="95e19-121">Line breaks are added for clarity:</span><span class="sxs-lookup"><span data-stu-id="95e19-121">Line breaks are added for clarity:</span></span>


<span data-ttu-id="95e19-122">For Windows:</span><span class="sxs-lookup"><span data-stu-id="95e19-122">For Windows:</span></span>

```
msgen submit ^
  --api-url-base <Genomics API URL> ^
  --access-key <Genomics access key> ^
  --process-args R=b37m1 ^
  --input-storage-account-name myaccount ^
  --input-storage-account-key <storage access key to "myaccount"> ^
  --input-storage-account-container inputs ^
  --input-blob-name-1 reads.bam additional_reads.bam yet_more_reads.bam ^
  --output-storage-account-name myaccount ^
  --output-storage-account-key <storage access key to "myaccount"> ^
  --output-storage-account-container outputs
```


<span data-ttu-id="95e19-123">For Unix</span><span class="sxs-lookup"><span data-stu-id="95e19-123">For Unix</span></span>

```
msgen submit \
  --api-url-base <Genomics API URL> \
  --access-key <Genomics access key> \
  --process-args R=b37m1 \
  --input-storage-account-name myaccount \
  --input-storage-account-key <storage access key to "myaccount"> \
  --input-storage-account-container inputs \
  --input-blob-name-1 reads.bam additional_reads.bam yet_more_reads.bam \
  --output-storage-account-name myaccount \
  --output-storage-account-key <storage access key to "myaccount"> \
  --output-storage-account-container outputs
```


<span data-ttu-id="95e19-124">If you prefer using a configuration file, here is what it would contain:</span><span class="sxs-lookup"><span data-stu-id="95e19-124">If you prefer using a configuration file, here is what it would contain:</span></span>

``` config.txt
api_url_base:                     <Genomics API URL>
access_key:                       <Genomics access key>
process_args:                     R=b37m1
input_storage_account_name:       myaccount
input_storage_account_key:        <storage access key to "myaccount">
input_storage_account_container:  inputs
input_blob_name_1:                reads.bam additional_reads.bam yet_more_reads.bam
output_storage_account_name:      myaccount
output_storage_account_key:       <storage access key to "myaccount">
output_storage_account_container: outputs
```

<span data-ttu-id="95e19-125">Submit the `config.txt` file with this invocation: `msgen submit -f config.txt`</span><span class="sxs-lookup"><span data-stu-id="95e19-125">Submit the `config.txt` file with this invocation: `msgen submit -f config.txt`</span></span>


## <a name="multiple-paired-fastq-files"></a><span data-ttu-id="95e19-126">Multiple paired FASTQ files</span><span class="sxs-lookup"><span data-stu-id="95e19-126">Multiple paired FASTQ files</span></span>

### <a name="upload-your-input-files-to-azure-storage"></a><span data-ttu-id="95e19-127">Upload your input files to Azure storage</span><span class="sxs-lookup"><span data-stu-id="95e19-127">Upload your input files to Azure storage</span></span>
<span data-ttu-id="95e19-128">Let’s assume you have multiple paired FASTQ files as input, *reads_1.fq.gz* and *reads_2.fq.gz*,  *additional_reads_1.fq.gz* and *additional_reads_2.fq.gz*, and *yet_more_reads_1.fq.gz* and  *yet_more_reads_2.fq.gz*.</span><span class="sxs-lookup"><span data-stu-id="95e19-128">Let’s assume you have multiple paired FASTQ files as input, *reads_1.fq.gz* and *reads_2.fq.gz*,  *additional_reads_1.fq.gz* and *additional_reads_2.fq.gz*, and *yet_more_reads_1.fq.gz* and  *yet_more_reads_2.fq.gz*.</span></span> <span data-ttu-id="95e19-129">You have uploaded them to your storage account *myaccount* in Azure and you.have the API URL and your access key.</span><span class="sxs-lookup"><span data-stu-id="95e19-129">You have uploaded them to your storage account *myaccount* in Azure and you.have the API URL and your access key.</span></span> <span data-ttu-id="95e19-130">You want to have outputs in **https://<span></span>myaccount.blob.core<span></span>.windows<span></span>.net<span></span>/outputs<span></span>**.</span><span class="sxs-lookup"><span data-stu-id="95e19-130">You want to have outputs in **https://<span></span>myaccount.blob.core<span></span>.windows<span></span>.net<span></span>/outputs<span></span>**.</span></span>


### <a name="submit-your-job-to-the-msgen-client"></a><span data-ttu-id="95e19-131">Submit your job to the `msgen` client</span><span class="sxs-lookup"><span data-stu-id="95e19-131">Submit your job to the `msgen` client</span></span> 

<span data-ttu-id="95e19-132">Paired FASTQ files not only need to come from the same sample, but they also need to be processed together.</span><span class="sxs-lookup"><span data-stu-id="95e19-132">Paired FASTQ files not only need to come from the same sample, but they also need to be processed together.</span></span>  <span data-ttu-id="95e19-133">The order of the file names matters when they are passed as arguments to --input-blob-name-1 and --input-blob-name-2.</span><span class="sxs-lookup"><span data-stu-id="95e19-133">The order of the file names matters when they are passed as arguments to --input-blob-name-1 and --input-blob-name-2.</span></span> 

<span data-ttu-id="95e19-134">The following section details example submissions from a command line in Windows, in Unix, and using a configuration file.</span><span class="sxs-lookup"><span data-stu-id="95e19-134">The following section details example submissions from a command line in Windows, in Unix, and using a configuration file.</span></span> <span data-ttu-id="95e19-135">Line breaks are added for clarity:</span><span class="sxs-lookup"><span data-stu-id="95e19-135">Line breaks are added for clarity:</span></span>


<span data-ttu-id="95e19-136">For Windows:</span><span class="sxs-lookup"><span data-stu-id="95e19-136">For Windows:</span></span>

```
msgen submit ^
  --api-url-base <Genomics API URL> ^
  --access-key <Genomics access key> ^
  --process-args R=b37m1 ^
  --input-storage-account-name myaccount ^
  --input-storage-account-key <storage access key to "myaccount"> ^
  --input-storage-account-container inputs ^
  --input-blob-name-1 reads_1.fastq.gz additional_reads_1.fastq.gz yet_more_reads_1.fastq.gz ^
  --input-blob-name-2 reads_2.fastq.gz additional_reads_2.fastq.gz yet_more_reads_2.fastq.gz ^
  --output-storage-account-name myaccount ^
  --output-storage-account-key <storage access key to "myaccount"> ^
  --output-storage-account-container outputs
```


<span data-ttu-id="95e19-137">For Unix:</span><span class="sxs-lookup"><span data-stu-id="95e19-137">For Unix:</span></span>

```
msgen submit \
  --api-url-base <Genomics API URL> \
  --access-key <Genomics access key> \
  --process-args R=b37m1 \
  --input-storage-account-name myaccount \
  --input-storage-account-key <storage access key to "myaccount"> \
  --input-storage-account-container inputs \
  --input-blob-name-1 reads_1.fastq.gz additional_reads_1.fastq.gz yet_more_reads_1.fastq.gz \
  --input-blob-name-2 reads_2.fastq.gz additional_reads_2.fastq.gz yet_more_reads_2.fastq.gz \
  --output-storage-account-name myaccount \
  --output-storage-account-key <storage access key to "myaccount"> \
  --output-storage-account-container outputs
```


<span data-ttu-id="95e19-138">If you prefer using a configuration file, here is what it would contain:</span><span class="sxs-lookup"><span data-stu-id="95e19-138">If you prefer using a configuration file, here is what it would contain:</span></span>

```
api_url_base:                     <Genomics API URL>
access_key:                       <Genomics access key>
process_args:                     R=b37m1
input_storage_account_name:       myaccount
input_storage_account_key:        <storage access key to "myaccount">
input_storage_account_container:  inputs
input_blob_name_1:                reads_1.fq.gz additional_reads_1.fastq.gz yet_more_reads_1.fastq.gz
input_blob_name_2:                reads_2.fq.gz additional_reads_2.fastq.gz yet_more_reads_2.fastq.gz
output_storage_account_name:      myaccount
output_storage_account_key:       <storage access key to "myaccount">
output_storage_account_container: outputs
```

<span data-ttu-id="95e19-139">Submit the `config.txt` file with this invocation: `msgen submit -f config.txt`</span><span class="sxs-lookup"><span data-stu-id="95e19-139">Submit the `config.txt` file with this invocation: `msgen submit -f config.txt`</span></span>

## <a name="next-steps"></a><span data-ttu-id="95e19-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="95e19-140">Next steps</span></span>
<span data-ttu-id="95e19-141">In this article, you uploaded multiple BAM files or paired FASTQ files into Azure Storage and submitted a workflow to the Microsoft Genomics service through the `msgen` python client.</span><span class="sxs-lookup"><span data-stu-id="95e19-141">In this article, you uploaded multiple BAM files or paired FASTQ files into Azure Storage and submitted a workflow to the Microsoft Genomics service through the `msgen` python client.</span></span> <span data-ttu-id="95e19-142">For more information regarding workflow submission and other commands you can use with the Microsoft Genomics service, see the [FAQ](frequently-asked-questions-genomics.md).</span><span class="sxs-lookup"><span data-stu-id="95e19-142">For more information regarding workflow submission and other commands you can use with the Microsoft Genomics service, see the [FAQ](frequently-asked-questions-genomics.md).</span></span> 