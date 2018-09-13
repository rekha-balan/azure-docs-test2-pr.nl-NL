---
title: Set up Microsoft Azure Data Box Disk| Microsoft Docs
description: Use this tutorial to learn how to set up your Azure Data Box Disk
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
ms.openlocfilehash: 89b83e07477dbf2d6ca53bed8b0fd50b21e30a8a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869451"
---
# <a name="tutorial-unpack-connect-and-unlock-azure-data-box-disk"></a><span data-ttu-id="ae154-103">Tutorial: Unpack, connect, and unlock Azure Data Box Disk</span><span class="sxs-lookup"><span data-stu-id="ae154-103">Tutorial: Unpack, connect, and unlock Azure Data Box Disk</span></span>

<span data-ttu-id="ae154-104">This tutorial describes how to unpack, connect, and unlock your Azure Data Box Disk.</span><span class="sxs-lookup"><span data-stu-id="ae154-104">This tutorial describes how to unpack, connect, and unlock your Azure Data Box Disk.</span></span>

<span data-ttu-id="ae154-105">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="ae154-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ae154-106">Unpack your Data Box Disk</span><span class="sxs-lookup"><span data-stu-id="ae154-106">Unpack your Data Box Disk</span></span>
> * <span data-ttu-id="ae154-107">Connect to disks and get the passkey</span><span class="sxs-lookup"><span data-stu-id="ae154-107">Connect to disks and get the passkey</span></span>
> * <span data-ttu-id="ae154-108">Unlock disks on Windows client</span><span class="sxs-lookup"><span data-stu-id="ae154-108">Unlock disks on Windows client</span></span>
> * <span data-ttu-id="ae154-109">Unlock disks on Linux client</span><span class="sxs-lookup"><span data-stu-id="ae154-109">Unlock disks on Linux client</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae154-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ae154-110">Prerequisites</span></span>

<span data-ttu-id="ae154-111">Before you begin, make sure that:</span><span class="sxs-lookup"><span data-stu-id="ae154-111">Before you begin, make sure that:</span></span>

