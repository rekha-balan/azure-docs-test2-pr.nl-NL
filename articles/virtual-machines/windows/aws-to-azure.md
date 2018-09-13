---
title: Move a Windows AWS VMs to Azure | Microsoft Docs
description: Move an Amazon Web Services (AWS) EC2 Windows instance to Azure Virtual Machines using Azure PowerShell.
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/01/2018
ms.author: cynthn
ms.openlocfilehash: c8d0a86b6a3a58f8b0f0bbbb93cce26396095bd8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44821345"
---
# <a name="move-a-windows-vm-from-amazon-web-services-aws-to-azure-using-powershell"></a><span data-ttu-id="52f87-103">Move a Windows VM from Amazon Web Services (AWS) to Azure using PowerShell</span><span class="sxs-lookup"><span data-stu-id="52f87-103">Move a Windows VM from Amazon Web Services (AWS) to Azure using PowerShell</span></span>

<span data-ttu-id="52f87-104">If you are evaluating Azure virtual machines for hosting your workloads, you can export an existing Amazon Web Services (AWS) EC2 Windows VM instance then upload the virtual hard disk (VHD) to Azure.</span><span class="sxs-lookup"><span data-stu-id="52f87-104">If you are evaluating Azure virtual machines for hosting your workloads, you can export an existing Amazon Web Services (AWS) EC2 Windows VM instance then upload the virtual hard disk (VHD) to Azure.</span></span> <span data-ttu-id="52f87-105">Once the VHD is uploaded, you can create a new VM in Azure from the VHD.</span><span class="sxs-lookup"><span data-stu-id="52f87-105">Once the VHD is uploaded, you can create a new VM in Azure from the VHD.</span></span> 

