---
title: Manage Users in Azure Blockchain Workbench
description: How to manage users in Azure Blockchain Workbench.
services: azure-blockchain
keywords: ''
author: PatAltimore
ms.author: patricka
ms.date: 4/26/2018
ms.topic: article
ms.service: azure-blockchain
ms.reviewer: zeyadr
manager: femila
ms.openlocfilehash: ff2c6a2d9b2aec7abc684a4b189ccf31c454aaeb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965661"
---
# <a name="manage-users-in-azure-blockchain-workbench"></a><span data-ttu-id="ff115-103">Manage Users in Azure Blockchain Workbench</span><span class="sxs-lookup"><span data-stu-id="ff115-103">Manage Users in Azure Blockchain Workbench</span></span>

<span data-ttu-id="ff115-104">Azure Blockchain Workbench includes user management for people and organizations that are part of your consortium.</span><span class="sxs-lookup"><span data-stu-id="ff115-104">Azure Blockchain Workbench includes user management for people and organizations that are part of your consortium.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff115-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ff115-105">Prerequisites</span></span>

<span data-ttu-id="ff115-106">A Blockchain Workbench deployment is required.</span><span class="sxs-lookup"><span data-stu-id="ff115-106">A Blockchain Workbench deployment is required.</span></span> <span data-ttu-id="ff115-107">See [Azure Blockchain Workbench deployment](blockchain-workbench-deploy.md) for details on deployment.</span><span class="sxs-lookup"><span data-stu-id="ff115-107">See [Azure Blockchain Workbench deployment](blockchain-workbench-deploy.md) for details on deployment.</span></span>

## <a name="add-azure-ad-users"></a><span data-ttu-id="ff115-108">Add Azure AD users</span><span class="sxs-lookup"><span data-stu-id="ff115-108">Add Azure AD users</span></span>

<span data-ttu-id="ff115-109">The Azure Blockchain Workbench uses Azure Active Directory (Azure AD) for authentication, access control, and roles.</span><span class="sxs-lookup"><span data-stu-id="ff115-109">The Azure Blockchain Workbench uses Azure Active Directory (Azure AD) for authentication, access control, and roles.</span></span> <span data-ttu-id="ff115-110">Users in the Blockchain Workbench Azure AD tenant can authenticate and use Blockchain Workbench.</span><span class="sxs-lookup"><span data-stu-id="ff115-110">Users in the Blockchain Workbench Azure AD tenant can authenticate and use Blockchain Workbench.</span></span> <span data-ttu-id="ff115-111">Add users to the Administrator application role to interact and perform actions.</span><span class="sxs-lookup"><span data-stu-id="ff115-111">Add users to the Administrator application role to interact and perform actions.</span></span>

<span data-ttu-id="ff115-112">Blockchain Workbench users need to exist in the Azure AD tenant before you can assign them to applications and roles.</span><span class="sxs-lookup"><span data-stu-id="ff115-112">Blockchain Workbench users need to exist in the Azure AD tenant before you can assign them to applications and roles.</span></span> <span data-ttu-id="ff115-113">To add users to Azure AD, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="ff115-113">To add users to Azure AD, use the following steps:</span></span>

1.  <span data-ttu-id="ff115-114">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ff115-114">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="ff115-115">Select your account in the top right corner, and switch to the Azure AD tenant associated to Blockchain Workbench.</span><span class="sxs-lookup"><span data-stu-id="ff115-115">Select your account in the top right corner, and switch to the Azure AD tenant associated to Blockchain Workbench.</span></span>
3.  <span data-ttu-id="ff115-116">Select **Azure Active Directory > Users**.</span><span class="sxs-lookup"><span data-stu-id="ff115-116">Select **Azure Active Directory > Users**.</span></span> <span data-ttu-id="ff115-117">You see a list of users in your directory.</span><span class="sxs-lookup"><span data-stu-id="ff115-117">You see a list of users in your directory.</span></span>
4.  <span data-ttu-id="ff115-118">To add users to the directory, select **New user**.</span><span class="sxs-lookup"><span data-stu-id="ff115-118">To add users to the directory, select **New user**.</span></span> <span data-ttu-id="ff115-119">For external users, select **New guest user**.</span><span class="sxs-lookup"><span data-stu-id="ff115-119">For external users, select **New guest user**.</span></span>

    ![New user](media/blockchain-workbench-manage-users/add-ad-user.png)

