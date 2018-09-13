---
title: Start and stop Azure Stack | Microsoft Docs
description: Learn how to start and shut down Azure Stack.
services: azure-stack
documentationcenter: ''
author: jeffgilb
manager: femila
editor: ''
ms.assetid: 43BF9DCF-F1B7-49B5-ADC5-1DA3AF9668CA
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/09/2018
ms.author: jeffgilb
ms.reviewer: misainat
ms.openlocfilehash: dd1e64d5ad6982c85a8205e3036d30a2ede92f7c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967634"
---
# <a name="start-and-stop-azure-stack"></a><span data-ttu-id="b9553-103">Start and stop Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b9553-103">Start and stop Azure Stack</span></span>
<span data-ttu-id="b9553-104">You should follow the procedures in this article to properly shut down and restart Azure Stack services.</span><span class="sxs-lookup"><span data-stu-id="b9553-104">You should follow the procedures in this article to properly shut down and restart Azure Stack services.</span></span> <span data-ttu-id="b9553-105">Shutdown will physically power off the entire Azure Stack environment.</span><span class="sxs-lookup"><span data-stu-id="b9553-105">Shutdown will physically power off the entire Azure Stack environment.</span></span> <span data-ttu-id="b9553-106">Startup powers on all infrastructure roles and returns tenant resources to the power state they were in prior to shutdown.</span><span class="sxs-lookup"><span data-stu-id="b9553-106">Startup powers on all infrastructure roles and returns tenant resources to the power state they were in prior to shutdown.</span></span>

## <a name="stop-azure-stack"></a><span data-ttu-id="b9553-107">Stop Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b9553-107">Stop Azure Stack</span></span> 

<span data-ttu-id="b9553-108">Shut down Azure Stack with the following steps:</span><span class="sxs-lookup"><span data-stu-id="b9553-108">Shut down Azure Stack with the following steps:</span></span>

1. <span data-ttu-id="b9553-109">Prepare all workloads running on your Azure Stack environment's tenant resources for the upcoming shutdown.</span><span class="sxs-lookup"><span data-stu-id="b9553-109">Prepare all workloads running on your Azure Stack environment's tenant resources for the upcoming shutdown.</span></span> 

