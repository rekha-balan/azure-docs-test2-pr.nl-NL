---
title: Tutorial - Use the Azure Batch SDK for Python | Microsoft Docs
description: Learn the basic concepts of Azure Batch and build a simple solution using Python.
services: batch
documentationcenter: python
author: tamram
manager: timlt
editor: ''
ms.assetid: 42cae157-d43d-47f8-88f5-486ccfd334f4
ms.service: batch
ms.devlang: python
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 13e16b14803380a9c57f6a53ae56dc827343c241
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563751"
---
# <a name="get-started-with-the-batch-sdk-for-python"></a><span data-ttu-id="ab2b6-103">Get started with the Batch SDK for Python</span><span class="sxs-lookup"><span data-stu-id="ab2b6-103">Get started with the Batch SDK for Python</span></span>

> [!div class="op_single_selector"]
> * [.NET](batch-dotnet-get-started.md)
> * [Python](batch-python-tutorial.md)
>
>

<span data-ttu-id="ab2b6-106">Learn the basics of [Azure Batch][azure_batch] and the [Batch Python][py_azure_sdk] client as we discuss a small Batch application written in Python.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-106">Learn the basics of [Azure Batch][azure_batch] and the [Batch Python][py_azure_sdk] client as we discuss a small Batch application written in Python.</span></span> <span data-ttu-id="ab2b6-107">We look at how two sample scripts use the Batch service to process a parallel workload on Linux virtual machines in the cloud, and how they interact with [Azure Storage](../storage/storage-introduction.md) for file staging and retrieval.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-107">We look at how two sample scripts use the Batch service to process a parallel workload on Linux virtual machines in the cloud, and how they interact with [Azure Storage](../storage/storage-introduction.md) for file staging and retrieval.</span></span> <span data-ttu-id="ab2b6-108">You'll learn a common Batch application workflow and gain a base understanding of the major components of Batch such as jobs, tasks, pools, and compute nodes.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-108">You'll learn a common Batch application workflow and gain a base understanding of the major components of Batch such as jobs, tasks, pools, and compute nodes.</span></span>

<span data-ttu-id="ab2b6-109">![Batch solution workflow (basic)][11]</span><span class="sxs-lookup"><span data-stu-id="ab2b6-109">![Batch solution workflow (basic)][11]</span></span><br/>

## <a name="prerequisites"></a><span data-ttu-id="ab2b6-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ab2b6-110">Prerequisites</span></span>
<span data-ttu-id="ab2b6-111">This article assumes that you have a working knowledge of Python and familiarity with Linux.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-111">This article assumes that you have a working knowledge of Python and familiarity with Linux.</span></span> <span data-ttu-id="ab2b6-112">It also assumes that you're able to satisfy the account creation requirements that are specified below for Azure and the Batch and Storage services.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-112">It also assumes that you're able to satisfy the account creation requirements that are specified below for Azure and the Batch and Storage services.</span></span>

