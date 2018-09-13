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
# <a name="using-the-azure-cloud-shell-editor"></a><span data-ttu-id="45734-103">Using the Azure Cloud Shell editor</span><span class="sxs-lookup"><span data-stu-id="45734-103">Using the Azure Cloud Shell editor</span></span>

<span data-ttu-id="45734-104">Azure Cloud Shell includes an integrated file editor built from the open-source [Monaco Editor](https://github.com/Microsoft/monaco-editor).</span><span class="sxs-lookup"><span data-stu-id="45734-104">Azure Cloud Shell includes an integrated file editor built from the open-source [Monaco Editor](https://github.com/Microsoft/monaco-editor).</span></span> <span data-ttu-id="45734-105">The Cloud Shell editor supports features such as language highlighting, the command palette, and a file explorer.</span><span class="sxs-lookup"><span data-stu-id="45734-105">The Cloud Shell editor supports features such as language highlighting, the command palette, and a file explorer.</span></span>

![Cloud Shell editor](media/using-cloud-shell-editor/open-editor.png)

## <a name="opening-the-editor"></a><span data-ttu-id="45734-107">Opening the editor</span><span class="sxs-lookup"><span data-stu-id="45734-107">Opening the editor</span></span>

<span data-ttu-id="45734-108">For simple file creation and editing, launch the editor by running `code .` in the Cloud Shell terminal.</span><span class="sxs-lookup"><span data-stu-id="45734-108">For simple file creation and editing, launch the editor by running `code .` in the Cloud Shell terminal.</span></span> <span data-ttu-id="45734-109">This action opens the editor with your active working directory set in the terminal.</span><span class="sxs-lookup"><span data-stu-id="45734-109">This action opens the editor with your active working directory set in the terminal.</span></span>

<span data-ttu-id="45734-110">To directly open a file for quick editing, run `code <filename>` to open the editor without the file explorer.</span><span class="sxs-lookup"><span data-stu-id="45734-110">To directly open a file for quick editing, run `code <filename>` to open the editor without the file explorer.</span></span>

<span data-ttu-id="45734-111">To open the editor via UI button, click the `{}` editor icon from the toolbar.</span><span class="sxs-lookup"><span data-stu-id="45734-111">To open the editor via UI button, click the `{}` editor icon from the toolbar.</span></span> <span data-ttu-id="45734-112">This will open the editor and default the file explorer to the `/home/<user>` directory.</span><span class="sxs-lookup"><span data-stu-id="45734-112">This will open the editor and default the file explorer to the `/home/<user>` directory.</span></span>

## <a name="closing-the-editor"></a><span data-ttu-id="45734-113">Closing the editor</span><span class="sxs-lookup"><span data-stu-id="45734-113">Closing the editor</span></span>

<span data-ttu-id="45734-114">To close the editor, open the `...` action panel in the top right of the editor and select `Close editor`.</span><span class="sxs-lookup"><span data-stu-id="45734-114">To close the editor, open the `...` action panel in the top right of the editor and select `Close editor`.</span></span>

![Close editor](media/using-cloud-shell-editor/close-editor.png)

## <a name="command-palette"></a><span data-ttu-id="45734-116">Command palette</span><span class="sxs-lookup"><span data-stu-id="45734-116">Command palette</span></span>

<span data-ttu-id="45734-117">To launch the command palette, use the `F1` key when focus is set on the editor.</span><span class="sxs-lookup"><span data-stu-id="45734-117">To launch the command palette, use the `F1` key when focus is set on the editor.</span></span> <span data-ttu-id="45734-118">Opening the command palette can also be done through the action panel.</span><span class="sxs-lookup"><span data-stu-id="45734-118">Opening the command palette can also be done through the action panel.</span></span>

![Cmd palette](media/using-cloud-shell-editor/cmd-palette.png)

## <a name="contributing-to-the-monaco-editor"></a><span data-ttu-id="45734-120">Contributing to the Monaco Editor</span><span class="sxs-lookup"><span data-stu-id="45734-120">Contributing to the Monaco Editor</span></span>

<span data-ttu-id="45734-121">Language highlight support in the Cloud Shell editor is supported through upstream functionality in the [Monaco Editor](https://github.com/Microsoft/monaco-editor)'s use of Monarch syntax definitions.</span><span class="sxs-lookup"><span data-stu-id="45734-121">Language highlight support in the Cloud Shell editor is supported through upstream functionality in the [Monaco Editor](https://github.com/Microsoft/monaco-editor)'s use of Monarch syntax definitions.</span></span> <span data-ttu-id="45734-122">To learn how to make contributions, read the [Monaco contributor guide](https://github.com/Microsoft/monaco-editor/blob/master/CONTRIBUTING.md).</span><span class="sxs-lookup"><span data-stu-id="45734-122">To learn how to make contributions, read the [Monaco contributor guide](https://github.com/Microsoft/monaco-editor/blob/master/CONTRIBUTING.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="45734-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="45734-123">Next steps</span></span>
<span data-ttu-id="45734-124">[Try the quickstart for Bash in Cloud Shell](quickstart.md)
[View the full list of integrated Cloud Shell tools](features.md)</span><span class="sxs-lookup"><span data-stu-id="45734-124">[Try the quickstart for Bash in Cloud Shell](quickstart.md)
[View the full list of integrated Cloud Shell tools](features.md)</span></span>