---
title: Use Azure Resource Manager templates in Azure Stack | Microsoft Docs
description: Learn how to use Azure Resource Manager templates in Azure Stack to provision resources.
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
editor: ''
ms.assetid: 2022dbe5-47fd-457d-9af3-6c01688171d7
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/07/2018
ms.author: sethm
ms.reviewer: jeffgo
ms.openlocfilehash: a50f91d5cbbc0eac7080437c96144014dad651ee
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856310"
---
# <a name="use-azure-resource-manager-templates-in-azure-stack"></a>Use Azure Resource Manager templates in Azure Stack

*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*

You can use Azure Resource Manager templates to deploy and provision all the resources for your application in a single, coordinated operation. You can also redeploy templates to make changes to the resources in a resource group.

These templates can be deployed with the Microsoft Azure Stack portal, PowerShell, the command line, and Visual Studio.

The following quickstart templates are available on [GitHub](http://aka.ms/azurestackgithub):

## <a name="deploy-sharepoint-server-non-high-availability-deployment"></a>Deploy SharePoint Server (non-high-availability deployment)

Use the PowerShell DSC extension to [create a SharePoint Server 2013 farm](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/AzureStackTechnicalPreview1/sharepoint-2013-non-ha) that includes the following resources:

* A virtual network
* Three storage accounts
* Two external load balancers
* One virtual machine (VM) configured as a domain controller for a new forest with a single domain
* One VM configured as a SQL Server 2014 stand-alone server
* One VM configured as a one machine SharePoint Server 2013 farm

## <a name="deploy-ad-non-high-availability-deployment"></a>Deploy AD (non-high-availability-deployment)

Use the PowerShell DSC extension to [create an AD domain controller server](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/AzureStackTechnicalPreview1/ad-non-ha) that includes the following resources:

* A virtual network
* One storage account
* One external load balancer
* One virtual machine (VM) configured as a domain controller for a new forest with a single domain

## <a name="deploy-adsql-non-high-availability-deployment"></a>Deploy AD/SQL (non-high-availability-deployment)

Use the PowerShell DSC extension to [create a SQL Server 2014 stand-alone server](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/AzureStackTechnicalPreview1/sql-2014-non-ha) that includes the following resources:

* A virtual network
* Two storage accounts
* One external load balancer
* One virtual machine (VM) configured as a domain controller for a new forest with a single domain
* One VM configured as a SQL Server 2014 stand-alone server

## <a name="vm-dsc-extension-azure-automation-pull-server"></a>VM-DSC-Extension-Azure-Automation-Pull-Server

Use the PowerShell DSC extension to configure an existing virtual machine Local Configuration Manager (LCM) and register it to an Azure Automation Account DSC Pull Server.

## <a name="create-a-virtual-machine-from-a-user-image"></a>Create a virtual machine from a user image

[Create a virtual machine from a custom user image](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/AzureStackTechnicalPreview1/101-vm-from-user-image). This template also deploys a virtual network (with DNS), public IP address, and a network interface.

## <a name="basic-virtual-machine"></a>Basic virtual machine

[Deploy a Windows VM](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/AzureStackTechnicalPreview1/101-simple-windows-vm) that includes a virtual network (with DNS), public IP address, and a network interface.

## <a name="cancel-a-running-template-deployment"></a>Cancel a running template deployment

To cancel a running template deployment, use the [Stop-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/stop-azurermresourcegroupdeployment) PowerShell cmdlet.

## <a name="next-steps"></a>Next steps

* [Deploy templates with the portal](azure-stack-deploy-template-portal.md)
* [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md)
