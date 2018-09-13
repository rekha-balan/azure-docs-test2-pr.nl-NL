---
title: 'Tutorial: Configure Workday for Inbound Synchronization | Microsoft Docs'
description: Learn how to use Workday as source of identity data for Azure Active Directory.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 1a2c375a-1bb1-4a61-8115-5a69972c6ad6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/24/2017
ms.author: jeedes
ms.openlocfilehash: 135034fa0407fc4798a21cd8d5acebf1fd947131
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555975"
---
# <a name="tutorial-configure-workday-for-inbound-synchronization"></a><span data-ttu-id="9ab62-103">Tutorial: Configure Workday for Inbound Synchronization</span><span class="sxs-lookup"><span data-stu-id="9ab62-103">Tutorial: Configure Workday for Inbound Synchronization</span></span>
<span data-ttu-id="9ab62-104">The objective of this tutorial is to show you the steps you need to perform in Workday and Azure AD to import people from Workday to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9ab62-104">The objective of this tutorial is to show you the steps you need to perform in Workday and Azure AD to import people from Workday to Azure AD.</span></span> 

<span data-ttu-id="9ab62-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="9ab62-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="9ab62-106">A valid Azure AD Premium subscription</span><span class="sxs-lookup"><span data-stu-id="9ab62-106">A valid Azure AD Premium subscription</span></span>
* <span data-ttu-id="9ab62-107">A tenant in Workday</span><span class="sxs-lookup"><span data-stu-id="9ab62-107">A tenant in Workday</span></span>

<span data-ttu-id="9ab62-108">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="9ab62-108">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="9ab62-109">Enabling the application integration for Workday</span><span class="sxs-lookup"><span data-stu-id="9ab62-109">Enabling the application integration for Workday</span></span> 
2. <span data-ttu-id="9ab62-110">Creating an integration system user</span><span class="sxs-lookup"><span data-stu-id="9ab62-110">Creating an integration system user</span></span> 
3. <span data-ttu-id="9ab62-111">Creating a security group</span><span class="sxs-lookup"><span data-stu-id="9ab62-111">Creating a security group</span></span> 
4. <span data-ttu-id="9ab62-112">Assigning the integration system user to the security group</span><span class="sxs-lookup"><span data-stu-id="9ab62-112">Assigning the integration system user to the security group</span></span> 
5. <span data-ttu-id="9ab62-113">Configuring security group options</span><span class="sxs-lookup"><span data-stu-id="9ab62-113">Configuring security group options</span></span> 
6. <span data-ttu-id="9ab62-114">Activating security policy changes</span><span class="sxs-lookup"><span data-stu-id="9ab62-114">Activating security policy changes</span></span> 
7. <span data-ttu-id="9ab62-115">Configuring user import in Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ab62-115">Configuring user import in Azure AD</span></span> 

## <a name="enable-the-application-integration-for-workday"></a><span data-ttu-id="9ab62-116">Enable the application integration for Workday</span><span class="sxs-lookup"><span data-stu-id="9ab62-116">Enable the application integration for Workday</span></span>
<span data-ttu-id="9ab62-117">The objective of this section is to outline how to enable the application integration for Workday.</span><span class="sxs-lookup"><span data-stu-id="9ab62-117">The objective of this section is to outline how to enable the application integration for Workday.</span></span>

<span data-ttu-id="9ab62-118">**To enable the application integration for Workday:**</span><span class="sxs-lookup"><span data-stu-id="9ab62-118">**To enable the application integration for Workday:**</span></span>

