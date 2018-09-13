---
title: 'Tutorial: Azure Active Directory integration with Citrix GoToMeeting | Microsoft Docs'
description: Learn how to use Citrix GoToMeeting with Azure Active Directory to enable single sign-on, automated provisioning, and more!.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 7d7897f6-b88e-4dd5-8f3a-e612337b1413
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: 6d29aa165ca052ba694057f33152fa382a05bc2d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555574"
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-gotomeeting"></a><span data-ttu-id="555fa-103">Tutorial: Azure Active Directory integration with Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="555fa-103">Tutorial: Azure Active Directory integration with Citrix GoToMeeting</span></span>

<span data-ttu-id="555fa-104">The objective of this tutorial is to show the integration of Azure and Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="555fa-104">The objective of this tutorial is to show the integration of Azure and Citrix GoToMeeting.</span></span> <span data-ttu-id="555fa-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="555fa-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="555fa-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="555fa-106">A valid Azure subscription</span></span>
* <span data-ttu-id="555fa-107">A tenant in Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="555fa-107">A tenant in Citrix GoToMeeting</span></span>

<span data-ttu-id="555fa-108">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="555fa-108">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="555fa-109">Enabling the application integration for Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="555fa-109">Enabling the application integration for Citrix GoToMeeting</span></span>
2. <span data-ttu-id="555fa-110">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="555fa-110">Configuring single sign-on</span></span>
3. <span data-ttu-id="555fa-111">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="555fa-111">Configuring user provisioning</span></span>
4. <span data-ttu-id="555fa-112">Assigning users</span><span class="sxs-lookup"><span data-stu-id="555fa-112">Assigning users</span></span>

<span data-ttu-id="555fa-113">![Configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-gotomeeting-tutorial/IC768996.png "Configuration")</span><span class="sxs-lookup"><span data-stu-id="555fa-113">![Configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-gotomeeting-tutorial/IC768996.png "Configuration")</span></span>

## <a name="enabling-the-application-integration-for-citrix-gotomeeting"></a><span data-ttu-id="555fa-114">Enabling the application integration for Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="555fa-114">Enabling the application integration for Citrix GoToMeeting</span></span>
<span data-ttu-id="555fa-115">The objective of this section is to outline how to enable the application integration for Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="555fa-115">The objective of this section is to outline how to enable the application integration for Citrix GoToMeeting.</span></span>

### <a name="to-enable-the-application-integration-for-citrix-gotomeeting-perform-the-following-steps"></a><span data-ttu-id="555fa-116">To enable the application integration for Citrix GoToMeeting, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="555fa-116">To enable the application integration for Citrix GoToMeeting, perform the following steps:</span></span>
1. <span data-ttu-id="555fa-117">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="555fa-117">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="555fa-118">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-gotomeeting-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="555fa-118">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-gotomeeting-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="555fa-119">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="555fa-119">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="555fa-120">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="555fa-120">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="555fa-121">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-gotomeeting-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="555fa-121">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-gotomeeting-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="555fa-122">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="555fa-122">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="555fa-123">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-gotomeeting-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="555fa-123">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-gotomeeting-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="555fa-124">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="555fa-124">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="555fa-125">![Add an application from gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-gotomeeting-tutorial/IC749322.png "Add an application from gallery")</span><span class="sxs-lookup"><span data-stu-id="555fa-125">![Add an application from gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-gotomeeting-tutorial/IC749322.png "Add an application from gallery")</span></span>

6. <span data-ttu-id="555fa-126">In the **search box**, type **Citrix GoToMeeting**.</span><span class="sxs-lookup"><span data-stu-id="555fa-126">In the **search box**, type **Citrix GoToMeeting**.</span></span>
   
    <span data-ttu-id="555fa-127">![Citrix GoToMeeting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-gotomeeting-tutorial/IC701006.png "Citrix GoToMeeting")</span><span class="sxs-lookup"><span data-stu-id="555fa-127">![Citrix GoToMeeting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-gotomeeting-tutorial/IC701006.png "Citrix GoToMeeting")</span></span>

7. <span data-ttu-id="555fa-128">In the results pane, select **Citrix GoToMeeting**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="555fa-128">In the results pane, select **Citrix GoToMeeting**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="555fa-129">![Citrix GoToMeeting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-gotomeeting-tutorial/IC701012.png "Citrix GoToMeeting")</span><span class="sxs-lookup"><span data-stu-id="555fa-129">![Citrix GoToMeeting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-gotomeeting-tutorial/IC701012.png "Citrix GoToMeeting")</span></span>
   
