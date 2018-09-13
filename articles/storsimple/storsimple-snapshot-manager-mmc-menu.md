---
title: StorSimple Snapshot Manager MMC menu actions | Microsoft Docs
description: Describes how to use the standard Microsoft Management Console (MMC) menu actions in StorSimple Snapshot Manager.
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: ''
ms.assetid: 78ef81af-0d3a-4802-be54-ad192f9ac8a6
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/25/2016
ms.author: v-sharos
ms.openlocfilehash: 0a98825e225f5102f9539f877917f38ebdfc308d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660918"
---
# <a name="use-the-mmc-menu-actions-in-storsimple-snapshot-manager"></a>Use the MMC menu actions in StorSimple Snapshot Manager
## <a name="overview"></a>Overview
In StorSimple Snapshot Manager, you will see the following actions listed on all action menus and all variations of the **Actions** pane. 

* View
* New Window from Here 
* Refresh 
* Export List 
* Help 

These actions are part of the Microsoft Management Console (MMC) and are not specific to StorSimple Snapshot Manager. This tutorial describes these actions and explains how to use each of them in StorSimple Snapshot Manager.

## <a name="view"></a>View
You can use the **View** option to change the **Results** pane view and to change the console window view. 

#### <a name="to-change-the-results-pane-view"></a>To change the Results pane view
1. Click the desktop icon to start StorSimple Snapshot Manager.
2. In the **Scope** pane, right-click any node or expand the node and right-click an item in the **Results** pane, and then click the **View** option. 
3. To add or remove the columns that appear in the **Results** pane, click **Add/Remove Columns**. The **Add/Remove Columns** dialog box appears.
   
    ![Add or remove columns from Results pane](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-snapshot-manager-mmc-menu/HCS_SSM_Add_remove_columns.png) 
4. Complete the form as follows:
   
   * Select items from the **Available** columns list and click **Add** to add them to the **Displayed columns** list. 
   * Click items in the **Displayed columns** list, and click **Remove** to remove them from the list. 
   * Select an item in the **Displayed** columns list and click **Move Up** or **Move Down** to move the item up or down in the list. 
   * Click **Restore Defaults** to return to the default **Results** pane configuration. 
5. When you are finished with your selections, click **OK**. 

#### <a name="to-change-the-console-window-view"></a>To change the console window view
1. Click the desktop icon to start StorSimple Snapshot Manager.
2. In the **Scope** pane, right-click any node, click **View**, and then click **Customize**. The **Customize** dialog box appears.
   
    ![Customize the console window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-snapshot-manager-mmc-menu/HCS_SSM_Customize.png) 
3. Select or clear the check boxes to show or hide items in the console window. When you are finished with your selections, click **OK**.

## <a name="new-window-from-here"></a>New Window from Here
You can use the **New Window from Here** option to open a new console window.

#### <a name="to-open-a-new-console-window"></a>To open a new console window
1. Click the desktop icon to start StorSimple Snapshot Manager.
2. In the **Scope** pane, right-click any node, and then click **New Window from Here**. 
   
    A new window appears, showing only the scope that you selected. For example, if you right-click the **Backup Policies** node, the new window will show only the **Backup Policies** node in the **Scope** pane and a list of defined backup policies in the **Results** pane. See the following example.
   
    ![New Window from Here](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-snapshot-manager-mmc-menu/HCS_SSM_NewWindow.png) 

## <a name="refresh"></a>Refresh
You can use the **Refresh** action to update the console window.

#### <a name="to-update-the-console-window"></a>To update the console window
1. Click the desktop icon to start StorSimple Snapshot Manager.
2. In the **Scope** pane, right-click any node or expand the node and right-click an item in the **Results** pane, and then click **Refresh**. 

## <a name="export-list"></a>Export List
You can use the **Export List** action to save a list in a comma-separated value (CSV) file. For example, you can export the list of backup policies or the backup catalog. You can then import the CSV file into a spreadsheet application for analysis.

#### <a name="to-save-a-list-in-a-comma-separated-value-csv-file"></a>To save a list in a comma-separated value (CSV) file
1. Click the desktop icon to start StorSimple Snapshot Manager. 
2. In the **Scope** pane, right-click any node or expand the node and right-click an item in the **Results** pane, and then click **Export List**. 
3. The **Export List** dialog box appears. Complete the form as follows: 
   
   1. In the **File name** box, type a name for the CSV file or click the arrow to select from the drop-down list.
   2. In the **Save as type** box, click the arrow and select a file type from the drop-down list.
   3. To save only selected items, select the rows and then click the **Save Only Selected Rows** check box. To save all exported lists, clear the **Save Only Selected Rows** check box.
   4. Click **Save**.
      
      ![Export list as a comma-separated value file](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-snapshot-manager-mmc-menu/HCS_SSM_Export_List.png) 

## <a name="help"></a>Help
You can use the **Help** menu to view available online help for StorSimple Snapshot Manager and the MMC.

#### <a name="to-view-available-online-help"></a>To view available online help
1. Click the desktop icon to start StorSimple Snapshot Manager.
2. In the **Scope** pane, right-click any node or expand the node and right-click an item in the **Results** pane, and then click **Help**. 

## <a name="next-steps"></a>Next steps
* Learn more about the [StorSimple Snapshot Manager user interface](storsimple-use-snapshot-manager.md).
* Learn more about [using StorSimple Snapshot Manager to administer your StorSimple solution](storsimple-snapshot-manager-admin.md).





