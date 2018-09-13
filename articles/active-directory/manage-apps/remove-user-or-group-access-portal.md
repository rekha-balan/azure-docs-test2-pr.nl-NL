---
title: Remove a user or group assignment from an enterprise app in Azure Active Directory | Microsoft Docs
description: How to remove the access assignment of a user or group from an enterprise app in Azure Active Directory
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
ms.date: 02/14/2018
ms.author: barbkess
ms.reviewer: asteen
ms.custom: it-pro
ms.openlocfilehash: fde6d5fa2488d86af542f409df7c5b76d2510f08
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864571"
---
# <a name="remove-a-user-or-group-assignment-from-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="90e40-103">Remove a user or group assignment from an enterprise app in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="90e40-103">Remove a user or group assignment from an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="90e40-104">It's easy to remove a user or a group from being assigned access to one of your enterprise applications in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="90e40-104">It's easy to remove a user or a group from being assigned access to one of your enterprise applications in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="90e40-105">You must have the appropriate permissions to manage the enterprise app, and you must be global admin for the directory.</span><span class="sxs-lookup"><span data-stu-id="90e40-105">You must have the appropriate permissions to manage the enterprise app, and you must be global admin for the directory.</span></span>

> [!NOTE]
> <span data-ttu-id="90e40-106">For Microsoft Applications (such as Office 365 apps), use PowerShell to remove users to an enterprise app.</span><span class="sxs-lookup"><span data-stu-id="90e40-106">For Microsoft Applications (such as Office 365 apps), use PowerShell to remove users to an enterprise app.</span></span>

## <a name="how-do-i-remove-a-user-or-group-assignment-to-an-enterprise-app-in-the-azure-portal"></a><span data-ttu-id="90e40-107">How do I remove a user or group assignment to an enterprise app in the Azure portal?</span><span class="sxs-lookup"><span data-stu-id="90e40-107">How do I remove a user or group assignment to an enterprise app in the Azure portal?</span></span>
1. <span data-ttu-id="90e40-108">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span><span class="sxs-lookup"><span data-stu-id="90e40-108">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="90e40-109">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span><span class="sxs-lookup"><span data-stu-id="90e40-109">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="90e40-110">On the **Azure Active Directory - *directoryname*** page (that is, the Azure AD page for the directory you are managing), select **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="90e40-110">On the **Azure Active Directory - *directoryname*** page (that is, the Azure AD page for the directory you are managing), select **Enterprise applications**.</span></span>

    ![Opening Enterprise apps](./media/remove-user-or-group-access-portal/open-enterprise-apps.png)
4. <span data-ttu-id="90e40-112">On the **Enterprise applications** page, select **All applications**.</span><span class="sxs-lookup"><span data-stu-id="90e40-112">On the **Enterprise applications** page, select **All applications**.</span></span> <span data-ttu-id="90e40-113">You'll see a list of the apps you can manage.</span><span class="sxs-lookup"><span data-stu-id="90e40-113">You'll see a list of the apps you can manage.</span></span>
5. <span data-ttu-id="90e40-114">On the **Enterprise applications - All applications** page, select an app.</span><span class="sxs-lookup"><span data-stu-id="90e40-114">On the **Enterprise applications - All applications** page, select an app.</span></span>
6. <span data-ttu-id="90e40-115">On the ***appname*** page (that is, the page with the name of the selected app in the title), select **Users & Groups**.</span><span class="sxs-lookup"><span data-stu-id="90e40-115">On the ***appname*** page (that is, the page with the name of the selected app in the title), select **Users & Groups**.</span></span>

    ![Selecting users or groups](./media/remove-user-or-group-access-portal/remove-app-users.png)
