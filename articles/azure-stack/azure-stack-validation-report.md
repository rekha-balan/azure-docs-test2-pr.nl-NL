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
# <a name="azure-stack-validation-report"></a>Azure Stack validation report
Use the Azure Stack Readiness Checker tool to run validations that support deployment and servicing of an Azure Stack environment. The tool writes results to a .json report file. The report displays detailed and summarized data about the state of prerequisites for deployment of Azure Stack. The report also displays information about Secrets Rotation for existing Azure Stack Deployments.  

 ## <a name="where-to-find-the-report"></a>Where to find the report
When the tool runs, it logs results to **AzsReadinessCheckerReport.json**. The tool also creates a log named **AzsReadinessChecker.log**. The location of these files displays with the validation results in PowerShell.

![run-validation](./media/azure-stack-validation-report/validation.png)

Both files persist the results of subsequent validation checks when run on the same computer.  For example, the tool can be run to validate certificates, run again to validate Azure identity, and then a third time to validate registration. The results of all three validations are available in the resulting .json report.  

By default, both files are written to *C:\Users\<username>\AppData\Local\Temp\AzsReadinessChecker\AzsReadinessCheckerReport.json*.  
- Use the **-OutputPath** ***&lt;path&gt;*** parameter at the end of the run command line to specify a different report location.   
- Use the **-CleanReport** parameter at the end of the run command to clear information from *AzsReadinessCheckerReport.json*. about previous runs of the tool.

## <a name="view-the-report"></a>View the report
To view the report in PowerShell, supply the path to the report as a value for **-ReportPath**. This command displays the contents of the report and identifies validations that do not yet have results.

For example, to view the report from a PowerShell prompt that is open to the location where the report is located, run: 
   > `Start-AzsReadinessChecker -ReportPath .\AzsReadinessReport.json` 

The output resembles the following image:

![view-report](./media/azure-stack-validation-report/view-report.png)

## <a name="view-the-report-summary"></a>View the report summary
To view a summary of the report, you can add the **-Summary** switch to the end of the PowerShell command line. For example: 
 > `Start-AzsReadinessChecker -ReportPath .\AzsReadinessReport.json -summary`  

The summary shows validations that don't have results and indicates pass or fail for validations that are complete. The output resembles the following image:

![report-summary](./media/azure-stack-validation-report/report-summary.png)


## <a name="view-a-filtered-report"></a>View a filtered report
To view a report that is filtered on a single type of validation, use the **-ReportSections** parameter with one of the following values:
- Certificate
- AzureRegistration
- AzureIdentity
- Jobs   
- All  

For example, to view the report summary for certificates only, use the following PowerShell command line: 
 > `Start-AzsReadinessChecker -ReportPath .\AzsReadinessReport.json -ReportSections Certificate – Summary`


## <a name="see-also"></a>See also
[Start-AzsReadinessChecker cmdlet reference](azure-stack-azsreadiness-cmdlet.md)
