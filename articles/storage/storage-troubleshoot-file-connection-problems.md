---
title: Troubleshooting Azure File storage issues | Microsoft Docs
description: Troubleshooting Azure File storage issues
services: storage
documentationcenter: ''
author: genlin
manager: felixwu
editor: na
tags: storage
ms.assetid: fbc5f600-131e-4b99-828a-42d0de85fff7
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: genli
ms.openlocfilehash: c62f8d077906ce8ad1b5501864a21ee369b2314a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549751"
---
# <a name="troubleshooting-azure-file-storage-problems"></a><span data-ttu-id="f9018-103">Troubleshooting Azure File storage problems</span><span class="sxs-lookup"><span data-stu-id="f9018-103">Troubleshooting Azure File storage problems</span></span>
<span data-ttu-id="f9018-104">This article lists common problems that are related to Microsoft Azure File storage when you connect from Windows and Linux clients.</span><span class="sxs-lookup"><span data-stu-id="f9018-104">This article lists common problems that are related to Microsoft Azure File storage when you connect from Windows and Linux clients.</span></span> <span data-ttu-id="f9018-105">It also provides the possible causes of and resolutions for these problems.</span><span class="sxs-lookup"><span data-stu-id="f9018-105">It also provides the possible causes of and resolutions for these problems.</span></span>

<span data-ttu-id="f9018-106">**General problems (occur in both Windows and Linux clients)**</span><span class="sxs-lookup"><span data-stu-id="f9018-106">**General problems (occur in both Windows and Linux clients)**</span></span>

