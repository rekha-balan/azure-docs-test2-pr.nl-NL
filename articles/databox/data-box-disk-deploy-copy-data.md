---
title: Copy data to  your Microsoft Azure Data Box Disk| Microsoft Docs
description: Use this tutorial to learn how to copy data to your Azure Data Box Disk
services: databox
documentationcenter: NA
author: alkohli
manager: twooley
editor: ''
ms.assetid: ''
ms.service: databox
ms.devlang: NA
ms.topic: tutorial
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 09/10/2018
ms.author: alkohli
Customer intent: As an IT admin, I need to be able to order Data Box Disk to upload on-premises data from my server onto Azure.
ms.openlocfilehash: b83258e7ff949184656d8329b5c48b6f14fe15af
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968902"
---
# <a name="tutorial-copy-data-to-azure-data-box-disk-and-verify"></a><span data-ttu-id="3b151-103">Tutorial: Copy data to Azure Data Box Disk and verify</span><span class="sxs-lookup"><span data-stu-id="3b151-103">Tutorial: Copy data to Azure Data Box Disk and verify</span></span>

<span data-ttu-id="3b151-104">This tutorial describes how to copy data from your host computer and then generate checksums to verify data integrity.</span><span class="sxs-lookup"><span data-stu-id="3b151-104">This tutorial describes how to copy data from your host computer and then generate checksums to verify data integrity.</span></span>

<span data-ttu-id="3b151-105">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="3b151-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3b151-106">Copy data to Data Box Disk</span><span class="sxs-lookup"><span data-stu-id="3b151-106">Copy data to Data Box Disk</span></span>
> * <span data-ttu-id="3b151-107">Verify data integrity</span><span class="sxs-lookup"><span data-stu-id="3b151-107">Verify data integrity</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b151-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3b151-108">Prerequisites</span></span>