2. <span data-ttu-id="b9553-110">Open a Privileged Endpoint Session (PEP) from a machine with network access to the Azure Stack ERCS VMs.</span><span class="sxs-lookup"><span data-stu-id="b9553-110">Open a Privileged Endpoint Session (PEP) from a machine with network access to the Azure Stack ERCS VMs.</span></span> <span data-ttu-id="b9553-111">For instructions, see [Using the privileged endpoint in Azure Stack](azure-stack-privileged-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="b9553-111">For instructions, see [Using the privileged endpoint in Azure Stack](azure-stack-privileged-endpoint.md).</span></span>

3. <span data-ttu-id="b9553-112">From the PEP, run:</span><span class="sxs-lookup"><span data-stu-id="b9553-112">From the PEP, run:</span></span>

    ```powershell
      Stop-AzureStack
    ```

4. <span data-ttu-id="b9553-113">Wait for all physical Azure Stack nodes to power off.</span><span class="sxs-lookup"><span data-stu-id="b9553-113">Wait for all physical Azure Stack nodes to power off.</span></span>

> [!Note]  
> <span data-ttu-id="b9553-114">You can verify the power status of a physical node by following the instructions from the Original Equipment Manufacturer (OEM) who supplied your Azure Stack hardware.</span><span class="sxs-lookup"><span data-stu-id="b9553-114">You can verify the power status of a physical node by following the instructions from the Original Equipment Manufacturer (OEM) who supplied your Azure Stack hardware.</span></span> 

## <a name="start-azure-stack"></a><span data-ttu-id="b9553-115">Start Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b9553-115">Start Azure Stack</span></span> 

<span data-ttu-id="b9553-116">Start Azure Stack with the following steps.</span><span class="sxs-lookup"><span data-stu-id="b9553-116">Start Azure Stack with the following steps.</span></span> <span data-ttu-id="b9553-117">Follow these steps regardless of how Azure Stack stopped.</span><span class="sxs-lookup"><span data-stu-id="b9553-117">Follow these steps regardless of how Azure Stack stopped.</span></span>

1. <span data-ttu-id="b9553-118">Power on each of the physical nodes in your Azure Stack environment.</span><span class="sxs-lookup"><span data-stu-id="b9553-118">Power on each of the physical nodes in your Azure Stack environment.</span></span> <span data-ttu-id="b9553-119">Verify the power on instructions for the physical nodes by following the instructions from the Original Equipment Manufacturer (OEM) who supplied the hardware for your Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="b9553-119">Verify the power on instructions for the physical nodes by following the instructions from the Original Equipment Manufacturer (OEM) who supplied the hardware for your Azure Stack.</span></span>

2. <span data-ttu-id="b9553-120">Wait until the Azure Stack infrastructure services starts.</span><span class="sxs-lookup"><span data-stu-id="b9553-120">Wait until the Azure Stack infrastructure services starts.</span></span> <span data-ttu-id="b9553-121">Azure Stack infrastructure services can require two hours to finishing the start process.</span><span class="sxs-lookup"><span data-stu-id="b9553-121">Azure Stack infrastructure services can require two hours to finishing the start process.</span></span> <span data-ttu-id="b9553-122">You can verify the start status of Azure Stack with the [**Get-ActionStatus** cmdlet](#get-the-startup-status-for-azure-stack).</span><span class="sxs-lookup"><span data-stu-id="b9553-122">You can verify the start status of Azure Stack with the [**Get-ActionStatus** cmdlet](#get-the-startup-status-for-azure-stack).</span></span>

3. <span data-ttu-id="b9553-123">Ensure that all of your tenant resources have returned to the state they were in prior to shutdown.</span><span class="sxs-lookup"><span data-stu-id="b9553-123">Ensure that all of your tenant resources have returned to the state they were in prior to shutdown.</span></span> <span data-ttu-id="b9553-124">Workloads running on tenant resources may need to be reconfigured after startup by the workload manager.</span><span class="sxs-lookup"><span data-stu-id="b9553-124">Workloads running on tenant resources may need to be reconfigured after startup by the workload manager.</span></span>

## <a name="get-the-startup-status-for-azure-stack"></a><span data-ttu-id="b9553-125">Get the startup status for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b9553-125">Get the startup status for Azure Stack</span></span>

<span data-ttu-id="b9553-126">Get the startup for the Azure Stack startup routine with the following steps:</span><span class="sxs-lookup"><span data-stu-id="b9553-126">Get the startup for the Azure Stack startup routine with the following steps:</span></span>

1. <span data-ttu-id="b9553-127">Open a Privileged Endpoint Session from a machine with network access to the Azure Stack ERCS VMs.</span><span class="sxs-lookup"><span data-stu-id="b9553-127">Open a Privileged Endpoint Session from a machine with network access to the Azure Stack ERCS VMs.</span></span>

2. <span data-ttu-id="b9553-128">From the PEP, run:</span><span class="sxs-lookup"><span data-stu-id="b9553-128">From the PEP, run:</span></span>

    ```powershell
      Get-ActionStatus Start-AzureStack
    ```

## <a name="troubleshoot-startup-and-shutdown-of-azure-stack"></a><span data-ttu-id="b9553-129">Troubleshoot startup and shutdown of Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b9553-129">Troubleshoot startup and shutdown of Azure Stack</span></span>

<span data-ttu-id="b9553-130">Perform the following steps if the infrastructure and tenant services don't successfully start 2 hours after you power on your Azure Stack environment.</span><span class="sxs-lookup"><span data-stu-id="b9553-130">Perform the following steps if the infrastructure and tenant services don't successfully start 2 hours after you power on your Azure Stack environment.</span></span> 

1. <span data-ttu-id="b9553-131">Open a Privileged Endpoint Session from a machine with network access to the Azure Stack ERCS VMs.</span><span class="sxs-lookup"><span data-stu-id="b9553-131">Open a Privileged Endpoint Session from a machine with network access to the Azure Stack ERCS VMs.</span></span>

2. <span data-ttu-id="b9553-132">Run:</span><span class="sxs-lookup"><span data-stu-id="b9553-132">Run:</span></span> 

    ```powershell
      Test-AzureStack
      ```

3. <span data-ttu-id="b9553-133">Review the output and resolve any health errors.</span><span class="sxs-lookup"><span data-stu-id="b9553-133">Review the output and resolve any health errors.</span></span> <span data-ttu-id="b9553-134">For more information, see [Run a validation test of Azure Stack](azure-stack-diagnostic-test.md).</span><span class="sxs-lookup"><span data-stu-id="b9553-134">For more information, see [Run a validation test of Azure Stack](azure-stack-diagnostic-test.md).</span></span>

4. <span data-ttu-id="b9553-135">Run:</span><span class="sxs-lookup"><span data-stu-id="b9553-135">Run:</span></span>

    ```powershell
      Start-AzureStack
    ```

5. <span data-ttu-id="b9553-136">If running **Start-AzureStack** results in a failure, contact Microsoft Customer Services Support.</span><span class="sxs-lookup"><span data-stu-id="b9553-136">If running **Start-AzureStack** results in a failure, contact Microsoft Customer Services Support.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b9553-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="b9553-137">Next steps</span></span> 

<span data-ttu-id="b9553-138">Learn more about Azure Stack diagnostic tool and issue logging, see [Azure Stack diagnostic tools](azure-stack-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="b9553-138">Learn more about Azure Stack diagnostic tool and issue logging, see [Azure Stack diagnostic tools](azure-stack-diagnostics.md).</span></span>
