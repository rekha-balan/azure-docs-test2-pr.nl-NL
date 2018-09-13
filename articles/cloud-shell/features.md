---
title: Azure Cloud Shell features | Microsoft Docs
description: Overview of features of Bash in Azure Cloud Shell
services: Azure
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
ms.date: 07/13/2018
ms.author: juluk
ms.openlocfilehash: 1321645d97e7f6ff2faed1e61ddb608afcb7b413
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869849"
---
# <a name="features--tools-for-azure-cloud-shell"></a><span data-ttu-id="14a7b-103">Features & tools for Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="14a7b-103">Features & tools for Azure Cloud Shell</span></span>

[!INCLUDE [features-introblock](../../includes/cloud-shell-features-introblock.md)]

<span data-ttu-id="14a7b-104">Azure Cloud Shell runs on `Ubuntu 16.04 LTS`.</span><span class="sxs-lookup"><span data-stu-id="14a7b-104">Azure Cloud Shell runs on `Ubuntu 16.04 LTS`.</span></span>

## <a name="features"></a><span data-ttu-id="14a7b-105">Features</span><span class="sxs-lookup"><span data-stu-id="14a7b-105">Features</span></span>

### <a name="secure-automatic-authentication"></a><span data-ttu-id="14a7b-106">Secure automatic authentication</span><span class="sxs-lookup"><span data-stu-id="14a7b-106">Secure automatic authentication</span></span>

<span data-ttu-id="14a7b-107">Cloud Shell securely and automatically authenticates account access for the Azure CLI 2.0 and Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="14a7b-107">Cloud Shell securely and automatically authenticates account access for the Azure CLI 2.0 and Azure PowerShell.</span></span>

### <a name="home-persistence-across-sessions"></a><span data-ttu-id="14a7b-108">$Home persistence across sessions</span><span class="sxs-lookup"><span data-stu-id="14a7b-108">$Home persistence across sessions</span></span>