<span data-ttu-id="3b151-109">Before you begin, make sure that:</span><span class="sxs-lookup"><span data-stu-id="3b151-109">Before you begin, make sure that:</span></span>
- <span data-ttu-id="3b151-110">You have completed the [Tutorial: Install and configure your Azure Data Box Disk](data-box-disk-deploy-set-up.md).</span><span class="sxs-lookup"><span data-stu-id="3b151-110">You have completed the [Tutorial: Install and configure your Azure Data Box Disk](data-box-disk-deploy-set-up.md).</span></span>
- <span data-ttu-id="3b151-111">Your disks are unlocked and connected to a client computer.</span><span class="sxs-lookup"><span data-stu-id="3b151-111">Your disks are unlocked and connected to a client computer.</span></span>
- <span data-ttu-id="3b151-112">Your client computer that is used to copy data to the disks must run a [Supported operating system](data-box-disk-system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="3b151-112">Your client computer that is used to copy data to the disks must run a [Supported operating system](data-box-disk-system-requirements.md).</span></span>


## <a name="copy-data-to-disks"></a><span data-ttu-id="3b151-113">Copy data to disks</span><span class="sxs-lookup"><span data-stu-id="3b151-113">Copy data to disks</span></span>

<span data-ttu-id="3b151-114">Perform the following steps to connect and copy data from your computer to the Data Box Disk.</span><span class="sxs-lookup"><span data-stu-id="3b151-114">Perform the following steps to connect and copy data from your computer to the Data Box Disk.</span></span>

1. <span data-ttu-id="3b151-115">View the contents of the unlocked drive.</span><span class="sxs-lookup"><span data-stu-id="3b151-115">View the contents of the unlocked drive.</span></span> 

    ![View drive content](media/data-box-disk-deploy-copy-data/data-box-disk-content.png)
 
2. <span data-ttu-id="3b151-117">Copy the data that needs to be imported as block blobs in to BlockBlob folder.</span><span class="sxs-lookup"><span data-stu-id="3b151-117">Copy the data that needs to be imported as block blobs in to BlockBlob folder.</span></span> <span data-ttu-id="3b151-118">Similarly, copy data such as VHD/VHDX to PageBlob folder.</span><span class="sxs-lookup"><span data-stu-id="3b151-118">Similarly, copy data such as VHD/VHDX to PageBlob folder.</span></span> 

    <span data-ttu-id="3b151-119">A container is created in the Azure storage account for each subfolder under BlockBlob and PageBlob folders.</span><span class="sxs-lookup"><span data-stu-id="3b151-119">A container is created in the Azure storage account for each subfolder under BlockBlob and PageBlob folders.</span></span> <span data-ttu-id="3b151-120">All files under BlockBlob and PageBlob folders are copied into a default container `$root` under the Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="3b151-120">All files under BlockBlob and PageBlob folders are copied into a default container `$root` under the Azure Storage account.</span></span> <span data-ttu-id="3b151-121">Any files in the `$root` container are always uploaded as block blobs.</span><span class="sxs-lookup"><span data-stu-id="3b151-121">Any files in the `$root` container are always uploaded as block blobs.</span></span>

    <span data-ttu-id="3b151-122">If files and folders exist in the root directory, then you must move those to a different folder before you begin data copy.</span><span class="sxs-lookup"><span data-stu-id="3b151-122">If files and folders exist in the root directory, then you must move those to a different folder before you begin data copy.</span></span>

    <span data-ttu-id="3b151-123">Follow the Azure naming requirements for container and blob names.</span><span class="sxs-lookup"><span data-stu-id="3b151-123">Follow the Azure naming requirements for container and blob names.</span></span>

    |<span data-ttu-id="3b151-124">Entity</span><span class="sxs-lookup"><span data-stu-id="3b151-124">Entity</span></span>   |<span data-ttu-id="3b151-125">Conventions</span><span class="sxs-lookup"><span data-stu-id="3b151-125">Conventions</span></span>  |
    |---------|---------|
    |<span data-ttu-id="3b151-126">Container names block blob and page blob</span><span class="sxs-lookup"><span data-stu-id="3b151-126">Container names block blob and page blob</span></span>     |<span data-ttu-id="3b151-127">Must start with a letter or number, and can contain only lowercase letters, numbers, and the hyphen (-).</span><span class="sxs-lookup"><span data-stu-id="3b151-127">Must start with a letter or number, and can contain only lowercase letters, numbers, and the hyphen (-).</span></span> <span data-ttu-id="3b151-128">Every hyphen (-) must be immediately preceded and followed by a letter or number.</span><span class="sxs-lookup"><span data-stu-id="3b151-128">Every hyphen (-) must be immediately preceded and followed by a letter or number.</span></span> <span data-ttu-id="3b151-129">Consecutive hyphens are not permitted in names.</span><span class="sxs-lookup"><span data-stu-id="3b151-129">Consecutive hyphens are not permitted in names.</span></span> <br><span data-ttu-id="3b151-130">Must be a valid DNS name, which is 3 to 63 characters long.</span><span class="sxs-lookup"><span data-stu-id="3b151-130">Must be a valid DNS name, which is 3 to 63 characters long.</span></span>          |
    |<span data-ttu-id="3b151-131">Blob names for block blob and page blob</span><span class="sxs-lookup"><span data-stu-id="3b151-131">Blob names for block blob and page blob</span></span>    |<span data-ttu-id="3b151-132">Blob names are case-sensitive and can contain any combination of characters.</span><span class="sxs-lookup"><span data-stu-id="3b151-132">Blob names are case-sensitive and can contain any combination of characters.</span></span> <br><span data-ttu-id="3b151-133">A blob name must be between 1 to 1,024 characters long.</span><span class="sxs-lookup"><span data-stu-id="3b151-133">A blob name must be between 1 to 1,024 characters long.</span></span><br><span data-ttu-id="3b151-134">Reserved URL characters must be properly escaped.</span><span class="sxs-lookup"><span data-stu-id="3b151-134">Reserved URL characters must be properly escaped.</span></span><br><span data-ttu-id="3b151-135">The number of path segments comprising the blob name cannot exceed 254.</span><span class="sxs-lookup"><span data-stu-id="3b151-135">The number of path segments comprising the blob name cannot exceed 254.</span></span> <span data-ttu-id="3b151-136">A path segment is the string between consecutive delimiter characters (for example, the forward slash '/') that correspond to the name of a virtual directory.</span><span class="sxs-lookup"><span data-stu-id="3b151-136">A path segment is the string between consecutive delimiter characters (for example, the forward slash '/') that correspond to the name of a virtual directory.</span></span>         |

    > [!IMPORTANT] 
    > <span data-ttu-id="3b151-137">All the containers and blobs should conform to [Azure naming conventions](data-box-disk-limits.md#azure-block-blob-and-page-blob-naming-conventions).</span><span class="sxs-lookup"><span data-stu-id="3b151-137">All the containers and blobs should conform to [Azure naming conventions](data-box-disk-limits.md#azure-block-blob-and-page-blob-naming-conventions).</span></span> <span data-ttu-id="3b151-138">If these rules are not followed, the data upload to Azure will fail.</span><span class="sxs-lookup"><span data-stu-id="3b151-138">If these rules are not followed, the data upload to Azure will fail.</span></span>

3. <span data-ttu-id="3b151-139">When copying files, ensure that files do not exceed ~4.7 TiB for block blobs and ~8 TiB for page blobs.</span><span class="sxs-lookup"><span data-stu-id="3b151-139">When copying files, ensure that files do not exceed ~4.7 TiB for block blobs and ~8 TiB for page blobs.</span></span> 
4. <span data-ttu-id="3b151-140">You can use drag and drop with File Explorer to copy the data.</span><span class="sxs-lookup"><span data-stu-id="3b151-140">You can use drag and drop with File Explorer to copy the data.</span></span> <span data-ttu-id="3b151-141">You can also use any SMB compatible file copy tool such as Robocopy to copy your data.</span><span class="sxs-lookup"><span data-stu-id="3b151-141">You can also use any SMB compatible file copy tool such as Robocopy to copy your data.</span></span> <span data-ttu-id="3b151-142">Multiple copy jobs can be initiated using the following Robocopy command:</span><span class="sxs-lookup"><span data-stu-id="3b151-142">Multiple copy jobs can be initiated using the following Robocopy command:</span></span>

    `Robocopy <source> <destination>  * /MT:64 /E /R:1 /W:1 /NFL /NDL /FFT /Log:c:\RobocopyLog.txt` 
    
    <span data-ttu-id="3b151-143">The parameters and options for the command are tabulated as follows:</span><span class="sxs-lookup"><span data-stu-id="3b151-143">The parameters and options for the command are tabulated as follows:</span></span>
    
    |<span data-ttu-id="3b151-144">Parameters/Options</span><span class="sxs-lookup"><span data-stu-id="3b151-144">Parameters/Options</span></span>  |<span data-ttu-id="3b151-145">Description</span><span class="sxs-lookup"><span data-stu-id="3b151-145">Description</span></span> |
    |--------------------|------------|
    |<span data-ttu-id="3b151-146">Source</span><span class="sxs-lookup"><span data-stu-id="3b151-146">Source</span></span>            | <span data-ttu-id="3b151-147">Specifies the path to the source directory.</span><span class="sxs-lookup"><span data-stu-id="3b151-147">Specifies the path to the source directory.</span></span>        |
    |<span data-ttu-id="3b151-148">Destination</span><span class="sxs-lookup"><span data-stu-id="3b151-148">Destination</span></span>       | <span data-ttu-id="3b151-149">Specifies the path to the destination directory.</span><span class="sxs-lookup"><span data-stu-id="3b151-149">Specifies the path to the destination directory.</span></span>        |
    |<span data-ttu-id="3b151-150">/E</span><span class="sxs-lookup"><span data-stu-id="3b151-150">/E</span></span>                  | <span data-ttu-id="3b151-151">Copies subdirectories including empty directories.</span><span class="sxs-lookup"><span data-stu-id="3b151-151">Copies subdirectories including empty directories.</span></span> |
    |<span data-ttu-id="3b151-152">/MT[:N]</span><span class="sxs-lookup"><span data-stu-id="3b151-152">/MT[:N]</span></span>             | <span data-ttu-id="3b151-153">Creates multi-threaded copies with N threads where N is an integer between 1 and 128.</span><span class="sxs-lookup"><span data-stu-id="3b151-153">Creates multi-threaded copies with N threads where N is an integer between 1 and 128.</span></span> <br><span data-ttu-id="3b151-154">The default value for N is 8.</span><span class="sxs-lookup"><span data-stu-id="3b151-154">The default value for N is 8.</span></span>        |
    |<span data-ttu-id="3b151-155">/R: <N></span><span class="sxs-lookup"><span data-stu-id="3b151-155">/R: <N></span></span>             | <span data-ttu-id="3b151-156">Specifies the number of retries on failed copies.</span><span class="sxs-lookup"><span data-stu-id="3b151-156">Specifies the number of retries on failed copies.</span></span> <span data-ttu-id="3b151-157">The default value of N is 1,000,000 (one million retries).</span><span class="sxs-lookup"><span data-stu-id="3b151-157">The default value of N is 1,000,000 (one million retries).</span></span>        |
    |<span data-ttu-id="3b151-158">/W: <N></span><span class="sxs-lookup"><span data-stu-id="3b151-158">/W: <N></span></span>             | <span data-ttu-id="3b151-159">Specifies the wait time between retries, in seconds.</span><span class="sxs-lookup"><span data-stu-id="3b151-159">Specifies the wait time between retries, in seconds.</span></span> <span data-ttu-id="3b151-160">The default value of N is 30 (wait time 30 seconds).</span><span class="sxs-lookup"><span data-stu-id="3b151-160">The default value of N is 30 (wait time 30 seconds).</span></span>        |
    |<span data-ttu-id="3b151-161">/NFL</span><span class="sxs-lookup"><span data-stu-id="3b151-161">/NFL</span></span>                | <span data-ttu-id="3b151-162">Specifies that file names are not to be logged.</span><span class="sxs-lookup"><span data-stu-id="3b151-162">Specifies that file names are not to be logged.</span></span>        |
    |<span data-ttu-id="3b151-163">/NDL</span><span class="sxs-lookup"><span data-stu-id="3b151-163">/NDL</span></span>                | <span data-ttu-id="3b151-164">Specifies that directory names are not to be logged.</span><span class="sxs-lookup"><span data-stu-id="3b151-164">Specifies that directory names are not to be logged.</span></span>        |
    |<span data-ttu-id="3b151-165">/FFT</span><span class="sxs-lookup"><span data-stu-id="3b151-165">/FFT</span></span>                | <span data-ttu-id="3b151-166">Assumes FAT file times (two-second precision).</span><span class="sxs-lookup"><span data-stu-id="3b151-166">Assumes FAT file times (two-second precision).</span></span>        |
    |<span data-ttu-id="3b151-167">/Log:<Log File></span><span class="sxs-lookup"><span data-stu-id="3b151-167">/Log:<Log File></span></span>     | <span data-ttu-id="3b151-168">Writes the status output to the log file (overwrites the existing log file).</span><span class="sxs-lookup"><span data-stu-id="3b151-168">Writes the status output to the log file (overwrites the existing log file).</span></span>         |

    <span data-ttu-id="3b151-169">Multiple disks can be used in parallel with multiple jobs running on each disk.</span><span class="sxs-lookup"><span data-stu-id="3b151-169">Multiple disks can be used in parallel with multiple jobs running on each disk.</span></span> 

6. <span data-ttu-id="3b151-170">Check the copy status when the job is in progress.</span><span class="sxs-lookup"><span data-stu-id="3b151-170">Check the copy status when the job is in progress.</span></span> <span data-ttu-id="3b151-171">The following sample shows the output of the robocopy command to copy files to the Data Box Disk.</span><span class="sxs-lookup"><span data-stu-id="3b151-171">The following sample shows the output of the robocopy command to copy files to the Data Box Disk.</span></span>

    ```
    C:\Users>robocopy
        -------------------------------------------------------------------------------
       ROBOCOPY     ::     Robust File Copy for Windows
    -------------------------------------------------------------------------------
    
      Started : Thursday, March 8, 2018 2:34:53 PM
           Simple Usage :: ROBOCOPY source destination /MIR
    
                 source :: Source Directory (drive:\path or \\server\share\path).
            destination :: Destination Dir  (drive:\path or \\server\share\path).
                   /MIR :: Mirror a complete directory tree.
    
        For more usage information run ROBOCOPY /?    
    
    ****  /MIR can DELETE files as well as copy them !
    
    C:\Users>Robocopy C:\Git\azure-docs-pr\contributor-guide \\10.126.76.172\devicemanagertest1_AzFile\templates /MT:64 /E /R:1 /W:1 /FFT 
    -------------------------------------------------------------------------------
       ROBOCOPY     ::     Robust File Copy for Windows
    -------------------------------------------------------------------------------
    
      Started : Thursday, March 8, 2018 2:34:58 PM
       Source : C:\Git\azure-docs-pr\contributor-guide\
         Dest : \\10.126.76.172\devicemanagertest1_AzFile\templates\
    
        Files : *.*
    
      Options : *.* /DCOPY:DA /COPY:DAT /MT:8 /R:1000000 /W:30
    
    ------------------------------------------------------------------------------
    
    100%        New File                 206        C:\Git\azure-docs-pr\contributor-guide\article-metadata.md
    100%        New File                 209        C:\Git\azure-docs-pr\contributor-guide\content-channel-guidance.md
    100%        New File                 732        C:\Git\azure-docs-pr\contributor-guide\contributor-guide-index.md
    100%        New File                 199        C:\Git\azure-docs-pr\contributor-guide\contributor-guide-pr-criteria.md
                New File                 178        C:\Git\azure-docs-pr\contributor-guide\contributor-guide-pull-request-co100%  .md
                New File                 250        C:\Git\azure-docs-pr\contributor-guide\contributor-guide-pull-request-et100%  e.md
    100%        New File                 174        C:\Git\azure-docs-pr\contributor-guide\create-images-markdown.md
    100%        New File                 197        C:\Git\azure-docs-pr\contributor-guide\create-links-markdown.md
    100%        New File                 184        C:\Git\azure-docs-pr\contributor-guide\create-tables-markdown.md
    100%        New File                 208        C:\Git\azure-docs-pr\contributor-guide\custom-markdown-extensions.md
    100%        New File                 210        C:\Git\azure-docs-pr\contributor-guide\file-names-and-locations.md
    100%        New File                 234        C:\Git\azure-docs-pr\contributor-guide\git-commands-for-master.md
    100%        New File                 186        C:\Git\azure-docs-pr\contributor-guide\release-branches.md
    100%        New File                 240        C:\Git\azure-docs-pr\contributor-guide\retire-or-rename-an-article.md
    100%        New File                 215        C:\Git\azure-docs-pr\contributor-guide\style-and-voice.md
    100%        New File                 212        C:\Git\azure-docs-pr\contributor-guide\syntax-highlighting-markdown.md
    100%        New File                 207        C:\Git\azure-docs-pr\contributor-guide\tools-and-setup.md
    ------------------------------------------------------------------------------
    
                   Total    Copied   Skipped  Mismatch    FAILED    Extras
        Dirs :         1         1         1         0         0         0
       Files :        17        17         0         0         0         0
       Bytes :     3.9 k     3.9 k         0         0         0         0
       Times :   0:00:05   0:00:00                       0:00:00   0:00:00
        
       Speed :                5620 Bytes/sec.
       Speed :               0.321 MegaBytes/min.
       Ended : Thursday, March 8, 2018 2:34:59 PM
        
    C:\Users>
    ```
 
    
7. <span data-ttu-id="3b151-172">Open the target folder to view and verify the copied files.</span><span class="sxs-lookup"><span data-stu-id="3b151-172">Open the target folder to view and verify the copied files.</span></span> <span data-ttu-id="3b151-173">If you have any errors during the copy process, download the log files for troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="3b151-173">If you have any errors during the copy process, download the log files for troubleshooting.</span></span> <span data-ttu-id="3b151-174">The log files are located as specified in the robobopy command.</span><span class="sxs-lookup"><span data-stu-id="3b151-174">The log files are located as specified in the robobopy command.</span></span>
 


> [!IMPORTANT]
> - <span data-ttu-id="3b151-175">It is your responsibility to ensure that you copy the data to folders that correspond to the appropriate data format.</span><span class="sxs-lookup"><span data-stu-id="3b151-175">It is your responsibility to ensure that you copy the data to folders that correspond to the appropriate data format.</span></span> <span data-ttu-id="3b151-176">For instance, copy the block blob data to the folder for block blobs.</span><span class="sxs-lookup"><span data-stu-id="3b151-176">For instance, copy the block blob data to the folder for block blobs.</span></span> <span data-ttu-id="3b151-177">If the data format does not match the appropriate folder (storage type), then at a later step, the data upload to Azure fails.</span><span class="sxs-lookup"><span data-stu-id="3b151-177">If the data format does not match the appropriate folder (storage type), then at a later step, the data upload to Azure fails.</span></span>
> -  <span data-ttu-id="3b151-178">While copying data, ensure that the data size conforms to the size limits described in the [Azure storage and Data Box Disk limits](data-box-disk-limits.md).</span><span class="sxs-lookup"><span data-stu-id="3b151-178">While copying data, ensure that the data size conforms to the size limits described in the [Azure storage and Data Box Disk limits](data-box-disk-limits.md).</span></span> 
> - <span data-ttu-id="3b151-179">If data, which is being uploaded by Data Box Disk, is concurrently uploaded by other applications outside of Data Box Disk, then this could result in upload job failures and data corruption.</span><span class="sxs-lookup"><span data-stu-id="3b151-179">If data, which is being uploaded by Data Box Disk, is concurrently uploaded by other applications outside of Data Box Disk, then this could result in upload job failures and data corruption.</span></span>

## <a name="verify-data-integrity"></a><span data-ttu-id="3b151-180">Verify data integrity</span><span class="sxs-lookup"><span data-stu-id="3b151-180">Verify data integrity</span></span>

<span data-ttu-id="3b151-181">To verify the data integrity, perform the following steps.</span><span class="sxs-lookup"><span data-stu-id="3b151-181">To verify the data integrity, perform the following steps.</span></span>

1. <span data-ttu-id="3b151-182">Run the `DataBoxDiskValidation.cmd` for checksum validation in the *AzureImportExport* folder of your drive.</span><span class="sxs-lookup"><span data-stu-id="3b151-182">Run the `DataBoxDiskValidation.cmd` for checksum validation in the *AzureImportExport* folder of your drive.</span></span> 
    
    ![Data Box Disk validation tool output](media/data-box-disk-deploy-copy-data/data-box-disk-validation-tool-output.png)

2. <span data-ttu-id="3b151-184">Choose the appropriate option.</span><span class="sxs-lookup"><span data-stu-id="3b151-184">Choose the appropriate option.</span></span> <span data-ttu-id="3b151-185">**We recommend that you always validate the files and generate checksums by selecting option 2**.</span><span class="sxs-lookup"><span data-stu-id="3b151-185">**We recommend that you always validate the files and generate checksums by selecting option 2**.</span></span> <span data-ttu-id="3b151-186">Depending upon your data size, this step may take a while.</span><span class="sxs-lookup"><span data-stu-id="3b151-186">Depending upon your data size, this step may take a while.</span></span> <span data-ttu-id="3b151-187">Once the script has completed, exit out of the command window.</span><span class="sxs-lookup"><span data-stu-id="3b151-187">Once the script has completed, exit out of the command window.</span></span> <span data-ttu-id="3b151-188">If there are any errors during validation and checksum generation, you are notified and a link to the error logs is also provided.</span><span class="sxs-lookup"><span data-stu-id="3b151-188">If there are any errors during validation and checksum generation, you are notified and a link to the error logs is also provided.</span></span>

    ![Checksum output](media/data-box-disk-deploy-copy-data/data-box-disk-checksum-output.png)

    > [!TIP]
    > - <span data-ttu-id="3b151-190">Reset the tool beween two runs.</span><span class="sxs-lookup"><span data-stu-id="3b151-190">Reset the tool beween two runs.</span></span>
    > - <span data-ttu-id="3b151-191">Use option 1 to validate the files only dealing with large data set containing small files (~KBs).</span><span class="sxs-lookup"><span data-stu-id="3b151-191">Use option 1 to validate the files only dealing with large data set containing small files (~KBs).</span></span> <span data-ttu-id="3b151-192">In these instances, checksum generation may take a very long time and the performance could be very slow.</span><span class="sxs-lookup"><span data-stu-id="3b151-192">In these instances, checksum generation may take a very long time and the performance could be very slow.</span></span>

3. <span data-ttu-id="3b151-193">If using multiple disks, run the command for each disk.</span><span class="sxs-lookup"><span data-stu-id="3b151-193">If using multiple disks, run the command for each disk.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b151-194">Next steps</span><span class="sxs-lookup"><span data-stu-id="3b151-194">Next steps</span></span>

<span data-ttu-id="3b151-195">In this tutorial, you learned about Azure Data Box Disk topics such as:</span><span class="sxs-lookup"><span data-stu-id="3b151-195">In this tutorial, you learned about Azure Data Box Disk topics such as:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3b151-196">Copy data to Data Box Disk</span><span class="sxs-lookup"><span data-stu-id="3b151-196">Copy data to Data Box Disk</span></span>
> * <span data-ttu-id="3b151-197">Verify data integrity</span><span class="sxs-lookup"><span data-stu-id="3b151-197">Verify data integrity</span></span>

<span data-ttu-id="3b151-198">Advance to the next tutorial to learn how to return the Data Box Disk and verify the data upload to Azure.</span><span class="sxs-lookup"><span data-stu-id="3b151-198">Advance to the next tutorial to learn how to return the Data Box Disk and verify the data upload to Azure.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3b151-199">Ship your Azure Data Box back to Microsoft</span><span class="sxs-lookup"><span data-stu-id="3b151-199">Ship your Azure Data Box back to Microsoft</span></span>](./data-box-disk-deploy-picked-up.md)

