---
title: 'Tutorial: Azure Active Directory integration with Mozy Enterprise | Microsoft Docs'
description: Learn how to use Mozy Enterprise with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 489b5e62-85c2-45c9-8766-326632d48114
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/24/2017
ms.author: jeedes
ms.openlocfilehash: 8cc919642b71f276ed2f3598b5caaea4a6128de3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661519"
---
# <a name="tutorial-azure-active-directory-integration-with-mozy-enterprise"></a><span data-ttu-id="6436b-103">Tutorial: Azure Active Directory integration with Mozy Enterprise</span><span class="sxs-lookup"><span data-stu-id="6436b-103">Tutorial: Azure Active Directory integration with Mozy Enterprise</span></span>
<span data-ttu-id="6436b-104">The objective of this tutorial is to show the integration of Azure and Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="6436b-104">The objective of this tutorial is to show the integration of Azure and Mozy Enterprise.</span></span>  

<span data-ttu-id="6436b-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="6436b-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="6436b-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="6436b-106">A valid Azure subscription</span></span>
* <span data-ttu-id="6436b-107">A Mozy Enterprise tenant</span><span class="sxs-lookup"><span data-stu-id="6436b-107">A Mozy Enterprise tenant</span></span>

<span data-ttu-id="6436b-108">After completing this tutorial, the Azure AD users you have assigned to Mozy Enterprise will be able to single sign-on (SSO) to the application at your Mozy Enterprise company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6436b-108">After completing this tutorial, the Azure AD users you have assigned to Mozy Enterprise will be able to single sign-on (SSO) to the application at your Mozy Enterprise company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="6436b-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="6436b-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="6436b-110">Enabling the application integration for Mozy Enterprise</span><span class="sxs-lookup"><span data-stu-id="6436b-110">Enabling the application integration for Mozy Enterprise</span></span>
2. <span data-ttu-id="6436b-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="6436b-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="6436b-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="6436b-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="6436b-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="6436b-113">Assigning users</span></span>

<span data-ttu-id="6436b-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mozy-enterprise-tutorial/IC777308.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="6436b-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mozy-enterprise-tutorial/IC777308.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-mozy-enterprise"></a><span data-ttu-id="6436b-115">Enabling the application integration for Mozy Enterprise</span><span class="sxs-lookup"><span data-stu-id="6436b-115">Enabling the application integration for Mozy Enterprise</span></span>
<span data-ttu-id="6436b-116">The objective of this section is to outline how to enable the application integration for Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="6436b-116">The objective of this section is to outline how to enable the application integration for Mozy Enterprise.</span></span>

<span data-ttu-id="6436b-117">**To enable the application integration for Mozy Enterprise, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6436b-117">**To enable the application integration for Mozy Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="6436b-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6436b-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="6436b-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mozy-enterprise-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="6436b-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mozy-enterprise-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="6436b-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="6436b-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="6436b-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="6436b-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="6436b-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mozy-enterprise-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="6436b-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mozy-enterprise-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="6436b-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="6436b-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="6436b-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mozy-enterprise-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="6436b-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mozy-enterprise-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="6436b-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="6436b-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="6436b-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mozy-enterprise-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="6436b-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mozy-enterprise-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="6436b-127">In the **search box**, type **mozy enterprise**.</span><span class="sxs-lookup"><span data-stu-id="6436b-127">In the **search box**, type **mozy enterprise**.</span></span>
   
   <span data-ttu-id="6436b-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mozy-enterprise-tutorial/IC777309.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="6436b-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mozy-enterprise-tutorial/IC777309.png "Application Gallery")</span></span>
7. <span data-ttu-id="6436b-129">In the results pane, select **Mozy Enterprise**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="6436b-129">In the results pane, select **Mozy Enterprise**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="6436b-130">![Mozy Enterprise](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mozy-enterprise-tutorial/IC777310.png "Mozy Enterprise")</span><span class="sxs-lookup"><span data-stu-id="6436b-130">![Mozy Enterprise](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mozy-enterprise-tutorial/IC777310.png "Mozy Enterprise")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="6436b-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="6436b-131">Configure single sign-on</span></span>

