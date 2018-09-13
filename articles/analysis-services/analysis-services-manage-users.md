---
title: Manage users in Azure Analysis Services | Microsoft Docs
description: Learn how to manage users on an Analysis Services server in Azure.
services: analysis-services
documentationcenter: ''
author: minewiskan
manager: erikre
editor: ''
tags: ''
ms.assetid: ''
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 04/18/2016
ms.author: owend
ms.openlocfilehash: bb307f6f38da4b4e02fe1590646fe0a5e0e2d819
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556672"
---
# <a name="manage-users-in-azure-analysis-services"></a><span data-ttu-id="e8df3-103">Manage users in Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="e8df3-103">Manage users in Azure Analysis Services</span></span>
<span data-ttu-id="e8df3-104">In Azure Analysis Services, there are two types of users, server administrators and database users.</span><span class="sxs-lookup"><span data-stu-id="e8df3-104">In Azure Analysis Services, there are two types of users, server administrators and database users.</span></span> 

## <a name="server-administrators"></a><span data-ttu-id="e8df3-105">Server administrators</span><span class="sxs-lookup"><span data-stu-id="e8df3-105">Server administrators</span></span>
<span data-ttu-id="e8df3-106">You can use **Analysis Services Admins** in the control blade for your server in Azure portal, or Server Properties in SSMS to manage server administrators.</span><span class="sxs-lookup"><span data-stu-id="e8df3-106">You can use **Analysis Services Admins** in the control blade for your server in Azure portal, or Server Properties in SSMS to manage server administrators.</span></span> <span data-ttu-id="e8df3-107">Analysis Services Admins are database server administrators with rights for common database administration tasks such as adding and removing databases and managing users.</span><span class="sxs-lookup"><span data-stu-id="e8df3-107">Analysis Services Admins are database server administrators with rights for common database administration tasks such as adding and removing databases and managing users.</span></span> <span data-ttu-id="e8df3-108">By default, the user that creates the server in Azure portal is automatically added as an Analysis Services Admin.</span><span class="sxs-lookup"><span data-stu-id="e8df3-108">By default, the user that creates the server in Azure portal is automatically added as an Analysis Services Admin.</span></span>

![Server Admins in Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/analysis-services/media/analysis-services-manage-users/aas-manage-users-admins.png)

<span data-ttu-id="e8df3-110">You should also know:</span><span class="sxs-lookup"><span data-stu-id="e8df3-110">You should also know:</span></span>

* <span data-ttu-id="e8df3-111">Windows Live ID is not a supported identity type for Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="e8df3-111">Windows Live ID is not a supported identity type for Azure Analysis Services.</span></span>  
* <span data-ttu-id="e8df3-112">Analysis Services Admins must be valid Azure Active Directory users.</span><span class="sxs-lookup"><span data-stu-id="e8df3-112">Analysis Services Admins must be valid Azure Active Directory users.</span></span>
* <span data-ttu-id="e8df3-113">If creating an Azure Analysis Services server via Azure Resource Manager templates, Analysis Services Admins takes a JSON array of users that should be added as admins.</span><span class="sxs-lookup"><span data-stu-id="e8df3-113">If creating an Azure Analysis Services server via Azure Resource Manager templates, Analysis Services Admins takes a JSON array of users that should be added as admins.</span></span>

<span data-ttu-id="e8df3-114">Analysis Services Admins can be different from Azure resource administrators, which can manage resources for Azure subscriptions.</span><span class="sxs-lookup"><span data-stu-id="e8df3-114">Analysis Services Admins can be different from Azure resource administrators, which can manage resources for Azure subscriptions.</span></span> <span data-ttu-id="e8df3-115">This maintains compatibility with existing XMLA and TMSL manage behaviors in Analysis Services and to allow you to segregate duties between Azure resource management and Analysis Services database management.</span><span class="sxs-lookup"><span data-stu-id="e8df3-115">This maintains compatibility with existing XMLA and TMSL manage behaviors in Analysis Services and to allow you to segregate duties between Azure resource management and Analysis Services database management.</span></span> <span data-ttu-id="e8df3-116">To view all roles and access types for your Azure Analysis Services resource, use Access control (IAM) on the control blade.</span><span class="sxs-lookup"><span data-stu-id="e8df3-116">To view all roles and access types for your Azure Analysis Services resource, use Access control (IAM) on the control blade.</span></span>

### <a name="to-add-administrators-using-azure-portal"></a><span data-ttu-id="e8df3-117">To add administrators using Azure portal</span><span class="sxs-lookup"><span data-stu-id="e8df3-117">To add administrators using Azure portal</span></span>
1. <span data-ttu-id="e8df3-118">In the control blade for your server, click **Analysis Services Admins**.</span><span class="sxs-lookup"><span data-stu-id="e8df3-118">In the control blade for your server, click **Analysis Services Admins**.</span></span>
2. <span data-ttu-id="e8df3-119">In the **\<servername> - Analysis Services Admins** blade, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="e8df3-119">In the **\<servername> - Analysis Services Admins** blade, click **Add**.</span></span>
3. <span data-ttu-id="e8df3-120">In the **Add Server Administrators** blade, select the users accounts to add.</span><span class="sxs-lookup"><span data-stu-id="e8df3-120">In the **Add Server Administrators** blade, select the users accounts to add.</span></span>

