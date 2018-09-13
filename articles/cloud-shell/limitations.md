---
title: Azure Cloud Shell limitations | Microsoft Docs
description: Overview of limitations of Azure Cloud Shell
services: azure
documentationcenter: ''
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: ''
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/15/2018
ms.author: juluk
ms.openlocfilehash: 135496e17ae884db580922aa31f6824b2e7fd934
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856473"
---
# <a name="limitations-of-azure-cloud-shell"></a>Limitations of Azure Cloud Shell

Azure Cloud Shell has the following known limitations:

## <a name="general-limitations"></a>General limitations

### <a name="system-state-and-persistence"></a>System state and persistence

The machine that provides your Cloud Shell session is temporary, and it is recycled after your session is inactive for 20 minutes. Cloud Shell requires an Azure file share to be mounted. As a result, your subscription must be able to set up storage resources to access Cloud Shell. Other considerations include:

* With mounted storage, only modifications within the `$Home` directory are persisted.
* Azure file shares can be mounted only from within your [assigned region](persisting-shell-storage.md#mount-a-new-clouddrive).
  * In Bash, run `env` to find your region set as `ACC_LOCATION`.

### <a name="browser-support"></a>Browser support

Cloud Shell supports the latest versions of Microsoft Edge, Microsoft Internet Explorer, Google Chrome, Mozilla Firefox, and Apple Safari. Safari in private mode is not supported.

### <a name="copy-and-paste"></a>Copy and paste

[!INCLUDE [copy-paste](../../includes/cloud-shell-copy-paste.md)]

### <a name="for-a-given-user-only-one-shell-can-be-active"></a>For a given user, only one shell can be active

Users can only launch one type of shell at a time, either **Bash** or **PowerShell**. However, you may have multiple instances of Bash or PowerShell running at one time. Swapping between Bash or PowerShell causes Cloud Shell to restart, which terminates existing sessions.

### <a name="usage-limits"></a>Usage limits

Cloud Shell is intended for interactive use cases. As a result, any long-running non-interactive sessions are ended without warning.

## <a name="bash-limitations"></a>Bash limitations

### <a name="user-permissions"></a>User permissions

Permissions are set as regular users without sudo access. Any installation outside your `$Home` directory is not persisted.

### <a name="editing-bashrc"></a>Editing .bashrc

Take caution when editing .bashrc, doing so can cause unexpected errors in Cloud Shell.

## <a name="powershell-limitations"></a>PowerShell limitations

### <a name="azuread-module-name"></a>`AzureAD` module name

The `AzureAD` module name is currently `AzureAD.Standard.Preview`, the module provides the same functionality.

### <a name="sqlserver-module-functionality"></a>`SqlServer` module functionality

The `SqlServer` module included in Cloud Shell has only prerelease support for PowerShell Core. In particular, `Invoke-SqlCmd` is not available yet.

### <a name="default-file-location-when-created-from-azure-drive"></a>Default file location when created from Azure drive:

Using PowerShell cmdlets, users can not create files under the Azure drive. When users create new files using other tools, such as vim or nano, the files are saved to the `$HOME` by default. 

### <a name="gui-applications-are-not-supported"></a>GUI applications are not supported

If the user runs a command that would create a Windows dialog box, such as `Connect-AzureAD` or `Connect-AzureRmAccount`, one sees an error message such as: `Unable to load DLL 'IEFRAME.dll': The specified module could not be found. (Exception from HRESULT: 0x8007007E)`.

### <a name="tab-completion-crashes-psreadline"></a>Tab completion crashes PSReadline

If the user's EditMode in PSReadline is set to Emacs, the user tries to display all possibilities via tab completion, and the window size is too small to display all the possibilities, PSReadline will crash.

### <a name="large-gap-after-displaying-progress-bar"></a>Large Gap after displaying progress bar

If the user performs an action that displays a progress bar, such a tab completing while in the `Azure:` drive, then it is possible that the cursor is not set properly and a gap appears where the progress bar was previously.

### <a name="random-characters-appear-inline"></a>Random characters appear inline

The cursor position sequence codes, for example `5;13R`, can appear in the user input.  The characters can be manually removed.

## <a name="next-steps"></a>Next steps

[Troubleshooting Cloud Shell](troubleshooting.md) <br>
[Quickstart for Bash](quickstart.md) <br>
[Quickstart for PowerShell](quickstart-powershell.md)
