---
title: How to use Azure Files with Linux | Microsoft Docs
description: Create an Azure file share in the cloud with this step-by-step tutorial. Manage your file share content, and mount a file share from an Azure virtual machine (VM) running Linux or an on-premises application that supports SMB 3.0.
services: storage
documentationcenter: na
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 6edc37ce-698f-4d50-8fc1-591ad456175d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/8/2017
ms.author: renash
ms.openlocfilehash: 201ceaec874c2367c232076faba25bdae128e7e1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563401"
---
# <a name="how-to-use-azure-file-storage-with-linux"></a><span data-ttu-id="bffa3-104">How to use Azure File Storage with Linux</span><span class="sxs-lookup"><span data-stu-id="bffa3-104">How to use Azure File Storage with Linux</span></span>
## <a name="overview"></a><span data-ttu-id="bffa3-105">Overview</span><span class="sxs-lookup"><span data-stu-id="bffa3-105">Overview</span></span>
<span data-ttu-id="bffa3-106">Azure File storage offers file shares in the cloud using the standard SMB protocol.</span><span class="sxs-lookup"><span data-stu-id="bffa3-106">Azure File storage offers file shares in the cloud using the standard SMB protocol.</span></span> <span data-ttu-id="bffa3-107">With Azure Files, you can migrate enterprise applications that rely on file servers to Azure.</span><span class="sxs-lookup"><span data-stu-id="bffa3-107">With Azure Files, you can migrate enterprise applications that rely on file servers to Azure.</span></span> <span data-ttu-id="bffa3-108">Applications running in Azure can easily mount file shares from Azure virtual machines running Linux.</span><span class="sxs-lookup"><span data-stu-id="bffa3-108">Applications running in Azure can easily mount file shares from Azure virtual machines running Linux.</span></span> <span data-ttu-id="bffa3-109">And with the latest release of File storage, you can also mount a file share from an on-premises application that supports SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="bffa3-109">And with the latest release of File storage, you can also mount a file share from an on-premises application that supports SMB 3.0.</span></span>

