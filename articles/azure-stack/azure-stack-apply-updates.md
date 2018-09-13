---
title: Apply updates in Azure Stack | Microsoft Docs
description: Learn how to import and install Microsoft update packages for an Azure Stack integrated system.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.assetid: 449ae53e-b951-401a-b2c9-17fee2f491f1
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/07/2018
ms.author: mabrigg
ms.openlocfilehash: 8e4c86a3c9ff40f23a2a758b450d685b81dabc1a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856549"
---
# <a name="apply-updates-in-azure-stack"></a><span data-ttu-id="fa5a2-103">Apply updates in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="fa5a2-103">Apply updates in Azure Stack</span></span>

<span data-ttu-id="fa5a2-104">*Applies to: Azure Stack integrated systems*</span><span class="sxs-lookup"><span data-stu-id="fa5a2-104">*Applies to: Azure Stack integrated systems*</span></span>

<span data-ttu-id="fa5a2-105">As an Azure Stack operator, you can apply Microsoft or OEM update packages for Azure Stack by using the Update tile in the administrator portal.</span><span class="sxs-lookup"><span data-stu-id="fa5a2-105">As an Azure Stack operator, you can apply Microsoft or OEM update packages for Azure Stack by using the Update tile in the administrator portal.</span></span> <span data-ttu-id="fa5a2-106">You must download the update package, import the package files to Azure Stack, and then install the update package.</span><span class="sxs-lookup"><span data-stu-id="fa5a2-106">You must download the update package, import the package files to Azure Stack, and then install the update package.</span></span> 

## <a name="download-the-update-package"></a><span data-ttu-id="fa5a2-107">Download the update package</span><span class="sxs-lookup"><span data-stu-id="fa5a2-107">Download the update package</span></span>

<span data-ttu-id="fa5a2-108">When a Microsoft or OEM update package for Azure Stack is available, download the package to a location that's reachable from Azure Stack, and review the package contents.</span><span class="sxs-lookup"><span data-stu-id="fa5a2-108">When a Microsoft or OEM update package for Azure Stack is available, download the package to a location that's reachable from Azure Stack, and review the package contents.</span></span> <span data-ttu-id="fa5a2-109">An update package typically consists of the following files:</span><span class="sxs-lookup"><span data-stu-id="fa5a2-109">An update package typically consists of the following files:</span></span>

- <span data-ttu-id="fa5a2-110">A self-extracting *PackageName*.exe file.</span><span class="sxs-lookup"><span data-stu-id="fa5a2-110">A self-extracting *PackageName*.exe file.</span></span> <span data-ttu-id="fa5a2-111">This file contains the payload for the update, for example the latest cumulative update for Windows Server.</span><span class="sxs-lookup"><span data-stu-id="fa5a2-111">This file contains the payload for the update, for example the latest cumulative update for Windows Server.</span></span>   
- <span data-ttu-id="fa5a2-112">Corresponding *PackageName*.bin files.</span><span class="sxs-lookup"><span data-stu-id="fa5a2-112">Corresponding *PackageName*.bin files.</span></span> <span data-ttu-id="fa5a2-113">These files provide compression for the payload that's associated with the *PackageName*.exe file.</span><span class="sxs-lookup"><span data-stu-id="fa5a2-113">These files provide compression for the payload that's associated with the *PackageName*.exe file.</span></span> 
- <span data-ttu-id="fa5a2-114">A Metadata.xml file.</span><span class="sxs-lookup"><span data-stu-id="fa5a2-114">A Metadata.xml file.</span></span> <span data-ttu-id="fa5a2-115">This file contains essential information about the update, for example the publisher, name, prerequisite, size, and support path URL.</span><span class="sxs-lookup"><span data-stu-id="fa5a2-115">This file contains essential information about the update, for example the publisher, name, prerequisite, size, and support path URL.</span></span>

## <a name="import-and-install-updates"></a><span data-ttu-id="fa5a2-116">Import and install updates</span><span class="sxs-lookup"><span data-stu-id="fa5a2-116">Import and install updates</span></span>

