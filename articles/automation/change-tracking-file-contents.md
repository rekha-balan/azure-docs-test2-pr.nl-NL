---
title: View file content changes with Azure Automation
description: Use the file content change feature of Change tracking to view the contents of a file that has changed.
services: automation
ms.service: automation
ms.component: change-inventory-management
author: georgewallace
ms.author: gwallace
ms.date: 07/03/2018
ms.topic: conceptual
manager: carmonm
ms.openlocfilehash: 0582505d66bbef3064359fa4047676c4ba60b4e9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855924"
---
# <a name="view-contents-of-a-file-that-is-being-tracked-with-change-tracking"></a><span data-ttu-id="4e73c-103">View contents of a file that is being tracked with Change Tracking</span><span class="sxs-lookup"><span data-stu-id="4e73c-103">View contents of a file that is being tracked with Change Tracking</span></span>

<span data-ttu-id="4e73c-104">File content tracking allows you to view the contents of a file before and after a change that is being tracked with Change Tracking.</span><span class="sxs-lookup"><span data-stu-id="4e73c-104">File content tracking allows you to view the contents of a file before and after a change that is being tracked with Change Tracking.</span></span> <span data-ttu-id="4e73c-105">To do this, it saves the file contents to a storage account after each change occurs.</span><span class="sxs-lookup"><span data-stu-id="4e73c-105">To do this, it saves the file contents to a storage account after each change occurs.</span></span>

## <a name="requirements"></a><span data-ttu-id="4e73c-106">Requirements</span><span class="sxs-lookup"><span data-stu-id="4e73c-106">Requirements</span></span>

* <span data-ttu-id="4e73c-107">A standard storage account using the Resource Manager deployment model is required for storing file content.</span><span class="sxs-lookup"><span data-stu-id="4e73c-107">A standard storage account using the Resource Manager deployment model is required for storing file content.</span></span> <span data-ttu-id="4e73c-108">Premium and classic deployment model storage accounts should not be used.</span><span class="sxs-lookup"><span data-stu-id="4e73c-108">Premium and classic deployment model storage accounts should not be used.</span></span> <span data-ttu-id="4e73c-109">For more information on storage accounts, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md)</span><span class="sxs-lookup"><span data-stu-id="4e73c-109">For more information on storage accounts, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md)</span></span>

* <span data-ttu-id="4e73c-110">The storage account used can only have 1 Automation Account connected.</span><span class="sxs-lookup"><span data-stu-id="4e73c-110">The storage account used can only have 1 Automation Account connected.</span></span>

* <span data-ttu-id="4e73c-111">[Change Tracking](automation-change-tracking.md) is enabled in your Automation Account.</span><span class="sxs-lookup"><span data-stu-id="4e73c-111">[Change Tracking](automation-change-tracking.md) is enabled in your Automation Account.</span></span>

## <a name="enable-file-content-tracking"></a><span data-ttu-id="4e73c-112">Enable file content tracking</span><span class="sxs-lookup"><span data-stu-id="4e73c-112">Enable file content tracking</span></span>

1. <span data-ttu-id="4e73c-113">In the Azure portal, open your Automation account, and then select **Change tracking**.</span><span class="sxs-lookup"><span data-stu-id="4e73c-113">In the Azure portal, open your Automation account, and then select **Change tracking**.</span></span>
2. <span data-ttu-id="4e73c-114">On the top menu, select **Edit Settings**.</span><span class="sxs-lookup"><span data-stu-id="4e73c-114">On the top menu, select **Edit Settings**.</span></span>
3. <span data-ttu-id="4e73c-115">Select **File Content** and click **Link**.</span><span class="sxs-lookup"><span data-stu-id="4e73c-115">Select **File Content** and click **Link**.</span></span> <span data-ttu-id="4e73c-116">This opens the **Add Content Location for Change Tracking** pane.</span><span class="sxs-lookup"><span data-stu-id="4e73c-116">This opens the **Add Content Location for Change Tracking** pane.</span></span>

   ![enable](./media/change-tracking-file-contents/enable.png)

4. <span data-ttu-id="4e73c-118">Select the subscription and storage account to use to store the file contents to.</span><span class="sxs-lookup"><span data-stu-id="4e73c-118">Select the subscription and storage account to use to store the file contents to.</span></span> <span data-ttu-id="4e73c-119">If you want to enable file content tracking for all existing tracked files, select **On** for **Upload file content for all settings**.</span><span class="sxs-lookup"><span data-stu-id="4e73c-119">If you want to enable file content tracking for all existing tracked files, select **On** for **Upload file content for all settings**.</span></span> <span data-ttu-id="4e73c-120">You can change this for each file path afterwards.</span><span class="sxs-lookup"><span data-stu-id="4e73c-120">You can change this for each file path afterwards.</span></span>

   ![set storage account](./media/change-tracking-file-contents/storage-account.png)