<span data-ttu-id="6436b-132">The objective of this section is to outline how to enable users to authenticate to Mozy Enterprise with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="6436b-132">The objective of this section is to outline how to enable users to authenticate to Mozy Enterprise with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="6436b-133">As part of this procedure, you are required to upload a base-64 encoded certificate to your Mozy Enterprise tenant.</span><span class="sxs-lookup"><span data-stu-id="6436b-133">As part of this procedure, you are required to upload a base-64 encoded certificate to your Mozy Enterprise tenant.</span></span> <span data-ttu-id="6436b-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="6436b-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="6436b-135">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6436b-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="6436b-136">In the Azure classic portal, on the **Mozy Enterprise** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="6436b-136">In the Azure classic portal, on the **Mozy Enterprise** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="6436b-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mozy-enterprise-tutorial/IC771709.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="6436b-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mozy-enterprise-tutorial/IC771709.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="6436b-138">On the **How would you like users to sign on to Mozy Enterprise** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6436b-138">On the **How would you like users to sign on to Mozy Enterprise** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="6436b-139">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mozy-enterprise-tutorial/IC777311.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="6436b-139">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mozy-enterprise-tutorial/IC777311.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="6436b-140">On the **Configure App URL** page, in the **Mozy Enterprise Sign In URL** textbox, type your URL using the following pattern "*https://\<tenant-name\>.Mozyenterprise.com*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6436b-140">On the **Configure App URL** page, in the **Mozy Enterprise Sign In URL** textbox, type your URL using the following pattern "*https://\<tenant-name\>.Mozyenterprise.com*", and then click **Next**.</span></span>
   
   <span data-ttu-id="6436b-141">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mozy-enterprise-tutorial/IC777312.png "Configure app URL")</span><span class="sxs-lookup"><span data-stu-id="6436b-141">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mozy-enterprise-tutorial/IC777312.png "Configure app URL")</span></span>
4. <span data-ttu-id="6436b-142">On the **Configure single sign-on at Mozy Enterprise** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="6436b-142">On the **Configure single sign-on at Mozy Enterprise** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
   <span data-ttu-id="6436b-143">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mozy-enterprise-tutorial/IC777313.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="6436b-143">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mozy-enterprise-tutorial/IC777313.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="6436b-144">In a different web browser window, log into your Mozy Enterprise company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="6436b-144">In a different web browser window, log into your Mozy Enterprise company site as an administrator.</span></span>
6. <span data-ttu-id="6436b-145">In the **Configuration** section, click **Authentication Policy**.</span><span class="sxs-lookup"><span data-stu-id="6436b-145">In the **Configuration** section, click **Authentication Policy**.</span></span>
   
   <span data-ttu-id="6436b-146">![Authentication policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mozy-enterprise-tutorial/IC777314.png "Authentication policy")</span><span class="sxs-lookup"><span data-stu-id="6436b-146">![Authentication policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mozy-enterprise-tutorial/IC777314.png "Authentication policy")</span></span>
