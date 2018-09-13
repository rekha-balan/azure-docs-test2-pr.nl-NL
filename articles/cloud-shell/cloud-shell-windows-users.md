---
title: Azure Cloud Shell for Windows users | Microsoft Docs
description: Guide for users who are not familiar with Linux systems
services: azure
documentationcenter: ''
author: maertendMSFT
manager: hemantm
tags: azure-resource-manager
ms.assetid: ''
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/03/2018
ms.author: damaerte
ms.openlocfilehash: aad474195060c01a3f9d85e6f9037b568b0c16ad
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967464"
---
# <a name="powershell-in-azure-cloud-shell-for-windows-users"></a><span data-ttu-id="00564-103">PowerShell in Azure Cloud Shell for Windows users</span><span class="sxs-lookup"><span data-stu-id="00564-103">PowerShell in Azure Cloud Shell for Windows users</span></span>

<span data-ttu-id="00564-104">In May 2018, changes were [announced](https://azure.microsoft.com/blog/pscloudshellrefresh/) to PowerShell in Azure Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="00564-104">In May 2018, changes were [announced](https://azure.microsoft.com/blog/pscloudshellrefresh/) to PowerShell in Azure Cloud Shell.</span></span>
<span data-ttu-id="00564-105">The PowerShell experience in Azure Cloud Shell now runs [PowerShell Core 6](https://github.com/powershell/powershell) in a Linux environment.</span><span class="sxs-lookup"><span data-stu-id="00564-105">The PowerShell experience in Azure Cloud Shell now runs [PowerShell Core 6](https://github.com/powershell/powershell) in a Linux environment.</span></span>
<span data-ttu-id="00564-106">With this change, there may be some differences in the PowerShell experience in Cloud Shell compared to what is expected in a Windows PowerShell experience.</span><span class="sxs-lookup"><span data-stu-id="00564-106">With this change, there may be some differences in the PowerShell experience in Cloud Shell compared to what is expected in a Windows PowerShell experience.</span></span>

## <a name="file-system-case-sensitivity"></a><span data-ttu-id="00564-107">File system case sensitivity</span><span class="sxs-lookup"><span data-stu-id="00564-107">File system case sensitivity</span></span>

<span data-ttu-id="00564-108">The file system is case-insensitive in Windows, whereas on Linux, the file system is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="00564-108">The file system is case-insensitive in Windows, whereas on Linux, the file system is case-sensitive.</span></span>
<span data-ttu-id="00564-109">Previously `file.txt` and `FILE.txt` were considered to be the same file, but now they are considered to be different files.</span><span class="sxs-lookup"><span data-stu-id="00564-109">Previously `file.txt` and `FILE.txt` were considered to be the same file, but now they are considered to be different files.</span></span>
<span data-ttu-id="00564-110">Proper casing must be used while `tab-completing` in the file system.</span><span class="sxs-lookup"><span data-stu-id="00564-110">Proper casing must be used while `tab-completing` in the file system.</span></span>
<span data-ttu-id="00564-111">PowerShell specific experiences, such as `tab-completing` cmdlet names, parameters, and values, are not case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="00564-111">PowerShell specific experiences, such as `tab-completing` cmdlet names, parameters, and values, are not case-sensitive.</span></span>

## <a name="windows-powershell-aliases-vs-linux-utilities"></a><span data-ttu-id="00564-112">Windows PowerShell aliases vs Linux utilities</span><span class="sxs-lookup"><span data-stu-id="00564-112">Windows PowerShell aliases vs Linux utilities</span></span>

<span data-ttu-id="00564-113">Some existing PowerShell aliases have the same names as built-in Linux commands, such as `cat`,`ls`, `sort`, `sleep`, etc. In PowerShell Core 6, aliases that collide with built-in Linux commands have been removed.</span><span class="sxs-lookup"><span data-stu-id="00564-113">Some existing PowerShell aliases have the same names as built-in Linux commands, such as `cat`,`ls`, `sort`, `sleep`, etc. In PowerShell Core 6, aliases that collide with built-in Linux commands have been removed.</span></span>
<span data-ttu-id="00564-114">Below are the common aliases that have been removed as well as their equivalent commands:</span><span class="sxs-lookup"><span data-stu-id="00564-114">Below are the common aliases that have been removed as well as their equivalent commands:</span></span>  

|<span data-ttu-id="00564-115">Removed Alias</span><span class="sxs-lookup"><span data-stu-id="00564-115">Removed Alias</span></span>   |<span data-ttu-id="00564-116">Equivalent Command</span><span class="sxs-lookup"><span data-stu-id="00564-116">Equivalent Command</span></span>   |
|---|---|
|`cat`    | `Get-Content` |
|`curl`   | `Invoke-WebRequest` |
|`diff`   | `Compare-Object` |
|`ls`     | `dir` <br> `Get-ChildItem` |
|`mv`     | `Move-Item`   |
|`rm`     | `Remove-Item` |
|`sleep`  | `Start-Sleep` |
|`sort`   | `Sort-Object` |
|`wget`   | `Invoke-WebRequest` |

## <a name="persisting-home"></a><span data-ttu-id="00564-117">Persisting $HOME</span><span class="sxs-lookup"><span data-stu-id="00564-117">Persisting $HOME</span></span>

<span data-ttu-id="00564-118">Earlier users could only persist scripts and other files in their Cloud Drive.</span><span class="sxs-lookup"><span data-stu-id="00564-118">Earlier users could only persist scripts and other files in their Cloud Drive.</span></span>
<span data-ttu-id="00564-119">Now, the user's $HOME directory is also now persisted across sessions.</span><span class="sxs-lookup"><span data-stu-id="00564-119">Now, the user's $HOME directory is also now persisted across sessions.</span></span>

## <a name="powershell-profile"></a><span data-ttu-id="00564-120">PowerShell profile</span><span class="sxs-lookup"><span data-stu-id="00564-120">PowerShell profile</span></span>

<span data-ttu-id="00564-121">By default, a user's PowerShell profile is not created.</span><span class="sxs-lookup"><span data-stu-id="00564-121">By default, a user's PowerShell profile is not created.</span></span>
<span data-ttu-id="00564-122">To create your profile, create a `PowerShell` directory under `$HOME/.config`.</span><span class="sxs-lookup"><span data-stu-id="00564-122">To create your profile, create a `PowerShell` directory under `$HOME/.config`.</span></span>

```azurepowershell-interactive
mkdir (Split-Path $profile.CurrentUserAllHosts)
```

<span data-ttu-id="00564-123">Under `$HOME/.config/PowerShell`, you can create your profile files - `profile.ps1` and/or `Microsoft.PowerShell_profile.ps1`.</span><span class="sxs-lookup"><span data-stu-id="00564-123">Under `$HOME/.config/PowerShell`, you can create your profile files - `profile.ps1` and/or `Microsoft.PowerShell_profile.ps1`.</span></span>

## <a name="whats-new-in-powershell-core-6"></a><span data-ttu-id="00564-124">What's new in PowerShell Core 6</span><span class="sxs-lookup"><span data-stu-id="00564-124">What's new in PowerShell Core 6</span></span>

<span data-ttu-id="00564-125">For more information about what is new in PowerShell Core 6, reference the [PowerShell docs](https://docs.microsoft.com/powershell/scripting/whats-new/what-s-new-in-powershell-core-60?view=powershell-6) and the [Getting Started with PowerShell Core](https://blogs.msdn.microsoft.com/powershell/2017/06/09/getting-started-with-powershell-core-on-windows-mac-and-linux/) blog post.</span><span class="sxs-lookup"><span data-stu-id="00564-125">For more information about what is new in PowerShell Core 6, reference the [PowerShell docs](https://docs.microsoft.com/powershell/scripting/whats-new/what-s-new-in-powershell-core-60?view=powershell-6) and the [Getting Started with PowerShell Core](https://blogs.msdn.microsoft.com/powershell/2017/06/09/getting-started-with-powershell-core-on-windows-mac-and-linux/) blog post.</span></span>
