---
title: Run runbooks on Azure Automation Hybrid Runbook Worker
description: This article provides information about running runbooks on machines in your local datacenter or cloud provider with the Hybrid Runbook Worker role.
services: automation
ms.service: automation
ms.component: process-automation
author: georgewallace
ms.author: gwallace
ms.date: 07/17/2018
ms.topic: conceptual
manager: carmonm
ms.openlocfilehash: 8f21457a63470b88e93ead97454f996cea38073a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965609"
---
# <a name="running-runbooks-on-a-hybrid-runbook-worker"></a>Running runbooks on a Hybrid Runbook Worker

There is no difference in the structure of runbooks that run in Azure Automation and those that run on a Hybrid Runbook Worker. Runbooks that you use with each most likely differ significantly though since runbooks targeting a Hybrid Runbook Worker typically manage resources on the local computer itself or against resources in the local environment where it is deployed, while runbooks in Azure Automation typically manage resources in the Azure cloud.

When you author runbooks to run on a Hybrid Runbook Worker, you should edit and test the runbooks within the machine that hosts the Hybrid worker. The host machine has all of the PowerShell modules and network access you need to manage and access the local resources. Once a runbook has been edited and tested on the Hybrid worker machine, you can then upload it to the Azure Automation environment where it is available to run in the Hybrid worker. It is important to know that jobs run under the Local System account for windows or a special user account **nxautomation** on Linux, which can introduce subtle differences when authoring runbooks for a Hybrid Runbook Worker this should be taken into account.

## <a name="starting-a-runbook-on-hybrid-runbook-worker"></a>Starting a runbook on Hybrid Runbook Worker

[Starting a Runbook in Azure Automation](automation-starting-a-runbook.md) describes different methods for starting a runbook. Hybrid Runbook Worker adds a **RunOn** option where you can specify the name of a Hybrid Runbook Worker Group. If a group is specified, then the runbook is retrieved and run by one of the workers in that group. If this option is not specified, then it is run in Azure Automation as normal.

When you start a runbook in the Azure portal, you are presented with a **Run on** option where you can select **Azure** or **Hybrid Worker**. If you select **Hybrid Worker**, then you can select the group from a dropdown.

Use the **RunOn** parameter. You can use the following command to start a runbook named Test-Runbook on a Hybrid Runbook Worker Group named MyHybridGroup using Windows PowerShell.

```azurepowershell-interactive
Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -RunOn "MyHybridGroup"
```