5. <span data-ttu-id="4e73c-122">Once enabled, the storage account and the SAS Uris are shown.</span><span class="sxs-lookup"><span data-stu-id="4e73c-122">Once enabled, the storage account and the SAS Uris are shown.</span></span> <span data-ttu-id="4e73c-123">The SAS Uris expire after 365 days, and can be recreated by clicking the **Regenerate** button.</span><span class="sxs-lookup"><span data-stu-id="4e73c-123">The SAS Uris expire after 365 days, and can be recreated by clicking the **Regenerate** button.</span></span>

   ![list account keys](./media/change-tracking-file-contents/account-keys.png)

## <a name="add-a-file"></a><span data-ttu-id="4e73c-125">Add a file</span><span class="sxs-lookup"><span data-stu-id="4e73c-125">Add a file</span></span>

<span data-ttu-id="4e73c-126">The following steps walk you through turning on change tracking for a file:</span><span class="sxs-lookup"><span data-stu-id="4e73c-126">The following steps walk you through turning on change tracking for a file:</span></span>

1. <span data-ttu-id="4e73c-127">On the **Edit Settings** page of **Change Tracking**, select either **Windows Files** or **Linux Files** tab, and click **Add**</span><span class="sxs-lookup"><span data-stu-id="4e73c-127">On the **Edit Settings** page of **Change Tracking**, select either **Windows Files** or **Linux Files** tab, and click **Add**</span></span>

1. <span data-ttu-id="4e73c-128">Fill out the information for the file path and select **True** under **Upload file content for all settings**.</span><span class="sxs-lookup"><span data-stu-id="4e73c-128">Fill out the information for the file path and select **True** under **Upload file content for all settings**.</span></span> <span data-ttu-id="4e73c-129">This setting enables file content tracking for that file path only.</span><span class="sxs-lookup"><span data-stu-id="4e73c-129">This setting enables file content tracking for that file path only.</span></span>

   ![add a linux file](./media/change-tracking-file-contents/add-linux-file.png)

## <a name="viewing-the-contents-of-a-tracked-file"></a><span data-ttu-id="4e73c-131">Viewing the contents of a tracked file</span><span class="sxs-lookup"><span data-stu-id="4e73c-131">Viewing the contents of a tracked file</span></span>

1. <span data-ttu-id="4e73c-132">Once a change has been detected for the file or a file in the path, it shows in the portal.</span><span class="sxs-lookup"><span data-stu-id="4e73c-132">Once a change has been detected for the file or a file in the path, it shows in the portal.</span></span> <span data-ttu-id="4e73c-133">Select the file change from the list of changes.</span><span class="sxs-lookup"><span data-stu-id="4e73c-133">Select the file change from the list of changes.</span></span> <span data-ttu-id="4e73c-134">The **Change details** pane is displayed.</span><span class="sxs-lookup"><span data-stu-id="4e73c-134">The **Change details** pane is displayed.</span></span>

   ![list changes](./media/change-tracking-file-contents/change-list.png)

1. <span data-ttu-id="4e73c-136">On the **Change details** page, you see the standard before and after file information, in the top left, click **View File Content Changes** to see the contents of the file.</span><span class="sxs-lookup"><span data-stu-id="4e73c-136">On the **Change details** page, you see the standard before and after file information, in the top left, click **View File Content Changes** to see the contents of the file.</span></span>

  ![change details](./media/change-tracking-file-contents/change-details.png)

1. <span data-ttu-id="4e73c-138">The new page shows you the file contents in a side-by-side view.</span><span class="sxs-lookup"><span data-stu-id="4e73c-138">The new page shows you the file contents in a side-by-side view.</span></span> <span data-ttu-id="4e73c-139">You can also select **Inline** to see an inline view of the changes.</span><span class="sxs-lookup"><span data-stu-id="4e73c-139">You can also select **Inline** to see an inline view of the changes.</span></span>

  ![view file changes](./media/change-tracking-file-contents/view-file-changes.png)

## <a name="next-steps"></a><span data-ttu-id="4e73c-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="4e73c-141">Next steps</span></span>

<span data-ttu-id="4e73c-142">Visit the tutorial on Change Tracking to learn more about using the solution:</span><span class="sxs-lookup"><span data-stu-id="4e73c-142">Visit the tutorial on Change Tracking to learn more about using the solution:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4e73c-143">Troubleshoot changes in your environment</span><span class="sxs-lookup"><span data-stu-id="4e73c-143">Troubleshoot changes in your environment</span></span>](automation-tutorial-troubleshoot-changes.md)

* <span data-ttu-id="4e73c-144">Use [Log searches in Log Analytics](../log-analytics/log-analytics-log-searches.md) to view detailed change tracking data.</span><span class="sxs-lookup"><span data-stu-id="4e73c-144">Use [Log searches in Log Analytics](../log-analytics/log-analytics-log-searches.md) to view detailed change tracking data.</span></span>
