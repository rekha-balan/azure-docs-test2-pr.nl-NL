---
title: Passing credentials to Azure using DSC | Microsoft Docs
description: Overview on securely passing credentials to Azure virtual machines using PowerShell Desired State Configuration
services: virtual-machines-windows
documentationcenter: ''
author: zjalexander
manager: timlt
editor: ''
tags: azure-service-management,azure-resource-manager
keywords: ''
ms.assetid: ea76b7e8-b576-445a-8107-88ea2f3876b9
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 09/15/2016
ms.author: zachal
ms.openlocfilehash: e9c6068a4254f3ab9676388ffb90f927363fce0f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553930"
---
# <a name="passing-credentials-to-the-azure-dsc-extension-handler"></a><span data-ttu-id="565f0-103">Passing credentials to the Azure DSC extension handler</span><span class="sxs-lookup"><span data-stu-id="565f0-103">Passing credentials to the Azure DSC extension handler</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="565f0-104">This article covers the Desired State Configuration extension for Azure.</span><span class="sxs-lookup"><span data-stu-id="565f0-104">This article covers the Desired State Configuration extension for Azure.</span></span> <span data-ttu-id="565f0-105">An overview of the DSC extension handler can be found at [Introduction to the Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="565f0-105">An overview of the DSC extension handler can be found at [Introduction to the Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="passing-in-credentials"></a><span data-ttu-id="565f0-106">Passing in credentials</span><span class="sxs-lookup"><span data-stu-id="565f0-106">Passing in credentials</span></span>
<span data-ttu-id="565f0-107">As a part of the configuration process, you may need to set up user accounts, access services, or install a program in a user context.</span><span class="sxs-lookup"><span data-stu-id="565f0-107">As a part of the configuration process, you may need to set up user accounts, access services, or install a program in a user context.</span></span> <span data-ttu-id="565f0-108">To do these things, you need to provide credentials.</span><span class="sxs-lookup"><span data-stu-id="565f0-108">To do these things, you need to provide credentials.</span></span> 

<span data-ttu-id="565f0-109">DSC allows for parameterized configurations in which credentials are passed into the configuration and securely stored in MOF files.</span><span class="sxs-lookup"><span data-stu-id="565f0-109">DSC allows for parameterized configurations in which credentials are passed into the configuration and securely stored in MOF files.</span></span> <span data-ttu-id="565f0-110">The Azure Extension Handler simplifies credential management by providing automatic management of certificates.</span><span class="sxs-lookup"><span data-stu-id="565f0-110">The Azure Extension Handler simplifies credential management by providing automatic management of certificates.</span></span> 

<span data-ttu-id="565f0-111">Consider the following DSC configuration script that creates a local user account with the specified password:</span><span class="sxs-lookup"><span data-stu-id="565f0-111">Consider the following DSC configuration script that creates a local user account with the specified password:</span></span>

<span data-ttu-id="565f0-112">*user_configuration.ps1*</span><span class="sxs-lookup"><span data-stu-id="565f0-112">*user_configuration.ps1*</span></span>

```
configuration Main
{
    param(
        [Parameter(Mandatory=$true)]
        [ValidateNotNullorEmpty()]
        [PSCredential]
        $Credential
    )    
    Node localhost {       
        User LocalUserAccount
        {
            Username = $Credential.UserName
            Password = $Credential
            Disabled = $false
            Ensure = "Present"
            FullName = "Local User Account"
            Description = "Local User Account"
            PasswordNeverExpires = $true
        } 
    }  
} 
```

<span data-ttu-id="565f0-113">It is important to include *node localhost* as part of the configuration.</span><span class="sxs-lookup"><span data-stu-id="565f0-113">It is important to include *node localhost* as part of the configuration.</span></span> <span data-ttu-id="565f0-114">If this statement is missing, the following steps do not work as the extension handler specifically looks for the node localhost statement.</span><span class="sxs-lookup"><span data-stu-id="565f0-114">If this statement is missing, the following steps do not work as the extension handler specifically looks for the node localhost statement.</span></span> <span data-ttu-id="565f0-115">It is also important to include the typecast *[PsCredential]*, as this specific type triggers the extension to encrypt the credential.</span><span class="sxs-lookup"><span data-stu-id="565f0-115">It is also important to include the typecast *[PsCredential]*, as this specific type triggers the extension to encrypt the credential.</span></span> 

