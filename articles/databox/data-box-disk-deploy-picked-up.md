---
title: Ship Microsoft Azure Data Box Disk back| Microsoft Docs
description: Use this tutorial to learn how to ship your Azure Data Box Disk to Microsoft
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
ms.date: 07/10/2018
ms.author: alkohli
Customer intent: As an IT admin, I need to be able to order Data Box Disk to upload on-premises data from my server onto Azure.
ms.openlocfilehash: 783c837bbb9ce22e7354252523e6725753776836
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966608"
---
# <a name="tutorial-return-azure-data-box-disk-and-verify-data-upload-to-azure"></a><span data-ttu-id="a5988-103">Tutorial: Return Azure Data Box Disk and verify data upload to Azure</span><span class="sxs-lookup"><span data-stu-id="a5988-103">Tutorial: Return Azure Data Box Disk and verify data upload to Azure</span></span>

<span data-ttu-id="a5988-104">This is the last tutorial of the series: Deploy Azure Data Box Disk.</span><span class="sxs-lookup"><span data-stu-id="a5988-104">This is the last tutorial of the series: Deploy Azure Data Box Disk.</span></span> <span data-ttu-id="a5988-105">In this tutorial, you will learn how to:</span><span class="sxs-lookup"><span data-stu-id="a5988-105">In this tutorial, you will learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a5988-106">Ship Data Box Disk to Microsoft</span><span class="sxs-lookup"><span data-stu-id="a5988-106">Ship Data Box Disk to Microsoft</span></span>
> * <span data-ttu-id="a5988-107">Verify data upload to Azure</span><span class="sxs-lookup"><span data-stu-id="a5988-107">Verify data upload to Azure</span></span>
> * <span data-ttu-id="a5988-108">Erasure of data from Data Box Disk</span><span class="sxs-lookup"><span data-stu-id="a5988-108">Erasure of data from Data Box Disk</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a5988-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a5988-109">Prerequisites</span></span>

<span data-ttu-id="a5988-110">Before you begin, make sure that you have completed the [Tutorial: Copy data to Azure Data Box Disk and verify](data-box-disk-deploy-copy-data.md).</span><span class="sxs-lookup"><span data-stu-id="a5988-110">Before you begin, make sure that you have completed the [Tutorial: Copy data to Azure Data Box Disk and verify](data-box-disk-deploy-copy-data.md).</span></span>

## <a name="ship-data-box-disk-back"></a><span data-ttu-id="a5988-111">Ship Data Box Disk back</span><span class="sxs-lookup"><span data-stu-id="a5988-111">Ship Data Box Disk back</span></span>

1. <span data-ttu-id="a5988-112">Once the data validation is complete, unplug the disks.</span><span class="sxs-lookup"><span data-stu-id="a5988-112">Once the data validation is complete, unplug the disks.</span></span> <span data-ttu-id="a5988-113">Remove the connecting cables.</span><span class="sxs-lookup"><span data-stu-id="a5988-113">Remove the connecting cables.</span></span>
2. <span data-ttu-id="a5988-114">Wrap all the disks and the connecting cables with a bubble wrap and place those into the shipping box.</span><span class="sxs-lookup"><span data-stu-id="a5988-114">Wrap all the disks and the connecting cables with a bubble wrap and place those into the shipping box.</span></span>
3. <span data-ttu-id="a5988-115">Use the return shipping label in the clear plastic sleeve affixed to the box.</span><span class="sxs-lookup"><span data-stu-id="a5988-115">Use the return shipping label in the clear plastic sleeve affixed to the box.</span></span> <span data-ttu-id="a5988-116">If the label is damaged or lost, download a new shipping label from the Azure portal and affix on the device.</span><span class="sxs-lookup"><span data-stu-id="a5988-116">If the label is damaged or lost, download a new shipping label from the Azure portal and affix on the device.</span></span> <span data-ttu-id="a5988-117">Go to **Overview > Download shipping label**.</span><span class="sxs-lookup"><span data-stu-id="a5988-117">Go to **Overview > Download shipping label**.</span></span> 

    ![Download shipping label](media/data-box-disk-deploy-picked-up/download-shipping-label.png)

    <span data-ttu-id="a5988-119">This action downloads a return shipping label as shown below.</span><span class="sxs-lookup"><span data-stu-id="a5988-119">This action downloads a return shipping label as shown below.</span></span>

    ![Example shipping label](media/data-box-disk-deploy-picked-up/exmple-shipping-label.png)

