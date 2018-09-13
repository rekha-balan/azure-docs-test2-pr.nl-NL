---
title: Download Azure Stack tools from GitHub | Microsoft Docs
description: Learn how to download tools required to work with Azure Stack.
services: azure-stack
documentationcenter: ''
author: SnehaGunda
manager: byronr
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: sngun
ms.openlocfilehash: 32cefba8d76fcb57d1fefbfe71645b493f4042d4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562897"
---
# <a name="download-azure-stack-tools-from-github"></a><span data-ttu-id="dd4fc-103">Download Azure Stack tools from GitHub</span><span class="sxs-lookup"><span data-stu-id="dd4fc-103">Download Azure Stack tools from GitHub</span></span>

<span data-ttu-id="dd4fc-104">AzureStack-Tools is a GitHub repository that hosts PowerShell modules that you can use to manage and deploy resources to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="dd4fc-104">AzureStack-Tools is a GitHub repository that hosts PowerShell modules that you can use to manage and deploy resources to Azure Stack.</span></span> <span data-ttu-id="dd4fc-105">You can download and use these PowerShell modules from MAS-CON01, Azure Stack host computer, or from a windows-based external client through VPN connectivity.</span><span class="sxs-lookup"><span data-stu-id="dd4fc-105">You can download and use these PowerShell modules from MAS-CON01, Azure Stack host computer, or from a windows-based external client through VPN connectivity.</span></span> <span data-ttu-id="dd4fc-106">To obtain these tools, clone the GitHub repository or download the AzureStack-Tools folder.</span><span class="sxs-lookup"><span data-stu-id="dd4fc-106">To obtain these tools, clone the GitHub repository or download the AzureStack-Tools folder.</span></span> 