1. <span data-ttu-id="9ab62-119">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9ab62-119">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="9ab62-120">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="9ab62-120">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="9ab62-121">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="9ab62-121">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="9ab62-122">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="9ab62-122">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="9ab62-123">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="9ab62-123">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="9ab62-124">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="9ab62-124">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="9ab62-125">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="9ab62-125">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="9ab62-126">In the search box, type **Workday**.</span><span class="sxs-lookup"><span data-stu-id="9ab62-126">In the search box, type **Workday**.</span></span>
   
   <span data-ttu-id="9ab62-127">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC701021.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="9ab62-127">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC701021.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="9ab62-128">In the results pane, select Workday, and then click Complete to add the application.</span><span class="sxs-lookup"><span data-stu-id="9ab62-128">In the results pane, select Workday, and then click Complete to add the application.</span></span>
   
   <span data-ttu-id="9ab62-129">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC701022.png "Application gallery")</span><span class="sxs-lookup"><span data-stu-id="9ab62-129">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC701022.png "Application gallery")</span></span>

## <a name="create-an-integration-system-user"></a><span data-ttu-id="9ab62-130">Create an integration system user</span><span class="sxs-lookup"><span data-stu-id="9ab62-130">Create an integration system user</span></span>

<span data-ttu-id="9ab62-131">**To create an integration system user:**</span><span class="sxs-lookup"><span data-stu-id="9ab62-131">**To create an integration system user:**</span></span>

1. <span data-ttu-id="9ab62-132">In the **Workday Workbench**, enter create user in the search box, and then click **Create Integration System User**.</span><span class="sxs-lookup"><span data-stu-id="9ab62-132">In the **Workday Workbench**, enter create user in the search box, and then click **Create Integration System User**.</span></span> 
   
    <span data-ttu-id="9ab62-133">![Create user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC750979.png "Create user")</span><span class="sxs-lookup"><span data-stu-id="9ab62-133">![Create user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC750979.png "Create user")</span></span>
2. <span data-ttu-id="9ab62-134">Complete the **Create Integration System User** task by supplying a user name and password for a new Integration System User.</span><span class="sxs-lookup"><span data-stu-id="9ab62-134">Complete the **Create Integration System User** task by supplying a user name and password for a new Integration System User.</span></span>  
 * <span data-ttu-id="9ab62-135">Leave the **Require New Password at Next Sign In** option unchecked, because this user will be logging on programmatically.</span><span class="sxs-lookup"><span data-stu-id="9ab62-135">Leave the **Require New Password at Next Sign In** option unchecked, because this user will be logging on programmatically.</span></span> 
 * <span data-ttu-id="9ab62-136">Leave the **Session Timeout Minutes** with its default value of 0, which will prevent the user’s sessions from timing out prematurely.</span><span class="sxs-lookup"><span data-stu-id="9ab62-136">Leave the **Session Timeout Minutes** with its default value of 0, which will prevent the user’s sessions from timing out prematurely.</span></span> 
   
    <span data-ttu-id="9ab62-137">![Create Integration System User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC750980.png "Create Integration System User")</span><span class="sxs-lookup"><span data-stu-id="9ab62-137">![Create Integration System User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC750980.png "Create Integration System User")</span></span>

## <a name="create-a-security-group"></a><span data-ttu-id="9ab62-138">Create a security group</span><span class="sxs-lookup"><span data-stu-id="9ab62-138">Create a security group</span></span>
<span data-ttu-id="9ab62-139">For the scenario outlined in this tutorial, you need to create an unconstrained integration system security group and assign the user to it.</span><span class="sxs-lookup"><span data-stu-id="9ab62-139">For the scenario outlined in this tutorial, you need to create an unconstrained integration system security group and assign the user to it.</span></span>

<span data-ttu-id="9ab62-140">**To create a security group:**</span><span class="sxs-lookup"><span data-stu-id="9ab62-140">**To create a security group:**</span></span>

1. <span data-ttu-id="9ab62-141">Enter create security group in the search box, and then click **Create Security Group**.</span><span class="sxs-lookup"><span data-stu-id="9ab62-141">Enter create security group in the search box, and then click **Create Security Group**.</span></span> 
   
    <span data-ttu-id="9ab62-142">![CreateSecurity Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC750981.png "CreateSecurity Group")</span><span class="sxs-lookup"><span data-stu-id="9ab62-142">![CreateSecurity Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC750981.png "CreateSecurity Group")</span></span>
