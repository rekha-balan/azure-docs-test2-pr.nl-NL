---
title: Manage database roles and users in Azure Analysis Services | Microsoft Docs
description: Learn how to manage database roles and users on an Analysis Services server in Azure.
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: conceptual
ms.date: 07/03/2018
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: 8c777d5376614f7afe59342dc5a9fbfa37ca4556
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857787"
---
# <a name="manage-database-roles-and-users"></a><span data-ttu-id="258e1-103">Manage database roles and users</span><span class="sxs-lookup"><span data-stu-id="258e1-103">Manage database roles and users</span></span>

<span data-ttu-id="258e1-104">At the model database level, all users must belong to a role.</span><span class="sxs-lookup"><span data-stu-id="258e1-104">At the model database level, all users must belong to a role.</span></span> <span data-ttu-id="258e1-105">Roles define users with particular permissions for the model database.</span><span class="sxs-lookup"><span data-stu-id="258e1-105">Roles define users with particular permissions for the model database.</span></span> <span data-ttu-id="258e1-106">Any user or security group added to a role must have an account in an Azure AD tenant in the same subscription as the server.</span><span class="sxs-lookup"><span data-stu-id="258e1-106">Any user or security group added to a role must have an account in an Azure AD tenant in the same subscription as the server.</span></span> 

<span data-ttu-id="258e1-107">How you define roles is different depending on the tool you use, but the effect is the same.</span><span class="sxs-lookup"><span data-stu-id="258e1-107">How you define roles is different depending on the tool you use, but the effect is the same.</span></span>

<span data-ttu-id="258e1-108">Role permissions include:</span><span class="sxs-lookup"><span data-stu-id="258e1-108">Role permissions include:</span></span>
*  <span data-ttu-id="258e1-109">**Administrator** - Users have full permissions for the database.</span><span class="sxs-lookup"><span data-stu-id="258e1-109">**Administrator** - Users have full permissions for the database.</span></span> <span data-ttu-id="258e1-110">Database roles with Administrator permissions are different from server administrators.</span><span class="sxs-lookup"><span data-stu-id="258e1-110">Database roles with Administrator permissions are different from server administrators.</span></span>
*  <span data-ttu-id="258e1-111">**Process** - Users can connect to and perform process operations on the database, and analyze model database data.</span><span class="sxs-lookup"><span data-stu-id="258e1-111">**Process** - Users can connect to and perform process operations on the database, and analyze model database data.</span></span>
*  <span data-ttu-id="258e1-112">**Read** -  Users can use a client application to connect to and analyze model database data.</span><span class="sxs-lookup"><span data-stu-id="258e1-112">**Read** -  Users can use a client application to connect to and analyze model database data.</span></span>