### <a name="accounts"></a><span data-ttu-id="ab2b6-113">Accounts</span><span class="sxs-lookup"><span data-stu-id="ab2b6-113">Accounts</span></span>
* <span data-ttu-id="ab2b6-114">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account][azure_free_account].</span><span class="sxs-lookup"><span data-stu-id="ab2b6-114">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account][azure_free_account].</span></span>
* <span data-ttu-id="ab2b6-115">**Batch account**: Once you have an Azure subscription, [create an Azure Batch account](batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ab2b6-115">**Batch account**: Once you have an Azure subscription, [create an Azure Batch account](batch-account-create-portal.md).</span></span>
* <span data-ttu-id="ab2b6-116">**Storage account**: See [Create a storage account](../storage/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="ab2b6-116">**Storage account**: See [Create a storage account](../storage/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/storage-create-storage-account.md).</span></span>

### <a name="code-sample"></a><span data-ttu-id="ab2b6-117">Code sample</span><span class="sxs-lookup"><span data-stu-id="ab2b6-117">Code sample</span></span>
<span data-ttu-id="ab2b6-118">The Python tutorial [code sample][github_article_samples] is one of the many Batch code samples found in the [azure-batch-samples][github_samples] repository on GitHub.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-118">The Python tutorial [code sample][github_article_samples] is one of the many Batch code samples found in the [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="ab2b6-119">You can download all the samples by clicking **Clone or download > Download ZIP** on the repository home page, or by clicking the [azure-batch-samples-master.zip][github_samples_zip] direct download link.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-119">You can download all the samples by clicking **Clone or download > Download ZIP** on the repository home page, or by clicking the [azure-batch-samples-master.zip][github_samples_zip] direct download link.</span></span> <span data-ttu-id="ab2b6-120">Once you've extracted the contents of the ZIP file, the two scripts for this tutorial are found in the `article_samples` directory:</span><span class="sxs-lookup"><span data-stu-id="ab2b6-120">Once you've extracted the contents of the ZIP file, the two scripts for this tutorial are found in the `article_samples` directory:</span></span>

`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_client.py`<br/>
`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_task.py`

### <a name="python-environment"></a><span data-ttu-id="ab2b6-121">Python environment</span><span class="sxs-lookup"><span data-stu-id="ab2b6-121">Python environment</span></span>
<span data-ttu-id="ab2b6-122">To run the *python_tutorial_client.py* sample script on your local workstation, you need a **Python interpreter** compatible with version **2.7** or **3.3+**.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-122">To run the *python_tutorial_client.py* sample script on your local workstation, you need a **Python interpreter** compatible with version **2.7** or **3.3+**.</span></span> <span data-ttu-id="ab2b6-123">The script has been tested on both Linux and Windows.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-123">The script has been tested on both Linux and Windows.</span></span>

### <a name="cryptography-dependencies"></a><span data-ttu-id="ab2b6-124">cryptography dependencies</span><span class="sxs-lookup"><span data-stu-id="ab2b6-124">cryptography dependencies</span></span>
<span data-ttu-id="ab2b6-125">You must install the dependencies for the [cryptography][crypto] library, required by the `azure-batch` and `azure-storage` Python packages.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-125">You must install the dependencies for the [cryptography][crypto] library, required by the `azure-batch` and `azure-storage` Python packages.</span></span> <span data-ttu-id="ab2b6-126">Perform one of the following operations appropriate for your platform, or refer to the [cryptography installation][crypto_install] details for more information:</span><span class="sxs-lookup"><span data-stu-id="ab2b6-126">Perform one of the following operations appropriate for your platform, or refer to the [cryptography installation][crypto_install] details for more information:</span></span>

* <span data-ttu-id="ab2b6-127">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="ab2b6-127">Ubuntu</span></span>

    `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython-dev python-dev`
* <span data-ttu-id="ab2b6-128">CentOS</span><span class="sxs-lookup"><span data-stu-id="ab2b6-128">CentOS</span></span>

    `yum update && yum install -y gcc openssl-dev libffi-devel python-devel`
* <span data-ttu-id="ab2b6-129">SLES/OpenSUSE</span><span class="sxs-lookup"><span data-stu-id="ab2b6-129">SLES/OpenSUSE</span></span>

    `zypper ref && zypper -n in libopenssl-dev libffi48-devel python-devel`
* <span data-ttu-id="ab2b6-130">Windows</span><span class="sxs-lookup"><span data-stu-id="ab2b6-130">Windows</span></span>

    `pip install cryptography`

> [!NOTE]
> If installing for Python 3.3+ on Linux, use the python3 equivalents for the Python dependencies. For example, on Ubuntu: `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython3-dev python3-dev`
>
>

### <a name="azure-packages"></a><span data-ttu-id="ab2b6-133">Azure packages</span><span class="sxs-lookup"><span data-stu-id="ab2b6-133">Azure packages</span></span>
<span data-ttu-id="ab2b6-134">Next, install the **Azure Batch** and **Azure Storage** Python packages.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-134">Next, install the **Azure Batch** and **Azure Storage** Python packages.</span></span> <span data-ttu-id="ab2b6-135">You can install both packages by using **pip** and the *requirements.txt* found here:</span><span class="sxs-lookup"><span data-stu-id="ab2b6-135">You can install both packages by using **pip** and the *requirements.txt* found here:</span></span>

`/azure-batch-samples/Python/Batch/requirements.txt`

<span data-ttu-id="ab2b6-136">Issue following **pip** command to install the Batch and Storage packages:</span><span class="sxs-lookup"><span data-stu-id="ab2b6-136">Issue following **pip** command to install the Batch and Storage packages:</span></span>

`pip install -r requirements.txt`

<span data-ttu-id="ab2b6-137">Or, you can install the [azure-batch][pypi_batch] and [azure-storage][pypi_storage] Python packages manually:</span><span class="sxs-lookup"><span data-stu-id="ab2b6-137">Or, you can install the [azure-batch][pypi_batch] and [azure-storage][pypi_storage] Python packages manually:</span></span>

`pip install azure-batch`<br/>
`pip install azure-storage`

> [!TIP]
> If you are using an unprivileged account, you may need to prefix your commands with `sudo`. For example, `sudo pip install -r requirements.txt`. For more information on installing Python packages, see [Installing Packages][pypi_install] on python.org.
>
>

## <a name="batch-python-tutorial-code-sample"></a><span data-ttu-id="ab2b6-141">Batch Python tutorial code sample</span><span class="sxs-lookup"><span data-stu-id="ab2b6-141">Batch Python tutorial code sample</span></span>
<span data-ttu-id="ab2b6-142">The Batch Python tutorial code sample consists of two Python scripts and a few data files.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-142">The Batch Python tutorial code sample consists of two Python scripts and a few data files.</span></span>

* <span data-ttu-id="ab2b6-143">**python_tutorial_client.py**: Interacts with the Batch and Storage services to execute a parallel workload on compute nodes (virtual machines).</span><span class="sxs-lookup"><span data-stu-id="ab2b6-143">**python_tutorial_client.py**: Interacts with the Batch and Storage services to execute a parallel workload on compute nodes (virtual machines).</span></span> <span data-ttu-id="ab2b6-144">The *python_tutorial_client.py* script runs on your local workstation.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-144">The *python_tutorial_client.py* script runs on your local workstation.</span></span>
* <span data-ttu-id="ab2b6-145">**python_tutorial_task.py**: The script that runs on compute nodes in Azure to perform the actual work.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-145">**python_tutorial_task.py**: The script that runs on compute nodes in Azure to perform the actual work.</span></span> <span data-ttu-id="ab2b6-146">In the sample, *python_tutorial_task.py* parses the text in a file downloaded from Azure Storage (the input file).</span><span class="sxs-lookup"><span data-stu-id="ab2b6-146">In the sample, *python_tutorial_task.py* parses the text in a file downloaded from Azure Storage (the input file).</span></span> <span data-ttu-id="ab2b6-147">Then it produces a text file (the output file) that contains a list of the top three words that appear in the input file.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-147">Then it produces a text file (the output file) that contains a list of the top three words that appear in the input file.</span></span> <span data-ttu-id="ab2b6-148">After it creates the output file, *python_tutorial_task.py* uploads the file to Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-148">After it creates the output file, *python_tutorial_task.py* uploads the file to Azure Storage.</span></span> <span data-ttu-id="ab2b6-149">This makes it available for download to the client script running on your workstation.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-149">This makes it available for download to the client script running on your workstation.</span></span> <span data-ttu-id="ab2b6-150">The *python_tutorial_task.py* script runs in parallel on multiple compute nodes in the Batch service.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-150">The *python_tutorial_task.py* script runs in parallel on multiple compute nodes in the Batch service.</span></span>
* <span data-ttu-id="ab2b6-151">**./data/taskdata\*.txt**: These three text files provide the input for the tasks that run on the compute nodes.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-151">**./data/taskdata\*.txt**: These three text files provide the input for the tasks that run on the compute nodes.</span></span>

<span data-ttu-id="ab2b6-152">The following diagram illustrates the primary operations that are performed by the client and task scripts.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-152">The following diagram illustrates the primary operations that are performed by the client and task scripts.</span></span> <span data-ttu-id="ab2b6-153">This basic workflow is typical of many compute solutions that are created with Batch.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-153">This basic workflow is typical of many compute solutions that are created with Batch.</span></span> <span data-ttu-id="ab2b6-154">While it does not demonstrate every feature available in the Batch service, nearly every Batch scenario includes portions of this workflow.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-154">While it does not demonstrate every feature available in the Batch service, nearly every Batch scenario includes portions of this workflow.</span></span>

<span data-ttu-id="ab2b6-155">![Batch example workflow][8]</span><span class="sxs-lookup"><span data-stu-id="ab2b6-155">![Batch example workflow][8]</span></span><br/>

[<span data-ttu-id="ab2b6-156">**Step 1.**</span><span class="sxs-lookup"><span data-stu-id="ab2b6-156">**Step 1.**</span></span>](#step-1-create-storage-containers) <span data-ttu-id="ab2b6-157">Create **containers** in Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-157">Create **containers** in Azure Blob Storage.</span></span><br/>
[<span data-ttu-id="ab2b6-158">**Step 2.**</span><span class="sxs-lookup"><span data-stu-id="ab2b6-158">**Step 2.**</span></span>](#step-2-upload-task-script-and-data-files) <span data-ttu-id="ab2b6-159">Upload task script and input files to containers.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-159">Upload task script and input files to containers.</span></span><br/>
[<span data-ttu-id="ab2b6-160">**Step 3.**</span><span class="sxs-lookup"><span data-stu-id="ab2b6-160">**Step 3.**</span></span>](#step-3-create-batch-pool) <span data-ttu-id="ab2b6-161">Create a Batch **pool**.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-161">Create a Batch **pool**.</span></span><br/>
  <span data-ttu-id="ab2b6-162">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span><span class="sxs-lookup"><span data-stu-id="ab2b6-162">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span></span> <span data-ttu-id="ab2b6-163">The pool **StartTask** downloads the task script (python_tutorial_task.py) to nodes as they join the pool.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-163">The pool **StartTask** downloads the task script (python_tutorial_task.py) to nodes as they join the pool.</span></span><br/>
[<span data-ttu-id="ab2b6-164">**Step 4.**</span><span class="sxs-lookup"><span data-stu-id="ab2b6-164">**Step 4.**</span></span>](#step-4-create-batch-job) <span data-ttu-id="ab2b6-165">Create a Batch **job**.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-165">Create a Batch **job**.</span></span><br/>
[<span data-ttu-id="ab2b6-166">**Step 5.**</span><span class="sxs-lookup"><span data-stu-id="ab2b6-166">**Step 5.**</span></span>](#step-5-add-tasks-to-job) <span data-ttu-id="ab2b6-167">Add **tasks** to the job.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-167">Add **tasks** to the job.</span></span><br/>
  <span data-ttu-id="ab2b6-168">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span><span class="sxs-lookup"><span data-stu-id="ab2b6-168">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span></span> <span data-ttu-id="ab2b6-169">The tasks are scheduled to execute on nodes.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-169">The tasks are scheduled to execute on nodes.</span></span><br/>
    <span data-ttu-id="ab2b6-170">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span><span class="sxs-lookup"><span data-stu-id="ab2b6-170">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span></span> <span data-ttu-id="ab2b6-171">Each task downloads its input data from Azure Storage, then begins execution.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-171">Each task downloads its input data from Azure Storage, then begins execution.</span></span><br/>
[<span data-ttu-id="ab2b6-172">**Step 6.**</span><span class="sxs-lookup"><span data-stu-id="ab2b6-172">**Step 6.**</span></span>](#step-6-monitor-tasks) <span data-ttu-id="ab2b6-173">Monitor tasks.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-173">Monitor tasks.</span></span><br/>
  <span data-ttu-id="ab2b6-174">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span><span class="sxs-lookup"><span data-stu-id="ab2b6-174">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span></span> <span data-ttu-id="ab2b6-175">As tasks are completed, they upload their output data to Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-175">As tasks are completed, they upload their output data to Azure Storage.</span></span><br/>
[<span data-ttu-id="ab2b6-176">**Step 7.**</span><span class="sxs-lookup"><span data-stu-id="ab2b6-176">**Step 7.**</span></span>](#step-7-download-task-output) <span data-ttu-id="ab2b6-177">Download task output from Storage.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-177">Download task output from Storage.</span></span>

<span data-ttu-id="ab2b6-178">As mentioned, not every Batch solution performs these exact steps, and may include many more, but this sample demonstrates common processes found in a Batch solution.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-178">As mentioned, not every Batch solution performs these exact steps, and may include many more, but this sample demonstrates common processes found in a Batch solution.</span></span>

## <a name="prepare-client-script"></a><span data-ttu-id="ab2b6-179">Prepare client script</span><span class="sxs-lookup"><span data-stu-id="ab2b6-179">Prepare client script</span></span>
<span data-ttu-id="ab2b6-180">Before you run the sample, add your Batch and Storage account credentials to *python_tutorial_client.py*.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-180">Before you run the sample, add your Batch and Storage account credentials to *python_tutorial_client.py*.</span></span> <span data-ttu-id="ab2b6-181">If you have not done so already, open the file in your favorite editor and update the following lines with your credentials.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-181">If you have not done so already, open the file in your favorite editor and update the following lines with your credentials.</span></span>

```python
# Update the Batch and Storage account credential strings below with the values
# unique to your accounts. These are used when constructing connection strings
# for the Batch and Storage client objects.

# Batch account credentials
batch_account_name = "";
batch_account_key  = "";
batch_account_url  = "";

# Storage account credentials
storage_account_name = "";
storage_account_key  = "";
```

<span data-ttu-id="ab2b6-182">You can find your Batch and Storage account credentials within the account blade of each service in the [Azure portal][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="ab2b6-182">You can find your Batch and Storage account credentials within the account blade of each service in the [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="ab2b6-183">![Batch credentials in the portal][9]
![Storage credentials in the portal][10]</span><span class="sxs-lookup"><span data-stu-id="ab2b6-183">![Batch credentials in the portal][9]
![Storage credentials in the portal][10]</span></span><br/>

<span data-ttu-id="ab2b6-184">In the following sections, we analyze the steps used by the scripts to process a workload in the Batch service.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-184">In the following sections, we analyze the steps used by the scripts to process a workload in the Batch service.</span></span> <span data-ttu-id="ab2b6-185">We encourage you to refer regularly to the scripts in your editor while you work your way through the rest of the article.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-185">We encourage you to refer regularly to the scripts in your editor while you work your way through the rest of the article.</span></span>

<span data-ttu-id="ab2b6-186">Navigate to the following line in **python_tutorial_client.py** to start with Step 1:</span><span class="sxs-lookup"><span data-stu-id="ab2b6-186">Navigate to the following line in **python_tutorial_client.py** to start with Step 1:</span></span>

```python
if __name__ == '__main__':
```

## <a name="step-1-create-storage-containers"></a><span data-ttu-id="ab2b6-187">Step 1: Create Storage containers</span><span class="sxs-lookup"><span data-stu-id="ab2b6-187">Step 1: Create Storage containers</span></span>
<span data-ttu-id="ab2b6-188">![Create containers in Azure Storage][1]</span><span class="sxs-lookup"><span data-stu-id="ab2b6-188">![Create containers in Azure Storage][1]</span></span>
<br/>

<span data-ttu-id="ab2b6-189">Batch includes built-in support for interacting with Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-189">Batch includes built-in support for interacting with Azure Storage.</span></span> <span data-ttu-id="ab2b6-190">Containers in your Storage account will provide the files needed by the tasks that run in your Batch account.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-190">Containers in your Storage account will provide the files needed by the tasks that run in your Batch account.</span></span> <span data-ttu-id="ab2b6-191">The containers also provide a place to store the output data that the tasks produce.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-191">The containers also provide a place to store the output data that the tasks produce.</span></span> <span data-ttu-id="ab2b6-192">The first thing the *python_tutorial_client.py* script does is create three containers in [Azure Blob Storage](../storage/storage-introduction.md#blob-storage):</span><span class="sxs-lookup"><span data-stu-id="ab2b6-192">The first thing the *python_tutorial_client.py* script does is create three containers in [Azure Blob Storage](../storage/storage-introduction.md#blob-storage):</span></span>

* <span data-ttu-id="ab2b6-193">**application**: This container will store the Python script run by the tasks, *python_tutorial_task.py*.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-193">**application**: This container will store the Python script run by the tasks, *python_tutorial_task.py*.</span></span>
* <span data-ttu-id="ab2b6-194">**input**: Tasks will download the data files to process from the *input* container.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-194">**input**: Tasks will download the data files to process from the *input* container.</span></span>
* <span data-ttu-id="ab2b6-195">**output**: When tasks complete input file processing, they will upload the results to the *output* container.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-195">**output**: When tasks complete input file processing, they will upload the results to the *output* container.</span></span>

<span data-ttu-id="ab2b6-196">In order to interact with a Storage account and create containers, we use the [azure-storage][pypi_storage] package to create a [BlockBlobService][py_blockblobservice] object--the "blob client."</span><span class="sxs-lookup"><span data-stu-id="ab2b6-196">In order to interact with a Storage account and create containers, we use the [azure-storage][pypi_storage] package to create a [BlockBlobService][py_blockblobservice] object--the "blob client."</span></span> <span data-ttu-id="ab2b6-197">We then create three containers in the Storage account using the blob client.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-197">We then create three containers in the Storage account using the blob client.</span></span>

```python
 # Create the blob client, for use in obtaining references to
 # blob storage containers and uploading files to containers.
 blob_client = azureblob.BlockBlobService(
     account_name=_STORAGE_ACCOUNT_NAME,
     account_key=_STORAGE_ACCOUNT_KEY)

 # Use the blob client to create the containers in Azure Storage if they
 # don't yet exist.
 app_container_name = 'application'
 input_container_name = 'input'
 output_container_name = 'output'
 blob_client.create_container(app_container_name, fail_on_exist=False)
 blob_client.create_container(input_container_name, fail_on_exist=False)
 blob_client.create_container(output_container_name, fail_on_exist=False)
```

<span data-ttu-id="ab2b6-198">Once the containers have been created, the application can now upload the files that will be used by the tasks.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-198">Once the containers have been created, the application can now upload the files that will be used by the tasks.</span></span>

> [!TIP]
> [How to use Azure Blob storage from Python](../storage/storage-python-how-to-use-blob-storage.md) provides a good overview of working with Azure Storage containers and blobs. It should be near the top of your reading list as you start working with Batch.
>
>

## <a name="step-2-upload-task-script-and-data-files"></a><span data-ttu-id="ab2b6-201">Step 2: Upload task script and data files</span><span class="sxs-lookup"><span data-stu-id="ab2b6-201">Step 2: Upload task script and data files</span></span>
<span data-ttu-id="ab2b6-202">![Upload task application and input (data) files to containers][2]</span><span class="sxs-lookup"><span data-stu-id="ab2b6-202">![Upload task application and input (data) files to containers][2]</span></span>
<br/>

<span data-ttu-id="ab2b6-203">In the file upload operation, *python_tutorial_client.py* first defines collections of **application** and **input** file paths as they exist on the local machine.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-203">In the file upload operation, *python_tutorial_client.py* first defines collections of **application** and **input** file paths as they exist on the local machine.</span></span> <span data-ttu-id="ab2b6-204">Then it uploads these files to the containers that you created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-204">Then it uploads these files to the containers that you created in the previous step.</span></span>

```python
 # Paths to the task script. This script will be executed by the tasks that
 # run on the compute nodes.
 application_file_paths = [os.path.realpath('python_tutorial_task.py')]

 # The collection of data files that are to be processed by the tasks.
 input_file_paths = [os.path.realpath('./data/taskdata1.txt'),
                     os.path.realpath('./data/taskdata2.txt'),
                     os.path.realpath('./data/taskdata3.txt')]

 # Upload the application script to Azure Storage. This is the script that
 # will process the data files, and is executed by each of the tasks on the
 # compute nodes.
 application_files = [
     upload_file_to_container(blob_client, app_container_name, file_path)
     for file_path in application_file_paths]

 # Upload the data files. This is the data that will be processed by each of
 # the tasks executed on the compute nodes in the pool.
 input_files = [
     upload_file_to_container(blob_client, input_container_name, file_path)
     for file_path in input_file_paths]
```

<span data-ttu-id="ab2b6-205">Using list comprehension, the `upload_file_to_container` function is called for each file in the collections, and two [ResourceFile][py_resource_file] collections are populated.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-205">Using list comprehension, the `upload_file_to_container` function is called for each file in the collections, and two [ResourceFile][py_resource_file] collections are populated.</span></span> <span data-ttu-id="ab2b6-206">The `upload_file_to_container` function appears below:</span><span class="sxs-lookup"><span data-stu-id="ab2b6-206">The `upload_file_to_container` function appears below:</span></span>

```python
def upload_file_to_container(block_blob_client, container_name, file_path):
    """
    Uploads a local file to an Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param str container_name: The name of the Azure Blob storage container.
    :param str file_path: The local path to the file.
    :rtype: `azure.batch.models.ResourceFile`
    :return: A ResourceFile initialized with a SAS URL appropriate for Batch
    tasks.
    """
    blob_name = os.path.basename(file_path)

    print('Uploading file {} to container [{}]...'.format(file_path,
                                                          container_name))

    block_blob_client.create_blob_from_path(container_name,
                                            blob_name,
                                            file_path)

    sas_token = block_blob_client.generate_blob_shared_access_signature(
        container_name,
        blob_name,
        permission=azureblob.BlobPermissions.READ,
        expiry=datetime.datetime.utcnow() + datetime.timedelta(hours=2))

    sas_url = block_blob_client.make_blob_url(container_name,
                                              blob_name,
                                              sas_token=sas_token)

    return batchmodels.ResourceFile(file_path=blob_name,
                                    blob_source=sas_url)
```

### <a name="resourcefiles"></a><span data-ttu-id="ab2b6-207">ResourceFiles</span><span class="sxs-lookup"><span data-stu-id="ab2b6-207">ResourceFiles</span></span>
<span data-ttu-id="ab2b6-208">A [ResourceFile][py_resource_file] provides tasks in Batch with the URL to a file in Azure Storage that is downloaded to a compute node before that task is run.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-208">A [ResourceFile][py_resource_file] provides tasks in Batch with the URL to a file in Azure Storage that is downloaded to a compute node before that task is run.</span></span> <span data-ttu-id="ab2b6-209">The [ResourceFile][py_resource_file].**blob_source** property specifies the full URL of the file as it exists in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-209">The [ResourceFile][py_resource_file].**blob_source** property specifies the full URL of the file as it exists in Azure Storage.</span></span> <span data-ttu-id="ab2b6-210">The URL may also include a shared access signature (SAS) that provides secure access to the file.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-210">The URL may also include a shared access signature (SAS) that provides secure access to the file.</span></span> <span data-ttu-id="ab2b6-211">Most task types in Batch include a *ResourceFiles* property, including:</span><span class="sxs-lookup"><span data-stu-id="ab2b6-211">Most task types in Batch include a *ResourceFiles* property, including:</span></span>

* <span data-ttu-id="ab2b6-212">[CloudTask][py_task]</span><span class="sxs-lookup"><span data-stu-id="ab2b6-212">[CloudTask][py_task]</span></span>
* <span data-ttu-id="ab2b6-213">[StartTask][py_starttask]</span><span class="sxs-lookup"><span data-stu-id="ab2b6-213">[StartTask][py_starttask]</span></span>
* <span data-ttu-id="ab2b6-214">[JobPreparationTask][py_jobpreptask]</span><span class="sxs-lookup"><span data-stu-id="ab2b6-214">[JobPreparationTask][py_jobpreptask]</span></span>
* <span data-ttu-id="ab2b6-215">[JobReleaseTask][py_jobreltask]</span><span class="sxs-lookup"><span data-stu-id="ab2b6-215">[JobReleaseTask][py_jobreltask]</span></span>

<span data-ttu-id="ab2b6-216">This sample does not use the JobPreparationTask or JobReleaseTask task types, but you can read more about them in [Run job preparation and completion tasks on Azure Batch compute nodes](batch-job-prep-release.md).</span><span class="sxs-lookup"><span data-stu-id="ab2b6-216">This sample does not use the JobPreparationTask or JobReleaseTask task types, but you can read more about them in [Run job preparation and completion tasks on Azure Batch compute nodes](batch-job-prep-release.md).</span></span>

### <a name="shared-access-signature-sas"></a><span data-ttu-id="ab2b6-217">Shared access signature (SAS)</span><span class="sxs-lookup"><span data-stu-id="ab2b6-217">Shared access signature (SAS)</span></span>
<span data-ttu-id="ab2b6-218">Shared access signatures are strings that provide secure access to containers and blobs in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-218">Shared access signatures are strings that provide secure access to containers and blobs in Azure Storage.</span></span> <span data-ttu-id="ab2b6-219">The *python_tutorial_client.py* script uses both blob and container shared access signatures, and demonstrates how to obtain these shared access signature strings from the Storage service.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-219">The *python_tutorial_client.py* script uses both blob and container shared access signatures, and demonstrates how to obtain these shared access signature strings from the Storage service.</span></span>

* <span data-ttu-id="ab2b6-220">**Blob shared access signatures**: The pool's StartTask uses blob shared access signatures when it downloads the task script and input data files from Storage (see [Step #3](#step-3-create-batch-pool) below).</span><span class="sxs-lookup"><span data-stu-id="ab2b6-220">**Blob shared access signatures**: The pool's StartTask uses blob shared access signatures when it downloads the task script and input data files from Storage (see [Step #3](#step-3-create-batch-pool) below).</span></span> <span data-ttu-id="ab2b6-221">The `upload_file_to_container` function in *python_tutorial_client.py* contains the code that obtains each blob's shared access signature.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-221">The `upload_file_to_container` function in *python_tutorial_client.py* contains the code that obtains each blob's shared access signature.</span></span> <span data-ttu-id="ab2b6-222">It does so by calling [BlockBlobService.make_blob_url][py_make_blob_url] in the Storage module.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-222">It does so by calling [BlockBlobService.make_blob_url][py_make_blob_url] in the Storage module.</span></span>
* <span data-ttu-id="ab2b6-223">**Container shared access signature**: As each task finishes its work on the compute node, it uploads its output file to the *output* container in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-223">**Container shared access signature**: As each task finishes its work on the compute node, it uploads its output file to the *output* container in Azure Storage.</span></span> <span data-ttu-id="ab2b6-224">To do so, *python_tutorial_task.py* uses a container shared access signature that provides write access to the container.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-224">To do so, *python_tutorial_task.py* uses a container shared access signature that provides write access to the container.</span></span> <span data-ttu-id="ab2b6-225">The `get_container_sas_token` function in *python_tutorial_client.py* obtains the container's shared access signature, which is then passed as a command-line argument to the tasks.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-225">The `get_container_sas_token` function in *python_tutorial_client.py* obtains the container's shared access signature, which is then passed as a command-line argument to the tasks.</span></span> <span data-ttu-id="ab2b6-226">Step #5, [Add tasks to a job](#step-5-add-tasks-to-job), discusses the usage of the container SAS.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-226">Step #5, [Add tasks to a job](#step-5-add-tasks-to-job), discusses the usage of the container SAS.</span></span>

> [!TIP]
> Check out the two-part series on shared access signatures, [Part 1: Understanding the SAS model](../storage/storage-dotnet-shared-access-signature-part-1.md) and [Part 2: Create and use a SAS with the Blob service](../storage/storage-dotnet-shared-access-signature-part-2.md), to learn more about providing secure access to data in your Storage account.
>
>

## <a name="step-3-create-batch-pool"></a><span data-ttu-id="ab2b6-228">Step 3: Create Batch pool</span><span class="sxs-lookup"><span data-stu-id="ab2b6-228">Step 3: Create Batch pool</span></span>
<span data-ttu-id="ab2b6-229">![Create a Batch pool][3]</span><span class="sxs-lookup"><span data-stu-id="ab2b6-229">![Create a Batch pool][3]</span></span>
<br/>

<span data-ttu-id="ab2b6-230">A Batch **pool** is a collection of compute nodes (virtual machines) on which Batch executes a job's tasks.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-230">A Batch **pool** is a collection of compute nodes (virtual machines) on which Batch executes a job's tasks.</span></span>

<span data-ttu-id="ab2b6-231">After it uploads the task script and data files to the Storage account, *python_tutorial_client.py* starts its interaction with the Batch service by using the Batch Python module.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-231">After it uploads the task script and data files to the Storage account, *python_tutorial_client.py* starts its interaction with the Batch service by using the Batch Python module.</span></span> <span data-ttu-id="ab2b6-232">To do so, a [BatchServiceClient][py_batchserviceclient] is created:</span><span class="sxs-lookup"><span data-stu-id="ab2b6-232">To do so, a [BatchServiceClient][py_batchserviceclient] is created:</span></span>

```python
 # Create a Batch service client. We'll now be interacting with the Batch
 # service in addition to Storage.
 credentials = batchauth.SharedKeyCredentials(_BATCH_ACCOUNT_NAME,
                                              _BATCH_ACCOUNT_KEY)

 batch_client = batch.BatchServiceClient(
     credentials,
     base_url=_BATCH_ACCOUNT_URL)
```

<span data-ttu-id="ab2b6-233">Next, a pool of compute nodes is created in the Batch account with a call to `create_pool`.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-233">Next, a pool of compute nodes is created in the Batch account with a call to `create_pool`.</span></span>

```python
def create_pool(batch_service_client, pool_id,
                resource_files, publisher, offer, sku):
    """
    Creates a pool of compute nodes with the specified OS settings.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str pool_id: An ID for the new pool.
    :param list resource_files: A collection of resource files for the pool's
    start task.
    :param str publisher: Marketplace image publisher
    :param str offer: Marketplace image offer
    :param str sku: Marketplace image sku
    """
    print('Creating pool [{}]...'.format(pool_id))

    # Create a new pool of Linux compute nodes using an Azure Virtual Machines
    # Marketplace image. For more information about creating pools of Linux
    # nodes, see:
    # https://azure.microsoft.com/documentation/articles/batch-linux-nodes/

    # Specify the commands for the pool's start task. The start task is run
    # on each node as it joins the pool, and when it's rebooted or re-imaged.
    # We use the start task to prep the node for running our task script.
    task_commands = [
        # Copy the python_tutorial_task.py script to the "shared" directory
        # that all tasks that run on the node have access to.
        'cp -r $AZ_BATCH_TASK_WORKING_DIR/* $AZ_BATCH_NODE_SHARED_DIR',
        # Install pip and the dependencies for cryptography
        'apt-get update',
        'apt-get -y install python-pip',
        'apt-get -y install build-essential libssl-dev libffi-dev python-dev',
        # Install the azure-storage module so that the task script can access
        # Azure Blob storage
        'pip install azure-storage']

    # Get the node agent SKU and image reference for the virtual machine
    # configuration.
    # For more information about the virtual machine configuration, see:
    # https://azure.microsoft.com/documentation/articles/batch-linux-nodes/
    sku_to_use, image_ref_to_use = \
        common.helpers.select_latest_verified_vm_image_with_node_agent_sku(
            batch_service_client, publisher, offer, sku)

    new_pool = batch.models.PoolAddParameter(
        id=pool_id,
        virtual_machine_configuration=batchmodels.VirtualMachineConfiguration(
            image_reference=image_ref_to_use,
            node_agent_sku_id=sku_to_use),
        vm_size=_POOL_VM_SIZE,
        target_dedicated=_POOL_NODE_COUNT,
        start_task=batch.models.StartTask(
            command_line=
            common.helpers.wrap_commands_in_shell('linux', task_commands),
            run_elevated=True,
            wait_for_success=True,
            resource_files=resource_files),
        )

    try:
        batch_service_client.pool.add(new_pool)
    except batchmodels.batch_error.BatchErrorException as err:
        print_batch_exception(err)
        raise
```

<span data-ttu-id="ab2b6-234">When you create a pool, you define a [PoolAddParameter][py_pooladdparam] that specifies several properties for the pool:</span><span class="sxs-lookup"><span data-stu-id="ab2b6-234">When you create a pool, you define a [PoolAddParameter][py_pooladdparam] that specifies several properties for the pool:</span></span>

* <span data-ttu-id="ab2b6-235">**ID** of the pool (*id* - required)</span><span class="sxs-lookup"><span data-stu-id="ab2b6-235">**ID** of the pool (*id* - required)</span></span><p/><span data-ttu-id="ab2b6-236">As with most entities in Batch, your new pool must have a unique ID within your Batch account.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-236">As with most entities in Batch, your new pool must have a unique ID within your Batch account.</span></span> <span data-ttu-id="ab2b6-237">Your code refers to this pool using its ID, and it's how you identify the pool in the Azure [portal][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="ab2b6-237">Your code refers to this pool using its ID, and it's how you identify the pool in the Azure [portal][azure_portal].</span></span>
* <span data-ttu-id="ab2b6-238">**Number of compute nodes** (*target_dedicated* - required)</span><span class="sxs-lookup"><span data-stu-id="ab2b6-238">**Number of compute nodes** (*target_dedicated* - required)</span></span><p/><span data-ttu-id="ab2b6-239">This property specifies how many VMs should be deployed in the pool.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-239">This property specifies how many VMs should be deployed in the pool.</span></span> <span data-ttu-id="ab2b6-240">It is important to note that all Batch accounts have a default **quota** that limits the number of **cores** (and thus, compute nodes) in a Batch account.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-240">It is important to note that all Batch accounts have a default **quota** that limits the number of **cores** (and thus, compute nodes) in a Batch account.</span></span> <span data-ttu-id="ab2b6-241">You can find the default quotas and instructions on how to [increase a quota](batch-quota-limit.md#increase-a-quota) (such as the maximum number of cores in your Batch account) in [Quotas and limits for the Azure Batch service](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="ab2b6-241">You can find the default quotas and instructions on how to [increase a quota](batch-quota-limit.md#increase-a-quota) (such as the maximum number of cores in your Batch account) in [Quotas and limits for the Azure Batch service](batch-quota-limit.md).</span></span> <span data-ttu-id="ab2b6-242">If you find yourself asking "Why won't my pool reach more than X nodes?"</span><span class="sxs-lookup"><span data-stu-id="ab2b6-242">If you find yourself asking "Why won't my pool reach more than X nodes?"</span></span> <span data-ttu-id="ab2b6-243">this core quota may be the cause.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-243">this core quota may be the cause.</span></span>
* <span data-ttu-id="ab2b6-244">**Operating system** for nodes (*virtual_machine_configuration* **or** *cloud_service_configuration* - required)</span><span class="sxs-lookup"><span data-stu-id="ab2b6-244">**Operating system** for nodes (*virtual_machine_configuration* **or** *cloud_service_configuration* - required)</span></span><p/><span data-ttu-id="ab2b6-245">In *python_tutorial_client.py*, we create a pool of Linux nodes using a [VirtualMachineConfiguration][py_vm_config].</span><span class="sxs-lookup"><span data-stu-id="ab2b6-245">In *python_tutorial_client.py*, we create a pool of Linux nodes using a [VirtualMachineConfiguration][py_vm_config].</span></span> <span data-ttu-id="ab2b6-246">The `select_latest_verified_vm_image_with_node_agent_sku` function in `common.helpers` simplifies working with [Azure Virtual Machines Marketplace][vm_marketplace] images.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-246">The `select_latest_verified_vm_image_with_node_agent_sku` function in `common.helpers` simplifies working with [Azure Virtual Machines Marketplace][vm_marketplace] images.</span></span> <span data-ttu-id="ab2b6-247">See [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) for more information about using Marketplace images.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-247">See [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) for more information about using Marketplace images.</span></span>
* <span data-ttu-id="ab2b6-248">**Size of compute nodes** (*vm_size* - required)</span><span class="sxs-lookup"><span data-stu-id="ab2b6-248">**Size of compute nodes** (*vm_size* - required)</span></span><p/><span data-ttu-id="ab2b6-249">Since we're specifying Linux nodes for our [VirtualMachineConfiguration][py_vm_config], we specify a VM size (`STANDARD_A1` in this sample) from [Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ab2b6-249">Since we're specifying Linux nodes for our [VirtualMachineConfiguration][py_vm_config], we specify a VM size (`STANDARD_A1` in this sample) from [Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="ab2b6-250">Again, see [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) for more information.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-250">Again, see [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) for more information.</span></span>
* <span data-ttu-id="ab2b6-251">**Start task** (*start_task* - not required)</span><span class="sxs-lookup"><span data-stu-id="ab2b6-251">**Start task** (*start_task* - not required)</span></span><p/><span data-ttu-id="ab2b6-252">Along with the above physical node properties, you may also specify a [StartTask][py_starttask] for the pool (it is not required).</span><span class="sxs-lookup"><span data-stu-id="ab2b6-252">Along with the above physical node properties, you may also specify a [StartTask][py_starttask] for the pool (it is not required).</span></span> <span data-ttu-id="ab2b6-253">The StartTask executes on each node as that node joins the pool, and each time a node is restarted.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-253">The StartTask executes on each node as that node joins the pool, and each time a node is restarted.</span></span> <span data-ttu-id="ab2b6-254">The StartTask is especially useful for preparing compute nodes for the execution of tasks, such as installing the applications that your tasks run.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-254">The StartTask is especially useful for preparing compute nodes for the execution of tasks, such as installing the applications that your tasks run.</span></span><p/><span data-ttu-id="ab2b6-255">In this sample application, the StartTask copies the files that it downloads from Storage (which are specified by using the StartTask's **resource_files** property) from the StartTask *working directory* to the *shared* directory that all tasks running on the node can access.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-255">In this sample application, the StartTask copies the files that it downloads from Storage (which are specified by using the StartTask's **resource_files** property) from the StartTask *working directory* to the *shared* directory that all tasks running on the node can access.</span></span> <span data-ttu-id="ab2b6-256">Essentially, this copies `python_tutorial_task.py` to the shared directory on each node as the node joins the pool, so that any tasks that run on the node can access it.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-256">Essentially, this copies `python_tutorial_task.py` to the shared directory on each node as the node joins the pool, so that any tasks that run on the node can access it.</span></span>

<span data-ttu-id="ab2b6-257">You may notice the call to the `wrap_commands_in_shell` helper function.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-257">You may notice the call to the `wrap_commands_in_shell` helper function.</span></span> <span data-ttu-id="ab2b6-258">This function takes a collection of separate commands and creates a single command line appropriate for a task's command-line property.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-258">This function takes a collection of separate commands and creates a single command line appropriate for a task's command-line property.</span></span>

<span data-ttu-id="ab2b6-259">Also notable in the code snippet above is the use of two environment variables in the **command_line** property of the StartTask: `AZ_BATCH_TASK_WORKING_DIR` and `AZ_BATCH_NODE_SHARED_DIR`.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-259">Also notable in the code snippet above is the use of two environment variables in the **command_line** property of the StartTask: `AZ_BATCH_TASK_WORKING_DIR` and `AZ_BATCH_NODE_SHARED_DIR`.</span></span> <span data-ttu-id="ab2b6-260">Each compute node within a Batch pool is automatically configured with several environment variables that are specific to Batch.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-260">Each compute node within a Batch pool is automatically configured with several environment variables that are specific to Batch.</span></span> <span data-ttu-id="ab2b6-261">Any process that is executed by a task has access to these environment variables.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-261">Any process that is executed by a task has access to these environment variables.</span></span>

> [!TIP]
> To find out more about the environment variables that are available on compute nodes in a Batch pool, as well as information on task working directories, see **Environment settings for tasks** and **Files and directories** in the [overview of Azure Batch features](batch-api-basics.md).
>
>

## <a name="step-4-create-batch-job"></a><span data-ttu-id="ab2b6-263">Step 4: Create Batch job</span><span class="sxs-lookup"><span data-stu-id="ab2b6-263">Step 4: Create Batch job</span></span>
<span data-ttu-id="ab2b6-264">![Create Batch job][4]</span><span class="sxs-lookup"><span data-stu-id="ab2b6-264">![Create Batch job][4]</span></span><br/>

<span data-ttu-id="ab2b6-265">A Batch **job** is a collection of tasks, and is associated with a pool of compute nodes.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-265">A Batch **job** is a collection of tasks, and is associated with a pool of compute nodes.</span></span> <span data-ttu-id="ab2b6-266">The tasks in a job execute on the associated pool's compute nodes.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-266">The tasks in a job execute on the associated pool's compute nodes.</span></span>

<span data-ttu-id="ab2b6-267">You can use a job not only for organizing and tracking tasks in related workloads, but also for imposing certain constraints--such as the maximum runtime for the job (and by extension, its tasks) and job priority in relation to other jobs in the Batch account.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-267">You can use a job not only for organizing and tracking tasks in related workloads, but also for imposing certain constraints--such as the maximum runtime for the job (and by extension, its tasks) and job priority in relation to other jobs in the Batch account.</span></span> <span data-ttu-id="ab2b6-268">In this example, however, the job is associated only with the pool that was created in step #3.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-268">In this example, however, the job is associated only with the pool that was created in step #3.</span></span> <span data-ttu-id="ab2b6-269">No additional properties are configured.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-269">No additional properties are configured.</span></span>

<span data-ttu-id="ab2b6-270">All Batch jobs are associated with a specific pool.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-270">All Batch jobs are associated with a specific pool.</span></span> <span data-ttu-id="ab2b6-271">This association indicates which nodes the job's tasks execute on.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-271">This association indicates which nodes the job's tasks execute on.</span></span> <span data-ttu-id="ab2b6-272">You specify the pool by using the [PoolInformation][py_poolinfo] property, as shown in the code snippet below.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-272">You specify the pool by using the [PoolInformation][py_poolinfo] property, as shown in the code snippet below.</span></span>

```python
def create_job(batch_service_client, job_id, pool_id):
    """
    Creates a job with the specified ID, associated with the specified pool.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: The ID for the job.
    :param str pool_id: The ID for the pool.
    """
    print('Creating job [{}]...'.format(job_id))

    job = batch.models.JobAddParameter(
        job_id,
        batch.models.PoolInformation(pool_id=pool_id))

    try:
        batch_service_client.job.add(job)
    except batchmodels.batch_error.BatchErrorException as err:
        print_batch_exception(err)
        raise
```

<span data-ttu-id="ab2b6-273">Now that a job has been created, tasks are added to perform the work.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-273">Now that a job has been created, tasks are added to perform the work.</span></span>

## <a name="step-5-add-tasks-to-job"></a><span data-ttu-id="ab2b6-274">Step 5: Add tasks to job</span><span class="sxs-lookup"><span data-stu-id="ab2b6-274">Step 5: Add tasks to job</span></span>
<span data-ttu-id="ab2b6-275">![Add tasks to job][5]</span><span class="sxs-lookup"><span data-stu-id="ab2b6-275">![Add tasks to job][5]</span></span><br/>
<span data-ttu-id="ab2b6-276">*(1) Tasks are added to the job, (2) the tasks are scheduled to run on nodes, and (3) the tasks download the data files to process*</span><span class="sxs-lookup"><span data-stu-id="ab2b6-276">*(1) Tasks are added to the job, (2) the tasks are scheduled to run on nodes, and (3) the tasks download the data files to process*</span></span>

<span data-ttu-id="ab2b6-277">Batch **tasks** are the individual units of work that execute on the compute nodes.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-277">Batch **tasks** are the individual units of work that execute on the compute nodes.</span></span> <span data-ttu-id="ab2b6-278">A task has a command line and runs the scripts or executables that you specify in that command line.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-278">A task has a command line and runs the scripts or executables that you specify in that command line.</span></span>

<span data-ttu-id="ab2b6-279">To actually perform work, tasks must be added to a job.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-279">To actually perform work, tasks must be added to a job.</span></span> <span data-ttu-id="ab2b6-280">Each [CloudTask][py_task] is configured with a command-line property and [ResourceFiles][py_resource_file] (as with the pool's StartTask) that the task downloads to the node before its command line is automatically executed.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-280">Each [CloudTask][py_task] is configured with a command-line property and [ResourceFiles][py_resource_file] (as with the pool's StartTask) that the task downloads to the node before its command line is automatically executed.</span></span> <span data-ttu-id="ab2b6-281">In the sample, each task processes only one file.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-281">In the sample, each task processes only one file.</span></span> <span data-ttu-id="ab2b6-282">Thus, its ResourceFiles collection contains a single element.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-282">Thus, its ResourceFiles collection contains a single element.</span></span>

```python
def add_tasks(batch_service_client, job_id, input_files,
              output_container_name, output_container_sas_token):
    """
    Adds a task for each input file in the collection to the specified job.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: The ID of the job to which to add the tasks.
    :param list input_files: A collection of input files. One task will be
     created for each input file.
    :param output_container_name: The ID of an Azure Blob storage container to
    which the tasks will upload their results.
    :param output_container_sas_token: A SAS token granting write access to
    the specified Azure Blob storage container.
    """

    print('Adding {} tasks to job [{}]...'.format(len(input_files), job_id))

    tasks = list()

    for input_file in input_files:

        command = ['python $AZ_BATCH_NODE_SHARED_DIR/python_tutorial_task.py '
                   '--filepath {} --numwords {} --storageaccount {} '
                   '--storagecontainer {} --sastoken "{}"'.format(
                    input_file.file_path,
                    '3',
                    _STORAGE_ACCOUNT_NAME,
                    output_container_name,
                    output_container_sas_token)]

        tasks.append(batch.models.TaskAddParameter(
                'topNtask{}'.format(input_files.index(input_file)),
                wrap_commands_in_shell('linux', command),
                resource_files=[input_file]
                )
        )

    batch_service_client.task.add_collection(job_id, tasks)
```

> [!IMPORTANT]
> When they access environment variables such as `$AZ_BATCH_NODE_SHARED_DIR` or execute an application not found in the node's `PATH`, task command lines must invoke the shell explicitly, such as with `/bin/sh -c MyTaskApplication $MY_ENV_VAR`. This requirement is unnecessary if your tasks execute an application in the node's `PATH` and do not reference any environment variables.
>
>

<span data-ttu-id="ab2b6-285">Within the `for` loop in the code snippet above, you can see that the command line for the task is constructed with five command-line arguments that are passed to *python_tutorial_task.py*:</span><span class="sxs-lookup"><span data-stu-id="ab2b6-285">Within the `for` loop in the code snippet above, you can see that the command line for the task is constructed with five command-line arguments that are passed to *python_tutorial_task.py*:</span></span>

1. <span data-ttu-id="ab2b6-286">**filepath**: This is the local path to the file as it exists on the node.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-286">**filepath**: This is the local path to the file as it exists on the node.</span></span> <span data-ttu-id="ab2b6-287">When the ResourceFile object in `upload_file_to_container` was created in Step 2 above, the file name was used for this property (the `file_path` parameter in the ResourceFile constructor).</span><span class="sxs-lookup"><span data-stu-id="ab2b6-287">When the ResourceFile object in `upload_file_to_container` was created in Step 2 above, the file name was used for this property (the `file_path` parameter in the ResourceFile constructor).</span></span> <span data-ttu-id="ab2b6-288">This indicates that the file can be found in the same directory on the node as *python_tutorial_task.py*.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-288">This indicates that the file can be found in the same directory on the node as *python_tutorial_task.py*.</span></span>
2. <span data-ttu-id="ab2b6-289">**numwords**: The top *N* words should be written to the output file.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-289">**numwords**: The top *N* words should be written to the output file.</span></span>
3. <span data-ttu-id="ab2b6-290">**storageaccount**: The name of the Storage account that owns the container to which the task output should be uploaded.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-290">**storageaccount**: The name of the Storage account that owns the container to which the task output should be uploaded.</span></span>
4. <span data-ttu-id="ab2b6-291">**storagecontainer**: The name of the Storage container to which the output files should be uploaded.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-291">**storagecontainer**: The name of the Storage container to which the output files should be uploaded.</span></span>
5. <span data-ttu-id="ab2b6-292">**sastoken**: The shared access signature (SAS) that provides write access to the **output** container in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-292">**sastoken**: The shared access signature (SAS) that provides write access to the **output** container in Azure Storage.</span></span> <span data-ttu-id="ab2b6-293">The *python_tutorial_task.py* script uses this shared access signature when creates its BlockBlobService reference.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-293">The *python_tutorial_task.py* script uses this shared access signature when creates its BlockBlobService reference.</span></span> <span data-ttu-id="ab2b6-294">This provides write access to the container without requiring an access key for the storage account.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-294">This provides write access to the container without requiring an access key for the storage account.</span></span>

```python
# NOTE: Taken from python_tutorial_task.py

# Create the blob client using the container's SAS token.
# This allows us to create a client that provides write
# access only to the container.
blob_client = azureblob.BlockBlobService(account_name=args.storageaccount,
                                         sas_token=args.sastoken)
```

## <a name="step-6-monitor-tasks"></a><span data-ttu-id="ab2b6-295">Step 6: Monitor tasks</span><span class="sxs-lookup"><span data-stu-id="ab2b6-295">Step 6: Monitor tasks</span></span>
<span data-ttu-id="ab2b6-296">![Monitor tasks][6]</span><span class="sxs-lookup"><span data-stu-id="ab2b6-296">![Monitor tasks][6]</span></span><br/>
<span data-ttu-id="ab2b6-297">*The script (1) monitors the tasks for completion status, and (2) the tasks upload result data to Azure Storage*</span><span class="sxs-lookup"><span data-stu-id="ab2b6-297">*The script (1) monitors the tasks for completion status, and (2) the tasks upload result data to Azure Storage*</span></span>

<span data-ttu-id="ab2b6-298">When tasks are added to a job, they are automatically queued and scheduled for execution on compute nodes within the pool associated with the job.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-298">When tasks are added to a job, they are automatically queued and scheduled for execution on compute nodes within the pool associated with the job.</span></span> <span data-ttu-id="ab2b6-299">Based on the settings you specify, Batch handles all task queuing, scheduling, retrying, and other task administration duties for you.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-299">Based on the settings you specify, Batch handles all task queuing, scheduling, retrying, and other task administration duties for you.</span></span>

<span data-ttu-id="ab2b6-300">There are many approaches to monitoring task execution.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-300">There are many approaches to monitoring task execution.</span></span> <span data-ttu-id="ab2b6-301">The `wait_for_tasks_to_complete` function in *python_tutorial_client.py* provides a simple example of monitoring tasks for a certain state, in this case, the [completed][py_taskstate] state.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-301">The `wait_for_tasks_to_complete` function in *python_tutorial_client.py* provides a simple example of monitoring tasks for a certain state, in this case, the [completed][py_taskstate] state.</span></span>

```python
def wait_for_tasks_to_complete(batch_service_client, job_id, timeout):
    """
    Returns when all tasks in the specified job reach the Completed state.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: The id of the job whose tasks should be to monitored.
    :param timedelta timeout: The duration to wait for task completion. If all
    tasks in the specified job do not reach Completed state within this time
    period, an exception will be raised.
    """
    timeout_expiration = datetime.datetime.now() + timeout

    print("Monitoring all tasks for 'Completed' state, timeout in {}..."
          .format(timeout), end='')

    while datetime.datetime.now() < timeout_expiration:
        print('.', end='')
        sys.stdout.flush()
        tasks = batch_service_client.task.list(job_id)

        incomplete_tasks = [task for task in tasks if
                            task.state != batchmodels.TaskState.completed]
        if not incomplete_tasks:
            print()
            return True
        else:
            time.sleep(1)

    print()
    raise RuntimeError("ERROR: Tasks did not reach 'Completed' state within "
                       "timeout period of " + str(timeout))
```

## <a name="step-7-download-task-output"></a><span data-ttu-id="ab2b6-302">Step 7: Download task output</span><span class="sxs-lookup"><span data-stu-id="ab2b6-302">Step 7: Download task output</span></span>
<span data-ttu-id="ab2b6-303">![Download task output from Storage][7]</span><span class="sxs-lookup"><span data-stu-id="ab2b6-303">![Download task output from Storage][7]</span></span><br/>

<span data-ttu-id="ab2b6-304">Now that the job is completed, the output from the tasks can be downloaded from Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-304">Now that the job is completed, the output from the tasks can be downloaded from Azure Storage.</span></span> <span data-ttu-id="ab2b6-305">This is done with a call to `download_blobs_from_container` in *python_tutorial_client.py*:</span><span class="sxs-lookup"><span data-stu-id="ab2b6-305">This is done with a call to `download_blobs_from_container` in *python_tutorial_client.py*:</span></span>

```python
def download_blobs_from_container(block_blob_client,
                                  container_name, directory_path):
    """
    Downloads all blobs from the specified Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param container_name: The Azure Blob storage container from which to
     download files.
    :param directory_path: The local directory to which to download the files.
    """
    print('Downloading all files from container [{}]...'.format(
        container_name))

    container_blobs = block_blob_client.list_blobs(container_name)

    for blob in container_blobs.items:
        destination_file_path = os.path.join(directory_path, blob.name)

        block_blob_client.get_blob_to_path(container_name,
                                           blob.name,
                                           destination_file_path)

        print('  Downloaded blob [{}] from container [{}] to {}'.format(
            blob.name,
            container_name,
            destination_file_path))

    print('  Download complete!')
```

> [!NOTE]
> The call to `download_blobs_from_container` in *python_tutorial_client.py* specifies that the files should be downloaded to your home directory. Feel free to modify this output location.
>
>

## <a name="step-8-delete-containers"></a><span data-ttu-id="ab2b6-308">Step 8: Delete containers</span><span class="sxs-lookup"><span data-stu-id="ab2b6-308">Step 8: Delete containers</span></span>
<span data-ttu-id="ab2b6-309">Because you are charged for data that resides in Azure Storage, it is always a good idea to remove any blobs that are no longer needed for your Batch jobs.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-309">Because you are charged for data that resides in Azure Storage, it is always a good idea to remove any blobs that are no longer needed for your Batch jobs.</span></span> <span data-ttu-id="ab2b6-310">In *python_tutorial_client.py*, this is done with three calls to [BlockBlobService.delete_container][py_delete_container]:</span><span class="sxs-lookup"><span data-stu-id="ab2b6-310">In *python_tutorial_client.py*, this is done with three calls to [BlockBlobService.delete_container][py_delete_container]:</span></span>

```python
# Clean up storage resources
print('Deleting containers...')
blob_client.delete_container(app_container_name)
blob_client.delete_container(input_container_name)
blob_client.delete_container(output_container_name)
```

## <a name="step-9-delete-the-job-and-the-pool"></a><span data-ttu-id="ab2b6-311">Step 9: Delete the job and the pool</span><span class="sxs-lookup"><span data-stu-id="ab2b6-311">Step 9: Delete the job and the pool</span></span>
<span data-ttu-id="ab2b6-312">In the final step, you are prompted to delete the job and the pool that were created by the *python_tutorial_client.py* script.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-312">In the final step, you are prompted to delete the job and the pool that were created by the *python_tutorial_client.py* script.</span></span> <span data-ttu-id="ab2b6-313">Although you are not charged for jobs and tasks themselves, you *are* charged for compute nodes.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-313">Although you are not charged for jobs and tasks themselves, you *are* charged for compute nodes.</span></span> <span data-ttu-id="ab2b6-314">Thus, we recommend that you allocate nodes only as needed.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-314">Thus, we recommend that you allocate nodes only as needed.</span></span> <span data-ttu-id="ab2b6-315">Deleting unused pools can be part of your maintenance process.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-315">Deleting unused pools can be part of your maintenance process.</span></span>

<span data-ttu-id="ab2b6-316">The BatchServiceClient's [JobOperations][py_job] and [PoolOperations][py_pool] both have corresponding deletion methods, which are called if you confirm deletion:</span><span class="sxs-lookup"><span data-stu-id="ab2b6-316">The BatchServiceClient's [JobOperations][py_job] and [PoolOperations][py_pool] both have corresponding deletion methods, which are called if you confirm deletion:</span></span>

```python
# Clean up Batch resources (if the user so chooses).
if query_yes_no('Delete job?') == 'yes':
    batch_client.job.delete(_JOB_ID)

if query_yes_no('Delete pool?') == 'yes':
    batch_client.pool.delete(_POOL_ID)
```

> [!IMPORTANT]
> Keep in mind that you are charged for compute resources--deleting unused pools will minimize cost. Also, be aware that deleting a pool deletes all compute nodes within that pool, and that any data on the nodes will be unrecoverable after the pool is deleted.
>
>

## <a name="run-the-sample-script"></a><span data-ttu-id="ab2b6-319">Run the sample script</span><span class="sxs-lookup"><span data-stu-id="ab2b6-319">Run the sample script</span></span>
<span data-ttu-id="ab2b6-320">When you run the *python_tutorial_client.py* script from the tutorial [code sample][github_article_samples], the console output is similar to the following.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-320">When you run the *python_tutorial_client.py* script from the tutorial [code sample][github_article_samples], the console output is similar to the following.</span></span> <span data-ttu-id="ab2b6-321">There is a pause at `Monitoring all tasks for 'Completed' state, timeout in 0:20:00...` while the pool's compute nodes are created, started, and the commands in the pool's start task are executed.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-321">There is a pause at `Monitoring all tasks for 'Completed' state, timeout in 0:20:00...` while the pool's compute nodes are created, started, and the commands in the pool's start task are executed.</span></span> <span data-ttu-id="ab2b6-322">Use the [Azure portal][azure_portal] to monitor your pool, compute nodes, job, and tasks during and after execution.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-322">Use the [Azure portal][azure_portal] to monitor your pool, compute nodes, job, and tasks during and after execution.</span></span> <span data-ttu-id="ab2b6-323">Use the [Azure portal][azure_portal] or the [Microsoft Azure Storage Explorer][storage_explorer] to view the Storage resources (containers and blobs) that are created by the application.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-323">Use the [Azure portal][azure_portal] or the [Microsoft Azure Storage Explorer][storage_explorer] to view the Storage resources (containers and blobs) that are created by the application.</span></span>

> [!TIP]
> Run the *python_tutorial_client.py* script from within the `azure-batch-samples/Python/Batch/article_samples` directory. It uses a relative path for the `common.helpers` module import, so you might see `ImportError: No module named 'common'` if you don't run the script from within this directory.
>
>

<span data-ttu-id="ab2b6-326">Typical execution time is **approximately 5-7 minutes** when you run the sample in its default configuration.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-326">Typical execution time is **approximately 5-7 minutes** when you run the sample in its default configuration.</span></span>

```
Sample start: 2016-05-20 22:47:10

Uploading file /home/user/py_tutorial/python_tutorial_task.py to container [application]...
Uploading file /home/user/py_tutorial/data/taskdata1.txt to container [input]...
Uploading file /home/user/py_tutorial/data/taskdata2.txt to container [input]...
Uploading file /home/user/py_tutorial/data/taskdata3.txt to container [input]...
Creating pool [PythonTutorialPool]...
Creating job [PythonTutorialJob]...
Adding 3 tasks to job [PythonTutorialJob]...
Monitoring all tasks for 'Completed' state, timeout in 0:20:00..........................................................................
  Success! All tasks reached the 'Completed' state within the specified timeout period.
Downloading all files from container [output]...
  Downloaded blob [taskdata1_OUTPUT.txt] from container [output] to /home/user/taskdata1_OUTPUT.txt
  Downloaded blob [taskdata2_OUTPUT.txt] from container [output] to /home/user/taskdata2_OUTPUT.txt
  Downloaded blob [taskdata3_OUTPUT.txt] from container [output] to /home/user/taskdata3_OUTPUT.txt
  Download complete!
Deleting containers...

Sample end: 2016-05-20 22:53:12
Elapsed time: 0:06:02

Delete job? [Y/n]
Delete pool? [Y/n]

Press ENTER to exit...
```

## <a name="next-steps"></a><span data-ttu-id="ab2b6-327">Next steps</span><span class="sxs-lookup"><span data-stu-id="ab2b6-327">Next steps</span></span>
<span data-ttu-id="ab2b6-328">Feel free to make changes to *python_tutorial_client.py* and *python_tutorial_task.py* to experiment with different compute scenarios.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-328">Feel free to make changes to *python_tutorial_client.py* and *python_tutorial_task.py* to experiment with different compute scenarios.</span></span> <span data-ttu-id="ab2b6-329">For example, try adding an execution delay to *python_tutorial_task.py* to simulate long-running tasks and monitor them in the portal.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-329">For example, try adding an execution delay to *python_tutorial_task.py* to simulate long-running tasks and monitor them in the portal.</span></span> <span data-ttu-id="ab2b6-330">Try adding more tasks or adjusting the number of compute nodes.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-330">Try adding more tasks or adjusting the number of compute nodes.</span></span> <span data-ttu-id="ab2b6-331">Add logic to check for and allow the use of an existing pool to speed execution time.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-331">Add logic to check for and allow the use of an existing pool to speed execution time.</span></span>

<span data-ttu-id="ab2b6-332">Now that you're familiar with the basic workflow of a Batch solution, it's time to dig in to the additional features of the Batch service.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-332">Now that you're familiar with the basic workflow of a Batch solution, it's time to dig in to the additional features of the Batch service.</span></span>

* <span data-ttu-id="ab2b6-333">Review the [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new to the service.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-333">Review the [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new to the service.</span></span>
* <span data-ttu-id="ab2b6-334">Start on the other Batch development articles under **Development in-depth** in the [Batch learning path][batch_learning_path].</span><span class="sxs-lookup"><span data-stu-id="ab2b6-334">Start on the other Batch development articles under **Development in-depth** in the [Batch learning path][batch_learning_path].</span></span>
* <span data-ttu-id="ab2b6-335">Check out a different implementation of processing the "top N words" workload with Batch in the [TopNWords][github_topnwords] sample.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-335">Check out a different implementation of processing the "top N words" workload with Batch in the [TopNWords][github_topnwords] sample.</span></span>

[azure_batch]: https://azure.microsoft.com/services/batch/
[azure_free_account]: https://azure.microsoft.com/free/
[azure_portal]: https://portal.azure.com
[batch_learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[blog_linux]: http://blogs.technet.com/b/windowshpc/archive/2016/03/30/introducing-linux-support-on-azure-batch.aspx
[crypto]: https://cryptography.io/en/latest/
[crypto_install]: https://cryptography.io/en/latest/installation/
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[github_topnwords]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/TopNWords
[github_article_samples]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch/article_samples

[nuget_packagemgr]: https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c
[nuget_restore]: https://docs.nuget.org/consume/package-restore/msbuild-integrated#enabling-package-restore-during-build

[py_account_ops]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations
[py_azure_sdk]: https://pypi.python.org/pypi/azure
[py_batch_docs]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.html
[py_batch_package]: https://pypi.python.org/pypi/azure-batch
[py_batchserviceclient]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.html#azure.batch.BatchServiceClient
[py_blockblobservice]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.blockblobservice.html#azure.storage.blob.blockblobservice.BlockBlobService
[py_cloudtask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudTask
[py_computenodeuser]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.models.html#azure.batch.models.ComputeNodeUser
[py_cs_config]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudServiceConfiguration
[py_delete_container]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.delete_container
[py_gen_blob_sas]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.generate_blob_shared_access_signature
[py_gen_container_sas]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.generate_container_shared_access_signature
[py_image_ref]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_imagereference]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_job]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.JobOperations
[py_jobpreptask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.JobPreparationTask
[py_jobreltask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.JobReleaseTask
[py_list_skus]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations.list_node_agent_skus
[py_make_blob_url]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.make_blob_url
[py_pool]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.PoolOperations
[py_pooladdparam]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.PoolAddParameter
[py_poolinfo]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.PoolInformation
[py_resource_file]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.ResourceFile
[py_samples_github]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch/
[py_starttask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.StartTask
[py_starttask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.StartTask
[py_task]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudTask
[py_taskstate]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.TaskState
[py_vm_config]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.VirtualMachineConfiguration
[pypi_batch]: https://pypi.python.org/pypi/azure-batch
[pypi_storage]: https://pypi.python.org/pypi/azure-storage
[pypi_install]: https://packaging.python.org/installing/
[storage_explorer]: http://storageexplorer.com/
[visual_studio]: https://www.visualstudio.com/products/vs-2015-product-editions
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-python-tutorial/batch_workflow_01_sm.png "Create containers in Azure Storage"
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-python-tutorial/batch_workflow_02_sm.png "Upload task application and input (data) files to containers"
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-python-tutorial/batch_workflow_03_sm.png "Create Batch pool"
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-python-tutorial/batch_workflow_04_sm.png "Create Batch job"
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-python-tutorial/batch_workflow_05_sm.png "Add tasks to job"
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-python-tutorial/batch_workflow_06_sm.png "Monitor tasks"
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-python-tutorial/batch_workflow_07_sm.png "Download task output from Storage"
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-python-tutorial/batch_workflow_sm.png "Batch solution workflow (full diagram)"
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-python-tutorial/credentials_batch_sm.png "Batch credentials in Portal"
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-python-tutorial/credentials_storage_sm.png "Storage credentials in Portal"
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-python-tutorial/batch_workflow_minimal_sm.png "Batch solution workflow (minimal diagram)"











