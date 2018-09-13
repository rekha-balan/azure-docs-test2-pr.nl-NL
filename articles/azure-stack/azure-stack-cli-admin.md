---
title: Enable Azure CLI for Azure Stack users | Microsoft Docs
description: Learn how to use the cross-platform command-line interface (CLI) to manage and deploy resources on Azure Stack
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.assetid: f576079c-5384-4c23-b5a4-9ae165d1e3c3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/11/2018
ms.author: mabrigg
ms.openlocfilehash: 09c551ea7196ae20a60a5dd34c1cda889ff5df46
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856073"
---
# <a name="enable-azure-cli-for-azure-stack-users"></a><span data-ttu-id="9e11b-103">Enable Azure CLI for Azure Stack users</span><span class="sxs-lookup"><span data-stu-id="9e11b-103">Enable Azure CLI for Azure Stack users</span></span>

<span data-ttu-id="9e11b-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="9e11b-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="9e11b-105">You can provide the CA root certificate to users of Azure Stack so that they can use Azure CLI on their development machines.</span><span class="sxs-lookup"><span data-stu-id="9e11b-105">You can provide the CA root certificate to users of Azure Stack so that they can use Azure CLI on their development machines.</span></span> <span data-ttu-id="9e11b-106">Your users will need the certificate to manage resources through CLI.</span><span class="sxs-lookup"><span data-stu-id="9e11b-106">Your users will need the certificate to manage resources through CLI.</span></span>

* <span data-ttu-id="9e11b-107">**The Azure Stack CA root certificate** is required if users are using CLI from a workstation outside the Azure Stack Development Kit.</span><span class="sxs-lookup"><span data-stu-id="9e11b-107">**The Azure Stack CA root certificate** is required if users are using CLI from a workstation outside the Azure Stack Development Kit.</span></span>  

* <span data-ttu-id="9e11b-108">**The virtual machine aliases endpoint** provides an alias, like "UbuntuLTS" or "Win2012Datacenter," that references an image publisher, offer, SKU, and version as a single parameter when deploying VMs.</span><span class="sxs-lookup"><span data-stu-id="9e11b-108">**The virtual machine aliases endpoint** provides an alias, like "UbuntuLTS" or "Win2012Datacenter," that references an image publisher, offer, SKU, and version as a single parameter when deploying VMs.</span></span>  

<span data-ttu-id="9e11b-109">The following sections describe how to get these values.</span><span class="sxs-lookup"><span data-stu-id="9e11b-109">The following sections describe how to get these values.</span></span>

## <a name="export-the-azure-stack-ca-root-certificate"></a><span data-ttu-id="9e11b-110">Export the Azure Stack CA root certificate</span><span class="sxs-lookup"><span data-stu-id="9e11b-110">Export the Azure Stack CA root certificate</span></span>

<span data-ttu-id="9e11b-111">You can find the Azure Stack CA root certificate on the development kit and on a tenant virtual machine that is running within the development kit environment.</span><span class="sxs-lookup"><span data-stu-id="9e11b-111">You can find the Azure Stack CA root certificate on the development kit and on a tenant virtual machine that is running within the development kit environment.</span></span> <span data-ttu-id="9e11b-112">To export the Azure Stack root certificate in PEM format, sign in to your development kit or the tenant virtual machine and run the following script:</span><span class="sxs-lookup"><span data-stu-id="9e11b-112">To export the Azure Stack root certificate in PEM format, sign in to your development kit or the tenant virtual machine and run the following script:</span></span>

```powershell
$label = "AzureStackSelfSignedRootCert"
Write-Host "Getting certificate from the current user trusted store with subject CN=$label"
$root = Get-ChildItem Cert:\CurrentUser\Root | Where-Object Subject -eq "CN=$label" | select -First 1
if (-not $root)
{
    Log-Error "Certificate with subject CN=$label not found"
    return
}

Write-Host "Exporting certificate"
Export-Certificate -Type CERT -FilePath root.cer -Cert $root

Write-Host "Converting certificate to PEM format"
certutil -encode root.cer root.pem
```

## <a name="set-up-the-virtual-machine-aliases-endpoint"></a><span data-ttu-id="9e11b-113">Set up the virtual machine aliases endpoint</span><span class="sxs-lookup"><span data-stu-id="9e11b-113">Set up the virtual machine aliases endpoint</span></span>

<span data-ttu-id="9e11b-114">Azure Stack operators should set up a publicly accessible endpoint that hosts a virtual machine alias file.</span><span class="sxs-lookup"><span data-stu-id="9e11b-114">Azure Stack operators should set up a publicly accessible endpoint that hosts a virtual machine alias file.</span></span> <span data-ttu-id="9e11b-115">The virtual machine alias file is a JSON file that provides a common name for an image.</span><span class="sxs-lookup"><span data-stu-id="9e11b-115">The virtual machine alias file is a JSON file that provides a common name for an image.</span></span> <span data-ttu-id="9e11b-116">That name is subsequently specified when a VM is deployed as an Azure CLI parameter.</span><span class="sxs-lookup"><span data-stu-id="9e11b-116">That name is subsequently specified when a VM is deployed as an Azure CLI parameter.</span></span>  