5.  <span data-ttu-id="ff115-121">Complete the required fields for the new user.</span><span class="sxs-lookup"><span data-stu-id="ff115-121">Complete the required fields for the new user.</span></span> <span data-ttu-id="ff115-122">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="ff115-122">Select **Create**.</span></span>

<span data-ttu-id="ff115-123">Visit [Azure AD](../active-directory/fundamentals/add-users-azure-active-directory.md) documentation for more details on how to manage users within Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ff115-123">Visit [Azure AD](../active-directory/fundamentals/add-users-azure-active-directory.md) documentation for more details on how to manage users within Azure AD.</span></span>

## <a name="manage-blockchain-workbench-administrators"></a><span data-ttu-id="ff115-124">Manage Blockchain Workbench administrators</span><span class="sxs-lookup"><span data-stu-id="ff115-124">Manage Blockchain Workbench administrators</span></span>

<span data-ttu-id="ff115-125">Once users have been added to the directory, the next step is to choose which users are Blockchain Workbench administrators.</span><span class="sxs-lookup"><span data-stu-id="ff115-125">Once users have been added to the directory, the next step is to choose which users are Blockchain Workbench administrators.</span></span> <span data-ttu-id="ff115-126">Users in the **Administrator** group are associated with the **Administrator application role** in Blockchain Workbench.</span><span class="sxs-lookup"><span data-stu-id="ff115-126">Users in the **Administrator** group are associated with the **Administrator application role** in Blockchain Workbench.</span></span> <span data-ttu-id="ff115-127">Administrators can add or remove users, assign users to specific scenarios, and create new applications.</span><span class="sxs-lookup"><span data-stu-id="ff115-127">Administrators can add or remove users, assign users to specific scenarios, and create new applications.</span></span>

<span data-ttu-id="ff115-128">To add users to the **Administrator** group in the Azure AD directory:</span><span class="sxs-lookup"><span data-stu-id="ff115-128">To add users to the **Administrator** group in the Azure AD directory:</span></span>

1.  <span data-ttu-id="ff115-129">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ff115-129">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="ff115-130">Verify you are in the Azure AD tenant associated to Blockchain Workbench by selecting your account in the top right corner.</span><span class="sxs-lookup"><span data-stu-id="ff115-130">Verify you are in the Azure AD tenant associated to Blockchain Workbench by selecting your account in the top right corner.</span></span>
3.  <span data-ttu-id="ff115-131">Select **Azure Active Directory >  Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="ff115-131">Select **Azure Active Directory >  Enterprise applications**.</span></span>
4.  <span data-ttu-id="ff115-132">Select the Azure AD client application for Blockchain Workbench</span><span class="sxs-lookup"><span data-stu-id="ff115-132">Select the Azure AD client application for Blockchain Workbench</span></span>
    
    ![All enterprise application registrations](media/blockchain-workbench-manage-users/select-blockchain-client-app.png)

5.  <span data-ttu-id="ff115-134">Select **Users and groups > Add user**.</span><span class="sxs-lookup"><span data-stu-id="ff115-134">Select **Users and groups > Add user**.</span></span>
6.  <span data-ttu-id="ff115-135">In **Add Assignment**, select **Users**.</span><span class="sxs-lookup"><span data-stu-id="ff115-135">In **Add Assignment**, select **Users**.</span></span> <span data-ttu-id="ff115-136">Choose or search for the user you want to add as an administrator.</span><span class="sxs-lookup"><span data-stu-id="ff115-136">Choose or search for the user you want to add as an administrator.</span></span> <span data-ttu-id="ff115-137">Click **Select** when finished choosing.</span><span class="sxs-lookup"><span data-stu-id="ff115-137">Click **Select** when finished choosing.</span></span>

    ![Add assignment](media/blockchain-workbench-manage-users/add-user-assignment.png)