2. <span data-ttu-id="9ab62-143">Complete the **Create Security Group** task.</span><span class="sxs-lookup"><span data-stu-id="9ab62-143">Complete the **Create Security Group** task.</span></span>  
3. <span data-ttu-id="9ab62-144">Select Integration System Security Group—Unconstrained from the **Type of Tenanted Security Group** dropdown.</span><span class="sxs-lookup"><span data-stu-id="9ab62-144">Select Integration System Security Group—Unconstrained from the **Type of Tenanted Security Group** dropdown.</span></span>
4. <span data-ttu-id="9ab62-145">Create a security group to which members will be explicitly added.</span><span class="sxs-lookup"><span data-stu-id="9ab62-145">Create a security group to which members will be explicitly added.</span></span> 
   
    <span data-ttu-id="9ab62-146">![CreateSecurity Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC750982.png "CreateSecurity Group")</span><span class="sxs-lookup"><span data-stu-id="9ab62-146">![CreateSecurity Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC750982.png "CreateSecurity Group")</span></span>

## <a name="assign-the-integration-system-user-to-the-security-group"></a><span data-ttu-id="9ab62-147">Assign the integration system user to the security group</span><span class="sxs-lookup"><span data-stu-id="9ab62-147">Assign the integration system user to the security group</span></span>

<span data-ttu-id="9ab62-148">**To assign the integration system user:**</span><span class="sxs-lookup"><span data-stu-id="9ab62-148">**To assign the integration system user:**</span></span>

1. <span data-ttu-id="9ab62-149">Enter edit security group in the search box, and then click **Edit Security Group**.</span><span class="sxs-lookup"><span data-stu-id="9ab62-149">Enter edit security group in the search box, and then click **Edit Security Group**.</span></span> 
   
    <span data-ttu-id="9ab62-150">![Edit Security Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC750983.png "Edit Security Group")</span><span class="sxs-lookup"><span data-stu-id="9ab62-150">![Edit Security Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC750983.png "Edit Security Group")</span></span>
2. <span data-ttu-id="9ab62-151">Search for, and select the new integration security group by name.</span><span class="sxs-lookup"><span data-stu-id="9ab62-151">Search for, and select the new integration security group by name.</span></span> 
   
    <span data-ttu-id="9ab62-152">![Edit Security Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC750984.png "Edit Security Group")</span><span class="sxs-lookup"><span data-stu-id="9ab62-152">![Edit Security Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC750984.png "Edit Security Group")</span></span>
3. <span data-ttu-id="9ab62-153">Add the new integration system user to the new security group.</span><span class="sxs-lookup"><span data-stu-id="9ab62-153">Add the new integration system user to the new security group.</span></span> 
   
    <span data-ttu-id="9ab62-154">![System Security Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC750985.png "System Security Group")</span><span class="sxs-lookup"><span data-stu-id="9ab62-154">![System Security Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC750985.png "System Security Group")</span></span>  

## <a name="configure-security-group-options"></a><span data-ttu-id="9ab62-155">Configure security group options</span><span class="sxs-lookup"><span data-stu-id="9ab62-155">Configure security group options</span></span>
<span data-ttu-id="9ab62-156">In this step, you grant to the new security group permissions for **Get** and **Put** operations on the objects secured by the following domain security policies:</span><span class="sxs-lookup"><span data-stu-id="9ab62-156">In this step, you grant to the new security group permissions for **Get** and **Put** operations on the objects secured by the following domain security policies:</span></span>

