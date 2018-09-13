---
title: Automate Azure Stack validation with PowerShell | Microsoft Docs
description: You can automate Azure Stack validation with PowerShell.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 07/24/2018
ms.author: mabrigg
ms.reviewer: johnhas
ms.openlocfilehash: 1cb4b1a7cfd72ea302676244a53af58e77215aa9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968570"
---
# <a name="automate-azure-stack-validation-with-powershell"></a><span data-ttu-id="7a293-103">Automate Azure Stack validation with PowerShell</span><span class="sxs-lookup"><span data-stu-id="7a293-103">Automate Azure Stack validation with PowerShell</span></span> 

<span data-ttu-id="7a293-104">Validation as a service (VaaS) provides the ability to automate the launching of tests using the **LaunchVaaSTests.ps1** script.</span><span class="sxs-lookup"><span data-stu-id="7a293-104">Validation as a service (VaaS) provides the ability to automate the launching of tests using the **LaunchVaaSTests.ps1** script.</span></span>

<span data-ttu-id="7a293-105">You can use PowerShell for the following workflow:</span><span class="sxs-lookup"><span data-stu-id="7a293-105">You can use PowerShell for the following workflow:</span></span>

- <span data-ttu-id="7a293-106">Test-pass workflow</span><span class="sxs-lookup"><span data-stu-id="7a293-106">Test-pass workflow</span></span>

<span data-ttu-id="7a293-107">This script encompasses the four elements of a workflow:</span><span class="sxs-lookup"><span data-stu-id="7a293-107">This script encompasses the four elements of a workflow:</span></span>

- <span data-ttu-id="7a293-108">Installs prerequisites.</span><span class="sxs-lookup"><span data-stu-id="7a293-108">Installs prerequisites.</span></span>
- <span data-ttu-id="7a293-109">Installs and starting the local agent.</span><span class="sxs-lookup"><span data-stu-id="7a293-109">Installs and starting the local agent.</span></span>
- <span data-ttu-id="7a293-110">Launches a category of tests, such as integration, functional, reliability.</span><span class="sxs-lookup"><span data-stu-id="7a293-110">Launches a category of tests, such as integration, functional, reliability.</span></span>
- <span data-ttu-id="7a293-111">Reports each test pass result for monitoring and report file generation.</span><span class="sxs-lookup"><span data-stu-id="7a293-111">Reports each test pass result for monitoring and report file generation.</span></span>

## <a name="launch-the-test-pass-workflow"></a><span data-ttu-id="7a293-112">Launch the test pass workflow</span><span class="sxs-lookup"><span data-stu-id="7a293-112">Launch the test pass workflow</span></span>

1. <span data-ttu-id="7a293-113">Open an elevated PowerShell prompt.</span><span class="sxs-lookup"><span data-stu-id="7a293-113">Open an elevated PowerShell prompt.</span></span>

2. <span data-ttu-id="7a293-114">Run the following script to download the automation script:</span><span class="sxs-lookup"><span data-stu-id="7a293-114">Run the following script to download the automation script:</span></span>

    ````PowerShell  
    New-Item -ItemType Directory -Path <VaaSLaunchDirectory>
    Set-Location <VaaSLaunchDirectory>
    Invoke-WebRequest -Uri https://vaastestpacksprodeastus.blob.core.windows.net/packages/Microsoft.VaaS.Scripts.3.0.0.nupkg -OutFile "LaunchVaaS.zip"
    Expand-Archive -Path ".\LaunchVaaS.zip" -DestinationPath .\ -Force
    ````

