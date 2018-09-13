---
title: Start and stop the Azure Stack Development Kit (ASDK) | Microsoft Docs
description: Learn how to start and shut down the Azure Stack Development Kit (ASDK).
services: azure-stack
documentationcenter: ''
author: jeffgilb
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/11/2018
ms.author: jeffgilb
ms.reviewer: misainat
ms.openlocfilehash: dfb565803746ecdda9b36a4e12a3c3f2b4d9e0d0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869952"
---
# <a name="start-and-stop-the-azure-stack-development-kit-asdk"></a><span data-ttu-id="3243c-103">Start and stop the Azure Stack Development Kit (ASDK)</span><span class="sxs-lookup"><span data-stu-id="3243c-103">Start and stop the Azure Stack Development Kit (ASDK)</span></span>
<span data-ttu-id="3243c-104">It is not recommended to simply restart the ASDK host computer.</span><span class="sxs-lookup"><span data-stu-id="3243c-104">It is not recommended to simply restart the ASDK host computer.</span></span> <span data-ttu-id="3243c-105">Instead, you should follow the procedures in this article to properly shut down and restart ASDK services.</span><span class="sxs-lookup"><span data-stu-id="3243c-105">Instead, you should follow the procedures in this article to properly shut down and restart ASDK services.</span></span> 

## <a name="stop-azure-stack"></a><span data-ttu-id="3243c-106">Stop Azure Stack</span><span class="sxs-lookup"><span data-stu-id="3243c-106">Stop Azure Stack</span></span> 
<span data-ttu-id="3243c-107">To properly shut down Azure Stack services, and the ASDK host computer, use the following PowerShell commands:</span><span class="sxs-lookup"><span data-stu-id="3243c-107">To properly shut down Azure Stack services, and the ASDK host computer, use the following PowerShell commands:</span></span>

1. <span data-ttu-id="3243c-108">Log in as AzureStack\CloudAdmin on the ASDK host computer.</span><span class="sxs-lookup"><span data-stu-id="3243c-108">Log in as AzureStack\CloudAdmin on the ASDK host computer.</span></span>
2. <span data-ttu-id="3243c-109">Open PowerShell as an administrator (not PowerShell ISE).</span><span class="sxs-lookup"><span data-stu-id="3243c-109">Open PowerShell as an administrator (not PowerShell ISE).</span></span>
3. <span data-ttu-id="3243c-110">Run the following commands to establish a privileged endpoint (PEP) session:</span><span class="sxs-lookup"><span data-stu-id="3243c-110">Run the following commands to establish a privileged endpoint (PEP) session:</span></span> 

   ```powershell
   Enter-PSSession -ComputerName AzS-ERCS01 -ConfigurationName PrivilegedEndpoint
   ```
4. <span data-ttu-id="3243c-111">Next, in the PEP session, use the **Stop-AzureStack** cmdlet to stop Azure Stack services and shut down the ASDK host computer:</span><span class="sxs-lookup"><span data-stu-id="3243c-111">Next, in the PEP session, use the **Stop-AzureStack** cmdlet to stop Azure Stack services and shut down the ASDK host computer:</span></span>

   ```powershell
   Stop-AzureStack
   ```
5. <span data-ttu-id="3243c-112">Review the PowerShell output to ensure all Azure Stack services are successfully shut down before the ASDK host computer shuts down.</span><span class="sxs-lookup"><span data-stu-id="3243c-112">Review the PowerShell output to ensure all Azure Stack services are successfully shut down before the ASDK host computer shuts down.</span></span> <span data-ttu-id="3243c-113">The shutdown process takes several minutes.</span><span class="sxs-lookup"><span data-stu-id="3243c-113">The shutdown process takes several minutes.</span></span>

## <a name="start-azure-stack"></a><span data-ttu-id="3243c-114">Start Azure Stack</span><span class="sxs-lookup"><span data-stu-id="3243c-114">Start Azure Stack</span></span> 
<span data-ttu-id="3243c-115">ASDK services should start automatically when the host computer is started.</span><span class="sxs-lookup"><span data-stu-id="3243c-115">ASDK services should start automatically when the host computer is started.</span></span> <span data-ttu-id="3243c-116">However, ASDK infrastructure services startup time varies based on the performance of the ASDK host computer hardware configuration.</span><span class="sxs-lookup"><span data-stu-id="3243c-116">However, ASDK infrastructure services startup time varies based on the performance of the ASDK host computer hardware configuration.</span></span> <span data-ttu-id="3243c-117">It can take several hours for all services to successfully restart in some cases.</span><span class="sxs-lookup"><span data-stu-id="3243c-117">It can take several hours for all services to successfully restart in some cases.</span></span>

<span data-ttu-id="3243c-118">Regardless of how the ASDK was shut down, you should use the following steps to verify that all Azure Stack services are started and fully operational after the host computer is powered on:</span><span class="sxs-lookup"><span data-stu-id="3243c-118">Regardless of how the ASDK was shut down, you should use the following steps to verify that all Azure Stack services are started and fully operational after the host computer is powered on:</span></span> 

