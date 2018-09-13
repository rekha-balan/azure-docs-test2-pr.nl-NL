---
title: Using the Azure Cloud Shell editor | Microsoft Docs
description: Overview of how to use the Azure Cloud Shell editor.
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
ms.date: 07/24/2018
ms.author: juluk
ms.openlocfilehash: caf6e18a9a30654710f5445ed6ab957a5253d62e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865461"
---
# <a name="using-the-azure-cloud-shell-editor"></a>Using the Azure Cloud Shell editor

Azure Cloud Shell includes an integrated file editor built from the open-source [Monaco Editor](https://github.com/Microsoft/monaco-editor). The Cloud Shell editor supports features such as language highlighting, the command palette, and a file explorer.

![Cloud Shell editor](media/using-cloud-shell-editor/open-editor.png)

## <a name="opening-the-editor"></a>Opening the editor

For simple file creation and editing, launch the editor by running `code .` in the Cloud Shell terminal. This action opens the editor with your active working directory set in the terminal.

To directly open a file for quick editing, run `code <filename>` to open the editor without the file explorer.

To open the editor via UI button, click the `{}` editor icon from the toolbar. This will open the editor and default the file explorer to the `/home/<user>` directory.

## <a name="closing-the-editor"></a>Closing the editor

To close the editor, open the `...` action panel in the top right of the editor and select `Close editor`.

![Close editor](media/using-cloud-shell-editor/close-editor.png)

## <a name="command-palette"></a>Command palette

To launch the command palette, use the `F1` key when focus is set on the editor. Opening the command palette can also be done through the action panel.

![Cmd palette](media/using-cloud-shell-editor/cmd-palette.png)

## <a name="contributing-to-the-monaco-editor"></a>Contributing to the Monaco Editor

Language highlight support in the Cloud Shell editor is supported through upstream functionality in the [Monaco Editor](https://github.com/Microsoft/monaco-editor)'s use of Monarch syntax definitions. To learn how to make contributions, read the [Monaco contributor guide](https://github.com/Microsoft/monaco-editor/blob/master/CONTRIBUTING.md).

## <a name="next-steps"></a>Next steps
[Try the quickstart for Bash in Cloud Shell](quickstart.md)
[View the full list of integrated Cloud Shell tools](features.md)