3. <span data-ttu-id="7a293-115">Run the following script with your values:</span><span class="sxs-lookup"><span data-stu-id="7a293-115">Run the following script with your values:</span></span>

    ````PowerShell  
    $VaaSAccountCreds = New-Object System.Management.Automation.PSCredential "<VaaSUserId>", (ConvertTo-SecureString "<VaaSUserPassword>"  -AsPlainText -Force)
    $ServiceAdminCreds = New-Object System.Management.Automation.PSCredential "<ServiceAdminUser>", (ConvertTo-SecureString "<ServiceAdminPassword>" -AsPlainText -Force)
    $TenantAdminCreds = New-Object System.Management.Automation.PSCredential "<TenantAdminUser>", (ConvertTo-SecureString "<TenantAdminPassword>" -AsPlainText -Force)
    .\LaunchVaaSTests.ps1 -VaaSAccountCreds $VaaSAccountCreds `
        -VaaSAccountTenantId <VaaSAccountTenantId> `
        -VaaSSolutionName <VaaSSolutionName> `
        -VaaSTestPassName <VaaSTestPassName> `
        -VaaSTestCategories Integration,Functional `
        -MaxScriptWaitTimeInHours 12 `
        -ServiceAdminCreds $ServiceAdminCreds `
    ````

    <span data-ttu-id="7a293-116">**Parameters**</span><span class="sxs-lookup"><span data-stu-id="7a293-116">**Parameters**</span></span>

    | <span data-ttu-id="7a293-117">Parameter</span><span class="sxs-lookup"><span data-stu-id="7a293-117">Parameter</span></span> | <span data-ttu-id="7a293-118">Description</span><span class="sxs-lookup"><span data-stu-id="7a293-118">Description</span></span> |
    | --- | --- |
    | <span data-ttu-id="7a293-119">VaaSUserld</span><span class="sxs-lookup"><span data-stu-id="7a293-119">VaaSUserld</span></span> | <span data-ttu-id="7a293-120">Your VaaS user ID.</span><span class="sxs-lookup"><span data-stu-id="7a293-120">Your VaaS user ID.</span></span> | 
    | <span data-ttu-id="7a293-121">VaaSUserPassword</span><span class="sxs-lookup"><span data-stu-id="7a293-121">VaaSUserPassword</span></span> | <span data-ttu-id="7a293-122">Your VaaS password.</span><span class="sxs-lookup"><span data-stu-id="7a293-122">Your VaaS password.</span></span> |
    | <span data-ttu-id="7a293-123">ServiceAdminUser</span><span class="sxs-lookup"><span data-stu-id="7a293-123">ServiceAdminUser</span></span> | <span data-ttu-id="7a293-124">Your Azure Stack service admin account.</span><span class="sxs-lookup"><span data-stu-id="7a293-124">Your Azure Stack service admin account.</span></span>  |
    | <span data-ttu-id="7a293-125">ServiceAdminPassword</span><span class="sxs-lookup"><span data-stu-id="7a293-125">ServiceAdminPassword</span></span> | <span data-ttu-id="7a293-126">Your Azure Stack service password.</span><span class="sxs-lookup"><span data-stu-id="7a293-126">Your Azure Stack service password.</span></span>  |
    | <span data-ttu-id="7a293-127">TenantAdminUser</span><span class="sxs-lookup"><span data-stu-id="7a293-127">TenantAdminUser</span></span> | <span data-ttu-id="7a293-128">The administrator for the primary tenant.</span><span class="sxs-lookup"><span data-stu-id="7a293-128">The administrator for the primary tenant.</span></span>  |
    | <span data-ttu-id="7a293-129">TenantAdminPassword</span><span class="sxs-lookup"><span data-stu-id="7a293-129">TenantAdminPassword</span></span> | <span data-ttu-id="7a293-130">The password for the primary tenant.</span><span class="sxs-lookup"><span data-stu-id="7a293-130">The password for the primary tenant.</span></span>  |
    | <span data-ttu-id="7a293-131">FunctionalCategory</span><span class="sxs-lookup"><span data-stu-id="7a293-131">FunctionalCategory</span></span>| <span data-ttu-id="7a293-132">Integration, Functional, or.</span><span class="sxs-lookup"><span data-stu-id="7a293-132">Integration, Functional, or.</span></span> <span data-ttu-id="7a293-133">Reliability.</span><span class="sxs-lookup"><span data-stu-id="7a293-133">Reliability.</span></span> <span data-ttu-id="7a293-134">If you use multiple values, separate each value by a comma.</span><span class="sxs-lookup"><span data-stu-id="7a293-134">If you use multiple values, separate each value by a comma.</span></span>  |

4. <span data-ttu-id="7a293-135">Review the results of your test.</span><span class="sxs-lookup"><span data-stu-id="7a293-135">Review the results of your test.</span></span> <span data-ttu-id="7a293-136">For information about reading your test results, see [Monitor tests](azure-stack-vaas-monitor-test.md).</span><span class="sxs-lookup"><span data-stu-id="7a293-136">For information about reading your test results, see [Monitor tests](azure-stack-vaas-monitor-test.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a293-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="7a293-137">Next steps</span></span>

 - <span data-ttu-id="7a293-138">To learn more about [Azure Stack validation as a service](https://docs.microsoft.com/azure/azure-stack/partner).</span><span class="sxs-lookup"><span data-stu-id="7a293-138">To learn more about [Azure Stack validation as a service](https://docs.microsoft.com/azure/azure-stack/partner).</span></span>
 - <span data-ttu-id="7a293-139">To learn more about PowerShell on Azure Stack, see the [Azure Stack Module](https://docs.microsoft.com/powershell/azure/azure-stack/overview?view=azurestackps-1.3.0) Reference.</span><span class="sxs-lookup"><span data-stu-id="7a293-139">To learn more about PowerShell on Azure Stack, see the [Azure Stack Module](https://docs.microsoft.com/powershell/azure/azure-stack/overview?view=azurestackps-1.3.0) Reference.</span></span>