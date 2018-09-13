---
title: Validate Azure Automation account configuration | Microsoft Docs
description: This article describes how to confirm the configuration of your Automation account is setup correctly.
services: automation
documentationcenter: ''
author: mgoedtel
manager: carmonm
editor: ''
ms.assetid: ''
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/14/2017
ms.author: magoedte
ms.openlocfilehash: a3b18e5bc24559d437a96cbd076951bbfcccec81
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671096"
---
# <a name="test-azure-automation-run-as-account-authentication"></a><span data-ttu-id="99a81-103">Test Azure Automation Run As account authentication</span><span class="sxs-lookup"><span data-stu-id="99a81-103">Test Azure Automation Run As account authentication</span></span>
<span data-ttu-id="99a81-104">After an Automation account is successfully created, you can perform a simple test to confirm you are able to successfully authenticate in Azure Resource Manager or Azure classic deployment using your newly created or updated Automation Run As account.</span><span class="sxs-lookup"><span data-stu-id="99a81-104">After an Automation account is successfully created, you can perform a simple test to confirm you are able to successfully authenticate in Azure Resource Manager or Azure classic deployment using your newly created or updated Automation Run As account.</span></span>    

## <a name="automation-run-as-authentication"></a><span data-ttu-id="99a81-105">Automation Run As authentication</span><span class="sxs-lookup"><span data-stu-id="99a81-105">Automation Run As authentication</span></span>

1. <span data-ttu-id="99a81-106">In the Azure portal, open the Automation account created earlier.</span><span class="sxs-lookup"><span data-stu-id="99a81-106">In the Azure portal, open the Automation account created earlier.</span></span>  
2. <span data-ttu-id="99a81-107">Click on the **Runbooks** tile to open the list of runbooks.</span><span class="sxs-lookup"><span data-stu-id="99a81-107">Click on the **Runbooks** tile to open the list of runbooks.</span></span>
3. <span data-ttu-id="99a81-108">Select the **AzureAutomationTutorialScript** runbook and then click **Start** to start the runbook.</span><span class="sxs-lookup"><span data-stu-id="99a81-108">Select the **AzureAutomationTutorialScript** runbook and then click **Start** to start the runbook.</span></span>  <span data-ttu-id="99a81-109">You will receive a prompt verifying you wish to start the runbook.</span><span class="sxs-lookup"><span data-stu-id="99a81-109">You will receive a prompt verifying you wish to start the runbook.</span></span>
4. <span data-ttu-id="99a81-110">A [runbook job](automation-runbook-execution.md) is created, the Job blade is displayed, and the job status displayed in the **Job Summary** tile.</span><span class="sxs-lookup"><span data-stu-id="99a81-110">A [runbook job](automation-runbook-execution.md) is created, the Job blade is displayed, and the job status displayed in the **Job Summary** tile.</span></span>  
5. <span data-ttu-id="99a81-111">The job status will start as *Queued* indicating that it is waiting for a runbook worker in the cloud to become available.</span><span class="sxs-lookup"><span data-stu-id="99a81-111">The job status will start as *Queued* indicating that it is waiting for a runbook worker in the cloud to become available.</span></span> <span data-ttu-id="99a81-112">It will then move to *Starting* when a worker claims the job, and then *Running* when the runbook actually starts running.</span><span class="sxs-lookup"><span data-stu-id="99a81-112">It will then move to *Starting* when a worker claims the job, and then *Running* when the runbook actually starts running.</span></span>  
6. <span data-ttu-id="99a81-113">When the runbook job completes, we should see a status of **Completed**.</span><span class="sxs-lookup"><span data-stu-id="99a81-113">When the runbook job completes, we should see a status of **Completed**.</span></span><br> <span data-ttu-id="99a81-114">![Security Principal Runbook Test](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-verify-runas-authentication/job-summary-automationtutorialscript.png)</span><span class="sxs-lookup"><span data-stu-id="99a81-114">![Security Principal Runbook Test](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-verify-runas-authentication/job-summary-automationtutorialscript.png)</span></span><br>
7. <span data-ttu-id="99a81-115">To see the detailed results of the runbook, click on the **Output** tile.</span><span class="sxs-lookup"><span data-stu-id="99a81-115">To see the detailed results of the runbook, click on the **Output** tile.</span></span>
8. <span data-ttu-id="99a81-116">In the **Output** blade, you should see it has successfully authenticated and returned a list of all resources available in the resource group.</span><span class="sxs-lookup"><span data-stu-id="99a81-116">In the **Output** blade, you should see it has successfully authenticated and returned a list of all resources available in the resource group.</span></span>
9. <span data-ttu-id="99a81-117">Close the **Output** blade to return to the **Job Summary** blade.</span><span class="sxs-lookup"><span data-stu-id="99a81-117">Close the **Output** blade to return to the **Job Summary** blade.</span></span>
10. <span data-ttu-id="99a81-118">Close the **Job Summary** and the corresponding **AzureAutomationTutorialScript** runbook blade.</span><span class="sxs-lookup"><span data-stu-id="99a81-118">Close the **Job Summary** and the corresponding **AzureAutomationTutorialScript** runbook blade.</span></span>

