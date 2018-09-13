---
title: Replace a physical disk in Azure Stack | Microsoft Docs
description: Outlines the process for how to replace a physical disk in Azure Stack.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.assetid: 449ae53e-b951-401a-b2c9-17fee2f491f1
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/10/2018
ms.author: mabrigg
ms.openlocfilehash: 7ce501be5458282273e51a5b2bc18482592d2333
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870675"
---
# <a name="replace-a-physical-disk-in-azure-stack"></a><span data-ttu-id="27708-103">Replace a physical disk in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="27708-103">Replace a physical disk in Azure Stack</span></span>

<span data-ttu-id="27708-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="27708-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="27708-105">This article describes the general process to replace a physical disk in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="27708-105">This article describes the general process to replace a physical disk in Azure Stack.</span></span> <span data-ttu-id="27708-106">If a physical disk fails, you should replace it as soon as possible.</span><span class="sxs-lookup"><span data-stu-id="27708-106">If a physical disk fails, you should replace it as soon as possible.</span></span>

<span data-ttu-id="27708-107">You can use this procedure for integrated systems, and for development kit deployments that have hot-swappable disks.</span><span class="sxs-lookup"><span data-stu-id="27708-107">You can use this procedure for integrated systems, and for development kit deployments that have hot-swappable disks.</span></span>

<span data-ttu-id="27708-108">Actual disk replacement steps will vary based on your original equipment manufacturer (OEM) hardware vendor.</span><span class="sxs-lookup"><span data-stu-id="27708-108">Actual disk replacement steps will vary based on your original equipment manufacturer (OEM) hardware vendor.</span></span> <span data-ttu-id="27708-109">See your vendor’s field replaceable unit (FRU) documentation for detailed steps that are specific to your system.</span><span class="sxs-lookup"><span data-stu-id="27708-109">See your vendor’s field replaceable unit (FRU) documentation for detailed steps that are specific to your system.</span></span> 

## <a name="review-disk-alert-information"></a><span data-ttu-id="27708-110">Review disk alert information</span><span class="sxs-lookup"><span data-stu-id="27708-110">Review disk alert information</span></span>
<span data-ttu-id="27708-111">When a disk fails, you receive an alert that tells you that connectivity has been lost to a physical disk.</span><span class="sxs-lookup"><span data-stu-id="27708-111">When a disk fails, you receive an alert that tells you that connectivity has been lost to a physical disk.</span></span> 

 ![Alert showing connectivity lost to physical disk](media/azure-stack-replace-disk/DiskAlert.png)

<span data-ttu-id="27708-113">If you open the alert, the alert description contains the scale unit node and the exact physical slot location for the disk that you must replace.</span><span class="sxs-lookup"><span data-stu-id="27708-113">If you open the alert, the alert description contains the scale unit node and the exact physical slot location for the disk that you must replace.</span></span> <span data-ttu-id="27708-114">Azure Stack further helps you to identify the failed disk by using LED indicator capabilities.</span><span class="sxs-lookup"><span data-stu-id="27708-114">Azure Stack further helps you to identify the failed disk by using LED indicator capabilities.</span></span>

 ## <a name="replace-the-disk"></a><span data-ttu-id="27708-115">Replace the disk</span><span class="sxs-lookup"><span data-stu-id="27708-115">Replace the disk</span></span>

<span data-ttu-id="27708-116">Follow your OEM hardware vendor’s FRU instructions for actual disk replacement.</span><span class="sxs-lookup"><span data-stu-id="27708-116">Follow your OEM hardware vendor’s FRU instructions for actual disk replacement.</span></span>

> [!note]
> <span data-ttu-id="27708-117">Replace disks for one scale unit node at a time.</span><span class="sxs-lookup"><span data-stu-id="27708-117">Replace disks for one scale unit node at a time.</span></span> <span data-ttu-id="27708-118">Wait for the virtual disk repair jobs to complete before moving on to the next scale unit node</span><span class="sxs-lookup"><span data-stu-id="27708-118">Wait for the virtual disk repair jobs to complete before moving on to the next scale unit node</span></span>