<span data-ttu-id="bffa3-110">You can create Azure file shares using the [Azure Portal](https://portal.azure.com), the Azure Storage PowerShell cmdlets, the Azure Storage client libraries, or the Azure Storage REST API.</span><span class="sxs-lookup"><span data-stu-id="bffa3-110">You can create Azure file shares using the [Azure Portal](https://portal.azure.com), the Azure Storage PowerShell cmdlets, the Azure Storage client libraries, or the Azure Storage REST API.</span></span> <span data-ttu-id="bffa3-111">Additionally, because file shares are SMB shares, you can access them via standard file system APIs.</span><span class="sxs-lookup"><span data-stu-id="bffa3-111">Additionally, because file shares are SMB shares, you can access them via standard file system APIs.</span></span>

<span data-ttu-id="bffa3-112">File storage is built on the same technology as Blob, Table, and Queue storage, so File storage offers the availability, durability, scalability, and geo-redundancy that is built into the Azure storage platform.</span><span class="sxs-lookup"><span data-stu-id="bffa3-112">File storage is built on the same technology as Blob, Table, and Queue storage, so File storage offers the availability, durability, scalability, and geo-redundancy that is built into the Azure storage platform.</span></span> <span data-ttu-id="bffa3-113">For details about File storage performance targets and limits, see [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md).</span><span class="sxs-lookup"><span data-stu-id="bffa3-113">For details about File storage performance targets and limits, see [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md).</span></span>

<span data-ttu-id="bffa3-114">File storage is now generally available and supports both SMB 2.1 and SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="bffa3-114">File storage is now generally available and supports both SMB 2.1 and SMB 3.0.</span></span> <span data-ttu-id="bffa3-115">For additional details on File storage, see the [File service REST API](https://msdn.microsoft.com/library/azure/dn167006.aspx).</span><span class="sxs-lookup"><span data-stu-id="bffa3-115">For additional details on File storage, see the [File service REST API](https://msdn.microsoft.com/library/azure/dn167006.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="bffa3-116">The Linux SMB client doesn't yet support encryption, so mounting a file share from Linux still requires that the client be in the same Azure region as the file share.</span><span class="sxs-lookup"><span data-stu-id="bffa3-116">The Linux SMB client doesn't yet support encryption, so mounting a file share from Linux still requires that the client be in the same Azure region as the file share.</span></span> <span data-ttu-id="bffa3-117">However, encryption support for Linux is on the roadmap of Linux developers responsible for SMB functionality.</span><span class="sxs-lookup"><span data-stu-id="bffa3-117">However, encryption support for Linux is on the roadmap of Linux developers responsible for SMB functionality.</span></span> <span data-ttu-id="bffa3-118">Linux distributions that support encryption in the future will be able to mount an Azure File share from anywhere as well.</span><span class="sxs-lookup"><span data-stu-id="bffa3-118">Linux distributions that support encryption in the future will be able to mount an Azure File share from anywhere as well.</span></span>
> 
> 

## <a name="video-using-azure-file-storage-with-linux"></a><span data-ttu-id="bffa3-119">Video: Using Azure File storage with Linux</span><span class="sxs-lookup"><span data-stu-id="bffa3-119">Video: Using Azure File storage with Linux</span></span>
<span data-ttu-id="bffa3-120">Here's a video that demonstrates how to create and use Azure File shares on Linux.</span><span class="sxs-lookup"><span data-stu-id="bffa3-120">Here's a video that demonstrates how to create and use Azure File shares on Linux.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-File-Storage-with-Linux/player]
> 
> 

## <a name="choose-a-linux-distribution-to-use"></a><span data-ttu-id="bffa3-121">Choose a Linux distribution to use</span><span class="sxs-lookup"><span data-stu-id="bffa3-121">Choose a Linux distribution to use</span></span>
<span data-ttu-id="bffa3-122">When creating a Linux virtual machine in Azure, you can specify a Linux image which supports SMB 2.1 or higher from the Azure image gallery.</span><span class="sxs-lookup"><span data-stu-id="bffa3-122">When creating a Linux virtual machine in Azure, you can specify a Linux image which supports SMB 2.1 or higher from the Azure image gallery.</span></span> <span data-ttu-id="bffa3-123">Below is a list of recommended Linux images:</span><span class="sxs-lookup"><span data-stu-id="bffa3-123">Below is a list of recommended Linux images:</span></span>

* <span data-ttu-id="bffa3-124">Ubuntu Server 14.04+</span><span class="sxs-lookup"><span data-stu-id="bffa3-124">Ubuntu Server 14.04+</span></span>
* <span data-ttu-id="bffa3-125">RHEL 7+</span><span class="sxs-lookup"><span data-stu-id="bffa3-125">RHEL 7+</span></span>
* <span data-ttu-id="bffa3-126">CentOS 7+</span><span class="sxs-lookup"><span data-stu-id="bffa3-126">CentOS 7+</span></span>
* <span data-ttu-id="bffa3-127">Debian 8</span><span class="sxs-lookup"><span data-stu-id="bffa3-127">Debian 8</span></span>
* <span data-ttu-id="bffa3-128">openSUSE 13.2+</span><span class="sxs-lookup"><span data-stu-id="bffa3-128">openSUSE 13.2+</span></span>
* <span data-ttu-id="bffa3-129">SUSE Linux Enterprise Server 12</span><span class="sxs-lookup"><span data-stu-id="bffa3-129">SUSE Linux Enterprise Server 12</span></span>
* <span data-ttu-id="bffa3-130">SUSE Linux Enterprise Server 12 (Premium Image)</span><span class="sxs-lookup"><span data-stu-id="bffa3-130">SUSE Linux Enterprise Server 12 (Premium Image)</span></span>

## <a name="mount-the-file-share"></a><span data-ttu-id="bffa3-131">Mount the file share</span><span class="sxs-lookup"><span data-stu-id="bffa3-131">Mount the file share</span></span>
<span data-ttu-id="bffa3-132">To mount the file share from a virtual machine running Linux, you may need to install an SMB/CIFS client if the distribution you are using doesn't have a built-in client.</span><span class="sxs-lookup"><span data-stu-id="bffa3-132">To mount the file share from a virtual machine running Linux, you may need to install an SMB/CIFS client if the distribution you are using doesn't have a built-in client.</span></span> <span data-ttu-id="bffa3-133">This is the command from Ubuntu to install one choice cifs-utils:</span><span class="sxs-lookup"><span data-stu-id="bffa3-133">This is the command from Ubuntu to install one choice cifs-utils:</span></span>

```
sudo apt-get install cifs-utils
```

<span data-ttu-id="bffa3-134">Next, you need to make a mount point (mkdir mymountpoint), and then issue the mount command that is similar to this:</span><span class="sxs-lookup"><span data-stu-id="bffa3-134">Next, you need to make a mount point (mkdir mymountpoint), and then issue the mount command that is similar to this:</span></span>

```
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename ./mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777,serverino
```

<span data-ttu-id="bffa3-135">You can also add settings in your /etc/fstab to mount the share.</span><span class="sxs-lookup"><span data-stu-id="bffa3-135">You can also add settings in your /etc/fstab to mount the share.</span></span>

<span data-ttu-id="bffa3-136">Note that 0777 here represent a directory/file permission code that gives execution/read/write permissions to all users.</span><span class="sxs-lookup"><span data-stu-id="bffa3-136">Note that 0777 here represent a directory/file permission code that gives execution/read/write permissions to all users.</span></span> <span data-ttu-id="bffa3-137">You can replace it with other file permission code following Linux file permission document.</span><span class="sxs-lookup"><span data-stu-id="bffa3-137">You can replace it with other file permission code following Linux file permission document.</span></span>

<span data-ttu-id="bffa3-138">Also to keep a file share mounted after reboot, you can add a setting like below in your /etc/fstab:</span><span class="sxs-lookup"><span data-stu-id="bffa3-138">Also to keep a file share mounted after reboot, you can add a setting like below in your /etc/fstab:</span></span>

```
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777,serverino
```

<span data-ttu-id="bffa3-139">For example, if you created a Azure VM using Linux image Ubuntu Server 15.04 (which is available from the Azure image gallery), you can mount the file as below:</span><span class="sxs-lookup"><span data-stu-id="bffa3-139">For example, if you created a Azure VM using Linux image Ubuntu Server 15.04 (which is available from the Azure image gallery), you can mount the file as below:</span></span>

```
azureuser@azureconubuntu:~$ sudo apt-get install cifs-utils
azureuser@azureconubuntu:~$ sudo mkdir /mnt/mountpoint
azureuser@azureconubuntu:~$ sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mnt/mountpoint -o vers=3.0,user=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777,serverino
azureuser@azureconubuntu:~$ df -h /mnt/mountpoint
Filesystem  Size  Used Avail Use% Mounted on
//myaccountname.file.core.windows.net/mysharename  5.0T   64K  5.0T   1% /mnt/mountpoint
```

<span data-ttu-id="bffa3-140">If you use CentOS 7.1, you can mount the file as below:</span><span class="sxs-lookup"><span data-stu-id="bffa3-140">If you use CentOS 7.1, you can mount the file as below:</span></span>

```
[azureuser@AzureconCent ~]$ sudo yum install samba-client samba-common cifs-utils
[azureuser@AzureconCent ~]$ sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mnt/mountpoint -o vers=3.0,user=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777,serverino
[azureuser@AzureconCent ~]$ df -h /mnt/mountpoint
Filesystem  Size  Used Avail Use% Mounted on
//myaccountname.file.core.windows.net/mysharename  5.0T   64K  5.0T   1% /mnt/mountpoint
```

<span data-ttu-id="bffa3-141">If you use Open SUSE 13.2, you can mount the file as below:</span><span class="sxs-lookup"><span data-stu-id="bffa3-141">If you use Open SUSE 13.2, you can mount the file as below:</span></span>

```
azureuser@AzureconSuse:~> sudo zypper install samba*  
azureuser@AzureconSuse:~> sudo mkdir /mnt/mountpoint
azureuser@AzureconSuse:~> sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mnt/mountpoint -o vers=3.0,user=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777,serverino
azureuser@AzureconSuse:~> df -h /mnt/mountpoint
Filesystem  Size  Used Avail Use% Mounted on
//myaccountname.file.core.windows.net/mysharename  5.0T   64K  5.0T   1% /mnt/mountpoint
```

<span data-ttu-id="bffa3-142">If you use RHEL 7.3, you can mount the file as below:</span><span class="sxs-lookup"><span data-stu-id="bffa3-142">If you use RHEL 7.3, you can mount the file as below:</span></span>

```
azureuser@AzureconRedhat:~> sudo yum install cifs-utils
azureuser@AzureconRedhat:~> sudo mkdir /mnt/mountpoint
azureuser@AzureconRedhat:~> sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mnt/mountpoint -o vers=3.0,user=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777,serverino
azureuser@AzureconRedhat:~> df -h /mnt/mountpoint
Filesystem  Size  Used Avail Use% Mounted on
//myaccountname.file.core.windows.net/mysharename  5.0T   64K  5.0T   1% /mnt/mountpoint
```

## <a name="manage-the-file-share"></a><span data-ttu-id="bffa3-143">Manage the file share</span><span class="sxs-lookup"><span data-stu-id="bffa3-143">Manage the file share</span></span>
<span data-ttu-id="bffa3-144">The [Azure Portal](https://portal.azure.com) provides a user interface for managing Azure File Storage.</span><span class="sxs-lookup"><span data-stu-id="bffa3-144">The [Azure Portal](https://portal.azure.com) provides a user interface for managing Azure File Storage.</span></span> <span data-ttu-id="bffa3-145">You can perform the following actions from your web browser:</span><span class="sxs-lookup"><span data-stu-id="bffa3-145">You can perform the following actions from your web browser:</span></span>

* <span data-ttu-id="bffa3-146">Upload and download files to and from your file share.</span><span class="sxs-lookup"><span data-stu-id="bffa3-146">Upload and download files to and from your file share.</span></span>
* <span data-ttu-id="bffa3-147">Monitor the actual usage of each file share.</span><span class="sxs-lookup"><span data-stu-id="bffa3-147">Monitor the actual usage of each file share.</span></span>
* <span data-ttu-id="bffa3-148">Adjust the file share size quota.</span><span class="sxs-lookup"><span data-stu-id="bffa3-148">Adjust the file share size quota.</span></span>
* <span data-ttu-id="bffa3-149">Copy the `net use` command to use to mount your file share from a Windows client.</span><span class="sxs-lookup"><span data-stu-id="bffa3-149">Copy the `net use` command to use to mount your file share from a Windows client.</span></span>

<span data-ttu-id="bffa3-150">You can also use the Azure Cross-Platform Command-Line Interface (Azure CLI) from Linux to manage the file share.</span><span class="sxs-lookup"><span data-stu-id="bffa3-150">You can also use the Azure Cross-Platform Command-Line Interface (Azure CLI) from Linux to manage the file share.</span></span> <span data-ttu-id="bffa3-151">Azure CLI provides a set of open source, cross-platform commands for you to work with Azure Storage, including File storage.</span><span class="sxs-lookup"><span data-stu-id="bffa3-151">Azure CLI provides a set of open source, cross-platform commands for you to work with Azure Storage, including File storage.</span></span> <span data-ttu-id="bffa3-152">It provides much of the same functionality found in the Azure Portal as well as rich data access functionality.</span><span class="sxs-lookup"><span data-stu-id="bffa3-152">It provides much of the same functionality found in the Azure Portal as well as rich data access functionality.</span></span> <span data-ttu-id="bffa3-153">For examples, see [Using the Azure CLI with Azure Storage](storage-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="bffa3-153">For examples, see [Using the Azure CLI with Azure Storage](storage-azure-cli.md).</span></span>

## <a name="develop-with-file-storage"></a><span data-ttu-id="bffa3-154">Develop with File storage</span><span class="sxs-lookup"><span data-stu-id="bffa3-154">Develop with File storage</span></span>
<span data-ttu-id="bffa3-155">As a developer, you can build an application with File storage by using the [Azure Storage Client Library for Java](https://github.com/azure/azure-storage-java).</span><span class="sxs-lookup"><span data-stu-id="bffa3-155">As a developer, you can build an application with File storage by using the [Azure Storage Client Library for Java](https://github.com/azure/azure-storage-java).</span></span> <span data-ttu-id="bffa3-156">For code examples, see [How to use File storage from Java](storage-java-how-to-use-file-storage.md).</span><span class="sxs-lookup"><span data-stu-id="bffa3-156">For code examples, see [How to use File storage from Java](storage-java-how-to-use-file-storage.md).</span></span>

<span data-ttu-id="bffa3-157">You can also use the [Azure Storage Client Library for Node.js](https://github.com/Azure/azure-storage-node) to develop against File storage.</span><span class="sxs-lookup"><span data-stu-id="bffa3-157">You can also use the [Azure Storage Client Library for Node.js](https://github.com/Azure/azure-storage-node) to develop against File storage.</span></span>

## <a name="feedback-and-more-information"></a><span data-ttu-id="bffa3-158">Feedback and more information</span><span class="sxs-lookup"><span data-stu-id="bffa3-158">Feedback and more information</span></span>
<span data-ttu-id="bffa3-159">Linux users, we want to hear from you!</span><span class="sxs-lookup"><span data-stu-id="bffa3-159">Linux users, we want to hear from you!</span></span>

<span data-ttu-id="bffa3-160">The Azure File storage for Linux users' group provides a forum for you to share feedback as you evaluate and adopt File storage on Linux.</span><span class="sxs-lookup"><span data-stu-id="bffa3-160">The Azure File storage for Linux users' group provides a forum for you to share feedback as you evaluate and adopt File storage on Linux.</span></span> <span data-ttu-id="bffa3-161">Email [Azure File Storage Linux Users](mailto:azurefileslinuxusers@microsoft.com) to join the users' group.</span><span class="sxs-lookup"><span data-stu-id="bffa3-161">Email [Azure File Storage Linux Users](mailto:azurefileslinuxusers@microsoft.com) to join the users' group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bffa3-162">Next steps</span><span class="sxs-lookup"><span data-stu-id="bffa3-162">Next steps</span></span>
<span data-ttu-id="bffa3-163">See these links for more information about Azure File storage.</span><span class="sxs-lookup"><span data-stu-id="bffa3-163">See these links for more information about Azure File storage.</span></span>

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="bffa3-164">Conceptual articles and videos</span><span class="sxs-lookup"><span data-stu-id="bffa3-164">Conceptual articles and videos</span></span>
* [<span data-ttu-id="bffa3-165">Azure Files Storage: a frictionless cloud SMB file system for Windows and Linux</span><span class="sxs-lookup"><span data-stu-id="bffa3-165">Azure Files Storage: a frictionless cloud SMB file system for Windows and Linux</span></span>](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [<span data-ttu-id="bffa3-166">Get started with Azure File storage on Windows</span><span class="sxs-lookup"><span data-stu-id="bffa3-166">Get started with Azure File storage on Windows</span></span>](storage-dotnet-how-to-use-files.md)

### <a name="tooling-support-for-file-storage"></a><span data-ttu-id="bffa3-167">Tooling support for File storage</span><span class="sxs-lookup"><span data-stu-id="bffa3-167">Tooling support for File storage</span></span>
* [<span data-ttu-id="bffa3-168">Transfer data with the AzCopy Command-Line Utility</span><span class="sxs-lookup"><span data-stu-id="bffa3-168">Transfer data with the AzCopy Command-Line Utility</span></span>](storage-use-azcopy.md)
* <span data-ttu-id="bffa3-169">[Create and manage file shares](storage-azure-cli.md#create-and-manage-file-shares) using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="bffa3-169">[Create and manage file shares](storage-azure-cli.md#create-and-manage-file-shares) using the Azure CLI</span></span>

### <a name="reference"></a><span data-ttu-id="bffa3-170">Reference</span><span class="sxs-lookup"><span data-stu-id="bffa3-170">Reference</span></span>
* [<span data-ttu-id="bffa3-171">File Service REST API reference</span><span class="sxs-lookup"><span data-stu-id="bffa3-171">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
* [<span data-ttu-id="bffa3-172">Azure Files Troubleshooting Article</span><span class="sxs-lookup"><span data-stu-id="bffa3-172">Azure Files Troubleshooting Article</span></span>](storage-troubleshoot-file-connection-problems.md)

### <a name="blog-posts"></a><span data-ttu-id="bffa3-173">Blog posts</span><span class="sxs-lookup"><span data-stu-id="bffa3-173">Blog posts</span></span>
* [<span data-ttu-id="bffa3-174">Azure File storage is now generally available</span><span class="sxs-lookup"><span data-stu-id="bffa3-174">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [<span data-ttu-id="bffa3-175">Inside Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="bffa3-175">Inside Azure File Storage</span></span>](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [<span data-ttu-id="bffa3-176">Introducing Microsoft Azure File Service</span><span class="sxs-lookup"><span data-stu-id="bffa3-176">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [<span data-ttu-id="bffa3-177">Persisting connections to Microsoft Azure Files</span><span class="sxs-lookup"><span data-stu-id="bffa3-177">Persisting connections to Microsoft Azure Files</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx)
