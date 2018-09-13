---
title: 'Tutorial: Configure Workday for Inbound Synchronization | Microsoft Docs'
description: Learn how to use Inbound Synchronization with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 8fe96f0a-f142-4d66-b53d-3ac3eb41a661
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 1e97b830e457b4e029bc75964a1e6fae20030b94
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540647"
---
# <a name="tutorial-configure-workday-for-inbound-synchronization"></a><span data-ttu-id="c73ee-103">Tutorial: Configure Workday for Inbound Synchronization</span><span class="sxs-lookup"><span data-stu-id="c73ee-103">Tutorial: Configure Workday for Inbound Synchronization</span></span>

<span data-ttu-id="c73ee-104">The objective of this tutorial is to show you the steps you need to perform in Workday and Microsoft Azure AD to import people from Workday to Microsoft Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c73ee-104">The objective of this tutorial is to show you the steps you need to perform in Workday and Microsoft Azure AD to import people from Workday to Microsoft Azure AD.</span></span>    

>[!NOTE]
><span data-ttu-id="c73ee-105">Azure Active Directory (AD) Premium is available for customers in China using the worldwide instance of Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c73ee-105">Azure Active Directory (AD) Premium is available for customers in China using the worldwide instance of Azure AD.</span></span> <span data-ttu-id="c73ee-106">Azure AD Premium is not currently supported in the Microsoft Azure service operated by 21Vianet in China.</span><span class="sxs-lookup"><span data-stu-id="c73ee-106">Azure AD Premium is not currently supported in the Microsoft Azure service operated by 21Vianet in China.</span></span>    
> 
> 

<span data-ttu-id="c73ee-107">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="c73ee-107">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>  

* <span data-ttu-id="c73ee-108">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="c73ee-108">A valid Azure subscription</span></span>  
* <span data-ttu-id="c73ee-109">A tenant in Workday</span><span class="sxs-lookup"><span data-stu-id="c73ee-109">A tenant in Workday</span></span>  

<span data-ttu-id="c73ee-110">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="c73ee-110">The scenario outlined in this tutorial consists of the following building blocks:</span></span>  

1. <span data-ttu-id="c73ee-111">Enabling the application integration for Workday</span><span class="sxs-lookup"><span data-stu-id="c73ee-111">Enabling the application integration for Workday</span></span>  
2. <span data-ttu-id="c73ee-112">Creating an integration system user</span><span class="sxs-lookup"><span data-stu-id="c73ee-112">Creating an integration system user</span></span>  
3. <span data-ttu-id="c73ee-113">Creating a security group</span><span class="sxs-lookup"><span data-stu-id="c73ee-113">Creating a security group</span></span>  
4. <span data-ttu-id="c73ee-114">Assigning the integration system user to the security group</span><span class="sxs-lookup"><span data-stu-id="c73ee-114">Assigning the integration system user to the security group</span></span>  
5. <span data-ttu-id="c73ee-115">Configuring security group options</span><span class="sxs-lookup"><span data-stu-id="c73ee-115">Configuring security group options</span></span>  
6. <span data-ttu-id="c73ee-116">Activating security policy changes</span><span class="sxs-lookup"><span data-stu-id="c73ee-116">Activating security policy changes</span></span>  
7. <span data-ttu-id="c73ee-117">Configuring user import in Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="c73ee-117">Configuring user import in Microsoft Azure AD</span></span>  

## <a name="enable-the-application-integration-for-workday"></a><span data-ttu-id="c73ee-118">Enable the application integration for Workday</span><span class="sxs-lookup"><span data-stu-id="c73ee-118">Enable the application integration for Workday</span></span>
<span data-ttu-id="c73ee-119">The objective of this section is to outline how to enable the application integration for Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c73ee-119">The objective of this section is to outline how to enable the application integration for Salesforce.</span></span>    

<span data-ttu-id="c73ee-120">**To enable the application integration for Workday, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c73ee-120">**To enable the application integration for Workday, perform the following steps:**</span></span>