## <a name="configuring-single-sign-on"></a><span data-ttu-id="555fa-130">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="555fa-130">Configuring single sign-on</span></span>

<span data-ttu-id="555fa-131">The objective of this section is to outline how to enable users to authenticate to Citrix GoToMeeting with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="555fa-131">The objective of this section is to outline how to enable users to authenticate to Citrix GoToMeeting with their account in Azure AD using federation based on the SAML protocol.</span></span>  
<span data-ttu-id="555fa-132">As part of this procedure, you are required to upload a base-64 encoded certificate to your Citrix GoToMeeting tenant.</span><span class="sxs-lookup"><span data-stu-id="555fa-132">As part of this procedure, you are required to upload a base-64 encoded certificate to your Citrix GoToMeeting tenant.</span></span>  
<span data-ttu-id="555fa-133">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="555fa-133">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a><span data-ttu-id="555fa-134">To configure single sign-on, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="555fa-134">To configure single sign-on, perform the following steps:</span></span>
1. <span data-ttu-id="555fa-135">On the **Citrix GoToMeeting** application integration page, click **Configure single sign-on** to open the **CONFIGURE SINGLE SIGN ON** dialog.</span><span class="sxs-lookup"><span data-stu-id="555fa-135">On the **Citrix GoToMeeting** application integration page, click **Configure single sign-on** to open the **CONFIGURE SINGLE SIGN ON** dialog.</span></span>
   
    <span data-ttu-id="555fa-136">![Enable single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-gotomeeting-tutorial/IC768997.png "Enable single sign-on")</span><span class="sxs-lookup"><span data-stu-id="555fa-136">![Enable single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-gotomeeting-tutorial/IC768997.png "Enable single sign-on")</span></span>

2. <span data-ttu-id="555fa-137">On the **How would you like users to sign on to Citrix GoToMeeting** page, select **Microsoft Azure AD Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="555fa-137">On the **How would you like users to sign on to Citrix GoToMeeting** page, select **Microsoft Azure AD Single Sign-On**.</span></span>
   
    <span data-ttu-id="555fa-138">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-gotomeeting-tutorial/IC768998.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="555fa-138">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-gotomeeting-tutorial/IC768998.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="555fa-139">On the **Configure App Settings** page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="555fa-139">On the **Configure App Settings** page, click **Next**.</span></span> 
   
    <span data-ttu-id="555fa-140">![Enable single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-gotomeeting-tutorial/IC7689981.png "Enable single sign-on")</span><span class="sxs-lookup"><span data-stu-id="555fa-140">![Enable single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-gotomeeting-tutorial/IC7689981.png "Enable single sign-on")</span></span>

4. <span data-ttu-id="555fa-141">On the **Configure single sign-on at Citrix GoToMeeting** page, click **Download certificate**, and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="555fa-141">On the **Configure single sign-on at Citrix GoToMeeting** page, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
    <span data-ttu-id="555fa-142">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-gotomeeting-tutorial/IC768999.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="555fa-142">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-gotomeeting-tutorial/IC768999.png "Configure single sign-on")</span></span>

