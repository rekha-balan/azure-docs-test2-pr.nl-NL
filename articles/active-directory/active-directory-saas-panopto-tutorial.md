---
title: 'Tutorial: Azure Active Directory integration with Panopto | Microsoft Docs'
description: Learn how to use Panopto with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 89c88e23-93ce-4970-9baa-1104c4e8fe4a
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/24/2017
ms.author: jeedes
ms.openlocfilehash: 9276d0b4c0138547a134f376b4bd933de8aff554
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555951"
---
# <a name="tutorial-azure-active-directory-integration-with-panopto"></a><span data-ttu-id="daacf-103">Tutorial: Azure Active Directory integration with Panopto</span><span class="sxs-lookup"><span data-stu-id="daacf-103">Tutorial: Azure Active Directory integration with Panopto</span></span>
<span data-ttu-id="daacf-104">The objective of this tutorial is to show the integration of Azure and Panopto.</span><span class="sxs-lookup"><span data-stu-id="daacf-104">The objective of this tutorial is to show the integration of Azure and Panopto.</span></span> 

<span data-ttu-id="daacf-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="daacf-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="daacf-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="daacf-106">A valid Azure subscription</span></span>
* <span data-ttu-id="daacf-107">A Panopto tenant</span><span class="sxs-lookup"><span data-stu-id="daacf-107">A Panopto tenant</span></span>

<span data-ttu-id="daacf-108">After completing this tutorial, the Azure AD users you have assigned to Panopto will be able to single sign into the application at your Panopto company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="daacf-108">After completing this tutorial, the Azure AD users you have assigned to Panopto will be able to single sign into the application at your Panopto company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="daacf-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="daacf-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="daacf-110">Enabling the application integration for Panopto</span><span class="sxs-lookup"><span data-stu-id="daacf-110">Enabling the application integration for Panopto</span></span>
2. <span data-ttu-id="daacf-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="daacf-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="daacf-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="daacf-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="daacf-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="daacf-113">Assigning users</span></span>

<span data-ttu-id="daacf-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panopto-tutorial/IC777665.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="daacf-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panopto-tutorial/IC777665.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-panopto"></a><span data-ttu-id="daacf-115">Enable the application integration for Panopto</span><span class="sxs-lookup"><span data-stu-id="daacf-115">Enable the application integration for Panopto</span></span>
<span data-ttu-id="daacf-116">The objective of this section is to outline how to enable the application integration for Panopto.</span><span class="sxs-lookup"><span data-stu-id="daacf-116">The objective of this section is to outline how to enable the application integration for Panopto.</span></span>

<span data-ttu-id="daacf-117">**To enable the application integration for Panopto, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="daacf-117">**To enable the application integration for Panopto, perform the following steps:**</span></span>

1. <span data-ttu-id="daacf-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="daacf-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="daacf-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panopto-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="daacf-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panopto-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="daacf-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="daacf-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="daacf-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="daacf-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="daacf-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panopto-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="daacf-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panopto-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="daacf-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="daacf-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="daacf-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panopto-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="daacf-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panopto-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="daacf-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="daacf-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="daacf-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panopto-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="daacf-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panopto-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="daacf-127">In the **search box**, type **Panopto**.</span><span class="sxs-lookup"><span data-stu-id="daacf-127">In the **search box**, type **Panopto**.</span></span>
   
   <span data-ttu-id="daacf-128">![Appkication Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panopto-tutorial/IC777666.png "Appkication Gallery")</span><span class="sxs-lookup"><span data-stu-id="daacf-128">![Appkication Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panopto-tutorial/IC777666.png "Appkication Gallery")</span></span>
7. <span data-ttu-id="daacf-129">In the results pane, select **Panopto**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="daacf-129">In the results pane, select **Panopto**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="daacf-130">![Panopto](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panopto-tutorial/IC782936.png "Panopto")</span><span class="sxs-lookup"><span data-stu-id="daacf-130">![Panopto](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panopto-tutorial/IC782936.png "Panopto")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="daacf-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="daacf-131">Configure single sign-on</span></span>

