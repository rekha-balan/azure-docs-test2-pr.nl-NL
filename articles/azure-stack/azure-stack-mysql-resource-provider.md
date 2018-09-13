---
title: Use MySQL databases as PaaS on Azure Stack | Microsoft Docs
description: Learn how you can deploy the MySQL Resource Provider and provide MySQL databases as a service on Azure Stack.
services: azure-stack
documentationCenter: ''
author: jeffgilb
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2018
ms.author: jeffgilb
ms.reviewer: jeffgo
ms.openlocfilehash: 24ba595413cde07c420a94de234d7926e0eb0e7f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871328"
---
# <a name="use-mysql-databases-on-microsoft-azure-stack"></a>Use MySQL databases on Microsoft Azure Stack

You can deploy the MySQL resource provider API to use MySQL databases deployed in Azure Stack. For more information about the resource provider API, see [Windows Azure Pack MySQL Resource Provider REST API Reference](https://msdn.microsoft.com/library/dn528442.aspx).

MySQL databases are common on websites and support many website platforms. For example, you can create WordPress websites using the Web Apps platform as a service (PaaS) add-on.

After you deploy the resource provider, you can:

* Create MySQL servers and databases using Azure Resource Manager deployment templates.
* Provide MySQL databases as a service.  

## <a name="mysql-resource-provider-adapter-architecture"></a>MySQL resource provider adapter architecture

The resource provider has the following components:

* **The MySQL resource provider adapter virtual machine (VM)**, which is a Windows Server VM that's running the provider services.
* **The resource provider**, which processes requests and accesses database resources.
* **Servers that host MySQL Server**, which provide capacity for databases that are called hosting servers. You can create MySQL instances yourself, or provide access to external MySQL instances. The [Azure Stack Quickstart Gallery](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/mysql-standalone-server-windows) has an example template that you can use to:

  * Create a MySQL server for you.
  * Download and deploy a MySQL Server from the Azure Marketplace.

> [!NOTE]
> Hosting servers that are installed on Azure Stack integrated systems must be created from a tenant subscription. They can't be created from the default provider subscription. They must be created from the tenant portal or from a PowerShell session with an appropriate sign-in. All hosting servers are billable VMs and must have licenses. The service administrator can be the owner of the tenant subscription.

### <a name="required-privileges"></a>Required privileges

The system account must have the following privileges:

* **Database:** create, drop
* **Login:** create, set, drop, grant, revoke  

## <a name="next-steps"></a>Next steps

[Deploy the MySQL resource provider](azure-stack-mysql-resource-provider-deploy.md)