> [!NOTE]
> The **RunOn** parameter was added to the **Start-AzureAutomationRunbook** cmdlet in version 0.9.1 of Microsoft Azure PowerShell. You should [download the latest version](https://azure.microsoft.com/downloads/) if you have an earlier one installed. You only need to install this version on a workstation where you are starting the runbook from PowerShell. You do not need to install it on the worker computer unless you intend to start runbooks from that computer"

## <a name="runbook-permissions"></a>Runbook permissions

Runbooks running on a Hybrid Runbook Worker cannot use the same method that is typically used for runbooks authenticating to Azure resources, since they are accessing resources outside of Azure. The runbook can either provide its own authentication to local resources, or you can specify a RunAs account to provide a user context for all runbooks.

### <a name="runbook-authentication"></a>Runbook authentication

By default, runbooks run in the context of the Local System account for Windows and a special user account **nxautomation** for Linux on the on-premises computer, so they must provide their own authentication to resources that they access.

You can use [Credential](automation-credentials.md) and [Certificate](automation-certificates.md) assets in your runbook with cmdlets that allow you to specify credentials so you can authenticate to different resources. The following example shows a portion of a runbook that restarts a computer. It retrieves credentials from a credential asset and the name of the computer from a variable asset and then uses these values with the Restart-Computer cmdlet.

```powershell
$Cred = Get-AutomationPSCredential -Name "MyCredential"
$Computer = Get-AutomationVariable -Name "ComputerName"

Restart-Computer -ComputerName $Computer -Credential $Cred
```

You can also leverage [InlineScript](automation-powershell-workflow.md#inlinescript), which  allows you to run blocks of code on another computer with credentials specified by the [PSCredential common parameter](/powershell/module/psworkflow/about/about_workflowcommonparameters).

### <a name="runas-account"></a>RunAs account

By default the Hybrid Runbook Worker uses Local System for Windows and a special user account **nxautomation** for Linux to execute runbooks. Instead of having runbooks provide their own authentication to local resources, you can specify a **RunAs** account for a Hybrid worker group. You specify a [credential asset](automation-credentials.md) that has access to local resources, and all runbooks run under these credentials when running on a Hybrid Runbook Worker in the group.

The user name for the credential must be in one of the following formats:

* domain\username
* username@domain
* username (for accounts local to the on-premises computer)

Use the following procedure to specify a RunAs account for a Hybrid worker group:

1. Create a [credential asset](automation-credentials.md) with access to local resources.
2. Open the Automation account in the Azure portal.
3. Select the **Hybrid Worker Groups** tile, and then select the group.
4. Select **All settings** and then **Hybrid worker group settings**.
5. Change **Run As** from **Default** to **Custom**.
6. Select the credential and click **Save**.

### <a name="automation-run-as-account"></a>Automation Run As account

As part of your automated build process for deploying resources in Azure, you may require access to on-premises systems to support a task or set of steps in your deployment sequence. To support authentication against Azure using the Run As account, you need to install the Run As account certificate.

The following PowerShell runbook, *Export-RunAsCertificateToHybridWorker*, exports the Run As certificate from your Azure Automation account and downloads and imports it into the local machine certificate store on a Hybrid worker connected to the same account. Once that step is completed, it verifies the worker can successfully authenticate to Azure using the Run As account.

```azurepowershell-interactive
<#PSScriptInfo
.VERSION 1.0
.GUID 3a796b9a-623d-499d-86c8-c249f10a6986
.AUTHOR Azure Automation Team
.COMPANYNAME Microsoft
.COPYRIGHT
.TAGS Azure Automation
.LICENSEURI
.PROJECTURI
.ICONURI
.EXTERNALMODULEDEPENDENCIES
.REQUIREDSCRIPTS
.EXTERNALSCRIPTDEPENDENCIES
.RELEASENOTES
#>

<#
.SYNOPSIS
Exports the Run As certificate from an Azure Automation account to a hybrid worker in that account.

.DESCRIPTION
This runbook exports the Run As certificate from an Azure Automation account to a hybrid worker in that account.
Run this runbook in the hybrid worker where you want the certificate installed.
This allows the use of the AzureRunAsConnection to authenticate to Azure and manage Azure resources from runbooks running in the hybrid worker.

.EXAMPLE
.\Export-RunAsCertificateToHybridWorker

.NOTES
AUTHOR: Azure Automation Team
LASTEDIT: 2016.10.13
#>

# Generate the password used for this certificate
Add-Type -AssemblyName System.Web -ErrorAction SilentlyContinue | Out-Null
$Password = [System.Web.Security.Membership]::GeneratePassword(25, 10)

# Stop on errors
$ErrorActionPreference = 'stop'

# Get the management certificate that will be used to make calls into Azure Service Management resources
$RunAsCert = Get-AutomationCertificate -Name "AzureRunAsCertificate"

# location to store temporary certificate in the Automation service host
$CertPath = Join-Path $env:temp  "AzureRunAsCertificate.pfx"

# Save the certificate
$Cert = $RunAsCert.Export("pfx",$Password)
Set-Content -Value $Cert -Path $CertPath -Force -Encoding Byte | Write-Verbose

Write-Output ("Importing certificate into $env:computername local machine root store from " + $CertPath)
$SecurePassword = ConvertTo-SecureString $Password -AsPlainText -Force
Import-PfxCertificate -FilePath $CertPath -CertStoreLocation Cert:\LocalMachine\My -Password $SecurePassword -Exportable | Write-Verbose

# Test that authentication to Azure Resource Manager is working
$RunAsConnection = Get-AutomationConnection -Name "AzureRunAsConnection"

Connect-AzureRmAccount `
    -ServicePrincipal `
    -TenantId $RunAsConnection.TenantId `
    -ApplicationId $RunAsConnection.ApplicationId `
    -CertificateThumbprint $RunAsConnection.CertificateThumbprint | Write-Verbose

Set-AzureRmContext -SubscriptionId $RunAsConnection.SubscriptionID | Write-Verbose

# List automation accounts to confirm Azure Resource Manager calls are working
Get-AzureRmAutomationAccount | Select-Object AutomationAccountName
```

> [!IMPORTANT]
> **Add-AzureRmAccount** is now an alias for **Connect-AzureRMAccount**. When searching your library items, if you do not see **Connect-AzureRMAccount**, you can use **Add-AzureRmAccount**, or you can update your modules in your Automation Account.

Save the *Export-RunAsCertificateToHybridWorker* runbook to your computer with a `.ps1` extension. Import it into your Automation account and edit the runbook, changing the value of the variable `$Password` with your own password. Publish and then run the runbook targeting the Hybrid Worker group that run and authenticate runbooks using the Run As account. The job stream reports the attempt to import the certificate into the local machine store, and follows with multiple lines depending on how many Automation accounts are defined in your subscription and if authentication is successful.

## <a name="job-behavior"></a>Job behavior

Jobs are handled slightly different on Hybrid Runbook Workers than they are when they run on Azure sandboxes. One key difference is that there is no limit on job duration on Hybrid Runbook Workers. Runbooks ran in Azure sandboxes are limited to 3 hours due to [fair share](automation-runbook-execution.md#fair-share). If you have a long-running runbook you want to ensure that it is resilient to possible restart, for example if the machine that hosts the Hybrid worker reboots. If the Hybrid worker host machine reboots, then any running runbook job restarts from the beginning, or from the last checkpoint for PowerShell Workflow runbooks. If a runbook job is restarted more than 3 times, then it is suspended.

## <a name="run-only-signed-runbooks"></a>Run only signed Runbooks

Hybrid Runbook Workers can be configured to run only signed runbooks with some configuration. The following section describes how to setup your Hybrid Runbook Workers to run signed runbooks and how to sign your runbooks.

> [!NOTE]
> Once you have configured a Hybrid Runbook Worker to run only signed runbooks, runbooks that have **not** been signed will fail to execute on the worker.

### <a name="create-signing-certificate"></a>Create Signing Certificate

The following example creates a self-signed certificate that can be used for signing runbooks. The sample creates the certificate and exports it. The certificate is imported into the Hybrid Runbook Workers later. The thumbprint is returned as well, this is used later to reference the certificate.

```powershell
# Create a self-signed certificate that can be used for code signing
$SigningCert = New-SelfSignedCertificate -CertStoreLocation cert:\LocalMachine\my `
                                        -Subject "CN=contoso.com" `
                                        -KeyAlgorithm RSA `
                                        -KeyLength 2048 `
                                        -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
                                        -KeyExportPolicy Exportable `
                                        -KeyUsage DigitalSignature `
                                        -Type CodeSigningCert


# Export the certificate so that it can be imported to the hybrid workers
Export-Certificate -Cert $SigningCert -FilePath .\hybridworkersigningcertificate.cer

# Import the certificate into the trusted root store so the certificate chain can be validated
Import-Certificate -FilePath .\hybridworkersigningcertificate.cer -CertStoreLocation Cert:\LocalMachine\Root

# Retrieve the thumbprint for later use
$SigningCert.Thumbprint
```

### <a name="configure-the-hybrid-runbook-workers"></a>Configure the Hybrid Runbook Workers

Copy the certificate created to each Hybrid Runbook Worker in a group. Run the following script to import the certificate and configure the Hybrid Worker to use signature validation on runbooks.

```powershell
# Install the certificate into a location that will be used for validation.
New-Item -Path Cert:\LocalMachine\AutomationHybridStore
Import-Certificate -FilePath .\hybridworkersigningcertificate.cer -CertStoreLocation Cert:\LocalMachine\AutomationHybridStore

# Import the certificate into the trusted root store so the certificate chain can be validated
Import-Certificate -FilePath .\hybridworkersigningcertificate.cer -CertStoreLocation Cert:\LocalMachine\Root

# Configure the hybrid worker to use signature validation on runbooks.
Set-HybridRunbookWorkerSignatureValidation -Enable $true -TrustedCertStoreLocation "Cert:\LocalMachine\AutomationHybridStore"
```

### <a name="sign-your-runbooks-using-the-certificate"></a>Sign your Runbooks using the certificate

With the Hybrid Runbook workers configured to use only signed runbooks, you must sign runbooks that are to be used on the Hybrid Runbook Worker. Use the following sample PowerShell to sign your runbooks.

```powershell
$SigningCert = ( Get-ChildItem -Path cert:\LocalMachine\My\<CertificateThumbprint>)
Set-AuthenticodeSignature .\TestRunbook.ps1 -Certificate $SigningCert
```

When the runbook has been signed, it must be imported into your Automation Account and published with the signature block. To learn how to import runbooks, see [Importing a runbook from a file into Azure Automation](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).

## <a name="troubleshoot"></a>Troubleshoot

If your runbooks are not completing successfully, review the troubleshooting guide on [runbook execution failures](troubleshoot/hybrid-runbook-worker.md#runbook-execution-fails).

## <a name="next-steps"></a>Next steps

* To learn more about the different methods that can be used to start a runbook, see [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md).
* To understand the different procedures for working with PowerShell and PowerShell Workflow runbooks in Azure Automation using the textual editor, see [Editing a Runbook in Azure Automation](automation-edit-textual-runbook.md)