---
title: Dynamic group membership add remove users automatically tutorial in Azure Active Directory
description: In this tutorial, you use groups with user membership rules to add or remove users automatically
services: active-directory
documentationcenter: ''
author: curtand
manager: mtillman
editor: ''
ms.service: active-directory
ms.workload: identity
ms.component: users-groups-roles
ms.topic: tutorial
ms.date: 08/07/2018
ms.author: curtand
ms.reviewer: krbain
ms.custom: it-pro
ms.openlocfilehash: 2119bb60cbdc36f62623ce0db52885e17f3d3006
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856224"
---
# <a name="tutorial-add-or-remove-group-members-automatically"></a><span data-ttu-id="226c3-103">Tutorial: Add or remove group members automatically</span><span class="sxs-lookup"><span data-stu-id="226c3-103">Tutorial: Add or remove group members automatically</span></span>

<span data-ttu-id="226c3-104">In Azure Active Directory (Azure AD), you can automatically add or remove users to security groups or Office 365 groups, so you don't always have to do it manually.</span><span class="sxs-lookup"><span data-stu-id="226c3-104">In Azure Active Directory (Azure AD), you can automatically add or remove users to security groups or Office 365 groups, so you don't always have to do it manually.</span></span> <span data-ttu-id="226c3-105">Whenever any properties of a user or device change, Azure AD evaluates all dynamic group rules in your tenant to see if the change should add or remove members.</span><span class="sxs-lookup"><span data-stu-id="226c3-105">Whenever any properties of a user or device change, Azure AD evaluates all dynamic group rules in your tenant to see if the change should add or remove members.</span></span>

<span data-ttu-id="226c3-106">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="226c3-106">In this tutorial, you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="226c3-107">Create an automatically populated group of guest users from a particular partner company</span><span class="sxs-lookup"><span data-stu-id="226c3-107">Create an automatically populated group of guest users from a particular partner company</span></span>
> * <span data-ttu-id="226c3-108">Assign licenses to the group for the partner-specific features for guest users to access</span><span class="sxs-lookup"><span data-stu-id="226c3-108">Assign licenses to the group for the partner-specific features for guest users to access</span></span>
> * <span data-ttu-id="226c3-109">Bonus: secure the **All users** group by removing guest users so that, for example, you can give your member users access to internal-only sites</span><span class="sxs-lookup"><span data-stu-id="226c3-109">Bonus: secure the **All users** group by removing guest users so that, for example, you can give your member users access to internal-only sites</span></span>

<span data-ttu-id="226c3-110">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="226c3-110">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="226c3-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="226c3-111">Prerequisites</span></span>

<span data-ttu-id="226c3-112">This feature requires one Azure AD Premium license for you as the gobal administrator of the tenant.</span><span class="sxs-lookup"><span data-stu-id="226c3-112">This feature requires one Azure AD Premium license for you as the gobal administrator of the tenant.</span></span> <span data-ttu-id="226c3-113">If you don't have one, in Azure AD, select **Licenses** > **Products** > **Try/Buy**.</span><span class="sxs-lookup"><span data-stu-id="226c3-113">If you don't have one, in Azure AD, select **Licenses** > **Products** > **Try/Buy**.</span></span>

<span data-ttu-id="226c3-114">You're not required to assign licenses to the users for them to be members in dynamic groups.</span><span class="sxs-lookup"><span data-stu-id="226c3-114">You're not required to assign licenses to the users for them to be members in dynamic groups.</span></span> <span data-ttu-id="226c3-115">You only need the minimum number of available Azure AD Premium P1 licenses in the tenant to cover all such users.</span><span class="sxs-lookup"><span data-stu-id="226c3-115">You only need the minimum number of available Azure AD Premium P1 licenses in the tenant to cover all such users.</span></span> 

## <a name="create-a-group-of-guest-users"></a><span data-ttu-id="226c3-116">Create a group of guest users</span><span class="sxs-lookup"><span data-stu-id="226c3-116">Create a group of guest users</span></span>

<span data-ttu-id="226c3-117">First, you'll create a group for your guest users who all are from a single partner company.</span><span class="sxs-lookup"><span data-stu-id="226c3-117">First, you'll create a group for your guest users who all are from a single partner company.</span></span> <span data-ttu-id="226c3-118">They need special licensing, so it's often more efficient to create a group for this purpose.</span><span class="sxs-lookup"><span data-stu-id="226c3-118">They need special licensing, so it's often more efficient to create a group for this purpose.</span></span>

