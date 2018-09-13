---
title: Azure Active Directory group-based licensing additional scenarios | Microsoft Docs
description: More scenarios for Azure Active Directory group-based licensing
services: active-directory
keywords: Azure AD licensing
documentationcenter: ''
author: curtand
manager: femila
editor: ''
ms.assetid: ''
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/20/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bae5a339f5ea11adc4481311b297bec38dc5a740
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550397"
---
# <a name="scenarios-limitations-and-known-issues-with-using-groups-to-manage-licensing-in-azure-active-directory"></a><span data-ttu-id="6b1ba-104">Scenarios, limitations, and known issues with using groups to manage licensing in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6b1ba-104">Scenarios, limitations, and known issues with using groups to manage licensing in Azure Active Directory</span></span>

<span data-ttu-id="6b1ba-105">Use the following information and examples to gain a more advanced understanding of Azure Active Directory (Azure AD) group-based licensing.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-105">Use the following information and examples to gain a more advanced understanding of Azure Active Directory (Azure AD) group-based licensing.</span></span>

## <a name="use-group-based-licensing-with-dynamic-groups"></a><span data-ttu-id="6b1ba-106">Use group-based licensing with dynamic groups</span><span class="sxs-lookup"><span data-stu-id="6b1ba-106">Use group-based licensing with dynamic groups</span></span>

<span data-ttu-id="6b1ba-107">You can use group-based licensing with any security group, which means it can be combined with Azure AD dynamic groups.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-107">You can use group-based licensing with any security group, which means it can be combined with Azure AD dynamic groups.</span></span> <span data-ttu-id="6b1ba-108">Dynamic groups run rules against user object attributes to automatically add and remove users from groups.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-108">Dynamic groups run rules against user object attributes to automatically add and remove users from groups.</span></span>

<span data-ttu-id="6b1ba-109">For example, you could create multiple dynamic groups, one per each set of products you want to assign to users.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-109">For example, you could create multiple dynamic groups, one per each set of products you want to assign to users.</span></span> <span data-ttu-id="6b1ba-110">Each group contains a rule looking at a specific attribute on a user, describing which set of licenses they should receive.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-110">Each group contains a rule looking at a specific attribute on a user, describing which set of licenses they should receive.</span></span> <span data-ttu-id="6b1ba-111">You can assign the attribute on-premises and sync it with Azure AD, or you can manage the attribute directly in the cloud.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-111">You can assign the attribute on-premises and sync it with Azure AD, or you can manage the attribute directly in the cloud.</span></span>

<span data-ttu-id="6b1ba-112">When you specify the attribute, the user is added to one or more of these dynamic licensing groups.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-112">When you specify the attribute, the user is added to one or more of these dynamic licensing groups.</span></span> <span data-ttu-id="6b1ba-113">Licenses are assigned to the user shortly after that.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-113">Licenses are assigned to the user shortly after that.</span></span> <span data-ttu-id="6b1ba-114">When the attribute is removed, the user leaves the groups and the licenses are removed.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-114">When the attribute is removed, the user leaves the groups and the licenses are removed.</span></span>

### <a name="example"></a><span data-ttu-id="6b1ba-115">Example</span><span class="sxs-lookup"><span data-stu-id="6b1ba-115">Example</span></span>

<span data-ttu-id="6b1ba-116">Consider an on-premises identity management solution that decides which users should have access to what Microsoft web services.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-116">Consider an on-premises identity management solution that decides which users should have access to what Microsoft web services.</span></span> <span data-ttu-id="6b1ba-117">It uses **extensionAttribute1** to store a string value representing the licenses the user should have.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-117">It uses **extensionAttribute1** to store a string value representing the licenses the user should have.</span></span> <span data-ttu-id="6b1ba-118">Azure AD Connect syncs it with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-118">Azure AD Connect syncs it with Azure AD.</span></span>

