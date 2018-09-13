---
title: Security Considerations for SQL Server in Azure | Microsoft Docs
description: This topic refers to resources created with the classic deployment model, and provides general guidance for securing SQL Server running in an Azure Virtual Machine.
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: ''
tags: azure-service-management
ms.assetid: d710c296-e490-43e7-8ca9-8932586b71da
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 11/15/2016
ms.author: jroth
ms.openlocfilehash: 9fc96d70592bd55685ebbf1b80f6017b74f58925
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540775"
---
# <a name="security-considerations-for-sql-server-in-azure-virtual-machines"></a>Security Considerations for SQL Server in Azure Virtual Machines
This topic includes overall security guidelines that help establish secure access to SQL Server instances in an Azure VM. However, in order to ensure better protection to your SQL Server database instances in Azure, we recommend that you implement the traditional on-premises security practices in addition to the security best practices for Azure.

> [!IMPORTANT] 
> Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md). This article covers using the Classic deployment model. Microsoft recommends that most new deployments use the Resource Manager model.

For more information about the SQL Server security practices, see [SQL Server 2008 R2 Security Best Practices - Operational and Administrative Tasks](http://download.microsoft.com/download/1/2/A/12ABE102-4427-4335-B989-5DA579A4D29D/SQL_Server_2008_R2_Security_Best_Practice_Whitepaper.docx)

Azure complies with several industry regulations and standards that can enable you to build a compliant solution with SQL Server running in a Virtual Machine. For information about regulatory compliance with Azure, see [Azure Trust Center](https://azure.microsoft.com/support/trust-center/).

Following is a list of security recommendations to consider when configuring and connecting to the instance of SQL Server in an Azure VM.

## <a name="considerations-for-managing-accounts"></a>Considerations for managing accounts:
* Create a unique local administrator account that is not named **Administrator**.
* Use complex strong passwords for all your accounts. For more information about how to create a strong password, see [Tips for creating a strong passwords](http://windows.microsoft.com/en-us/windows-vista/Tips-for-creating-a-strong-password) article .
* By default, Azure selects Windows Authentication during SQL Server Virtual Machine setup. Therefore, the **SA** login is disabled and a password is assigned by setup. We recommend that the **SA** login should be not be used or enabled. The following are alternative strategies if a SQL Login is desired:
  
  * Create a SQL account that has sysadmin membership.
  * If you must use a **SA** login, enable the login and rename it and assign a new password.
  * Both the options that were mentioned earlier require a change the authentication mode to **SQL Server and Windows Authentication Mode**. For more information, see [Change Server Authentication Mode](https://msdn.microsoft.com/library/ms188670.aspx).

## <a name="considerations-for-securing-connections-to-azure-virtual-machine"></a>Considerations for Securing Connections to Azure Virtual Machine:
* Consider using [Azure Virtual Network](../../../virtual-network/virtual-networks-overview.md) to administer the virtual machines instead of public RDP ports.
* Use a [Network Security Group](../../../virtual-network/virtual-networks-nsg.md) (NSG) to allow or deny network traffic to your virtual machine. If you want to use an NSG and have an endpoint ACL already in place, first remove the endpoint ACL. For information about how to do this, see [Managing Access Control Lists (ACLs) for Endpoints by using PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).
* If you are using endpoints, remove any endpoints on the virtual machine if you do not use them. For instructions on using ACLs with endpoints, see [Manage the ACL on an endpoint](../classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).
* Enable an encrypted connection option for an instance of the SQL Server Database Engine in Azure Virtual Machines. Configure SQL server instance with a signed certificate. For more information, see [Enable Encrypted Connections to the Database Engine](https://msdn.microsoft.com/library/ms191192.aspx) and [Connection String Syntax](https://msdn.microsoft.com/library/ms254500.aspx).
* If your virtual machines should be accessed only from a specific network, use Windows Firewall to restrict access to certain IP addresses or network subnets.

## <a name="next-steps"></a>Next Steps
If you are also interested in best practices around performance, see [Performance Best Practices for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md).

For other topics related to running SQL Server in Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).