1. <span data-ttu-id="3243c-119">Power on the ASDK host computer.</span><span class="sxs-lookup"><span data-stu-id="3243c-119">Power on the ASDK host computer.</span></span> 
2. <span data-ttu-id="3243c-120">Log in as AzureStack\CloudAdmin on the ASDK host computer.</span><span class="sxs-lookup"><span data-stu-id="3243c-120">Log in as AzureStack\CloudAdmin on the ASDK host computer.</span></span>
3. <span data-ttu-id="3243c-121">Open PowerShell as an administrator (not PowerShell ISE).</span><span class="sxs-lookup"><span data-stu-id="3243c-121">Open PowerShell as an administrator (not PowerShell ISE).</span></span>
4. <span data-ttu-id="3243c-122">Run the following commands to establish a privileged endpoint (PEP) session:</span><span class="sxs-lookup"><span data-stu-id="3243c-122">Run the following commands to establish a privileged endpoint (PEP) session:</span></span>

   ```powershell
   Enter-PSSession -ComputerName AzS-ERCS01 -ConfigurationName PrivilegedEndpoint
   ```
5. <span data-ttu-id="3243c-123">Next, in the PEP session, run the following commands to check the startup status of Azure Stack services:</span><span class="sxs-lookup"><span data-stu-id="3243c-123">Next, in the PEP session, run the following commands to check the startup status of Azure Stack services:</span></span>

   ```powershell
   Get-ActionStatus Start-AzureStack
   ```
6. <span data-ttu-id="3243c-124">Review the output to ensure that Azure Stack services have restarted successfully.</span><span class="sxs-lookup"><span data-stu-id="3243c-124">Review the output to ensure that Azure Stack services have restarted successfully.</span></span>

<span data-ttu-id="3243c-125">To learn more about the recommended procedures to properly shut down and restart Azure Stack services, see [Start and stop Azure Stack](.\.\azure-stack-start-and-stop.md).</span><span class="sxs-lookup"><span data-stu-id="3243c-125">To learn more about the recommended procedures to properly shut down and restart Azure Stack services, see [Start and stop Azure Stack](.\.\azure-stack-start-and-stop.md).</span></span> 

## <a name="troubleshoot-startup-and-shutdown"></a><span data-ttu-id="3243c-126">Troubleshoot startup and shutdown</span><span class="sxs-lookup"><span data-stu-id="3243c-126">Troubleshoot startup and shutdown</span></span> 
<span data-ttu-id="3243c-127">Perform these steps if Azure Stack services don't successfully start within two hours after you power on your ASDK host computer:</span><span class="sxs-lookup"><span data-stu-id="3243c-127">Perform these steps if Azure Stack services don't successfully start within two hours after you power on your ASDK host computer:</span></span>

1. <span data-ttu-id="3243c-128">Log in as AzureStack\CloudAdmin on the ASDK host computer.</span><span class="sxs-lookup"><span data-stu-id="3243c-128">Log in as AzureStack\CloudAdmin on the ASDK host computer.</span></span>
2. <span data-ttu-id="3243c-129">Open PowerShell as an administrator (not PowerShell ISE).</span><span class="sxs-lookup"><span data-stu-id="3243c-129">Open PowerShell as an administrator (not PowerShell ISE).</span></span>
3. <span data-ttu-id="3243c-130">Run the following commands to establish a privileged endpoint (PEP) session:</span><span class="sxs-lookup"><span data-stu-id="3243c-130">Run the following commands to establish a privileged endpoint (PEP) session:</span></span>

   ```powershell
   Enter-PSSession -ComputerName AzS-ERCS01 -ConfigurationName PrivilegedEndpoint
   ```
4. <span data-ttu-id="3243c-131">Next, in the PEP session, run the following commands to check the startup status of Azure Stack services:</span><span class="sxs-lookup"><span data-stu-id="3243c-131">Next, in the PEP session, run the following commands to check the startup status of Azure Stack services:</span></span>

   ```powershell
   Test-AzureStack
   ```
5. <span data-ttu-id="3243c-132">Review the output and resolve any errors.</span><span class="sxs-lookup"><span data-stu-id="3243c-132">Review the output and resolve any errors.</span></span> <span data-ttu-id="3243c-133">For more information, see [Run a validation test of Azure Stack](.\.\azure-stack-diagnostic-test.md).</span><span class="sxs-lookup"><span data-stu-id="3243c-133">For more information, see [Run a validation test of Azure Stack](.\.\azure-stack-diagnostic-test.md).</span></span>
6. <span data-ttu-id="3243c-134">Restart Azure Stack services from within the PEP session by running the **Start-AzureStack** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3243c-134">Restart Azure Stack services from within the PEP session by running the **Start-AzureStack** cmdlet:</span></span>

   ```powershell
   Start-AzureStack
   ```

<span data-ttu-id="3243c-135">If running **Start-AzureStack** results in a failure, visit the [Azure Stack support forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurestack) to get ASDK troubleshooting support.</span><span class="sxs-lookup"><span data-stu-id="3243c-135">If running **Start-AzureStack** results in a failure, visit the [Azure Stack support forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurestack) to get ASDK troubleshooting support.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3243c-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="3243c-136">Next steps</span></span> 
<span data-ttu-id="3243c-137">Learn more about Azure Stack diagnostic tool and issue logging, see [Azure Stack diagnostic tools](.\.\azure-stack-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="3243c-137">Learn more about Azure Stack diagnostic tool and issue logging, see [Azure Stack diagnostic tools](.\.\azure-stack-diagnostics.md).</span></span>
