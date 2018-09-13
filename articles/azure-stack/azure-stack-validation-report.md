---
title: Validation report for Azure Stack | Microsoft Docs
description: Use the Azure Stack Readiness Checker report to review validation results.
services: azure-stack
documentationcenter: ''
author: brenduns
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/08/2018
ms.author: brenduns
ms.reviewer: ''
ms.openlocfilehash: 06b5660a9428e98d2e99b5d447a05700968ec884
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857318"
---
# <a name="azure-stack-validation-report"></a><span data-ttu-id="07085-103">Azure Stack validation report</span><span class="sxs-lookup"><span data-stu-id="07085-103">Azure Stack validation report</span></span>
<span data-ttu-id="07085-104">Use the Azure Stack Readiness Checker tool to run validations that support deployment and servicing of an Azure Stack environment.</span><span class="sxs-lookup"><span data-stu-id="07085-104">Use the Azure Stack Readiness Checker tool to run validations that support deployment and servicing of an Azure Stack environment.</span></span> <span data-ttu-id="07085-105">The tool writes results to a .json report file.</span><span class="sxs-lookup"><span data-stu-id="07085-105">The tool writes results to a .json report file.</span></span> <span data-ttu-id="07085-106">The report displays detailed and summarized data about the state of prerequisites for deployment of Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="07085-106">The report displays detailed and summarized data about the state of prerequisites for deployment of Azure Stack.</span></span> <span data-ttu-id="07085-107">The report also displays information about Secrets Rotation for existing Azure Stack Deployments.</span><span class="sxs-lookup"><span data-stu-id="07085-107">The report also displays information about Secrets Rotation for existing Azure Stack Deployments.</span></span>  

 ## <a name="where-to-find-the-report"></a><span data-ttu-id="07085-108">Where to find the report</span><span class="sxs-lookup"><span data-stu-id="07085-108">Where to find the report</span></span>
<span data-ttu-id="07085-109">When the tool runs, it logs results to **AzsReadinessCheckerReport.json**.</span><span class="sxs-lookup"><span data-stu-id="07085-109">When the tool runs, it logs results to **AzsReadinessCheckerReport.json**.</span></span> <span data-ttu-id="07085-110">The tool also creates a log named **AzsReadinessChecker.log**.</span><span class="sxs-lookup"><span data-stu-id="07085-110">The tool also creates a log named **AzsReadinessChecker.log**.</span></span> <span data-ttu-id="07085-111">The location of these files displays with the validation results in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="07085-111">The location of these files displays with the validation results in PowerShell.</span></span>

![run-validation](./media/azure-stack-validation-report/validation.png)

<span data-ttu-id="07085-113">Both files persist the results of subsequent validation checks when run on the same computer.</span><span class="sxs-lookup"><span data-stu-id="07085-113">Both files persist the results of subsequent validation checks when run on the same computer.</span></span>  <span data-ttu-id="07085-114">For example, the tool can be run to validate certificates, run again to validate Azure identity, and then a third time to validate registration.</span><span class="sxs-lookup"><span data-stu-id="07085-114">For example, the tool can be run to validate certificates, run again to validate Azure identity, and then a third time to validate registration.</span></span> <span data-ttu-id="07085-115">The results of all three validations are available in the resulting .json report.</span><span class="sxs-lookup"><span data-stu-id="07085-115">The results of all three validations are available in the resulting .json report.</span></span>  

<span data-ttu-id="07085-116">By default, both files are written to *C:\Users\<username>\AppData\Local\Temp\AzsReadinessChecker\AzsReadinessCheckerReport.json*.</span><span class="sxs-lookup"><span data-stu-id="07085-116">By default, both files are written to *C:\Users\<username>\AppData\Local\Temp\AzsReadinessChecker\AzsReadinessCheckerReport.json*.</span></span>  
- <span data-ttu-id="07085-117">Use the **-OutputPath** ***&lt;path&gt;*** parameter at the end of the run command line to specify a different report location.</span><span class="sxs-lookup"><span data-stu-id="07085-117">Use the **-OutputPath** ***&lt;path&gt;*** parameter at the end of the run command line to specify a different report location.</span></span>   
- <span data-ttu-id="07085-118">Use the **-CleanReport** parameter at the end of the run command to clear information from *AzsReadinessCheckerReport.json*.</span><span class="sxs-lookup"><span data-stu-id="07085-118">Use the **-CleanReport** parameter at the end of the run command to clear information from *AzsReadinessCheckerReport.json*.</span></span> <span data-ttu-id="07085-119">about previous runs of the tool.</span><span class="sxs-lookup"><span data-stu-id="07085-119">about previous runs of the tool.</span></span>