1. <span data-ttu-id="c73ee-121">In the Azure Management Portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c73ee-121">In the Azure Management Portal, on the left navigation pane, click **Active Directory**.</span></span>    
   
   <span data-ttu-id="c73ee-122">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="c73ee-122">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC700993.png "Active Directory")</span></span>  
2. <span data-ttu-id="c73ee-123">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="c73ee-123">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>    
3. <span data-ttu-id="c73ee-124">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="c73ee-124">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>    
   
   <span data-ttu-id="c73ee-125">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="c73ee-125">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC700994.png "Applications")</span></span>  
4. <span data-ttu-id="c73ee-126">To open the **Application Gallery**, click **Add An App**, and then click **Add an application for my organization to use**.</span><span class="sxs-lookup"><span data-stu-id="c73ee-126">To open the **Application Gallery**, click **Add An App**, and then click **Add an application for my organization to use**.</span></span>    
   
   <span data-ttu-id="c73ee-127">![What do you want to do?](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC700995.png "What do you want to do?")</span><span class="sxs-lookup"><span data-stu-id="c73ee-127">![What do you want to do?](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC700995.png "What do you want to do?")</span></span>  
5. <span data-ttu-id="c73ee-128">In the **search box**, type **Workday**.</span><span class="sxs-lookup"><span data-stu-id="c73ee-128">In the **search box**, type **Workday**.</span></span>    
   
   <span data-ttu-id="c73ee-129">![Workday](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC701021.png "Workday")</span><span class="sxs-lookup"><span data-stu-id="c73ee-129">![Workday](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC701021.png "Workday")</span></span>  
6. <span data-ttu-id="c73ee-130">In the results pane, select **Workday**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="c73ee-130">In the results pane, select **Workday**, and then click **Complete** to add the application.</span></span>    
   
   <span data-ttu-id="c73ee-131">![Workday](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC701022.png "Workday")</span><span class="sxs-lookup"><span data-stu-id="c73ee-131">![Workday](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC701022.png "Workday")</span></span>  

## <a name="create-an-integration-system-user"></a><span data-ttu-id="c73ee-132">Create an integration system user</span><span class="sxs-lookup"><span data-stu-id="c73ee-132">Create an integration system user</span></span>
1. <span data-ttu-id="c73ee-133">In the **Workday Workbench**, enter **create user** in the search box, and then click on the link, **Create Integration System User**.</span><span class="sxs-lookup"><span data-stu-id="c73ee-133">In the **Workday Workbench**, enter **create user** in the search box, and then click on the link, **Create Integration System User**.</span></span>     
   
   <span data-ttu-id="c73ee-134">![create user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750979.png "create user")</span><span class="sxs-lookup"><span data-stu-id="c73ee-134">![create user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750979.png "create user")</span></span>  
2. <span data-ttu-id="c73ee-135">Complete the Create Integration System User task by supplying a user name and password for a new Integration System User.</span><span class="sxs-lookup"><span data-stu-id="c73ee-135">Complete the Create Integration System User task by supplying a user name and password for a new Integration System User.</span></span>  
 * <span data-ttu-id="c73ee-136">Leave the **Require New Password at Next Sign In** option unchecked, because this user will be logging on programmatically.</span><span class="sxs-lookup"><span data-stu-id="c73ee-136">Leave the **Require New Password at Next Sign In** option unchecked, because this user will be logging on programmatically.</span></span>    
 * <span data-ttu-id="c73ee-137">Leave the **Session Timeout Minutes** with its default value of 0, which will prevent the user’s sessions from timing out prematurely.</span><span class="sxs-lookup"><span data-stu-id="c73ee-137">Leave the **Session Timeout Minutes** with its default value of 0, which will prevent the user’s sessions from timing out prematurely.</span></span>    
   
   <span data-ttu-id="c73ee-138">![Create Integration System User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750980.png "Create Integration System User")</span><span class="sxs-lookup"><span data-stu-id="c73ee-138">![Create Integration System User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750980.png "Create Integration System User")</span></span>  

