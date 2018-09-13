---
title: 'Tutorial: Azure Active Directory integration with Work.com | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Work.com.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 98e6739e-eb24-46bd-9dd3-20b489839076
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: f4247a24905b5865635495774412237118e3372a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856975"
---
# <a name="tutorial-azure-active-directory-integration-with-workcom"></a><span data-ttu-id="150b0-103">Tutorial: Azure Active Directory integration with Work.com</span><span class="sxs-lookup"><span data-stu-id="150b0-103">Tutorial: Azure Active Directory integration with Work.com</span></span>

<span data-ttu-id="150b0-104">In this tutorial, you learn how to integrate Work.com with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="150b0-104">In this tutorial, you learn how to integrate Work.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="150b0-105">Integrating Work.com with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="150b0-105">Integrating Work.com with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="150b0-106">You can control in Azure AD who has access to Work.com</span><span class="sxs-lookup"><span data-stu-id="150b0-106">You can control in Azure AD who has access to Work.com</span></span>
- <span data-ttu-id="150b0-107">You can enable your users to automatically get signed-on to Work.com (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="150b0-107">You can enable your users to automatically get signed-on to Work.com (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="150b0-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="150b0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="150b0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="150b0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="150b0-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="150b0-110">Prerequisites</span></span>

<span data-ttu-id="150b0-111">To configure Azure AD integration with Work.com, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="150b0-111">To configure Azure AD integration with Work.com, you need the following items:</span></span>

- <span data-ttu-id="150b0-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="150b0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="150b0-113">A Work.com single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="150b0-113">A Work.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="150b0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="150b0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="150b0-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="150b0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="150b0-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="150b0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="150b0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="150b0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="150b0-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="150b0-118">Scenario description</span></span>
<span data-ttu-id="150b0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="150b0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="150b0-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="150b0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="150b0-121">Add Work.com from the gallery</span><span class="sxs-lookup"><span data-stu-id="150b0-121">Add Work.com from the gallery</span></span>
1. <span data-ttu-id="150b0-122">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="150b0-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-workcom-from-the-gallery"></a><span data-ttu-id="150b0-123">Add Work.com from the gallery</span><span class="sxs-lookup"><span data-stu-id="150b0-123">Add Work.com from the gallery</span></span>
<span data-ttu-id="150b0-124">To configure the integration of Work.com into Azure AD, you need to add Work.com from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="150b0-124">To configure the integration of Work.com into Azure AD, you need to add Work.com from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="150b0-125">**To add Work.com from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="150b0-125">**To add Work.com from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="150b0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="150b0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="150b0-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="150b0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="150b0-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="150b0-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="150b0-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="150b0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="150b0-133">In the search box, type **Work.com**, select **Work.com** from results panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="150b0-133">In the search box, type **Work.com**, select **Work.com** from results panel then click **Add** button to add the application.</span></span>

    ![Add from gallery](./media/work-com-tutorial/tutorial_work-com_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="150b0-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="150b0-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="150b0-136">In this section, you configure and test Azure AD single sign-on with Work.com based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="150b0-136">In this section, you configure and test Azure AD single sign-on with Work.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="150b0-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Work.com is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="150b0-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Work.com is to a user in Azure AD.</span></span> <span data-ttu-id="150b0-138">In other words, a link relationship between an Azure AD user and the related user in Work.com needs to be established.</span><span class="sxs-lookup"><span data-stu-id="150b0-138">In other words, a link relationship between an Azure AD user and the related user in Work.com needs to be established.</span></span>

<span data-ttu-id="150b0-139">In Work.com, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="150b0-139">In Work.com, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="150b0-140">To configure and test Azure AD single sign-on with Work.com, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="150b0-140">To configure and test Azure AD single sign-on with Work.com, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="150b0-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="150b0-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="150b0-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="150b0-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="150b0-143">**[Create a Work.com test user](#create-a-workcom-test-user)** - to have a counterpart of Britta Simon in Work.com that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="150b0-143">**[Create a Work.com test user](#create-a-workcom-test-user)** - to have a counterpart of Britta Simon in Work.com that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="150b0-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="150b0-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="150b0-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="150b0-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="150b0-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="150b0-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="150b0-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Work.com application.</span><span class="sxs-lookup"><span data-stu-id="150b0-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Work.com application.</span></span>

>[!NOTE]
><span data-ttu-id="150b0-148">To configure single sign-on, you need to setup a custom Work.com domain name yet.</span><span class="sxs-lookup"><span data-stu-id="150b0-148">To configure single sign-on, you need to setup a custom Work.com domain name yet.</span></span> <span data-ttu-id="150b0-149">You need to define at least a domain name, test your domain name, and deploy it to your entire organization.</span><span class="sxs-lookup"><span data-stu-id="150b0-149">You need to define at least a domain name, test your domain name, and deploy it to your entire organization.</span></span>

<span data-ttu-id="150b0-150">**To configure Azure AD single sign-on with Work.com, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="150b0-150">**To configure Azure AD single sign-on with Work.com, perform the following steps:**</span></span>

1. <span data-ttu-id="150b0-151">In the Azure portal, on the **Work.com** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="150b0-151">In the Azure portal, on the **Work.com** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="150b0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="150b0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![SAML-based Sign-on](./media/work-com-tutorial/tutorial_work-com_samlbase.png)

1. <span data-ttu-id="150b0-155">On the **Work.com Domain and URLs** section, perform the following:</span><span class="sxs-lookup"><span data-stu-id="150b0-155">On the **Work.com Domain and URLs** section, perform the following:</span></span>

    ![Work.com Domain and URLs section](./media/work-com-tutorial/tutorial_work-com_url.png)

    <span data-ttu-id="150b0-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://<companyname>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="150b0-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://<companyname>.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="150b0-158">This value is not real.</span><span class="sxs-lookup"><span data-stu-id="150b0-158">This value is not real.</span></span> <span data-ttu-id="150b0-159">Update this value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="150b0-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="150b0-160">Contact [Work.com Client support team](https://help.salesforce.com/articleView?id=000159855&type=3) to get this value.</span><span class="sxs-lookup"><span data-stu-id="150b0-160">Contact [Work.com Client support team](https://help.salesforce.com/articleView?id=000159855&type=3) to get this value.</span></span> 

1. <span data-ttu-id="150b0-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="150b0-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![SAML Signing Certificate section](./media/work-com-tutorial/tutorial_work-com_certificate.png) 

1. <span data-ttu-id="150b0-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="150b0-163">Click **Save** button.</span></span>

    ![Save Button](./media/work-com-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="150b0-165">On the **Work.com Configuration** section, click **Configure Work.com** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="150b0-165">On the **Work.com Configuration** section, click **Configure Work.com** to open **Configure sign-on** window.</span></span> <span data-ttu-id="150b0-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="150b0-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Work.com Configuration section](./media/work-com-tutorial/tutorial_work-com_configure.png) 
1. <span data-ttu-id="150b0-168">Log in to your Work.com tenant as administrator.</span><span class="sxs-lookup"><span data-stu-id="150b0-168">Log in to your Work.com tenant as administrator.</span></span>

1. <span data-ttu-id="150b0-169">Go to **Setup**.</span><span class="sxs-lookup"><span data-stu-id="150b0-169">Go to **Setup**.</span></span>
   
    <span data-ttu-id="150b0-170">![Setup](./media/work-com-tutorial/ic794108.png "Setup")</span><span class="sxs-lookup"><span data-stu-id="150b0-170">![Setup](./media/work-com-tutorial/ic794108.png "Setup")</span></span>

1. <span data-ttu-id="150b0-171">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span><span class="sxs-lookup"><span data-stu-id="150b0-171">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
   
    <span data-ttu-id="150b0-172">![My Domain](./media/work-com-tutorial/ic767825.png "My Domain")</span><span class="sxs-lookup"><span data-stu-id="150b0-172">![My Domain](./media/work-com-tutorial/ic767825.png "My Domain")</span></span>

1. <span data-ttu-id="150b0-173">To verify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed to Users**” and review your “**My Domain Settings**”.</span><span class="sxs-lookup"><span data-stu-id="150b0-173">To verify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed to Users**” and review your “**My Domain Settings**”.</span></span>
   
    <span data-ttu-id="150b0-174">![Domain Deployed to User](./media/work-com-tutorial/ic784377.png "Domain Deployed to User")</span><span class="sxs-lookup"><span data-stu-id="150b0-174">![Domain Deployed to User](./media/work-com-tutorial/ic784377.png "Domain Deployed to User")</span></span>

1. <span data-ttu-id="150b0-175">Log in to your Work.com tenant.</span><span class="sxs-lookup"><span data-stu-id="150b0-175">Log in to your Work.com tenant.</span></span>

1. <span data-ttu-id="150b0-176">Go to **Setup**.</span><span class="sxs-lookup"><span data-stu-id="150b0-176">Go to **Setup**.</span></span>
    
    <span data-ttu-id="150b0-177">![Setup](./media/work-com-tutorial/ic794108.png "Setup")</span><span class="sxs-lookup"><span data-stu-id="150b0-177">![Setup](./media/work-com-tutorial/ic794108.png "Setup")</span></span>

1. <span data-ttu-id="150b0-178">Expand the **Security Controls** menu, and then click **Single Sign-On Settings**.</span><span class="sxs-lookup"><span data-stu-id="150b0-178">Expand the **Security Controls** menu, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="150b0-179">![Single Sign-On Settings](./media/work-com-tutorial/ic794113.png "Single Sign-On Settings")</span><span class="sxs-lookup"><span data-stu-id="150b0-179">![Single Sign-On Settings](./media/work-com-tutorial/ic794113.png "Single Sign-On Settings")</span></span>

1. <span data-ttu-id="150b0-180">On the **Single Sign-On Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="150b0-180">On the **Single Sign-On Settings** dialog page, perform the following steps:</span></span>
    
    <span data-ttu-id="150b0-181">![SAML Enabled](./media/work-com-tutorial/ic781026.png "SAML Enabled")</span><span class="sxs-lookup"><span data-stu-id="150b0-181">![SAML Enabled](./media/work-com-tutorial/ic781026.png "SAML Enabled")</span></span>
    
    <span data-ttu-id="150b0-182">a.</span><span class="sxs-lookup"><span data-stu-id="150b0-182">a.</span></span> <span data-ttu-id="150b0-183">Select **SAML Enabled**.</span><span class="sxs-lookup"><span data-stu-id="150b0-183">Select **SAML Enabled**.</span></span>
    
    <span data-ttu-id="150b0-184">b.</span><span class="sxs-lookup"><span data-stu-id="150b0-184">b.</span></span> <span data-ttu-id="150b0-185">Click **New**.</span><span class="sxs-lookup"><span data-stu-id="150b0-185">Click **New**.</span></span>

1. <span data-ttu-id="150b0-186">In the **SAML Single Sign-On Settings** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="150b0-186">In the **SAML Single Sign-On Settings** section, perform the following steps:</span></span>
    
    <span data-ttu-id="150b0-187">![SAML Single Sign-On Setting](./media/work-com-tutorial/ic794114.png "SAML Single Sign-On Setting")</span><span class="sxs-lookup"><span data-stu-id="150b0-187">![SAML Single Sign-On Setting](./media/work-com-tutorial/ic794114.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="150b0-188">a.</span><span class="sxs-lookup"><span data-stu-id="150b0-188">a.</span></span> <span data-ttu-id="150b0-189">In the **Name** textbox, type a name for your configuration.</span><span class="sxs-lookup"><span data-stu-id="150b0-189">In the **Name** textbox, type a name for your configuration.</span></span>  
       
    > [!NOTE]
    > <span data-ttu-id="150b0-190">Providing a value for **Name** does automatically populate the **API Name** textbox.</span><span class="sxs-lookup"><span data-stu-id="150b0-190">Providing a value for **Name** does automatically populate the **API Name** textbox.</span></span>
    
    <span data-ttu-id="150b0-191">b.</span><span class="sxs-lookup"><span data-stu-id="150b0-191">b.</span></span> <span data-ttu-id="150b0-192">In **Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="150b0-192">In **Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="150b0-193">c.</span><span class="sxs-lookup"><span data-stu-id="150b0-193">c.</span></span> <span data-ttu-id="150b0-194">To upload the downloaded certificate from Azure portal, click **Browse**.</span><span class="sxs-lookup"><span data-stu-id="150b0-194">To upload the downloaded certificate from Azure portal, click **Browse**.</span></span>
    
    <span data-ttu-id="150b0-195">d.</span><span class="sxs-lookup"><span data-stu-id="150b0-195">d.</span></span> <span data-ttu-id="150b0-196">In the **Entity Id** textbox, type `https://salesforce-work.com`.</span><span class="sxs-lookup"><span data-stu-id="150b0-196">In the **Entity Id** textbox, type `https://salesforce-work.com`.</span></span>
    
    <span data-ttu-id="150b0-197">e.</span><span class="sxs-lookup"><span data-stu-id="150b0-197">e.</span></span> <span data-ttu-id="150b0-198">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span><span class="sxs-lookup"><span data-stu-id="150b0-198">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span>
    
    <span data-ttu-id="150b0-199">f.</span><span class="sxs-lookup"><span data-stu-id="150b0-199">f.</span></span> <span data-ttu-id="150b0-200">As **SAML Identity Location**, select **Identity is in the NameIdentfier element of the Subject statement**.</span><span class="sxs-lookup"><span data-stu-id="150b0-200">As **SAML Identity Location**, select **Identity is in the NameIdentfier element of the Subject statement**.</span></span>
    
    <span data-ttu-id="150b0-201">g.</span><span class="sxs-lookup"><span data-stu-id="150b0-201">g.</span></span> <span data-ttu-id="150b0-202">In **Identity Provider Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="150b0-202">In **Identity Provider Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="150b0-203">h.</span><span class="sxs-lookup"><span data-stu-id="150b0-203">h.</span></span> <span data-ttu-id="150b0-204">In **Identity Provider Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="150b0-204">In **Identity Provider Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="150b0-205">i.</span><span class="sxs-lookup"><span data-stu-id="150b0-205">i.</span></span> <span data-ttu-id="150b0-206">As **Service Provider Initiated Request Binding**, select **HTTP Post**.</span><span class="sxs-lookup"><span data-stu-id="150b0-206">As **Service Provider Initiated Request Binding**, select **HTTP Post**.</span></span>
    
    <span data-ttu-id="150b0-207">j.</span><span class="sxs-lookup"><span data-stu-id="150b0-207">j.</span></span> <span data-ttu-id="150b0-208">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="150b0-208">Click **Save**.</span></span>

1. <span data-ttu-id="150b0-209">In your Work.com classic portal, on the left navigation pane, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span><span class="sxs-lookup"><span data-stu-id="150b0-209">In your Work.com classic portal, on the left navigation pane, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
    
    <span data-ttu-id="150b0-210">![My Domain](./media/work-com-tutorial/ic794115.png "My Domain")</span><span class="sxs-lookup"><span data-stu-id="150b0-210">![My Domain](./media/work-com-tutorial/ic794115.png "My Domain")</span></span>

1. <span data-ttu-id="150b0-211">On the **My Domain** page, in the **Login Page Branding** section, click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="150b0-211">On the **My Domain** page, in the **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="150b0-212">![Login Page Branding](./media/work-com-tutorial/ic767826.png "Login Page Branding")</span><span class="sxs-lookup"><span data-stu-id="150b0-212">![Login Page Branding](./media/work-com-tutorial/ic767826.png "Login Page Branding")</span></span>

1. <span data-ttu-id="150b0-213">On the **Login Page Branding** page, in the **Authentication Service** section, the name of your **SAML SSO Settings** is displayed.</span><span class="sxs-lookup"><span data-stu-id="150b0-213">On the **Login Page Branding** page, in the **Authentication Service** section, the name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="150b0-214">Select it, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="150b0-214">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="150b0-215">![Login Page Branding](./media/work-com-tutorial/ic784366.png "Login Page Branding")</span><span class="sxs-lookup"><span data-stu-id="150b0-215">![Login Page Branding](./media/work-com-tutorial/ic784366.png "Login Page Branding")</span></span>

> [!TIP]
> <span data-ttu-id="150b0-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="150b0-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="150b0-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="150b0-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="150b0-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="150b0-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="150b0-219">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="150b0-219">Create an Azure AD test user</span></span>
<span data-ttu-id="150b0-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="150b0-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="150b0-222">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="150b0-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="150b0-223">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="150b0-223">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/work-com-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="150b0-225">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="150b0-225">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Users and groups -> All users](./media/work-com-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="150b0-227">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="150b0-227">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Add](./media/work-com-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="150b0-229">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="150b0-229">On the **User** dialog page, perform the following steps:</span></span>
 
    ![User dialog page](./media/work-com-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="150b0-231">a.</span><span class="sxs-lookup"><span data-stu-id="150b0-231">a.</span></span> <span data-ttu-id="150b0-232">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="150b0-232">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="150b0-233">b.</span><span class="sxs-lookup"><span data-stu-id="150b0-233">b.</span></span> <span data-ttu-id="150b0-234">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="150b0-234">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="150b0-235">c.</span><span class="sxs-lookup"><span data-stu-id="150b0-235">c.</span></span> <span data-ttu-id="150b0-236">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="150b0-236">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="150b0-237">d.</span><span class="sxs-lookup"><span data-stu-id="150b0-237">d.</span></span> <span data-ttu-id="150b0-238">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="150b0-238">Click **Create**.</span></span>
 
### <a name="create-a-workcom-test-user"></a><span data-ttu-id="150b0-239">Create a Work.com test user</span><span class="sxs-lookup"><span data-stu-id="150b0-239">Create a Work.com test user</span></span>
<span data-ttu-id="150b0-240">For Azure Active Directory users to be able to sign in, they must be provisioned to Work.com.</span><span class="sxs-lookup"><span data-stu-id="150b0-240">For Azure Active Directory users to be able to sign in, they must be provisioned to Work.com.</span></span> <span data-ttu-id="150b0-241">In the case of Work.com, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="150b0-241">In the case of Work.com, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="150b0-242">To configure user provisioning, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="150b0-242">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="150b0-243">Sign on to your Work.com company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="150b0-243">Sign on to your Work.com company site as an administrator.</span></span>

1. <span data-ttu-id="150b0-244">Go to **Setup**.</span><span class="sxs-lookup"><span data-stu-id="150b0-244">Go to **Setup**.</span></span>
   
    <span data-ttu-id="150b0-245">![Setup](./media/work-com-tutorial/IC794108.png "Setup")</span><span class="sxs-lookup"><span data-stu-id="150b0-245">![Setup](./media/work-com-tutorial/IC794108.png "Setup")</span></span>
1. <span data-ttu-id="150b0-246">Go to **Manage Users \> Users**.</span><span class="sxs-lookup"><span data-stu-id="150b0-246">Go to **Manage Users \> Users**.</span></span>
   
    <span data-ttu-id="150b0-247">![Manage Users](./media/work-com-tutorial/IC784369.png "Manage Users")</span><span class="sxs-lookup"><span data-stu-id="150b0-247">![Manage Users](./media/work-com-tutorial/IC784369.png "Manage Users")</span></span>

1. <span data-ttu-id="150b0-248">Click **New User**.</span><span class="sxs-lookup"><span data-stu-id="150b0-248">Click **New User**.</span></span>
   
    <span data-ttu-id="150b0-249">![All Users](./media/work-com-tutorial/IC794117.png "All Users")</span><span class="sxs-lookup"><span data-stu-id="150b0-249">![All Users](./media/work-com-tutorial/IC794117.png "All Users")</span></span>

1. <span data-ttu-id="150b0-250">In the User Edit section, perform the following steps, in attributes of a valid Azure AD account you want to provision into the related textboxes:</span><span class="sxs-lookup"><span data-stu-id="150b0-250">In the User Edit section, perform the following steps, in attributes of a valid Azure AD account you want to provision into the related textboxes:</span></span>
   
    <span data-ttu-id="150b0-251">![User Edit](./media/work-com-tutorial/ic794118.png "User Edit")</span><span class="sxs-lookup"><span data-stu-id="150b0-251">![User Edit](./media/work-com-tutorial/ic794118.png "User Edit")</span></span>
   
    <span data-ttu-id="150b0-252">a.</span><span class="sxs-lookup"><span data-stu-id="150b0-252">a.</span></span> <span data-ttu-id="150b0-253">In the **First Name** textbox, type the **first name** of the user **Britta**.</span><span class="sxs-lookup"><span data-stu-id="150b0-253">In the **First Name** textbox, type the **first name** of the user **Britta**.</span></span>
    
    <span data-ttu-id="150b0-254">b.</span><span class="sxs-lookup"><span data-stu-id="150b0-254">b.</span></span> <span data-ttu-id="150b0-255">In the **Last Name** textbox, type the **last name** of the user **Simon**.</span><span class="sxs-lookup"><span data-stu-id="150b0-255">In the **Last Name** textbox, type the **last name** of the user **Simon**.</span></span>
    
    <span data-ttu-id="150b0-256">c.</span><span class="sxs-lookup"><span data-stu-id="150b0-256">c.</span></span> <span data-ttu-id="150b0-257">In the **Alias** textbox, type the **name** of the user **BrittaS**.</span><span class="sxs-lookup"><span data-stu-id="150b0-257">In the **Alias** textbox, type the **name** of the user **BrittaS**.</span></span>
    
    <span data-ttu-id="150b0-258">d.</span><span class="sxs-lookup"><span data-stu-id="150b0-258">d.</span></span> <span data-ttu-id="150b0-259">In the **Email** textbox, type the **email address** of user **Brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="150b0-259">In the **Email** textbox, type the **email address** of user **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="150b0-260">e.</span><span class="sxs-lookup"><span data-stu-id="150b0-260">e.</span></span> <span data-ttu-id="150b0-261">In the **User Name** textbox, type a user name of user like **Brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="150b0-261">In the **User Name** textbox, type a user name of user like **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="150b0-262">f.</span><span class="sxs-lookup"><span data-stu-id="150b0-262">f.</span></span> <span data-ttu-id="150b0-263">In the **Nick Name** textbox, type a **nick name** of user **Simon**.</span><span class="sxs-lookup"><span data-stu-id="150b0-263">In the **Nick Name** textbox, type a **nick name** of user **Simon**.</span></span>
    
    <span data-ttu-id="150b0-264">g.</span><span class="sxs-lookup"><span data-stu-id="150b0-264">g.</span></span> <span data-ttu-id="150b0-265">Select **Role**, **User License**, and **Profile**.</span><span class="sxs-lookup"><span data-stu-id="150b0-265">Select **Role**, **User License**, and **Profile**.</span></span>
    
    <span data-ttu-id="150b0-266">h.</span><span class="sxs-lookup"><span data-stu-id="150b0-266">h.</span></span> <span data-ttu-id="150b0-267">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="150b0-267">Click **Save**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="150b0-268">The Azure AD account holder will get an email including a link to confirm the account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="150b0-268">The Azure AD account holder will get an email including a link to confirm the account before it becomes active.</span></span>
    > 
    > 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="150b0-269">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="150b0-269">Assign the Azure AD test user</span></span>

<span data-ttu-id="150b0-270">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Work.com.</span><span class="sxs-lookup"><span data-stu-id="150b0-270">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Work.com.</span></span>

![Assign User][200] 

<span data-ttu-id="150b0-272">**To assign Britta Simon to Work.com, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="150b0-272">**To assign Britta Simon to Work.com, perform the following steps:**</span></span>

1. <span data-ttu-id="150b0-273">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="150b0-273">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="150b0-275">In the applications list, select **Work.com**.</span><span class="sxs-lookup"><span data-stu-id="150b0-275">In the applications list, select **Work.com**.</span></span>

    ![Work.com in app's list](./media/work-com-tutorial/tutorial_work-com_app.png) 

1. <span data-ttu-id="150b0-277">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="150b0-277">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="150b0-279">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="150b0-279">Click **Add** button.</span></span> <span data-ttu-id="150b0-280">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="150b0-280">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="150b0-282">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="150b0-282">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="150b0-283">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="150b0-283">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="150b0-284">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="150b0-284">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="150b0-285">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="150b0-285">Test single sign-on</span></span>

<span data-ttu-id="150b0-286">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="150b0-286">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="150b0-287">When you click the Work.com tile in the Access Panel, you should get automatically signed-on to your Work.com application.</span><span class="sxs-lookup"><span data-stu-id="150b0-287">When you click the Work.com tile in the Access Panel, you should get automatically signed-on to your Work.com application.</span></span>
<span data-ttu-id="150b0-288">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="150b0-288">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="150b0-289">Additional resources</span><span class="sxs-lookup"><span data-stu-id="150b0-289">Additional resources</span></span>

* [<span data-ttu-id="150b0-290">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="150b0-290">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="150b0-291">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="150b0-291">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)


<!--Image references-->

[1]: ./media/work-com-tutorial/tutorial_general_01.png
[2]: ./media/work-com-tutorial/tutorial_general_02.png
[3]: ./media/work-com-tutorial/tutorial_general_03.png
[4]: ./media/work-com-tutorial/tutorial_general_04.png

[100]: ./media/work-com-tutorial/tutorial_general_100.png

[200]: ./media/work-com-tutorial/tutorial_general_200.png
[201]: ./media/work-com-tutorial/tutorial_general_201.png
[202]: ./media/work-com-tutorial/tutorial_general_202.png
[203]: ./media/work-com-tutorial/tutorial_general_203.png