5. <span data-ttu-id="555fa-143">In a different browser window, log into your [Citrix Organization Center](https://account.citrixonline.com/organization/administration/).</span><span class="sxs-lookup"><span data-stu-id="555fa-143">In a different browser window, log into your [Citrix Organization Center](https://account.citrixonline.com/organization/administration/).</span></span>

6. <span data-ttu-id="555fa-144">Click the **Identity Provider** tab, and then perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="555fa-144">Click the **Identity Provider** tab, and then perform the following steps:</span></span>  
   
    <span data-ttu-id="555fa-145">![SAML setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "SAML setup")</span><span class="sxs-lookup"><span data-stu-id="555fa-145">![SAML setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "SAML setup")</span></span>
   
    <span data-ttu-id="555fa-146">a.</span><span class="sxs-lookup"><span data-stu-id="555fa-146">a.</span></span> <span data-ttu-id="555fa-147">Select **Manual**</span><span class="sxs-lookup"><span data-stu-id="555fa-147">Select **Manual**</span></span>

    <span data-ttu-id="555fa-148">b.</span><span class="sxs-lookup"><span data-stu-id="555fa-148">b.</span></span> <span data-ttu-id="555fa-149">In the Azure classic portal, on the **Configure single sign-on at Citrix GoToMeeting** dialog page, copy the **Sign-In Page URL** value, and then paste it into the **Sign-in page URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="555fa-149">In the Azure classic portal, on the **Configure single sign-on at Citrix GoToMeeting** dialog page, copy the **Sign-In Page URL** value, and then paste it into the **Sign-in page URL** textbox.</span></span> 

    <span data-ttu-id="555fa-150">c.</span><span class="sxs-lookup"><span data-stu-id="555fa-150">c.</span></span> <span data-ttu-id="555fa-151">In the Azure classic portal, on the **Configure single sign-on at Citrix GoToMeeting** dialog page, copy the **Sign-Out Page URL** value, and then paste it into the **Sign-out page URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="555fa-151">In the Azure classic portal, on the **Configure single sign-on at Citrix GoToMeeting** dialog page, copy the **Sign-Out Page URL** value, and then paste it into the **Sign-out page URL** textbox.</span></span>

    <span data-ttu-id="555fa-152">d.</span><span class="sxs-lookup"><span data-stu-id="555fa-152">d.</span></span> <span data-ttu-id="555fa-153">In the Azure classic portal, on the **Configure single sign-on at Citrix GoToMeeting** dialog page, copy the **Entity ID** value, and then paste it into the **Identity Provider Entity ID** textbox.</span><span class="sxs-lookup"><span data-stu-id="555fa-153">In the Azure classic portal, on the **Configure single sign-on at Citrix GoToMeeting** dialog page, copy the **Entity ID** value, and then paste it into the **Identity Provider Entity ID** textbox.</span></span>

    <span data-ttu-id="555fa-154">e.</span><span class="sxs-lookup"><span data-stu-id="555fa-154">e.</span></span> <span data-ttu-id="555fa-155">To upload your downloaded certificate, click **Upload Certificate**.</span><span class="sxs-lookup"><span data-stu-id="555fa-155">To upload your downloaded certificate, click **Upload Certificate**.</span></span>

    <span data-ttu-id="555fa-156">f.</span><span class="sxs-lookup"><span data-stu-id="555fa-156">f.</span></span> <span data-ttu-id="555fa-157">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="555fa-157">Click **Save**.</span></span>


1. <span data-ttu-id="555fa-158">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="555fa-158">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    <span data-ttu-id="555fa-159">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-gotomeeting-tutorial/IC769000.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="555fa-159">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-gotomeeting-tutorial/IC769000.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="555fa-160">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="555fa-160">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="555fa-161">![SAML setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-gotomeeting-tutorial/IC7689982.png "SAML setup")</span><span class="sxs-lookup"><span data-stu-id="555fa-161">![SAML setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-gotomeeting-tutorial/IC7689982.png "SAML setup")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="555fa-162">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="555fa-162">Configuring user provisioning</span></span>
<span data-ttu-id="555fa-163">The objective of this section is to outline how to enable provisioning of Active Directory user accounts to Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="555fa-163">The objective of this section is to outline how to enable provisioning of Active Directory user accounts to Citrix GoToMeeting.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="555fa-164">To configure user provisioning, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="555fa-164">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="555fa-165">In the Azure classic portal, on the **Citrix GoToMeeting** application integration page, click **Configure user provisioning** to open the **Configure User Provisioning** dialog.</span><span class="sxs-lookup"><span data-stu-id="555fa-165">In the Azure classic portal, on the **Citrix GoToMeeting** application integration page, click **Configure user provisioning** to open the **Configure User Provisioning** dialog.</span></span>
   
    <span data-ttu-id="555fa-166">![Configure user provisioning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-gotomeeting-tutorial/IC769001.png "Configure user provisioning")</span><span class="sxs-lookup"><span data-stu-id="555fa-166">![Configure user provisioning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-gotomeeting-tutorial/IC769001.png "Configure user provisioning")</span></span>

2. <span data-ttu-id="555fa-167">On the **Settings and admin credentials** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="555fa-167">On the **Settings and admin credentials** page, perform the following steps:</span></span>
   
    <span data-ttu-id="555fa-168">![Configure user provisioning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-gotomeeting-tutorial/IC769002.png "Configure user provisioning")</span><span class="sxs-lookup"><span data-stu-id="555fa-168">![Configure user provisioning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-gotomeeting-tutorial/IC769002.png "Configure user provisioning")</span></span>
   
    <span data-ttu-id="555fa-169">a.</span><span class="sxs-lookup"><span data-stu-id="555fa-169">a.</span></span> <span data-ttu-id="555fa-170">In the **Citrix GoToMeeting Admin User Name** textbox, type the user name of an administrator.</span><span class="sxs-lookup"><span data-stu-id="555fa-170">In the **Citrix GoToMeeting Admin User Name** textbox, type the user name of an administrator.</span></span>

    <span data-ttu-id="555fa-171">b.</span><span class="sxs-lookup"><span data-stu-id="555fa-171">b.</span></span> <span data-ttu-id="555fa-172">In the **Citrix GoToMeeting Admin Password** textbox, the administrator's password.</span><span class="sxs-lookup"><span data-stu-id="555fa-172">In the **Citrix GoToMeeting Admin Password** textbox, the administrator's password.</span></span>

    <span data-ttu-id="555fa-173">c.</span><span class="sxs-lookup"><span data-stu-id="555fa-173">c.</span></span> <span data-ttu-id="555fa-174">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="555fa-174">Click **Next**.</span></span>

1. <span data-ttu-id="555fa-175">On the **Confirmation** page, click the checkmark to save your configuration.</span><span class="sxs-lookup"><span data-stu-id="555fa-175">On the **Confirmation** page, click the checkmark to save your configuration.</span></span>
2. <span data-ttu-id="555fa-176">Click the **validate** button, to verify your configuration.</span><span class="sxs-lookup"><span data-stu-id="555fa-176">Click the **validate** button, to verify your configuration.</span></span>

## <a name="assigning-users"></a><span data-ttu-id="555fa-177">Assigning users</span><span class="sxs-lookup"><span data-stu-id="555fa-177">Assigning users</span></span>
<span data-ttu-id="555fa-178">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="555fa-178">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-citrix-gotomeeting-perform-the-following-steps"></a><span data-ttu-id="555fa-179">To assign users to Citrix GoToMeeting, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="555fa-179">To assign users to Citrix GoToMeeting, perform the following steps:</span></span>
1. <span data-ttu-id="555fa-180">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="555fa-180">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="555fa-181">On the **Citrix GoToMeeting** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="555fa-181">On the **Citrix GoToMeeting** application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="555fa-182">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-gotomeeting-tutorial/IC769003.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="555fa-182">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-gotomeeting-tutorial/IC769003.png "Assign users")</span></span>

