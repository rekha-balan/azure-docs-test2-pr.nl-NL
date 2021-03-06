---
title: Deploy templates using PowerShell in Azure Stack | Microsoft Docs
description: Deploy a template to Azure Stack using PowerShell.
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
editor: ''
ms.assetid: 12fe32d7-0a1a-4c02-835d-7b97f151ed0f
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2018
ms.author: sethm
ms.reviewer: ''
ms.openlocfilehash: 445628679a09a1884f63cdce446adec476af39af
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867868"
---
# <a name="deploy-a-template-to-azure-stack-using-powershell"></a>Deploy a template to Azure Stack using PowerShell

*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*

You can use PowerShell to deploy Azure Resource Manager templates to Azure Stack. This article shows you how to use PowerShell to deploy a template.

## <a name="run-azurerm-powershell-cmdlets"></a>Run AzureRM PowerShell cmdlets

This example uses AzureRM PowerShell cmdlets and a template stored on GitHub. The template creates a Windows Server 2012 R2 Datacenter virtual machine.

>[!NOTE]
>Before you try this example, make sure that you've [configured PowerShell](azure-stack-powershell-configure-user.md) for an Azure Stack user.

1. Go to <http://aka.ms/AzureStackGitHub> and find the **101-simple-windows-vm** template. Save the template to this location: C:\\templates\\azuredeploy-101-simple-windows-vm.json.
2. Open an elevated PowerShell command prompt.
3. Replace *username* and *password* in the following script with your username and password, and then run the script.

   ```PowerShell
       # Set Deployment Variables
       $myNum = "001" #Modify this per deployment
       $RGName = "myRG$myNum"
       $myLocation = "local"
   
       # Create Resource Group for Template Deployment
       New-AzureRmResourceGroup -Name $RGName -Location $myLocation
   
       # Deploy Simple IaaS Template
       New-AzureRmResourceGroupDeployment `
           -Name myDeployment$myNum `
           -ResourceGroupName $RGName `
           -TemplateFile c:\templates\azuredeploy-101-simple-windows-vm.json `
           -NewStorageAccountName mystorage$myNum `
           -DnsNameForPublicIP mydns$myNum `
           -AdminUsername <username> `
           -AdminPassword ("<password>" | ConvertTo-SecureString -AsPlainText -Force) `
           -VmName myVM$myNum `
           -WindowsOSVersion 2012-R2-Datacenter
   ```

   >[!IMPORTANT]
   >Everytime you run this script, increment the value of the "$myNum" parameter to prevent overwriting your deployment.

4. Open the Azure Stack portal, select **Browse**, and then select  **Virtual machines** to find your new virtual machine (*myDeployment001*).

## <a name="next-steps"></a>Next steps

[Deploy templates with Visual Studio](azure-stack-deploy-template-visual-studio.md)
