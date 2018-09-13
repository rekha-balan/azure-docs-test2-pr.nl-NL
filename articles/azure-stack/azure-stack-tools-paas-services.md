---
title: Tools and PaaS services for Azure Stack | Microsoft Docs
description: Learn how to get started with PaaS services in Azure Stack.
services: azure-stack
documentationcenter: ''
author: ErikjeMS
manager: byronr
editor: ''
ms.assetid: 2ce8d7e3-bc5d-4d61-8ab8-e8f61df40675
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: erikje
ms.openlocfilehash: 1b751162631611f43841019d7c3f0af8aa3373c0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550052"
---
# <a name="tools-and-paas-services-for-azure-stack"></a><span data-ttu-id="5dcac-103">Tools and PaaS services for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="5dcac-103">Tools and PaaS services for Azure Stack</span></span>

<span data-ttu-id="5dcac-104">You can deploy [Platform as a Service](https://azure.microsoft.com/overview/what-is-paas/) (PaaS) services for Azure Stack from Microsoft and other 3rd party providers.</span><span class="sxs-lookup"><span data-stu-id="5dcac-104">You can deploy [Platform as a Service](https://azure.microsoft.com/overview/what-is-paas/) (PaaS) services for Azure Stack from Microsoft and other 3rd party providers.</span></span> <span data-ttu-id="5dcac-105">You can also download the tools described below.</span><span class="sxs-lookup"><span data-stu-id="5dcac-105">You can also download the tools described below.</span></span> <span data-ttu-id="5dcac-106">If you want to be notified of new services and tools, follow #AzureStack on Twitter.</span><span class="sxs-lookup"><span data-stu-id="5dcac-106">If you want to be notified of new services and tools, follow #AzureStack on Twitter.</span></span>

## <a name="paas-services"></a><span data-ttu-id="5dcac-107">PaaS services</span><span class="sxs-lookup"><span data-stu-id="5dcac-107">PaaS services</span></span>

[<span data-ttu-id="5dcac-108">Add an App Service resource provider to Azure Stack</span><span class="sxs-lookup"><span data-stu-id="5dcac-108">Add an App Service resource provider to Azure Stack</span></span>](https://docs.microsoft.com/azure/azure-stack/azure-stack-app-service-overview)

[<span data-ttu-id="5dcac-109">Add a SQL Server resource provider to Azure Stack</span><span class="sxs-lookup"><span data-stu-id="5dcac-109">Add a SQL Server resource provider to Azure Stack</span></span>](https://docs.microsoft.com/azure/azure-stack/azure-stack-sql-resource-provider-deploy)

[<span data-ttu-id="5dcac-110">Add a MySQL Server resource provider to Azure Stack</span><span class="sxs-lookup"><span data-stu-id="5dcac-110">Add a MySQL Server resource provider to Azure Stack</span></span>](https://docs.microsoft.com/azure/azure-stack/azure-stack-mysql-resource-provider-deploy)


## <a name="template-tools"></a><span data-ttu-id="5dcac-111">Template tools</span><span class="sxs-lookup"><span data-stu-id="5dcac-111">Template tools</span></span>
### <a name="azure-stack-github-templates"></a><span data-ttu-id="5dcac-112">Azure Stack GitHub templates</span><span class="sxs-lookup"><span data-stu-id="5dcac-112">Azure Stack GitHub templates</span></span>
<span data-ttu-id="5dcac-113">Explore the growing collection of [Azure Stack GitHub Templates](https://github.com/Azure/AzureStack-QuickStart-Templates).</span><span class="sxs-lookup"><span data-stu-id="5dcac-113">Explore the growing collection of [Azure Stack GitHub Templates](https://github.com/Azure/AzureStack-QuickStart-Templates).</span></span> <span data-ttu-id="5dcac-114">Just like [Azure](https://github.com/Azure/azure-quickstart-templates), these “Quick Start” Azure Resource Manager templates aim to get you started with simple building blocks and examples, ready to deploy on the Microsoft Azure Stack Technical Preview Proof of Concept Environment.</span><span class="sxs-lookup"><span data-stu-id="5dcac-114">Just like [Azure](https://github.com/Azure/azure-quickstart-templates), these “Quick Start” Azure Resource Manager templates aim to get you started with simple building blocks and examples, ready to deploy on the Microsoft Azure Stack Technical Preview Proof of Concept Environment.</span></span> <span data-ttu-id="5dcac-115">Included are first party workload examples for [ad-non-ha](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/ad-non-ha), [sql-2014-non-ha](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/sql-2014-non-ha), [sharepoint-2013-non-ha](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/sharepoint-2013-non-ha), as well as several simple 101 templates like [101-simple-windows-vm](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-simple-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="5dcac-115">Included are first party workload examples for [ad-non-ha](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/ad-non-ha), [sql-2014-non-ha](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/sql-2014-non-ha), [sharepoint-2013-non-ha](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/sharepoint-2013-non-ha), as well as several simple 101 templates like [101-simple-windows-vm](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-simple-windows-vm).</span></span>

### <a name="marketplace-item-packaging-tool-and-sample"></a><span data-ttu-id="5dcac-116">Marketplace item packaging tool and sample</span><span class="sxs-lookup"><span data-stu-id="5dcac-116">Marketplace item packaging tool and sample</span></span>
<span data-ttu-id="5dcac-117">[Download and use the Packaging tool](http://www.aka.ms/azurestackmarketplaceitem) to create marketplace items for your own custom templates to add to the Azure Stack marketplace.</span><span class="sxs-lookup"><span data-stu-id="5dcac-117">[Download and use the Packaging tool](http://www.aka.ms/azurestackmarketplaceitem) to create marketplace items for your own custom templates to add to the Azure Stack marketplace.</span></span> <span data-ttu-id="5dcac-118">Instructions on how to create a marketplace item and make it available to your tenants can be found in [Create Marketplace item](azure-stack-create-and-publish-marketplace-item.md).</span><span class="sxs-lookup"><span data-stu-id="5dcac-118">Instructions on how to create a marketplace item and make it available to your tenants can be found in [Create Marketplace item](azure-stack-create-and-publish-marketplace-item.md).</span></span>

## <a name="developer-tools"></a><span data-ttu-id="5dcac-119">Developer tools</span><span class="sxs-lookup"><span data-stu-id="5dcac-119">Developer tools</span></span>
### <a name="use-visual-studio-and-azure-stack-tp2-on-the-mas-con01-virtual-machine"></a><span data-ttu-id="5dcac-120">Use Visual Studio and Azure Stack TP2 on the MAS-CON01 virtual machine</span><span class="sxs-lookup"><span data-stu-id="5dcac-120">Use Visual Studio and Azure Stack TP2 on the MAS-CON01 virtual machine</span></span>
<span data-ttu-id="5dcac-121">If you want to use Visual Studio on the console VM to work with Azure Stack templates, you must install the correct versions of the required tools.</span><span class="sxs-lookup"><span data-stu-id="5dcac-121">If you want to use Visual Studio on the console VM to work with Azure Stack templates, you must install the correct versions of the required tools.</span></span> <span data-ttu-id="5dcac-122">Use the following procedure to install the supported versions for TP2.</span><span class="sxs-lookup"><span data-stu-id="5dcac-122">Use the following procedure to install the supported versions for TP2.</span></span>

1. <span data-ttu-id="5dcac-123">Use Remote Desktop Connection to log in to the MAS-CON01 virtual machine with the azurestack\azurestackadmin credentials.</span><span class="sxs-lookup"><span data-stu-id="5dcac-123">Use Remote Desktop Connection to log in to the MAS-CON01 virtual machine with the azurestack\azurestackadmin credentials.</span></span>
2. <span data-ttu-id="5dcac-124">Install and open Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="5dcac-124">Install and open Web Platform Installer.</span></span>
3. <span data-ttu-id="5dcac-125">Find and install **Visual Studio Community 2015 with Microsoft Azure SDK - 2.9.5**.</span><span class="sxs-lookup"><span data-stu-id="5dcac-125">Find and install **Visual Studio Community 2015 with Microsoft Azure SDK - 2.9.5**.</span></span>
4. <span data-ttu-id="5dcac-126">Using **Add/Remove Programs**, uninstall the **Microsoft Azure PowerShell (Sept)** that gets installed as part of the SDK.</span><span class="sxs-lookup"><span data-stu-id="5dcac-126">Using **Add/Remove Programs**, uninstall the **Microsoft Azure PowerShell (Sept)** that gets installed as part of the SDK.</span></span>
5. <span data-ttu-id="5dcac-127">Open the Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="5dcac-127">Open the Web Platform Installer.</span></span>
6. <span data-ttu-id="5dcac-128">Find and install **Microsoft Azure PowerShell - Azure Stack Technical Preview 2**.</span><span class="sxs-lookup"><span data-stu-id="5dcac-128">Find and install **Microsoft Azure PowerShell - Azure Stack Technical Preview 2**.</span></span> 
7. <span data-ttu-id="5dcac-129">Restart the MAS-CON01 virtual machine.</span><span class="sxs-lookup"><span data-stu-id="5dcac-129">Restart the MAS-CON01 virtual machine.</span></span>
8. <span data-ttu-id="5dcac-130">Use Remote Desktop Connection to log in to the MAS-CON01 virtual machine with the azurestack\azurestackadmin credentials.</span><span class="sxs-lookup"><span data-stu-id="5dcac-130">Use Remote Desktop Connection to log in to the MAS-CON01 virtual machine with the azurestack\azurestackadmin credentials.</span></span>
9. <span data-ttu-id="5dcac-131">Open Visual Studio and validate that you can connect to the Azure Stack environment, get templates, and so on.</span><span class="sxs-lookup"><span data-stu-id="5dcac-131">Open Visual Studio and validate that you can connect to the Azure Stack environment, get templates, and so on.</span></span> 

### <a name="azure-powershell-sdk"></a><span data-ttu-id="5dcac-132">Azure PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="5dcac-132">Azure PowerShell SDK</span></span>
<span data-ttu-id="5dcac-133">Azure PowerShell is a module that provides cmdlets to manage Azure and Azure Stack with Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5dcac-133">Azure PowerShell is a module that provides cmdlets to manage Azure and Azure Stack with Windows PowerShell.</span></span> <span data-ttu-id="5dcac-134">You can use the cmdlets to create, test, deploy, and manage solutions and services delivered through the Azure Stack platform.</span><span class="sxs-lookup"><span data-stu-id="5dcac-134">You can use the cmdlets to create, test, deploy, and manage solutions and services delivered through the Azure Stack platform.</span></span>
<span data-ttu-id="5dcac-135">[Download Azure PowerShell SDK](http://aka.ms/azStackPsh) and [install PowerShell](azure-stack-connect-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="5dcac-135">[Download Azure PowerShell SDK](http://aka.ms/azStackPsh) and [install PowerShell](azure-stack-connect-powershell.md).</span></span>

### <a name="azure-cross-platform-command-line-interfaces"></a><span data-ttu-id="5dcac-136">Azure cross platform command line interfaces</span><span class="sxs-lookup"><span data-stu-id="5dcac-136">Azure cross platform command line interfaces</span></span>
<span data-ttu-id="5dcac-137">Quickly install the Azure Command-Line Interface (Azure CLI) to use a set of open-source shell-based commands for creating and managing resources in Microsoft Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="5dcac-137">Quickly install the Azure Command-Line Interface (Azure CLI) to use a set of open-source shell-based commands for creating and managing resources in Microsoft Azure Stack.</span></span>

[<span data-ttu-id="5dcac-138">Download the Windows CLI</span><span class="sxs-lookup"><span data-stu-id="5dcac-138">Download the Windows CLI</span></span>](http://aka.ms/azstack-windows-cli)

[<span data-ttu-id="5dcac-139">Download the Mac CLI</span><span class="sxs-lookup"><span data-stu-id="5dcac-139">Download the Mac CLI</span></span>](http://aka.ms/azstack-linux-cli)

[<span data-ttu-id="5dcac-140">Download the Linux CLI</span><span class="sxs-lookup"><span data-stu-id="5dcac-140">Download the Linux CLI</span></span>](http://aka.ms/azstack-mac-cli)

> [!NOTE]
> * <span data-ttu-id="5dcac-141">If you’re on a Mac or Linux machine, you can also get the CLI by using the command `npm install -g azure-cli@0.10.4`</span><span class="sxs-lookup"><span data-stu-id="5dcac-141">If you’re on a Mac or Linux machine, you can also get the CLI by using the command `npm install -g azure-cli@0.10.4`</span></span></br>
> * <span data-ttu-id="5dcac-142">If you're getting certificate validation issues, run the command `set NODE_TLS_REJECT_UNAUTHORIZED=0`</span><span class="sxs-lookup"><span data-stu-id="5dcac-142">If you're getting certificate validation issues, run the command `set NODE_TLS_REJECT_UNAUTHORIZED=0`</span></span>
> 
> 

