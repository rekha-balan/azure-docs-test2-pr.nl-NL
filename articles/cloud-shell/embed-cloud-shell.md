---
title: Embed Azure Cloud Shell | Microsoft Docs
description: Learn to embed Azure Cloud Shell.
services: cloud-shell
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
ms.date: 12/11/2017
ms.author: juluk
ms.openlocfilehash: 0bd5382e5ea37f7c3c52d119e9d39fe7e0bfdc7c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855959"
---
# <a name="embed-azure-cloud-shell"></a><span data-ttu-id="b49ed-103">Embed Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="b49ed-103">Embed Azure Cloud Shell</span></span>

<span data-ttu-id="b49ed-104">Embedding Cloud Shell enables developers and content writers to directly open Cloud Shell from a dedicated URL, [shell.azure.com](https://shell.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b49ed-104">Embedding Cloud Shell enables developers and content writers to directly open Cloud Shell from a dedicated URL, [shell.azure.com](https://shell.azure.com).</span></span> <span data-ttu-id="b49ed-105">This immediately brings the full power of Cloud Shell's authentication, tooling, and up-to-date Azure CLI/Azure PowerShell tools to your users.</span><span class="sxs-lookup"><span data-stu-id="b49ed-105">This immediately brings the full power of Cloud Shell's authentication, tooling, and up-to-date Azure CLI/Azure PowerShell tools to your users.</span></span>

<span data-ttu-id="b49ed-106">Regular sized button</span><span class="sxs-lookup"><span data-stu-id="b49ed-106">Regular sized button</span></span>

<span data-ttu-id="b49ed-107">[![](https://shell.azure.com/images/launchcloudshell.png "Launch Azure Cloud Shell")](https://shell.azure.com)</span><span class="sxs-lookup"><span data-stu-id="b49ed-107">[![](https://shell.azure.com/images/launchcloudshell.png "Launch Azure Cloud Shell")](https://shell.azure.com)</span></span>

<span data-ttu-id="b49ed-108">Large sized button</span><span class="sxs-lookup"><span data-stu-id="b49ed-108">Large sized button</span></span>

<span data-ttu-id="b49ed-109">[![](https://shell.azure.com/images/launchcloudshell@2x.png "Launch Azure Cloud Shell")](https://shell.azure.com)</span><span class="sxs-lookup"><span data-stu-id="b49ed-109">[![](https://shell.azure.com/images/launchcloudshell@2x.png "Launch Azure Cloud Shell")](https://shell.azure.com)</span></span>

## <a name="how-to"></a><span data-ttu-id="b49ed-110">How-to</span><span class="sxs-lookup"><span data-stu-id="b49ed-110">How-to</span></span>

<span data-ttu-id="b49ed-111">Integrate Cloud Shell's launch button into markdown files by copying the following:</span><span class="sxs-lookup"><span data-stu-id="b49ed-111">Integrate Cloud Shell's launch button into markdown files by copying the following:</span></span>

```markdown
[![Launch Cloud Shell](https://shell.azure.com/images/launchcloudshell.png "Launch Cloud Shell")](https://shell.azure.com)
```

<span data-ttu-id="b49ed-112">The HTML to embed a pop-up Cloud Shell is below:</span><span class="sxs-lookup"><span data-stu-id="b49ed-112">The HTML to embed a pop-up Cloud Shell is below:</span></span>
```html
<a style="cursor:pointer" onclick='javascript:window.open("https://shell.azure.com", "_blank", "toolbar=no,scrollbars=yes,resizable=yes,menubar=no,location=no,status=no")'><img alt="Launch Azure Cloud Shell" src="https://shell.azure.com/images/launchcloudshell.png" /></a>
```

## <a name="customize-experience"></a><span data-ttu-id="b49ed-113">Customize experience</span><span class="sxs-lookup"><span data-stu-id="b49ed-113">Customize experience</span></span>

<span data-ttu-id="b49ed-114">Set a specific shell experience by augmenting your URL.</span><span class="sxs-lookup"><span data-stu-id="b49ed-114">Set a specific shell experience by augmenting your URL.</span></span>
|<span data-ttu-id="b49ed-115">Experience</span><span class="sxs-lookup"><span data-stu-id="b49ed-115">Experience</span></span>   |<span data-ttu-id="b49ed-116">URL</span><span class="sxs-lookup"><span data-stu-id="b49ed-116">URL</span></span>   |
|---|---|
|<span data-ttu-id="b49ed-117">Most recently used shell</span><span class="sxs-lookup"><span data-stu-id="b49ed-117">Most recently used shell</span></span>   |[<span data-ttu-id="b49ed-118">shell.azure.com</span><span class="sxs-lookup"><span data-stu-id="b49ed-118">shell.azure.com</span></span>](https://shell.azure.com)           |
|<span data-ttu-id="b49ed-119">Bash</span><span class="sxs-lookup"><span data-stu-id="b49ed-119">Bash</span></span>                       |[<span data-ttu-id="b49ed-120">shell.azure.com/bash</span><span class="sxs-lookup"><span data-stu-id="b49ed-120">shell.azure.com/bash</span></span>](https://shell.azure.com/bash)       |
|<span data-ttu-id="b49ed-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b49ed-121">PowerShell</span></span>                 |[<span data-ttu-id="b49ed-122">shell.azure.com/powershell</span><span class="sxs-lookup"><span data-stu-id="b49ed-122">shell.azure.com/powershell</span></span>](https://shell.azure.com/powershell) |

## <a name="next-steps"></a><span data-ttu-id="b49ed-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="b49ed-123">Next steps</span></span>
[<span data-ttu-id="b49ed-124">Bash in Cloud Shell quickstart</span><span class="sxs-lookup"><span data-stu-id="b49ed-124">Bash in Cloud Shell quickstart</span></span>](quickstart.md)<br>
[<span data-ttu-id="b49ed-125">PowerShell in Cloud Shell quickstart</span><span class="sxs-lookup"><span data-stu-id="b49ed-125">PowerShell in Cloud Shell quickstart</span></span>](quickstart-powershell.md)