<span data-ttu-id="9e11b-117">Before you add an entry to an alias file, make sure that you [download images from the Azure Marketplace](azure-stack-download-azure-marketplace-item.md), or have [published your own custom image](azure-stack-add-vm-image.md).</span><span class="sxs-lookup"><span data-stu-id="9e11b-117">Before you add an entry to an alias file, make sure that you [download images from the Azure Marketplace](azure-stack-download-azure-marketplace-item.md), or have [published your own custom image](azure-stack-add-vm-image.md).</span></span> <span data-ttu-id="9e11b-118">If you publish a custom image, make note of the publisher, offer, SKU, and version information that you specified during publishing.</span><span class="sxs-lookup"><span data-stu-id="9e11b-118">If you publish a custom image, make note of the publisher, offer, SKU, and version information that you specified during publishing.</span></span> <span data-ttu-id="9e11b-119">If it is an image from the marketplace, you can view the information by using the ```Get-AzureVMImage``` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9e11b-119">If it is an image from the marketplace, you can view the information by using the ```Get-AzureVMImage``` cmdlet.</span></span>  

<span data-ttu-id="9e11b-120">A [sample alias file](https://raw.githubusercontent.com/Azure/azure-rest-api-specs/master/arm-compute/quickstart-templates/aliases.json) with many common image aliases is available.</span><span class="sxs-lookup"><span data-stu-id="9e11b-120">A [sample alias file](https://raw.githubusercontent.com/Azure/azure-rest-api-specs/master/arm-compute/quickstart-templates/aliases.json) with many common image aliases is available.</span></span> <span data-ttu-id="9e11b-121">You can use that as a starting point.</span><span class="sxs-lookup"><span data-stu-id="9e11b-121">You can use that as a starting point.</span></span> <span data-ttu-id="9e11b-122">Host this file in a space where your CLI clients can reach it.</span><span class="sxs-lookup"><span data-stu-id="9e11b-122">Host this file in a space where your CLI clients can reach it.</span></span> <span data-ttu-id="9e11b-123">One way is to host the file in a blob storage account and share the URL with your users:</span><span class="sxs-lookup"><span data-stu-id="9e11b-123">One way is to host the file in a blob storage account and share the URL with your users:</span></span>

1. <span data-ttu-id="9e11b-124">Download the [sample file](https://raw.githubusercontent.com/Azure/azure-rest-api-specs/master/arm-compute/quickstart-templates/aliases.json) from GitHub.</span><span class="sxs-lookup"><span data-stu-id="9e11b-124">Download the [sample file](https://raw.githubusercontent.com/Azure/azure-rest-api-specs/master/arm-compute/quickstart-templates/aliases.json) from GitHub.</span></span>
2. <span data-ttu-id="9e11b-125">Create a new storage account in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="9e11b-125">Create a new storage account in Azure Stack.</span></span> <span data-ttu-id="9e11b-126">When that's done, create a new blob container.</span><span class="sxs-lookup"><span data-stu-id="9e11b-126">When that's done, create a new blob container.</span></span> <span data-ttu-id="9e11b-127">Set the access policy to "public."</span><span class="sxs-lookup"><span data-stu-id="9e11b-127">Set the access policy to "public."</span></span>  
3. <span data-ttu-id="9e11b-128">Upload the JSON file to the new container.</span><span class="sxs-lookup"><span data-stu-id="9e11b-128">Upload the JSON file to the new container.</span></span> <span data-ttu-id="9e11b-129">When that's done, you can view the URL of the blob by selecting the blob name and then selecting the URL from the blob properties.</span><span class="sxs-lookup"><span data-stu-id="9e11b-129">When that's done, you can view the URL of the blob by selecting the blob name and then selecting the URL from the blob properties.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e11b-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="9e11b-130">Next steps</span></span>

- [<span data-ttu-id="9e11b-131">Deploy templates with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9e11b-131">Deploy templates with Azure CLI</span></span>](azure-stack-deploy-template-command-line.md)

- [<span data-ttu-id="9e11b-132">Connect with PowerShell</span><span class="sxs-lookup"><span data-stu-id="9e11b-132">Connect with PowerShell</span></span>](azure-stack-connect-powershell.md)

- [<span data-ttu-id="9e11b-133">Manage user permissions</span><span class="sxs-lookup"><span data-stu-id="9e11b-133">Manage user permissions</span></span>](azure-stack-manage-permissions.md)