<span data-ttu-id="6b1ba-119">For this example, the goal is to distribute Office 365 Enterprise E5 and Enterprise Mobility + Security licenses to users.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-119">For this example, the goal is to distribute Office 365 Enterprise E5 and Enterprise Mobility + Security licenses to users.</span></span> <span data-ttu-id="6b1ba-120">In Azure AD, create two dynamic groups, one for each product.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-120">In Azure AD, create two dynamic groups, one for each product.</span></span> <span data-ttu-id="6b1ba-121">This is because some users may need one of the products, but not the other.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-121">This is because some users may need one of the products, but not the other.</span></span> <span data-ttu-id="6b1ba-122">Then specify the dynamic membership rule and license settings on each group.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-122">Then specify the dynamic membership rule and license settings on each group.</span></span> <span data-ttu-id="6b1ba-123">Here's what they look like:</span><span class="sxs-lookup"><span data-stu-id="6b1ba-123">Here's what they look like:</span></span>

#### <a name="office-365-enterprise-e5-base-services"></a><span data-ttu-id="6b1ba-124">Office 365 Enterprise E5: base services</span><span class="sxs-lookup"><span data-stu-id="6b1ba-124">Office 365 Enterprise E5: base services</span></span>

![Screenshot of Office 365 Enterprise E5 base services](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-licensing-group-advanced/o365-e5-base-services.png)

#### <a name="enterprise-mobility--security-licensed-users"></a><span data-ttu-id="6b1ba-126">Enterprise Mobility + Security: licensed users</span><span class="sxs-lookup"><span data-stu-id="6b1ba-126">Enterprise Mobility + Security: licensed users</span></span>

![Screenshot of Enterprise Mobility + Security licensed users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-licensing-group-advanced/o365-e5-licensed-users.png)

<span data-ttu-id="6b1ba-128">For this example, modify one user and set their extensionAttribute1 to the value of `EMS;E5_baseservices;`.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-128">For this example, modify one user and set their extensionAttribute1 to the value of `EMS;E5_baseservices;`.</span></span> <span data-ttu-id="6b1ba-129">This is because you want this user to have both licenses.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-129">This is because you want this user to have both licenses.</span></span> <span data-ttu-id="6b1ba-130">Note that you can make this modification on-premises.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-130">Note that you can make this modification on-premises.</span></span> <span data-ttu-id="6b1ba-131">After the change syncs with the cloud, the user is automatically added to both groups, and licenses are assigned.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-131">After the change syncs with the cloud, the user is automatically added to both groups, and licenses are assigned.</span></span>

