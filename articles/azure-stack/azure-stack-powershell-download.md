---
title: Download Azure Stack tools from GitHub | Microsoft Docs
description: Learn how to download tools that are required for working with Azure Stack.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: PowerShell
ms.topic: article
ms.date: 05/10/2018
ms.author: mabrigg
ms.reviewer: thoroet
ms.openlocfilehash: 5800cb1bf0badce6e1d0c53c3164f7d2bd2d8b1b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44814228"
---
# <a name="download-azure-stack-tools-from-github"></a><span data-ttu-id="2a8c7-103">Download Azure Stack tools from GitHub</span><span class="sxs-lookup"><span data-stu-id="2a8c7-103">Download Azure Stack tools from GitHub</span></span>

<span data-ttu-id="2a8c7-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="2a8c7-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="2a8c7-105">**AzureStack-Tools** is a [GitHub repository](https://github.com/Azure/AzureStack-Tools) that hosts PowerShell modules for managing and deploying resources to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="2a8c7-105">**AzureStack-Tools** is a [GitHub repository](https://github.com/Azure/AzureStack-Tools) that hosts PowerShell modules for managing and deploying resources to Azure Stack.</span></span> <span data-ttu-id="2a8c7-106">If you are planning to establish VPN connectivity, you can download these PowerShell modules to the Azure Stack Development Kit, or to a Windows-based external client.</span><span class="sxs-lookup"><span data-stu-id="2a8c7-106">If you are planning to establish VPN connectivity, you can download these PowerShell modules to the Azure Stack Development Kit, or to a Windows-based external client.</span></span> <span data-ttu-id="2a8c7-107">To obtain these tools, clone the GitHub repository or download the **AzureStack-Tools** folder by running the following script:</span><span class="sxs-lookup"><span data-stu-id="2a8c7-107">To obtain these tools, clone the GitHub repository or download the **AzureStack-Tools** folder by running the following script:</span></span>

```PowerShell
# Change directory to the root directory. 
cd \

# Download the tools archive.
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12 
invoke-webrequest `
  https://github.com/Azure/AzureStack-Tools/archive/master.zip `
  -OutFile master.zip

# Expand the downloaded files.
expand-archive master.zip `
  -DestinationPath . `
  -Force

# Change to the tools directory.
cd AzureStack-Tools-master

```

## <a name="functionality-provided-by-the-modules"></a><span data-ttu-id="2a8c7-108">Functionality provided by the modules</span><span class="sxs-lookup"><span data-stu-id="2a8c7-108">Functionality provided by the modules</span></span>

<span data-ttu-id="2a8c7-109">The **AzureStack-Tools** repository contains PowerShell modules that support the following functionalities for Azure Stack:</span><span class="sxs-lookup"><span data-stu-id="2a8c7-109">The **AzureStack-Tools** repository contains PowerShell modules that support the following functionalities for Azure Stack:</span></span>  

| <span data-ttu-id="2a8c7-110">Functionality</span><span class="sxs-lookup"><span data-stu-id="2a8c7-110">Functionality</span></span> | <span data-ttu-id="2a8c7-111">Description</span><span class="sxs-lookup"><span data-stu-id="2a8c7-111">Description</span></span> | <span data-ttu-id="2a8c7-112">Who can use this module?</span><span class="sxs-lookup"><span data-stu-id="2a8c7-112">Who can use this module?</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="2a8c7-113">Cloud capabilities</span><span class="sxs-lookup"><span data-stu-id="2a8c7-113">Cloud capabilities</span></span>](user/azure-stack-validate-templates.md) | <span data-ttu-id="2a8c7-114">Use this module to get the cloud capabilities of a cloud.</span><span class="sxs-lookup"><span data-stu-id="2a8c7-114">Use this module to get the cloud capabilities of a cloud.</span></span> <span data-ttu-id="2a8c7-115">For example, by using this module, you can get the cloud capabilities such as API version and Azure Resource Manager resources.</span><span class="sxs-lookup"><span data-stu-id="2a8c7-115">For example, by using this module, you can get the cloud capabilities such as API version and Azure Resource Manager resources.</span></span> <span data-ttu-id="2a8c7-116">You can also get the VM extensions for Azure Stack and Azure clouds by using this module.</span><span class="sxs-lookup"><span data-stu-id="2a8c7-116">You can also get the VM extensions for Azure Stack and Azure clouds by using this module.</span></span> | <span data-ttu-id="2a8c7-117">Cloud operators and users</span><span class="sxs-lookup"><span data-stu-id="2a8c7-117">Cloud operators and users</span></span> |
| [<span data-ttu-id="2a8c7-118">Resource Manager policy for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="2a8c7-118">Resource Manager policy for Azure Stack</span></span>](user/azure-stack-policy-module.md) | <span data-ttu-id="2a8c7-119">Use this module to configure an Azure subscription or an Azure resource group with the same versioning and service availability as Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="2a8c7-119">Use this module to configure an Azure subscription or an Azure resource group with the same versioning and service availability as Azure Stack.</span></span> | <span data-ttu-id="2a8c7-120">Cloud operators and users</span><span class="sxs-lookup"><span data-stu-id="2a8c7-120">Cloud operators and users</span></span> |
| [<span data-ttu-id="2a8c7-121">Register with Azure</span><span class="sxs-lookup"><span data-stu-id="2a8c7-121">Register with Azure</span></span>](azure-stack-register.md) | <span data-ttu-id="2a8c7-122">Use this module to register your development kit instance with Azure.</span><span class="sxs-lookup"><span data-stu-id="2a8c7-122">Use this module to register your development kit instance with Azure.</span></span> <span data-ttu-id="2a8c7-123">After registering, you can download the marketplace items from Azure and use them in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="2a8c7-123">After registering, you can download the marketplace items from Azure and use them in Azure Stack.</span></span> | <span data-ttu-id="2a8c7-124">Cloud operators</span><span class="sxs-lookup"><span data-stu-id="2a8c7-124">Cloud operators</span></span> |
| [<span data-ttu-id="2a8c7-125">Azure Stack deployment</span><span class="sxs-lookup"><span data-stu-id="2a8c7-125">Azure Stack deployment</span></span>](azure-stack-run-powershell-script.md) | <span data-ttu-id="2a8c7-126">Use this module to prepare the Azure Stack host computer to deploy and redeploy by using the Azure Stack virtual hard disk (VHD) image.</span><span class="sxs-lookup"><span data-stu-id="2a8c7-126">Use this module to prepare the Azure Stack host computer to deploy and redeploy by using the Azure Stack virtual hard disk (VHD) image.</span></span> | <span data-ttu-id="2a8c7-127">Cloud operators</span><span class="sxs-lookup"><span data-stu-id="2a8c7-127">Cloud operators</span></span>|
| [<span data-ttu-id="2a8c7-128">Connecting to Azure Stack</span><span class="sxs-lookup"><span data-stu-id="2a8c7-128">Connecting to Azure Stack</span></span>](azure-stack-connect-powershell.md) | <span data-ttu-id="2a8c7-129">Use this module to configure VPN connectivity to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="2a8c7-129">Use this module to configure VPN connectivity to Azure Stack.</span></span> | <span data-ttu-id="2a8c7-130">Cloud operators and users</span><span class="sxs-lookup"><span data-stu-id="2a8c7-130">Cloud operators and users</span></span> |
| [<span data-ttu-id="2a8c7-131">Template validator</span><span class="sxs-lookup"><span data-stu-id="2a8c7-131">Template validator</span></span>](user/azure-stack-validate-templates.md) | <span data-ttu-id="2a8c7-132">Use this module to verify if an existing or a new template can be deployed to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="2a8c7-132">Use this module to verify if an existing or a new template can be deployed to Azure Stack.</span></span> | <span data-ttu-id="2a8c7-133">Cloud operators and users</span><span class="sxs-lookup"><span data-stu-id="2a8c7-133">Cloud operators and users</span></span>|


## <a name="next-steps"></a><span data-ttu-id="2a8c7-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="2a8c7-134">Next steps</span></span>
* [<span data-ttu-id="2a8c7-135">Configure the Azure Stack user's PowerShell environment</span><span class="sxs-lookup"><span data-stu-id="2a8c7-135">Configure the Azure Stack user's PowerShell environment</span></span>](user/azure-stack-powershell-configure-user.md)   
* [<span data-ttu-id="2a8c7-136">Connect to Azure Stack Development Kit over a VPN</span><span class="sxs-lookup"><span data-stu-id="2a8c7-136">Connect to Azure Stack Development Kit over a VPN</span></span>](azure-stack-connect-azure-stack.md)  
