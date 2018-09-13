---
title: 'Tutorial: Azure Active Directory integration with Envoy | Microsoft Docs'
description: Learn how to use Envoy with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 71f7afcc-1033-4098-9b7e-4f9f2b26f734
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 58ea7c3abe0bc01240af15c9fc0e4ffd75d14f74
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554977"
---
# <a name="tutorial-azure-active-directory-integration-with-envoy"></a><span data-ttu-id="5ca29-103">Tutorial: Azure Active Directory integration with Envoy</span><span class="sxs-lookup"><span data-stu-id="5ca29-103">Tutorial: Azure Active Directory integration with Envoy</span></span>
<span data-ttu-id="5ca29-104">The objective of this tutorial is to show the integration of Azure and Envoy.</span><span class="sxs-lookup"><span data-stu-id="5ca29-104">The objective of this tutorial is to show the integration of Azure and Envoy.</span></span>  
<span data-ttu-id="5ca29-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="5ca29-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="5ca29-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="5ca29-106">A valid Azure subscription</span></span>
* <span data-ttu-id="5ca29-107">A Envoy tenant</span><span class="sxs-lookup"><span data-stu-id="5ca29-107">A Envoy tenant</span></span>

<span data-ttu-id="5ca29-108">After completing this tutorial, the Azure AD users you have assigned to Envoy will be able to single sign into the application at your Envoy company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5ca29-108">After completing this tutorial, the Azure AD users you have assigned to Envoy will be able to single sign into the application at your Envoy company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="5ca29-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="5ca29-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="5ca29-110">Enabling the application integration for Envoy</span><span class="sxs-lookup"><span data-stu-id="5ca29-110">Enabling the application integration for Envoy</span></span>
* <span data-ttu-id="5ca29-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="5ca29-111">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="5ca29-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="5ca29-112">Configuring user provisioning</span></span>
* <span data-ttu-id="5ca29-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="5ca29-113">Assigning users</span></span>

<span data-ttu-id="5ca29-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-envoy-tutorial/IC776759.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="5ca29-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-envoy-tutorial/IC776759.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-envoy"></a><span data-ttu-id="5ca29-115">Enable the application integration for Envoy</span><span class="sxs-lookup"><span data-stu-id="5ca29-115">Enable the application integration for Envoy</span></span>
<span data-ttu-id="5ca29-116">The objective of this section is to outline how to enable the application integration for Envoy.</span><span class="sxs-lookup"><span data-stu-id="5ca29-116">The objective of this section is to outline how to enable the application integration for Envoy.</span></span>

<span data-ttu-id="5ca29-117">**To enable the application integration for Envoy, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5ca29-117">**To enable the application integration for Envoy, perform the following steps:**</span></span>

1. <span data-ttu-id="5ca29-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5ca29-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="5ca29-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-envoy-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="5ca29-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-envoy-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="5ca29-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="5ca29-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="5ca29-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="5ca29-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="5ca29-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-envoy-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="5ca29-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-envoy-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="5ca29-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="5ca29-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="5ca29-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-envoy-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="5ca29-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-envoy-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="5ca29-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="5ca29-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="5ca29-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-envoy-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="5ca29-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-envoy-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="5ca29-127">In the **search box**, type **Envoy**.</span><span class="sxs-lookup"><span data-stu-id="5ca29-127">In the **search box**, type **Envoy**.</span></span>
   
   <span data-ttu-id="5ca29-128">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-envoy-tutorial/IC776760.png "Application gallery")</span><span class="sxs-lookup"><span data-stu-id="5ca29-128">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-envoy-tutorial/IC776760.png "Application gallery")</span></span>
7. <span data-ttu-id="5ca29-129">In the results pane, select **Envoy**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="5ca29-129">In the results pane, select **Envoy**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="5ca29-130">![Envoy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-envoy-tutorial/IC776777.png "Envoy")</span><span class="sxs-lookup"><span data-stu-id="5ca29-130">![Envoy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-envoy-tutorial/IC776777.png "Envoy")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="5ca29-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="5ca29-131">Configure single sign-on</span></span>