9.  <span data-ttu-id="ff115-139">Verify **Role** is set to **Administrator**</span><span class="sxs-lookup"><span data-stu-id="ff115-139">Verify **Role** is set to **Administrator**</span></span>
10. <span data-ttu-id="ff115-140">Select **Assign**.</span><span class="sxs-lookup"><span data-stu-id="ff115-140">Select **Assign**.</span></span> <span data-ttu-id="ff115-141">The added users are displayed in the list with the administrator role assigned.</span><span class="sxs-lookup"><span data-stu-id="ff115-141">The added users are displayed in the list with the administrator role assigned.</span></span>

    ![Blockchain client app users](media/blockchain-workbench-manage-users/blockchain-admin-list.png)

## <a name="managing-blockchain-workbench-members"></a><span data-ttu-id="ff115-143">Managing Blockchain Workbench members</span><span class="sxs-lookup"><span data-stu-id="ff115-143">Managing Blockchain Workbench members</span></span>

<span data-ttu-id="ff115-144">Use the Blockchain Workbench application to manage users and organizations that are part of your consortium.</span><span class="sxs-lookup"><span data-stu-id="ff115-144">Use the Blockchain Workbench application to manage users and organizations that are part of your consortium.</span></span> <span data-ttu-id="ff115-145">You can add or remove users to applications and roles.</span><span class="sxs-lookup"><span data-stu-id="ff115-145">You can add or remove users to applications and roles.</span></span>

