---
title: Using the Azure Cloud Shell window | Microsoft Docs
description: Overview of how to use the Azure Cloud Shell window.
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
ms.date: 01/30/2018
ms.author: juluk
ms.openlocfilehash: 43da2bf5b66ff7db03a6fb5c2e1ceaebe322bcbb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870977"
---
# <a name="using-the-azure-cloud-shell-window"></a>Using the Azure Cloud Shell window

This document explains how to use the Cloud Shell window.

## <a name="swap-between-bash-and-powershell-environments"></a>Swap between Bash and PowerShell environments
![](media/using-the-shell-window/env-selector.png)

Use the environment selector in the Cloud Shell toolbar to swap between Bash and PowerShell environments.

## <a name="restart-cloud-shell"></a>Restart Cloud Shell
![](media/using-the-shell-window/restart.png)
> [!WARNING]
> Restarting Cloud Shell will reset machine state and any files not persisted by your Azure file share will be lost.

* Click the restart icon in the Cloud Shell toolbar to reset machine state.

## <a name="minimize--maximize-cloud-shell-window"></a>Minimize & maximize Cloud Shell window
![](media/using-the-shell-window/minmax.png)
* Click the minimize icon on the top right of the window to hide it. Click the Cloud Shell icon again to unhide.
* Click the maximize icon to set window to max height. To restore window to previous size, click restore.

## <a name="concurrent-sessions"></a>Concurrent sessions
Cloud Shell enables multiple concurrent sessions across browser tabs by allowing each session to exist as a separate Bash process.
If exiting a session, be sure to exit from each session window as each process runs independently although they run on the same machine.

## <a name="copy-and-paste"></a>Copy and paste
[!INCLUDE [copy-paste](../../includes/cloud-shell-copy-paste.md)]

## <a name="resize-cloud-shell-window"></a>Resize Cloud Shell window
* Click and drag the top edge of the toolbar up or down to resize the Cloud Shell window.

## <a name="scrolling-text-display"></a>Scrolling text display
* Scroll with your mouse or touchpad to move terminal text.

## <a name="changing-the-text-size"></a>Changing the text size
![](media/using-the-shell-window/text-size.png)
* Click the settings icon on the top left of the window, then hover over the "Text size" option and select your desired text size. Your selection will be persisted across sessions.

## <a name="exit-command"></a>Exit command
Running `exit` terminates the active session. This behavior occurs by default after 20 minutes without interaction.

## <a name="next-steps"></a>Next steps

[Bash in Cloud Shell Quickstart](quickstart.md)
[PowerShell in Cloud Shell Quickstart](quickstart-powershell.md)