<span data-ttu-id="5ca29-132">The objective of this section is to outline how to enable users to authenticate to Envoy with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="5ca29-132">The objective of this section is to outline how to enable users to authenticate to Envoy with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="5ca29-133">Configuring SSO for Envoy requires you to retrieve a thumbprint value from a certificate.</span><span class="sxs-lookup"><span data-stu-id="5ca29-133">Configuring SSO for Envoy requires you to retrieve a thumbprint value from a certificate.</span></span> <span data-ttu-id="5ca29-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="5ca29-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>

<span data-ttu-id="5ca29-135">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5ca29-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="5ca29-136">In the Azure classic portal, on the **Envoy** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="5ca29-136">In the Azure classic portal, on the **Envoy** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="5ca29-137">![Enable single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-envoy-tutorial/IC776778.png "Enable single sign-on")</span><span class="sxs-lookup"><span data-stu-id="5ca29-137">![Enable single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-envoy-tutorial/IC776778.png "Enable single sign-on")</span></span>
2. <span data-ttu-id="5ca29-138">On the **How would you like users to sign on to Envoy** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5ca29-138">On the **How would you like users to sign on to Envoy** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="5ca29-139">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-envoy-tutorial/IC776779.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="5ca29-139">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-envoy-tutorial/IC776779.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="5ca29-140">On the **Configure App URL** page, in the **Envoy Sign In URL** textbox, type your URL using the following pattern "*https://\<tenant-name\>.Envoy.com*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5ca29-140">On the **Configure App URL** page, in the **Envoy Sign In URL** textbox, type your URL using the following pattern "*https://\<tenant-name\>.Envoy.com*", and then click **Next**.</span></span>
   
   <span data-ttu-id="5ca29-141">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-envoy-tutorial/IC776780.png "Configure app URL")</span><span class="sxs-lookup"><span data-stu-id="5ca29-141">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-envoy-tutorial/IC776780.png "Configure app URL")</span></span>
4. <span data-ttu-id="5ca29-142">On the **Configure single sign-on at Envoy** page, to download your certificate, click **Download certificate**, and then save the certificate file locally as **c:\\Envoy.cer**.</span><span class="sxs-lookup"><span data-stu-id="5ca29-142">On the **Configure single sign-on at Envoy** page, to download your certificate, click **Download certificate**, and then save the certificate file locally as **c:\\Envoy.cer**.</span></span>
   
   <span data-ttu-id="5ca29-143">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-envoy-tutorial/IC776781.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="5ca29-143">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-envoy-tutorial/IC776781.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="5ca29-144">In a different web browser window, log into your Envoy company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="5ca29-144">In a different web browser window, log into your Envoy company site as an administrator.</span></span>
6. <span data-ttu-id="5ca29-145">In the toolbar on the top, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="5ca29-145">In the toolbar on the top, click **Settings**.</span></span>
   
   <span data-ttu-id="5ca29-146">![Envoy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-envoy-tutorial/IC776782.png "Envoy")</span><span class="sxs-lookup"><span data-stu-id="5ca29-146">![Envoy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-envoy-tutorial/IC776782.png "Envoy")</span></span>
7. <span data-ttu-id="5ca29-147">Click **Company**.</span><span class="sxs-lookup"><span data-stu-id="5ca29-147">Click **Company**.</span></span>
   
   <span data-ttu-id="5ca29-148">![Company](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-envoy-tutorial/IC776783.png "Company")</span><span class="sxs-lookup"><span data-stu-id="5ca29-148">![Company](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-envoy-tutorial/IC776783.png "Company")</span></span>