* [<span data-ttu-id="f9018-107">Quota error when trying to open a file</span><span class="sxs-lookup"><span data-stu-id="f9018-107">Quota error when trying to open a file</span></span>](#quotaerror)
* [<span data-ttu-id="f9018-108">Slow performance when you access Azure File storage from Windows or from Linux</span><span class="sxs-lookup"><span data-stu-id="f9018-108">Slow performance when you access Azure File storage from Windows or from Linux</span></span>](#slowboth)
* [<span data-ttu-id="f9018-109">How to trace the read and write operations in Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="f9018-109">How to trace the read and write operations in Azure File Storage</span></span>](#traceop)

<span data-ttu-id="f9018-110">**Windows client problems**</span><span class="sxs-lookup"><span data-stu-id="f9018-110">**Windows client problems**</span></span>

* [<span data-ttu-id="f9018-111">Slow performance when you access Azure File storage from Windows 8.1 or Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="f9018-111">Slow performance when you access Azure File storage from Windows 8.1 or Windows Server 2012 R2</span></span>](#windowsslow)
* [<span data-ttu-id="f9018-112">Error 53 attempting to mount an Azure File Share</span><span class="sxs-lookup"><span data-stu-id="f9018-112">Error 53 attempting to mount an Azure File Share</span></span>](#error53)
* [<span data-ttu-id="f9018-113">Error 87 The parameter is incorrect while attempting to mount an Azure File Share</span><span class="sxs-lookup"><span data-stu-id="f9018-113">Error 87 The parameter is incorrect while attempting to mount an Azure File Share</span></span>](#error87)
* [<span data-ttu-id="f9018-114">Net use was successful but I don't see the Azure file share mounted or drive letter in Windows Explorer UI</span><span class="sxs-lookup"><span data-stu-id="f9018-114">Net use was successful but I don't see the Azure file share mounted or drive letter in Windows Explorer UI</span></span>](#netuse)
* [<span data-ttu-id="f9018-115">My storage account contains "/" and the net use command fails</span><span class="sxs-lookup"><span data-stu-id="f9018-115">My storage account contains "/" and the net use command fails</span></span>](#slashfails)
* [<span data-ttu-id="f9018-116">My application/service cannot access mounted Azure Files drive.</span><span class="sxs-lookup"><span data-stu-id="f9018-116">My application/service cannot access mounted Azure Files drive.</span></span>](#accessfiledrive)
* [<span data-ttu-id="f9018-117">Additional recommendations to optimize performance</span><span class="sxs-lookup"><span data-stu-id="f9018-117">Additional recommendations to optimize performance</span></span>](#additional)
* [<span data-ttu-id="f9018-118">Error "You are copying a file to a destination that does not support encryption" when uploading/copying files to Azure Files</span><span class="sxs-lookup"><span data-stu-id="f9018-118">Error "You are copying a file to a destination that does not support encryption" when uploading/copying files to Azure Files</span></span>](#encryption)

<span data-ttu-id="f9018-119">**Linux client problems**</span><span class="sxs-lookup"><span data-stu-id="f9018-119">**Linux client problems**</span></span>

* [<span data-ttu-id="f9018-120">Intermittent IO Error - "Host is down (Error 112)" on existing file shares, or the shell hangs when doing list commands on the mount point</span><span class="sxs-lookup"><span data-stu-id="f9018-120">Intermittent IO Error - "Host is down (Error 112)" on existing file shares, or the shell hangs when doing list commands on the mount point</span></span>](#error112)
* [<span data-ttu-id="f9018-121">Mount error 115 when attempting to mount Azure Files on the Linux VM</span><span class="sxs-lookup"><span data-stu-id="f9018-121">Mount error 115 when attempting to mount Azure Files on the Linux VM</span></span>](#error15)
* [<span data-ttu-id="f9018-122">Azure file share mounted on Linux VM experiencing slow performance</span><span class="sxs-lookup"><span data-stu-id="f9018-122">Azure file share mounted on Linux VM experiencing slow performance</span></span>](#delayproblem)
* [<span data-ttu-id="f9018-123">Mount error(11): Resource temporarily unavailable when mounting to Ubuntu 4.8+ kernel</span><span class="sxs-lookup"><span data-stu-id="f9018-123">Mount error(11): Resource temporarily unavailable when mounting to Ubuntu 4.8+ kernel</span></span>](#ubuntumounterror)

<a id="quotaerror"></a>

## <a name="quota-error-when-trying-to-open-a-file"></a><span data-ttu-id="f9018-124">Quota error when trying to open a file</span><span class="sxs-lookup"><span data-stu-id="f9018-124">Quota error when trying to open a file</span></span>
<span data-ttu-id="f9018-125">In Windows, you receive error messages that resemble the following:</span><span class="sxs-lookup"><span data-stu-id="f9018-125">In Windows, you receive error messages that resemble the following:</span></span>

`1816 ERROR_NOT_ENOUGH_QUOTA <--> 0xc0000044`
`STATUS_QUOTA_EXCEEDED`
`Not enough quota is available to process this command`
`Invalid handle value GetLastError: 53`

<span data-ttu-id="f9018-126">On Linux, you receive error messages that resemble the following:</span><span class="sxs-lookup"><span data-stu-id="f9018-126">On Linux, you receive error messages that resemble the following:</span></span>

`<filename> [permission denied]`
`Disk quota exceeded`

### <a name="cause"></a><span data-ttu-id="f9018-127">Cause</span><span class="sxs-lookup"><span data-stu-id="f9018-127">Cause</span></span>
<span data-ttu-id="f9018-128">The problem occurs because you have reached the upper limit of concurrent open handles that are allowed for a file.</span><span class="sxs-lookup"><span data-stu-id="f9018-128">The problem occurs because you have reached the upper limit of concurrent open handles that are allowed for a file.</span></span>

### <a name="solution"></a><span data-ttu-id="f9018-129">Solution</span><span class="sxs-lookup"><span data-stu-id="f9018-129">Solution</span></span>
<span data-ttu-id="f9018-130">Reduce the number of concurrent open handles by closing some handles,  and then retry.</span><span class="sxs-lookup"><span data-stu-id="f9018-130">Reduce the number of concurrent open handles by closing some handles,  and then retry.</span></span> <span data-ttu-id="f9018-131">For more information, see [Microsoft Azure Storage Performance and Scalability Checklist](storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="f9018-131">For more information, see [Microsoft Azure Storage Performance and Scalability Checklist](storage-performance-checklist.md).</span></span>

<a id="slowboth"></a>

## <a name="slow-performance-when-accessing-file-storage-from-windows-or-linux"></a><span data-ttu-id="f9018-132">Slow performance when accessing File storage from Windows or Linux</span><span class="sxs-lookup"><span data-stu-id="f9018-132">Slow performance when accessing File storage from Windows or Linux</span></span>
* <span data-ttu-id="f9018-133">If you don't have a specific minimum I/O size requirement, we recommend that you use 1 MB as the I/O size for optimal performance.</span><span class="sxs-lookup"><span data-stu-id="f9018-133">If you don't have a specific minimum I/O size requirement, we recommend that you use 1 MB as the I/O size for optimal performance.</span></span>
* <span data-ttu-id="f9018-134">If you know the final size of a file that you are extending with writes, and your software doesn't have compatibility issues when the not yet written tail on the file containing zeros, then set the file size in advance instead of every write being an extending write.</span><span class="sxs-lookup"><span data-stu-id="f9018-134">If you know the final size of a file that you are extending with writes, and your software doesn't have compatibility issues when the not yet written tail on the file containing zeros, then set the file size in advance instead of every write being an extending write.</span></span>
* <span data-ttu-id="f9018-135">Use the right copy method:</span><span class="sxs-lookup"><span data-stu-id="f9018-135">Use the right copy method:</span></span>
      * <span data-ttu-id="f9018-136">Use AZCopy for any transfer between two file shares.</span><span class="sxs-lookup"><span data-stu-id="f9018-136">Use AZCopy for any transfer between two file shares.</span></span> <span data-ttu-id="f9018-137">See [Transfer data with the AzCopy Command-Line Utility](https://docs.microsoft.com/en-us/azure/storage/storage-use-azcopy#file-copy) for more details.</span><span class="sxs-lookup"><span data-stu-id="f9018-137">See [Transfer data with the AzCopy Command-Line Utility](https://docs.microsoft.com/en-us/azure/storage/storage-use-azcopy#file-copy) for more details.</span></span>
      * <span data-ttu-id="f9018-138">Use Robocopy between a file share an on-premises computer.</span><span class="sxs-lookup"><span data-stu-id="f9018-138">Use Robocopy between a file share an on-premises computer.</span></span> <span data-ttu-id="f9018-139">Please see [Multi-threaded robocopy for faster copies](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) for more details.</span><span class="sxs-lookup"><span data-stu-id="f9018-139">Please see [Multi-threaded robocopy for faster copies](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) for more details.</span></span>
<a id="windowsslow"></a>

## <a name="slow-performance-when-accessing-the-file-storage-from-windows-81-or-windows-server-2012-r2"></a><span data-ttu-id="f9018-140">Slow performance when accessing the File storage from Windows 8.1 or Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="f9018-140">Slow performance when accessing the File storage from Windows 8.1 or Windows Server 2012 R2</span></span>
<span data-ttu-id="f9018-141">For clients who are running Windows 8.1 or Windows Server 2012 R2, make sure that the hotfix [KB3114025](https://support.microsoft.com/kb/3114025) is installed.</span><span class="sxs-lookup"><span data-stu-id="f9018-141">For clients who are running Windows 8.1 or Windows Server 2012 R2, make sure that the hotfix [KB3114025](https://support.microsoft.com/kb/3114025) is installed.</span></span> <span data-ttu-id="f9018-142">This hotfix improves the create and close handle performance.</span><span class="sxs-lookup"><span data-stu-id="f9018-142">This hotfix improves the create and close handle performance.</span></span>

<span data-ttu-id="f9018-143">You can run the following script to check whether the hotfix has been installed on:</span><span class="sxs-lookup"><span data-stu-id="f9018-143">You can run the following script to check whether the hotfix has been installed on:</span></span>

`reg query HKLM\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies`

<span data-ttu-id="f9018-144">If hotfix is installed, the following output is displayed:</span><span class="sxs-lookup"><span data-stu-id="f9018-144">If hotfix is installed, the following output is displayed:</span></span>

`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies`
`{96c345ef-3cac-477b-8fcd-bea1a564241c}    REG_DWORD    0x1`

> [!NOTE]
> <span data-ttu-id="f9018-145">Windows Server 2012 R2 images in Azure Marketplace have the hotfix KB3114025 installed by default starting in December 2015.</span><span class="sxs-lookup"><span data-stu-id="f9018-145">Windows Server 2012 R2 images in Azure Marketplace have the hotfix KB3114025 installed by default starting in December 2015.</span></span>
>
>

<a id="traceop"></a>

### <a name="how-to-trace-the-read-and-write-operations-in-azure-file-storage"></a><span data-ttu-id="f9018-146">How to trace the read and write operations in Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="f9018-146">How to trace the read and write operations in Azure File Storage</span></span>

<span data-ttu-id="f9018-147">[Microsoft Message Analyzer](https://www.microsoft.com/en-us/download/details.aspx?id=44226) is able to show you a client's request in clear text and there's a pretty good relation between wire requests and transactions (assuming SMB here not REST).</span><span class="sxs-lookup"><span data-stu-id="f9018-147">[Microsoft Message Analyzer](https://www.microsoft.com/en-us/download/details.aspx?id=44226) is able to show you a client's request in clear text and there's a pretty good relation between wire requests and transactions (assuming SMB here not REST).</span></span>  <span data-ttu-id="f9018-148">The downside is that you have to run this on each client which is time-consuming if you have many IaaS VM workers.</span><span class="sxs-lookup"><span data-stu-id="f9018-148">The downside is that you have to run this on each client which is time-consuming if you have many IaaS VM workers.</span></span>

<span data-ttu-id="f9018-149">If you use the Message Analyze with ProcMon, you can get a pretty good idea which App code is responsible for the transactions.</span><span class="sxs-lookup"><span data-stu-id="f9018-149">If you use the Message Analyze with ProcMon, you can get a pretty good idea which App code is responsible for the transactions.</span></span>

<a id="additional"></a>

## <a name="additional-recommendations-to-optimize-performance"></a><span data-ttu-id="f9018-150">Additional recommendations to optimize performance</span><span class="sxs-lookup"><span data-stu-id="f9018-150">Additional recommendations to optimize performance</span></span>
<span data-ttu-id="f9018-151">Never create or open a file for cached I/O that is requesting write access but not read access.</span><span class="sxs-lookup"><span data-stu-id="f9018-151">Never create or open a file for cached I/O that is requesting write access but not read access.</span></span> <span data-ttu-id="f9018-152">That is, when you call **CreateFile()**, never specify only **GENERIC_WRITE**, but always specify **GENERIC_READ | GENERIC_WRITE**.</span><span class="sxs-lookup"><span data-stu-id="f9018-152">That is, when you call **CreateFile()**, never specify only **GENERIC_WRITE**, but always specify **GENERIC_READ | GENERIC_WRITE**.</span></span> <span data-ttu-id="f9018-153">A write-only handle cannot cache small writes locally, even when it is the only open handle for the file.</span><span class="sxs-lookup"><span data-stu-id="f9018-153">A write-only handle cannot cache small writes locally, even when it is the only open handle for the file.</span></span> <span data-ttu-id="f9018-154">This imposes a severe performance penalty on small writes.</span><span class="sxs-lookup"><span data-stu-id="f9018-154">This imposes a severe performance penalty on small writes.</span></span> <span data-ttu-id="f9018-155">Note that the "a" mode to CRT **fopen()** opens a write-only handle.</span><span class="sxs-lookup"><span data-stu-id="f9018-155">Note that the "a" mode to CRT **fopen()** opens a write-only handle.</span></span>

<a id="error53"></a>

## <a name="error-53-or-error-67-when-you-try-to-mount-or-unmount-an-azure-file-share"></a><span data-ttu-id="f9018-156">"Error 53" or "Error 67" when you try to mount or unmount an Azure File Share</span><span class="sxs-lookup"><span data-stu-id="f9018-156">"Error 53" or "Error 67" when you try to mount or unmount an Azure File Share</span></span>
<span data-ttu-id="f9018-157">This problem can be caused by following conditions:</span><span class="sxs-lookup"><span data-stu-id="f9018-157">This problem can be caused by following conditions:</span></span>

### <a name="cause-1"></a><span data-ttu-id="f9018-158">Cause 1</span><span class="sxs-lookup"><span data-stu-id="f9018-158">Cause 1</span></span>
<span data-ttu-id="f9018-159">"System error 53 has occurred.</span><span class="sxs-lookup"><span data-stu-id="f9018-159">"System error 53 has occurred.</span></span> <span data-ttu-id="f9018-160">Access is denied."</span><span class="sxs-lookup"><span data-stu-id="f9018-160">Access is denied."</span></span> <span data-ttu-id="f9018-161">For security reasons, connections to Azure Files shares are blocked if the communication channel isn't encrypted and the connection attempt is not made from the same Azure region on which Azure File shares reside.</span><span class="sxs-lookup"><span data-stu-id="f9018-161">For security reasons, connections to Azure Files shares are blocked if the communication channel isn't encrypted and the connection attempt is not made from the same Azure region on which Azure File shares reside.</span></span> <span data-ttu-id="f9018-162">Communication channel encryption is not provided if the user's client OS doesn't support SMB encryption.</span><span class="sxs-lookup"><span data-stu-id="f9018-162">Communication channel encryption is not provided if the user's client OS doesn't support SMB encryption.</span></span> <span data-ttu-id="f9018-163">This is indicated by a "System error 53 has occurred.</span><span class="sxs-lookup"><span data-stu-id="f9018-163">This is indicated by a "System error 53 has occurred.</span></span> <span data-ttu-id="f9018-164">Access is denied" Error message when a user tries to mount a file share from on-premises or from a different data center.</span><span class="sxs-lookup"><span data-stu-id="f9018-164">Access is denied" Error message when a user tries to mount a file share from on-premises or from a different data center.</span></span> <span data-ttu-id="f9018-165">Windows 8, Windows Server 2012, and later versions of each negotiate request that includes SMB 3.0, which supports encryption.</span><span class="sxs-lookup"><span data-stu-id="f9018-165">Windows 8, Windows Server 2012, and later versions of each negotiate request that includes SMB 3.0, which supports encryption.</span></span>

### <a name="solution-for-cause-1"></a><span data-ttu-id="f9018-166">Solution for Cause 1</span><span class="sxs-lookup"><span data-stu-id="f9018-166">Solution for Cause 1</span></span>
<span data-ttu-id="f9018-167">Connect from a client that meets the requirements of Windows 8, Windows Server 2012 or later versions, or that connect from a virtual machine that is on the same Azure region as the Azure Storage account that is used for the Azure File share.</span><span class="sxs-lookup"><span data-stu-id="f9018-167">Connect from a client that meets the requirements of Windows 8, Windows Server 2012 or later versions, or that connect from a virtual machine that is on the same Azure region as the Azure Storage account that is used for the Azure File share.</span></span>

### <a name="cause-2"></a><span data-ttu-id="f9018-168">Cause 2</span><span class="sxs-lookup"><span data-stu-id="f9018-168">Cause 2</span></span>
<span data-ttu-id="f9018-169">"System Error 53" or "System Error 67" when you mount an Azure file share can occur if Port 445 outbound communication to Azure Files Azure region is blocked.</span><span class="sxs-lookup"><span data-stu-id="f9018-169">"System Error 53" or "System Error 67" when you mount an Azure file share can occur if Port 445 outbound communication to Azure Files Azure region is blocked.</span></span> <span data-ttu-id="f9018-170">Click [here](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx) to see the summary of ISPs that allow or disallow access from port 445.</span><span class="sxs-lookup"><span data-stu-id="f9018-170">Click [here](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx) to see the summary of ISPs that allow or disallow access from port 445.</span></span>

<span data-ttu-id="f9018-171">Comcast and some IT organizations block this port.</span><span class="sxs-lookup"><span data-stu-id="f9018-171">Comcast and some IT organizations block this port.</span></span> <span data-ttu-id="f9018-172">To understand whether this is the reason behind the "System Error 53" message, you can use Portqry to query the TCP:445 endpoint.</span><span class="sxs-lookup"><span data-stu-id="f9018-172">To understand whether this is the reason behind the "System Error 53" message, you can use Portqry to query the TCP:445 endpoint.</span></span> <span data-ttu-id="f9018-173">If the TCP:445 endpoint is displayed as filtered, the TCP port is blocked.</span><span class="sxs-lookup"><span data-stu-id="f9018-173">If the TCP:445 endpoint is displayed as filtered, the TCP port is blocked.</span></span> <span data-ttu-id="f9018-174">Here is an example query:</span><span class="sxs-lookup"><span data-stu-id="f9018-174">Here is an example query:</span></span>

`g:\DataDump\Tools\Portqry>PortQry.exe -n [storage account name].file.core.windows.net -p TCP -e 445`

<span data-ttu-id="f9018-175">If the TCP 445 being blocked by a rule along the network path, you will see the following output:</span><span class="sxs-lookup"><span data-stu-id="f9018-175">If the TCP 445 being blocked by a rule along the network path, you will see the following output:</span></span>

<span data-ttu-id="f9018-176">**TCP port 445 (microsoft-ds service): FILTERED**</span><span class="sxs-lookup"><span data-stu-id="f9018-176">**TCP port 445 (microsoft-ds service): FILTERED**</span></span>

<span data-ttu-id="f9018-177">For more information on using Portqry, see [Description of the Portqry.exe command-line utility](https://support.microsoft.com/kb/310099).</span><span class="sxs-lookup"><span data-stu-id="f9018-177">For more information on using Portqry, see [Description of the Portqry.exe command-line utility](https://support.microsoft.com/kb/310099).</span></span>

### <a name="solution-for-cause-2"></a><span data-ttu-id="f9018-178">Solution for Cause 2</span><span class="sxs-lookup"><span data-stu-id="f9018-178">Solution for Cause 2</span></span>
<span data-ttu-id="f9018-179">Work with your IT organization to open Port 445 outbound to [Azure IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="f9018-179">Work with your IT organization to open Port 445 outbound to [Azure IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

<a id="error87"></a>
### <a name="cause-3"></a><span data-ttu-id="f9018-180">Cause 3</span><span class="sxs-lookup"><span data-stu-id="f9018-180">Cause 3</span></span>
<span data-ttu-id="f9018-181">"System Error 53 or System error 87" can also be received if NTLMv1 communication is enabled on the client.</span><span class="sxs-lookup"><span data-stu-id="f9018-181">"System Error 53 or System error 87" can also be received if NTLMv1 communication is enabled on the client.</span></span> <span data-ttu-id="f9018-182">Having NTLMv1 enabled creates a less-secure client.</span><span class="sxs-lookup"><span data-stu-id="f9018-182">Having NTLMv1 enabled creates a less-secure client.</span></span> <span data-ttu-id="f9018-183">Therefore, communication will be blocked for Azure Files.</span><span class="sxs-lookup"><span data-stu-id="f9018-183">Therefore, communication will be blocked for Azure Files.</span></span> <span data-ttu-id="f9018-184">To verify whether this is the cause of the error, verify that the following registry subkey is set to a value of 3:</span><span class="sxs-lookup"><span data-stu-id="f9018-184">To verify whether this is the cause of the error, verify that the following registry subkey is set to a value of 3:</span></span>

<span data-ttu-id="f9018-185">HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel.</span><span class="sxs-lookup"><span data-stu-id="f9018-185">HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel.</span></span>

<span data-ttu-id="f9018-186">For more information, see the [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) topic on TechNet.</span><span class="sxs-lookup"><span data-stu-id="f9018-186">For more information, see the [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) topic on TechNet.</span></span>

### <a name="solution-for-cause-3"></a><span data-ttu-id="f9018-187">Solution for Cause 3</span><span class="sxs-lookup"><span data-stu-id="f9018-187">Solution for Cause 3</span></span>
<span data-ttu-id="f9018-188">To resolve this issue, revert the LmCompatibilityLevel value in the HKLM\SYSTEM\CurrentControlSet\Control\Lsa registry key to the default value of 3.</span><span class="sxs-lookup"><span data-stu-id="f9018-188">To resolve this issue, revert the LmCompatibilityLevel value in the HKLM\SYSTEM\CurrentControlSet\Control\Lsa registry key to the default value of 3.</span></span>

<span data-ttu-id="f9018-189">Azure Files supports only NTLMv2 authentication.</span><span class="sxs-lookup"><span data-stu-id="f9018-189">Azure Files supports only NTLMv2 authentication.</span></span> <span data-ttu-id="f9018-190">Make sure that Group Policy is applied to the clients.</span><span class="sxs-lookup"><span data-stu-id="f9018-190">Make sure that Group Policy is applied to the clients.</span></span> <span data-ttu-id="f9018-191">This will prevent this error from occurring.</span><span class="sxs-lookup"><span data-stu-id="f9018-191">This will prevent this error from occurring.</span></span> <span data-ttu-id="f9018-192">This is also considered to be a security best practice.</span><span class="sxs-lookup"><span data-stu-id="f9018-192">This is also considered to be a security best practice.</span></span> <span data-ttu-id="f9018-193">For more information, see [how to configure clients to use NTLMv2 using Group Policy](https://technet.microsoft.com/library/jj852207\(v=ws.11\).aspx)</span><span class="sxs-lookup"><span data-stu-id="f9018-193">For more information, see [how to configure clients to use NTLMv2 using Group Policy](https://technet.microsoft.com/library/jj852207\(v=ws.11\).aspx)</span></span>

<span data-ttu-id="f9018-194">The recommended policy setting is **Send NTLMv2 response only**.</span><span class="sxs-lookup"><span data-stu-id="f9018-194">The recommended policy setting is **Send NTLMv2 response only**.</span></span> <span data-ttu-id="f9018-195">This corresponds to a registry value of 3.</span><span class="sxs-lookup"><span data-stu-id="f9018-195">This corresponds to a registry value of 3.</span></span> <span data-ttu-id="f9018-196">Clients use only NTLMv2 authentication, and they use NTLMv2 session security if the server supports it.</span><span class="sxs-lookup"><span data-stu-id="f9018-196">Clients use only NTLMv2 authentication, and they use NTLMv2 session security if the server supports it.</span></span> <span data-ttu-id="f9018-197">Domain controllers accept LM, NTLM, and NTLMv2 authentication.</span><span class="sxs-lookup"><span data-stu-id="f9018-197">Domain controllers accept LM, NTLM, and NTLMv2 authentication.</span></span>

<a id="netuse"></a>

## <a name="net-use-was-successful-but-dont-see-the-azure-file-share-mounted-in-windows-explorer"></a><span data-ttu-id="f9018-198">Net use was successful but don't see the Azure file share mounted in Windows Explorer</span><span class="sxs-lookup"><span data-stu-id="f9018-198">Net use was successful but don't see the Azure file share mounted in Windows Explorer</span></span>
### <a name="cause"></a><span data-ttu-id="f9018-199">Cause</span><span class="sxs-lookup"><span data-stu-id="f9018-199">Cause</span></span>
<span data-ttu-id="f9018-200">By default, Windows Explorer does not run as Administrator.</span><span class="sxs-lookup"><span data-stu-id="f9018-200">By default, Windows Explorer does not run as Administrator.</span></span> <span data-ttu-id="f9018-201">If you run **net use** from an Administrator command prompt, you map the network drive "As Administrator."</span><span class="sxs-lookup"><span data-stu-id="f9018-201">If you run **net use** from an Administrator command prompt, you map the network drive "As Administrator."</span></span> <span data-ttu-id="f9018-202">Because mapped drives are user-centric, the user account that is logged in does not display the drives if they are mounted under a different user account.</span><span class="sxs-lookup"><span data-stu-id="f9018-202">Because mapped drives are user-centric, the user account that is logged in does not display the drives if they are mounted under a different user account.</span></span>

### <a name="solution"></a><span data-ttu-id="f9018-203">Solution</span><span class="sxs-lookup"><span data-stu-id="f9018-203">Solution</span></span>
<span data-ttu-id="f9018-204">Mount the share from a non-administrator command line.</span><span class="sxs-lookup"><span data-stu-id="f9018-204">Mount the share from a non-administrator command line.</span></span> <span data-ttu-id="f9018-205">Alternatively, you can follow [this TechNet topic](https://technet.microsoft.com/library/ee844140.aspx) to configure the **EnableLinkedConnections** registry value.</span><span class="sxs-lookup"><span data-stu-id="f9018-205">Alternatively, you can follow [this TechNet topic](https://technet.microsoft.com/library/ee844140.aspx) to configure the **EnableLinkedConnections** registry value.</span></span>

<a id="slashfails"></a>

## <a name="my-storage-account-contains--and-the-net-use-command-fails"></a><span data-ttu-id="f9018-206">My storage account contains "/" and the net use command fails</span><span class="sxs-lookup"><span data-stu-id="f9018-206">My storage account contains "/" and the net use command fails</span></span>
### <a name="cause"></a><span data-ttu-id="f9018-207">Cause</span><span class="sxs-lookup"><span data-stu-id="f9018-207">Cause</span></span>
<span data-ttu-id="f9018-208">When the **net use** command is run under Command Prompt (cmd.exe), it's parsed by adding "/" as a command-line option.</span><span class="sxs-lookup"><span data-stu-id="f9018-208">When the **net use** command is run under Command Prompt (cmd.exe), it's parsed by adding "/" as a command-line option.</span></span> <span data-ttu-id="f9018-209">This causes the drive mapping to fail.</span><span class="sxs-lookup"><span data-stu-id="f9018-209">This causes the drive mapping to fail.</span></span>

### <a name="solution"></a><span data-ttu-id="f9018-210">Solution</span><span class="sxs-lookup"><span data-stu-id="f9018-210">Solution</span></span>
<span data-ttu-id="f9018-211">You can use either of the following steps to work around the issue:</span><span class="sxs-lookup"><span data-stu-id="f9018-211">You can use either of the following steps to work around the issue:</span></span>

<span data-ttu-id="f9018-212">•    Use the following PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="f9018-212">•    Use the following PowerShell command:</span></span>

`New-SmbMapping -LocalPath y: -RemotePath \\server\share  -UserName acountName -Password "password can contain / and \ etc"`

<span data-ttu-id="f9018-213">From a batch file this can be done as</span><span class="sxs-lookup"><span data-stu-id="f9018-213">From a batch file this can be done as</span></span>

`Echo new-smbMapping ... | powershell -command –`

<span data-ttu-id="f9018-214">•    Put double quotation marks around the key to work around this issue — unless "/" is the first character.</span><span class="sxs-lookup"><span data-stu-id="f9018-214">•    Put double quotation marks around the key to work around this issue — unless "/" is the first character.</span></span> <span data-ttu-id="f9018-215">If it is, either use the interactive mode and enter your password separately or regenerate your keys to get a key that doesn't start with the forward slash (/) character.</span><span class="sxs-lookup"><span data-stu-id="f9018-215">If it is, either use the interactive mode and enter your password separately or regenerate your keys to get a key that doesn't start with the forward slash (/) character.</span></span>

<a id="accessfiledrive"></a>

## <a name="my-applicationservice-cannot-access-mounted-azure-files-drive"></a><span data-ttu-id="f9018-216">My application/service cannot access mounted Azure Files drive</span><span class="sxs-lookup"><span data-stu-id="f9018-216">My application/service cannot access mounted Azure Files drive</span></span>
### <a name="cause"></a><span data-ttu-id="f9018-217">Cause</span><span class="sxs-lookup"><span data-stu-id="f9018-217">Cause</span></span>
<span data-ttu-id="f9018-218">Drives are mounted per user.</span><span class="sxs-lookup"><span data-stu-id="f9018-218">Drives are mounted per user.</span></span> <span data-ttu-id="f9018-219">If your application or service is running under a different user account, users won't see the drive.</span><span class="sxs-lookup"><span data-stu-id="f9018-219">If your application or service is running under a different user account, users won't see the drive.</span></span>

### <a name="solution"></a><span data-ttu-id="f9018-220">Solution</span><span class="sxs-lookup"><span data-stu-id="f9018-220">Solution</span></span>
<span data-ttu-id="f9018-221">Mount drive from the same user account under which the application is.</span><span class="sxs-lookup"><span data-stu-id="f9018-221">Mount drive from the same user account under which the application is.</span></span> <span data-ttu-id="f9018-222">This can be done using tools such as psexec.</span><span class="sxs-lookup"><span data-stu-id="f9018-222">This can be done using tools such as psexec.</span></span>

<span data-ttu-id="f9018-223">Another option for **net use** is to pass in the storage account name and key in the user name and password parameters of the **net use** command.</span><span class="sxs-lookup"><span data-stu-id="f9018-223">Another option for **net use** is to pass in the storage account name and key in the user name and password parameters of the **net use** command.</span></span>

<span data-ttu-id="f9018-224">After you follow these instructions, you may receive the following error message: "System error 1312 has occurred.</span><span class="sxs-lookup"><span data-stu-id="f9018-224">After you follow these instructions, you may receive the following error message: "System error 1312 has occurred.</span></span> <span data-ttu-id="f9018-225">A specified logon session does not exist.</span><span class="sxs-lookup"><span data-stu-id="f9018-225">A specified logon session does not exist.</span></span> <span data-ttu-id="f9018-226">It may already have been terminated" when you run **net use** for the system/network service account.</span><span class="sxs-lookup"><span data-stu-id="f9018-226">It may already have been terminated" when you run **net use** for the system/network service account.</span></span> <span data-ttu-id="f9018-227">If this occurs, make sure that the username that is passed to **net use** includes domain information (for example: "[storage account name].file.core.windows.net").</span><span class="sxs-lookup"><span data-stu-id="f9018-227">If this occurs, make sure that the username that is passed to **net use** includes domain information (for example: "[storage account name].file.core.windows.net").</span></span>

<a id="encryption"></a>

## <a name="error-you-are-copying-a-file-to-a-destination-that-does-not-support-encryption"></a><span data-ttu-id="f9018-228">Error "You are copying a file to a destination that does not support encryption"</span><span class="sxs-lookup"><span data-stu-id="f9018-228">Error "You are copying a file to a destination that does not support encryption"</span></span>
### <a name="cause"></a><span data-ttu-id="f9018-229">Cause</span><span class="sxs-lookup"><span data-stu-id="f9018-229">Cause</span></span>
<span data-ttu-id="f9018-230">Bitlocker-encrypted files can be copied to Azure Files.</span><span class="sxs-lookup"><span data-stu-id="f9018-230">Bitlocker-encrypted files can be copied to Azure Files.</span></span> <span data-ttu-id="f9018-231">However, the File storage does not support NTFS EFS.</span><span class="sxs-lookup"><span data-stu-id="f9018-231">However, the File storage does not support NTFS EFS.</span></span> <span data-ttu-id="f9018-232">Therefore, you are likely using EFS in this case.</span><span class="sxs-lookup"><span data-stu-id="f9018-232">Therefore, you are likely using EFS in this case.</span></span> <span data-ttu-id="f9018-233">If you have files that are encrypted through EFS, a copy operation to the File storage can fail unless the copy command is decrypting a copied file.</span><span class="sxs-lookup"><span data-stu-id="f9018-233">If you have files that are encrypted through EFS, a copy operation to the File storage can fail unless the copy command is decrypting a copied file.</span></span>

### <a name="workaround"></a><span data-ttu-id="f9018-234">Workaround</span><span class="sxs-lookup"><span data-stu-id="f9018-234">Workaround</span></span>
<span data-ttu-id="f9018-235">To copy a file to the File storage, you must first decrypt it.</span><span class="sxs-lookup"><span data-stu-id="f9018-235">To copy a file to the File storage, you must first decrypt it.</span></span> <span data-ttu-id="f9018-236">You can do this by using one of the following methods:</span><span class="sxs-lookup"><span data-stu-id="f9018-236">You can do this by using one of the following methods:</span></span>

<span data-ttu-id="f9018-237">•    Use **copy /d**.</span><span class="sxs-lookup"><span data-stu-id="f9018-237">•    Use **copy /d**.</span></span>

<span data-ttu-id="f9018-238">•    Set the following registry key:</span><span class="sxs-lookup"><span data-stu-id="f9018-238">•    Set the following registry key:</span></span>

* <span data-ttu-id="f9018-239">Path=HKLM\Software\Policies\Microsoft\Windows\System</span><span class="sxs-lookup"><span data-stu-id="f9018-239">Path=HKLM\Software\Policies\Microsoft\Windows\System</span></span>
* <span data-ttu-id="f9018-240">Value type=DWORD</span><span class="sxs-lookup"><span data-stu-id="f9018-240">Value type=DWORD</span></span>
* <span data-ttu-id="f9018-241">Name = CopyFileAllowDecryptedRemoteDestination</span><span class="sxs-lookup"><span data-stu-id="f9018-241">Name = CopyFileAllowDecryptedRemoteDestination</span></span>
* <span data-ttu-id="f9018-242">Value = 1</span><span class="sxs-lookup"><span data-stu-id="f9018-242">Value = 1</span></span>

<span data-ttu-id="f9018-243">However, note that setting the registry key affects all copy operations to network shares.</span><span class="sxs-lookup"><span data-stu-id="f9018-243">However, note that setting the registry key affects all copy operations to network shares.</span></span>

<a id="error112"></a>

## <a name="host-is-down-error-112-on-existing-file-shares-or-the-shell-hangs-when-you-run-list-commands-on-the-mount-point"></a><span data-ttu-id="f9018-244">"Host is down (Error 112)" on existing file shares, or the shell hangs when you run list commands on the mount point</span><span class="sxs-lookup"><span data-stu-id="f9018-244">"Host is down (Error 112)" on existing file shares, or the shell hangs when you run list commands on the mount point</span></span>
### <a name="cause"></a><span data-ttu-id="f9018-245">Cause</span><span class="sxs-lookup"><span data-stu-id="f9018-245">Cause</span></span>
<span data-ttu-id="f9018-246">This error occurs on the Linux client when the client has been idle for an extended period of time.</span><span class="sxs-lookup"><span data-stu-id="f9018-246">This error occurs on the Linux client when the client has been idle for an extended period of time.</span></span> <span data-ttu-id="f9018-247">When the client is idle for long time, the client disconnects, and the connection times out.</span><span class="sxs-lookup"><span data-stu-id="f9018-247">When the client is idle for long time, the client disconnects, and the connection times out.</span></span> 

<span data-ttu-id="f9018-248">The connection can be idle due to various reasons.</span><span class="sxs-lookup"><span data-stu-id="f9018-248">The connection can be idle due to various reasons.</span></span> <span data-ttu-id="f9018-249">One reason being network communication failures that prevent re-establishing a TCP connection to the server when "soft" mount option is used, which is the default.</span><span class="sxs-lookup"><span data-stu-id="f9018-249">One reason being network communication failures that prevent re-establishing a TCP connection to the server when "soft" mount option is used, which is the default.</span></span>

<span data-ttu-id="f9018-250">Another reason could be that there are also some reconnect fixes which are not present in older kernels.</span><span class="sxs-lookup"><span data-stu-id="f9018-250">Another reason could be that there are also some reconnect fixes which are not present in older kernels.</span></span>

### <a name="solution"></a><span data-ttu-id="f9018-251">Solution</span><span class="sxs-lookup"><span data-stu-id="f9018-251">Solution</span></span>

<span data-ttu-id="f9018-252">Specifying a hard mount will force the client to wait until a connection is established or until explicitly interrupted, and can be used to prevent errors due to network timeouts.</span><span class="sxs-lookup"><span data-stu-id="f9018-252">Specifying a hard mount will force the client to wait until a connection is established or until explicitly interrupted, and can be used to prevent errors due to network timeouts.</span></span> <span data-ttu-id="f9018-253">However, users should be aware that this could lead to indefinite waits and should handle halting a connection as needed.</span><span class="sxs-lookup"><span data-stu-id="f9018-253">However, users should be aware that this could lead to indefinite waits and should handle halting a connection as needed.</span></span>

<span data-ttu-id="f9018-254">This reconnect problem in Linux kernel is now fixed as part of following change sets</span><span class="sxs-lookup"><span data-stu-id="f9018-254">This reconnect problem in Linux kernel is now fixed as part of following change sets</span></span>

* [<span data-ttu-id="f9018-255">Fix reconnect to not defer smb3 session reconnect long after socket reconnect</span><span class="sxs-lookup"><span data-stu-id="f9018-255">Fix reconnect to not defer smb3 session reconnect long after socket reconnect</span></span>](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/fs/cifs?id=4fcd1813e6404dd4420c7d12fb483f9320f0bf93)

* [<span data-ttu-id="f9018-256">Call echo service immediately after socket reconnect</span><span class="sxs-lookup"><span data-stu-id="f9018-256">Call echo service immediately after socket reconnect</span></span>](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=b8c600120fc87d53642476f48c8055b38d6e14c7)

* [<span data-ttu-id="f9018-257">CIFS: Fix a possible memory corruption during reconnect</span><span class="sxs-lookup"><span data-stu-id="f9018-257">CIFS: Fix a possible memory corruption during reconnect</span></span>](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=53e0e11efe9289535b060a51d4cf37c25e0d0f2b)

* [<span data-ttu-id="f9018-258">CIFS: Fix a possible double locking of mutex during reconnect - for kernels v4.9 and higher</span><span class="sxs-lookup"><span data-stu-id="f9018-258">CIFS: Fix a possible double locking of mutex during reconnect - for kernels v4.9 and higher</span></span>](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=96a988ffeb90dba33a71c3826086fe67c897a183) 

<span data-ttu-id="f9018-259">However this change may not be ported to all the Linux distributions yet.</span><span class="sxs-lookup"><span data-stu-id="f9018-259">However this change may not be ported to all the Linux distributions yet.</span></span> <span data-ttu-id="f9018-260">This is the list of known popular Linux kernels that have this and other reconnect fixes: 4.4.40+ 4.8.16+ 4.9.1+.</span><span class="sxs-lookup"><span data-stu-id="f9018-260">This is the list of known popular Linux kernels that have this and other reconnect fixes: 4.4.40+ 4.8.16+ 4.9.1+.</span></span>
<span data-ttu-id="f9018-261">You can move to the above recommended kernel versions in order to pick up the latest fix.</span><span class="sxs-lookup"><span data-stu-id="f9018-261">You can move to the above recommended kernel versions in order to pick up the latest fix.</span></span>

### <a name="workaround"></a><span data-ttu-id="f9018-262">Workaround</span><span class="sxs-lookup"><span data-stu-id="f9018-262">Workaround</span></span>
<span data-ttu-id="f9018-263">If you are unable to move to latest kernel versions, you can workaround this issue by keeping a file in the Azure File share that you write to every 30 seconds or less.</span><span class="sxs-lookup"><span data-stu-id="f9018-263">If you are unable to move to latest kernel versions, you can workaround this issue by keeping a file in the Azure File share that you write to every 30 seconds or less.</span></span> <span data-ttu-id="f9018-264">This has to be a write operation, such as rewriting the created/modified date on the file.</span><span class="sxs-lookup"><span data-stu-id="f9018-264">This has to be a write operation, such as rewriting the created/modified date on the file.</span></span> <span data-ttu-id="f9018-265">Otherwise, you might get cached results, and your operation might not trigger the re-connection.</span><span class="sxs-lookup"><span data-stu-id="f9018-265">Otherwise, you might get cached results, and your operation might not trigger the re-connection.</span></span> 


<a id="error15"></a>

## <a name="mount-error-115-when-you-try-to-mount-azure-files-on-the-linux-vm"></a><span data-ttu-id="f9018-266">"Mount error 115" when you try to mount Azure Files on the Linux VM</span><span class="sxs-lookup"><span data-stu-id="f9018-266">"Mount error 115" when you try to mount Azure Files on the Linux VM</span></span>
### <a name="cause"></a><span data-ttu-id="f9018-267">Cause</span><span class="sxs-lookup"><span data-stu-id="f9018-267">Cause</span></span>
<span data-ttu-id="f9018-268">Linux distributions do not yet support encryption feature in SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="f9018-268">Linux distributions do not yet support encryption feature in SMB 3.0.</span></span> <span data-ttu-id="f9018-269">In some distributions, user may receive a "115" error message if they try to mount Azure Files by using SMB 3.0 because of a missing feature.</span><span class="sxs-lookup"><span data-stu-id="f9018-269">In some distributions, user may receive a "115" error message if they try to mount Azure Files by using SMB 3.0 because of a missing feature.</span></span>

### <a name="solution"></a><span data-ttu-id="f9018-270">Solution</span><span class="sxs-lookup"><span data-stu-id="f9018-270">Solution</span></span>
<span data-ttu-id="f9018-271">If the Linux SMB client that is used does not support encryption, mount Azure Files by using SMB 2.1 from a Linux VM on the same Azure region as the File storage account.</span><span class="sxs-lookup"><span data-stu-id="f9018-271">If the Linux SMB client that is used does not support encryption, mount Azure Files by using SMB 2.1 from a Linux VM on the same Azure region as the File storage account.</span></span>

<a id="delayproblem"></a>

## <a name="azure-file-share-mounted-on-linux-vm-experiencing-slow-performance"></a><span data-ttu-id="f9018-272">Azure file share mounted on Linux VM experiencing slow performance</span><span class="sxs-lookup"><span data-stu-id="f9018-272">Azure file share mounted on Linux VM experiencing slow performance</span></span>

<span data-ttu-id="f9018-273">A possible reason for slow performance could be that caching is disabled.</span><span class="sxs-lookup"><span data-stu-id="f9018-273">A possible reason for slow performance could be that caching is disabled.</span></span> <span data-ttu-id="f9018-274">In order to check if caching is enabled, look for "cache=".</span><span class="sxs-lookup"><span data-stu-id="f9018-274">In order to check if caching is enabled, look for "cache=".</span></span>  <span data-ttu-id="f9018-275">*cache=none* indicates that caching is disabled.</span><span class="sxs-lookup"><span data-stu-id="f9018-275">*cache=none* indicates that caching is disabled.</span></span> <span data-ttu-id="f9018-276">Please remount the share with default mount command or explicitly adding **cache=strict** option to mount command to ensure default caching or "strict" caching mode is enabled.</span><span class="sxs-lookup"><span data-stu-id="f9018-276">Please remount the share with default mount command or explicitly adding **cache=strict** option to mount command to ensure default caching or "strict" caching mode is enabled.</span></span>

<span data-ttu-id="f9018-277">In some scenarios serverino mount option can cause ls command to run stat against every directory entry and this behavior results in performance degradation when listing a big directory.</span><span class="sxs-lookup"><span data-stu-id="f9018-277">In some scenarios serverino mount option can cause ls command to run stat against every directory entry and this behavior results in performance degradation when listing a big directory.</span></span> <span data-ttu-id="f9018-278">You can check the mount options in your "/etc/fstab" entry:</span><span class="sxs-lookup"><span data-stu-id="f9018-278">You can check the mount options in your "/etc/fstab" entry:</span></span>

`//azureuser.file.core.windows.net/cifs        /cifs   cifs vers=3.0,serverino,username=xxx,password=xxx,dir_mode=0777,file_mode=0777`

<span data-ttu-id="f9018-279">You can also check if correct options are being used by just running the command **sudo mount | grep cifs** and looking as its output:</span><span class="sxs-lookup"><span data-stu-id="f9018-279">You can also check if correct options are being used by just running the command **sudo mount | grep cifs** and looking as its output:</span></span>

`//mabiccacifs.file.core.windows.net/cifs on /cifs type cifs
(rw,relatime,vers=3.0,sec=ntlmssp,cache=strict,username=xxx,domain=X,uid=0,noforceuid,gid=0,noforcegid,addr=192.168.10.1,file_mode=0777,
dir_mode=0777,persistenthandles,nounix,serverino,mapposix,rsize=1048576,wsize=1048576,actimeo=1)`

<span data-ttu-id="f9018-280">If the cache=strict or serverino options are not present, unmount and mount Azure Files again by running the mount command from the [documentation](https://docs.microsoft.com/en-us/azure/storage/storage-how-to-use-files-linux#mount-the-file-share) and re-check that "/etc/fstab" entry has the correct options.</span><span class="sxs-lookup"><span data-stu-id="f9018-280">If the cache=strict or serverino options are not present, unmount and mount Azure Files again by running the mount command from the [documentation](https://docs.microsoft.com/en-us/azure/storage/storage-how-to-use-files-linux#mount-the-file-share) and re-check that "/etc/fstab" entry has the correct options.</span></span>

<a id="ubuntumounterror"></a>
## <a name="mount-error11-resource-temporarily-unavailable-when-mounting-to-ubuntu-48-kernel"></a><span data-ttu-id="f9018-281">mount error(11): Resource temporarily unavailable when mounting to Ubuntu 4.8+ kernel</span><span class="sxs-lookup"><span data-stu-id="f9018-281">mount error(11): Resource temporarily unavailable when mounting to Ubuntu 4.8+ kernel</span></span>

### <a name="cause"></a><span data-ttu-id="f9018-282">Cause</span><span class="sxs-lookup"><span data-stu-id="f9018-282">Cause</span></span>
<span data-ttu-id="f9018-283">Known issue in Ubuntu 16.10 kernel (v.4.8) where the client claims to support encryption but it doesn't.</span><span class="sxs-lookup"><span data-stu-id="f9018-283">Known issue in Ubuntu 16.10 kernel (v.4.8) where the client claims to support encryption but it doesn't.</span></span> 

### <a name="solution"></a><span data-ttu-id="f9018-284">Solution</span><span class="sxs-lookup"><span data-stu-id="f9018-284">Solution</span></span>
<span data-ttu-id="f9018-285">Until Ubuntu 16.10 is fixed, specify the "vers=2.1" mount option or use Ubuntu 16.04.</span><span class="sxs-lookup"><span data-stu-id="f9018-285">Until Ubuntu 16.10 is fixed, specify the "vers=2.1" mount option or use Ubuntu 16.04.</span></span>
## <a name="learn-more"></a><span data-ttu-id="f9018-286">Learn more</span><span class="sxs-lookup"><span data-stu-id="f9018-286">Learn more</span></span>
* [<span data-ttu-id="f9018-287">Get started with Azure File storage on Windows</span><span class="sxs-lookup"><span data-stu-id="f9018-287">Get started with Azure File storage on Windows</span></span>](storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="f9018-288">Get started with Azure File storage on Linux</span><span class="sxs-lookup"><span data-stu-id="f9018-288">Get started with Azure File storage on Linux</span></span>](storage-how-to-use-files-linux.md)
