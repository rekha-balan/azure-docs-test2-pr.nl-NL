---
title: Upload VHD file to Azure DevTest Labs using Microsoft Azure Storage Explorer | Microsoft Docs
description: Upload VHD file to lab's storage account using Microsoft Azure Storage Explorer
services: devtest-lab,virtual-machines,lab-services
documentationcenter: na
author: spelluru
manager: femila
editor: ''
ms.assetid: ''
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2018
ms.author: spelluru
ms.openlocfilehash: cafb3ec2da335165a3b66c18d83930008c6d72e5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857263"
---
# <a name="upload-vhd-file-to-labs-storage-account-using-microsoft-azure-storage-explorer"></a><span data-ttu-id="b6ad9-103">Upload VHD file to lab's storage account using Microsoft Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="b6ad9-103">Upload VHD file to lab's storage account using Microsoft Azure Storage Explorer</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="b6ad9-104">In Azure DevTest Labs, VHD files can be used to create custom images, which are used to provision virtual machines.</span><span class="sxs-lookup"><span data-stu-id="b6ad9-104">In Azure DevTest Labs, VHD files can be used to create custom images, which are used to provision virtual machines.</span></span> <span data-ttu-id="b6ad9-105">This article illustrates how to use [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) to upload a VHD file to a lab's storage account.</span><span class="sxs-lookup"><span data-stu-id="b6ad9-105">This article illustrates how to use [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) to upload a VHD file to a lab's storage account.</span></span> <span data-ttu-id="b6ad9-106">Once you've uploaded your VHD file, the [Next steps section](#next-steps) lists some articles that illustrate how to create a custom image from the uploaded VHD file.</span><span class="sxs-lookup"><span data-stu-id="b6ad9-106">Once you've uploaded your VHD file, the [Next steps section](#next-steps) lists some articles that illustrate how to create a custom image from the uploaded VHD file.</span></span> <span data-ttu-id="b6ad9-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span><span class="sxs-lookup"><span data-stu-id="b6ad9-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="b6ad9-108">Step-by-step instructions</span><span class="sxs-lookup"><span data-stu-id="b6ad9-108">Step-by-step instructions</span></span>