8. <span data-ttu-id="5ca29-149">Click **SAML**.</span><span class="sxs-lookup"><span data-stu-id="5ca29-149">Click **SAML**.</span></span>
   
   <span data-ttu-id="5ca29-150">![SAML](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-envoy-tutorial/IC776784.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="5ca29-150">![SAML](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-envoy-tutorial/IC776784.png "SAML")</span></span>
9. <span data-ttu-id="5ca29-151">In the **SAML Authentication** configuration section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5ca29-151">In the **SAML Authentication** configuration section, perform the following steps:</span></span>
   
   <span data-ttu-id="5ca29-152">![SAML authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-envoy-tutorial/IC776785.png "SAML authentication")</span><span class="sxs-lookup"><span data-stu-id="5ca29-152">![SAML authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-envoy-tutorial/IC776785.png "SAML authentication")</span></span>   
   >[!NOTE]
   ><span data-ttu-id="5ca29-153">The value for the HQ location ID is auto generated by the application.</span><span class="sxs-lookup"><span data-stu-id="5ca29-153">The value for the HQ location ID is auto generated by the application.</span></span> 
   > 
   
   1. <span data-ttu-id="5ca29-154">Copy the **Thumbprint** value from the exported certificate, and then paste it into the **Fingerprint** textbox.</span><span class="sxs-lookup"><span data-stu-id="5ca29-154">Copy the **Thumbprint** value from the exported certificate, and then paste it into the **Fingerprint** textbox.</span></span>  
   
      >[!TIP]
      ><span data-ttu-id="5ca29-155">For more details, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="5ca29-155">For more details, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span> 
      > 
   2. <span data-ttu-id="5ca29-156">In the Azure classic portal, on the **Configure single sign-on at Envoy** dialog page, copy the **SAML SSO URL** value, and then paste it into the **Identity Provider HTTP SAML URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="5ca29-156">In the Azure classic portal, on the **Configure single sign-on at Envoy** dialog page, copy the **SAML SSO URL** value, and then paste it into the **Identity Provider HTTP SAML URL** textbox.</span></span>
   3. <span data-ttu-id="5ca29-157">Click **Save changes**.</span><span class="sxs-lookup"><span data-stu-id="5ca29-157">Click **Save changes**.</span></span>
10. <span data-ttu-id="5ca29-158">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="5ca29-158">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="5ca29-159">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-envoy-tutorial/IC776786.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="5ca29-159">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-envoy-tutorial/IC776786.png "Configure single sign-on")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="5ca29-160">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="5ca29-160">Configure user provisioning</span></span>

<span data-ttu-id="5ca29-161">There is no action item for you to configure user provisioning to Envoy.</span><span class="sxs-lookup"><span data-stu-id="5ca29-161">There is no action item for you to configure user provisioning to Envoy.</span></span>  
<span data-ttu-id="5ca29-162">When an assigned user tries to log into Envoy using the access panel, Envoy checks whether the user exists.</span><span class="sxs-lookup"><span data-stu-id="5ca29-162">When an assigned user tries to log into Envoy using the access panel, Envoy checks whether the user exists.</span></span>  

* <span data-ttu-id="5ca29-163">If there is no user account available yet, it is automatically created by Envoy.</span><span class="sxs-lookup"><span data-stu-id="5ca29-163">If there is no user account available yet, it is automatically created by Envoy.</span></span>

## <a name="assign-users"></a><span data-ttu-id="5ca29-164">Assign users</span><span class="sxs-lookup"><span data-stu-id="5ca29-164">Assign users</span></span>
<span data-ttu-id="5ca29-165">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="5ca29-165">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-envoy-perform-the-following-steps"></a><span data-ttu-id="5ca29-166">To assign users to Envoy, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5ca29-166">To assign users to Envoy, perform the following steps:</span></span>
1. <span data-ttu-id="5ca29-167">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="5ca29-167">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="5ca29-168">On the **Envoy** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="5ca29-168">On the **Envoy** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="5ca29-169">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-envoy-tutorial/IC776787.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="5ca29-169">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-envoy-tutorial/IC776787.png "Assign users")</span></span>
3. <span data-ttu-id="5ca29-170">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="5ca29-170">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="5ca29-171">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-envoy-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="5ca29-171">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-envoy-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="5ca29-172">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="5ca29-172">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="5ca29-173">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5ca29-173">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>



