![Screenshot showing how to set the user's extensionAttribute1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-licensing-group-advanced/user-set-extensionAttribute1.png)

### <a name="modify-a-dynamic-group-membership-rule"></a><span data-ttu-id="6b1ba-133">Modify a dynamic group membership rule</span><span class="sxs-lookup"><span data-stu-id="6b1ba-133">Modify a dynamic group membership rule</span></span>

<span data-ttu-id="6b1ba-134">Use caution when modifying an existing group’s membership rule.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-134">Use caution when modifying an existing group’s membership rule.</span></span> <span data-ttu-id="6b1ba-135">When a rule is changed, all users are removed from the group.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-135">When a rule is changed, all users are removed from the group.</span></span> <span data-ttu-id="6b1ba-136">The rule is evaluated, and then users are added to the group based on the new conditions.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-136">The rule is evaluated, and then users are added to the group based on the new conditions.</span></span>

<span data-ttu-id="6b1ba-137">If the group has licenses assigned, all users have those licenses removed during the process.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-137">If the group has licenses assigned, all users have those licenses removed during the process.</span></span> <span data-ttu-id="6b1ba-138">New licenses are applied only after the new rule is evaluated and users are added back.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-138">New licenses are applied only after the new rule is evaluated and users are added back.</span></span> <span data-ttu-id="6b1ba-139">This means that users might experience loss of service, or in some cases, loss of data.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-139">This means that users might experience loss of service, or in some cases, loss of data.</span></span>

<span data-ttu-id="6b1ba-140">It's better not to change the membership rule on a group used for license assignment.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-140">It's better not to change the membership rule on a group used for license assignment.</span></span> <span data-ttu-id="6b1ba-141">Instead, create a new group with the new rule and specify the same license settings as on the original group.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-141">Instead, create a new group with the new rule and specify the same license settings as on the original group.</span></span> <span data-ttu-id="6b1ba-142">Wait until members have been added and licenses have been applied to all users.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-142">Wait until members have been added and licenses have been applied to all users.</span></span> <span data-ttu-id="6b1ba-143">Only then can you delete the original group.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-143">Only then can you delete the original group.</span></span> <span data-ttu-id="6b1ba-144">This approach ensures a safe, staged transition to the new membership rule, without any loss of access or data for users.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-144">This approach ensures a safe, staged transition to the new membership rule, without any loss of access or data for users.</span></span>


## <a name="multiple-groups-and-multiple-licenses"></a><span data-ttu-id="6b1ba-145">Multiple groups and multiple licenses</span><span class="sxs-lookup"><span data-stu-id="6b1ba-145">Multiple groups and multiple licenses</span></span>

<span data-ttu-id="6b1ba-146">A user can be a member of multiple groups with licenses.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-146">A user can be a member of multiple groups with licenses.</span></span> <span data-ttu-id="6b1ba-147">Here are some things to consider:</span><span class="sxs-lookup"><span data-stu-id="6b1ba-147">Here are some things to consider:</span></span>

- <span data-ttu-id="6b1ba-148">Multiple licenses for the same product can overlap, and result in all of the enabled services being applied to the user.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-148">Multiple licenses for the same product can overlap, and result in all of the enabled services being applied to the user.</span></span> <span data-ttu-id="6b1ba-149">The following example shows two licensing groups: *E3 base services* contains the foundation services to deploy first, to all users.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-149">The following example shows two licensing groups: *E3 base services* contains the foundation services to deploy first, to all users.</span></span> <span data-ttu-id="6b1ba-150">And *E3 extended services* contains additional services (Sway and Planner) to deploy only to some users.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-150">And *E3 extended services* contains additional services (Sway and Planner) to deploy only to some users.</span></span> <span data-ttu-id="6b1ba-151">Note that Yammer remains disabled for future deployment.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-151">Note that Yammer remains disabled for future deployment.</span></span> <span data-ttu-id="6b1ba-152">In this example, the user was added to both groups:</span><span class="sxs-lookup"><span data-stu-id="6b1ba-152">In this example, the user was added to both groups:</span></span>

  ![Screenshot of enabled services](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-licensing-group-advanced/view-enabled-services.png)

  <span data-ttu-id="6b1ba-154">As a result, the user has 7 of the 12 services in the product enabled, while using only one license for this product.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-154">As a result, the user has 7 of the 12 services in the product enabled, while using only one license for this product.</span></span>

- <span data-ttu-id="6b1ba-155">Selecting the *E3* license shows more details, including information about which groups caused what services to be enabled for the user.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-155">Selecting the *E3* license shows more details, including information about which groups caused what services to be enabled for the user.</span></span>

  ![Screenshot of enabled services by group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-licensing-group-advanced/view-enabled-service-by-group.png)

## <a name="direct-licenses-coexist-with-group-licenses"></a><span data-ttu-id="6b1ba-157">Direct licenses coexist with group licenses</span><span class="sxs-lookup"><span data-stu-id="6b1ba-157">Direct licenses coexist with group licenses</span></span>

<span data-ttu-id="6b1ba-158">When a user inherits a license from a group, it is not possible to remove or modify that license assignment directly on the user object.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-158">When a user inherits a license from a group, it is not possible to remove or modify that license assignment directly on the user object.</span></span> <span data-ttu-id="6b1ba-159">Instead, any changes must be made in the group and then propagated by the system to all users.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-159">Instead, any changes must be made in the group and then propagated by the system to all users.</span></span>

<span data-ttu-id="6b1ba-160">It is possible, however, to assign the same product license directly to the user, in addition to the inherited license.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-160">It is possible, however, to assign the same product license directly to the user, in addition to the inherited license.</span></span> <span data-ttu-id="6b1ba-161">This may be used, for example, to enable additional services from the product just for one user, without affecting other users.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-161">This may be used, for example, to enable additional services from the product just for one user, without affecting other users.</span></span>

<span data-ttu-id="6b1ba-162">Directly assigned licenses can be removed, but that won’t affect the inherited license.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-162">Directly assigned licenses can be removed, but that won’t affect the inherited license.</span></span> <span data-ttu-id="6b1ba-163">For example, consider the following user, who inherits an Office 365 Enterprise E3 license from a group.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-163">For example, consider the following user, who inherits an Office 365 Enterprise E3 license from a group.</span></span>

1. <span data-ttu-id="6b1ba-164">Initially, the user inherits the license only from the *E3 basic services* group.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-164">Initially, the user inherits the license only from the *E3 basic services* group.</span></span> <span data-ttu-id="6b1ba-165">This enables 4 service plans, as shown in the following image.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-165">This enables 4 service plans, as shown in the following image.</span></span>

  ![Screenshot of E3 group enabled services](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-licensing-group-advanced/e3-group-enabled-services.png)

2. <span data-ttu-id="6b1ba-167">By clicking **Assign**, you can directly assign an E3 license to the user.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-167">By clicking **Assign**, you can directly assign an E3 license to the user.</span></span> <span data-ttu-id="6b1ba-168">In this case, you are going to disable all service plans except Yammer Enterprise.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-168">In this case, you are going to disable all service plans except Yammer Enterprise.</span></span>

  ![Screenshot of how to assign a license directly to a user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-licensing-group-advanced/assign-license-to-user.png)

3. <span data-ttu-id="6b1ba-170">As a result, the user still uses only one license of the E3 product.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-170">As a result, the user still uses only one license of the E3 product.</span></span> <span data-ttu-id="6b1ba-171">But the direct assignment enables the Yammer Enterprise service for that user only.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-171">But the direct assignment enables the Yammer Enterprise service for that user only.</span></span> <span data-ttu-id="6b1ba-172">The following image shows which services are enabled by the group membership versus the direct assignment.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-172">The following image shows which services are enabled by the group membership versus the direct assignment.</span></span>

  ![Screenshot of inherited versus direct assignment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-licensing-group-advanced/direct-vs-inherited-assignment.png)

4. <span data-ttu-id="6b1ba-174">When you use direct assignment, the following operations are allowed:</span><span class="sxs-lookup"><span data-stu-id="6b1ba-174">When you use direct assignment, the following operations are allowed:</span></span>

  <span data-ttu-id="6b1ba-175">a.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-175">a.</span></span> <span data-ttu-id="6b1ba-176">Yammer Enterprise can be turned off on the user object directly.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-176">Yammer Enterprise can be turned off on the user object directly.</span></span> <span data-ttu-id="6b1ba-177">Notice that the **On/Off** toggle is enabled for this service, as opposed to the other service toggles.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-177">Notice that the **On/Off** toggle is enabled for this service, as opposed to the other service toggles.</span></span> <span data-ttu-id="6b1ba-178">This is because this service is enabled directly on the user, and thus can be modified.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-178">This is because this service is enabled directly on the user, and thus can be modified.</span></span>

  <span data-ttu-id="6b1ba-179">b.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-179">b.</span></span> <span data-ttu-id="6b1ba-180">Additional services can be enabled as well, as part of the directly assigned license.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-180">Additional services can be enabled as well, as part of the directly assigned license.</span></span>

  <span data-ttu-id="6b1ba-181">c.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-181">c.</span></span> <span data-ttu-id="6b1ba-182">The **Remove** button can be used to remove the direct license from the user.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-182">The **Remove** button can be used to remove the direct license from the user.</span></span> <span data-ttu-id="6b1ba-183">You can see that the user now only has the inherited group license and only the original services remain enabled.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-183">You can see that the user now only has the inherited group license and only the original services remain enabled.</span></span>

    ![Screenshot showing how to remove direct assignment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-licensing-group-advanced/remove-direct-license.png)

## <a name="usage-location"></a><span data-ttu-id="6b1ba-185">Usage location</span><span class="sxs-lookup"><span data-stu-id="6b1ba-185">Usage location</span></span>

<span data-ttu-id="6b1ba-186">Some Microsoft services are not available in all locations.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-186">Some Microsoft services are not available in all locations.</span></span> <span data-ttu-id="6b1ba-187">Before a license can be assigned to a user, the administrator has to specify the **Usage location** property on the user.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-187">Before a license can be assigned to a user, the administrator has to specify the **Usage location** property on the user.</span></span> <span data-ttu-id="6b1ba-188">This can be done in [the Azure portal](https://portal.azure.com), under **User** &gt; **Profile** &gt; **Settings**.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-188">This can be done in [the Azure portal](https://portal.azure.com), under **User** &gt; **Profile** &gt; **Settings**.</span></span>

<span data-ttu-id="6b1ba-189">For group license assignment, any users without a usage location specified inherit the location of the directory.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-189">For group license assignment, any users without a usage location specified inherit the location of the directory.</span></span> <span data-ttu-id="6b1ba-190">If you have users in different locations, make sure to reflect that correctly in your user objects before adding users to groups with licenses.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-190">If you have users in different locations, make sure to reflect that correctly in your user objects before adding users to groups with licenses.</span></span>

## <a name="use-powershell-to-see-who-has-inherited-and-direct-licenses"></a><span data-ttu-id="6b1ba-191">Use PowerShell to see who has inherited and direct licenses</span><span class="sxs-lookup"><span data-stu-id="6b1ba-191">Use PowerShell to see who has inherited and direct licenses</span></span>

<span data-ttu-id="6b1ba-192">During the preview period of an Azure AD release, PowerShell cannot be used to fully control group license assignments.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-192">During the preview period of an Azure AD release, PowerShell cannot be used to fully control group license assignments.</span></span> <span data-ttu-id="6b1ba-193">However, it can be used to discover basic information about user state, and to determine if licenses are inherited from a group or assigned directly.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-193">However, it can be used to discover basic information about user state, and to determine if licenses are inherited from a group or assigned directly.</span></span> <span data-ttu-id="6b1ba-194">The following code sample shows how an admin can produce a basic report about license assignments.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-194">The following code sample shows how an admin can produce a basic report about license assignments.</span></span>

1. <span data-ttu-id="6b1ba-195">Run the `connect-msolservice` cmdlet to authenticate and connect to your tenant.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-195">Run the `connect-msolservice` cmdlet to authenticate and connect to your tenant.</span></span>

2. <span data-ttu-id="6b1ba-196">`Get-MsolAccountSku` can be used to discover all provisioned product licenses in the tenant.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-196">`Get-MsolAccountSku` can be used to discover all provisioned product licenses in the tenant.</span></span>

  ![Screenshot of the Get-Msolaccountsku cmdlet](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-licensing-group-advanced/get-msolaccountsku-cmdlet.png)

3. <span data-ttu-id="6b1ba-198">In this example, you want to find out which users have the Enterprise Mobility + Security license assigned directly, from a group, or both.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-198">In this example, you want to find out which users have the Enterprise Mobility + Security license assigned directly, from a group, or both.</span></span> <span data-ttu-id="6b1ba-199">You can use the following PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-199">You can use the following PowerShell script.</span></span>
  
  ```
  #Returns TRUE if the user has the license assigned directly
  function UserHasLicenseAssignedDirectly
  {
      Param([Microsoft.Online.Administration.User]$user, [string]$skuId)
      foreach($license in $user.Licenses)
      {
          #we look for the specific license SKU in all licenses assigned to the user
          if ($license.AccountSkuId -ieq $skuId)
          {
              #GroupsAssigningLicense contains a collection of IDs of objects assigning the license
              #This could be a group object or a user object (contrary to what the name suggests)
              #If the collection is empty, this means the license is assigned directly. This is the case for users who have never been licensed via groups in the past
              if ($license.GroupsAssigningLicense.Count -eq 0)
              {
                  return $true
              }
              #If the collection contains the ID of the user object, this means the license is assigned directly
              #Note: the license may also be assigned through one or more groups in addition to being assigned directly
              foreach ($assignmentSource in $license.GroupsAssigningLicense)
              {
                  if ($assignmentSource -ieq $user.ObjectId)
                  {
                      return $true
                  }
              }
              return $false
          }
      }
      return $false
  }
  #Returns TRUE if the user is inheriting the license from a group
  function UserHasLicenseAssignedFromGroup
  {
    Param([Microsoft.Online.Administration.User]$user, [string]$skuId)
     foreach($license in $user.Licenses
     {
        #we look for the specific license SKU in all licenses assigned to the user
        if ($license.AccountSkuId -ieq $skuId)
        {
          #GroupsAssigningLicense contains a collection of IDs of objects assigning the license
          #This could be a group object or a user object (contrary to what the name suggests)
            foreach ($assignmentSource in $license.GroupsAssigningLicense)
          {
                  #If the collection contains at least one ID not matching the user ID this means that the license is inherited from a group.
                  #Note: the license may also be assigned directly in addition to being inherited
                  if ($assignmentSource -ine $user.ObjectId)

            {
                      return $true
            }
          }
              return $false
        }
      }
      return $false
  }
  ```

4. <span data-ttu-id="6b1ba-200">The rest of the script gets all users, and runs these functions on each user.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-200">The rest of the script gets all users, and runs these functions on each user.</span></span> <span data-ttu-id="6b1ba-201">Then it formats the output into a table.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-201">Then it formats the output into a table.</span></span>
    
  ```
  #the license SKU we are interested in
  $skuId = "reseller-account:EMS"
  #find all users that have the SKU license assigned
  Get-MsolUser -All | where {$_.isLicensed -eq $true -and $_.Licenses.AccountSKUID -eq $skuId} | select `
      ObjectId, `
      @{Name="SkuId";Expression={$skuId}}, `
      @{Name="AssignedDirectly";Expression={(UserHasLicenseAssignedDirectly $_ $skuId)}}, `
      @{Name="AssignedFromGroup";Expression={(UserHasLicenseAssignedFromGroup $_ $skuId)}}
  ```

5. <span data-ttu-id="6b1ba-202">The output of the complete script appears as the following:</span><span class="sxs-lookup"><span data-stu-id="6b1ba-202">The output of the complete script appears as the following:</span></span>

  ![Screenshot of PowerShell script output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-licensing-group-advanced/powershell-script-output.png)

## <a name="limitations-and-known-issues"></a><span data-ttu-id="6b1ba-204">Limitations and known issues</span><span class="sxs-lookup"><span data-stu-id="6b1ba-204">Limitations and known issues</span></span>

<span data-ttu-id="6b1ba-205">If you use group-based licensing, it's a good idea to familiarize yourself with the following list of limitations and known issues.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-205">If you use group-based licensing, it's a good idea to familiarize yourself with the following list of limitations and known issues.</span></span>

- <span data-ttu-id="6b1ba-206">Group-based licensing currently does not support “nested groups” (groups that contain other groups).</span><span class="sxs-lookup"><span data-stu-id="6b1ba-206">Group-based licensing currently does not support “nested groups” (groups that contain other groups).</span></span> <span data-ttu-id="6b1ba-207">If you apply a license to a nested group, only the immediate first-level user members of the group have the licenses applied.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-207">If you apply a license to a nested group, only the immediate first-level user members of the group have the licenses applied.</span></span>

- <span data-ttu-id="6b1ba-208">One or more of the licenses could not be modified because they are inherited from a group membership.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-208">One or more of the licenses could not be modified because they are inherited from a group membership.</span></span> <span data-ttu-id="6b1ba-209">To view or modify group based licenses visit the Azure admin portal.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-209">To view or modify group based licenses visit the Azure admin portal.</span></span>

- <span data-ttu-id="6b1ba-210">The [Office 365 admin portal](https://portal.office.com ) does not currently support group-based licensing.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-210">The [Office 365 admin portal](https://portal.office.com ) does not currently support group-based licensing.</span></span> <span data-ttu-id="6b1ba-211">If a user inherits a license from a group, this license appears in the Office admin portal as a regular user license.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-211">If a user inherits a license from a group, this license appears in the Office admin portal as a regular user license.</span></span> <span data-ttu-id="6b1ba-212">If you try to modify that license (for example, to disable a service in the license), or try to remove the license, the portal returns an error message.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-212">If you try to modify that license (for example, to disable a service in the license), or try to remove the license, the portal returns an error message.</span></span> <span data-ttu-id="6b1ba-213">Inherited group licenses cannot be modified directly on a user.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-213">Inherited group licenses cannot be modified directly on a user.</span></span>

- <span data-ttu-id="6b1ba-214">When a user is removed from a group and loses the license, the service plans from that license (for example, Exchange Online or SharePoint Online) are set to a “suspended” state.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-214">When a user is removed from a group and loses the license, the service plans from that license (for example, Exchange Online or SharePoint Online) are set to a “suspended” state.</span></span> <span data-ttu-id="6b1ba-215">The service plans are not set to a final, disabled state.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-215">The service plans are not set to a final, disabled state.</span></span> <span data-ttu-id="6b1ba-216">This is a precaution to avoid accidental removal of user data, if an admin makes a mistake in group membership management.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-216">This is a precaution to avoid accidental removal of user data, if an admin makes a mistake in group membership management.</span></span>

- <span data-ttu-id="6b1ba-217">When licenses are assigned or modified for an extremely large group (for example, 100,000 users), this could impact performance.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-217">When licenses are assigned or modified for an extremely large group (for example, 100,000 users), this could impact performance.</span></span> <span data-ttu-id="6b1ba-218">Specifically, the volume of changes generated by Azure AD automation might negatively impact the performance of your directory synchronization between Azure AD and on-premises systems.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-218">Specifically, the volume of changes generated by Azure AD automation might negatively impact the performance of your directory synchronization between Azure AD and on-premises systems.</span></span> <span data-ttu-id="6b1ba-219">This could cause delays in directory sync in your environment.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-219">This could cause delays in directory sync in your environment.</span></span>

- <span data-ttu-id="6b1ba-220">License management automation does not automatically react to all types of changes in the environment.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-220">License management automation does not automatically react to all types of changes in the environment.</span></span> <span data-ttu-id="6b1ba-221">For example, you might have run out of licenses, causing some users to be in an error state.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-221">For example, you might have run out of licenses, causing some users to be in an error state.</span></span> <span data-ttu-id="6b1ba-222">To free up the available seat count, you can remove some directly assigned licenses from other users.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-222">To free up the available seat count, you can remove some directly assigned licenses from other users.</span></span> <span data-ttu-id="6b1ba-223">However, the system does not automatically react to this change and fix users in that error state.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-223">However, the system does not automatically react to this change and fix users in that error state.</span></span>

  <span data-ttu-id="6b1ba-224">As a workaround to these types of limitations, you can go to the **Group** blade in Azure AD, and click **Reprocess**.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-224">As a workaround to these types of limitations, you can go to the **Group** blade in Azure AD, and click **Reprocess**.</span></span> <span data-ttu-id="6b1ba-225">This processes all users in that group and resolves the error states, if possible.</span><span class="sxs-lookup"><span data-stu-id="6b1ba-225">This processes all users in that group and resolves the error states, if possible.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b1ba-226">Next steps</span><span class="sxs-lookup"><span data-stu-id="6b1ba-226">Next steps</span></span>

<span data-ttu-id="6b1ba-227">To learn more about other scenarios for license management through group-based licensing, see:</span><span class="sxs-lookup"><span data-stu-id="6b1ba-227">To learn more about other scenarios for license management through group-based licensing, see:</span></span>

* [<span data-ttu-id="6b1ba-228">What is group-based licensing in Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6b1ba-228">What is group-based licensing in Azure Active Directory?</span></span>](active-directory-licensing-whatis-azure-portal.md)
* [<span data-ttu-id="6b1ba-229">Assigning licenses to a group in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6b1ba-229">Assigning licenses to a group in Azure Active Directory</span></span>](active-directory-licensing-group-assignment-azure-portal.md)
* [<span data-ttu-id="6b1ba-230">Identifying and resolving license problems for a group in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6b1ba-230">Identifying and resolving license problems for a group in Azure Active Directory</span></span>](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [<span data-ttu-id="6b1ba-231">How to migrate individual licensed users to group-based licensing in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6b1ba-231">How to migrate individual licensed users to group-based licensing in Azure Active Directory</span></span>](active-directory-licensing-group-migration-azure-portal.md)











