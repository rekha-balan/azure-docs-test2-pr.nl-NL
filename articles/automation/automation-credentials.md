---
title: Credential assets in Azure Automation | Microsoft Docs
description: Credential assets in Azure Automation contain security credentials that can be used to authenticate to resources accessed by the runbook or DSC configuration. This article describes how to create credential assets and use them in a runbook or DSC configuration.
services: automation
documentationcenter: ''
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 3209bf73-c208-425e-82b6-df49860546dd
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/14/2017
ms.author: bwren
ms.openlocfilehash: 7d04853df4e30b44ab1316053543f94fa59f762d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553061"
---
# <a name="credential-assets-in-azure-automation"></a>Credential assets in Azure Automation
An Automation credential asset holds a [PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential)  object which contains security credentials such as a username and password. Runbooks and DSC configurations may use cmdlets that accept a PSCredential object for authentication, or they may extract the username and password of the PSCredential object to provide to some application or service requiring authentication. The properties for a credential are stored securely in Azure Automation and can be accessed in the runbook or DSC configuration with the [Get-AutomationPSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential.aspx) activity.

> [!NOTE]
> Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables. These assets are encrypted and stored in the Azure Automation using a unique key that is generated for each automation account. This key is encrypted by a master certificate and stored in Azure Automation. Before storing a secure asset, the key for the automation account is decrypted using the master certificate and then used to encrypt the asset.  

## <a name="windows-powershell-cmdlets"></a>Windows PowerShell cmdlets
The cmdlets in the following table are used to create and manage automation credential assets with Windows PowerShell.  They ship as part of the [Azure PowerShell module](/powershell/azureps-cmdlets-docs) which is available for use in Automation runbooks and DSC configurations.

| Cmdlets | Description |
|:--- |:--- |
| [Get-AzureAutomationCredential](http://msdn.microsoft.com/library/dn913781.aspx) |Retrieves information about a credential asset. You can only retrieve the credential itself from **Get-AutomationPSCredential** activity. |
| [New-AzureAutomationCredential](http://msdn.microsoft.com/library/azure/jj554330.aspx) |Creates a new Automation credential. |
| [Remove- AzureAutomationCredential](http://msdn.microsoft.com/library/azure/jj554330.aspx) |Removes an Automation credential. |
| [Set- AzureAutomationCredential](http://msdn.microsoft.com/library/azure/jj554330.aspx) |Sets the properties for an existing Automation credential. |

## <a name="runbook-activities"></a>Runbook activities
The activities in the following table are used to access credentials in a runbook and DSC configurations.

| Activities | Description |
|:--- |:--- |
| Get-AutomationPSCredential |Gets a credential to use in a runbook or DSC configuration. Returns a [System.Management.Automation.PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential) object. |

> [!NOTE]
> You should avoid using variables in the –Name parameter of Get-AutomationPSCredential since this can complicate discovering dependencies between runbooks or DSC configurations, and credential assets at design time.
> 
> 

## <a name="creating-a-new-credential-asset"></a>Creating a new credential asset

### <a name="to-create-a-new-credential-asset-with-the-azure-portal"></a>To create a new credential asset with the Azure portal
1. From your automation account, click the **Assets** part to open the **Assets** blade.
2. Click the **Credentials** part to open the **Credentials** blade.
3. Click **Add a credential** at the top of the blade.
4. Complete the form and click **Create** to save the new credential.

### <a name="to-create-a-new-credential-asset-with-windows-powershell"></a>To create a new credential asset with Windows PowerShell
The following sample commands show how to create a new automation credential. A PSCredential object is first created with the name and password and then used to create the credential asset. Alternatively, you could use the **Get-Credential** cmdlet to be prompted to type in a name and password.

    $user = "MyDomain\MyUser"
    $pw = ConvertTo-SecureString "PassWord!" -AsPlainText -Force
    $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $user, $pw
    New-AzureAutomationCredential -AutomationAccountName "MyAutomationAccount" -Name "MyCredential" -Value $cred

### <a name="to-create-a-new-credential-asset-with-the-azure-classic-portal"></a>To create a new credential asset with the Azure classic portal
1. From your automation account, click **Assets** at the top of the window.
2. At the bottom of the window, click **Add Setting**.
3. Click **Add Credential**.
4. In the **Credential Type** dropdown, select **PowerShell Credential**.
5. Complete the wizard and click the checkbox to save the new credential.

## <a name="using-a-powershell-credential"></a>Using a PowerShell credential
You retrieve a credential asset in a runbook or DSC configuration with the **Get-AutomationPSCredential** activity. This returns a [PSCredential object](http://msdn.microsoft.com/library/system.management.automation.pscredential.aspx) that you can use with an activity or cmdlet that requires a PSCredential parameter. You can also retrieve the properties of the credential object to use individually. The object has a property for the username and the secure password, or you can use the **GetNetworkCredential** method to return a [NetworkCredential](http://msdn.microsoft.com/library/system.net.networkcredential.aspx) object that will provide an unsecured version of the password.

### <a name="textual-runbook-sample"></a>Textual runbook sample
The following sample commands show how to use a PowerShell credential in a runbook. In this example, the credential is retrieved and its username and password assigned to variables.

    $myCredential = Get-AutomationPSCredential -Name 'MyCredential'
    $userName = $myCredential.UserName
    $securePassword = $myCredential.Password
    $password = $myCredential.GetNetworkCredential().Password


### <a name="graphical-runbook-sample"></a>Graphical runbook sample
You add a **Get-AutomationPSCredential** activity to a graphical runbook by right-clicking on the credential in the Library pane of the graphical editor and selecting **Add to canvas**.

![Add credential to canvas](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-credentials/credential-add-canvas.png)

The following image shows an example of using a credential in a graphical runbook.  In this case, it is being used to provide authentication for a runbook to Azure resources as described in [Authenticate Runbooks with Azure AD User account](automation-create-aduser-account.md).  The first activity retrieves the credential that has access to the Azure subscription.  The **Add-AzureAccount** activity then uses this credential to provide authentication for any activities that come after it.  A [pipeline link](automation-graphical-authoring-intro.md#links-and-workflow) is here since **Get-AutomationPSCredential** is expecting a single object.  

![Add credential to canvas](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-credentials/get-credential.png)

## <a name="using-a-powershell-credential-in-dsc"></a>Using a PowerShell credential in DSC
While DSC configurations in Azure Automation can reference credential assets using **Get-AutomationPSCredential**, credential assets can also be passed in via parameters, if desired. For more information, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md#credential-assets).

## <a name="next-steps"></a>Next Steps
* To learn more about links in graphical authoring, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow)
* To understand the different authentication methods with Automation, see [Azure Automation Security](automation-security-overview.md)
* To get started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)
* To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md) 



