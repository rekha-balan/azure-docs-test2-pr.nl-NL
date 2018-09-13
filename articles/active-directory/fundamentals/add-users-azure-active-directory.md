---
title: Add or delete users in Azure Active Directory | Microsoft Docs
description: Explains how to add new users or delete existing users in Azure Active Directory
services: active-directory
documentationcenter: ''
author: eross-msft
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.component: fundamentals
ms.topic: quickstart
ms.date: 01/08/2018
ms.author: lizross
ms.reviewer: jeffsta
ms.custom: it-pro
ms.openlocfilehash: e6e21ea09909a3bd92a21e15428af347e3f20b93
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870566"
---
# <a name="quickstart-add-new-users-to-azure-active-directory"></a><span data-ttu-id="98864-103">Quickstart: Add new users to Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="98864-103">Quickstart: Add new users to Azure Active Directory</span></span>
<span data-ttu-id="98864-104">This article explains how to delete or add users in your organization into your orgnization's Azure Active Directory (Azure AD) tenant using the Azure portal or by synchronizing your on-premises Windows Server AD user account data.</span><span class="sxs-lookup"><span data-stu-id="98864-104">This article explains how to delete or add users in your organization into your orgnization's Azure Active Directory (Azure AD) tenant using the Azure portal or by synchronizing your on-premises Windows Server AD user account data.</span></span> 

