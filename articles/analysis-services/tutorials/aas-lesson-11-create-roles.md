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
# <a name="create-roles"></a><span data-ttu-id="2be11-103">Create roles</span><span class="sxs-lookup"><span data-stu-id="2be11-103">Create roles</span></span>

<span data-ttu-id="2be11-104">In this lesson, you create roles.</span><span class="sxs-lookup"><span data-stu-id="2be11-104">In this lesson, you create roles.</span></span> <span data-ttu-id="2be11-105">Roles provide model database object and data security by limiting access to only those users that are role members.</span><span class="sxs-lookup"><span data-stu-id="2be11-105">Roles provide model database object and data security by limiting access to only those users that are role members.</span></span> <span data-ttu-id="2be11-106">Each role is defined with a single permission: None, Read, Read and Process, Process, or Administrator.</span><span class="sxs-lookup"><span data-stu-id="2be11-106">Each role is defined with a single permission: None, Read, Read and Process, Process, or Administrator.</span></span> <span data-ttu-id="2be11-107">Roles can be defined during model authoring by using Role Manager.</span><span class="sxs-lookup"><span data-stu-id="2be11-107">Roles can be defined during model authoring by using Role Manager.</span></span> <span data-ttu-id="2be11-108">After a model has been deployed, you can manage roles by using SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="2be11-108">After a model has been deployed, you can manage roles by using SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="2be11-109">To learn more, see [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="2be11-109">To learn more, see [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular).</span></span>
  
> [!NOTE]  
> <span data-ttu-id="2be11-110">Creating roles is not necessary to complete this tutorial.</span><span class="sxs-lookup"><span data-stu-id="2be11-110">Creating roles is not necessary to complete this tutorial.</span></span> <span data-ttu-id="2be11-111">By default, the account you are currently logged in with has Administrator privileges on the model.</span><span class="sxs-lookup"><span data-stu-id="2be11-111">By default, the account you are currently logged in with has Administrator privileges on the model.</span></span> <span data-ttu-id="2be11-112">However, for other users in your organization to browse by using a reporting client, you must create at least one role with Read permissions and add those users as members.</span><span class="sxs-lookup"><span data-stu-id="2be11-112">However, for other users in your organization to browse by using a reporting client, you must create at least one role with Read permissions and add those users as members.</span></span>  
  
<span data-ttu-id="2be11-113">You create three roles:</span><span class="sxs-lookup"><span data-stu-id="2be11-113">You create three roles:</span></span>  
  
-   <span data-ttu-id="2be11-114">**Sales Manager** – This role can include users in your organization for which you want to have Read permission to all model objects and data.</span><span class="sxs-lookup"><span data-stu-id="2be11-114">**Sales Manager** – This role can include users in your organization for which you want to have Read permission to all model objects and data.</span></span>  
  
-   <span data-ttu-id="2be11-115">**Sales Analyst US** – This role can include users in your organization for which you want only to be able to browse data related to sales in the United States.</span><span class="sxs-lookup"><span data-stu-id="2be11-115">**Sales Analyst US** – This role can include users in your organization for which you want only to be able to browse data related to sales in the United States.</span></span> <span data-ttu-id="2be11-116">For this role, you use a DAX formula to define a *Row Filter*, which restricts members to browse data only for the United States.</span><span class="sxs-lookup"><span data-stu-id="2be11-116">For this role, you use a DAX formula to define a *Row Filter*, which restricts members to browse data only for the United States.</span></span>  
  
-   <span data-ttu-id="2be11-117">**Administrator** – This role can include users for which you want to have Administrator permission, which allows unlimited access and permissions to perform administrative tasks on the model database.</span><span class="sxs-lookup"><span data-stu-id="2be11-117">**Administrator** – This role can include users for which you want to have Administrator permission, which allows unlimited access and permissions to perform administrative tasks on the model database.</span></span>  
  
<span data-ttu-id="2be11-118">Because Windows user and group accounts in your organization are unique, you can add accounts from your particular organization to members.</span><span class="sxs-lookup"><span data-stu-id="2be11-118">Because Windows user and group accounts in your organization are unique, you can add accounts from your particular organization to members.</span></span> <span data-ttu-id="2be11-119">However, for this tutorial, you can also leave the members blank.</span><span class="sxs-lookup"><span data-stu-id="2be11-119">However, for this tutorial, you can also leave the members blank.</span></span> <span data-ttu-id="2be11-120">You test the effect of each role later in Lesson 12: Analyze in Excel.</span><span class="sxs-lookup"><span data-stu-id="2be11-120">You test the effect of each role later in Lesson 12: Analyze in Excel.</span></span>  
  
<span data-ttu-id="2be11-121">Estimated time to complete this lesson: **15 minutes**</span><span class="sxs-lookup"><span data-stu-id="2be11-121">Estimated time to complete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="2be11-122">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2be11-122">Prerequisites</span></span>  
<span data-ttu-id="2be11-123">This topic is part of a tabular modeling tutorial, which should be completed in order.</span><span class="sxs-lookup"><span data-stu-id="2be11-123">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="2be11-124">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 10: Create partitions](../tutorials/aas-lesson-10-create-partitions.md).</span><span class="sxs-lookup"><span data-stu-id="2be11-124">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 10: Create partitions](../tutorials/aas-lesson-10-create-partitions.md).</span></span>  
  
## <a name="create-roles"></a><span data-ttu-id="2be11-125">Create roles</span><span class="sxs-lookup"><span data-stu-id="2be11-125">Create roles</span></span>  
  
#### <a name="to-create-a-sales-manager-user-role"></a><span data-ttu-id="2be11-126">To create a Sales Manager user role</span><span class="sxs-lookup"><span data-stu-id="2be11-126">To create a Sales Manager user role</span></span>  
  