<span data-ttu-id="14a7b-109">To persist files across sessions, Cloud Shell walks you through attaching an Azure file share on first launch.</span><span class="sxs-lookup"><span data-stu-id="14a7b-109">To persist files across sessions, Cloud Shell walks you through attaching an Azure file share on first launch.</span></span>
<span data-ttu-id="14a7b-110">Once completed, Cloud Shell will automatically attach your storage (mounted as `$Home\clouddrive`) for all future sessions.</span><span class="sxs-lookup"><span data-stu-id="14a7b-110">Once completed, Cloud Shell will automatically attach your storage (mounted as `$Home\clouddrive`) for all future sessions.</span></span>
<span data-ttu-id="14a7b-111">Additionally, your `$Home` directory is persisted as an .img in your Azure File share.</span><span class="sxs-lookup"><span data-stu-id="14a7b-111">Additionally, your `$Home` directory is persisted as an .img in your Azure File share.</span></span>
<span data-ttu-id="14a7b-112">Files outside of `$Home` and machine state are not persisted across sessions.</span><span class="sxs-lookup"><span data-stu-id="14a7b-112">Files outside of `$Home` and machine state are not persisted across sessions.</span></span> <span data-ttu-id="14a7b-113">Use best practices when storing secrets such as SSH keys.</span><span class="sxs-lookup"><span data-stu-id="14a7b-113">Use best practices when storing secrets such as SSH keys.</span></span> <span data-ttu-id="14a7b-114">Services like [Azure Key Vault have tutorials for setup](https://docs.microsoft.com/azure/key-vault/key-vault-manage-with-cli2#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="14a7b-114">Services like [Azure Key Vault have tutorials for setup](https://docs.microsoft.com/azure/key-vault/key-vault-manage-with-cli2#prerequisites).</span></span>

[<span data-ttu-id="14a7b-115">Learn more about persisting files in Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="14a7b-115">Learn more about persisting files in Cloud Shell.</span></span>](persisting-shell-storage.md)

### <a name="azure-drive-azure"></a><span data-ttu-id="14a7b-116">Azure drive (Azure:)</span><span class="sxs-lookup"><span data-stu-id="14a7b-116">Azure drive (Azure:)</span></span>

<span data-ttu-id="14a7b-117">PowerShell in Cloud Shell (Preview) starts you in Azure drive (`Azure:`).</span><span class="sxs-lookup"><span data-stu-id="14a7b-117">PowerShell in Cloud Shell (Preview) starts you in Azure drive (`Azure:`).</span></span>
<span data-ttu-id="14a7b-118">The Azure drive enables easy discovery and navigation of Azure resources such as Compute, Network, Storage etc. similar to filesystem navigation.</span><span class="sxs-lookup"><span data-stu-id="14a7b-118">The Azure drive enables easy discovery and navigation of Azure resources such as Compute, Network, Storage etc. similar to filesystem navigation.</span></span>
<span data-ttu-id="14a7b-119">You can continue to use the familiar [Azure PowerShell cmdlets](https://docs.microsoft.com/powershell/azure) to manage these resources regardless of the drive you are in.</span><span class="sxs-lookup"><span data-stu-id="14a7b-119">You can continue to use the familiar [Azure PowerShell cmdlets](https://docs.microsoft.com/powershell/azure) to manage these resources regardless of the drive you are in.</span></span>
<span data-ttu-id="14a7b-120">Any changes made to the Azure resources, either made directly in Azure portal or through Azure PowerShell cmdlets, are reflected in the Azure drive.</span><span class="sxs-lookup"><span data-stu-id="14a7b-120">Any changes made to the Azure resources, either made directly in Azure portal or through Azure PowerShell cmdlets, are reflected in the Azure drive.</span></span>  <span data-ttu-id="14a7b-121">You can run `dir -Force` to refresh your resources.</span><span class="sxs-lookup"><span data-stu-id="14a7b-121">You can run `dir -Force` to refresh your resources.</span></span>

![](media/features-powershell/azure-drive.png)

### <a name="deep-integration-with-open-source-tooling"></a><span data-ttu-id="14a7b-122">Deep integration with open-source tooling</span><span class="sxs-lookup"><span data-stu-id="14a7b-122">Deep integration with open-source tooling</span></span>

<span data-ttu-id="14a7b-123">Cloud Shell includes pre-configured authentication for open-source tools such as Terraform, Ansible, and Chef InSpec.</span><span class="sxs-lookup"><span data-stu-id="14a7b-123">Cloud Shell includes pre-configured authentication for open-source tools such as Terraform, Ansible, and Chef InSpec.</span></span> <span data-ttu-id="14a7b-124">Try it out from the example walkthroughs.</span><span class="sxs-lookup"><span data-stu-id="14a7b-124">Try it out from the example walkthroughs.</span></span>

## <a name="tools"></a><span data-ttu-id="14a7b-125">Tools</span><span class="sxs-lookup"><span data-stu-id="14a7b-125">Tools</span></span>

|<span data-ttu-id="14a7b-126">Category</span><span class="sxs-lookup"><span data-stu-id="14a7b-126">Category</span></span>   |<span data-ttu-id="14a7b-127">Name</span><span class="sxs-lookup"><span data-stu-id="14a7b-127">Name</span></span>   |
|---|---|
|<span data-ttu-id="14a7b-128">Linux tools</span><span class="sxs-lookup"><span data-stu-id="14a7b-128">Linux tools</span></span>            |<span data-ttu-id="14a7b-129">bash</span><span class="sxs-lookup"><span data-stu-id="14a7b-129">bash</span></span><br> <span data-ttu-id="14a7b-130">zsh</span><span class="sxs-lookup"><span data-stu-id="14a7b-130">zsh</span></span><br> <span data-ttu-id="14a7b-131">sh</span><span class="sxs-lookup"><span data-stu-id="14a7b-131">sh</span></span><br> <span data-ttu-id="14a7b-132">tmux</span><span class="sxs-lookup"><span data-stu-id="14a7b-132">tmux</span></span><br> <span data-ttu-id="14a7b-133">dig</span><span class="sxs-lookup"><span data-stu-id="14a7b-133">dig</span></span><br>               |
|<span data-ttu-id="14a7b-134">Azure tools</span><span class="sxs-lookup"><span data-stu-id="14a7b-134">Azure tools</span></span>            |<span data-ttu-id="14a7b-135">[Azure CLI 2.0](https://github.com/Azure/azure-cli) and [1.0](https://github.com/Azure/azure-xplat-cli)</span><span class="sxs-lookup"><span data-stu-id="14a7b-135">[Azure CLI 2.0](https://github.com/Azure/azure-cli) and [1.0](https://github.com/Azure/azure-xplat-cli)</span></span><br> [<span data-ttu-id="14a7b-136">AzCopy</span><span class="sxs-lookup"><span data-stu-id="14a7b-136">AzCopy</span></span>](https://docs.microsoft.com/azure/storage/storage-use-azcopy)<br> [<span data-ttu-id="14a7b-137">Service Fabric CLI</span><span class="sxs-lookup"><span data-stu-id="14a7b-137">Service Fabric CLI</span></span>](https://docs.microsoft.com/azure/service-fabric/service-fabric-cli) |
|<span data-ttu-id="14a7b-138">Text editors</span><span class="sxs-lookup"><span data-stu-id="14a7b-138">Text editors</span></span>           |<span data-ttu-id="14a7b-139">vim</span><span class="sxs-lookup"><span data-stu-id="14a7b-139">vim</span></span><br> <span data-ttu-id="14a7b-140">nano</span><span class="sxs-lookup"><span data-stu-id="14a7b-140">nano</span></span><br> <span data-ttu-id="14a7b-141">emacs</span><span class="sxs-lookup"><span data-stu-id="14a7b-141">emacs</span></span>       |
|<span data-ttu-id="14a7b-142">Source control</span><span class="sxs-lookup"><span data-stu-id="14a7b-142">Source control</span></span>         |<span data-ttu-id="14a7b-143">git</span><span class="sxs-lookup"><span data-stu-id="14a7b-143">git</span></span>                    |
|<span data-ttu-id="14a7b-144">Build tools</span><span class="sxs-lookup"><span data-stu-id="14a7b-144">Build tools</span></span>            |<span data-ttu-id="14a7b-145">make</span><span class="sxs-lookup"><span data-stu-id="14a7b-145">make</span></span><br> <span data-ttu-id="14a7b-146">maven</span><span class="sxs-lookup"><span data-stu-id="14a7b-146">maven</span></span><br> <span data-ttu-id="14a7b-147">npm</span><span class="sxs-lookup"><span data-stu-id="14a7b-147">npm</span></span><br> <span data-ttu-id="14a7b-148">pip</span><span class="sxs-lookup"><span data-stu-id="14a7b-148">pip</span></span>         |
|<span data-ttu-id="14a7b-149">Containers</span><span class="sxs-lookup"><span data-stu-id="14a7b-149">Containers</span></span>             |<span data-ttu-id="14a7b-150">[Docker CLI](https://github.com/docker/cli)/[Docker Machine](https://github.com/docker/machine)</span><span class="sxs-lookup"><span data-stu-id="14a7b-150">[Docker CLI](https://github.com/docker/cli)/[Docker Machine](https://github.com/docker/machine)</span></span><br> [<span data-ttu-id="14a7b-151">Kubectl</span><span class="sxs-lookup"><span data-stu-id="14a7b-151">Kubectl</span></span>](https://kubernetes.io/docs/user-guide/kubectl-overview/)<br> [<span data-ttu-id="14a7b-152">Helm</span><span class="sxs-lookup"><span data-stu-id="14a7b-152">Helm</span></span>](https://github.com/kubernetes/helm)<br> [<span data-ttu-id="14a7b-153">DC/OS CLI</span><span class="sxs-lookup"><span data-stu-id="14a7b-153">DC/OS CLI</span></span>](https://github.com/dcos/dcos-cli)         |
|<span data-ttu-id="14a7b-154">Databases</span><span class="sxs-lookup"><span data-stu-id="14a7b-154">Databases</span></span>              |<span data-ttu-id="14a7b-155">MySQL client</span><span class="sxs-lookup"><span data-stu-id="14a7b-155">MySQL client</span></span><br> <span data-ttu-id="14a7b-156">PostgreSql client</span><span class="sxs-lookup"><span data-stu-id="14a7b-156">PostgreSql client</span></span><br> [<span data-ttu-id="14a7b-157">sqlcmd Utility</span><span class="sxs-lookup"><span data-stu-id="14a7b-157">sqlcmd Utility</span></span>](https://docs.microsoft.com/sql/tools/sqlcmd-utility)<br> [<span data-ttu-id="14a7b-158">mssql-scripter</span><span class="sxs-lookup"><span data-stu-id="14a7b-158">mssql-scripter</span></span>](https://github.com/Microsoft/sql-xplat-cli) |
|<span data-ttu-id="14a7b-159">Other</span><span class="sxs-lookup"><span data-stu-id="14a7b-159">Other</span></span>                  |<span data-ttu-id="14a7b-160">iPython Client</span><span class="sxs-lookup"><span data-stu-id="14a7b-160">iPython Client</span></span><br> [<span data-ttu-id="14a7b-161">Cloud Foundry CLI</span><span class="sxs-lookup"><span data-stu-id="14a7b-161">Cloud Foundry CLI</span></span>](https://github.com/cloudfoundry/cli)<br> [<span data-ttu-id="14a7b-162">Terraform</span><span class="sxs-lookup"><span data-stu-id="14a7b-162">Terraform</span></span>](https://www.terraform.io/docs/providers/azurerm/)<br> [<span data-ttu-id="14a7b-163">Ansible</span><span class="sxs-lookup"><span data-stu-id="14a7b-163">Ansible</span></span>](https://www.ansible.com/microsoft-azure)<br> [<span data-ttu-id="14a7b-164">Chef InSpec</span><span class="sxs-lookup"><span data-stu-id="14a7b-164">Chef InSpec</span></span>](https://www.chef.io/inspec/)| 

## <a name="language-support"></a><span data-ttu-id="14a7b-165">Language support</span><span class="sxs-lookup"><span data-stu-id="14a7b-165">Language support</span></span>

|<span data-ttu-id="14a7b-166">Language</span><span class="sxs-lookup"><span data-stu-id="14a7b-166">Language</span></span>   |<span data-ttu-id="14a7b-167">Version</span><span class="sxs-lookup"><span data-stu-id="14a7b-167">Version</span></span>   |
|---|---|
|<span data-ttu-id="14a7b-168">.NET Core</span><span class="sxs-lookup"><span data-stu-id="14a7b-168">.NET Core</span></span>  |<span data-ttu-id="14a7b-169">2.0.0</span><span class="sxs-lookup"><span data-stu-id="14a7b-169">2.0.0</span></span>       |
|<span data-ttu-id="14a7b-170">Go</span><span class="sxs-lookup"><span data-stu-id="14a7b-170">Go</span></span>         |<span data-ttu-id="14a7b-171">1.9</span><span class="sxs-lookup"><span data-stu-id="14a7b-171">1.9</span></span>        |
|<span data-ttu-id="14a7b-172">Java</span><span class="sxs-lookup"><span data-stu-id="14a7b-172">Java</span></span>       |<span data-ttu-id="14a7b-173">1.8</span><span class="sxs-lookup"><span data-stu-id="14a7b-173">1.8</span></span>        |
|<span data-ttu-id="14a7b-174">Node.js</span><span class="sxs-lookup"><span data-stu-id="14a7b-174">Node.js</span></span>    |<span data-ttu-id="14a7b-175">8.9.4</span><span class="sxs-lookup"><span data-stu-id="14a7b-175">8.9.4</span></span>      |
|<span data-ttu-id="14a7b-176">PowerShell</span><span class="sxs-lookup"><span data-stu-id="14a7b-176">PowerShell</span></span> |[<span data-ttu-id="14a7b-177">6.1.0-preview.4</span><span class="sxs-lookup"><span data-stu-id="14a7b-177">6.1.0-preview.4</span></span>](https://github.com/PowerShell/powershell/releases)       |
|<span data-ttu-id="14a7b-178">Python</span><span class="sxs-lookup"><span data-stu-id="14a7b-178">Python</span></span>     |<span data-ttu-id="14a7b-179">2.7 and 3.5 (default)</span><span class="sxs-lookup"><span data-stu-id="14a7b-179">2.7 and 3.5 (default)</span></span>|

## <a name="next-steps"></a><span data-ttu-id="14a7b-180">Next steps</span><span class="sxs-lookup"><span data-stu-id="14a7b-180">Next steps</span></span>
[<span data-ttu-id="14a7b-181">Bash in Cloud Shell Quickstart</span><span class="sxs-lookup"><span data-stu-id="14a7b-181">Bash in Cloud Shell Quickstart</span></span>](quickstart.md) <br>
[<span data-ttu-id="14a7b-182">PowerShell in Cloud Shell (Preview) Quickstart</span><span class="sxs-lookup"><span data-stu-id="14a7b-182">PowerShell in Cloud Shell (Preview) Quickstart</span></span>](quickstart-powershell.md) <br>
[<span data-ttu-id="14a7b-183">Learn about Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="14a7b-183">Learn about Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/) <br>
[<span data-ttu-id="14a7b-184">Learn about Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="14a7b-184">Learn about Azure PowerShell</span></span>](https://docs.microsoft.com/powershell/azure/) <br>
