---
title: Manage Azure Key Vault using Azure Automation | Microsoft Docs
description: Learn about how the Azure Automation service can be used to manage Azure Key Vault.
services: Key-Vault, automation
documentationcenter: ''
author: mgoedtel
manager: jwhit
editor: ''
ms.assetid: 4e780762-19b6-4ca6-b894-ebb44c538f35
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: magoedte;csand
ms.openlocfilehash: dee39662472fe54776b591977f2b1ecb39d15b00
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552515"
---
# <a name="managing-azure-key-vault-using-azure-automation"></a><span data-ttu-id="0ba89-103">Managing Azure Key Vault using Azure Automation</span><span class="sxs-lookup"><span data-stu-id="0ba89-103">Managing Azure Key Vault using Azure Automation</span></span>
<span data-ttu-id="0ba89-104">This guide will introduce you to the Azure Automation service and how it can be used to simplify management of your keys and secrets in Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="0ba89-104">This guide will introduce you to the Azure Automation service and how it can be used to simplify management of your keys and secrets in Azure Key Vault.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="0ba89-105">What is Azure Automation?</span><span class="sxs-lookup"><span data-stu-id="0ba89-105">What is Azure Automation?</span></span>
<span data-ttu-id="0ba89-106">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation and desired state configuration.</span><span class="sxs-lookup"><span data-stu-id="0ba89-106">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation and desired state configuration.</span></span> <span data-ttu-id="0ba89-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span><span class="sxs-lookup"><span data-stu-id="0ba89-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="0ba89-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales to meet your needs.</span><span class="sxs-lookup"><span data-stu-id="0ba89-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales to meet your needs.</span></span> <span data-ttu-id="0ba89-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span><span class="sxs-lookup"><span data-stu-id="0ba89-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="0ba89-110">Reduce operational overhead and free up IT and DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="0ba89-110">Reduce operational overhead and free up IT and DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-key-vault"></a><span data-ttu-id="0ba89-111">How can Azure Automation help manage Azure Key Vault?</span><span class="sxs-lookup"><span data-stu-id="0ba89-111">How can Azure Automation help manage Azure Key Vault?</span></span>
<span data-ttu-id="0ba89-112">Key Vault can be managed in Azure Automation by using the [AzureRM Key Vault cmdlets](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) and [Azure Classic Key Vault cmdlets](https://msdn.microsoft.com/library/azure/dn868052.aspx).</span><span class="sxs-lookup"><span data-stu-id="0ba89-112">Key Vault can be managed in Azure Automation by using the [AzureRM Key Vault cmdlets](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) and [Azure Classic Key Vault cmdlets](https://msdn.microsoft.com/library/azure/dn868052.aspx).</span></span> <span data-ttu-id="0ba89-113">The Azure module for managing classic Key Vault is available automatically in Azure Automation, and you can import the [AzureRM-KeyVault module](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) into Azure Automation, so that you can perform many of your Key Vault management tasks within the service.</span><span class="sxs-lookup"><span data-stu-id="0ba89-113">The Azure module for managing classic Key Vault is available automatically in Azure Automation, and you can import the [AzureRM-KeyVault module](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) into Azure Automation, so that you can perform many of your Key Vault management tasks within the service.</span></span> <span data-ttu-id="0ba89-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span><span class="sxs-lookup"><span data-stu-id="0ba89-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="0ba89-115">With the Azure Key Vault cmdlets you can perform these tasks among others:</span><span class="sxs-lookup"><span data-stu-id="0ba89-115">With the Azure Key Vault cmdlets you can perform these tasks among others:</span></span> 

* <span data-ttu-id="0ba89-116">Create and configure a key vault</span><span class="sxs-lookup"><span data-stu-id="0ba89-116">Create and configure a key vault</span></span>
* <span data-ttu-id="0ba89-117">Create or import a key</span><span class="sxs-lookup"><span data-stu-id="0ba89-117">Create or import a key</span></span>
* <span data-ttu-id="0ba89-118">Create or update a secret</span><span class="sxs-lookup"><span data-stu-id="0ba89-118">Create or update a secret</span></span>
* <span data-ttu-id="0ba89-119">Update attributes of a key</span><span class="sxs-lookup"><span data-stu-id="0ba89-119">Update attributes of a key</span></span>
* <span data-ttu-id="0ba89-120">Get a key or secret</span><span class="sxs-lookup"><span data-stu-id="0ba89-120">Get a key or secret</span></span>
* <span data-ttu-id="0ba89-121">Delete a key or secret</span><span class="sxs-lookup"><span data-stu-id="0ba89-121">Delete a key or secret</span></span>

<span data-ttu-id="0ba89-122">Here are some examples of using PowerShell to manage Key Vault:</span><span class="sxs-lookup"><span data-stu-id="0ba89-122">Here are some examples of using PowerShell to manage Key Vault:</span></span>  

* [<span data-ttu-id="0ba89-123">Azure Key Vault - Step by Step</span><span class="sxs-lookup"><span data-stu-id="0ba89-123">Azure Key Vault - Step by Step</span></span>](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step)
* [<span data-ttu-id="0ba89-124">Setting Up and Configuring an Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="0ba89-124">Setting Up and Configuring an Azure Key Vault</span></span>](https://www.simple-talk.com/cloud/platform-as-a-service/setting-up-and-configuring-an-azure-key-vault)

## <a name="next-steps"></a><span data-ttu-id="0ba89-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="0ba89-125">Next steps</span></span>
<span data-ttu-id="0ba89-126">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure Key Vault, follow these links to learn more about Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="0ba89-126">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure Key Vault, follow these links to learn more about Azure Automation.</span></span>

* <span data-ttu-id="0ba89-127">See the Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="0ba89-127">See the Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md).</span></span>
* <span data-ttu-id="0ba89-128">See the [Azure Key Vault PowerShell scripts](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).</span><span class="sxs-lookup"><span data-stu-id="0ba89-128">See the [Azure Key Vault PowerShell scripts](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).</span></span>

