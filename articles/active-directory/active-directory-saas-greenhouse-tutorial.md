---
title: 'Tutorial: Azure Active Directory integration with Greenhouse | Microsoft Docs'
description: Learn how to use Greenhouse with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 78ec1766-4f79-4f16-9a66-d5584c4b6151
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 3f3c1d757d3f1f18c48123905a5261f63da17fdc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550158"
---
# <a name="tutorial-azure-active-directory-integration-with-greenhouse"></a><span data-ttu-id="a5c27-103">Tutorial: Azure Active Directory integration with Greenhouse</span><span class="sxs-lookup"><span data-stu-id="a5c27-103">Tutorial: Azure Active Directory integration with Greenhouse</span></span>
<span data-ttu-id="a5c27-104">The objective of this tutorial is to show the integration of Azure and Greenhouse.</span><span class="sxs-lookup"><span data-stu-id="a5c27-104">The objective of this tutorial is to show the integration of Azure and Greenhouse.</span></span>  

<span data-ttu-id="a5c27-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="a5c27-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="a5c27-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="a5c27-106">A valid Azure subscription</span></span>
* <span data-ttu-id="a5c27-107">A Greenhouse single sign-on (SSO) subscription</span><span class="sxs-lookup"><span data-stu-id="a5c27-107">A Greenhouse single sign-on (SSO) subscription</span></span>

<span data-ttu-id="a5c27-108">After completing this tutorial, the Azure AD users you have assigned to Greenhouse will be able to single sign into the application at your Greenhouse company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a5c27-108">After completing this tutorial, the Azure AD users you have assigned to Greenhouse will be able to single sign into the application at your Greenhouse company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="a5c27-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="a5c27-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="a5c27-110">Enabling the application integration for Greenhouse</span><span class="sxs-lookup"><span data-stu-id="a5c27-110">Enabling the application integration for Greenhouse</span></span>
* <span data-ttu-id="a5c27-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="a5c27-111">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="a5c27-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="a5c27-112">Configuring user provisioning</span></span>
* <span data-ttu-id="a5c27-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="a5c27-113">Assigning users</span></span>

<span data-ttu-id="a5c27-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC790783.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="a5c27-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC790783.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-greenhouse"></a><span data-ttu-id="a5c27-115">Enable the application integration for Greenhouse</span><span class="sxs-lookup"><span data-stu-id="a5c27-115">Enable the application integration for Greenhouse</span></span>
<span data-ttu-id="a5c27-116">The objective of this section is to outline how to enable the application integration for Greenhouse.</span><span class="sxs-lookup"><span data-stu-id="a5c27-116">The objective of this section is to outline how to enable the application integration for Greenhouse.</span></span>

<span data-ttu-id="a5c27-117">**To enable the application integration for Greenhouse, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a5c27-117">**To enable the application integration for Greenhouse, perform the following steps:**</span></span>

1. <span data-ttu-id="a5c27-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a5c27-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="a5c27-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="a5c27-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="a5c27-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="a5c27-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="a5c27-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="a5c27-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="a5c27-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="a5c27-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="a5c27-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="a5c27-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="a5c27-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="a5c27-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="a5c27-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="a5c27-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="a5c27-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="a5c27-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="a5c27-127">In the **search box**, type **greenhouse**.</span><span class="sxs-lookup"><span data-stu-id="a5c27-127">In the **search box**, type **greenhouse**.</span></span>
   
   <span data-ttu-id="a5c27-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC790784.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="a5c27-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC790784.png "Application Gallery")</span></span>
7. <span data-ttu-id="a5c27-129">In the results pane, select **Greenhouse**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="a5c27-129">In the results pane, select **Greenhouse**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="a5c27-130">![Greenhouse](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC790785.png "Greenhouse")</span><span class="sxs-lookup"><span data-stu-id="a5c27-130">![Greenhouse](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC790785.png "Greenhouse")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="a5c27-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="a5c27-131">Configure single sign-on</span></span>

<span data-ttu-id="a5c27-132">The objective of this section is to outline how to enable users to authenticate to Greenhouse with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="a5c27-132">The objective of this section is to outline how to enable users to authenticate to Greenhouse with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="a5c27-133">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a5c27-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="a5c27-134">In the Azure classic portal, on the **Greenhouse** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="a5c27-134">In the Azure classic portal, on the **Greenhouse** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="a5c27-135">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC790786.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="a5c27-135">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC790786.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="a5c27-136">On the **How would you like users to sign on to Greenhouse** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a5c27-136">On the **How would you like users to sign on to Greenhouse** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="a5c27-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC790787.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="a5c27-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC790787.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="a5c27-138">On the **Configure App URL** page, in the **Sign On URL** textbox, type your URL using the following pattern "*https://company.greenhouse.io*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a5c27-138">On the **Configure App URL** page, in the **Sign On URL** textbox, type your URL using the following pattern "*https://company.greenhouse.io*", and then click **Next**.</span></span>
   
   <span data-ttu-id="a5c27-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC790788.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="a5c27-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC790788.png "Configure App URL")</span></span>
