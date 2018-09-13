---
title: Azure Cloud Shell overview | Microsoft Docs
description: Overview of the Azure Cloud Shell.
services: ''
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
ms.date: 09/04/2018
ms.author: juluk
ms.openlocfilehash: ff50ea8c49d35306ccb48ec703de39c27c24bf7b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871403"
---
# <a name="overview-of-azure-cloud-shell"></a><span data-ttu-id="491f7-103">Overview of Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="491f7-103">Overview of Azure Cloud Shell</span></span>
<span data-ttu-id="491f7-104">Azure Cloud Shell is an interactive, browser-accessible shell for managing Azure resources.</span><span class="sxs-lookup"><span data-stu-id="491f7-104">Azure Cloud Shell is an interactive, browser-accessible shell for managing Azure resources.</span></span>
<span data-ttu-id="491f7-105">It provides the flexibility of choosing the shell experience that best suits the way you work.</span><span class="sxs-lookup"><span data-stu-id="491f7-105">It provides the flexibility of choosing the shell experience that best suits the way you work.</span></span>
<span data-ttu-id="491f7-106">Linux users can opt for a Bash experience, while Windows users can opt for PowerShell.</span><span class="sxs-lookup"><span data-stu-id="491f7-106">Linux users can opt for a Bash experience, while Windows users can opt for PowerShell.</span></span>

<span data-ttu-id="491f7-107">Try from shell.azure.com by clicking below.</span><span class="sxs-lookup"><span data-stu-id="491f7-107">Try from shell.azure.com by clicking below.</span></span>