* <span data-ttu-id="9ab62-157">External Account Provisioning</span><span class="sxs-lookup"><span data-stu-id="9ab62-157">External Account Provisioning</span></span>
* <span data-ttu-id="9ab62-158">Worker Data: Public Worker Reports</span><span class="sxs-lookup"><span data-stu-id="9ab62-158">Worker Data: Public Worker Reports</span></span>
* <span data-ttu-id="9ab62-159">Worker Data: All Positions</span><span class="sxs-lookup"><span data-stu-id="9ab62-159">Worker Data: All Positions</span></span>
* <span data-ttu-id="9ab62-160">Worker Data: Current Staffing Information</span><span class="sxs-lookup"><span data-stu-id="9ab62-160">Worker Data: Current Staffing Information</span></span>
* <span data-ttu-id="9ab62-161">Worker Data: Business Title on Worker Profile</span><span class="sxs-lookup"><span data-stu-id="9ab62-161">Worker Data: Business Title on Worker Profile</span></span>

<span data-ttu-id="9ab62-162">**To configure security group options:**</span><span class="sxs-lookup"><span data-stu-id="9ab62-162">**To configure security group options:**</span></span>

1. <span data-ttu-id="9ab62-163">Enter domain security policies in the search box, and then click on the link **Domain Security Policies for Functional Area**.</span><span class="sxs-lookup"><span data-stu-id="9ab62-163">Enter domain security policies in the search box, and then click on the link **Domain Security Policies for Functional Area**.</span></span>  
   
    <span data-ttu-id="9ab62-164">![Domain Security Policies](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC750986.png "Domain Security Policies")</span><span class="sxs-lookup"><span data-stu-id="9ab62-164">![Domain Security Policies](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC750986.png "Domain Security Policies")</span></span>  
2. <span data-ttu-id="9ab62-165">Search for system and select the **System** functional area.</span><span class="sxs-lookup"><span data-stu-id="9ab62-165">Search for system and select the **System** functional area.</span></span>  <span data-ttu-id="9ab62-166">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="9ab62-166">Click **OK**.</span></span>  
   
    <span data-ttu-id="9ab62-167">![Domain Security Policies](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC750987.png "Domain Security Policies")</span><span class="sxs-lookup"><span data-stu-id="9ab62-167">![Domain Security Policies](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC750987.png "Domain Security Policies")</span></span>  
3. <span data-ttu-id="9ab62-168">In the list of security policies for the System functional area, expand **Security Administration** and select the domain security policy **External Account Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="9ab62-168">In the list of security policies for the System functional area, expand **Security Administration** and select the domain security policy **External Account Provisioning**.</span></span>  
   
    <span data-ttu-id="9ab62-169">![Domain Security Policies](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC750988.png "Domain Security Policies")</span><span class="sxs-lookup"><span data-stu-id="9ab62-169">![Domain Security Policies](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC750988.png "Domain Security Policies")</span></span>  
4. <span data-ttu-id="9ab62-170">Click **Edit Permissions**, and then, on the **Edit Permissions**dialog page, add the new security group to the list of security groups with **Get** and **Put** integration permissions.</span><span class="sxs-lookup"><span data-stu-id="9ab62-170">Click **Edit Permissions**, and then, on the **Edit Permissions**dialog page, add the new security group to the list of security groups with **Get** and **Put** integration permissions.</span></span> 
   
    <span data-ttu-id="9ab62-171">![Edit Permission](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC750989.png "Edit Permission")</span><span class="sxs-lookup"><span data-stu-id="9ab62-171">![Edit Permission](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC750989.png "Edit Permission")</span></span>  
5. <span data-ttu-id="9ab62-172">Repeat step 1 above to return to the screen for selecting functional areas, and this time, search for staffing, select the **Staffing functional area** and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="9ab62-172">Repeat step 1 above to return to the screen for selecting functional areas, and this time, search for staffing, select the **Staffing functional area** and click **OK**.</span></span>
   
    <span data-ttu-id="9ab62-173">![Domain Security Policies](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC750990.png "Domain Security Policies")</span><span class="sxs-lookup"><span data-stu-id="9ab62-173">![Domain Security Policies](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC750990.png "Domain Security Policies")</span></span>  
