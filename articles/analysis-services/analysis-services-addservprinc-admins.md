---
title: Add a service principal to Azure Analysis Services server admin role | Microsoft Docs
description: Learn how to add an automation service principal to the server admin role
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: conceptual
ms.date: 07/03/2018
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: 779a202fccd3ff56c174ebc1ebbf3c4adfdd8c7b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857021"
---
# <a name="add-a-service-principal-to-the-server-administrator-role"></a>Add a service principal to the server administrator role 

 To automate unattended PowerShell tasks, a service principal must have **server administrator** privileges on the Analysis Services server being managed. This article describes how to add a service principal to the server administrators role on an Azure AS server.

## <a name="before-you-begin"></a>Before you begin
Before completing this task, you must have a service principal registered in Azure Active Directory.

[Create service principal - Azure portal](../azure-resource-manager/resource-group-create-service-principal-portal.md)   
[Create service principal - PowerShell](../azure-resource-manager/resource-group-authenticate-service-principal.md)

## <a name="required-permissions"></a>Required permissions
To complete this task, you must have [server administrator](analysis-services-server-admins.md) permissions on the Azure AS server. 

## <a name="add-service-principal-to-server-administrators-role"></a>Add service principal to server administrators role

1. In SSMS, connect to your Azure AS server.
2. In **Server Properties** > **Security**, click **Add**.
3. In **Select a User or Group**, search for your registered app by name, select, and then click **Add**.

    ![Search for service principal account](./media/analysis-services-addservprinc-admins/aas-add-sp-ssms-picker.png)

4. Verify the service principal account ID, and then click **OK**.
    
    ![Search for service principal account](./media/analysis-services-addservprinc-admins/aas-add-sp-ssms-add.png)


> [!NOTE]
> For server operations using AzureRm cmdlets, service principal running scheduler must also belong to the **Owner** role for the resource in [Azure Role-Based Access Control (RBAC)](../role-based-access-control/overview.md). 

## <a name="related-information"></a>Related information

* [Download SQL Server PowerShell Module](https://docs.microsoft.com/sql/ssms/download-sql-server-ps-module)   
* [Download SSMS](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)   