1. <span data-ttu-id="226c3-119">Sign in to the Azure portal (https://portal.azure.com) with an account that is the gobal administrator for your tenant.</span><span class="sxs-lookup"><span data-stu-id="226c3-119">Sign in to the Azure portal (https://portal.azure.com) with an account that is the gobal administrator for your tenant.</span></span>
2. <span data-ttu-id="226c3-120">Select **Azure Active Directory** > **Groups** > **New group**.</span><span class="sxs-lookup"><span data-stu-id="226c3-120">Select **Azure Active Directory** > **Groups** > **New group**.</span></span>
  <span data-ttu-id="226c3-121">![select the new group command](./media/groups-dynamic-tutorial/new-group.png)</span><span class="sxs-lookup"><span data-stu-id="226c3-121">![select the new group command](./media/groups-dynamic-tutorial/new-group.png)</span></span>
3. <span data-ttu-id="226c3-122">On the **Group** blade:</span><span class="sxs-lookup"><span data-stu-id="226c3-122">On the **Group** blade:</span></span>
  
  * <span data-ttu-id="226c3-123">Select **Security** as the group type</span><span class="sxs-lookup"><span data-stu-id="226c3-123">Select **Security** as the group type</span></span>
  * <span data-ttu-id="226c3-124">Enter `Guest users Contoso` as the name and description for the group</span><span class="sxs-lookup"><span data-stu-id="226c3-124">Enter `Guest users Contoso` as the name and description for the group</span></span>
  * <span data-ttu-id="226c3-125">Change **Membership type** to **Dynamic User**</span><span class="sxs-lookup"><span data-stu-id="226c3-125">Change **Membership type** to **Dynamic User**</span></span>
  * <span data-ttu-id="226c3-126">Select **Add dynamic query**</span><span class="sxs-lookup"><span data-stu-id="226c3-126">Select **Add dynamic query**</span></span>
  
4. <span data-ttu-id="226c3-127">Select **Advanced rule**, and in the **Advanced rule** box, enter: `(user.userType -eq "Guest") -and (user.companyName -eq "Contoso")`</span><span class="sxs-lookup"><span data-stu-id="226c3-127">Select **Advanced rule**, and in the **Advanced rule** box, enter: `(user.userType -eq "Guest") -and (user.companyName -eq "Contoso")`</span></span>
5. <span data-ttu-id="226c3-128">Select **Add query** to close the blade.</span><span class="sxs-lookup"><span data-stu-id="226c3-128">Select **Add query** to close the blade.</span></span>
6. <span data-ttu-id="226c3-129">On the **Group** blade, select **Create** to create the group.</span><span class="sxs-lookup"><span data-stu-id="226c3-129">On the **Group** blade, select **Create** to create the group.</span></span>

## <a name="assign-licenses"></a><span data-ttu-id="226c3-130">Assign licenses</span><span class="sxs-lookup"><span data-stu-id="226c3-130">Assign licenses</span></span>

<span data-ttu-id="226c3-131">Now that you have your new group, you can apply the licenses that these partner users need.</span><span class="sxs-lookup"><span data-stu-id="226c3-131">Now that you have your new group, you can apply the licenses that these partner users need.</span></span>

1. <span data-ttu-id="226c3-132">In Azure AD, select **Licenses**, select one or more licenses, and then select **Assign**.</span><span class="sxs-lookup"><span data-stu-id="226c3-132">In Azure AD, select **Licenses**, select one or more licenses, and then select **Assign**.</span></span>
2. <span data-ttu-id="226c3-133">Select **Users and groups**, and select the **Guest users Contoso** group, and save your changes.</span><span class="sxs-lookup"><span data-stu-id="226c3-133">Select **Users and groups**, and select the **Guest users Contoso** group, and save your changes.</span></span>
3. <span data-ttu-id="226c3-134">**Assignment options** allow you to turn on or off the service plans included the licenses that you selected.</span><span class="sxs-lookup"><span data-stu-id="226c3-134">**Assignment options** allow you to turn on or off the service plans included the licenses that you selected.</span></span> <span data-ttu-id="226c3-135">When you make a change, be sure to click **OK** to save your changes.</span><span class="sxs-lookup"><span data-stu-id="226c3-135">When you make a change, be sure to click **OK** to save your changes.</span></span>
4. <span data-ttu-id="226c3-136">To complete the assignment, on the **Assign license** pane, click **Assign** at the bottom of the pane.</span><span class="sxs-lookup"><span data-stu-id="226c3-136">To complete the assignment, on the **Assign license** pane, click **Assign** at the bottom of the pane.</span></span>

## <a name="remove-guests-from-all-users-group"></a><span data-ttu-id="226c3-137">Remove guests from All users group</span><span class="sxs-lookup"><span data-stu-id="226c3-137">Remove guests from All users group</span></span>

<span data-ttu-id="226c3-138">Perhaps your ultimate administrative plan is to assign all of your guest users to their own groups by company.</span><span class="sxs-lookup"><span data-stu-id="226c3-138">Perhaps your ultimate administrative plan is to assign all of your guest users to their own groups by company.</span></span> <span data-ttu-id="226c3-139">You can also now change the **All users** group so that it is reserved for only members users in your tenant.</span><span class="sxs-lookup"><span data-stu-id="226c3-139">You can also now change the **All users** group so that it is reserved for only members users in your tenant.</span></span> <span data-ttu-id="226c3-140">Then you can use it to assign apps and licenses that are specific to your home organization.</span><span class="sxs-lookup"><span data-stu-id="226c3-140">Then you can use it to assign apps and licenses that are specific to your home organization.</span></span>

   ![Change All users group to members only](./media/groups-dynamic-tutorial/all-users-edit.png)

## <a name="clean-up-resources"></a><span data-ttu-id="226c3-142">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="226c3-142">Clean up resources</span></span>

<span data-ttu-id="226c3-143">**To remove the guest users group**</span><span class="sxs-lookup"><span data-stu-id="226c3-143">**To remove the guest users group**</span></span>

1. <span data-ttu-id="226c3-144">Sign in to the [Azure portal](https://portal.azure.com) with an account that is the Global Administrator for your tenant.</span><span class="sxs-lookup"><span data-stu-id="226c3-144">Sign in to the [Azure portal](https://portal.azure.com) with an account that is the Global Administrator for your tenant.</span></span>
2. <span data-ttu-id="226c3-145">Select **Azure Active Directory** > **Groups**.</span><span class="sxs-lookup"><span data-stu-id="226c3-145">Select **Azure Active Directory** > **Groups**.</span></span> <span data-ttu-id="226c3-146">Select the **Guest users Contoso** group, select the ellipsis (...), and then select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="226c3-146">Select the **Guest users Contoso** group, select the ellipsis (...), and then select **Delete**.</span></span> <span data-ttu-id="226c3-147">When you delete the group, any assigned licenses are removed.</span><span class="sxs-lookup"><span data-stu-id="226c3-147">When you delete the group, any assigned licenses are removed.</span></span>

<span data-ttu-id="226c3-148">**To restore the All Users group**</span><span class="sxs-lookup"><span data-stu-id="226c3-148">**To restore the All Users group**</span></span>
1. <span data-ttu-id="226c3-149">Select **Azure Active Directory** > **Groups**.</span><span class="sxs-lookup"><span data-stu-id="226c3-149">Select **Azure Active Directory** > **Groups**.</span></span> <span data-ttu-id="226c3-150">Select the name of the **All users** group to open the group.</span><span class="sxs-lookup"><span data-stu-id="226c3-150">Select the name of the **All users** group to open the group.</span></span>
1. <span data-ttu-id="226c3-151">Select **Dynamic membership rules**, clear all the text in the rule, and select **Save**.</span><span class="sxs-lookup"><span data-stu-id="226c3-151">Select **Dynamic membership rules**, clear all the text in the rule, and select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="226c3-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="226c3-152">Next steps</span></span>

<span data-ttu-id="226c3-153">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="226c3-153">In this tutorial, you learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="226c3-154">Create a group of guest users</span><span class="sxs-lookup"><span data-stu-id="226c3-154">Create a group of guest users</span></span>
> * <span data-ttu-id="226c3-155">Assign licenses to your new group</span><span class="sxs-lookup"><span data-stu-id="226c3-155">Assign licenses to your new group</span></span>
> * <span data-ttu-id="226c3-156">Change All users group to members only</span><span class="sxs-lookup"><span data-stu-id="226c3-156">Change All users group to members only</span></span>

<span data-ttu-id="226c3-157">Advance to the next article to learn more group-based licensing basics</span><span class="sxs-lookup"><span data-stu-id="226c3-157">Advance to the next article to learn more group-based licensing basics</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="226c3-158">Group licensing basics</span><span class="sxs-lookup"><span data-stu-id="226c3-158">Group licensing basics</span></span>](../fundamentals/active-directory-licensing-whatis-azure-portal.md)