## <a name="create-a-security-group"></a><span data-ttu-id="c73ee-139">Create a security group</span><span class="sxs-lookup"><span data-stu-id="c73ee-139">Create a security group</span></span>
<span data-ttu-id="c73ee-140">For the scenario outlined in this tutorial, you need to create an unconstrained integration system security group and assign the user to it.</span><span class="sxs-lookup"><span data-stu-id="c73ee-140">For the scenario outlined in this tutorial, you need to create an unconstrained integration system security group and assign the user to it.</span></span>    

1. <span data-ttu-id="c73ee-141">Enter create security group in the search box, and then click on the link, Create Security Group.</span><span class="sxs-lookup"><span data-stu-id="c73ee-141">Enter create security group in the search box, and then click on the link, Create Security Group.</span></span>     
   
   <span data-ttu-id="c73ee-142">![CreateSecurity Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750981.png "CreateSecurity Group")</span><span class="sxs-lookup"><span data-stu-id="c73ee-142">![CreateSecurity Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750981.png "CreateSecurity Group")</span></span>  
2. <span data-ttu-id="c73ee-143">Complete the Create Security Group task.</span><span class="sxs-lookup"><span data-stu-id="c73ee-143">Complete the Create Security Group task.</span></span>  <span data-ttu-id="c73ee-144">Select Integration System Security Group—Unconstrained from the Type of Tenanted Security Group dropdown, to create a security group to which members will be explicitly added.</span><span class="sxs-lookup"><span data-stu-id="c73ee-144">Select Integration System Security Group—Unconstrained from the Type of Tenanted Security Group dropdown, to create a security group to which members will be explicitly added.</span></span>     
   
   <span data-ttu-id="c73ee-145">![CreateSecurity Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750982.png "CreateSecurity Group")</span><span class="sxs-lookup"><span data-stu-id="c73ee-145">![CreateSecurity Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750982.png "CreateSecurity Group")</span></span>  

## <a name="assign-the-integration-system-user-to-the-security-group"></a><span data-ttu-id="c73ee-146">Assign the integration system user to the security group</span><span class="sxs-lookup"><span data-stu-id="c73ee-146">Assign the integration system user to the security group</span></span>
1. <span data-ttu-id="c73ee-147">Enter edit security group in the search box, and then click on the link,  **Edit Security Group**.</span><span class="sxs-lookup"><span data-stu-id="c73ee-147">Enter edit security group in the search box, and then click on the link,  **Edit Security Group**.</span></span>     
   
   <span data-ttu-id="c73ee-148">![Edit Security Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750983.png "Edit Security Group")</span><span class="sxs-lookup"><span data-stu-id="c73ee-148">![Edit Security Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750983.png "Edit Security Group")</span></span>  
2. <span data-ttu-id="c73ee-149">Search for, and select the new integration security group by name.</span><span class="sxs-lookup"><span data-stu-id="c73ee-149">Search for, and select the new integration security group by name.</span></span>    
   
   <span data-ttu-id="c73ee-150">![Edit Security Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750984.png "Edit Security Group")</span><span class="sxs-lookup"><span data-stu-id="c73ee-150">![Edit Security Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750984.png "Edit Security Group")</span></span>  
3. <span data-ttu-id="c73ee-151">Add the new integration system user to the new security group.</span><span class="sxs-lookup"><span data-stu-id="c73ee-151">Add the new integration system user to the new security group.</span></span>       
   
   <span data-ttu-id="c73ee-152">![System Security Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750985.png "System Security Group")</span><span class="sxs-lookup"><span data-stu-id="c73ee-152">![System Security Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750985.png "System Security Group")</span></span>  

## <a name="configure-security-group-options"></a><span data-ttu-id="c73ee-153">Configure security group options</span><span class="sxs-lookup"><span data-stu-id="c73ee-153">Configure security group options</span></span>
<span data-ttu-id="c73ee-154">In this step, you grant to the new security group permissions for Get and Put operations on the objects secured by the following domain security policies:</span><span class="sxs-lookup"><span data-stu-id="c73ee-154">In this step, you grant to the new security group permissions for Get and Put operations on the objects secured by the following domain security policies:</span></span>  