6. <span data-ttu-id="9ab62-174">In the list of security policies for the Staffing functional area, expand **Worker Data: Staffing** and repeat step 4 above for each of these remaining security policies:</span><span class="sxs-lookup"><span data-stu-id="9ab62-174">In the list of security policies for the Staffing functional area, expand **Worker Data: Staffing** and repeat step 4 above for each of these remaining security policies:</span></span>

   * <span data-ttu-id="9ab62-175">Worker Data: Public Worker Reports</span><span class="sxs-lookup"><span data-stu-id="9ab62-175">Worker Data: Public Worker Reports</span></span>
   * <span data-ttu-id="9ab62-176">Worker Data: All Positions</span><span class="sxs-lookup"><span data-stu-id="9ab62-176">Worker Data: All Positions</span></span>
   * <span data-ttu-id="9ab62-177">Worker Data: Current Staffing Information</span><span class="sxs-lookup"><span data-stu-id="9ab62-177">Worker Data: Current Staffing Information</span></span>
   * <span data-ttu-id="9ab62-178">Worker Data: Business Title on Worker Profile</span><span class="sxs-lookup"><span data-stu-id="9ab62-178">Worker Data: Business Title on Worker Profile</span></span>

    <span data-ttu-id="9ab62-179">![Domain Security Policies](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC750991.png "Domain Security Policies")</span><span class="sxs-lookup"><span data-stu-id="9ab62-179">![Domain Security Policies](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC750991.png "Domain Security Policies")</span></span>  
    
## <a name="activate-security-policy-changes"></a><span data-ttu-id="9ab62-180">Activate security policy changes</span><span class="sxs-lookup"><span data-stu-id="9ab62-180">Activate security policy changes</span></span>

<span data-ttu-id="9ab62-181">**To activate security policy changes:**</span><span class="sxs-lookup"><span data-stu-id="9ab62-181">**To activate security policy changes:**</span></span>

1. <span data-ttu-id="9ab62-182">Enter activate in the search box, and then click on the link **Activate Pending Security Policy Changes**.</span><span class="sxs-lookup"><span data-stu-id="9ab62-182">Enter activate in the search box, and then click on the link **Activate Pending Security Policy Changes**.</span></span> 
   
    <span data-ttu-id="9ab62-183">![Activate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC750992.png "Activate")</span><span class="sxs-lookup"><span data-stu-id="9ab62-183">![Activate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC750992.png "Activate")</span></span> 
2. <span data-ttu-id="9ab62-184">Begin the Activate Pending Security Policy Changes task by entering a comment for auditing purposes, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="9ab62-184">Begin the Activate Pending Security Policy Changes task by entering a comment for auditing purposes, and then click **OK**.</span></span> 
   
    <span data-ttu-id="9ab62-185">![Activate Pending Security](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC750993.png "Activate Pending Security")</span><span class="sxs-lookup"><span data-stu-id="9ab62-185">![Activate Pending Security](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC750993.png "Activate Pending Security")</span></span>   
3. <span data-ttu-id="9ab62-186">Complete the task on the next screen by checking the checkbox **Confirm**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="9ab62-186">Complete the task on the next screen by checking the checkbox **Confirm**, and then click **OK**.</span></span> 
   
    <span data-ttu-id="9ab62-187">![Activate Pending Security](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC750994.png "Activate Pending Security")</span><span class="sxs-lookup"><span data-stu-id="9ab62-187">![Activate Pending Security](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC750994.png "Activate Pending Security")</span></span>  

## <a name="configure-user-import-in-azure-ad"></a><span data-ttu-id="9ab62-188">Configure user import in Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ab62-188">Configure user import in Azure AD</span></span>
<span data-ttu-id="9ab62-189">The objective of this section is to outline how to configure Azure AD to import people from Workday.</span><span class="sxs-lookup"><span data-stu-id="9ab62-189">The objective of this section is to outline how to configure Azure AD to import people from Workday.</span></span>