7. <span data-ttu-id="6436b-147">On the **Authentication Policy** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6436b-147">On the **Authentication Policy** section, perform the following steps:</span></span>
   
   <span data-ttu-id="6436b-148">![Authentication policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mozy-enterprise-tutorial/IC777315.png "Authentication policy")</span><span class="sxs-lookup"><span data-stu-id="6436b-148">![Authentication policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mozy-enterprise-tutorial/IC777315.png "Authentication policy")</span></span>
   
   1. <span data-ttu-id="6436b-149">Select **Directory Service** as **Provider**.</span><span class="sxs-lookup"><span data-stu-id="6436b-149">Select **Directory Service** as **Provider**.</span></span>
   2. <span data-ttu-id="6436b-150">Select **Use LDAP Push**.</span><span class="sxs-lookup"><span data-stu-id="6436b-150">Select **Use LDAP Push**.</span></span>
   3. <span data-ttu-id="6436b-151">Click the **SAML Authentication** tab.</span><span class="sxs-lookup"><span data-stu-id="6436b-151">Click the **SAML Authentication** tab.</span></span>
   4. <span data-ttu-id="6436b-152">In the Azure classic portal, on the **Configure single sign-on at Mozy Enterprise** dialog page, copy the **Authentication Request URL** value, and then paste it into the **Authentication URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="6436b-152">In the Azure classic portal, on the **Configure single sign-on at Mozy Enterprise** dialog page, copy the **Authentication Request URL** value, and then paste it into the **Authentication URL** textbox.</span></span>
   5. <span data-ttu-id="6436b-153">In the Azure classic portal, on the **Configure single sign-on at Mozy Enterprise** dialog page, copy the **Identity Provider ID** value, and then paste it into the **SAML Endpoint** textbox.</span><span class="sxs-lookup"><span data-stu-id="6436b-153">In the Azure classic portal, on the **Configure single sign-on at Mozy Enterprise** dialog page, copy the **Identity Provider ID** value, and then paste it into the **SAML Endpoint** textbox.</span></span>
   6. <span data-ttu-id="6436b-154">Create a **Base-64 encoded** file from your downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="6436b-154">Create a **Base-64 encoded** file from your downloaded certificate.</span></span>  
   
      >[!TIP]
      ><span data-ttu-id="6436b-155">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="6436b-155">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>
      >
      >

   7. <span data-ttu-id="6436b-156">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **SAML Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="6436b-156">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **SAML Certificate** textbox.</span></span>
   8. <span data-ttu-id="6436b-157">Select **Enable SSO for Admins to log in with their network credentials**.</span><span class="sxs-lookup"><span data-stu-id="6436b-157">Select **Enable SSO for Admins to log in with their network credentials**.</span></span>
   9. <span data-ttu-id="6436b-158">Click **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="6436b-158">Click **Save Changes**.</span></span>
8. <span data-ttu-id="6436b-159">In the Azure classic portal, on the **Configure single sign-on at Mozy Enterprise** dialog page, select the single sign-on configuration confirmation, and then click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="6436b-159">In the Azure classic portal, on the **Configure single sign-on at Mozy Enterprise** dialog page, select the single sign-on configuration confirmation, and then click **Complete**.</span></span>
   
   <span data-ttu-id="6436b-160">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mozy-enterprise-tutorial/IC777316.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="6436b-160">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mozy-enterprise-tutorial/IC777316.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="6436b-161">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="6436b-161">Configure user provisioning</span></span>

<span data-ttu-id="6436b-162">In order to enable Azure AD users to log into Mozy Enterprise, they must be provisioned into Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="6436b-162">In order to enable Azure AD users to log into Mozy Enterprise, they must be provisioned into Mozy Enterprise.</span></span>

<span data-ttu-id="6436b-163">In the case of Mozy Enterprise, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="6436b-163">In the case of Mozy Enterprise, provisioning is a manual task.</span></span>

<span data-ttu-id="6436b-164">**To provision a user accounts, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6436b-164">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="6436b-165">Log in to your **Mozy Enterprise** tenant.</span><span class="sxs-lookup"><span data-stu-id="6436b-165">Log in to your **Mozy Enterprise** tenant.</span></span>
2. <span data-ttu-id="6436b-166">Click **Users**, and then click **Add New User**.</span><span class="sxs-lookup"><span data-stu-id="6436b-166">Click **Users**, and then click **Add New User**.</span></span>
   
   <span data-ttu-id="6436b-167">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mozy-enterprise-tutorial/IC777317.png "Users")</span><span class="sxs-lookup"><span data-stu-id="6436b-167">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mozy-enterprise-tutorial/IC777317.png "Users")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="6436b-168">The **Add New User** option is only displayed only if **Mozy** is selected as the provider under **Authentication policy**.</span><span class="sxs-lookup"><span data-stu-id="6436b-168">The **Add New User** option is only displayed only if **Mozy** is selected as the provider under **Authentication policy**.</span></span> <span data-ttu-id="6436b-169">If SAML Authentication is configured then the users are added automatically on their first login through Single sign on.</span><span class="sxs-lookup"><span data-stu-id="6436b-169">If SAML Authentication is configured then the users are added automatically on their first login through Single sign on.</span></span>
   >
   > 
    