* <span data-ttu-id="c73ee-155">External Account Provisioning</span><span class="sxs-lookup"><span data-stu-id="c73ee-155">External Account Provisioning</span></span>  
* <span data-ttu-id="c73ee-156">Worker Data: Public Worker Reports</span><span class="sxs-lookup"><span data-stu-id="c73ee-156">Worker Data: Public Worker Reports</span></span>  
* <span data-ttu-id="c73ee-157">Worker Data: All Positions</span><span class="sxs-lookup"><span data-stu-id="c73ee-157">Worker Data: All Positions</span></span>  
* <span data-ttu-id="c73ee-158">Worker Data: Current Staffing Information</span><span class="sxs-lookup"><span data-stu-id="c73ee-158">Worker Data: Current Staffing Information</span></span>  
* <span data-ttu-id="c73ee-159">Worker Data: Business Title on Worker Profile</span><span class="sxs-lookup"><span data-stu-id="c73ee-159">Worker Data: Business Title on Worker Profile</span></span>  

1. <span data-ttu-id="c73ee-160">Enter domain security policies in the search box, and then click on the link, Domain Security Policies for Functional Area.</span><span class="sxs-lookup"><span data-stu-id="c73ee-160">Enter domain security policies in the search box, and then click on the link, Domain Security Policies for Functional Area.</span></span>     
   
   <span data-ttu-id="c73ee-161">![Domain Security Policies](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750986.png "Domain Security Policies")</span><span class="sxs-lookup"><span data-stu-id="c73ee-161">![Domain Security Policies](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750986.png "Domain Security Policies")</span></span>  
2. <span data-ttu-id="c73ee-162">Search for system and select the System functional area.</span><span class="sxs-lookup"><span data-stu-id="c73ee-162">Search for system and select the System functional area.</span></span>  <span data-ttu-id="c73ee-163">Click on the button labelled, OK.</span><span class="sxs-lookup"><span data-stu-id="c73ee-163">Click on the button labelled, OK.</span></span>     
   
   <span data-ttu-id="c73ee-164">![Domain Security Policies](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750987.png "Domain Security Policies")</span><span class="sxs-lookup"><span data-stu-id="c73ee-164">![Domain Security Policies](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750987.png "Domain Security Policies")</span></span>  
3. <span data-ttu-id="c73ee-165">In the list of security policies for the System functional area, expand Security Administration and select the domain security policy, External Account Provisioning.</span><span class="sxs-lookup"><span data-stu-id="c73ee-165">In the list of security policies for the System functional area, expand Security Administration and select the domain security policy, External Account Provisioning.</span></span>     
   
   <span data-ttu-id="c73ee-166">![Domain Security Policies](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750988.png "Domain Security Policies")</span><span class="sxs-lookup"><span data-stu-id="c73ee-166">![Domain Security Policies](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750988.png "Domain Security Policies")</span></span>  
4. <span data-ttu-id="c73ee-167">Click on the Edit Permissions button, and then, on the Edit Permissions screen, add the new security group to the list of security groups with Get and Put integration permissions.</span><span class="sxs-lookup"><span data-stu-id="c73ee-167">Click on the Edit Permissions button, and then, on the Edit Permissions screen, add the new security group to the list of security groups with Get and Put integration permissions.</span></span>     
   
   <span data-ttu-id="c73ee-168">![Edit Permission](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750989.png "Edit Permission")</span><span class="sxs-lookup"><span data-stu-id="c73ee-168">![Edit Permission](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750989.png "Edit Permission")</span></span>  
5. <span data-ttu-id="c73ee-169">Repeat step 1, above, to return to the screen for selecting functional areas, and this time, search for staffing, select the Staffing functional area, and click on the button labelled, OK.</span><span class="sxs-lookup"><span data-stu-id="c73ee-169">Repeat step 1, above, to return to the screen for selecting functional areas, and this time, search for staffing, select the Staffing functional area, and click on the button labelled, OK.</span></span>    
   
   <span data-ttu-id="c73ee-170">![Domain Security Policies](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750990.png "Domain Security Policies")</span><span class="sxs-lookup"><span data-stu-id="c73ee-170">![Domain Security Policies](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750990.png "Domain Security Policies")</span></span>  
