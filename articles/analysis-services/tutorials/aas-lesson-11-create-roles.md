---
title: 'Azure Analysis Services tutorial lesson 11: Create roles | Microsoft Docs'
description: Describes how to create roles in the Azure Analysis Services tutorial project.
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: conceptual
ms.date: 07/03/2018
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: 38c69b65d33a915d0b7cf43dc8ef5d43413163eb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870078"
---
# <a name="create-roles"></a>Create roles

In this lesson, you create roles. Roles provide model database object and data security by limiting access to only those users that are role members. Each role is defined with a single permission: None, Read, Read and Process, Process, or Administrator. Roles can be defined during model authoring by using Role Manager. After a model has been deployed, you can manage roles by using SQL Server Management Studio (SSMS). To learn more, see [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular).
  
> [!NOTE]  
> Creating roles is not necessary to complete this tutorial. By default, the account you are currently logged in with has Administrator privileges on the model. However, for other users in your organization to browse by using a reporting client, you must create at least one role with Read permissions and add those users as members.  
  
You create three roles:  
  
-   **Sales Manager** – This role can include users in your organization for which you want to have Read permission to all model objects and data.  
  
-   **Sales Analyst US** – This role can include users in your organization for which you want only to be able to browse data related to sales in the United States. For this role, you use a DAX formula to define a *Row Filter*, which restricts members to browse data only for the United States.  
  
-   **Administrator** – This role can include users for which you want to have Administrator permission, which allows unlimited access and permissions to perform administrative tasks on the model database.  
  
Because Windows user and group accounts in your organization are unique, you can add accounts from your particular organization to members. However, for this tutorial, you can also leave the members blank. You test the effect of each role later in Lesson 12: Analyze in Excel.  
  
Estimated time to complete this lesson: **15 minutes**  
  
## <a name="prerequisites"></a>Prerequisites  
This topic is part of a tabular modeling tutorial, which should be completed in order. Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 10: Create partitions](../tutorials/aas-lesson-10-create-partitions.md).  
  
## <a name="create-roles"></a>Create roles  
  
#### <a name="to-create-a-sales-manager-user-role"></a>To create a Sales Manager user role  
  
1.  In Tabular Model Explorer, right-click **Roles** > **Roles**.  
  
2.  In Role Manager, click **New**.  
  
3.  Click the new role, and then in the **Name** column, rename the role to **Sales Manager**.  
  
4.  In the **Permissions** column, click the dropdown list, and then select the **Read** permission. 

    ![aas-lesson11-new-role](../tutorials/media/aas-lesson11-new-role.png) 
  
5.  Optional: Click the **Members** tab, and then click **Add**. In the **Select Users or Groups** dialog box, enter the Windows users or groups from your organization you want to include in the role.  
  
#### <a name="to-create-a-sales-analyst-us-user-role"></a>To create a Sales Analyst US user role  
  
1.  In Role Manager, click **New**.    
  
2.  Rename the role to **Sales Analyst US**.  
  
3.  Give this role **Read** permission.  
  
4.  Click the Row Filters tab, and then for the **DimGeography** table only, in the DAX Filter column, type the following formula:  
  
    ```Administrator
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    A Row Filter formula must resolve to a Boolean (TRUE/FALSE) value. With this formula, you are specifying that only rows with the Country Region Code value of “US” are visible to the user.  
    ![aas-lesson11-role-filter](../tutorials/media/aas-lesson11-role-filter.png) 
  
6.  Optional: Click the **Members** tab, and then click **Add**. In the **Select Users or Groups** dialog box, enter the Windows users or groups from your organization you want to include in the role.  
  
#### <a name="to-create-an-administrator-user-role"></a>To create an Administrator user role  
  
1.  Click **New**.  
  
2.  Rename the role to **Administrator**.  
  
3.  Give this role **Administrator** permission.  
  
4.  Optional: Click the **Members** tab, and then click **Add**. In the **Select Users or Groups** dialog box, enter the Windows users or groups from your organization you want to include in the role. 
  
  
## <a name="whats-next"></a>What's next?
[Lesson 12: Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).

  
  