<span data-ttu-id="fa5a2-117">The following procedure shows how to import and install update packages in the administrator portal.</span><span class="sxs-lookup"><span data-stu-id="fa5a2-117">The following procedure shows how to import and install update packages in the administrator portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fa5a2-118">We strongly recommend that you notify users of any maintenance operations, and that you schedule normal maintenance windows during non-business hours as much as possible.</span><span class="sxs-lookup"><span data-stu-id="fa5a2-118">We strongly recommend that you notify users of any maintenance operations, and that you schedule normal maintenance windows during non-business hours as much as possible.</span></span> <span data-ttu-id="fa5a2-119">Maintenance operations may affect both user workloads and portal operations.</span><span class="sxs-lookup"><span data-stu-id="fa5a2-119">Maintenance operations may affect both user workloads and portal operations.</span></span>

1. <span data-ttu-id="fa5a2-120">In the administrator portal, select **All services**.</span><span class="sxs-lookup"><span data-stu-id="fa5a2-120">In the administrator portal, select **All services**.</span></span> <span data-ttu-id="fa5a2-121">Then, under the **DATA + STORAGE** category, select **Storage accounts**.</span><span class="sxs-lookup"><span data-stu-id="fa5a2-121">Then, under the **DATA + STORAGE** category, select **Storage accounts**.</span></span> <span data-ttu-id="fa5a2-122">(Or, in the filter box, start typing **storage accounts**, and select it.)</span><span class="sxs-lookup"><span data-stu-id="fa5a2-122">(Or, in the filter box, start typing **storage accounts**, and select it.)</span></span>

    ![Shows where to find storage accounts in the portal](media/azure-stack-apply-updates/ApplyUpdates1.png)

2. <span data-ttu-id="fa5a2-124">In the filter box, type **update**, and select the **updateadminaccount** storage account.</span><span class="sxs-lookup"><span data-stu-id="fa5a2-124">In the filter box, type **update**, and select the **updateadminaccount** storage account.</span></span>

    ![Shows how to search for updateadminaccount](media/azure-stack-apply-updates/ApplyUpdates2.png)

3. <span data-ttu-id="fa5a2-126">In the storage account details, under **Services**, select **Blobs**.</span><span class="sxs-lookup"><span data-stu-id="fa5a2-126">In the storage account details, under **Services**, select **Blobs**.</span></span>
 
    ![Shows how to get to Blobs for the storage account](media/azure-stack-apply-updates/ApplyUpdates3.png) 
 
4. <span data-ttu-id="fa5a2-128">Under **Blob service**, select **+ Container** to create a  container.</span><span class="sxs-lookup"><span data-stu-id="fa5a2-128">Under **Blob service**, select **+ Container** to create a  container.</span></span> <span data-ttu-id="fa5a2-129">Enter a name (for example *Update-1709*), and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="fa5a2-129">Enter a name (for example *Update-1709*), and then select **OK**.</span></span>
 
     ![Shows how to add a container in the storage account](media/azure-stack-apply-updates/ApplyUpdates4.png)

5. <span data-ttu-id="fa5a2-131">After the container is created, click the container name, and then click **Upload** to upload the package files to the container.</span><span class="sxs-lookup"><span data-stu-id="fa5a2-131">After the container is created, click the container name, and then click **Upload** to upload the package files to the container.</span></span>
 
    ![Shows how to upload the package files](media/azure-stack-apply-updates/ApplyUpdates5.png)

6. <span data-ttu-id="fa5a2-133">Under **Upload blob**, click the folder icon, browse to the update package's .exe file, and then click **Open** in the file explorer window.</span><span class="sxs-lookup"><span data-stu-id="fa5a2-133">Under **Upload blob**, click the folder icon, browse to the update package's .exe file, and then click **Open** in the file explorer window.</span></span>
  
7. <span data-ttu-id="fa5a2-134">Under **Upload blob**, click **Upload**.</span><span class="sxs-lookup"><span data-stu-id="fa5a2-134">Under **Upload blob**, click **Upload**.</span></span> 
  
    ![Shows where to upload each package file](media/azure-stack-apply-updates/ApplyUpdates6.png)