6. <span data-ttu-id="c73ee-171">In the list of security policies for the Staffing functional area, expand Worker Data: Staffing, and repeat step 4 above for each of these remaining security policies:</span><span class="sxs-lookup"><span data-stu-id="c73ee-171">In the list of security policies for the Staffing functional area, expand Worker Data: Staffing, and repeat step 4 above for each of these remaining security policies:</span></span>    
   
   * <span data-ttu-id="c73ee-172">Worker Data: Public Worker Reports</span><span class="sxs-lookup"><span data-stu-id="c73ee-172">Worker Data: Public Worker Reports</span></span>  
   * <span data-ttu-id="c73ee-173">Worker Data: All Positions</span><span class="sxs-lookup"><span data-stu-id="c73ee-173">Worker Data: All Positions</span></span>  
   * <span data-ttu-id="c73ee-174">Worker Data: Current Staffing Information</span><span class="sxs-lookup"><span data-stu-id="c73ee-174">Worker Data: Current Staffing Information</span></span>  
   * <span data-ttu-id="c73ee-175">Worker Data: Business Title on Worker Profile</span><span class="sxs-lookup"><span data-stu-id="c73ee-175">Worker Data: Business Title on Worker Profile</span></span>    
   
   <span data-ttu-id="c73ee-176">![Domain Security Policies](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750991.png "Domain Security Policies")</span><span class="sxs-lookup"><span data-stu-id="c73ee-176">![Domain Security Policies](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750991.png "Domain Security Policies")</span></span>  

## <a name="activate-security-policy-changes"></a><span data-ttu-id="c73ee-177">Activate security policy changes</span><span class="sxs-lookup"><span data-stu-id="c73ee-177">Activate security policy changes</span></span>
1. <span data-ttu-id="c73ee-178">Enter activate in the search box, and then click on the link,Activate Pending Security Policy Changes.</span><span class="sxs-lookup"><span data-stu-id="c73ee-178">Enter activate in the search box, and then click on the link,Activate Pending Security Policy Changes.</span></span>    
   
   <span data-ttu-id="c73ee-179">![Activate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750992.png "Activate")</span><span class="sxs-lookup"><span data-stu-id="c73ee-179">![Activate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750992.png "Activate")</span></span>  
2. <span data-ttu-id="c73ee-180">Begin the Activate Pending Security Policy Changes task by entering a comment for auditing purposes, and then clicking on the button labelled, OK.</span><span class="sxs-lookup"><span data-stu-id="c73ee-180">Begin the Activate Pending Security Policy Changes task by entering a comment for auditing purposes, and then clicking on the button labelled, OK.</span></span>      
   
   <span data-ttu-id="c73ee-181">![Activate Pending Security](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750993.png "Activate Pending Security")</span><span class="sxs-lookup"><span data-stu-id="c73ee-181">![Activate Pending Security](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750993.png "Activate Pending Security")</span></span>  
3. <span data-ttu-id="c73ee-182">Complete the task on the next screen by checking the checkbox labelled Confirm and clicking on the button labelled, OK.</span><span class="sxs-lookup"><span data-stu-id="c73ee-182">Complete the task on the next screen by checking the checkbox labelled Confirm and clicking on the button labelled, OK.</span></span>     
   
   <span data-ttu-id="c73ee-183">![Activate Pending Security](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750994.png "Activate Pending Security")</span><span class="sxs-lookup"><span data-stu-id="c73ee-183">![Activate Pending Security](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750994.png "Activate Pending Security")</span></span>  

## <a name="configure-user-import-in-microsoft-azure-ad"></a><span data-ttu-id="c73ee-184">Configure user import in Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="c73ee-184">Configure user import in Microsoft Azure AD</span></span>
<span data-ttu-id="c73ee-185">The objective of this section is to outline how Microsoft Azure AD to import people from Workday.</span><span class="sxs-lookup"><span data-stu-id="c73ee-185">The objective of this section is to outline how Microsoft Azure AD to import people from Workday.</span></span>    