7. <span data-ttu-id="90e40-117">On the ***appname*** **- User & Group Assignment** page, select one of more users or groups and then select the **Remove** command.</span><span class="sxs-lookup"><span data-stu-id="90e40-117">On the ***appname*** **- User & Group Assignment** page, select one of more users or groups and then select the **Remove** command.</span></span> <span data-ttu-id="90e40-118">Confirm your decision at the prompt.</span><span class="sxs-lookup"><span data-stu-id="90e40-118">Confirm your decision at the prompt.</span></span>

    ![Selecting the Remove command](./media/remove-user-or-group-access-portal/remove-users.png)

## <a name="how-do-i-remove-a-user-or-group-assignment-to-an-enterprise-app-using-powershell"></a><span data-ttu-id="90e40-120">How do I remove a user or group assignment to an enterprise app using PowerShell?</span><span class="sxs-lookup"><span data-stu-id="90e40-120">How do I remove a user or group assignment to an enterprise app using PowerShell?</span></span>
1. <span data-ttu-id="90e40-121">Open an elevated Windows PowerShell command prompt.</span><span class="sxs-lookup"><span data-stu-id="90e40-121">Open an elevated Windows PowerShell command prompt.</span></span>

    >[!NOTE] 
    > <span data-ttu-id="90e40-122">You need to install the AzureAD module (use the command `Install-Module -Name AzureAD`).</span><span class="sxs-lookup"><span data-stu-id="90e40-122">You need to install the AzureAD module (use the command `Install-Module -Name AzureAD`).</span></span> <span data-ttu-id="90e40-123">If prompted to install a NuGet module or the new Azure Active Directory V2 PowerShell module, type Y and press ENTER.</span><span class="sxs-lookup"><span data-stu-id="90e40-123">If prompted to install a NuGet module or the new Azure Active Directory V2 PowerShell module, type Y and press ENTER.</span></span>

2. <span data-ttu-id="90e40-124">Run `Connect-AzureAD` and sign in with a Global Admin user account.</span><span class="sxs-lookup"><span data-stu-id="90e40-124">Run `Connect-AzureAD` and sign in with a Global Admin user account.</span></span>
3. <span data-ttu-id="90e40-125">Use the following script to assign a user and role to an application:</span><span class="sxs-lookup"><span data-stu-id="90e40-125">Use the following script to assign a user and role to an application:</span></span>

    ```powershell
    # Store the proper parameters
    $user = get-azureaduser -ObjectId <objectId>
    $spo = Get-AzureADServicePrincipal -ObjectId <objectId>

    #Get the ID of role assignment 
    $assignments = Get-AzureADServiceAppRoleAssignment -ObjectId $spo.ObjectId | Where {$_.PrincipalDisplayName -eq $user.DisplayName}

    #if you run the following, it will show you what is assigned what
    $assignments | Select *

    #To remove the App role assignment run the following command.
    Remove-AzureADServiceAppRoleAssignment -ObjectId $spo.ObjectId -AppRoleAssignmentId $assignments[assignment #].ObjectId
    ``` 
## <a name="next-steps"></a><span data-ttu-id="90e40-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="90e40-126">Next steps</span></span>

- [<span data-ttu-id="90e40-127">See all of my groups</span><span class="sxs-lookup"><span data-stu-id="90e40-127">See all of my groups</span></span>](../fundamentals/active-directory-groups-view-azure-portal.md)
- [<span data-ttu-id="90e40-128">Assign a user or group to an enterprise app</span><span class="sxs-lookup"><span data-stu-id="90e40-128">Assign a user or group to an enterprise app</span></span>](assign-user-or-group-access-portal.md)
- [<span data-ttu-id="90e40-129">Disable user sign-ins for an enterprise app</span><span class="sxs-lookup"><span data-stu-id="90e40-129">Disable user sign-ins for an enterprise app</span></span>](disable-user-sign-in-portal.md)
- [<span data-ttu-id="90e40-130">Change the name or logo of an enterprise app</span><span class="sxs-lookup"><span data-stu-id="90e40-130">Change the name or logo of an enterprise app</span></span>](change-name-or-logo-portal.md)