## <a name="database-users"></a><span data-ttu-id="e8df3-121">Database users</span><span class="sxs-lookup"><span data-stu-id="e8df3-121">Database users</span></span>
<span data-ttu-id="e8df3-122">Database users must be added to database roles.</span><span class="sxs-lookup"><span data-stu-id="e8df3-122">Database users must be added to database roles.</span></span> <span data-ttu-id="e8df3-123">Roles define users and groups that have the same permissions for a database.</span><span class="sxs-lookup"><span data-stu-id="e8df3-123">Roles define users and groups that have the same permissions for a database.</span></span> <span data-ttu-id="e8df3-124">By default, tabular model databases have a default Users role with Read permissions.</span><span class="sxs-lookup"><span data-stu-id="e8df3-124">By default, tabular model databases have a default Users role with Read permissions.</span></span> <span data-ttu-id="e8df3-125">To learn more, see [Roles in tabular models](https://msdn.microsoft.com/library/hh213165.aspx).</span><span class="sxs-lookup"><span data-stu-id="e8df3-125">To learn more, see [Roles in tabular models](https://msdn.microsoft.com/library/hh213165.aspx).</span></span>

<span data-ttu-id="e8df3-126">Azure Analysis Services model database users *must be in your Azure Active Directory*.</span><span class="sxs-lookup"><span data-stu-id="e8df3-126">Azure Analysis Services model database users *must be in your Azure Active Directory*.</span></span> <span data-ttu-id="e8df3-127">Usernames specified must be by organizational email address or UPN.</span><span class="sxs-lookup"><span data-stu-id="e8df3-127">Usernames specified must be by organizational email address or UPN.</span></span> <span data-ttu-id="e8df3-128">This is different from on-premises tabular model databases, which support users by Windows domain usernames.</span><span class="sxs-lookup"><span data-stu-id="e8df3-128">This is different from on-premises tabular model databases, which support users by Windows domain usernames.</span></span> 

<span data-ttu-id="e8df3-129">You can create database roles, add users and groups to roles, and configure row-level security in SQL Server Data Tools (SSDT) or in SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="e8df3-129">You can create database roles, add users and groups to roles, and configure row-level security in SQL Server Data Tools (SSDT) or in SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="e8df3-130">You can also add or remove users to roles by using [Analysis Services PowerShell cmdlets](https://msdn.microsoft.com/library/hh758425.aspx) or by using [Tabular Model Scripting Language](https://msdn.microsoft.com/library/mt614797.aspx) (TMSL).</span><span class="sxs-lookup"><span data-stu-id="e8df3-130">You can also add or remove users to roles by using [Analysis Services PowerShell cmdlets](https://msdn.microsoft.com/library/hh758425.aspx) or by using [Tabular Model Scripting Language](https://msdn.microsoft.com/library/mt614797.aspx) (TMSL).</span></span>

<span data-ttu-id="e8df3-131">**Sample TMSL script**</span><span class="sxs-lookup"><span data-stu-id="e8df3-131">**Sample TMSL script**</span></span>

<span data-ttu-id="e8df3-132">In this sample, a user and a group are added to the Users role for the SalesBI database.</span><span class="sxs-lookup"><span data-stu-id="e8df3-132">In this sample, a user and a group are added to the Users role for the SalesBI database.</span></span>

```
{
  "createOrReplace": {
    "object": {
      "database": "SalesBI",
      "role": "Users"
    },
    "role": {
      "name": "Users",
      "description": "All allowed users to query the model",
      "modelPermission": "read",
      "members": [
        {
          "memberName": "user1@contoso.com",
          "identityProvider": "AzureAD"
        },
        {
          "memberName": "group1@contoso.com",
          "identityProvider": "AzureAD"
        }
      ]
    }
  }
}
```

## <a name="role-based-access-control-rbac"></a><span data-ttu-id="e8df3-133">Role-Based Access Control (RBAC)</span><span class="sxs-lookup"><span data-stu-id="e8df3-133">Role-Based Access Control (RBAC)</span></span>

<span data-ttu-id="e8df3-134">Subscription administrators can use **Access control** in the control blade to configure roles.</span><span class="sxs-lookup"><span data-stu-id="e8df3-134">Subscription administrators can use **Access control** in the control blade to configure roles.</span></span> <span data-ttu-id="e8df3-135">This is not the same as server admins or database users, which as described above are configured at the server or database level.</span><span class="sxs-lookup"><span data-stu-id="e8df3-135">This is not the same as server admins or database users, which as described above are configured at the server or database level.</span></span> 

![Access control in Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/analysis-services/media/analysis-services-manage-users/aas-manage-users-rbac.png)

<span data-ttu-id="e8df3-137">Roles apply to users or accounts that need to perform tasks that can be completed in the portal or by using Azure Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="e8df3-137">Roles apply to users or accounts that need to perform tasks that can be completed in the portal or by using Azure Resource Manager templates.</span></span> <span data-ttu-id="e8df3-138">To learn more, see [Role-Based Access Control](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="e8df3-138">To learn more, see [Role-Based Access Control](../active-directory/role-based-access-control-what-is.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8df3-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="e8df3-139">Next steps</span></span>
<span data-ttu-id="e8df3-140">If you haven't already deployed a tabular model to your server, now is a good time.</span><span class="sxs-lookup"><span data-stu-id="e8df3-140">If you haven't already deployed a tabular model to your server, now is a good time.</span></span> <span data-ttu-id="e8df3-141">To learn more, see [Deploy to Azure Analysis Services](analysis-services-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="e8df3-141">To learn more, see [Deploy to Azure Analysis Services](analysis-services-deploy.md).</span></span>

<span data-ttu-id="e8df3-142">If you've deployed a model to your server, you're ready to connect to it using a client or browser.</span><span class="sxs-lookup"><span data-stu-id="e8df3-142">If you've deployed a model to your server, you're ready to connect to it using a client or browser.</span></span> <span data-ttu-id="e8df3-143">To learn more, see [Get data from Azure Analysis Services server](analysis-services-connect.md).</span><span class="sxs-lookup"><span data-stu-id="e8df3-143">To learn more, see [Get data from Azure Analysis Services server](analysis-services-connect.md).</span></span>