1. <span data-ttu-id="ae154-112">You have completed the [Tutorial: Order Azure Data Box Disk](data-box-disk-deploy-ordered.md).</span><span class="sxs-lookup"><span data-stu-id="ae154-112">You have completed the [Tutorial: Order Azure Data Box Disk](data-box-disk-deploy-ordered.md).</span></span>
2. <span data-ttu-id="ae154-113">You have received your disks and the job status in the portal is updated to **Delivered**.</span><span class="sxs-lookup"><span data-stu-id="ae154-113">You have received your disks and the job status in the portal is updated to **Delivered**.</span></span>
3. <span data-ttu-id="ae154-114">You have a client computer on which you can install the Data Box Disk unlock tool.</span><span class="sxs-lookup"><span data-stu-id="ae154-114">You have a client computer on which you can install the Data Box Disk unlock tool.</span></span> <span data-ttu-id="ae154-115">Your client computer must:</span><span class="sxs-lookup"><span data-stu-id="ae154-115">Your client computer must:</span></span>
    - <span data-ttu-id="ae154-116">Run a [Supported operating system](data-box-disk-system-requirements.md#supported-operating-systems-for-clients).</span><span class="sxs-lookup"><span data-stu-id="ae154-116">Run a [Supported operating system](data-box-disk-system-requirements.md#supported-operating-systems-for-clients).</span></span>
    - <span data-ttu-id="ae154-117">Have other [required software](data-box-disk-system-requirements.md#other-required-software-for-windows-clients) installed if it is a Windows client.</span><span class="sxs-lookup"><span data-stu-id="ae154-117">Have other [required software](data-box-disk-system-requirements.md#other-required-software-for-windows-clients) installed if it is a Windows client.</span></span>  

## <a name="unpack-your-disks"></a><span data-ttu-id="ae154-118">Unpack your disks</span><span class="sxs-lookup"><span data-stu-id="ae154-118">Unpack your disks</span></span>

 <span data-ttu-id="ae154-119">Perform the following steps to unpack your disks.</span><span class="sxs-lookup"><span data-stu-id="ae154-119">Perform the following steps to unpack your disks.</span></span>

1. <span data-ttu-id="ae154-120">The Data Box Disks are mailed in a small shipping Box.</span><span class="sxs-lookup"><span data-stu-id="ae154-120">The Data Box Disks are mailed in a small shipping Box.</span></span> <span data-ttu-id="ae154-121">Open the box and remove its contents.</span><span class="sxs-lookup"><span data-stu-id="ae154-121">Open the box and remove its contents.</span></span> <span data-ttu-id="ae154-122">Check that the box has 1 to 5 solid-state disks (SSDs) and a USB connecting cable per disk.</span><span class="sxs-lookup"><span data-stu-id="ae154-122">Check that the box has 1 to 5 solid-state disks (SSDs) and a USB connecting cable per disk.</span></span> <span data-ttu-id="ae154-123">Inspect the box for any evidence of tampering, or any other obvious damage.</span><span class="sxs-lookup"><span data-stu-id="ae154-123">Inspect the box for any evidence of tampering, or any other obvious damage.</span></span> 

    ![Data Box Disk shipping package](media/data-box-disk-deploy-set-up/data-box-disk-ship-package1.png)

2. <span data-ttu-id="ae154-125">If the shipping box is tampered or severely damaged, do not open the box.</span><span class="sxs-lookup"><span data-stu-id="ae154-125">If the shipping box is tampered or severely damaged, do not open the box.</span></span> <span data-ttu-id="ae154-126">Contact Microsoft Support to help you assess whether the disks are in good working order and if they need to ship you a replacement.</span><span class="sxs-lookup"><span data-stu-id="ae154-126">Contact Microsoft Support to help you assess whether the disks are in good working order and if they need to ship you a replacement.</span></span>
3. <span data-ttu-id="ae154-127">Verify that the box has a clear sleeve containing a shipping label (under the current label) for return shipment.</span><span class="sxs-lookup"><span data-stu-id="ae154-127">Verify that the box has a clear sleeve containing a shipping label (under the current label) for return shipment.</span></span> <span data-ttu-id="ae154-128">If this label is lost or damaged, you can always download and print a new one from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ae154-128">If this label is lost or damaged, you can always download and print a new one from the Azure portal.</span></span> 

    ![Data Box Disk shipping label](media/data-box-disk-deploy-set-up/data-box-disk-package-ship-label.png)

4. <span data-ttu-id="ae154-130">Save the box and packaging foam for return shipment of the disks.</span><span class="sxs-lookup"><span data-stu-id="ae154-130">Save the box and packaging foam for return shipment of the disks.</span></span>

## <a name="connect-to-disks-and-get-the-passkey"></a><span data-ttu-id="ae154-131">Connect to disks and get the passkey</span><span class="sxs-lookup"><span data-stu-id="ae154-131">Connect to disks and get the passkey</span></span> 

1. <span data-ttu-id="ae154-132">Use the included cable to connect the disk to the client computer running a supported OS as stated in the prerequisites.</span><span class="sxs-lookup"><span data-stu-id="ae154-132">Use the included cable to connect the disk to the client computer running a supported OS as stated in the prerequisites.</span></span> 

    ![Data Box Disk connect](media/data-box-disk-deploy-set-up/data-box-disk-connect-unlock.png)    
    
2. <span data-ttu-id="ae154-134">In the Azure portal, go to **General > Device details**.</span><span class="sxs-lookup"><span data-stu-id="ae154-134">In the Azure portal, go to **General > Device details**.</span></span> <span data-ttu-id="ae154-135">Use the copy icon to copy the passkey.</span><span class="sxs-lookup"><span data-stu-id="ae154-135">Use the copy icon to copy the passkey.</span></span> <span data-ttu-id="ae154-136">This passkey will be used to unlock the disks.</span><span class="sxs-lookup"><span data-stu-id="ae154-136">This passkey will be used to unlock the disks.</span></span>

    ![Data Box Disk unlock passkey](media/data-box-disk-deploy-set-up/data-box-disk-get-passkey.png) 

<span data-ttu-id="ae154-138">Depending on whether you are connected to a Windows or Linux client, the steps to unlock the disks are different.</span><span class="sxs-lookup"><span data-stu-id="ae154-138">Depending on whether you are connected to a Windows or Linux client, the steps to unlock the disks are different.</span></span>

## <a name="unlock-disks-on-windows-client"></a><span data-ttu-id="ae154-139">Unlock disks on Windows client</span><span class="sxs-lookup"><span data-stu-id="ae154-139">Unlock disks on Windows client</span></span>

<span data-ttu-id="ae154-140">Perform the following steps to connect and unlock your disks.</span><span class="sxs-lookup"><span data-stu-id="ae154-140">Perform the following steps to connect and unlock your disks.</span></span>
     
1. <span data-ttu-id="ae154-141">In the Azure portal, go to **General > Device details**.</span><span class="sxs-lookup"><span data-stu-id="ae154-141">In the Azure portal, go to **General > Device details**.</span></span> 
2. <span data-ttu-id="ae154-142">Download the Data Box Disk toolset corresponding to the Windows client.</span><span class="sxs-lookup"><span data-stu-id="ae154-142">Download the Data Box Disk toolset corresponding to the Windows client.</span></span> 

    > [!div class="nextstepaction"]
    > [<span data-ttu-id="ae154-143">Download Data Box Disk toolset for Windows</span><span class="sxs-lookup"><span data-stu-id="ae154-143">Download Data Box Disk toolset for Windows</span></span>](http://aka.ms/databoxdisktoolswin)         

3. <span data-ttu-id="ae154-144">Extract the tool on the same computer that you will use to copy the data.</span><span class="sxs-lookup"><span data-stu-id="ae154-144">Extract the tool on the same computer that you will use to copy the data.</span></span>
4. <span data-ttu-id="ae154-145">Open a Command Prompt window or run Windows PowerShell as administrator on the same computer.</span><span class="sxs-lookup"><span data-stu-id="ae154-145">Open a Command Prompt window or run Windows PowerShell as administrator on the same computer.</span></span>
5. <span data-ttu-id="ae154-146">(Optional) To verify the computer that you are using to unlock the disk meets the operating system requirements, run the system check command.</span><span class="sxs-lookup"><span data-stu-id="ae154-146">(Optional) To verify the computer that you are using to unlock the disk meets the operating system requirements, run the system check command.</span></span> <span data-ttu-id="ae154-147">A sample output is shown below.</span><span class="sxs-lookup"><span data-stu-id="ae154-147">A sample output is shown below.</span></span> 

    ```powershell
    Windows PowerShell
    Copyright (C) Microsoft Corporation. All rights reserved.
    
    PS C:\DataBoxDiskUnlockTool\DiskUnlock> .\DataBoxDiskUnlock.exe /SystemCheck
    Successfully verified that the system can run the tool.
    PS C:\DataBoxDiskUnlockTool\DiskUnlock>
    ``` 

6. <span data-ttu-id="ae154-148">Run `DataBoxDiskUnlock.exe` and supply the passkey you obtained in [Connect to disks and get the passkey](#Connect-to-disks-and-get-the-passkey).</span><span class="sxs-lookup"><span data-stu-id="ae154-148">Run `DataBoxDiskUnlock.exe` and supply the passkey you obtained in [Connect to disks and get the passkey](#Connect-to-disks-and-get-the-passkey).</span></span> <span data-ttu-id="ae154-149">The drive letter assigned to the disk is displayed.</span><span class="sxs-lookup"><span data-stu-id="ae154-149">The drive letter assigned to the disk is displayed.</span></span> <span data-ttu-id="ae154-150">A sample output is shown below.</span><span class="sxs-lookup"><span data-stu-id="ae154-150">A sample output is shown below.</span></span>

    ```powershell
    PS C:\WINDOWS\system32> cd C:\DataBoxDiskUnlockTool\DiskUnlock
    PS C:\DataBoxDiskUnlockTool\DiskUnlock> .\DataBoxDiskUnlock.exe
    Enter the passkey :
    testpasskey1
    
    Following volumes are unlocked and verified.
    Volume drive letters: D:
    
    PS C:\DataBoxDiskUnlockTool\DiskUnlock>
    ```

7. <span data-ttu-id="ae154-151">Repeat the unlock steps for any future disk reinserts.</span><span class="sxs-lookup"><span data-stu-id="ae154-151">Repeat the unlock steps for any future disk reinserts.</span></span> <span data-ttu-id="ae154-152">Use the `help` command if you need help with the Data Box Disk unlock tool.</span><span class="sxs-lookup"><span data-stu-id="ae154-152">Use the `help` command if you need help with the Data Box Disk unlock tool.</span></span>   

    ```powershell
    PS C:\DataBoxDiskUnlockTool\DiskUnlock> .\DataBoxDiskUnlock.exe /help
    USAGE:
    DataBoxUnlock /PassKey:<passkey_from_Azure_portal>
    
    Example: DataBoxUnlock /PassKey:<your passkey>
    Example: DataBoxUnlock /SystemCheck
    Example: DataBoxUnlock /Help
    
    /PassKey:        Get this passkey from Azure DataBox Disk order. The passkey unlocks your disks.
    /SystemCheck:    This option checks if your system meets the requirements to run the tool.
    /Help:           This option provides help on cmdlet usage and examples.
    
    PS C:\DataBoxDiskUnlockTool\DiskUnlock>
    ```  
8. <span data-ttu-id="ae154-153">Once the disk is unlocked, you can view the contents of the disk.</span><span class="sxs-lookup"><span data-stu-id="ae154-153">Once the disk is unlocked, you can view the contents of the disk.</span></span>    

    ![Data Box Disk contents](media/data-box-disk-deploy-set-up/data-box-disk-content.png) 

## <a name="unlock-disks-on-linux-client"></a><span data-ttu-id="ae154-155">Unlock disks on Linux client</span><span class="sxs-lookup"><span data-stu-id="ae154-155">Unlock disks on Linux client</span></span>

1. <span data-ttu-id="ae154-156">In the Azure portal, go to **General > Device details**.</span><span class="sxs-lookup"><span data-stu-id="ae154-156">In the Azure portal, go to **General > Device details**.</span></span> 
2. <span data-ttu-id="ae154-157">Download the Data Box Disk toolset corresponding to the Linux client.</span><span class="sxs-lookup"><span data-stu-id="ae154-157">Download the Data Box Disk toolset corresponding to the Linux client.</span></span>  

    > [!div class="nextstepaction"]
    > [<span data-ttu-id="ae154-158">Download Data Box Disk toolset for Linux</span><span class="sxs-lookup"><span data-stu-id="ae154-158">Download Data Box Disk toolset for Linux</span></span>](http://aka.ms/databoxdisktoolslinux) 

3. <span data-ttu-id="ae154-159">On your Linux client, open a terminal.</span><span class="sxs-lookup"><span data-stu-id="ae154-159">On your Linux client, open a terminal.</span></span> <span data-ttu-id="ae154-160">Navigate to the folder where you downloaded the software.</span><span class="sxs-lookup"><span data-stu-id="ae154-160">Navigate to the folder where you downloaded the software.</span></span> <span data-ttu-id="ae154-161">Change the file permissions so that you can execute these files.</span><span class="sxs-lookup"><span data-stu-id="ae154-161">Change the file permissions so that you can execute these files.</span></span> <span data-ttu-id="ae154-162">Type the following command:</span><span class="sxs-lookup"><span data-stu-id="ae154-162">Type the following command:</span></span> 

    `chmod +x DataBoxDiskUnlock_x86_64` 
    
    `chmod +x DataBoxDiskUnlock_Prep.sh` 
 
    <span data-ttu-id="ae154-163">A sample output is shown below.</span><span class="sxs-lookup"><span data-stu-id="ae154-163">A sample output is shown below.</span></span> <span data-ttu-id="ae154-164">Once the chmod command is run, you can verify that the file permissions are changed by running the `ls` command.</span><span class="sxs-lookup"><span data-stu-id="ae154-164">Once the chmod command is run, you can verify that the file permissions are changed by running the `ls` command.</span></span> 
 
    ```
        [user@localhost Downloads]$ chmod +x DataBoxDiskUnlock_x86_64  
        [user@localhost Downloads]$ chmod +x DataBoxDiskUnlock_Prep.sh   
        [user@localhost Downloads]$ ls -l  
        -rwxrwxr-x. 1 user user 1152664 Aug 10 17:26 DataBoxDiskUnlock_x86_64  
        -rwxrwxr-x. 1 user user 795 Aug 5 23:26 DataBoxDiskUnlock_Prep.sh
    ```
4. <span data-ttu-id="ae154-165">Execute the script so that it installs all the binaries needed for the Data Box Disk Unlock software.</span><span class="sxs-lookup"><span data-stu-id="ae154-165">Execute the script so that it installs all the binaries needed for the Data Box Disk Unlock software.</span></span> <span data-ttu-id="ae154-166">Use `sudo` to run the command as root.</span><span class="sxs-lookup"><span data-stu-id="ae154-166">Use `sudo` to run the command as root.</span></span> <span data-ttu-id="ae154-167">Once the binaries are successfully installed, you will see a note to that effect on the terminal.</span><span class="sxs-lookup"><span data-stu-id="ae154-167">Once the binaries are successfully installed, you will see a note to that effect on the terminal.</span></span>

    `sudo ./DataBoxDiskUnlock_Prep.sh`

    <span data-ttu-id="ae154-168">The script will first check whether your client computer is running a supported operating system.</span><span class="sxs-lookup"><span data-stu-id="ae154-168">The script will first check whether your client computer is running a supported operating system.</span></span> <span data-ttu-id="ae154-169">A sample output is shown below.</span><span class="sxs-lookup"><span data-stu-id="ae154-169">A sample output is shown below.</span></span> 
 
    ```
    [user@localhost Documents]$ sudo ./DataBoxDiskUnlock_Prep.sh 
        OS = CentOS Version = 6.9 
        Release = CentOS release 6.9 (Final) 
        Architecture = x64 
    
        The script will install the following packages and dependencies. 
        epel-release 
        dislocker 
        ntfs-3g 
        fuse-dislocker 
        Do you wish to continue? y|n :|
    ```
    
 
5. <span data-ttu-id="ae154-170">Type `y` to continue the install.</span><span class="sxs-lookup"><span data-stu-id="ae154-170">Type `y` to continue the install.</span></span> <span data-ttu-id="ae154-171">The packages that the script installs are:</span><span class="sxs-lookup"><span data-stu-id="ae154-171">The packages that the script installs are:</span></span> 
    - <span data-ttu-id="ae154-172">**epel-release** - Repository that contains the following three packages.</span><span class="sxs-lookup"><span data-stu-id="ae154-172">**epel-release** - Repository that contains the following three packages.</span></span> 
    - <span data-ttu-id="ae154-173">**dislocker and fuse-dislocker** - This utility helps decrypting BitLocker encrypted disks.</span><span class="sxs-lookup"><span data-stu-id="ae154-173">**dislocker and fuse-dislocker** - This utility helps decrypting BitLocker encrypted disks.</span></span> 
    - <span data-ttu-id="ae154-174">**ntfs-3g** - Package that helps mount NTFS volumes.</span><span class="sxs-lookup"><span data-stu-id="ae154-174">**ntfs-3g** - Package that helps mount NTFS volumes.</span></span> 
 
    <span data-ttu-id="ae154-175">Once the packages are successfully installed, the terminal will display a notification to that effect.</span><span class="sxs-lookup"><span data-stu-id="ae154-175">Once the packages are successfully installed, the terminal will display a notification to that effect.</span></span>     
    ```
    Dependency Installed: compat-readline5.x86 64 0:5.2-17.I.el6 dislocker-libs.x86 64 0:0.7.1-8.el6 mbedtls.x86 64 0:2.7.4-l.el6        ruby.x86 64 0:1.8.7.374-5.el6 
    ruby-libs.x86 64 0:1.8.7.374-5.el6 
    Complete! 
    Loaded plugins: fastestmirror, refresh-packagekit, security 
    Setting up Remove Process 
    Resolving Dependencies 
    --> Running transaction check 
    ---> Package epel-release.noarch 0:6-8 will be erased --> Finished Dependency Resolution 
    Dependencies Resolved 
    Package        Architecture        Version        Repository        Size 
    Removing:  epel-release        noarch         6-8        @extras        22 k 
    Transaction Summary                                 
    Remove        1 Package(s) 
    Installed size: 22 k 
    Downloading Packages: 
    Running rpmcheckdebug 
    Running Transaction Test 
    Transaction Test Succeeded 
    Running Transaction 
    Erasing : epel-release-6-8.noarch 
    Verifying : epel-release-6-8.noarch 
    Removed: 
    epel-release.noarch 0:6-8 
    Complete! 
    Dislocker is installed by the script. 
    OpenSSL is already installed.
    ```

6. <span data-ttu-id="ae154-176">Run the Data Box Disk Unlock tool.</span><span class="sxs-lookup"><span data-stu-id="ae154-176">Run the Data Box Disk Unlock tool.</span></span> <span data-ttu-id="ae154-177">Supply the passkey from the Azure portal you obtained in [Connect to disks and get the passkey](#Connect-to-disks-and-get-the-passkey).</span><span class="sxs-lookup"><span data-stu-id="ae154-177">Supply the passkey from the Azure portal you obtained in [Connect to disks and get the passkey](#Connect-to-disks-and-get-the-passkey).</span></span> <span data-ttu-id="ae154-178">Optionally specify a list of BitLocker encrypted volumes to unlock.</span><span class="sxs-lookup"><span data-stu-id="ae154-178">Optionally specify a list of BitLocker encrypted volumes to unlock.</span></span> <span data-ttu-id="ae154-179">The passkey and volume list should be specified within single quotes.</span><span class="sxs-lookup"><span data-stu-id="ae154-179">The passkey and volume list should be specified within single quotes.</span></span> 

    <span data-ttu-id="ae154-180">Type the following command.</span><span class="sxs-lookup"><span data-stu-id="ae154-180">Type the following command.</span></span>
 
    `sudo ./DataBoxDiskUnlock_x86_64 /PassKey:’<Your passkey from Azure portal>’ /Volumes:’<list of volumes>’`         

    <span data-ttu-id="ae154-181">The sample output is shown below.</span><span class="sxs-lookup"><span data-stu-id="ae154-181">The sample output is shown below.</span></span> 
 
    ```
    [user@localhost Downloads]$ sudo ./DataBoxDiskUnlock_x86_64 /Passkey:’qwerqwerqwer’ /Volumes:’/dev/sdbl’ 
    
    START: Mon Aug 13 14:25:49 2018 
    Volumes: /dev/sdbl 
    Passkey: qwerqwerqwer 
    
    Volumes for data copy : 
    /dev/sdbl: /mnt/DataBoxDisk/mountVoll/ 
    END: Mon Aug 13 14:26:02 2018
    ```
    <span data-ttu-id="ae154-182">The mount point for the volume that you can copy your data to is displayed.</span><span class="sxs-lookup"><span data-stu-id="ae154-182">The mount point for the volume that you can copy your data to is displayed.</span></span>

7. <span data-ttu-id="ae154-183">Repeat unlock steps for any future disk reinserts.</span><span class="sxs-lookup"><span data-stu-id="ae154-183">Repeat unlock steps for any future disk reinserts.</span></span> <span data-ttu-id="ae154-184">Use the `help` command if you need help with the Data Box Disk unlock tool.</span><span class="sxs-lookup"><span data-stu-id="ae154-184">Use the `help` command if you need help with the Data Box Disk unlock tool.</span></span> 
    
    `sudo ./DataBoxDiskUnlock_x86_64 /Help` 

    <span data-ttu-id="ae154-185">The sample output is shown below.</span><span class="sxs-lookup"><span data-stu-id="ae154-185">The sample output is shown below.</span></span> 
 
    ```
    [user@localhost Downloads]$ sudo ./DataBoxDiskUnlock_x86_64 /Help  
    START: Mon Aug 13 14:29:20 2018 
    USAGE: 
    sudo DataBoxDiskUnlock /PassKey:’<passkey from Azure_portal>’ 
    
    Example: sudo DataBoxDiskUnlock /PassKey:’passkey’ 
    Example: sudo DataBoxDiskUnlock /PassKey:’passkey’ /Volumes:’/dev/sdbl’ 
    Example: sudo DataBoxDiskUnlock /Help Example: sudo DataBoxDiskUnlock /Clean 
    
    /PassKey: This option takes a passkey as input and unlocks all of your disks. 
    Get the passkey from your Data Box Disk order in Azure portal. 
    /Volumes: This option is used to input a list of BitLocker encrypted volumes. 
    /Help: This option provides help on the tool usage and examples. 
    /Unmount: This option unmounts all the volumes mounted by this tool. 
   
    END: Mon Aug 13 14:29:20 2018 [user@localhost Downloads]$
    ```
    
8. <span data-ttu-id="ae154-186">Once the disk is unlocked, you can go to the mount point and view the contents of the disk.</span><span class="sxs-lookup"><span data-stu-id="ae154-186">Once the disk is unlocked, you can go to the mount point and view the contents of the disk.</span></span> <span data-ttu-id="ae154-187">You are now ready to copy the data to *BlockBlob* or *PageBlob* folders.</span><span class="sxs-lookup"><span data-stu-id="ae154-187">You are now ready to copy the data to *BlockBlob* or *PageBlob* folders.</span></span> 

    ![Data Box Disk contents](media/data-box-disk-deploy-set-up/data-box-disk-content-linux.png)

## <a name="next-steps"></a><span data-ttu-id="ae154-189">Next steps</span><span class="sxs-lookup"><span data-stu-id="ae154-189">Next steps</span></span>

<span data-ttu-id="ae154-190">In this tutorial, you learned about Azure Data Box Disk topics such as:</span><span class="sxs-lookup"><span data-stu-id="ae154-190">In this tutorial, you learned about Azure Data Box Disk topics such as:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ae154-191">Unpack your Data Box Disk</span><span class="sxs-lookup"><span data-stu-id="ae154-191">Unpack your Data Box Disk</span></span>
> * <span data-ttu-id="ae154-192">Connect to disks and get the passkey</span><span class="sxs-lookup"><span data-stu-id="ae154-192">Connect to disks and get the passkey</span></span>
> * <span data-ttu-id="ae154-193">Unlock disks on Windows client</span><span class="sxs-lookup"><span data-stu-id="ae154-193">Unlock disks on Windows client</span></span>
> * <span data-ttu-id="ae154-194">Unlock disks on Linux client</span><span class="sxs-lookup"><span data-stu-id="ae154-194">Unlock disks on Linux client</span></span>


<span data-ttu-id="ae154-195">Advance to the next tutorial to learn how to copy data on your Data Box Disk.</span><span class="sxs-lookup"><span data-stu-id="ae154-195">Advance to the next tutorial to learn how to copy data on your Data Box Disk.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ae154-196">Copy data on your Data Box Disk</span><span class="sxs-lookup"><span data-stu-id="ae154-196">Copy data on your Data Box Disk</span></span>](./data-box-disk-deploy-copy-data.md)