1.  <span data-ttu-id="2be11-127">In Tabular Model Explorer, right-click **Roles** > **Roles**.</span><span class="sxs-lookup"><span data-stu-id="2be11-127">In Tabular Model Explorer, right-click **Roles** > **Roles**.</span></span>  
  
2.  <span data-ttu-id="2be11-128">In Role Manager, click **New**.</span><span class="sxs-lookup"><span data-stu-id="2be11-128">In Role Manager, click **New**.</span></span>  
  
3.  <span data-ttu-id="2be11-129">Click the new role, and then in the **Name** column, rename the role to **Sales Manager**.</span><span class="sxs-lookup"><span data-stu-id="2be11-129">Click the new role, and then in the **Name** column, rename the role to **Sales Manager**.</span></span>  
  
4.  <span data-ttu-id="2be11-130">In the **Permissions** column, click the dropdown list, and then select the **Read** permission.</span><span class="sxs-lookup"><span data-stu-id="2be11-130">In the **Permissions** column, click the dropdown list, and then select the **Read** permission.</span></span> 

    ![aas-lesson11-new-role](../tutorials/media/aas-lesson11-new-role.png) 
  
5.  <span data-ttu-id="2be11-132">Optional: Click the **Members** tab, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="2be11-132">Optional: Click the **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="2be11-133">In the **Select Users or Groups** dialog box, enter the Windows users or groups from your organization you want to include in the role.</span><span class="sxs-lookup"><span data-stu-id="2be11-133">In the **Select Users or Groups** dialog box, enter the Windows users or groups from your organization you want to include in the role.</span></span>  
  
#### <a name="to-create-a-sales-analyst-us-user-role"></a><span data-ttu-id="2be11-134">To create a Sales Analyst US user role</span><span class="sxs-lookup"><span data-stu-id="2be11-134">To create a Sales Analyst US user role</span></span>  
  
1.  <span data-ttu-id="2be11-135">In Role Manager, click **New**.</span><span class="sxs-lookup"><span data-stu-id="2be11-135">In Role Manager, click **New**.</span></span>    
  
2.  <span data-ttu-id="2be11-136">Rename the role to **Sales Analyst US**.</span><span class="sxs-lookup"><span data-stu-id="2be11-136">Rename the role to **Sales Analyst US**.</span></span>  
  
3.  <span data-ttu-id="2be11-137">Give this role **Read** permission.</span><span class="sxs-lookup"><span data-stu-id="2be11-137">Give this role **Read** permission.</span></span>  
  
4.  <span data-ttu-id="2be11-138">Click the Row Filters tab, and then for the **DimGeography** table only, in the DAX Filter column, type the following formula:</span><span class="sxs-lookup"><span data-stu-id="2be11-138">Click the Row Filters tab, and then for the **DimGeography** table only, in the DAX Filter column, type the following formula:</span></span>  
  
    ```Administrator
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    <span data-ttu-id="2be11-139">A Row Filter formula must resolve to a Boolean (TRUE/FALSE) value.</span><span class="sxs-lookup"><span data-stu-id="2be11-139">A Row Filter formula must resolve to a Boolean (TRUE/FALSE) value.</span></span> <span data-ttu-id="2be11-140">With this formula, you are specifying that only rows with the Country Region Code value of “US” are visible to the user.</span><span class="sxs-lookup"><span data-stu-id="2be11-140">With this formula, you are specifying that only rows with the Country Region Code value of “US” are visible to the user.</span></span>  
    ![aas-lesson11-role-filter](../tutorials/media/aas-lesson11-role-filter.png) 
  
6.  <span data-ttu-id="2be11-142">Optional: Click the **Members** tab, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="2be11-142">Optional: Click the **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="2be11-143">In the **Select Users or Groups** dialog box, enter the Windows users or groups from your organization you want to include in the role.</span><span class="sxs-lookup"><span data-stu-id="2be11-143">In the **Select Users or Groups** dialog box, enter the Windows users or groups from your organization you want to include in the role.</span></span>  
  
#### <a name="to-create-an-administrator-user-role"></a><span data-ttu-id="2be11-144">To create an Administrator user role</span><span class="sxs-lookup"><span data-stu-id="2be11-144">To create an Administrator user role</span></span>  
  
1.  <span data-ttu-id="2be11-145">Click **New**.</span><span class="sxs-lookup"><span data-stu-id="2be11-145">Click **New**.</span></span>  
  
2.  <span data-ttu-id="2be11-146">Rename the role to **Administrator**.</span><span class="sxs-lookup"><span data-stu-id="2be11-146">Rename the role to **Administrator**.</span></span>  
  
3.  <span data-ttu-id="2be11-147">Give this role **Administrator** permission.</span><span class="sxs-lookup"><span data-stu-id="2be11-147">Give this role **Administrator** permission.</span></span>  
  
4.  <span data-ttu-id="2be11-148">Optional: Click the **Members** tab, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="2be11-148">Optional: Click the **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="2be11-149">In the **Select Users or Groups** dialog box, enter the Windows users or groups from your organization you want to include in the role.</span><span class="sxs-lookup"><span data-stu-id="2be11-149">In the **Select Users or Groups** dialog box, enter the Windows users or groups from your organization you want to include in the role.</span></span> 
  
  
## <a name="whats-next"></a><span data-ttu-id="2be11-150">What's next?</span><span class="sxs-lookup"><span data-stu-id="2be11-150">What's next?</span></span>
<span data-ttu-id="2be11-151">[Lesson 12: Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span><span class="sxs-lookup"><span data-stu-id="2be11-151">[Lesson 12: Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span></span>

  
  
