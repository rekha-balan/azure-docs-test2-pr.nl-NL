---
title: 'Quickstart: Submit a workflow using FASTQ file inputs | Microsoft Docs'
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
ms.date: 12/07/2017
ms.openlocfilehash: f093397803f21c023a2c32e42709ecfcd0e3aec7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867148"
---
# <a name="submit-a-workflow-using-fastq-file-inputs"></a><span data-ttu-id="4ac3d-103">Submit a workflow using FASTQ file inputs</span><span class="sxs-lookup"><span data-stu-id="4ac3d-103">Submit a workflow using FASTQ file inputs</span></span>

<span data-ttu-id="4ac3d-104">This quickstart demonstrates how to submit a workflow to the Microsoft Genomics service if your input files are a single pair of FASTQ files.</span><span class="sxs-lookup"><span data-stu-id="4ac3d-104">This quickstart demonstrates how to submit a workflow to the Microsoft Genomics service if your input files are a single pair of FASTQ files.</span></span> <span data-ttu-id="4ac3d-105">This topic assumes you have already installed and run the `msgen` client, and are familiar with how to use Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="4ac3d-105">This topic assumes you have already installed and run the `msgen` client, and are familiar with how to use Azure Storage.</span></span> <span data-ttu-id="4ac3d-106">If you have successfully submitted a workflow using the provided sample data, you are ready to proceed with this quickstart.</span><span class="sxs-lookup"><span data-stu-id="4ac3d-106">If you have successfully submitted a workflow using the provided sample data, you are ready to proceed with this quickstart.</span></span> 

## <a name="set-up-upload-your-fastq-files-to-azure-storage"></a><span data-ttu-id="4ac3d-107">Set up: Upload your FASTQ files to Azure storage</span><span class="sxs-lookup"><span data-stu-id="4ac3d-107">Set up: Upload your FASTQ files to Azure storage</span></span>
<span data-ttu-id="4ac3d-108">Let’s assume you have two files, *reads_1.fq.gz* and *reads_2.fq.gz*, and you have uploaded them to your storage account *myaccount* in Azure as **https://<span></span>myaccount.blob.core<span></span>.windows<span></span>.net<span></span>/inputs/reads_1<span></span>.fq<span></span>.gz<span></span>** and **https://<span></span>myaccount.blob.core.<span></span>windows<span></span>.net/<span></span>inputs/<span></span>reads_2.fq<span></span>.gz<span></span>**.</span><span class="sxs-lookup"><span data-stu-id="4ac3d-108">Let’s assume you have two files, *reads_1.fq.gz* and *reads_2.fq.gz*, and you have uploaded them to your storage account *myaccount* in Azure as **https://<span></span>myaccount.blob.core<span></span>.windows<span></span>.net<span></span>/inputs/reads_1<span></span>.fq<span></span>.gz<span></span>** and **https://<span></span>myaccount.blob.core.<span></span>windows<span></span>.net/<span></span>inputs/<span></span>reads_2.fq<span></span>.gz<span></span>**.</span></span> <span data-ttu-id="4ac3d-109">You have the API URL and your access key.</span><span class="sxs-lookup"><span data-stu-id="4ac3d-109">You have the API URL and your access key.</span></span> <span data-ttu-id="4ac3d-110">You want to have outputs in **https://<span></span>myaccount.blob.core<span></span>.windows<span></span>.net<span></span>/outputs<span></span>**.</span><span class="sxs-lookup"><span data-stu-id="4ac3d-110">You want to have outputs in **https://<span></span>myaccount.blob.core<span></span>.windows<span></span>.net<span></span>/outputs<span></span>**.</span></span>


## <a name="submit-your-job-to-the-msgen-client"></a><span data-ttu-id="4ac3d-111">Submit your job to the `msgen` client</span><span class="sxs-lookup"><span data-stu-id="4ac3d-111">Submit your job to the `msgen` client</span></span> 

<span data-ttu-id="4ac3d-112">Here is the minimal set of arguments that you will need to provide to the `msgen` client; line breaks are added for clarity:</span><span class="sxs-lookup"><span data-stu-id="4ac3d-112">Here is the minimal set of arguments that you will need to provide to the `msgen` client; line breaks are added for clarity:</span></span>

<span data-ttu-id="4ac3d-113">For Windows:</span><span class="sxs-lookup"><span data-stu-id="4ac3d-113">For Windows:</span></span>

```
msgen submit ^
  --api-url-base <Genomics API URL> ^
  --access-key <Genomics access key> ^
  --process-args R=b37m1 ^
  --input-storage-account-name myaccount ^
  --input-storage-account-key <storage access key to "myaccount"> ^
  --input-storage-account-container inputs ^
  --input-blob-name-1 reads_1.fq.gz ^
  --input-blob-name-2 reads_2.fq.gz ^
  --output-storage-account-name myaccount ^
  --output-storage-account-key <storage access key to "myaccount"> ^
  --output-storage-account-container outputs
```

<span data-ttu-id="4ac3d-114">For Unix:</span><span class="sxs-lookup"><span data-stu-id="4ac3d-114">For Unix:</span></span>

```
msgen submit \
  --api-url-base <Genomics API URL> \
  --access-key <Genomics access key> \
  --process-args R=b37m1 \
  --input-storage-account-name myaccount \
  --input-storage-account-key <storage access key to "myaccount"> \
  --input-storage-account-container inputs \
  --input-blob-name-1 reads_1.fq.gz \
  --input-blob-name-2 reads_2.fq.gz \
  --output-storage-account-name myaccount \
  --output-storage-account-key <storage access key to "myaccount"> \
  --output-storage-account-container outputs
```


<span data-ttu-id="4ac3d-115">If you prefer using a configuration file, here is what it would contain:</span><span class="sxs-lookup"><span data-stu-id="4ac3d-115">If you prefer using a configuration file, here is what it would contain:</span></span>

```
api_url_base:                     <Genomics API URL>
access_key:                       <Genomics access key>
process_args:                     R=b37m1
input_storage_account_name:       myaccount
input_storage_account_key:        <storage access key to "myaccount">
input_storage_account_container:  inputs
input_blob_name_1:                reads_1.fq.gz
input_blob_name_2:                reads_2.fq.gz
output_storage_account_name:      myaccount
output_storage_account_key:       <storage access key to "myaccount">
output_storage_account_container: outputs
```

<span data-ttu-id="4ac3d-116">Submit the `config.txt` file with this invocation: `msgen submit -f config.txt`</span><span class="sxs-lookup"><span data-stu-id="4ac3d-116">Submit the `config.txt` file with this invocation: `msgen submit -f config.txt`</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ac3d-117">Next steps</span><span class="sxs-lookup"><span data-stu-id="4ac3d-117">Next steps</span></span>
<span data-ttu-id="4ac3d-118">In this article, you uploaded a pair of FASTQ files into Azure Storage and submitted a workflow to the Microsoft Genomics service through the `msgen` python client.</span><span class="sxs-lookup"><span data-stu-id="4ac3d-118">In this article, you uploaded a pair of FASTQ files into Azure Storage and submitted a workflow to the Microsoft Genomics service through the `msgen` python client.</span></span> <span data-ttu-id="4ac3d-119">For additional information regarding workflow submission and other commands you can use with the Microsoft Genomics service, see our [FAQ](frequently-asked-questions-genomics.md).</span><span class="sxs-lookup"><span data-stu-id="4ac3d-119">For additional information regarding workflow submission and other commands you can use with the Microsoft Genomics service, see our [FAQ](frequently-asked-questions-genomics.md).</span></span> 