<span data-ttu-id="565f0-116">Publish this script to blob storage:</span><span class="sxs-lookup"><span data-stu-id="565f0-116">Publish this script to blob storage:</span></span>

`Publish-AzureVMDscConfiguration -ConfigurationPath .\user_configuration.ps1`

<span data-ttu-id="565f0-117">Set the Azure DSC extension and provide the credential:</span><span class="sxs-lookup"><span data-stu-id="565f0-117">Set the Azure DSC extension and provide the credential:</span></span>

```
$configurationName = "Main"
$configurationArguments = @{ Credential = Get-Credential }
$configurationArchive = "user_configuration.ps1.zip"
$vm = Get-AzureVM "example-1"

$vm = Set-AzureVMDSCExtension -VM $vm -ConfigurationArchive $configurationArchive 
-ConfigurationName $configurationName -ConfigurationArgument @configurationArguments

$vm | Update-AzureVM
```
## <a name="how-credentials-are-secured"></a><span data-ttu-id="565f0-118">How credentials are secured</span><span class="sxs-lookup"><span data-stu-id="565f0-118">How credentials are secured</span></span>
<span data-ttu-id="565f0-119">Running this code prompts for a credential.</span><span class="sxs-lookup"><span data-stu-id="565f0-119">Running this code prompts for a credential.</span></span> <span data-ttu-id="565f0-120">Once it is provided, it is stored in memory briefly.</span><span class="sxs-lookup"><span data-stu-id="565f0-120">Once it is provided, it is stored in memory briefly.</span></span> <span data-ttu-id="565f0-121">When it is published with `Set-AzureVmDscExtension` cmdlet, it is transmitted over HTTPS to the VM, where Azure stores it encrypted on disk, using the local VM certificate.</span><span class="sxs-lookup"><span data-stu-id="565f0-121">When it is published with `Set-AzureVmDscExtension` cmdlet, it is transmitted over HTTPS to the VM, where Azure stores it encrypted on disk, using the local VM certificate.</span></span> <span data-ttu-id="565f0-122">Then it is briefly decrypted in memory and re-encrypted to pass it to DSC.</span><span class="sxs-lookup"><span data-stu-id="565f0-122">Then it is briefly decrypted in memory and re-encrypted to pass it to DSC.</span></span>

<span data-ttu-id="565f0-123">This behavior is different than [using secure configurations without the extension handler](https://msdn.microsoft.com/powershell/dsc/securemof).</span><span class="sxs-lookup"><span data-stu-id="565f0-123">This behavior is different than [using secure configurations without the extension handler](https://msdn.microsoft.com/powershell/dsc/securemof).</span></span> <span data-ttu-id="565f0-124">The Azure environment gives a way to transmit configuration data securely via certificates.</span><span class="sxs-lookup"><span data-stu-id="565f0-124">The Azure environment gives a way to transmit configuration data securely via certificates.</span></span> <span data-ttu-id="565f0-125">When using the DSC extension handler, there is no need to provide $CertificatePath or a $CertificateID / $Thumbprint entry in ConfigurationData.</span><span class="sxs-lookup"><span data-stu-id="565f0-125">When using the DSC extension handler, there is no need to provide $CertificatePath or a $CertificateID / $Thumbprint entry in ConfigurationData.</span></span>

## <a name="next-steps"></a><span data-ttu-id="565f0-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="565f0-126">Next steps</span></span>
<span data-ttu-id="565f0-127">For more information on the Azure DSC extension handler, see [Introduction to the Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="565f0-127">For more information on the Azure DSC extension handler, see [Introduction to the Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="565f0-128">Examine the [Azure Resource Manager template for the DSC extension](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="565f0-128">Examine the [Azure Resource Manager template for the DSC extension](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="565f0-129">For more information about PowerShell DSC, [visit the PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="565f0-129">For more information about PowerShell DSC, [visit the PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

<span data-ttu-id="565f0-130">To find additional functionality you can manage with PowerShell DSC, [browse the PowerShell gallery](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) for more DSC resources.</span><span class="sxs-lookup"><span data-stu-id="565f0-130">To find additional functionality you can manage with PowerShell DSC, [browse the PowerShell gallery](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) for more DSC resources.</span></span>