3. <span data-ttu-id="555fa-183">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="555fa-183">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="555fa-184">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-gotomeeting-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="555fa-184">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-gotomeeting-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="555fa-185">You should now wait for 10 minutes and verify that the account has been synchronized to Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="555fa-185">You should now wait for 10 minutes and verify that the account has been synchronized to Dropbox for Business.</span></span>

<span data-ttu-id="555fa-186">As a first verification step, you can check the provisioning status, by clicking Dashboard in the D on the **Citrix GoToMeeting** application integration page on the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="555fa-186">As a first verification step, you can check the provisioning status, by clicking Dashboard in the D on the **Citrix GoToMeeting** application integration page on the Azure classic portal.</span></span>

<span data-ttu-id="555fa-187">![Dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-gotomeeting-tutorial/IC769004.png "Dashboard")</span><span class="sxs-lookup"><span data-stu-id="555fa-187">![Dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-gotomeeting-tutorial/IC769004.png "Dashboard")</span></span>

<span data-ttu-id="555fa-188">A successfully completed user provisioning cycle is indicated by a related status:</span><span class="sxs-lookup"><span data-stu-id="555fa-188">A successfully completed user provisioning cycle is indicated by a related status:</span></span>

<span data-ttu-id="555fa-189">![Integration status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-gotomeeting-tutorial/IC769005.png "Integration status")</span><span class="sxs-lookup"><span data-stu-id="555fa-189">![Integration status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-gotomeeting-tutorial/IC769005.png "Integration status")</span></span>

<span data-ttu-id="555fa-190">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="555fa-190">If you want to test your single sign-on settings, open the Access Panel.</span></span>

<span data-ttu-id="555fa-191">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="555fa-191">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>





