## <a name="add-cloud-based-users"></a><span data-ttu-id="98864-105">Add cloud-based users</span><span class="sxs-lookup"><span data-stu-id="98864-105">Add cloud-based users</span></span>
1. <span data-ttu-id="98864-106">Sign in to the [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for the directory.</span><span class="sxs-lookup"><span data-stu-id="98864-106">Sign in to the [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="98864-107">Select **Azure Active Directory** and then **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="98864-107">Select **Azure Active Directory** and then **Users and groups**.</span></span>
3. <span data-ttu-id="98864-108">On **Users and groups**, select **All users**, and then select **New user**.</span><span class="sxs-lookup"><span data-stu-id="98864-108">On **Users and groups**, select **All users**, and then select **New user**.</span></span>
   <span data-ttu-id="98864-109">![Selecting the Add command](./media/add-users-azure-active-directory/add-user.png)</span><span class="sxs-lookup"><span data-stu-id="98864-109">![Selecting the Add command](./media/add-users-azure-active-directory/add-user.png)</span></span>
4. <span data-ttu-id="98864-110">Enter details for the user, such as **Name** and **User name**.</span><span class="sxs-lookup"><span data-stu-id="98864-110">Enter details for the user, such as **Name** and **User name**.</span></span> <span data-ttu-id="98864-111">The domain name portion of the user name must either be the initial default domain name "[domain name].onmicrosoft.com" or a verified, non-federated [custom domain name](add-custom-domain.md) such as "contoso.com."</span><span class="sxs-lookup"><span data-stu-id="98864-111">The domain name portion of the user name must either be the initial default domain name "[domain name].onmicrosoft.com" or a verified, non-federated [custom domain name](add-custom-domain.md) such as "contoso.com."</span></span>
5. <span data-ttu-id="98864-112">Copy or otherwise note the generated user password so that you can provide it to the user after this process is complete.</span><span class="sxs-lookup"><span data-stu-id="98864-112">Copy or otherwise note the generated user password so that you can provide it to the user after this process is complete.</span></span>
6. <span data-ttu-id="98864-113">Optionally, you can open and fill out the information in **Profile**, **Groups**, or **Directory role** for the user.</span><span class="sxs-lookup"><span data-stu-id="98864-113">Optionally, you can open and fill out the information in **Profile**, **Groups**, or **Directory role** for the user.</span></span> <span data-ttu-id="98864-114">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](../users-groups-roles/directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="98864-114">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](../users-groups-roles/directory-assign-admin-roles.md).</span></span>
7. <span data-ttu-id="98864-115">On **User**, select **Create**.</span><span class="sxs-lookup"><span data-stu-id="98864-115">On **User**, select **Create**.</span></span>
8. <span data-ttu-id="98864-116">Securely distribute the generated password to the new user so that the user can sign in.</span><span class="sxs-lookup"><span data-stu-id="98864-116">Securely distribute the generated password to the new user so that the user can sign in.</span></span>

> [!TIP]
> <span data-ttu-id="98864-117">You can also synchronize user account data from on-premises Windows Server AD.</span><span class="sxs-lookup"><span data-stu-id="98864-117">You can also synchronize user account data from on-premises Windows Server AD.</span></span> <span data-ttu-id="98864-118">Microsoft’s identity solutions span on-premises and cloud-based capabilities, creating a single user identity for authentication and authorization to all resources, regardless of location.</span><span class="sxs-lookup"><span data-stu-id="98864-118">Microsoft’s identity solutions span on-premises and cloud-based capabilities, creating a single user identity for authentication and authorization to all resources, regardless of location.</span></span> <span data-ttu-id="98864-119">We call this Hybrid Identity.</span><span class="sxs-lookup"><span data-stu-id="98864-119">We call this Hybrid Identity.</span></span> <span data-ttu-id="98864-120">[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) can be used to integrate your on-premises directories with Azure Active Directory for hybrid identity scenarios.</span><span class="sxs-lookup"><span data-stu-id="98864-120">[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) can be used to integrate your on-premises directories with Azure Active Directory for hybrid identity scenarios.</span></span> <span data-ttu-id="98864-121">This allows you to provide a common identity for your users for Office 365, Azure, and SaaS applications integrated with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="98864-121">This allows you to provide a common identity for your users for Office 365, Azure, and SaaS applications integrated with Azure AD.</span></span> 

## <a name="delete-users-from-azure-ad"></a><span data-ttu-id="98864-122">Delete users from Azure AD</span><span class="sxs-lookup"><span data-stu-id="98864-122">Delete users from Azure AD</span></span>
1. <span data-ttu-id="98864-123">Sign in to the [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for the directory.</span><span class="sxs-lookup"><span data-stu-id="98864-123">Sign in to the [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="98864-124">Select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="98864-124">Select **Users and groups**.</span></span>
3. <span data-ttu-id="98864-125">On the **Users and groups** blade, select the user to delete from the list.</span><span class="sxs-lookup"><span data-stu-id="98864-125">On the **Users and groups** blade, select the user to delete from the list.</span></span> 
4. <span data-ttu-id="98864-126">On the blade for the selected user, select **Overview**, and then in the command bar, select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="98864-126">On the blade for the selected user, select **Overview**, and then in the command bar, select **Delete**.</span></span>
   <span data-ttu-id="98864-127">![Selecting the Add command](./media/add-users-azure-active-directory/delete-user.png)</span><span class="sxs-lookup"><span data-stu-id="98864-127">![Selecting the Add command](./media/add-users-azure-active-directory/delete-user.png)</span></span>


### <a name="learn-more"></a><span data-ttu-id="98864-128">Learn more</span><span class="sxs-lookup"><span data-stu-id="98864-128">Learn more</span></span> 
* [<span data-ttu-id="98864-129">Add guest users from another directory</span><span class="sxs-lookup"><span data-stu-id="98864-129">Add guest users from another directory</span></span>](../b2b/what-is-b2b.md) 
* [<span data-ttu-id="98864-130">Assign a user to a role in your Azure AD</span><span class="sxs-lookup"><span data-stu-id="98864-130">Assign a user to a role in your Azure AD</span></span>](active-directory-users-assign-role-azure-portal.md)
* [<span data-ttu-id="98864-131">Manage user profiles</span><span class="sxs-lookup"><span data-stu-id="98864-131">Manage user profiles</span></span>](active-directory-users-profile-azure-portal.md)
* [<span data-ttu-id="98864-132">Restore a deleted user</span><span class="sxs-lookup"><span data-stu-id="98864-132">Restore a deleted user</span></span>](active-directory-users-restore.md)



## <a name="next-steps"></a><span data-ttu-id="98864-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="98864-133">Next steps</span></span>
<span data-ttu-id="98864-134">In this quickstart, you’ve learned how to add new users to Azure AD Premium.</span><span class="sxs-lookup"><span data-stu-id="98864-134">In this quickstart, you’ve learned how to add new users to Azure AD Premium.</span></span> 

<span data-ttu-id="98864-135">You can use the following link to create a new user in Azure AD from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="98864-135">You can use the following link to create a new user in Azure AD from the Azure portal.</span></span>

>[!div class="nextstepaction"]
>[<span data-ttu-id="98864-136">Add users to Azure AD</span><span class="sxs-lookup"><span data-stu-id="98864-136">Add users to Azure AD</span></span>](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/)