<span data-ttu-id="9ab62-190">**To configure user import:**</span><span class="sxs-lookup"><span data-stu-id="9ab62-190">**To configure user import:**</span></span>

1. <span data-ttu-id="9ab62-191">On the **Workday** application integration page, click **Configure user import** to open the **Configure Provisioning** dialog.</span><span class="sxs-lookup"><span data-stu-id="9ab62-191">On the **Workday** application integration page, click **Configure user import** to open the **Configure Provisioning** dialog.</span></span>
2. <span data-ttu-id="9ab62-192">On the **Settings and admin credentials** page, perform the following steps, and then click **Next**:</span><span class="sxs-lookup"><span data-stu-id="9ab62-192">On the **Settings and admin credentials** page, perform the following steps, and then click **Next**:</span></span> 
   
    <span data-ttu-id="9ab62-193">![Settings and admin credentials](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC750995.png "Settings and admin credentials")</span><span class="sxs-lookup"><span data-stu-id="9ab62-193">![Settings and admin credentials](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC750995.png "Settings and admin credentials")</span></span>    
  1. <span data-ttu-id="9ab62-194">In the **Workday admin user name** textbox, type the name of the user you have created in the Creating an integration system user section.</span><span class="sxs-lookup"><span data-stu-id="9ab62-194">In the **Workday admin user name** textbox, type the name of the user you have created in the Creating an integration system user section.</span></span>
  2. <span data-ttu-id="9ab62-195">In the **Workday admin password** textbox, type the password of the user you have created in the Creating an integration system user section.</span><span class="sxs-lookup"><span data-stu-id="9ab62-195">In the **Workday admin password** textbox, type the password of the user you have created in the Creating an integration system user section.</span></span>
  3. <span data-ttu-id="9ab62-196">In the **Workday tenant URL** textbox, type the URL or your Workday tenant.</span><span class="sxs-lookup"><span data-stu-id="9ab62-196">In the **Workday tenant URL** textbox, type the URL or your Workday tenant.</span></span>
3. <span data-ttu-id="9ab62-197">On the **Test connection** page, click **Start test** to confirm connectivity, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="9ab62-197">On the **Test connection** page, click **Start test** to confirm connectivity, and then click **Next**.</span></span> 
   
    <span data-ttu-id="9ab62-198">![Test connection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC750996.png "Test connection")</span><span class="sxs-lookup"><span data-stu-id="9ab62-198">![Test connection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC750996.png "Test connection")</span></span>  
4. <span data-ttu-id="9ab62-199">On the **Provisioning** options page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="9ab62-199">On the **Provisioning** options page, click **Next**.</span></span> 
   
    <span data-ttu-id="9ab62-200">![Provisioning options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC750997.png "Provisioning options")</span><span class="sxs-lookup"><span data-stu-id="9ab62-200">![Provisioning options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC750997.png "Provisioning options")</span></span>
5. <span data-ttu-id="9ab62-201">On the **Start provisioning** dialog, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="9ab62-201">On the **Start provisioning** dialog, click **Complete**.</span></span> 
   
    <span data-ttu-id="9ab62-202">![Start provisioning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC750998.png "Start provisioning")</span><span class="sxs-lookup"><span data-stu-id="9ab62-202">![Start provisioning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workday-inbound-tutorial/IC750998.png "Start provisioning")</span></span>

<span data-ttu-id="9ab62-203">You can now go to the **Users** section and check whether your Workday user has been imported.</span><span class="sxs-lookup"><span data-stu-id="9ab62-203">You can now go to the **Users** section and check whether your Workday user has been imported.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9ab62-204">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="9ab62-204">Additional Resources</span></span>
* [<span data-ttu-id="9ab62-205">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9ab62-205">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9ab62-206">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9ab62-206">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


