<span data-ttu-id="258e1-113">When creating a tabular model project, you create roles and add users or groups to those roles by using Role Manager in SSDT.</span><span class="sxs-lookup"><span data-stu-id="258e1-113">When creating a tabular model project, you create roles and add users or groups to those roles by using Role Manager in SSDT.</span></span> <span data-ttu-id="258e1-114">When deployed to a server, you use SSMS, [Analysis Services PowerShell cmdlets](https://msdn.microsoft.com/library/hh758425.aspx), or [Tabular Model Scripting Language](https://msdn.microsoft.com/library/mt614797.aspx) (TMSL) to add or remove roles and user members.</span><span class="sxs-lookup"><span data-stu-id="258e1-114">When deployed to a server, you use SSMS, [Analysis Services PowerShell cmdlets](https://msdn.microsoft.com/library/hh758425.aspx), or [Tabular Model Scripting Language](https://msdn.microsoft.com/library/mt614797.aspx) (TMSL) to add or remove roles and user members.</span></span>

> [!NOTE]
> <span data-ttu-id="258e1-115">Security groups must have the `MailEnabled` property set to `True`.</span><span class="sxs-lookup"><span data-stu-id="258e1-115">Security groups must have the `MailEnabled` property set to `True`.</span></span>

## <a name="to-add-or-manage-roles-and-users-in-ssdt"></a><span data-ttu-id="258e1-116">To add or manage roles and users in SSDT</span><span class="sxs-lookup"><span data-stu-id="258e1-116">To add or manage roles and users in SSDT</span></span>  
  
1.  <span data-ttu-id="258e1-117">In SSDT > **Tabular Model Explorer**, right-click **Roles**.</span><span class="sxs-lookup"><span data-stu-id="258e1-117">In SSDT > **Tabular Model Explorer**, right-click **Roles**.</span></span>  
  
2.  <span data-ttu-id="258e1-118">In **Role Manager**, click **New**.</span><span class="sxs-lookup"><span data-stu-id="258e1-118">In **Role Manager**, click **New**.</span></span>  
  
3.  <span data-ttu-id="258e1-119">Type a name for the role.</span><span class="sxs-lookup"><span data-stu-id="258e1-119">Type a name for the role.</span></span>  
  
     <span data-ttu-id="258e1-120">By default, the name of the default role is incrementally numbered for each new role.</span><span class="sxs-lookup"><span data-stu-id="258e1-120">By default, the name of the default role is incrementally numbered for each new role.</span></span> <span data-ttu-id="258e1-121">It's recommended you type a name that clearly identifies the member type, for example, Finance Managers or Human Resources Specialists.</span><span class="sxs-lookup"><span data-stu-id="258e1-121">It's recommended you type a name that clearly identifies the member type, for example, Finance Managers or Human Resources Specialists.</span></span>  
  
4.  <span data-ttu-id="258e1-122">Select one of the following permissions:</span><span class="sxs-lookup"><span data-stu-id="258e1-122">Select one of the following permissions:</span></span>  
  
    |<span data-ttu-id="258e1-123">Permission</span><span class="sxs-lookup"><span data-stu-id="258e1-123">Permission</span></span>|<span data-ttu-id="258e1-124">Description</span><span class="sxs-lookup"><span data-stu-id="258e1-124">Description</span></span>|  
    |----------------|-----------------|  
    |<span data-ttu-id="258e1-125">**None**</span><span class="sxs-lookup"><span data-stu-id="258e1-125">**None**</span></span>|<span data-ttu-id="258e1-126">Members cannot modify the model schema and cannot query data.</span><span class="sxs-lookup"><span data-stu-id="258e1-126">Members cannot modify the model schema and cannot query data.</span></span>|  
    |<span data-ttu-id="258e1-127">**Read**</span><span class="sxs-lookup"><span data-stu-id="258e1-127">**Read**</span></span>|<span data-ttu-id="258e1-128">Members can query data (based on row filters) but cannot modify the model schema.</span><span class="sxs-lookup"><span data-stu-id="258e1-128">Members can query data (based on row filters) but cannot modify the model schema.</span></span>|  
    |<span data-ttu-id="258e1-129">**Read and Process**</span><span class="sxs-lookup"><span data-stu-id="258e1-129">**Read and Process**</span></span>|<span data-ttu-id="258e1-130">Members can query data (based on row-level filters) and run Process and Process All operations, but cannot modify the model schema.</span><span class="sxs-lookup"><span data-stu-id="258e1-130">Members can query data (based on row-level filters) and run Process and Process All operations, but cannot modify the model schema.</span></span>|  
    |<span data-ttu-id="258e1-131">**Process**</span><span class="sxs-lookup"><span data-stu-id="258e1-131">**Process**</span></span>|<span data-ttu-id="258e1-132">Members can run Process and Process All operations.</span><span class="sxs-lookup"><span data-stu-id="258e1-132">Members can run Process and Process All operations.</span></span> <span data-ttu-id="258e1-133">Cannot modify the model schema and cannot query data.</span><span class="sxs-lookup"><span data-stu-id="258e1-133">Cannot modify the model schema and cannot query data.</span></span>|  
    |<span data-ttu-id="258e1-134">**Administrator**</span><span class="sxs-lookup"><span data-stu-id="258e1-134">**Administrator**</span></span>|<span data-ttu-id="258e1-135">Members can modify the model schema and query all data.</span><span class="sxs-lookup"><span data-stu-id="258e1-135">Members can modify the model schema and query all data.</span></span>|   
  
5.  <span data-ttu-id="258e1-136">If the role you are creating has Read or Read and Process permission, you can add row filters by using a DAX formula.</span><span class="sxs-lookup"><span data-stu-id="258e1-136">If the role you are creating has Read or Read and Process permission, you can add row filters by using a DAX formula.</span></span> <span data-ttu-id="258e1-137">Click the **Row Filters** tab, then select a table, then click the **DAX Filter** field, and then type a DAX formula.</span><span class="sxs-lookup"><span data-stu-id="258e1-137">Click the **Row Filters** tab, then select a table, then click the **DAX Filter** field, and then type a DAX formula.</span></span>
  
6.  <span data-ttu-id="258e1-138">Click **Members** > **Add External**.</span><span class="sxs-lookup"><span data-stu-id="258e1-138">Click **Members** > **Add External**.</span></span>  
  
8.  <span data-ttu-id="258e1-139">In **Add External Member**, enter users or groups in your tenant Azure AD by email address.</span><span class="sxs-lookup"><span data-stu-id="258e1-139">In **Add External Member**, enter users or groups in your tenant Azure AD by email address.</span></span> <span data-ttu-id="258e1-140">After you click OK and close Role Manager, roles and role members appear in Tabular Model Explorer.</span><span class="sxs-lookup"><span data-stu-id="258e1-140">After you click OK and close Role Manager, roles and role members appear in Tabular Model Explorer.</span></span> 
 
     ![Roles and users in Tabular Model Explorer](./media/analysis-services-database-users/aas-roles-tmexplorer.png)

9. <span data-ttu-id="258e1-142">Deploy to your Azure Analysis Services server.</span><span class="sxs-lookup"><span data-stu-id="258e1-142">Deploy to your Azure Analysis Services server.</span></span>


## <a name="to-add-or-manage-roles-and-users-in-ssms"></a><span data-ttu-id="258e1-143">To add or manage roles and users in SSMS</span><span class="sxs-lookup"><span data-stu-id="258e1-143">To add or manage roles and users in SSMS</span></span>
<span data-ttu-id="258e1-144">To add roles and users to a deployed model database, you must be connected to the server as a Server administrator or already in a database role with administrator permissions.</span><span class="sxs-lookup"><span data-stu-id="258e1-144">To add roles and users to a deployed model database, you must be connected to the server as a Server administrator or already in a database role with administrator permissions.</span></span>

1. <span data-ttu-id="258e1-145">In Object Exporer, right-click **Roles** > **New Role**.</span><span class="sxs-lookup"><span data-stu-id="258e1-145">In Object Exporer, right-click **Roles** > **New Role**.</span></span>

2. <span data-ttu-id="258e1-146">In **Create Role**, enter a role name and description.</span><span class="sxs-lookup"><span data-stu-id="258e1-146">In **Create Role**, enter a role name and description.</span></span>

3. <span data-ttu-id="258e1-147">Select a permission.</span><span class="sxs-lookup"><span data-stu-id="258e1-147">Select a permission.</span></span>
   |<span data-ttu-id="258e1-148">Permission</span><span class="sxs-lookup"><span data-stu-id="258e1-148">Permission</span></span>|<span data-ttu-id="258e1-149">Description</span><span class="sxs-lookup"><span data-stu-id="258e1-149">Description</span></span>|  
   |----------------|-----------------|  
   |<span data-ttu-id="258e1-150">**Full control (Administrator)**</span><span class="sxs-lookup"><span data-stu-id="258e1-150">**Full control (Administrator)**</span></span>|<span data-ttu-id="258e1-151">Members can modify the model schema, process, and can query all data.</span><span class="sxs-lookup"><span data-stu-id="258e1-151">Members can modify the model schema, process, and can query all data.</span></span>| 
   |<span data-ttu-id="258e1-152">**Process database**</span><span class="sxs-lookup"><span data-stu-id="258e1-152">**Process database**</span></span>|<span data-ttu-id="258e1-153">Members can run Process and Process All operations.</span><span class="sxs-lookup"><span data-stu-id="258e1-153">Members can run Process and Process All operations.</span></span> <span data-ttu-id="258e1-154">Cannot modify the model schema and cannot query data.</span><span class="sxs-lookup"><span data-stu-id="258e1-154">Cannot modify the model schema and cannot query data.</span></span>|  
   |<span data-ttu-id="258e1-155">**Read**</span><span class="sxs-lookup"><span data-stu-id="258e1-155">**Read**</span></span>|<span data-ttu-id="258e1-156">Members can query data (based on row filters) but cannot modify the model schema.</span><span class="sxs-lookup"><span data-stu-id="258e1-156">Members can query data (based on row filters) but cannot modify the model schema.</span></span>|  
  
4. <span data-ttu-id="258e1-157">Click **Membership**, then enter a user or group in your tenant Azure AD by email address.</span><span class="sxs-lookup"><span data-stu-id="258e1-157">Click **Membership**, then enter a user or group in your tenant Azure AD by email address.</span></span>

     ![Add user](./media/analysis-services-database-users/aas-roles-adduser-ssms.png)

5. <span data-ttu-id="258e1-159">If the role you are creating has Read permission, you can add row filters by using a DAX formula.</span><span class="sxs-lookup"><span data-stu-id="258e1-159">If the role you are creating has Read permission, you can add row filters by using a DAX formula.</span></span> <span data-ttu-id="258e1-160">Click **Row Filters**, select a table, and then type a DAX formula in the **DAX Filter** field.</span><span class="sxs-lookup"><span data-stu-id="258e1-160">Click **Row Filters**, select a table, and then type a DAX formula in the **DAX Filter** field.</span></span> 

## <a name="to-add-roles-and-users-by-using-a-tmsl-script"></a><span data-ttu-id="258e1-161">To add roles and users by using a TMSL script</span><span class="sxs-lookup"><span data-stu-id="258e1-161">To add roles and users by using a TMSL script</span></span>
<span data-ttu-id="258e1-162">You can run a TMSL script in the XMLA window in SSMS or by using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="258e1-162">You can run a TMSL script in the XMLA window in SSMS or by using PowerShell.</span></span> <span data-ttu-id="258e1-163">Use the [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) command and the [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl) object.</span><span class="sxs-lookup"><span data-stu-id="258e1-163">Use the [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) command and the [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl) object.</span></span>

<span data-ttu-id="258e1-164">**Sample TMSL script**</span><span class="sxs-lookup"><span data-stu-id="258e1-164">**Sample TMSL script**</span></span>

<span data-ttu-id="258e1-165">In this sample, a B2B external user and a group are added to the Analyst role with Read permissions for the SalesBI database.</span><span class="sxs-lookup"><span data-stu-id="258e1-165">In this sample, a B2B external user and a group are added to the Analyst role with Read permissions for the SalesBI database.</span></span> <span data-ttu-id="258e1-166">Both the external user and group must be in same tenant Azure AD.</span><span class="sxs-lookup"><span data-stu-id="258e1-166">Both the external user and group must be in same tenant Azure AD.</span></span>

```
{
  "createOrReplace": {
    "object": {
      "database": "SalesBI",
      "role": "Analyst"
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
          "memberName": "group1@adventureworks.com",
          "identityProvider": "AzureAD"
        }
      ]
    }
  }
}
```

## <a name="to-add-roles-and-users-by-using-powershell"></a><span data-ttu-id="258e1-167">To add roles and users by using PowerShell</span><span class="sxs-lookup"><span data-stu-id="258e1-167">To add roles and users by using PowerShell</span></span>
<span data-ttu-id="258e1-168">The [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) module provides task-specific database management cmdlets and the general-purpose Invoke-ASCmd cmdlet that accepts a Tabular Model Scripting Language (TMSL) query or script.</span><span class="sxs-lookup"><span data-stu-id="258e1-168">The [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) module provides task-specific database management cmdlets and the general-purpose Invoke-ASCmd cmdlet that accepts a Tabular Model Scripting Language (TMSL) query or script.</span></span> <span data-ttu-id="258e1-169">The following cmdlets are used for managing database roles and users.</span><span class="sxs-lookup"><span data-stu-id="258e1-169">The following cmdlets are used for managing database roles and users.</span></span>
  
|<span data-ttu-id="258e1-170">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="258e1-170">Cmdlet</span></span>|<span data-ttu-id="258e1-171">Description</span><span class="sxs-lookup"><span data-stu-id="258e1-171">Description</span></span>|
|------------|-----------------| 
|[<span data-ttu-id="258e1-172">Add-RoleMember</span><span class="sxs-lookup"><span data-stu-id="258e1-172">Add-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510167.aspx)|<span data-ttu-id="258e1-173">Add a member to a database role.</span><span class="sxs-lookup"><span data-stu-id="258e1-173">Add a member to a database role.</span></span>| 
|[<span data-ttu-id="258e1-174">Remove-RoleMember</span><span class="sxs-lookup"><span data-stu-id="258e1-174">Remove-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510173.aspx)|<span data-ttu-id="258e1-175">Remove a member from a database role.</span><span class="sxs-lookup"><span data-stu-id="258e1-175">Remove a member from a database role.</span></span>|   
|[<span data-ttu-id="258e1-176">Invoke-ASCmd</span><span class="sxs-lookup"><span data-stu-id="258e1-176">Invoke-ASCmd</span></span>](https://msdn.microsoft.com/library/hh479579.aspx)|<span data-ttu-id="258e1-177">Execute a TMSL script.</span><span class="sxs-lookup"><span data-stu-id="258e1-177">Execute a TMSL script.</span></span>|

## <a name="row-filters"></a><span data-ttu-id="258e1-178">Row filters</span><span class="sxs-lookup"><span data-stu-id="258e1-178">Row filters</span></span>  
<span data-ttu-id="258e1-179">Row filters define which rows in a table can be queried by members of a particular role.</span><span class="sxs-lookup"><span data-stu-id="258e1-179">Row filters define which rows in a table can be queried by members of a particular role.</span></span> <span data-ttu-id="258e1-180">Row filters are defined for each table in a model by using DAX formulas.</span><span class="sxs-lookup"><span data-stu-id="258e1-180">Row filters are defined for each table in a model by using DAX formulas.</span></span>  
  
<span data-ttu-id="258e1-181">Row filters can be defined only for roles with Read and Read and Process permissions.</span><span class="sxs-lookup"><span data-stu-id="258e1-181">Row filters can be defined only for roles with Read and Read and Process permissions.</span></span> <span data-ttu-id="258e1-182">By default, if a row filter is not defined for a particular table, members  can query all rows in the table unless cross-filtering applies from another table.</span><span class="sxs-lookup"><span data-stu-id="258e1-182">By default, if a row filter is not defined for a particular table, members  can query all rows in the table unless cross-filtering applies from another table.</span></span>
  
 <span data-ttu-id="258e1-183">Row filters require a DAX formula, which must evaluate to a TRUE/FALSE value, to define the rows that can be queried by members of that particular role.</span><span class="sxs-lookup"><span data-stu-id="258e1-183">Row filters require a DAX formula, which must evaluate to a TRUE/FALSE value, to define the rows that can be queried by members of that particular role.</span></span> <span data-ttu-id="258e1-184">Rows not included in the DAX formula cannot be queried.</span><span class="sxs-lookup"><span data-stu-id="258e1-184">Rows not included in the DAX formula cannot be queried.</span></span> <span data-ttu-id="258e1-185">For example, the Customers table with the following row filters expression, *=Customers [Country] = “USA”*, members of the Sales role can only see customers in the USA.</span><span class="sxs-lookup"><span data-stu-id="258e1-185">For example, the Customers table with the following row filters expression, *=Customers [Country] = “USA”*, members of the Sales role can only see customers in the USA.</span></span>  
  
<span data-ttu-id="258e1-186">Row filters apply to the specified rows and related rows.</span><span class="sxs-lookup"><span data-stu-id="258e1-186">Row filters apply to the specified rows and related rows.</span></span> <span data-ttu-id="258e1-187">When a table has multiple relationships, filters apply security for the relationship that is active.</span><span class="sxs-lookup"><span data-stu-id="258e1-187">When a table has multiple relationships, filters apply security for the relationship that is active.</span></span> <span data-ttu-id="258e1-188">Row filters are intersected with other row filers defined for related tables, for example:</span><span class="sxs-lookup"><span data-stu-id="258e1-188">Row filters are intersected with other row filers defined for related tables, for example:</span></span>  
  
|<span data-ttu-id="258e1-189">Table</span><span class="sxs-lookup"><span data-stu-id="258e1-189">Table</span></span>|<span data-ttu-id="258e1-190">DAX expression</span><span class="sxs-lookup"><span data-stu-id="258e1-190">DAX expression</span></span>|  
|-----------|--------------------|  
|<span data-ttu-id="258e1-191">Region</span><span class="sxs-lookup"><span data-stu-id="258e1-191">Region</span></span>|<span data-ttu-id="258e1-192">=Region[Country]=”USA”</span><span class="sxs-lookup"><span data-stu-id="258e1-192">=Region[Country]=”USA”</span></span>|  
|<span data-ttu-id="258e1-193">ProductCategory</span><span class="sxs-lookup"><span data-stu-id="258e1-193">ProductCategory</span></span>|<span data-ttu-id="258e1-194">=ProductCategory[Name]=”Bicycles”</span><span class="sxs-lookup"><span data-stu-id="258e1-194">=ProductCategory[Name]=”Bicycles”</span></span>|  
|<span data-ttu-id="258e1-195">Transactions</span><span class="sxs-lookup"><span data-stu-id="258e1-195">Transactions</span></span>|<span data-ttu-id="258e1-196">=Transactions[Year]=2016</span><span class="sxs-lookup"><span data-stu-id="258e1-196">=Transactions[Year]=2016</span></span>|  
  
 <span data-ttu-id="258e1-197">The net effect is members can query rows of data where the customer is in the USA, the product category is bicycles, and the year is 2016.</span><span class="sxs-lookup"><span data-stu-id="258e1-197">The net effect is members can query rows of data where the customer is in the USA, the product category is bicycles, and the year is 2016.</span></span> <span data-ttu-id="258e1-198">Users cannot query transactions outside of the USA, transactions that are not bicycles, or transactions not in 2016 unless they are a member of another role that grants these permissions.</span><span class="sxs-lookup"><span data-stu-id="258e1-198">Users cannot query transactions outside of the USA, transactions that are not bicycles, or transactions not in 2016 unless they are a member of another role that grants these permissions.</span></span>
  
 <span data-ttu-id="258e1-199">You can use the filter, *=FALSE()*, to deny access to all rows for an entire table.</span><span class="sxs-lookup"><span data-stu-id="258e1-199">You can use the filter, *=FALSE()*, to deny access to all rows for an entire table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="258e1-200">Next steps</span><span class="sxs-lookup"><span data-stu-id="258e1-200">Next steps</span></span>
  <span data-ttu-id="258e1-201">[Manage server administrators](analysis-services-server-admins.md) </span><span class="sxs-lookup"><span data-stu-id="258e1-201">[Manage server administrators](analysis-services-server-admins.md) </span></span>  
  [<span data-ttu-id="258e1-202">Manage Azure Analysis Services with PowerShell</span><span class="sxs-lookup"><span data-stu-id="258e1-202">Manage Azure Analysis Services with PowerShell</span></span>](analysis-services-powershell.md)  
  [<span data-ttu-id="258e1-203">Tabular Model Scripting Language (TMSL) Reference</span><span class="sxs-lookup"><span data-stu-id="258e1-203">Tabular Model Scripting Language (TMSL) Reference</span></span>](https://docs.microsoft.com/sql/analysis-services/tabular-model-scripting-language-tmsl-reference)