## <a name="view-the-report"></a><span data-ttu-id="07085-120">View the report</span><span class="sxs-lookup"><span data-stu-id="07085-120">View the report</span></span>
<span data-ttu-id="07085-121">To view the report in PowerShell, supply the path to the report as a value for **-ReportPath**.</span><span class="sxs-lookup"><span data-stu-id="07085-121">To view the report in PowerShell, supply the path to the report as a value for **-ReportPath**.</span></span> <span data-ttu-id="07085-122">This command displays the contents of the report and identifies validations that do not yet have results.</span><span class="sxs-lookup"><span data-stu-id="07085-122">This command displays the contents of the report and identifies validations that do not yet have results.</span></span>

<span data-ttu-id="07085-123">For example, to view the report from a PowerShell prompt that is open to the location where the report is located, run:</span><span class="sxs-lookup"><span data-stu-id="07085-123">For example, to view the report from a PowerShell prompt that is open to the location where the report is located, run:</span></span> 
   > `Start-AzsReadinessChecker -ReportPath .\AzsReadinessReport.json` 

<span data-ttu-id="07085-124">The output resembles the following image:</span><span class="sxs-lookup"><span data-stu-id="07085-124">The output resembles the following image:</span></span>

![view-report](./media/azure-stack-validation-report/view-report.png)

## <a name="view-the-report-summary"></a><span data-ttu-id="07085-126">View the report summary</span><span class="sxs-lookup"><span data-stu-id="07085-126">View the report summary</span></span>
<span data-ttu-id="07085-127">To view a summary of the report, you can add the **-Summary** switch to the end of the PowerShell command line.</span><span class="sxs-lookup"><span data-stu-id="07085-127">To view a summary of the report, you can add the **-Summary** switch to the end of the PowerShell command line.</span></span> <span data-ttu-id="07085-128">For example:</span><span class="sxs-lookup"><span data-stu-id="07085-128">For example:</span></span> 
 > `Start-AzsReadinessChecker -ReportPath .\AzsReadinessReport.json -summary`  

<span data-ttu-id="07085-129">The summary shows validations that don't have results and indicates pass or fail for validations that are complete.</span><span class="sxs-lookup"><span data-stu-id="07085-129">The summary shows validations that don't have results and indicates pass or fail for validations that are complete.</span></span> <span data-ttu-id="07085-130">The output resembles the following image:</span><span class="sxs-lookup"><span data-stu-id="07085-130">The output resembles the following image:</span></span>

![report-summary](./media/azure-stack-validation-report/report-summary.png)


## <a name="view-a-filtered-report"></a><span data-ttu-id="07085-132">View a filtered report</span><span class="sxs-lookup"><span data-stu-id="07085-132">View a filtered report</span></span>
<span data-ttu-id="07085-133">To view a report that is filtered on a single type of validation, use the **-ReportSections** parameter with one of the following values:</span><span class="sxs-lookup"><span data-stu-id="07085-133">To view a report that is filtered on a single type of validation, use the **-ReportSections** parameter with one of the following values:</span></span>
- <span data-ttu-id="07085-134">Certificate</span><span class="sxs-lookup"><span data-stu-id="07085-134">Certificate</span></span>
- <span data-ttu-id="07085-135">AzureRegistration</span><span class="sxs-lookup"><span data-stu-id="07085-135">AzureRegistration</span></span>
- <span data-ttu-id="07085-136">AzureIdentity</span><span class="sxs-lookup"><span data-stu-id="07085-136">AzureIdentity</span></span>
- <span data-ttu-id="07085-137">Jobs</span><span class="sxs-lookup"><span data-stu-id="07085-137">Jobs</span></span>   
- <span data-ttu-id="07085-138">All</span><span class="sxs-lookup"><span data-stu-id="07085-138">All</span></span>  

<span data-ttu-id="07085-139">For example, to view the report summary for certificates only, use the following PowerShell command line:</span><span class="sxs-lookup"><span data-stu-id="07085-139">For example, to view the report summary for certificates only, use the following PowerShell command line:</span></span> 
 > `Start-AzsReadinessChecker -ReportPath .\AzsReadinessReport.json -ReportSections Certificate – Summary`


## <a name="see-also"></a><span data-ttu-id="07085-140">See also</span><span class="sxs-lookup"><span data-stu-id="07085-140">See also</span></span>
[<span data-ttu-id="07085-141">Start-AzsReadinessChecker cmdlet reference</span><span class="sxs-lookup"><span data-stu-id="07085-141">Start-AzsReadinessChecker cmdlet reference</span></span>](azure-stack-azsreadiness-cmdlet.md)