<span data-ttu-id="daacf-132">The objective of this section is to outline how to enable users to authenticate to Panopto with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="daacf-132">The objective of this section is to outline how to enable users to authenticate to Panopto with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="daacf-133">As part of this procedure, you are required to create a base-64 encoded certificate file.</span><span class="sxs-lookup"><span data-stu-id="daacf-133">As part of this procedure, you are required to create a base-64 encoded certificate file.</span></span> 

<span data-ttu-id="daacf-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="daacf-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

<span data-ttu-id="daacf-135">**To configure SSO, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="daacf-135">**To configure SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="daacf-136">In the Azure classic portal, on the **Panopto** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="daacf-136">In the Azure classic portal, on the **Panopto** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="daacf-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panopto-tutorial/IC777667.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="daacf-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panopto-tutorial/IC777667.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="daacf-138">On the **How would you like users to sign on to Panopto** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="daacf-138">On the **How would you like users to sign on to Panopto** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="daacf-139">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panopto-tutorial/IC777668.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="daacf-139">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panopto-tutorial/IC777668.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="daacf-140">On the **Configure App URL** page, in the **Panopto Sign In URL** textbox, type your URL using the following pattern "*https://\<tenant-name\>. Panopto.com*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="daacf-140">On the **Configure App URL** page, in the **Panopto Sign In URL** textbox, type your URL using the following pattern "*https://\<tenant-name\>. Panopto.com*", and then click **Next**.</span></span>
   
   <span data-ttu-id="daacf-141">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panopto-tutorial/IC777528.png "Configure app URL")</span><span class="sxs-lookup"><span data-stu-id="daacf-141">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panopto-tutorial/IC777528.png "Configure app URL")</span></span>
4. <span data-ttu-id="daacf-142">On the **Configure single sign-on at Panopto** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="daacf-142">On the **Configure single sign-on at Panopto** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
   <span data-ttu-id="daacf-143">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panopto-tutorial/IC777669.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="daacf-143">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panopto-tutorial/IC777669.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="daacf-144">In a different web browser window, log into your Panopto company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="daacf-144">In a different web browser window, log into your Panopto company site as an administrator.</span></span>
6. <span data-ttu-id="daacf-145">In the toolbar on the left, click **System**, and then click **Identity Providers**.</span><span class="sxs-lookup"><span data-stu-id="daacf-145">In the toolbar on the left, click **System**, and then click **Identity Providers**.</span></span>
   
   <span data-ttu-id="daacf-146">![System](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panopto-tutorial/IC777670.png "System")</span><span class="sxs-lookup"><span data-stu-id="daacf-146">![System](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panopto-tutorial/IC777670.png "System")</span></span>
7. <span data-ttu-id="daacf-147">Click **Add Provider**.</span><span class="sxs-lookup"><span data-stu-id="daacf-147">Click **Add Provider**.</span></span>
   
   <span data-ttu-id="daacf-148">![Identity Providers](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panopto-tutorial/IC777671.png "Identity Providers")</span><span class="sxs-lookup"><span data-stu-id="daacf-148">![Identity Providers](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panopto-tutorial/IC777671.png "Identity Providers")</span></span>