<span data-ttu-id="52f87-106">This article covers moving a single VM from AWS to Azure.</span><span class="sxs-lookup"><span data-stu-id="52f87-106">This article covers moving a single VM from AWS to Azure.</span></span> <span data-ttu-id="52f87-107">If you want to move VMs from AWS to Azure at scale, see [Migrate virtual machines in Amazon Web Services (AWS) to Azure with Azure Site Recovery](../../site-recovery/site-recovery-migrate-aws-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="52f87-107">If you want to move VMs from AWS to Azure at scale, see [Migrate virtual machines in Amazon Web Services (AWS) to Azure with Azure Site Recovery](../../site-recovery/site-recovery-migrate-aws-to-azure.md).</span></span>

## <a name="prepare-the-vm"></a><span data-ttu-id="52f87-108">Prepare the VM</span><span class="sxs-lookup"><span data-stu-id="52f87-108">Prepare the VM</span></span> 
 
<span data-ttu-id="52f87-109">You can upload both generalized and specialized VHDs to Azure.</span><span class="sxs-lookup"><span data-stu-id="52f87-109">You can upload both generalized and specialized VHDs to Azure.</span></span> <span data-ttu-id="52f87-110">Each type requires that you prepare the VM before exporting from AWS.</span><span class="sxs-lookup"><span data-stu-id="52f87-110">Each type requires that you prepare the VM before exporting from AWS.</span></span> 

- <span data-ttu-id="52f87-111">**Generalized VHD** - a generalized VHD has had all of your personal account information removed using Sysprep.</span><span class="sxs-lookup"><span data-stu-id="52f87-111">**Generalized VHD** - a generalized VHD has had all of your personal account information removed using Sysprep.</span></span> <span data-ttu-id="52f87-112">If you intend to use the VHD as an image to create new VMs from, you should:</span><span class="sxs-lookup"><span data-stu-id="52f87-112">If you intend to use the VHD as an image to create new VMs from, you should:</span></span> 
 
    * <span data-ttu-id="52f87-113">[Prepare a Windows VM](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="52f87-113">[Prepare a Windows VM](prepare-for-upload-vhd-image.md).</span></span>  
    * <span data-ttu-id="52f87-114">Generalize the virtual machine using Sysprep.</span><span class="sxs-lookup"><span data-stu-id="52f87-114">Generalize the virtual machine using Sysprep.</span></span>  

 
- <span data-ttu-id="52f87-115">**Specialized VHD** - a specialized VHD maintains the user accounts, applications and other state data from your original VM.</span><span class="sxs-lookup"><span data-stu-id="52f87-115">**Specialized VHD** - a specialized VHD maintains the user accounts, applications and other state data from your original VM.</span></span> <span data-ttu-id="52f87-116">If you intend to use the VHD as-is to create a new VM, ensure the following steps are completed.</span><span class="sxs-lookup"><span data-stu-id="52f87-116">If you intend to use the VHD as-is to create a new VM, ensure the following steps are completed.</span></span>  
    * <span data-ttu-id="52f87-117">[Prepare a Windows VHD to upload to Azure](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="52f87-117">[Prepare a Windows VHD to upload to Azure](prepare-for-upload-vhd-image.md).</span></span> <span data-ttu-id="52f87-118">**Do not** generalize the VM using Sysprep.</span><span class="sxs-lookup"><span data-stu-id="52f87-118">**Do not** generalize the VM using Sysprep.</span></span> 
    * <span data-ttu-id="52f87-119">Remove any guest virtualization tools and agents that are installed on the VM (i.e. VMware tools).</span><span class="sxs-lookup"><span data-stu-id="52f87-119">Remove any guest virtualization tools and agents that are installed on the VM (i.e. VMware tools).</span></span> 
    * <span data-ttu-id="52f87-120">Ensure the VM is configured to pull its IP address and DNS settings via DHCP.</span><span class="sxs-lookup"><span data-stu-id="52f87-120">Ensure the VM is configured to pull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="52f87-121">This ensures that the server obtains an IP address within the VNet when it starts up.</span><span class="sxs-lookup"><span data-stu-id="52f87-121">This ensures that the server obtains an IP address within the VNet when it starts up.</span></span>  


## <a name="export-and-download-the-vhd"></a><span data-ttu-id="52f87-122">Export and download the VHD</span><span class="sxs-lookup"><span data-stu-id="52f87-122">Export and download the VHD</span></span> 

<span data-ttu-id="52f87-123">Export the EC2 instance to a VHD in an Amazon S3 bucket.</span><span class="sxs-lookup"><span data-stu-id="52f87-123">Export the EC2 instance to a VHD in an Amazon S3 bucket.</span></span> <span data-ttu-id="52f87-124">Follow the steps in the Amazon documentation article [Exporting an Instance as a VM Using VM Import/Export](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html) and run the [create-instance-export-task](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html) command to export the EC2 instance to a VHD file.</span><span class="sxs-lookup"><span data-stu-id="52f87-124">Follow the steps in the Amazon documentation article [Exporting an Instance as a VM Using VM Import/Export](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html) and run the [create-instance-export-task](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html) command to export the EC2 instance to a VHD file.</span></span> 

<span data-ttu-id="52f87-125">The exported VHD file is saved in the Amazon S3 bucket you specify.</span><span class="sxs-lookup"><span data-stu-id="52f87-125">The exported VHD file is saved in the Amazon S3 bucket you specify.</span></span> <span data-ttu-id="52f87-126">The basic syntax for exporting the VHD is below, just replace the placeholder text in <brackets> with your information.</span><span class="sxs-lookup"><span data-stu-id="52f87-126">The basic syntax for exporting the VHD is below, just replace the placeholder text in <brackets> with your information.</span></span>

```
aws ec2 create-instance-export-task --instance-id <instanceID> --target-environment Microsoft \
  --export-to-s3-task DiskImageFormat=VHD,ContainerFormat=ova,S3Bucket=<bucket>,S3Prefix=<prefix>
```

<span data-ttu-id="52f87-127">Once the VHD has been exported, follow the instructions in [How Do I Download an Object from an S3 Bucket?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) to download the VHD file from the S3 bucket.</span><span class="sxs-lookup"><span data-stu-id="52f87-127">Once the VHD has been exported, follow the instructions in [How Do I Download an Object from an S3 Bucket?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) to download the VHD file from the S3 bucket.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="52f87-128">AWS charges data transfer fees for downloading the VHD.</span><span class="sxs-lookup"><span data-stu-id="52f87-128">AWS charges data transfer fees for downloading the VHD.</span></span> <span data-ttu-id="52f87-129">See [Amazon S3 Pricing](https://aws.amazon.com/s3/pricing/) for more information.</span><span class="sxs-lookup"><span data-stu-id="52f87-129">See [Amazon S3 Pricing](https://aws.amazon.com/s3/pricing/) for more information.</span></span>


## <a name="next-steps"></a><span data-ttu-id="52f87-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="52f87-130">Next steps</span></span>

<span data-ttu-id="52f87-131">Now you can upload the VHD to Azure and create a new VM.</span><span class="sxs-lookup"><span data-stu-id="52f87-131">Now you can upload the VHD to Azure and create a new VM.</span></span> 

- <span data-ttu-id="52f87-132">If you ran Sysprep on your source to **generalize** it before exporting, see [Upload a generalized VHD and use it to create a new VMs in Azure](upload-generalized-managed.md)</span><span class="sxs-lookup"><span data-stu-id="52f87-132">If you ran Sysprep on your source to **generalize** it before exporting, see [Upload a generalized VHD and use it to create a new VMs in Azure](upload-generalized-managed.md)</span></span>
- <span data-ttu-id="52f87-133">If you did not run Sysprep before exporting, the VHD is considered **specialized**, see [Upload a specialized VHD to Azure and create a new VM](create-vm-specialized.md)</span><span class="sxs-lookup"><span data-stu-id="52f87-133">If you did not run Sysprep before exporting, the VHD is considered **specialized**, see [Upload a specialized VHD to Azure and create a new VM](create-vm-specialized.md)</span></span>

 
