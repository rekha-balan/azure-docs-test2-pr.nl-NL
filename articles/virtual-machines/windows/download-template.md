---
title: Download the template for an Azure VM | Microsoft Docs
description: Download the templatefor a VM to help with automating deployments in the Resource Manager deployment model
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 51ef4f51-0942-4249-afea-4a3f87ce1ff8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: fed360253ba57c318f2ade53ca2bde104a2ea56a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555349"
---
# <a name="download-the-template-for-a-vm"></a><span data-ttu-id="5db6e-103">Download the template for a VM</span><span class="sxs-lookup"><span data-stu-id="5db6e-103">Download the template for a VM</span></span>
<span data-ttu-id="5db6e-104">When you create a VM in Azure using the portal or PowerShell, a Resource Manager template is automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="5db6e-104">When you create a VM in Azure using the portal or PowerShell, a Resource Manager template is automatically created for you.</span></span> <span data-ttu-id="5db6e-105">You can use this template to quickly duplicate a deployment.</span><span class="sxs-lookup"><span data-stu-id="5db6e-105">You can use this template to quickly duplicate a deployment.</span></span> <span data-ttu-id="5db6e-106">The template contains information about all of the resources in a resource group.</span><span class="sxs-lookup"><span data-stu-id="5db6e-106">The template contains information about all of the resources in a resource group.</span></span> <span data-ttu-id="5db6e-107">For a virtual machine, this means the template contains everything that is created in support of the VM in that resource group, including the networking resources.</span><span class="sxs-lookup"><span data-stu-id="5db6e-107">For a virtual machine, this means the template contains everything that is created in support of the VM in that resource group, including the networking resources.</span></span>

## <a name="download-the-template-using-the-portal"></a><span data-ttu-id="5db6e-108">Download the template using the portal</span><span class="sxs-lookup"><span data-stu-id="5db6e-108">Download the template using the portal</span></span>
1. <span data-ttu-id="5db6e-109">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5db6e-109">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="5db6e-110">One the hub menu, select **Virtual Machines**.</span><span class="sxs-lookup"><span data-stu-id="5db6e-110">One the hub menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="5db6e-111">Select the virtual machine from the list.</span><span class="sxs-lookup"><span data-stu-id="5db6e-111">Select the virtual machine from the list.</span></span>
4. <span data-ttu-id="5db6e-112">Select **Automation script**.</span><span class="sxs-lookup"><span data-stu-id="5db6e-112">Select **Automation script**.</span></span>
5. <span data-ttu-id="5db6e-113">Select **Download** and save the .zip file to your local computer.</span><span class="sxs-lookup"><span data-stu-id="5db6e-113">Select **Download** and save the .zip file to your local computer.</span></span>
6. <span data-ttu-id="5db6e-114">Open the .zip file and extract the files to a folder.</span><span class="sxs-lookup"><span data-stu-id="5db6e-114">Open the .zip file and extract the files to a folder.</span></span> <span data-ttu-id="5db6e-115">The .zip file will contain:</span><span class="sxs-lookup"><span data-stu-id="5db6e-115">The .zip file will contain:</span></span>
   
   * <span data-ttu-id="5db6e-116">deploy.ps1</span><span class="sxs-lookup"><span data-stu-id="5db6e-116">deploy.ps1</span></span>
   * <span data-ttu-id="5db6e-117">deploy.sh</span><span class="sxs-lookup"><span data-stu-id="5db6e-117">deploy.sh</span></span> 
   * <span data-ttu-id="5db6e-118">deployer.rb</span><span class="sxs-lookup"><span data-stu-id="5db6e-118">deployer.rb</span></span>
   * <span data-ttu-id="5db6e-119">DeploymentHelper.cs</span><span class="sxs-lookup"><span data-stu-id="5db6e-119">DeploymentHelper.cs</span></span>
   * <span data-ttu-id="5db6e-120">parameters.json</span><span class="sxs-lookup"><span data-stu-id="5db6e-120">parameters.json</span></span>
   * <span data-ttu-id="5db6e-121">template.json</span><span class="sxs-lookup"><span data-stu-id="5db6e-121">template.json</span></span>

<span data-ttu-id="5db6e-122">The template.json file is the template.</span><span class="sxs-lookup"><span data-stu-id="5db6e-122">The template.json file is the template.</span></span>

## <a name="download-the-template-using-powershell"></a><span data-ttu-id="5db6e-123">Download the template using PowerShell</span><span class="sxs-lookup"><span data-stu-id="5db6e-123">Download the template using PowerShell</span></span>
<span data-ttu-id="5db6e-124">You can also download the .json template file using the [Export-AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5db6e-124">You can also download the .json template file using the [Export-AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx) cmdlet.</span></span> <span data-ttu-id="5db6e-125">You can use the `-path` parameter to provide the filename and path for the .json file.</span><span class="sxs-lookup"><span data-stu-id="5db6e-125">You can use the `-path` parameter to provide the filename and path for the .json file.</span></span> <span data-ttu-id="5db6e-126">This example shows how to download the template for the resource group named **myResourceGroup** to the **C:\users\public\downloads** folder on your local computer.</span><span class="sxs-lookup"><span data-stu-id="5db6e-126">This example shows how to download the template for the resource group named **myResourceGroup** to the **C:\users\public\downloads** folder on your local computer.</span></span>

```powershell
    Export-AzureRmResourceGroup -ResourceGroupName "myResourceGroup" -Path "C:\users\public\downloads"
```

## <a name="next-steps"></a><span data-ttu-id="5db6e-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="5db6e-127">Next steps</span></span>
<span data-ttu-id="5db6e-128">To learn more about deploying resources using templates, see [Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="5db6e-128">To learn more about deploying resources using templates, see [Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