<span data-ttu-id="27708-119">To prevent the use of an unsupported disk in an integrated system, the system blocks disks that are not supported by your vendor.</span><span class="sxs-lookup"><span data-stu-id="27708-119">To prevent the use of an unsupported disk in an integrated system, the system blocks disks that are not supported by your vendor.</span></span> <span data-ttu-id="27708-120">If you try to use an unsupported disk, a new alert tells you that a disk has been quarantined because of an unsupported model or firmware.</span><span class="sxs-lookup"><span data-stu-id="27708-120">If you try to use an unsupported disk, a new alert tells you that a disk has been quarantined because of an unsupported model or firmware.</span></span>

<span data-ttu-id="27708-121">After you replace the disk, Azure Stack automatically discovers the new disk and starts the virtual disk repair process.</span><span class="sxs-lookup"><span data-stu-id="27708-121">After you replace the disk, Azure Stack automatically discovers the new disk and starts the virtual disk repair process.</span></span>  
 
 ## <a name="check-the-status-of-virtual-disk-repair"></a><span data-ttu-id="27708-122">Check the status of virtual disk repair</span><span class="sxs-lookup"><span data-stu-id="27708-122">Check the status of virtual disk repair</span></span>
 
 <span data-ttu-id="27708-123">After you replace the disk, you can monitor the virtual disk health status and repair job progress by using the privileged endpoint.</span><span class="sxs-lookup"><span data-stu-id="27708-123">After you replace the disk, you can monitor the virtual disk health status and repair job progress by using the privileged endpoint.</span></span> <span data-ttu-id="27708-124">Follow these steps from any computer that has network connectivity to the privileged endpoint.</span><span class="sxs-lookup"><span data-stu-id="27708-124">Follow these steps from any computer that has network connectivity to the privileged endpoint.</span></span>

1. <span data-ttu-id="27708-125">Open a Windows PowerShell session and connect to the privileged endpoint.</span><span class="sxs-lookup"><span data-stu-id="27708-125">Open a Windows PowerShell session and connect to the privileged endpoint.</span></span>
    ````PowerShell
        $cred = Get-Credential
        Enter-PSSession -ComputerName <IP_address_of_ERCS>`
          -ConfigurationName PrivilegedEndpoint -Credential $cred
    ```` 
  
2. <span data-ttu-id="27708-126">Run the following command to view virtual disk health:</span><span class="sxs-lookup"><span data-stu-id="27708-126">Run the following command to view virtual disk health:</span></span>
    ````PowerShell
        Get-VirtualDisk -CimSession s-cluster
    ````
   ![Powershell output of Get-VirtualDisk command](media/azure-stack-replace-disk/GetVirtualDiskOutput.png)

3. <span data-ttu-id="27708-128">Run the following command to view current storage job status:</span><span class="sxs-lookup"><span data-stu-id="27708-128">Run the following command to view current storage job status:</span></span>
    ```PowerShell
        Get-VirtualDisk -CimSession s-cluster | Get-StorageJob
    ````
      ![Powershell output of Get-StorageJob command](media/azure-stack-replace-disk/GetStorageJobOutput.png)

## <a name="troubleshoot-virtual-disk-repair"></a><span data-ttu-id="27708-130">Troubleshoot virtual disk repair</span><span class="sxs-lookup"><span data-stu-id="27708-130">Troubleshoot virtual disk repair</span></span>

<span data-ttu-id="27708-131">If the virtual disk repair job appears stuck, run the following command to restart the job:</span><span class="sxs-lookup"><span data-stu-id="27708-131">If the virtual disk repair job appears stuck, run the following command to restart the job:</span></span>
  ````PowerShell
        Get-VirtualDisk -CimSession s-cluster | Repair-VirtualDisk
  ```` 
