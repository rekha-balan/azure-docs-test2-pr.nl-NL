---
title: LogDownloader - Azure Cognitive Services | Microsoft Docs
description: Download log files that are produced by Azure Custom Decision Service.
services: cognitive-services
author: marco-rossi29
manager: marco-rossi29
ms.service: cognitive-services
ms.topic: article
ms.date: 05/09/2018
ms.author: marossi
ms.openlocfilehash: 783b534b3b3f4bb7f5d9f073f491690759edfea5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857340"
---
# <a name="logdownloader"></a><span data-ttu-id="1b779-103">LogDownloader</span><span class="sxs-lookup"><span data-stu-id="1b779-103">LogDownloader</span></span>

<span data-ttu-id="1b779-104">Download log files that are produced by Azure Custom Decision Service and generate the *.gz* files that are used by Experimentation.</span><span class="sxs-lookup"><span data-stu-id="1b779-104">Download log files that are produced by Azure Custom Decision Service and generate the *.gz* files that are used by Experimentation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b779-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1b779-105">Prerequisites</span></span>

- <span data-ttu-id="1b779-106">Python 3: Installed and on your path.</span><span class="sxs-lookup"><span data-stu-id="1b779-106">Python 3: Installed and on your path.</span></span> <span data-ttu-id="1b779-107">We recommend the 64-bit version to handle large files.</span><span class="sxs-lookup"><span data-stu-id="1b779-107">We recommend the 64-bit version to handle large files.</span></span>
- <span data-ttu-id="1b779-108">The *Microsoft/mwt-ds* repository: [Clone the repo](https://github.com/Microsoft/mwt-ds).</span><span class="sxs-lookup"><span data-stu-id="1b779-108">The *Microsoft/mwt-ds* repository: [Clone the repo](https://github.com/Microsoft/mwt-ds).</span></span>
- <span data-ttu-id="1b779-109">The *azure-storage-blob* package: For installation details, go to [Microsoft Azure Storage Library for Python](https://github.com/Azure/azure-storage-python#option-1-via-pypi).</span><span class="sxs-lookup"><span data-stu-id="1b779-109">The *azure-storage-blob* package: For installation details, go to [Microsoft Azure Storage Library for Python](https://github.com/Azure/azure-storage-python#option-1-via-pypi).</span></span>
- <span data-ttu-id="1b779-110">Enter your Azure storage connection string in *mwt-ds/DataScience/ds.config*: Follow the *my_app_id: my_connectionString* template.</span><span class="sxs-lookup"><span data-stu-id="1b779-110">Enter your Azure storage connection string in *mwt-ds/DataScience/ds.config*: Follow the *my_app_id: my_connectionString* template.</span></span> <span data-ttu-id="1b779-111">You can specify multiple `app_id`.</span><span class="sxs-lookup"><span data-stu-id="1b779-111">You can specify multiple `app_id`.</span></span> <span data-ttu-id="1b779-112">When you run `LogDownloader.py`, if the input `app_id` is not found in `ds.config`, `LogDownloader.py` uses the `$Default` connection string.</span><span class="sxs-lookup"><span data-stu-id="1b779-112">When you run `LogDownloader.py`, if the input `app_id` is not found in `ds.config`, `LogDownloader.py` uses the `$Default` connection string.</span></span>

## <a name="usage"></a><span data-ttu-id="1b779-113">Usage</span><span class="sxs-lookup"><span data-stu-id="1b779-113">Usage</span></span>

<span data-ttu-id="1b779-114">Go to `mwt-ds/DataScience` and run `LogDownloader.py` with the relevant arguments, as detailed in the following code:</span><span class="sxs-lookup"><span data-stu-id="1b779-114">Go to `mwt-ds/DataScience` and run `LogDownloader.py` with the relevant arguments, as detailed in the following code:</span></span>

```cmd
python LogDownloader.py [-h] -a APP_ID -l LOG_DIR [-s START_DATE]
                        [-e END_DATE] [-o OVERWRITE_MODE] [--dry_run]
                        [--create_gzip] [--delta_mod_t DELTA_MOD_T]
                        [--verbose] [-v VERSION]
```

### <a name="parameters"></a><span data-ttu-id="1b779-115">Parameters</span><span class="sxs-lookup"><span data-stu-id="1b779-115">Parameters</span></span>

| <span data-ttu-id="1b779-116">Input</span><span class="sxs-lookup"><span data-stu-id="1b779-116">Input</span></span> | <span data-ttu-id="1b779-117">Description</span><span class="sxs-lookup"><span data-stu-id="1b779-117">Description</span></span> | <span data-ttu-id="1b779-118">Default</span><span class="sxs-lookup"><span data-stu-id="1b779-118">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1b779-119">`-h`, `--help`</span><span class="sxs-lookup"><span data-stu-id="1b779-119">`-h`, `--help`</span></span> | <span data-ttu-id="1b779-120">Show the help message and exit.</span><span class="sxs-lookup"><span data-stu-id="1b779-120">Show the help message and exit.</span></span> | |
| <span data-ttu-id="1b779-121">`-a APP_ID`, `--app_id APP_ID`</span><span class="sxs-lookup"><span data-stu-id="1b779-121">`-a APP_ID`, `--app_id APP_ID`</span></span> | <span data-ttu-id="1b779-122">The app ID (that is, the Azure Storage blob container name).</span><span class="sxs-lookup"><span data-stu-id="1b779-122">The app ID (that is, the Azure Storage blob container name).</span></span> | <span data-ttu-id="1b779-123">Required</span><span class="sxs-lookup"><span data-stu-id="1b779-123">Required</span></span> |
| <span data-ttu-id="1b779-124">`-l LOG_DIR`, `--log_dir LOG_DIR`</span><span class="sxs-lookup"><span data-stu-id="1b779-124">`-l LOG_DIR`, `--log_dir LOG_DIR`</span></span> | <span data-ttu-id="1b779-125">The base directory for downloading data (a subfolder is created).</span><span class="sxs-lookup"><span data-stu-id="1b779-125">The base directory for downloading data (a subfolder is created).</span></span>  | <span data-ttu-id="1b779-126">Required</span><span class="sxs-lookup"><span data-stu-id="1b779-126">Required</span></span> |
| <span data-ttu-id="1b779-127">`-s START_DATE`, `--start_date START_DATE`</span><span class="sxs-lookup"><span data-stu-id="1b779-127">`-s START_DATE`, `--start_date START_DATE`</span></span> | <span data-ttu-id="1b779-128">The downloading start date (included), in *YYYY-MM-DD* format.</span><span class="sxs-lookup"><span data-stu-id="1b779-128">The downloading start date (included), in *YYYY-MM-DD* format.</span></span> | `None` |
| <span data-ttu-id="1b779-129">`-e END_DATE`, `--end_date END_DATE`</span><span class="sxs-lookup"><span data-stu-id="1b779-129">`-e END_DATE`, `--end_date END_DATE`</span></span> | <span data-ttu-id="1b779-130">The downloading end date (included), in *YYYY-MM-DD* format.</span><span class="sxs-lookup"><span data-stu-id="1b779-130">The downloading end date (included), in *YYYY-MM-DD* format.</span></span> | `None` |
| <span data-ttu-id="1b779-131">`-o OVERWRITE_MODE`, `--overwrite_mode OVERWRITE_MODE`</span><span class="sxs-lookup"><span data-stu-id="1b779-131">`-o OVERWRITE_MODE`, `--overwrite_mode OVERWRITE_MODE`</span></span> | <span data-ttu-id="1b779-132">The overwrite mode to use.</span><span class="sxs-lookup"><span data-stu-id="1b779-132">The overwrite mode to use.</span></span> | |
| | <span data-ttu-id="1b779-133">`0`: Never overwrite; ask the user whether blobs are currently used.</span><span class="sxs-lookup"><span data-stu-id="1b779-133">`0`: Never overwrite; ask the user whether blobs are currently used.</span></span> | <span data-ttu-id="1b779-134">Default</span><span class="sxs-lookup"><span data-stu-id="1b779-134">Default</span></span> | |
| | <span data-ttu-id="1b779-135">`1`: Ask the user how to proceed when the files have different sizes or when the blobs are currently being used.</span><span class="sxs-lookup"><span data-stu-id="1b779-135">`1`: Ask the user how to proceed when the files have different sizes or when the blobs are currently being used.</span></span> | |
| | <span data-ttu-id="1b779-136">`2`: Always overwrite; download currently used blobs.</span><span class="sxs-lookup"><span data-stu-id="1b779-136">`2`: Always overwrite; download currently used blobs.</span></span> | |
| | <span data-ttu-id="1b779-137">`3`: Never overwrite, and append if the size is larger, without asking; download currently used blobs.</span><span class="sxs-lookup"><span data-stu-id="1b779-137">`3`: Never overwrite, and append if the size is larger, without asking; download currently used blobs.</span></span> | |
| | <span data-ttu-id="1b779-138">`4`: Never overwrite, and append if the size is larger, without asking; skip currently used blobs.</span><span class="sxs-lookup"><span data-stu-id="1b779-138">`4`: Never overwrite, and append if the size is larger, without asking; skip currently used blobs.</span></span> | |
| `--dry_run` | <span data-ttu-id="1b779-139">Print which blobs would have been downloaded, without downloading.</span><span class="sxs-lookup"><span data-stu-id="1b779-139">Print which blobs would have been downloaded, without downloading.</span></span> | `False` |
| `--create_gzip` | <span data-ttu-id="1b779-140">Create a *gzip* file for Vowpal Wabbit.</span><span class="sxs-lookup"><span data-stu-id="1b779-140">Create a *gzip* file for Vowpal Wabbit.</span></span> | `False` |
| `--delta_mod_t DELTA_MOD_T` | <span data-ttu-id="1b779-141">The time window, in seconds, for detecting whether a file is currently in use.</span><span class="sxs-lookup"><span data-stu-id="1b779-141">The time window, in seconds, for detecting whether a file is currently in use.</span></span> | <span data-ttu-id="1b779-142">`3600` sec (`1` hour)</span><span class="sxs-lookup"><span data-stu-id="1b779-142">`3600` sec (`1` hour)</span></span> |
| `--verbose` | <span data-ttu-id="1b779-143">Print more details.</span><span class="sxs-lookup"><span data-stu-id="1b779-143">Print more details.</span></span> | `False` |
| <span data-ttu-id="1b779-144">`-v VERSION`, `--version VERSION`</span><span class="sxs-lookup"><span data-stu-id="1b779-144">`-v VERSION`, `--version VERSION`</span></span> | <span data-ttu-id="1b779-145">The log downloader version to use.</span><span class="sxs-lookup"><span data-stu-id="1b779-145">The log downloader version to use.</span></span> | |
| | <span data-ttu-id="1b779-146">`1`: For uncooked logs (only for backward compatibility).</span><span class="sxs-lookup"><span data-stu-id="1b779-146">`1`: For uncooked logs (only for backward compatibility).</span></span> | <span data-ttu-id="1b779-147">Deprecated</span><span class="sxs-lookup"><span data-stu-id="1b779-147">Deprecated</span></span> |
| | <span data-ttu-id="1b779-148">`2`: For cooked logs.</span><span class="sxs-lookup"><span data-stu-id="1b779-148">`2`: For cooked logs.</span></span> | <span data-ttu-id="1b779-149">Default</span><span class="sxs-lookup"><span data-stu-id="1b779-149">Default</span></span> |

### <a name="examples"></a><span data-ttu-id="1b779-150">Examples</span><span class="sxs-lookup"><span data-stu-id="1b779-150">Examples</span></span>

<span data-ttu-id="1b779-151">For a dry run of downloading all the data in your Azure Storage blob container, use the following code:</span><span class="sxs-lookup"><span data-stu-id="1b779-151">For a dry run of downloading all the data in your Azure Storage blob container, use the following code:</span></span>
```cmd
python LogDownloader.py -a your_app_id -l d:\data --dry_run
```

<span data-ttu-id="1b779-152">To download only logs created since January 1, 2018 with `overwrite_mode=4`, use the following code:</span><span class="sxs-lookup"><span data-stu-id="1b779-152">To download only logs created since January 1, 2018 with `overwrite_mode=4`, use the following code:</span></span>
```cmd
python LogDownloader.py -a your_app_id -l d:\data -s 2018-1-1 -o 4
```

<span data-ttu-id="1b779-153">To create a *gzip* file merging all the downloaded files, use the following code:</span><span class="sxs-lookup"><span data-stu-id="1b779-153">To create a *gzip* file merging all the downloaded files, use the following code:</span></span>
```cmd
python LogDownloader.py -a your_app_id -l d:\data -s 2018-1-1 -o 4 --create_gzip
```