<span data-ttu-id="c73ee-186">**To configure user import in Microsoft Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c73ee-186">**To configure user import in Microsoft Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c73ee-187">On the **Workday** application integration page, click **Configure user import** to open the **Configure Provisioning** dialog.</span><span class="sxs-lookup"><span data-stu-id="c73ee-187">On the **Workday** application integration page, click **Configure user import** to open the **Configure Provisioning** dialog.</span></span>    
2. <span data-ttu-id="c73ee-188">On the **Settings and admin credentials** page, perform the following steps, and then click Next:</span><span class="sxs-lookup"><span data-stu-id="c73ee-188">On the **Settings and admin credentials** page, perform the following steps, and then click Next:</span></span>    
   
   <span data-ttu-id="c73ee-189">![Settings and admin credentials](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750995.png "Settings and admin credentials")</span><span class="sxs-lookup"><span data-stu-id="c73ee-189">![Settings and admin credentials](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750995.png "Settings and admin credentials")</span></span>    
   
 * <span data-ttu-id="c73ee-190">In the **Workday admin user name** textbox, type the name of the user you have created in the [Creating an integration system user](https://msdn.microsoft.com/library/azure/Dn762434.aspx#BKMK_CreateUser) section.</span><span class="sxs-lookup"><span data-stu-id="c73ee-190">In the **Workday admin user name** textbox, type the name of the user you have created in the [Creating an integration system user](https://msdn.microsoft.com/library/azure/Dn762434.aspx#BKMK_CreateUser) section.</span></span>    
 * <span data-ttu-id="c73ee-191">In the **Workday admin password** textbox, type the password of the user you have created in the [Creating an integration system user](https://msdn.microsoft.com/library/azure/Dn762434.aspx#BKMK_CreateUser) section.</span><span class="sxs-lookup"><span data-stu-id="c73ee-191">In the **Workday admin password** textbox, type the password of the user you have created in the [Creating an integration system user](https://msdn.microsoft.com/library/azure/Dn762434.aspx#BKMK_CreateUser) section.</span></span>    
 * <span data-ttu-id="c73ee-192">In the **Workday tenant URL** textbox, type the URL or your Workday tenant.</span><span class="sxs-lookup"><span data-stu-id="c73ee-192">In the **Workday tenant URL** textbox, type the URL or your Workday tenant.</span></span>    
3. <span data-ttu-id="c73ee-193">On the **Test connection** page, click **Start test** to confirm connectivity, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c73ee-193">On the **Test connection** page, click **Start test** to confirm connectivity, and then click **Next**.</span></span>    
   
   <span data-ttu-id="c73ee-194">![Test connection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750996.png "Test connection")</span><span class="sxs-lookup"><span data-stu-id="c73ee-194">![Test connection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750996.png "Test connection")</span></span>  
4. <span data-ttu-id="c73ee-195">On the **Provisioning options** page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c73ee-195">On the **Provisioning options** page, click **Next**.</span></span>    
   
   <span data-ttu-id="c73ee-196">![Provisioning options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750997.png "Provisioning options")</span><span class="sxs-lookup"><span data-stu-id="c73ee-196">![Provisioning options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750997.png "Provisioning options")</span></span>  
5. <span data-ttu-id="c73ee-197">On the **Start provisioning** dialog, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="c73ee-197">On the **Start provisioning** dialog, click **Complete**.</span></span>    
   
   <span data-ttu-id="c73ee-198">![Start provisioning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750998.png "Start provisioning")</span><span class="sxs-lookup"><span data-stu-id="c73ee-198">![Start provisioning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750998.png "Start provisioning")</span></span>  

<span data-ttu-id="c73ee-199">You can now go to the **Users** section and check whether your Workday user has been imported.</span><span class="sxs-lookup"><span data-stu-id="c73ee-199">You can now go to the **Users** section and check whether your Workday user has been imported.</span></span>    


