4. <span data-ttu-id="a5c27-140">On the **Configure single sign-on at Greenhouse** page, click **Download metadata**, and then save metadata file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="a5c27-140">On the **Configure single sign-on at Greenhouse** page, click **Download metadata**, and then save metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="a5c27-141">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC790789.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="a5c27-141">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC790789.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="a5c27-142">Forward that Metadata file to Greenhouse Support team.</span><span class="sxs-lookup"><span data-stu-id="a5c27-142">Forward that Metadata file to Greenhouse Support team.</span></span>

>[!NOTE]
><span data-ttu-id="a5c27-143">Single sign-on has to be enabled by the Greenhouse support team.</span><span class="sxs-lookup"><span data-stu-id="a5c27-143">Single sign-on has to be enabled by the Greenhouse support team.</span></span>
>

6. <span data-ttu-id="a5c27-144">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="a5c27-144">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="a5c27-145">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC790790.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="a5c27-145">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC790790.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="a5c27-146">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="a5c27-146">Configure user provisioning</span></span>

<span data-ttu-id="a5c27-147">In order to enable Azure AD users to log into Greenhouse, they must be provisioned into Greenhouse.</span><span class="sxs-lookup"><span data-stu-id="a5c27-147">In order to enable Azure AD users to log into Greenhouse, they must be provisioned into Greenhouse.</span></span> <span data-ttu-id="a5c27-148">In the case of Greenhouse, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="a5c27-148">In the case of Greenhouse, provisioning is a manual task.</span></span>

<span data-ttu-id="a5c27-149">**To provision a user accounts, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a5c27-149">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="a5c27-150">Log in to your **Greenhouse** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="a5c27-150">Log in to your **Greenhouse** company site as an administrator.</span></span>
2. <span data-ttu-id="a5c27-151">In the menu on the top, click **Configure**, and then click **Users**.</span><span class="sxs-lookup"><span data-stu-id="a5c27-151">In the menu on the top, click **Configure**, and then click **Users**.</span></span>
   
   <span data-ttu-id="a5c27-152">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC790791.png "Users")</span><span class="sxs-lookup"><span data-stu-id="a5c27-152">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC790791.png "Users")</span></span>
3. <span data-ttu-id="a5c27-153">Click **New Users**.</span><span class="sxs-lookup"><span data-stu-id="a5c27-153">Click **New Users**.</span></span>
   
   <span data-ttu-id="a5c27-154">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC790792.png "New User")</span><span class="sxs-lookup"><span data-stu-id="a5c27-154">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC790792.png "New User")</span></span>
4. <span data-ttu-id="a5c27-155">In the **Add New User** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a5c27-155">In the **Add New User** section, perform the following steps:</span></span>
   
   <span data-ttu-id="a5c27-156">![Add New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC790793.png "Add New User")</span><span class="sxs-lookup"><span data-stu-id="a5c27-156">![Add New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC790793.png "Add New User")</span></span>
   1. <span data-ttu-id="a5c27-157">In the **Enter user emails** textbox, type the email address of a valid Azure Active Directory account you want to provision.</span><span class="sxs-lookup"><span data-stu-id="a5c27-157">In the **Enter user emails** textbox, type the email address of a valid Azure Active Directory account you want to provision.</span></span>
   2. <span data-ttu-id="a5c27-158">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="a5c27-158">Click **Save**.</span></span>    
   
      >[!NOTE]
      ><span data-ttu-id="a5c27-159">The Azure Active Directory account holders will receive an email including a link to confirm the account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="a5c27-159">The Azure Active Directory account holders will receive an email including a link to confirm the account before it becomes active.</span></span>
      >  

>[!NOTE]
><span data-ttu-id="a5c27-160">You can use any other Greenhouse user account creation tools or APIs provided by Greenhouse to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="a5c27-160">You can use any other Greenhouse user account creation tools or APIs provided by Greenhouse to provision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="a5c27-161">Assign users</span><span class="sxs-lookup"><span data-stu-id="a5c27-161">Assign users</span></span>
<span data-ttu-id="a5c27-162">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="a5c27-162">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="a5c27-163">**To assign users to Greenhouse, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a5c27-163">**To assign users to Greenhouse, perform the following steps:**</span></span>

1. <span data-ttu-id="a5c27-164">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="a5c27-164">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="a5c27-165">On the **Greenhouse** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="a5c27-165">On the **Greenhouse** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="a5c27-166">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC790794.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="a5c27-166">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC790794.png "Assign users")</span></span>
3. <span data-ttu-id="a5c27-167">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="a5c27-167">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="a5c27-168">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="a5c27-168">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="a5c27-169">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a5c27-169">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="a5c27-170">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a5c27-170">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


















