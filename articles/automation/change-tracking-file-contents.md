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
# <a name="view-contents-of-a-file-that-is-being-tracked-with-change-tracking"></a>View contents of a file that is being tracked with Change Tracking

File content tracking allows you to view the contents of a file before and after a change that is being tracked with Change Tracking. To do this, it saves the file contents to a storage account after each change occurs.

## <a name="requirements"></a>Requirements

* A standard storage account using the Resource Manager deployment model is required for storing file content. Premium and classic deployment model storage accounts should not be used. For more information on storage accounts, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md)

* The storage account used can only have 1 Automation Account connected.

* [Change Tracking](automation-change-tracking.md) is enabled in your Automation Account.

## <a name="enable-file-content-tracking"></a>Enable file content tracking

1. In the Azure portal, open your Automation account, and then select **Change tracking**.
2. On the top menu, select **Edit Settings**.
3. Select **File Content** and click **Link**. This opens the **Add Content Location for Change Tracking** pane.

   ![enable](./media/change-tracking-file-contents/enable.png)

4. Select the subscription and storage account to use to store the file contents to. If you want to enable file content tracking for all existing tracked files, select **On** for **Upload file content for all settings**. You can change this for each file path afterwards.

   ![set storage account](./media/change-tracking-file-contents/storage-account.png)

5. Once enabled, the storage account and the SAS Uris are shown. The SAS Uris expire after 365 days, and can be recreated by clicking the **Regenerate** button.

   ![list account keys](./media/change-tracking-file-contents/account-keys.png)

## <a name="add-a-file"></a>Add a file

The following steps walk you through turning on change tracking for a file:

1. On the **Edit Settings** page of **Change Tracking**, select either **Windows Files** or **Linux Files** tab, and click **Add**

1. Fill out the information for the file path and select **True** under **Upload file content for all settings**. This setting enables file content tracking for that file path only.

   ![add a linux file](./media/change-tracking-file-contents/add-linux-file.png)

## <a name="viewing-the-contents-of-a-tracked-file"></a>Viewing the contents of a tracked file

1. Once a change has been detected for the file or a file in the path, it shows in the portal. Select the file change from the list of changes. The **Change details** pane is displayed.

   ![list changes](./media/change-tracking-file-contents/change-list.png)

1. On the **Change details** page, you see the standard before and after file information, in the top left, click **View File Content Changes** to see the contents of the file.

  ![change details](./media/change-tracking-file-contents/change-details.png)

1. The new page shows you the file contents in a side-by-side view. You can also select **Inline** to see an inline view of the changes.

  ![view file changes](./media/change-tracking-file-contents/view-file-changes.png)

## <a name="next-steps"></a>Next steps

Visit the tutorial on Change Tracking to learn more about using the solution:

> [!div class="nextstepaction"]
> [Troubleshoot changes in your environment](automation-tutorial-troubleshoot-changes.md)

* Use [Log searches in Log Analytics](../log-analytics/log-analytics-log-searches.md) to view detailed change tracking data.