<span data-ttu-id="b6ad9-109">The following steps walk you through uploading a VHD file to DevTest Labs using [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="b6ad9-109">The following steps walk you through uploading a VHD file to DevTest Labs using [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>

1. <span data-ttu-id="b6ad9-110">[Download and install the latest version of the Microsoft Azure Storage Explorer](http://www.storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="b6ad9-110">[Download and install the latest version of the Microsoft Azure Storage Explorer](http://www.storageexplorer.com).</span></span>

1. <span data-ttu-id="b6ad9-111">Get the name of the lab's storage account using the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="b6ad9-111">Get the name of the lab's storage account using the Azure portal:</span></span>

    1. <span data-ttu-id="b6ad9-112">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="b6ad9-112">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
    
    1. <span data-ttu-id="b6ad9-113">Select **All services**, and then select **DevTest Labs** from the list.</span><span class="sxs-lookup"><span data-stu-id="b6ad9-113">Select **All services**, and then select **DevTest Labs** from the list.</span></span>
    
    1. <span data-ttu-id="b6ad9-114">From the list of labs, select the desired lab.</span><span class="sxs-lookup"><span data-stu-id="b6ad9-114">From the list of labs, select the desired lab.</span></span>  
    
    1. <span data-ttu-id="b6ad9-115">On the lab's blade, select **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="b6ad9-115">On the lab's blade, select **Configuration**.</span></span> 
    
    1. <span data-ttu-id="b6ad9-116">On the lab **Configuration** blade, select **Custom images (VHDs)**.</span><span class="sxs-lookup"><span data-stu-id="b6ad9-116">On the lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>
    
    1. <span data-ttu-id="b6ad9-117">On the **Custom images** blade, Select **+Add**.</span><span class="sxs-lookup"><span data-stu-id="b6ad9-117">On the **Custom images** blade, Select **+Add**.</span></span> 
    
    1. <span data-ttu-id="b6ad9-118">On the **Custom image** blade, select **VHD**.</span><span class="sxs-lookup"><span data-stu-id="b6ad9-118">On the **Custom image** blade, select **VHD**.</span></span>
    
    1. <span data-ttu-id="b6ad9-119">On the **VHD** blade, select **Upload a VHD using PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="b6ad9-119">On the **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>
    
        ![Upload VHD using PowerShell][0]
    
    1. <span data-ttu-id="b6ad9-121">The **Upload an image using PowerShell** blade displays a call to the **Add-AzureVhd** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b6ad9-121">The **Upload an image using PowerShell** blade displays a call to the **Add-AzureVhd** cmdlet.</span></span> <span data-ttu-id="b6ad9-122">The first parameter (*Destination*) contains the storage account name for the lab in the following format:</span><span class="sxs-lookup"><span data-stu-id="b6ad9-122">The first parameter (*Destination*) contains the storage account name for the lab in the following format:</span></span>
    
        <span data-ttu-id="b6ad9-123">https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...</span><span class="sxs-lookup"><span data-stu-id="b6ad9-123">https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...</span></span> 

    1. <span data-ttu-id="b6ad9-124">Make note of the storage account name as it is used in later steps.</span><span class="sxs-lookup"><span data-stu-id="b6ad9-124">Make note of the storage account name as it is used in later steps.</span></span>
    
1. <span data-ttu-id="b6ad9-125">Connect to an Azure subscription account using Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="b6ad9-125">Connect to an Azure subscription account using Storage Explorer.</span></span>

    > [!TIP] 
    > 
    > <span data-ttu-id="b6ad9-126">Storage Explorer supports several connection options.</span><span class="sxs-lookup"><span data-stu-id="b6ad9-126">Storage Explorer supports several connection options.</span></span> <span data-ttu-id="b6ad9-127">This section illustrates connecting to a storage account associated with your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="b6ad9-127">This section illustrates connecting to a storage account associated with your Azure subscription.</span></span> <span data-ttu-id="b6ad9-128">To see the other connection options supported by Storage Explorer, refer to the article, [Getting started with Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="b6ad9-128">To see the other connection options supported by Storage Explorer, refer to the article, [Getting started with Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>
 
    1. <span data-ttu-id="b6ad9-129">Open Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="b6ad9-129">Open Storage Explorer.</span></span>
    
    1. <span data-ttu-id="b6ad9-130">In Storage Explorer, select **Azure Account settings**.</span><span class="sxs-lookup"><span data-stu-id="b6ad9-130">In Storage Explorer, select **Azure Account settings**.</span></span> 
    
        ![Azure account settings][1]
    
    1. <span data-ttu-id="b6ad9-132">The left pane displays the Microsoft accounts you've logged in to.</span><span class="sxs-lookup"><span data-stu-id="b6ad9-132">The left pane displays the Microsoft accounts you've logged in to.</span></span> <span data-ttu-id="b6ad9-133">To connect to another account, select **Add an account**, and follow the dialogs to sign in with a Microsoft account that is associated with at least one active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="b6ad9-133">To connect to another account, select **Add an account**, and follow the dialogs to sign in with a Microsoft account that is associated with at least one active Azure subscription.</span></span>
    
        ![Add an account][2]
    
    1. <span data-ttu-id="b6ad9-135">Once you successfully sign in with a Microsoft account, the left pane populates with the Azure subscriptions associated with that account.</span><span class="sxs-lookup"><span data-stu-id="b6ad9-135">Once you successfully sign in with a Microsoft account, the left pane populates with the Azure subscriptions associated with that account.</span></span> <span data-ttu-id="b6ad9-136">Select the Azure subscriptions with which you want to work, and then select **Apply**.</span><span class="sxs-lookup"><span data-stu-id="b6ad9-136">Select the Azure subscriptions with which you want to work, and then select **Apply**.</span></span> <span data-ttu-id="b6ad9-137">(Selecting **All subscriptions** toggles the selection of all or none of the listed Azure subscriptions.)</span><span class="sxs-lookup"><span data-stu-id="b6ad9-137">(Selecting **All subscriptions** toggles the selection of all or none of the listed Azure subscriptions.)</span></span>
    
        ![Select Azure subscriptions][3]
    
    1. <span data-ttu-id="b6ad9-139">The left pane displays the storage accounts associated with the selected Azure subscriptions.</span><span class="sxs-lookup"><span data-stu-id="b6ad9-139">The left pane displays the storage accounts associated with the selected Azure subscriptions.</span></span>
    
        ![Selected Azure subscriptions][4]

1. <span data-ttu-id="b6ad9-141">Locate the lab's storage account:</span><span class="sxs-lookup"><span data-stu-id="b6ad9-141">Locate the lab's storage account:</span></span>

    1. <span data-ttu-id="b6ad9-142">In the Storage Explorer left pane, locate, and expand the node for the Azure subscription that owns the lab.</span><span class="sxs-lookup"><span data-stu-id="b6ad9-142">In the Storage Explorer left pane, locate, and expand the node for the Azure subscription that owns the lab.</span></span>
    
    1. <span data-ttu-id="b6ad9-143">Under the subscription's node, expand **Storage Accounts**.</span><span class="sxs-lookup"><span data-stu-id="b6ad9-143">Under the subscription's node, expand **Storage Accounts**.</span></span>

    1. <span data-ttu-id="b6ad9-144">Expand the lab's storage account node to reveal nodes for **Blob Containers**, **File Shares**, **Queues**, and **Tables**.</span><span class="sxs-lookup"><span data-stu-id="b6ad9-144">Expand the lab's storage account node to reveal nodes for **Blob Containers**, **File Shares**, **Queues**, and **Tables**.</span></span>
    
    1. <span data-ttu-id="b6ad9-145">Expand the **Blob Containers** node.</span><span class="sxs-lookup"><span data-stu-id="b6ad9-145">Expand the **Blob Containers** node.</span></span>
    
    1. <span data-ttu-id="b6ad9-146">Select the uploads blob container to display its contents in the right pane.</span><span class="sxs-lookup"><span data-stu-id="b6ad9-146">Select the uploads blob container to display its contents in the right pane.</span></span>
        
        ![Upload directory][5]

1. <span data-ttu-id="b6ad9-148">Upload the VHD file using Storage Explorer:</span><span class="sxs-lookup"><span data-stu-id="b6ad9-148">Upload the VHD file using Storage Explorer:</span></span>

    1. <span data-ttu-id="b6ad9-149">In the Storage Explorer right pane, you should see a listing of the blobs in the **uploads** blob container of the lab's storage account.</span><span class="sxs-lookup"><span data-stu-id="b6ad9-149">In the Storage Explorer right pane, you should see a listing of the blobs in the **uploads** blob container of the lab's storage account.</span></span> <span data-ttu-id="b6ad9-150">On the blob editor toolbar, select **Upload**</span><span class="sxs-lookup"><span data-stu-id="b6ad9-150">On the blob editor toolbar, select **Upload**</span></span> 
        
        ![Upload button][6]
    
    1. <span data-ttu-id="b6ad9-152">From the **Upload** drop-down menu, select **Upload files...**.</span><span class="sxs-lookup"><span data-stu-id="b6ad9-152">From the **Upload** drop-down menu, select **Upload files...**.</span></span>
    
    1. <span data-ttu-id="b6ad9-153">On the **Upload files** dialog, select the ellipsis.</span><span class="sxs-lookup"><span data-stu-id="b6ad9-153">On the **Upload files** dialog, select the ellipsis.</span></span>
        
        ![Select file][8]  

    1. <span data-ttu-id="b6ad9-155">On the **Select files to upload** dialog, browse to the desired VHD file, select it, and then select **Open**.</span><span class="sxs-lookup"><span data-stu-id="b6ad9-155">On the **Select files to upload** dialog, browse to the desired VHD file, select it, and then select **Open**.</span></span>
    
    1. <span data-ttu-id="b6ad9-156">When returned to the **Upload files** dialog, change **Blob type** to **Page Blob**.</span><span class="sxs-lookup"><span data-stu-id="b6ad9-156">When returned to the **Upload files** dialog, change **Blob type** to **Page Blob**.</span></span>
    
    1. <span data-ttu-id="b6ad9-157">Select **Upload**.</span><span class="sxs-lookup"><span data-stu-id="b6ad9-157">Select **Upload**.</span></span>

        ![Select file][9]  
    
    1. <span data-ttu-id="b6ad9-159">The Storage Explorer **Activity Log** pane shows the download status (along with links to cancel the upload).</span><span class="sxs-lookup"><span data-stu-id="b6ad9-159">The Storage Explorer **Activity Log** pane shows the download status (along with links to cancel the upload).</span></span> <span data-ttu-id="b6ad9-160">The process of uploading a VHD file can be lengthy depending on the size of the VHD file and your connection speed.</span><span class="sxs-lookup"><span data-stu-id="b6ad9-160">The process of uploading a VHD file can be lengthy depending on the size of the VHD file and your connection speed.</span></span> 

        ![Upload-file status][10]  

## <a name="next-steps"></a><span data-ttu-id="b6ad9-162">Next steps</span><span class="sxs-lookup"><span data-stu-id="b6ad9-162">Next steps</span></span>

- [<span data-ttu-id="b6ad9-163">Create a custom image in Azure DevTest Labs from a VHD file using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="b6ad9-163">Create a custom image in Azure DevTest Labs from a VHD file using the Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="b6ad9-164">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span><span class="sxs-lookup"><span data-stu-id="b6ad9-164">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)

[0]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-image-using-psh.png
[1]: ./media/devtest-lab-upload-vhd-using-storage-explorer/settings-icon.png
[2]: ./media/devtest-lab-upload-vhd-using-storage-explorer/add-account-link.png
[3]: ./media/devtest-lab-upload-vhd-using-storage-explorer/subscriptions-list.png
[4]: ./media/devtest-lab-upload-vhd-using-storage-explorer/storage-accounts-list.png
[5]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-dir.png
[6]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-button.png
[7]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-files.png
[8]: ./media/devtest-lab-upload-vhd-using-storage-explorer/select-file.png
[9]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-file.png
[10]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-status.png