1. <span data-ttu-id="ff115-146">[Open the Blockchain Workbench](blockchain-workbench-deploy.md#blockchain-workbench-web-url) in your browser and sign in as an administrator.</span><span class="sxs-lookup"><span data-stu-id="ff115-146">[Open the Blockchain Workbench](blockchain-workbench-deploy.md#blockchain-workbench-web-url) in your browser and sign in as an administrator.</span></span>

    ![Blockchain Workbench](media/blockchain-workbench-manage-users/blockchain-workbench-applications.png)

    <span data-ttu-id="ff115-148">Members are added to each application.</span><span class="sxs-lookup"><span data-stu-id="ff115-148">Members are added to each application.</span></span> <span data-ttu-id="ff115-149">Members can have one or more application roles to initiate contracts or take actions.</span><span class="sxs-lookup"><span data-stu-id="ff115-149">Members can have one or more application roles to initiate contracts or take actions.</span></span>

2. <span data-ttu-id="ff115-150">To manage members for an application, select an application tile in the **Applications** pane.</span><span class="sxs-lookup"><span data-stu-id="ff115-150">To manage members for an application, select an application tile in the **Applications** pane.</span></span>

    <span data-ttu-id="ff115-151">The number of members associated to the selected application is reflected in the members tile.</span><span class="sxs-lookup"><span data-stu-id="ff115-151">The number of members associated to the selected application is reflected in the members tile.</span></span>

    ![Select application](media/blockchain-workbench-manage-users/blockchain-workbench-select-application.png)


#### <a name="add-member-to-application"></a><span data-ttu-id="ff115-153">Add member to application</span><span class="sxs-lookup"><span data-stu-id="ff115-153">Add member to application</span></span>

1. <span data-ttu-id="ff115-154">Select the member tile to display a list of the current members.</span><span class="sxs-lookup"><span data-stu-id="ff115-154">Select the member tile to display a list of the current members.</span></span>
2. <span data-ttu-id="ff115-155">Select **Add members**.</span><span class="sxs-lookup"><span data-stu-id="ff115-155">Select **Add members**.</span></span>

    ![Add members](media/blockchain-workbench-manage-users/application-add-members.png)

3. <span data-ttu-id="ff115-157">Search for the user's name.</span><span class="sxs-lookup"><span data-stu-id="ff115-157">Search for the user's name.</span></span>  <span data-ttu-id="ff115-158">Only Azure AD users that exist in the Blockchain Workbench tenant are listed.</span><span class="sxs-lookup"><span data-stu-id="ff115-158">Only Azure AD users that exist in the Blockchain Workbench tenant are listed.</span></span> <span data-ttu-id="ff115-159">If the user is not found, you need to [Add Azure AD users](#add-azure-ad-users).</span><span class="sxs-lookup"><span data-stu-id="ff115-159">If the user is not found, you need to [Add Azure AD users](#add-azure-ad-users).</span></span>

    ![Add members](media/blockchain-workbench-manage-users/find-user.png)

4. <span data-ttu-id="ff115-161">Select a **Role** from the drop-down.</span><span class="sxs-lookup"><span data-stu-id="ff115-161">Select a **Role** from the drop-down.</span></span>

    ![Select role members](media/blockchain-workbench-manage-users/application-select-role.png)

5. <span data-ttu-id="ff115-163">Select **Add** to add the member with the associated role to the application.</span><span class="sxs-lookup"><span data-stu-id="ff115-163">Select **Add** to add the member with the associated role to the application.</span></span>

#### <a name="remove-member-from-application"></a><span data-ttu-id="ff115-164">Remove member from application</span><span class="sxs-lookup"><span data-stu-id="ff115-164">Remove member from application</span></span>

1. <span data-ttu-id="ff115-165">Select the member tile to display a list of the current members.</span><span class="sxs-lookup"><span data-stu-id="ff115-165">Select the member tile to display a list of the current members.</span></span>
2. <span data-ttu-id="ff115-166">For the user you want to remove, choose **Remove** from the role drop-down.</span><span class="sxs-lookup"><span data-stu-id="ff115-166">For the user you want to remove, choose **Remove** from the role drop-down.</span></span>

    ![Remove member](media/blockchain-workbench-manage-users/application-remove-member.png)

#### <a name="change-or-add-role"></a><span data-ttu-id="ff115-168">Change or add role</span><span class="sxs-lookup"><span data-stu-id="ff115-168">Change or add role</span></span>

1. <span data-ttu-id="ff115-169">Select the member tile to display a list of the current members.</span><span class="sxs-lookup"><span data-stu-id="ff115-169">Select the member tile to display a list of the current members.</span></span>
2. <span data-ttu-id="ff115-170">For the user you want to change, click the drop-down and select the new role.</span><span class="sxs-lookup"><span data-stu-id="ff115-170">For the user you want to change, click the drop-down and select the new role.</span></span>

    ![Change role](media/blockchain-workbench-manage-users/application-change-role.png)

## <a name="next-steps"></a><span data-ttu-id="ff115-172">Next steps</span><span class="sxs-lookup"><span data-stu-id="ff115-172">Next steps</span></span>

<span data-ttu-id="ff115-173">In this how-to article, you have learned how to manage users for Azure Blockchain Workbench.</span><span class="sxs-lookup"><span data-stu-id="ff115-173">In this how-to article, you have learned how to manage users for Azure Blockchain Workbench.</span></span> <span data-ttu-id="ff115-174">To learn how to create a blockchain application, continue to the next how-to article.</span><span class="sxs-lookup"><span data-stu-id="ff115-174">To learn how to create a blockchain application, continue to the next how-to article.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ff115-175">Create a blockchain application in Azure Blockchain Workbench</span><span class="sxs-lookup"><span data-stu-id="ff115-175">Create a blockchain application in Azure Blockchain Workbench</span></span>](blockchain-workbench-create-app.md)