4. <span data-ttu-id="a5988-121">Seal the shipping box and ensure that the return shipping label is visible.</span><span class="sxs-lookup"><span data-stu-id="a5988-121">Seal the shipping box and ensure that the return shipping label is visible.</span></span>
5. <span data-ttu-id="a5988-122">Schedule a pickup with UPS if returning the device in US.</span><span class="sxs-lookup"><span data-stu-id="a5988-122">Schedule a pickup with UPS if returning the device in US.</span></span> <span data-ttu-id="a5988-123">If you are returning the device in Europe with DHL, request for pickup from DHL by visiting their website and specifying the airway bill number.</span><span class="sxs-lookup"><span data-stu-id="a5988-123">If you are returning the device in Europe with DHL, request for pickup from DHL by visiting their website and specifying the airway bill number.</span></span> <span data-ttu-id="a5988-124">Go to the country DHL Express website and choose **Book a Courier Collection > eReturn Shipment**.</span><span class="sxs-lookup"><span data-stu-id="a5988-124">Go to the country DHL Express website and choose **Book a Courier Collection > eReturn Shipment**.</span></span>

    ![DHL ereturn shipment](media/data-box-disk-deploy-picked-up/dhl-ship-1.png)
    
    <span data-ttu-id="a5988-126">Specify the waybill number and click **Schedule Pickup** to arrange for pickup.</span><span class="sxs-lookup"><span data-stu-id="a5988-126">Specify the waybill number and click **Schedule Pickup** to arrange for pickup.</span></span>

      ![Schedule pickup](media/data-box-disk-deploy-picked-up/dhl-ship-2.png)

7. <span data-ttu-id="a5988-128">Once the disks are picked up by your carrier, the order status in the portal updates to **Picked up**.</span><span class="sxs-lookup"><span data-stu-id="a5988-128">Once the disks are picked up by your carrier, the order status in the portal updates to **Picked up**.</span></span> <span data-ttu-id="a5988-129">A tracking ID is also displayed.</span><span class="sxs-lookup"><span data-stu-id="a5988-129">A tracking ID is also displayed.</span></span>

    ![Disks picked up](media/data-box-disk-deploy-picked-up/data-box-portal-pickedup.png)

## <a name="verify-data-upload-to-azure"></a><span data-ttu-id="a5988-131">Verify data upload to Azure</span><span class="sxs-lookup"><span data-stu-id="a5988-131">Verify data upload to Azure</span></span>

<span data-ttu-id="a5988-132">When Microsoft receives and scans the disk, job status is updated to **Received**.</span><span class="sxs-lookup"><span data-stu-id="a5988-132">When Microsoft receives and scans the disk, job status is updated to **Received**.</span></span> 

![Disks received](media/data-box-disk-deploy-picked-up/data-box-portal-received.png)

<span data-ttu-id="a5988-134">The data automatically gets copied once the disks are connected to a server in the Azure datacenter.</span><span class="sxs-lookup"><span data-stu-id="a5988-134">The data automatically gets copied once the disks are connected to a server in the Azure datacenter.</span></span> <span data-ttu-id="a5988-135">Depending upon the data size, the copy operation may take a few hours to days to complete.</span><span class="sxs-lookup"><span data-stu-id="a5988-135">Depending upon the data size, the copy operation may take a few hours to days to complete.</span></span> <span data-ttu-id="a5988-136">You can monitor the copy job progress in the portal.</span><span class="sxs-lookup"><span data-stu-id="a5988-136">You can monitor the copy job progress in the portal.</span></span>

<span data-ttu-id="a5988-137">Once the copy is complete, order status updates to **Completed**.</span><span class="sxs-lookup"><span data-stu-id="a5988-137">Once the copy is complete, order status updates to **Completed**.</span></span>

![Data copy completed](media/data-box-disk-deploy-picked-up/data-box-portal-completed.png)

<span data-ttu-id="a5988-139">Verify that your data is in the storage account(s) before you delete it from the source.</span><span class="sxs-lookup"><span data-stu-id="a5988-139">Verify that your data is in the storage account(s) before you delete it from the source.</span></span> <span data-ttu-id="a5988-140">To verify that the data has uploaded into Azure, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a5988-140">To verify that the data has uploaded into Azure, perform the following steps:</span></span>