8. <span data-ttu-id="daacf-149">In the SAML provider section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="daacf-149">In the SAML provider section, perform the following steps:</span></span>
   
   <span data-ttu-id="daacf-150">![SaaS configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panopto-tutorial/IC777672.png "SaaS configuration")</span><span class="sxs-lookup"><span data-stu-id="daacf-150">![SaaS configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panopto-tutorial/IC777672.png "SaaS configuration")</span></span>
   
   1. <span data-ttu-id="daacf-151">From the **Provider Type** list, select **SAML20**.</span><span class="sxs-lookup"><span data-stu-id="daacf-151">From the **Provider Type** list, select **SAML20**.</span></span>
   2. <span data-ttu-id="daacf-152">In the **Instance Name** textbox, type a name for the instance.</span><span class="sxs-lookup"><span data-stu-id="daacf-152">In the **Instance Name** textbox, type a name for the instance.</span></span>
   3. <span data-ttu-id="daacf-153">In the **Friendly Description** textbox, type a friendly description.</span><span class="sxs-lookup"><span data-stu-id="daacf-153">In the **Friendly Description** textbox, type a friendly description.</span></span>
   4. <span data-ttu-id="daacf-154">In the Azure classic portal, on the **Configure single sign-on at Panopto** dialog page, copy the **Issuer URL** value, and then paste it into the **Issuer** textbox.</span><span class="sxs-lookup"><span data-stu-id="daacf-154">In the Azure classic portal, on the **Configure single sign-on at Panopto** dialog page, copy the **Issuer URL** value, and then paste it into the **Issuer** textbox.</span></span>
   5. <span data-ttu-id="daacf-155">In the Azure classic portal, on the **Configure single sign-on at Panopto** dialog page, copy the **SAML SSO URL** value, and then paste it into the **Bounce Page Url** textbox.</span><span class="sxs-lookup"><span data-stu-id="daacf-155">In the Azure classic portal, on the **Configure single sign-on at Panopto** dialog page, copy the **SAML SSO URL** value, and then paste it into the **Bounce Page Url** textbox.</span></span>
   6. <span data-ttu-id="daacf-156">Create a **base-64 encoded** file from your downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="daacf-156">Create a **base-64 encoded** file from your downloaded certificate.</span></span>    
   
      >[!TIP]
      ><span data-ttu-id="daacf-157">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="daacf-157">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>
      >
      
   7. <span data-ttu-id="daacf-158">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Public Key** textbox</span><span class="sxs-lookup"><span data-stu-id="daacf-158">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Public Key** textbox</span></span>
   8. <span data-ttu-id="daacf-159">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="daacf-159">Click **Save**.</span></span>

 <span data-ttu-id="daacf-160">![Save](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panopto-tutorial/IC777673.png "Save")</span><span class="sxs-lookup"><span data-stu-id="daacf-160">![Save](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panopto-tutorial/IC777673.png "Save")</span></span>
9. <span data-ttu-id="daacf-161">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="daacf-161">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
  <span data-ttu-id="daacf-162">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panopto-tutorial/IC777674.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="daacf-162">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panopto-tutorial/IC777674.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="daacf-163">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="daacf-163">Configure user provisioning</span></span>

<span data-ttu-id="daacf-164">There is no action item for you to configure user provisioning to Panopto.</span><span class="sxs-lookup"><span data-stu-id="daacf-164">There is no action item for you to configure user provisioning to Panopto.</span></span>  
<span data-ttu-id="daacf-165">When an assigned user tries to log into Panopto using the access panel, Panopto checks whether the user exists.</span><span class="sxs-lookup"><span data-stu-id="daacf-165">When an assigned user tries to log into Panopto using the access panel, Panopto checks whether the user exists.</span></span>  

<span data-ttu-id="daacf-166">If there is no user account available yet, it is automatically created by Panopto.</span><span class="sxs-lookup"><span data-stu-id="daacf-166">If there is no user account available yet, it is automatically created by Panopto.</span></span>

>[!NOTE]
><span data-ttu-id="daacf-167">You can use any other Panopto user account creation tools or APIs provided by Panopto to provision Azure AD user accounts.</span><span class="sxs-lookup"><span data-stu-id="daacf-167">You can use any other Panopto user account creation tools or APIs provided by Panopto to provision Azure AD user accounts.</span></span>
>
>

## <a name="assign-users"></a><span data-ttu-id="daacf-168">Assign users</span><span class="sxs-lookup"><span data-stu-id="daacf-168">Assign users</span></span>
<span data-ttu-id="daacf-169">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="daacf-169">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="daacf-170">**To assign users to Panopto, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="daacf-170">**To assign users to Panopto, perform the following steps:**</span></span>

1. <span data-ttu-id="daacf-171">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="daacf-171">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="daacf-172">On the **Panopto** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="daacf-172">On the **Panopto** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="daacf-173">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panopto-tutorial/IC777675.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="daacf-173">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panopto-tutorial/IC777675.png "Assign users")</span></span>
3. <span data-ttu-id="daacf-174">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="daacf-174">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="daacf-175">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panopto-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="daacf-175">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-panopto-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="daacf-176">If you want to test your SSO settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="daacf-176">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="daacf-177">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="daacf-177">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>



