<span data-ttu-id="dd4fc-107">To clone the repository, download [Git](https://git-scm.com/download/win) for Windows, open a Command Prompt window and run the following command:</span><span class="sxs-lookup"><span data-stu-id="dd4fc-107">To clone the repository, download [Git](https://git-scm.com/download/win) for Windows, open a Command Prompt window and run the following command:</span></span>

```PowerShell
# Change directory to the root directory 
cd \

# clone the repository
git clone https://github.com/Azure/AzureStack-Tools.git --recursive

# Change to the tools directory
cd AzureStack-Tools
```

<span data-ttu-id="dd4fc-108">To download the tools folder, run the following command:</span><span class="sxs-lookup"><span data-stu-id="dd4fc-108">To download the tools folder, run the following command:</span></span>

```PowerShell
# Change directory to the root directory 
cd \

# Download the tools archive
invoke-webrequest https://github.com/Azure/AzureStack-Tools/archive/master.zip -OutFile master.zip

# Expand the downloaded files
expand-archive master.zip -DestinationPath . -Force

# Change to the tools directory
cd AzureStack-Tools-master

```

## <a name="functionalities-provided-by-the-modules"></a><span data-ttu-id="dd4fc-109">Functionalities provided by the modules</span><span class="sxs-lookup"><span data-stu-id="dd4fc-109">Functionalities provided by the modules</span></span>

<span data-ttu-id="dd4fc-110">The AzureStack-Tools repository contains PowerShell modules that support the following functionalities for Azure Stack:</span><span class="sxs-lookup"><span data-stu-id="dd4fc-110">The AzureStack-Tools repository contains PowerShell modules that support the following functionalities for Azure Stack:</span></span>  

| <span data-ttu-id="dd4fc-111">Functionality</span><span class="sxs-lookup"><span data-stu-id="dd4fc-111">Functionality</span></span> | <span data-ttu-id="dd4fc-112">Description</span><span class="sxs-lookup"><span data-stu-id="dd4fc-112">Description</span></span> | <span data-ttu-id="dd4fc-113">who can use this module?</span><span class="sxs-lookup"><span data-stu-id="dd4fc-113">who can use this module?</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="dd4fc-114">Cloud capabilities</span><span class="sxs-lookup"><span data-stu-id="dd4fc-114">Cloud capabilities</span></span>](azure-stack-validate-templates.md) | <span data-ttu-id="dd4fc-115">Use this module to get the cloud capabilities of a cloud.</span><span class="sxs-lookup"><span data-stu-id="dd4fc-115">Use this module to get the cloud capabilities of a cloud.</span></span> <span data-ttu-id="dd4fc-116">For example, you can get the cloud capabilities such as API version, Azure Resource Manager resources, VM extensions etc. for Azure Stack and Azure clouds using this module.</span><span class="sxs-lookup"><span data-stu-id="dd4fc-116">For example, you can get the cloud capabilities such as API version, Azure Resource Manager resources, VM extensions etc. for Azure Stack and Azure clouds using this module.</span></span> | <span data-ttu-id="dd4fc-117">Cloud administrators and users.</span><span class="sxs-lookup"><span data-stu-id="dd4fc-117">Cloud administrators and users.</span></span> |
| [<span data-ttu-id="dd4fc-118">Azure Stack compute administration</span><span class="sxs-lookup"><span data-stu-id="dd4fc-118">Azure Stack compute administration</span></span>](azure-stack-add-vm-image.md) | <span data-ttu-id="dd4fc-119">Use this module to add or remove a VM image from the Azure Stack marketplace.</span><span class="sxs-lookup"><span data-stu-id="dd4fc-119">Use this module to add or remove a VM image from the Azure Stack marketplace.</span></span> | <span data-ttu-id="dd4fc-120">Cloud administrators.</span><span class="sxs-lookup"><span data-stu-id="dd4fc-120">Cloud administrators.</span></span> |
| [<span data-ttu-id="dd4fc-121">Azure Stack Infrastructure administration</span><span class="sxs-lookup"><span data-stu-id="dd4fc-121">Azure Stack Infrastructure administration</span></span>](https://github.com/Azure/AzureStack-Tools/blob/master/Infrastructure/README.md) | <span data-ttu-id="dd4fc-122">Use this module to manage Azure Stack infrastructure VMs, alerts, updates etc.</span><span class="sxs-lookup"><span data-stu-id="dd4fc-122">Use this module to manage Azure Stack infrastructure VMs, alerts, updates etc.</span></span> |  <span data-ttu-id="dd4fc-123">Cloud administrators.</span><span class="sxs-lookup"><span data-stu-id="dd4fc-123">Cloud administrators.</span></span>|
| [<span data-ttu-id="dd4fc-124">Resource Manager policy for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="dd4fc-124">Resource Manager policy for Azure Stack</span></span>](azure-stack-policy-module.md) | <span data-ttu-id="dd4fc-125">Use this module to configure an Azure subscription or an Azure resource group with the same versioning and service availability as Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="dd4fc-125">Use this module to configure an Azure subscription or an Azure resource group with the same versioning and service availability as Azure Stack.</span></span> | <span data-ttu-id="dd4fc-126">Cloud administrators and users</span><span class="sxs-lookup"><span data-stu-id="dd4fc-126">Cloud administrators and users</span></span> |
| [<span data-ttu-id="dd4fc-127">Register with Azure</span><span class="sxs-lookup"><span data-stu-id="dd4fc-127">Register with Azure</span></span>](azure-stack-register.md) | <span data-ttu-id="dd4fc-128">Use this module to register your Azure Stack POC instance with Azure.</span><span class="sxs-lookup"><span data-stu-id="dd4fc-128">Use this module to register your Azure Stack POC instance with Azure.</span></span> <span data-ttu-id="dd4fc-129">After registering, you can download the marketplace items from Azure and use them in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="dd4fc-129">After registering, you can download the marketplace items from Azure and use them in Azure Stack.</span></span> | <span data-ttu-id="dd4fc-130">Cloud administrators</span><span class="sxs-lookup"><span data-stu-id="dd4fc-130">Cloud administrators</span></span> |
| [<span data-ttu-id="dd4fc-131">Azure Stack deployment</span><span class="sxs-lookup"><span data-stu-id="dd4fc-131">Azure Stack deployment</span></span>](azure-stack-run-powershell-script.md) | <span data-ttu-id="dd4fc-132">Use this module to prepare the Azure Stack host computer to deploy and redeploy by using the Azure Stack Virtual Hard Disk(VHD) image.</span><span class="sxs-lookup"><span data-stu-id="dd4fc-132">Use this module to prepare the Azure Stack host computer to deploy and redeploy by using the Azure Stack Virtual Hard Disk(VHD) image.</span></span> | <span data-ttu-id="dd4fc-133">Cloud administrators.</span><span class="sxs-lookup"><span data-stu-id="dd4fc-133">Cloud administrators.</span></span> |
| [<span data-ttu-id="dd4fc-134">Connecting to Azure Stack</span><span class="sxs-lookup"><span data-stu-id="dd4fc-134">Connecting to Azure Stack</span></span>](azure-stack-connect-powershell.md) | <span data-ttu-id="dd4fc-135">Use this module to connect to an Azure Stack instance through PowerShell and to configure VPN connectivity to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="dd4fc-135">Use this module to connect to an Azure Stack instance through PowerShell and to configure VPN connectivity to Azure Stack.</span></span> | <span data-ttu-id="dd4fc-136">Cloud administrators and users</span><span class="sxs-lookup"><span data-stu-id="dd4fc-136">Cloud administrators and users</span></span> |
| [<span data-ttu-id="dd4fc-137">Azure Stack service administration</span><span class="sxs-lookup"><span data-stu-id="dd4fc-137">Azure Stack service administration</span></span>](azure-stack-create-offer.md) | <span data-ttu-id="dd4fc-138">Azure Stack administrators can use this module to create a default tenant offer with unlimited quota across Compute, Storage, Network, and Key Vault services.</span><span class="sxs-lookup"><span data-stu-id="dd4fc-138">Azure Stack administrators can use this module to create a default tenant offer with unlimited quota across Compute, Storage, Network, and Key Vault services.</span></span>   | <span data-ttu-id="dd4fc-139">Cloud administrators.</span><span class="sxs-lookup"><span data-stu-id="dd4fc-139">Cloud administrators.</span></span>|
| [<span data-ttu-id="dd4fc-140">Template validator</span><span class="sxs-lookup"><span data-stu-id="dd4fc-140">Template validator</span></span>](azure-stack-validate-templates.md) | <span data-ttu-id="dd4fc-141">Use this module to verify if an existing or a new template can be deployed to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="dd4fc-141">Use this module to verify if an existing or a new template can be deployed to Azure Stack.</span></span> | <span data-ttu-id="dd4fc-142">Cloud administrators and users</span><span class="sxs-lookup"><span data-stu-id="dd4fc-142">Cloud administrators and users</span></span> |


## <a name="next-steps"></a><span data-ttu-id="dd4fc-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="dd4fc-143">Next steps</span></span>
* [<span data-ttu-id="dd4fc-144">Configure powerShell for use with Azure Stack</span><span class="sxs-lookup"><span data-stu-id="dd4fc-144">Configure powerShell for use with Azure Stack</span></span>](azure-stack-powershell-configure.md)   
* [<span data-ttu-id="dd4fc-145">Connect to Azure Stack POC over a VPN</span><span class="sxs-lookup"><span data-stu-id="dd4fc-145">Connect to Azure Stack POC over a VPN</span></span>](azure-stack-connect-azure-stack.md)  