1. <span data-ttu-id="a5988-141">Go to the storage account associated with your disk order.</span><span class="sxs-lookup"><span data-stu-id="a5988-141">Go to the storage account associated with your disk order.</span></span>
2. <span data-ttu-id="a5988-142">Go to **Blob service > Browse blobs**.</span><span class="sxs-lookup"><span data-stu-id="a5988-142">Go to **Blob service > Browse blobs**.</span></span> <span data-ttu-id="a5988-143">The list of containers is presented.</span><span class="sxs-lookup"><span data-stu-id="a5988-143">The list of containers is presented.</span></span> <span data-ttu-id="a5988-144">Corresponding to the subfolder that you created under *BlockBlob* and *PageBlob* folders, containers with the same name are created in your storage account.</span><span class="sxs-lookup"><span data-stu-id="a5988-144">Corresponding to the subfolder that you created under *BlockBlob* and *PageBlob* folders, containers with the same name are created in your storage account.</span></span>
    <span data-ttu-id="a5988-145">If the folder names do not conform to Azure naming conventions, then the data upload to Azure will fail.</span><span class="sxs-lookup"><span data-stu-id="a5988-145">If the folder names do not conform to Azure naming conventions, then the data upload to Azure will fail.</span></span>

4. <span data-ttu-id="a5988-146">To verify that the entire dataset has loaded, use Microsoft Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="a5988-146">To verify that the entire dataset has loaded, use Microsoft Azure Storage Explorer.</span></span> <span data-ttu-id="a5988-147">Attach the storage account corresponding to the disk rental order and then look at the list of blob containers.</span><span class="sxs-lookup"><span data-stu-id="a5988-147">Attach the storage account corresponding to the disk rental order and then look at the list of blob containers.</span></span> <span data-ttu-id="a5988-148">Select a container, click **…More** and then click **Folder statistics**.</span><span class="sxs-lookup"><span data-stu-id="a5988-148">Select a container, click **…More** and then click **Folder statistics**.</span></span> <span data-ttu-id="a5988-149">In the **Activities** pane, the statistics for that folder including the number of blobs and the total blob size is displayed.</span><span class="sxs-lookup"><span data-stu-id="a5988-149">In the **Activities** pane, the statistics for that folder including the number of blobs and the total blob size is displayed.</span></span> <span data-ttu-id="a5988-150">The total blob size in bytes should match the size of the dataset.</span><span class="sxs-lookup"><span data-stu-id="a5988-150">The total blob size in bytes should match the size of the dataset.</span></span>

    ![Folder statistics in Storage Explorer](media/data-box-disk-deploy-picked-up/folder-statistics-storage-explorer.png)

## <a name="erasure-of-data-from-data-box-disk"></a><span data-ttu-id="a5988-152">Erasure of data from Data Box Disk</span><span class="sxs-lookup"><span data-stu-id="a5988-152">Erasure of data from Data Box Disk</span></span>

<span data-ttu-id="a5988-153">Once the copy is complete and you have verified that data is in the Azure storage account, disks are securely erased as per the NIST standard.</span><span class="sxs-lookup"><span data-stu-id="a5988-153">Once the copy is complete and you have verified that data is in the Azure storage account, disks are securely erased as per the NIST standard.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a5988-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="a5988-154">Next steps</span></span>

<span data-ttu-id="a5988-155">In this tutorial, you learned about Azure Data Box Disk topics such as:</span><span class="sxs-lookup"><span data-stu-id="a5988-155">In this tutorial, you learned about Azure Data Box Disk topics such as:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a5988-156">Ship Data Box Disk to Microsoft</span><span class="sxs-lookup"><span data-stu-id="a5988-156">Ship Data Box Disk to Microsoft</span></span>
> * <span data-ttu-id="a5988-157">Verify data upload to Azure</span><span class="sxs-lookup"><span data-stu-id="a5988-157">Verify data upload to Azure</span></span>
> * <span data-ttu-id="a5988-158">Erasure of data from Data Box Disk</span><span class="sxs-lookup"><span data-stu-id="a5988-158">Erasure of data from Data Box Disk</span></span>


<span data-ttu-id="a5988-159">Advance to the next how-to to learn how to manage Data Box Disk via the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a5988-159">Advance to the next how-to to learn how to manage Data Box Disk via the Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a5988-160">Use Azure portal to administer Azure Data Box Disk</span><span class="sxs-lookup"><span data-stu-id="a5988-160">Use Azure portal to administer Azure Data Box Disk</span></span>](./data-box-portal-ui-admin.md)