## <a name="classic-run-as-authentication"></a><span data-ttu-id="99a81-119">Classic Run As authentication</span><span class="sxs-lookup"><span data-stu-id="99a81-119">Classic Run As authentication</span></span>
<span data-ttu-id="99a81-120">Perform the following steps if you will be managing resources in the classic deployment model, to confirm you are able to successfully authenticate using the new Classic Run As account.</span><span class="sxs-lookup"><span data-stu-id="99a81-120">Perform the following steps if you will be managing resources in the classic deployment model, to confirm you are able to successfully authenticate using the new Classic Run As account.</span></span>     

1. <span data-ttu-id="99a81-121">In the Azure portal, open the Automation account created earlier.</span><span class="sxs-lookup"><span data-stu-id="99a81-121">In the Azure portal, open the Automation account created earlier.</span></span>  
2. <span data-ttu-id="99a81-122">Click on the **Runbooks** tile to open the list of runbooks.</span><span class="sxs-lookup"><span data-stu-id="99a81-122">Click on the **Runbooks** tile to open the list of runbooks.</span></span>
3. <span data-ttu-id="99a81-123">Select the **AzureClassicAutomationTutorialScript** runbook and then click **Start** to  start the runbook.</span><span class="sxs-lookup"><span data-stu-id="99a81-123">Select the **AzureClassicAutomationTutorialScript** runbook and then click **Start** to  start the runbook.</span></span>  <span data-ttu-id="99a81-124">You will receive a prompt verifying you wish to start the runbook.</span><span class="sxs-lookup"><span data-stu-id="99a81-124">You will receive a prompt verifying you wish to start the runbook.</span></span>
4. <span data-ttu-id="99a81-125">A [runbook job](automation-runbook-execution.md) is created, the Job blade is displayed, and the job status displayed in the **Job Summary** tile.</span><span class="sxs-lookup"><span data-stu-id="99a81-125">A [runbook job](automation-runbook-execution.md) is created, the Job blade is displayed, and the job status displayed in the **Job Summary** tile.</span></span>  
5. <span data-ttu-id="99a81-126">The job status will start as *Queued* indicating that it is waiting for a runbook worker in the cloud to become available.</span><span class="sxs-lookup"><span data-stu-id="99a81-126">The job status will start as *Queued* indicating that it is waiting for a runbook worker in the cloud to become available.</span></span> <span data-ttu-id="99a81-127">It will then move to *Starting* when a worker claims the job, and then *Running* when the runbook actually starts running.</span><span class="sxs-lookup"><span data-stu-id="99a81-127">It will then move to *Starting* when a worker claims the job, and then *Running* when the runbook actually starts running.</span></span>  
6. <span data-ttu-id="99a81-128">When the runbook job completes, we should see a status of **Completed**.</span><span class="sxs-lookup"><span data-stu-id="99a81-128">When the runbook job completes, we should see a status of **Completed**.</span></span><br><br> <span data-ttu-id="99a81-129">![Security Principal Runbook Test](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-verify-runas-authentication/job-summary-automationclassictutorialscript.png)</span><span class="sxs-lookup"><span data-stu-id="99a81-129">![Security Principal Runbook Test](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-verify-runas-authentication/job-summary-automationclassictutorialscript.png)</span></span><br>  
7. <span data-ttu-id="99a81-130">To see the detailed results of the runbook, click on the **Output** tile.</span><span class="sxs-lookup"><span data-stu-id="99a81-130">To see the detailed results of the runbook, click on the **Output** tile.</span></span>
8. <span data-ttu-id="99a81-131">In the **Output** blade, you should see it has successfully authenticated and returned a list of all classic VM’s in the subscription.</span><span class="sxs-lookup"><span data-stu-id="99a81-131">In the **Output** blade, you should see it has successfully authenticated and returned a list of all classic VM’s in the subscription.</span></span>
9. <span data-ttu-id="99a81-132">Close the **Output** blade to return to the **Job Summary** blade.</span><span class="sxs-lookup"><span data-stu-id="99a81-132">Close the **Output** blade to return to the **Job Summary** blade.</span></span>
10. <span data-ttu-id="99a81-133">Close the **Job Summary** and the corresponding **AzureClassicAutomationTutorialScript** runbook blade.</span><span class="sxs-lookup"><span data-stu-id="99a81-133">Close the **Job Summary** and the corresponding **AzureClassicAutomationTutorialScript** runbook blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="99a81-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="99a81-134">Next steps</span></span>
* <span data-ttu-id="99a81-135">To get started with PowerShell runbooks, see [My first PowerShell runbook](automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="99a81-135">To get started with PowerShell runbooks, see [My first PowerShell runbook](automation-first-runbook-textual-powershell.md).</span></span>
* <span data-ttu-id="99a81-136">To learn more about Graphical Authoring, see [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="99a81-136">To learn more about Graphical Authoring, see [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>