3. <span data-ttu-id="6436b-170">On the new user dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6436b-170">On the new user dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="6436b-171">![Add Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mozy-enterprise-tutorial/IC777318.png "Add Users")</span><span class="sxs-lookup"><span data-stu-id="6436b-171">![Add Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mozy-enterprise-tutorial/IC777318.png "Add Users")</span></span>
   
  1. <span data-ttu-id="6436b-172">From the **Choose a Group** list, select a group.</span><span class="sxs-lookup"><span data-stu-id="6436b-172">From the **Choose a Group** list, select a group.</span></span>
  2. <span data-ttu-id="6436b-173">From the **What type of user** list, select a type.</span><span class="sxs-lookup"><span data-stu-id="6436b-173">From the **What type of user** list, select a type.</span></span>
  3. <span data-ttu-id="6436b-174">In the **Username** textbox, type the name of the Azure AD user.</span><span class="sxs-lookup"><span data-stu-id="6436b-174">In the **Username** textbox, type the name of the Azure AD user.</span></span>
  4. <span data-ttu-id="6436b-175">In the **Email** textbox, type the email address of the Azure AD user.</span><span class="sxs-lookup"><span data-stu-id="6436b-175">In the **Email** textbox, type the email address of the Azure AD user.</span></span>
  5. <span data-ttu-id="6436b-176">Select **Send user instruction email**.</span><span class="sxs-lookup"><span data-stu-id="6436b-176">Select **Send user instruction email**.</span></span>
  6. <span data-ttu-id="6436b-177">Click **Add User(s)**.</span><span class="sxs-lookup"><span data-stu-id="6436b-177">Click **Add User(s)**.</span></span>

     >[!NOTE]
     > <span data-ttu-id="6436b-178">After creating the user, an email will be sent to the Azure AD user that includes a link to confirm the account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="6436b-178">After creating the user, an email will be sent to the Azure AD user that includes a link to confirm the account before it becomes active.</span></span>
     > 
     > 

>[!NOTE]
><span data-ttu-id="6436b-179">You can use any other Mozy Enterprise user account creation tools or APIs provided by Mozy Enterprise to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="6436b-179">You can use any other Mozy Enterprise user account creation tools or APIs provided by Mozy Enterprise to provision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="6436b-180">Assign users</span><span class="sxs-lookup"><span data-stu-id="6436b-180">Assign users</span></span>
<span data-ttu-id="6436b-181">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="6436b-181">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="6436b-182">**To assign users to Mozy Enterprise, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6436b-182">**To assign users to Mozy Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="6436b-183">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="6436b-183">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="6436b-184">On the \*\*Mozy Enterprise \*\*application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="6436b-184">On the \*\*Mozy Enterprise \*\*application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="6436b-185">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mozy-enterprise-tutorial/IC777319.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="6436b-185">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mozy-enterprise-tutorial/IC777319.png "Assign users")</span></span>
3. <span data-ttu-id="6436b-186">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="6436b-186">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="6436b-187">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mozy-enterprise-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="6436b-187">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mozy-enterprise-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="6436b-188">If you want to test your SSO settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="6436b-188">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="6436b-189">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6436b-189">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="6436b-190">Additional resources</span><span class="sxs-lookup"><span data-stu-id="6436b-190">Additional resources</span></span>

* [<span data-ttu-id="6436b-191">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6436b-191">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* <span data-ttu-id="6436b-192">[What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md</span><span class="sxs-lookup"><span data-stu-id="6436b-192">[What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md</span></span>


















