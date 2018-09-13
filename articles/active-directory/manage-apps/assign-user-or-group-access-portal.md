---
title: Assign a user or group to an enterprise app in Azure Active Directory | Microsoft Docs
description: How to select an enterprise app to assign a user or group to it in Azure Active Directory
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
editor: ''
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 06/06/2018
ms.author: barbkess
ms.reviewer: luleon
ms.openlocfilehash: f23c9976dacc1ca696772d6bf02b5d59e3e0b4d5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856275"
---
# <a name="assign-a-user-or-group-to-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="c7409-103">Assign a user or group to an enterprise app in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c7409-103">Assign a user or group to an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="c7409-104">To assign a user or group to an enterprise app, you must have the appropriate permissions to manage the enterprise app, and you must be global admin for the directory.</span><span class="sxs-lookup"><span data-stu-id="c7409-104">To assign a user or group to an enterprise app, you must have the appropriate permissions to manage the enterprise app, and you must be global admin for the directory.</span></span>

> [!NOTE]
> <span data-ttu-id="c7409-105">The features discussed in this article require an Azure Active Directory Premium P1 or Premium P2 license.</span><span class="sxs-lookup"><span data-stu-id="c7409-105">The features discussed in this article require an Azure Active Directory Premium P1 or Premium P2 license.</span></span> <span data-ttu-id="c7409-106">For more information, see the [Azure Active Directory pricing page](https://azure.microsoft.com/pricing/details/active-directory).</span><span class="sxs-lookup"><span data-stu-id="c7409-106">For more information, see the [Azure Active Directory pricing page](https://azure.microsoft.com/pricing/details/active-directory).</span></span>

> [!NOTE]
> <span data-ttu-id="c7409-107">For Microsoft Applications (such as Office 365 apps), use PowerShell to assign users to an enterprise app.</span><span class="sxs-lookup"><span data-stu-id="c7409-107">For Microsoft Applications (such as Office 365 apps), use PowerShell to assign users to an enterprise app.</span></span>


## <a name="how-do-i-assign-user-access-to-an-enterprise-app-in-the-azure-portal"></a><span data-ttu-id="c7409-108">How do I assign user access to an enterprise app in the Azure portal?</span><span class="sxs-lookup"><span data-stu-id="c7409-108">How do I assign user access to an enterprise app in the Azure portal?</span></span>
1. <span data-ttu-id="c7409-109">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span><span class="sxs-lookup"><span data-stu-id="c7409-109">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="c7409-110">Select **All services**, enter Azure Active Directory in the text box, and then select **Enter**.</span><span class="sxs-lookup"><span data-stu-id="c7409-110">Select **All services**, enter Azure Active Directory in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="c7409-111">On the **Azure Active Directory - *directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="c7409-111">On the **Azure Active Directory - *directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![Opening Enterprise apps](./media/assign-user-or-group-access-portal/open-enterprise-apps.png)
4. <span data-ttu-id="c7409-113">On the **Enterprise applications** blade, select **All applications**.</span><span class="sxs-lookup"><span data-stu-id="c7409-113">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="c7409-114">This lists the apps you can manage.</span><span class="sxs-lookup"><span data-stu-id="c7409-114">This lists the apps you can manage.</span></span>
5. <span data-ttu-id="c7409-115">On the **Enterprise applications - All applications** blade, select an app.</span><span class="sxs-lookup"><span data-stu-id="c7409-115">On the **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="c7409-116">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Users & Groups**.</span><span class="sxs-lookup"><span data-stu-id="c7409-116">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Users & Groups**.</span></span>

    ![Selecting the all applications command](./media/assign-user-or-group-access-portal/select-app-users.png)
7. <span data-ttu-id="c7409-118">On the ***appname*** **- User & Group Assignment** blade, select the **Add** command.</span><span class="sxs-lookup"><span data-stu-id="c7409-118">On the ***appname*** **- User & Group Assignment** blade, select the **Add** command.</span></span>
8. <span data-ttu-id="c7409-119">On the **Add Assignment** blade, select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="c7409-119">On the **Add Assignment** blade, select **Users and groups**.</span></span>

    ![Assign a user or group to the app](./media/assign-user-or-group-access-portal/assign-users.png)
9. <span data-ttu-id="c7409-121">On the **Users and groups** blade, select one or more users or groups from the list and then select the **Select** button at the bottom of the blade.</span><span class="sxs-lookup"><span data-stu-id="c7409-121">On the **Users and groups** blade, select one or more users or groups from the list and then select the **Select** button at the bottom of the blade.</span></span>
10. <span data-ttu-id="c7409-122">On the **Add Assignment** blade, select **Role**.</span><span class="sxs-lookup"><span data-stu-id="c7409-122">On the **Add Assignment** blade, select **Role**.</span></span> <span data-ttu-id="c7409-123">Then, on the **Select Role** blade, select a role to apply to the selected users or groups, and then select the **OK** button at the bottom of the blade.</span><span class="sxs-lookup"><span data-stu-id="c7409-123">Then, on the **Select Role** blade, select a role to apply to the selected users or groups, and then select the **OK** button at the bottom of the blade.</span></span>
11. <span data-ttu-id="c7409-124">On the **Add Assignment** blade, select the **Assign** button at the bottom of the blade.</span><span class="sxs-lookup"><span data-stu-id="c7409-124">On the **Add Assignment** blade, select the **Assign** button at the bottom of the blade.</span></span> <span data-ttu-id="c7409-125">The assigned users or groups have the permissions defined by the selected role for this enterprise app.</span><span class="sxs-lookup"><span data-stu-id="c7409-125">The assigned users or groups have the permissions defined by the selected role for this enterprise app.</span></span>

## <a name="how-do-i-assign-a-user-to-an-enterprise-app-using-powershell"></a><span data-ttu-id="c7409-126">How do I assign a user to an enterprise app using PowerShell?</span><span class="sxs-lookup"><span data-stu-id="c7409-126">How do I assign a user to an enterprise app using PowerShell?</span></span>

1. <span data-ttu-id="c7409-127">Open an elevated Windows PowerShell command prompt.</span><span class="sxs-lookup"><span data-stu-id="c7409-127">Open an elevated Windows PowerShell command prompt.</span></span>

    >[!NOTE] 
    > <span data-ttu-id="c7409-128">You need to install the AzureAD module (use the command `Install-Module -Name AzureAD`).</span><span class="sxs-lookup"><span data-stu-id="c7409-128">You need to install the AzureAD module (use the command `Install-Module -Name AzureAD`).</span></span> <span data-ttu-id="c7409-129">If prompted to install a NuGet module or the new Azure Active Directory V2 PowerShell module, type Y and press ENTER.</span><span class="sxs-lookup"><span data-stu-id="c7409-129">If prompted to install a NuGet module or the new Azure Active Directory V2 PowerShell module, type Y and press ENTER.</span></span>

2. <span data-ttu-id="c7409-130">Run `Connect-AzureAD` and sign in with a Global Admin user account.</span><span class="sxs-lookup"><span data-stu-id="c7409-130">Run `Connect-AzureAD` and sign in with a Global Admin user account.</span></span>
3. <span data-ttu-id="c7409-131">Use the following script to assign a user and role to an application:</span><span class="sxs-lookup"><span data-stu-id="c7409-131">Use the following script to assign a user and role to an application:</span></span>

    ```powershell
    # Assign the values to the variables
    $username = "<You user's UPN>"
    $app_name = "<Your App's display name>"
    $app_role_name = "<App role display name>"
    
    # Get the user to assign, and the service principal for the app to assign to
    $user = Get-AzureADUser -ObjectId "$username"
    $sp = Get-AzureADServicePrincipal -Filter "displayName eq '$app_name'"
    $appRole = $sp.AppRoles | Where-Object { $_.DisplayName -eq $app_role_name }
    
    # Assign the user to the app role
    New-AzureADUserAppRoleAssignment -ObjectId $user.ObjectId -PrincipalId $user.ObjectId -ResourceId $sp.ObjectId -Id $appRole.Id
    ```     

<span data-ttu-id="c7409-132">For more information about how to assign a user to an application role visit the documentation for [New-AzureADUserAppRoleAssignment](https://docs.microsoft.com/powershell/module/azuread/new-azureaduserapproleassignment?view=azureadps-2.0)</span><span class="sxs-lookup"><span data-stu-id="c7409-132">For more information about how to assign a user to an application role visit the documentation for [New-AzureADUserAppRoleAssignment](https://docs.microsoft.com/powershell/module/azuread/new-azureaduserapproleassignment?view=azureadps-2.0)</span></span>

<span data-ttu-id="c7409-133">To assign a group to an enterprise app, you need to replace `Get-AzureADUser` with `Get-AzureADGroup`.</span><span class="sxs-lookup"><span data-stu-id="c7409-133">To assign a group to an enterprise app, you need to replace `Get-AzureADUser` with `Get-AzureADGroup`.</span></span>

### <a name="example"></a><span data-ttu-id="c7409-134">Example</span><span class="sxs-lookup"><span data-stu-id="c7409-134">Example</span></span>

<span data-ttu-id="c7409-135">This example assigns the user Britta Simon to the [Microsoft Workplace Analytics](https://products.office.com/business/workplace-analytics) application using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c7409-135">This example assigns the user Britta Simon to the [Microsoft Workplace Analytics](https://products.office.com/business/workplace-analytics) application using PowerShell.</span></span>

1. <span data-ttu-id="c7409-136">In PowerShell, assign the corresponding values to the variables $username, $app_name and $app_role_name.</span><span class="sxs-lookup"><span data-stu-id="c7409-136">In PowerShell, assign the corresponding values to the variables $username, $app_name and $app_role_name.</span></span> 

    ```powershell
    # Assign the values to the variables
    $username = "britta.simon@contoso.com"
    $app_name = "Workplace Analytics"
    ```

2. <span data-ttu-id="c7409-137">In this example, we don't know what is the exact name of the application role we want to assign to Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c7409-137">In this example, we don't know what is the exact name of the application role we want to assign to Britta Simon.</span></span> <span data-ttu-id="c7409-138">Run the following commands to get the user ($user) and the service principal ($sp) using the user UPN and the service principal display names.</span><span class="sxs-lookup"><span data-stu-id="c7409-138">Run the following commands to get the user ($user) and the service principal ($sp) using the user UPN and the service principal display names.</span></span>

    ```powershell
    # Get the user to assign, and the service principal for the app to assign to
    $user = Get-AzureADUser -ObjectId "$username"
    $sp = Get-AzureADServicePrincipal -Filter "displayName eq '$app_name'"
    ```
        
3. <span data-ttu-id="c7409-139">Run the command `$sp.AppRoles` to display the roles available for the Workplace Analytics application.</span><span class="sxs-lookup"><span data-stu-id="c7409-139">Run the command `$sp.AppRoles` to display the roles available for the Workplace Analytics application.</span></span> <span data-ttu-id="c7409-140">In this example, we want to assign Britta Simon the Analyst (Limited access) Role.</span><span class="sxs-lookup"><span data-stu-id="c7409-140">In this example, we want to assign Britta Simon the Analyst (Limited access) Role.</span></span>
    
    ![Workplace Analytics Role](./media/assign-user-or-group-access-portal/workplace-analytics-role.png)

4. <span data-ttu-id="c7409-142">Assign the role name to the `$app_role_name` variable.</span><span class="sxs-lookup"><span data-stu-id="c7409-142">Assign the role name to the `$app_role_name` variable.</span></span>
        
    ```powershell
    # Assign the values to the variables
    $app_role_name = "Analyst (Limited access)"
    $appRole = $sp.AppRoles | Where-Object { $_.DisplayName -eq $app_role_name }
    ```

5. <span data-ttu-id="c7409-143">Run the following command to assign the user to the app role:</span><span class="sxs-lookup"><span data-stu-id="c7409-143">Run the following command to assign the user to the app role:</span></span>

    ```powershell
    # Assign the user to the app role
    New-AzureADUserAppRoleAssignment -ObjectId $user.ObjectId -PrincipalId $user.ObjectId -ResourceId $sp.ObjectId -Id $appRole.Id
    ```

## <a name="next-steps"></a><span data-ttu-id="c7409-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="c7409-144">Next steps</span></span>
* [<span data-ttu-id="c7409-145">See all of my groups</span><span class="sxs-lookup"><span data-stu-id="c7409-145">See all of my groups</span></span>](../fundamentals/active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="c7409-146">Remove a user or group assignment from an enterprise app</span><span class="sxs-lookup"><span data-stu-id="c7409-146">Remove a user or group assignment from an enterprise app</span></span>](remove-user-or-group-access-portal.md)
* [<span data-ttu-id="c7409-147">Disable user sign-ins for an enterprise app</span><span class="sxs-lookup"><span data-stu-id="c7409-147">Disable user sign-ins for an enterprise app</span></span>](disable-user-sign-in-portal.md)
* [<span data-ttu-id="c7409-148">Change the name or logo of an enterprise app</span><span class="sxs-lookup"><span data-stu-id="c7409-148">Change the name or logo of an enterprise app</span></span>](change-name-or-logo-portal.md)