8. <span data-ttu-id="fa5a2-136">Repeat steps 6 and 7 for the *PackageName*.bin and Metadata.xml files.</span><span class="sxs-lookup"><span data-stu-id="fa5a2-136">Repeat steps 6 and 7 for the *PackageName*.bin and Metadata.xml files.</span></span> <span data-ttu-id="fa5a2-137">Do not import the Supplemental Notice.txt file if included.</span><span class="sxs-lookup"><span data-stu-id="fa5a2-137">Do not import the Supplemental Notice.txt file if included.</span></span>
9. <span data-ttu-id="fa5a2-138">When done, you can review the notifications (bell icon in the top-right corner of the portal).</span><span class="sxs-lookup"><span data-stu-id="fa5a2-138">When done, you can review the notifications (bell icon in the top-right corner of the portal).</span></span> <span data-ttu-id="fa5a2-139">The notifications should indicate that the upload has completed.</span><span class="sxs-lookup"><span data-stu-id="fa5a2-139">The notifications should indicate that the upload has completed.</span></span> 
10. <span data-ttu-id="fa5a2-140">Navigate back to the Update tile on the dashboard.</span><span class="sxs-lookup"><span data-stu-id="fa5a2-140">Navigate back to the Update tile on the dashboard.</span></span> <span data-ttu-id="fa5a2-141">The tile should indicate that an update is available.</span><span class="sxs-lookup"><span data-stu-id="fa5a2-141">The tile should indicate that an update is available.</span></span> <span data-ttu-id="fa5a2-142">Click the tile to review the newly added update package.</span><span class="sxs-lookup"><span data-stu-id="fa5a2-142">Click the tile to review the newly added update package.</span></span>
11. <span data-ttu-id="fa5a2-143">To install the update, select the package that's marked as **Ready** and either right-click the package and select **Update now**, or click the **Update now** action near the top.</span><span class="sxs-lookup"><span data-stu-id="fa5a2-143">To install the update, select the package that's marked as **Ready** and either right-click the package and select **Update now**, or click the **Update now** action near the top.</span></span>
12. <span data-ttu-id="fa5a2-144">When you click the installing update package, you can view the status in the **Update run details** area.</span><span class="sxs-lookup"><span data-stu-id="fa5a2-144">When you click the installing update package, you can view the status in the **Update run details** area.</span></span> <span data-ttu-id="fa5a2-145">From here, you can also click **Download full logs** to download the log files.</span><span class="sxs-lookup"><span data-stu-id="fa5a2-145">From here, you can also click **Download full logs** to download the log files.</span></span>
13. <span data-ttu-id="fa5a2-146">When the update completes, the Update tile shows the updated Azure Stack version.</span><span class="sxs-lookup"><span data-stu-id="fa5a2-146">When the update completes, the Update tile shows the updated Azure Stack version.</span></span>

<span data-ttu-id="fa5a2-147">You can manually delete updates from the storage account after they have been installed on Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="fa5a2-147">You can manually delete updates from the storage account after they have been installed on Azure Stack.</span></span> <span data-ttu-id="fa5a2-148">Azure Stack periodically checks for older update packages and removes them from storage.</span><span class="sxs-lookup"><span data-stu-id="fa5a2-148">Azure Stack periodically checks for older update packages and removes them from storage.</span></span> <span data-ttu-id="fa5a2-149">It may take Azure Stack two weeks to remove the old packages.</span><span class="sxs-lookup"><span data-stu-id="fa5a2-149">It may take Azure Stack two weeks to remove the old packages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa5a2-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="fa5a2-150">Next steps</span></span>

- [<span data-ttu-id="fa5a2-151">Manage updates in Azure Stack overview</span><span class="sxs-lookup"><span data-stu-id="fa5a2-151">Manage updates in Azure Stack overview</span></span>](azure-stack-updates.md)
- [<span data-ttu-id="fa5a2-152">Azure Stack servicing policy</span><span class="sxs-lookup"><span data-stu-id="fa5a2-152">Azure Stack servicing policy</span></span>](azure-stack-servicing-policy.md)