<span data-ttu-id="491f7-108">[![](https://shell.azure.com/images/launchcloudshell.png "Launch Azure Cloud Shell")](https://shell.azure.com)</span><span class="sxs-lookup"><span data-stu-id="491f7-108">[![](https://shell.azure.com/images/launchcloudshell.png "Launch Azure Cloud Shell")](https://shell.azure.com)</span></span>

<span data-ttu-id="491f7-109">Try from Azure portal using the Cloud Shell icon.</span><span class="sxs-lookup"><span data-stu-id="491f7-109">Try from Azure portal using the Cloud Shell icon.</span></span>

![Portal launch](media/overview/portal-launch-icon.png)

## <a name="features"></a><span data-ttu-id="491f7-111">Features</span><span class="sxs-lookup"><span data-stu-id="491f7-111">Features</span></span>

### <a name="browser-based-shell-experience"></a><span data-ttu-id="491f7-112">Browser-based shell experience</span><span class="sxs-lookup"><span data-stu-id="491f7-112">Browser-based shell experience</span></span>
<span data-ttu-id="491f7-113">Cloud Shell enables access to a browser-based command-line experience built with Azure management tasks in mind.</span><span class="sxs-lookup"><span data-stu-id="491f7-113">Cloud Shell enables access to a browser-based command-line experience built with Azure management tasks in mind.</span></span>
<span data-ttu-id="491f7-114">Leverage Cloud Shell to work untethered from a local machine in a way only the cloud can provide.</span><span class="sxs-lookup"><span data-stu-id="491f7-114">Leverage Cloud Shell to work untethered from a local machine in a way only the cloud can provide.</span></span>

### <a name="choice-of-preferred-shell-experience"></a><span data-ttu-id="491f7-115">Choice of preferred shell experience</span><span class="sxs-lookup"><span data-stu-id="491f7-115">Choice of preferred shell experience</span></span>
<span data-ttu-id="491f7-116">Linux users can use Bash in Cloud Shell, while Windows users can use PowerShell in Cloud Shell (Preview) from the shell dropdown.</span><span class="sxs-lookup"><span data-stu-id="491f7-116">Linux users can use Bash in Cloud Shell, while Windows users can use PowerShell in Cloud Shell (Preview) from the shell dropdown.</span></span>

![Bash in Cloud Shell](media/overview/overview-bash-pic.png)

![PowerShell in Cloud Shell (Preview)](media/overview/overview-ps-pic.png)

### <a name="authenticated-and-configured-azure-workstation"></a><span data-ttu-id="491f7-119">Authenticated and configured Azure workstation</span><span class="sxs-lookup"><span data-stu-id="491f7-119">Authenticated and configured Azure workstation</span></span>
<span data-ttu-id="491f7-120">Cloud Shell is managed by Microsoft so it comes with popular command-line tools and language support.</span><span class="sxs-lookup"><span data-stu-id="491f7-120">Cloud Shell is managed by Microsoft so it comes with popular command-line tools and language support.</span></span> <span data-ttu-id="491f7-121">Cloud Shell also securely authenticates automatically for instant access to your resources through the Azure CLI 2.0 or Azure PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="491f7-121">Cloud Shell also securely authenticates automatically for instant access to your resources through the Azure CLI 2.0 or Azure PowerShell cmdlets.</span></span>

<span data-ttu-id="491f7-122">View the full [list of tools installed in Cloud Shell.](features.md#tools)</span><span class="sxs-lookup"><span data-stu-id="491f7-122">View the full [list of tools installed in Cloud Shell.](features.md#tools)</span></span>

### <a name="integrated-cloud-shell-editor"></a><span data-ttu-id="491f7-123">Integrated Cloud Shell editor</span><span class="sxs-lookup"><span data-stu-id="491f7-123">Integrated Cloud Shell editor</span></span>
<span data-ttu-id="491f7-124">Cloud Shell offers an integrated graphical text editor based on the open-source Monaco Editor.</span><span class="sxs-lookup"><span data-stu-id="491f7-124">Cloud Shell offers an integrated graphical text editor based on the open-source Monaco Editor.</span></span> <span data-ttu-id="491f7-125">Simply create and edit configuration files by running `code .` for seamless deployment through Azure CLI 2.0 or Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="491f7-125">Simply create and edit configuration files by running `code .` for seamless deployment through Azure CLI 2.0 or Azure PowerShell.</span></span>

<span data-ttu-id="491f7-126">[Learn more about the Cloud Shell editor](using-cloud-shell-editor.md).</span><span class="sxs-lookup"><span data-stu-id="491f7-126">[Learn more about the Cloud Shell editor](using-cloud-shell-editor.md).</span></span>

### <a name="multiple-access-points"></a><span data-ttu-id="491f7-127">Multiple access points</span><span class="sxs-lookup"><span data-stu-id="491f7-127">Multiple access points</span></span>
<span data-ttu-id="491f7-128">Cloud Shell is a flexible tool that can be used from:</span><span class="sxs-lookup"><span data-stu-id="491f7-128">Cloud Shell is a flexible tool that can be used from:</span></span>
* [<span data-ttu-id="491f7-129">portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="491f7-129">portal.azure.com</span></span>](https://portal.azure.com)
* [<span data-ttu-id="491f7-130">shell.azure.com</span><span class="sxs-lookup"><span data-stu-id="491f7-130">shell.azure.com</span></span>](https://shell.azure.com)
* [<span data-ttu-id="491f7-131">Azure CLI 2.0 "Try It" documentation</span><span class="sxs-lookup"><span data-stu-id="491f7-131">Azure CLI 2.0 "Try It" documentation</span></span>](https://docs.microsoft.com/cli/azure?view=azure-cli-latest)
* [<span data-ttu-id="491f7-132">Azure mobile app</span><span class="sxs-lookup"><span data-stu-id="491f7-132">Azure mobile app</span></span>](https://azure.microsoft.com/features/azure-portal/mobile-app/)
* [<span data-ttu-id="491f7-133">VS Code Azure Account extension</span><span class="sxs-lookup"><span data-stu-id="491f7-133">VS Code Azure Account extension</span></span>](https://marketplace.visualstudio.com/items?itemName=ms-vscode.azure-account)

### <a name="connect-your-microsoft-azure-files-storage"></a><span data-ttu-id="491f7-134">Connect your Microsoft Azure Files storage</span><span class="sxs-lookup"><span data-stu-id="491f7-134">Connect your Microsoft Azure Files storage</span></span>
<span data-ttu-id="491f7-135">Cloud Shell machines are temporary and require a new or existing Azure Files share to be mounted as `clouddrive` to persist your files.</span><span class="sxs-lookup"><span data-stu-id="491f7-135">Cloud Shell machines are temporary and require a new or existing Azure Files share to be mounted as `clouddrive` to persist your files.</span></span>

<span data-ttu-id="491f7-136">On first launch Cloud Shell prompts to create a resource group, storage account, and Azure Files share on your behalf.</span><span class="sxs-lookup"><span data-stu-id="491f7-136">On first launch Cloud Shell prompts to create a resource group, storage account, and Azure Files share on your behalf.</span></span> <span data-ttu-id="491f7-137">This is a one-time step and will be automatically attached for all sessions.</span><span class="sxs-lookup"><span data-stu-id="491f7-137">This is a one-time step and will be automatically attached for all sessions.</span></span> <span data-ttu-id="491f7-138">A single file share can be mapped and will be used by both Bash and PowerShell in Cloud Shell (Preview).</span><span class="sxs-lookup"><span data-stu-id="491f7-138">A single file share can be mapped and will be used by both Bash and PowerShell in Cloud Shell (Preview).</span></span>

<span data-ttu-id="491f7-139">Read more to learn how to mount a [new or existing storage account](persisting-shell-storage.md).</span><span class="sxs-lookup"><span data-stu-id="491f7-139">Read more to learn how to mount a [new or existing storage account](persisting-shell-storage.md).</span></span>

## <a name="concepts"></a><span data-ttu-id="491f7-140">Concepts</span><span class="sxs-lookup"><span data-stu-id="491f7-140">Concepts</span></span>
* <span data-ttu-id="491f7-141">Cloud Shell runs on a temporary host provided on a per-session, per-user basis</span><span class="sxs-lookup"><span data-stu-id="491f7-141">Cloud Shell runs on a temporary host provided on a per-session, per-user basis</span></span>
* <span data-ttu-id="491f7-142">Cloud Shell times out after 20 minutes without interactive activity</span><span class="sxs-lookup"><span data-stu-id="491f7-142">Cloud Shell times out after 20 minutes without interactive activity</span></span>
* <span data-ttu-id="491f7-143">Cloud Shell requires an Azure file share to be mounted</span><span class="sxs-lookup"><span data-stu-id="491f7-143">Cloud Shell requires an Azure file share to be mounted</span></span>
* <span data-ttu-id="491f7-144">Cloud Shell uses the same Azure file share for both Bash and PowerShell</span><span class="sxs-lookup"><span data-stu-id="491f7-144">Cloud Shell uses the same Azure file share for both Bash and PowerShell</span></span>
* <span data-ttu-id="491f7-145">Cloud Shell is assigned one machine per user account</span><span class="sxs-lookup"><span data-stu-id="491f7-145">Cloud Shell is assigned one machine per user account</span></span>
* <span data-ttu-id="491f7-146">Cloud Shell persists $Home using a 5-GB image held in your file share</span><span class="sxs-lookup"><span data-stu-id="491f7-146">Cloud Shell persists $Home using a 5-GB image held in your file share</span></span>
* <span data-ttu-id="491f7-147">Permissions are set as a regular Linux user in Bash</span><span class="sxs-lookup"><span data-stu-id="491f7-147">Permissions are set as a regular Linux user in Bash</span></span>

<span data-ttu-id="491f7-148">Learn more about features in [Bash in Cloud Shell](features.md) and [PowerShell in Cloud Shell (Preview)](features-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="491f7-148">Learn more about features in [Bash in Cloud Shell](features.md) and [PowerShell in Cloud Shell (Preview)](features-powershell.md).</span></span>

## <a name="pricing"></a><span data-ttu-id="491f7-149">Pricing</span><span class="sxs-lookup"><span data-stu-id="491f7-149">Pricing</span></span>
<span data-ttu-id="491f7-150">The machine hosting Cloud Shell is free, with a pre-requisite of a mounted Azure Files share.</span><span class="sxs-lookup"><span data-stu-id="491f7-150">The machine hosting Cloud Shell is free, with a pre-requisite of a mounted Azure Files share.</span></span> <span data-ttu-id="491f7-151">Regular storage costs apply.</span><span class="sxs-lookup"><span data-stu-id="491f7-151">Regular storage costs apply.</span></span>

## <a name="next-steps"></a><span data-ttu-id="491f7-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="491f7-152">Next steps</span></span>
[<span data-ttu-id="491f7-153">Bash in Cloud Shell quickstart</span><span class="sxs-lookup"><span data-stu-id="491f7-153">Bash in Cloud Shell quickstart</span></span>](quickstart.md) <br>
[<span data-ttu-id="491f7-154">PowerShell in Cloud Shell (Preview) quickstart</span><span class="sxs-lookup"><span data-stu-id="491f7-154">PowerShell in Cloud Shell (Preview) quickstart</span></span>](quickstart-powershell.md)