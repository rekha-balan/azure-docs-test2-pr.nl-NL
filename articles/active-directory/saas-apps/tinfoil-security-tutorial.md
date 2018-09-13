---
title: 'Tutorial: Azure Active Directory integration with TINFOIL SECURITY | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and TINFOIL SECURITY.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: da02da92-e3b0-4c09-ad6c-180882b0f9f8
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 4f25768cc7e4f5865c6cfa96ebfe3b0df97deeb6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857083"
---
# <a name="tutorial-azure-active-directory-integration-with-tinfoil-security"></a><span data-ttu-id="7facf-103">Tutorial: Azure Active Directory integration with TINFOIL SECURITY</span><span class="sxs-lookup"><span data-stu-id="7facf-103">Tutorial: Azure Active Directory integration with TINFOIL SECURITY</span></span>

<span data-ttu-id="7facf-104">In this tutorial, you learn how to integrate TINFOIL SECURITY with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7facf-104">In this tutorial, you learn how to integrate TINFOIL SECURITY with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7facf-105">Integrating TINFOIL SECURITY with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="7facf-105">Integrating TINFOIL SECURITY with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7facf-106">You can control in Azure AD who has access to TINFOIL SECURITY</span><span class="sxs-lookup"><span data-stu-id="7facf-106">You can control in Azure AD who has access to TINFOIL SECURITY</span></span>
- <span data-ttu-id="7facf-107">You can enable your users to automatically get signed-on to TINFOIL SECURITY (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="7facf-107">You can enable your users to automatically get signed-on to TINFOIL SECURITY (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7facf-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="7facf-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7facf-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="7facf-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7facf-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7facf-110">Prerequisites</span></span>

<span data-ttu-id="7facf-111">To configure Azure AD integration with TINFOIL SECURITY, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="7facf-111">To configure Azure AD integration with TINFOIL SECURITY, you need the following items:</span></span>

- <span data-ttu-id="7facf-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="7facf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7facf-113">A TINFOIL SECURITY single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="7facf-113">A TINFOIL SECURITY single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7facf-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="7facf-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7facf-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="7facf-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7facf-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="7facf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7facf-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7facf-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7facf-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="7facf-118">Scenario description</span></span>
<span data-ttu-id="7facf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="7facf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7facf-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="7facf-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7facf-121">Add TINFOIL SECURITY from the gallery</span><span class="sxs-lookup"><span data-stu-id="7facf-121">Add TINFOIL SECURITY from the gallery</span></span>
1. <span data-ttu-id="7facf-122">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7facf-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tinfoil-security-from-the-gallery"></a><span data-ttu-id="7facf-123">Add TINFOIL SECURITY from the gallery</span><span class="sxs-lookup"><span data-stu-id="7facf-123">Add TINFOIL SECURITY from the gallery</span></span>
<span data-ttu-id="7facf-124">To configure the integration of TINFOIL SECURITY into Azure AD, you need to add TINFOIL SECURITY from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="7facf-124">To configure the integration of TINFOIL SECURITY into Azure AD, you need to add TINFOIL SECURITY from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7facf-125">**To add TINFOIL SECURITY from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7facf-125">**To add TINFOIL SECURITY from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7facf-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="7facf-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="7facf-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="7facf-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7facf-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="7facf-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="7facf-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="7facf-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="7facf-133">In the search box, type **TINFOIL SECURITY**, select  **TINFOIL SECURITY** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="7facf-133">In the search box, type **TINFOIL SECURITY**, select  **TINFOIL SECURITY** from result panel then click **Add** button to add the application.</span></span>

    ![TINFOIL SECURITY from gallery](./media/tinfoil-security-tutorial/tutorial_tinfoil-security_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7facf-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7facf-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="7facf-136">In this section, you configure and test Azure AD single sign-on with TINFOIL SECURITY based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7facf-136">In this section, you configure and test Azure AD single sign-on with TINFOIL SECURITY based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7facf-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TINFOIL SECURITY is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7facf-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TINFOIL SECURITY is to a user in Azure AD.</span></span> <span data-ttu-id="7facf-138">In other words, a link relationship between an Azure AD user and the related user in TINFOIL SECURITY needs to be established.</span><span class="sxs-lookup"><span data-stu-id="7facf-138">In other words, a link relationship between an Azure AD user and the related user in TINFOIL SECURITY needs to be established.</span></span>

<span data-ttu-id="7facf-139">In TINFOIL SECURITY, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="7facf-139">In TINFOIL SECURITY, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7facf-140">To configure and test Azure AD single sign-on with TINFOIL SECURITY, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="7facf-140">To configure and test Azure AD single sign-on with TINFOIL SECURITY, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7facf-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="7facf-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="7facf-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7facf-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="7facf-143">**[Create a TINFOIL SECURITY test user](#create-a-tinfoil-security-test-user)** - to have a counterpart of Britta Simon in TINFOIL SECURITY that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="7facf-143">**[Create a TINFOIL SECURITY test user](#create-a-tinfoil-security-test-user)** - to have a counterpart of Britta Simon in TINFOIL SECURITY that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="7facf-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7facf-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="7facf-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="7facf-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7facf-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7facf-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7facf-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TINFOIL SECURITY application.</span><span class="sxs-lookup"><span data-stu-id="7facf-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TINFOIL SECURITY application.</span></span>

<span data-ttu-id="7facf-148">**To configure Azure AD single sign-on with TINFOIL SECURITY, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7facf-148">**To configure Azure AD single sign-on with TINFOIL SECURITY, perform the following steps:**</span></span>

1. <span data-ttu-id="7facf-149">In the Azure portal, on the **TINFOIL SECURITY** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="7facf-149">In the Azure portal, on the **TINFOIL SECURITY** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="7facf-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7facf-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![SAML based Sign-on](./media/tinfoil-security-tutorial/tutorial_tinfoil-security_samlbase.png)

1. <span data-ttu-id="7facf-153">On the **TINFOIL SECURITY Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span><span class="sxs-lookup"><span data-stu-id="7facf-153">On the **TINFOIL SECURITY Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Configure Single Sign-On](./media/tinfoil-security-tutorial/tutorial_tinfoil-security_url.png)


1. <span data-ttu-id="7facf-155">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value.</span><span class="sxs-lookup"><span data-stu-id="7facf-155">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value.</span></span>

    ![SAML Signing Certificate section](./media/tinfoil-security-tutorial/tutorial_tinfoil-security_certificate.png) 

1. <span data-ttu-id="7facf-157">To add the required attribute mappings, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7facf-157">To add the required attribute mappings, perform the following steps:</span></span>
    
    <span data-ttu-id="7facf-158">![Attributes](./media/tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "Attributes")</span><span class="sxs-lookup"><span data-stu-id="7facf-158">![Attributes](./media/tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "Attributes")</span></span>
    
    | <span data-ttu-id="7facf-159">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="7facf-159">Attribute Name</span></span>    |   <span data-ttu-id="7facf-160">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="7facf-160">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="7facf-161">accountid</span><span class="sxs-lookup"><span data-stu-id="7facf-161">accountid</span></span> | <span data-ttu-id="7facf-162">UXXXXXXXXXXXXX</span><span class="sxs-lookup"><span data-stu-id="7facf-162">UXXXXXXXXXXXXX</span></span> |
    
    <span data-ttu-id="7facf-163">a.</span><span class="sxs-lookup"><span data-stu-id="7facf-163">a.</span></span> <span data-ttu-id="7facf-164">Click **add user attribute**.</span><span class="sxs-lookup"><span data-stu-id="7facf-164">Click **add user attribute**.</span></span>
    
    <span data-ttu-id="7facf-165">![ADD Attribute](./media/tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "Attributes")</span><span class="sxs-lookup"><span data-stu-id="7facf-165">![ADD Attribute](./media/tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "Attributes")</span></span>
    
    <span data-ttu-id="7facf-166">![ADD Attribute](./media/tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "Attributes")</span><span class="sxs-lookup"><span data-stu-id="7facf-166">![ADD Attribute](./media/tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "Attributes")</span></span>
    
    <span data-ttu-id="7facf-167">b.</span><span class="sxs-lookup"><span data-stu-id="7facf-167">b.</span></span> <span data-ttu-id="7facf-168">In the **Attribute Name** textbox, type **accountid**.</span><span class="sxs-lookup"><span data-stu-id="7facf-168">In the **Attribute Name** textbox, type **accountid**.</span></span>
    
    <span data-ttu-id="7facf-169">c.</span><span class="sxs-lookup"><span data-stu-id="7facf-169">c.</span></span> <span data-ttu-id="7facf-170">In the **Attribute Value** textbox, paste the account ID value which you will get later on the tutorial.</span><span class="sxs-lookup"><span data-stu-id="7facf-170">In the **Attribute Value** textbox, paste the account ID value which you will get later on the tutorial.</span></span>
    
    <span data-ttu-id="7facf-171">d.</span><span class="sxs-lookup"><span data-stu-id="7facf-171">d.</span></span> <span data-ttu-id="7facf-172">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="7facf-172">Click **Ok**.</span></span>    

1. <span data-ttu-id="7facf-173">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="7facf-173">Click **Save** button.</span></span>

    ![Save button](./media/tinfoil-security-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="7facf-175">On the **TINFOIL SECURITY Configuration** section, click **Configure TINFOIL SECURITY** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="7facf-175">On the **TINFOIL SECURITY Configuration** section, click **Configure TINFOIL SECURITY** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7facf-176">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="7facf-176">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![TINFOIL SECURITY Configuration](./media/tinfoil-security-tutorial/tutorial_tinfoil-security_configure.png) 

1. <span data-ttu-id="7facf-178">In a different web browser window, log into your TINFOIL SECURITY company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="7facf-178">In a different web browser window, log into your TINFOIL SECURITY company site as an administrator.</span></span>

1. <span data-ttu-id="7facf-179">In the toolbar on the top, click **My Account**.</span><span class="sxs-lookup"><span data-stu-id="7facf-179">In the toolbar on the top, click **My Account**.</span></span>
   
    <span data-ttu-id="7facf-180">![Dashboard](./media/tinfoil-security-tutorial/ic798971.png "Dashboard")</span><span class="sxs-lookup"><span data-stu-id="7facf-180">![Dashboard](./media/tinfoil-security-tutorial/ic798971.png "Dashboard")</span></span>

1. <span data-ttu-id="7facf-181">Click **Security**.</span><span class="sxs-lookup"><span data-stu-id="7facf-181">Click **Security**.</span></span>
   
    <span data-ttu-id="7facf-182">![Security](./media/tinfoil-security-tutorial/ic798972.png "Security")</span><span class="sxs-lookup"><span data-stu-id="7facf-182">![Security](./media/tinfoil-security-tutorial/ic798972.png "Security")</span></span>

1. <span data-ttu-id="7facf-183">On the **Single Sign-On** configuration page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7facf-183">On the **Single Sign-On** configuration page, perform the following steps:</span></span>
   
    <span data-ttu-id="7facf-184">![Single Sign-On](./media/tinfoil-security-tutorial/ic798973.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="7facf-184">![Single Sign-On](./media/tinfoil-security-tutorial/ic798973.png "Single Sign-On")</span></span>
   
    <span data-ttu-id="7facf-185">a.</span><span class="sxs-lookup"><span data-stu-id="7facf-185">a.</span></span> <span data-ttu-id="7facf-186">Select **Enable SAML**.</span><span class="sxs-lookup"><span data-stu-id="7facf-186">Select **Enable SAML**.</span></span>
   
    <span data-ttu-id="7facf-187">b.</span><span class="sxs-lookup"><span data-stu-id="7facf-187">b.</span></span> <span data-ttu-id="7facf-188">Click **Manual Configuration**.</span><span class="sxs-lookup"><span data-stu-id="7facf-188">Click **Manual Configuration**.</span></span>
   
    <span data-ttu-id="7facf-189">c.</span><span class="sxs-lookup"><span data-stu-id="7facf-189">c.</span></span> <span data-ttu-id="7facf-190">In **SAML Post URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal</span><span class="sxs-lookup"><span data-stu-id="7facf-190">In **SAML Post URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal</span></span>
   
    <span data-ttu-id="7facf-191">d.</span><span class="sxs-lookup"><span data-stu-id="7facf-191">d.</span></span> <span data-ttu-id="7facf-192">In **SAML Certificate Fingerprint** textbox, paste the value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span><span class="sxs-lookup"><span data-stu-id="7facf-192">In **SAML Certificate Fingerprint** textbox, paste the value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span></span>
  
    <span data-ttu-id="7facf-193">e.</span><span class="sxs-lookup"><span data-stu-id="7facf-193">e.</span></span> <span data-ttu-id="7facf-194">Copy **Your Account ID** value and paste the value in **Attribute Value** textbox under **Add Attribute** section in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7facf-194">Copy **Your Account ID** value and paste the value in **Attribute Value** textbox under **Add Attribute** section in Azure portal.</span></span>
   
    <span data-ttu-id="7facf-195">f.</span><span class="sxs-lookup"><span data-stu-id="7facf-195">f.</span></span> <span data-ttu-id="7facf-196">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="7facf-196">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="7facf-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="7facf-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7facf-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="7facf-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7facf-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7facf-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7facf-200">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7facf-200">Create an Azure AD test user</span></span>
<span data-ttu-id="7facf-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7facf-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="7facf-203">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7facf-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7facf-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="7facf-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/tinfoil-security-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="7facf-206">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="7facf-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![<span data-ttu-id="7facf-207">Users and groups -> All users</span><span class="sxs-lookup"><span data-stu-id="7facf-207">Users and groups -> All users</span></span> ](./media/tinfoil-security-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="7facf-208">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="7facf-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![User](./media/tinfoil-security-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="7facf-210">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7facf-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/tinfoil-security-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7facf-212">a.</span><span class="sxs-lookup"><span data-stu-id="7facf-212">a.</span></span> <span data-ttu-id="7facf-213">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7facf-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7facf-214">b.</span><span class="sxs-lookup"><span data-stu-id="7facf-214">b.</span></span> <span data-ttu-id="7facf-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7facf-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7facf-216">c.</span><span class="sxs-lookup"><span data-stu-id="7facf-216">c.</span></span> <span data-ttu-id="7facf-217">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="7facf-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7facf-218">d.</span><span class="sxs-lookup"><span data-stu-id="7facf-218">d.</span></span> <span data-ttu-id="7facf-219">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="7facf-219">Click **Create**.</span></span>
 
### <a name="create-a-tinfoil-security-test-user"></a><span data-ttu-id="7facf-220">Create a TINFOIL SECURITY test user</span><span class="sxs-lookup"><span data-stu-id="7facf-220">Create a TINFOIL SECURITY test user</span></span>

<span data-ttu-id="7facf-221">In order to enable Azure AD users to log into TINFOIL SECURITY, they must be provisioned into TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="7facf-221">In order to enable Azure AD users to log into TINFOIL SECURITY, they must be provisioned into TINFOIL SECURITY.</span></span> <span data-ttu-id="7facf-222">In the case of TINFOIL SECURITY, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="7facf-222">In the case of TINFOIL SECURITY, provisioning is a manual task.</span></span>

<span data-ttu-id="7facf-223">**To get a user provisioned, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7facf-223">**To get a user provisioned, perform the following steps:**</span></span>

1. <span data-ttu-id="7facf-224">If the user is a part of an Enterprise account, you need to [contact the TINFOIL SECURITY support team](https://www.tinfoilsecurity.com/contact) to get the user account created.</span><span class="sxs-lookup"><span data-stu-id="7facf-224">If the user is a part of an Enterprise account, you need to [contact the TINFOIL SECURITY support team](https://www.tinfoilsecurity.com/contact) to get the user account created.</span></span>

1. <span data-ttu-id="7facf-225">If the user is a regular TINFOIL SECURITY SaaS user, then the user can add a collaborator to any of the user’s sites.</span><span class="sxs-lookup"><span data-stu-id="7facf-225">If the user is a regular TINFOIL SECURITY SaaS user, then the user can add a collaborator to any of the user’s sites.</span></span> <span data-ttu-id="7facf-226">This triggers a process to send an invitation to the specified email to create a new TINFOIL SECURITY user account.</span><span class="sxs-lookup"><span data-stu-id="7facf-226">This triggers a process to send an invitation to the specified email to create a new TINFOIL SECURITY user account.</span></span>

> [!NOTE]
> <span data-ttu-id="7facf-227">You can use any other TINFOIL SECURITY user account creation tools or APIs provided by TINFOIL SECURITY to provision Azure AD user accounts.</span><span class="sxs-lookup"><span data-stu-id="7facf-227">You can use any other TINFOIL SECURITY user account creation tools or APIs provided by TINFOIL SECURITY to provision Azure AD user accounts.</span></span>
> 
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="7facf-228">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7facf-228">Assign the Azure AD test user</span></span>

<span data-ttu-id="7facf-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="7facf-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TINFOIL SECURITY.</span></span>

![Assign User][200] 

<span data-ttu-id="7facf-231">**To assign Britta Simon to TINFOIL SECURITY, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7facf-231">**To assign Britta Simon to TINFOIL SECURITY, perform the following steps:**</span></span>

1. <span data-ttu-id="7facf-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="7facf-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="7facf-234">In the applications list, select **TINFOIL SECURITY**.</span><span class="sxs-lookup"><span data-stu-id="7facf-234">In the applications list, select **TINFOIL SECURITY**.</span></span>

    ![select TINFOIL SECURITY](./media/tinfoil-security-tutorial/tutorial_tinfoil-security_app.png) 

1. <span data-ttu-id="7facf-236">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="7facf-236">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="7facf-238">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="7facf-238">Click **Add** button.</span></span> <span data-ttu-id="7facf-239">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="7facf-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="7facf-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="7facf-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="7facf-242">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="7facf-242">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="7facf-243">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="7facf-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7facf-244">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="7facf-244">Test single sign-on</span></span>

<span data-ttu-id="7facf-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="7facf-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7facf-246">When you click the TINFOIL SECURITY tile in the Access Panel, you should get automatically signed-on to your TINFOIL SECURITY application.</span><span class="sxs-lookup"><span data-stu-id="7facf-246">When you click the TINFOIL SECURITY tile in the Access Panel, you should get automatically signed-on to your TINFOIL SECURITY application.</span></span> <span data-ttu-id="7facf-247">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7facf-247">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7facf-248">Additional resources</span><span class="sxs-lookup"><span data-stu-id="7facf-248">Additional resources</span></span>

* [<span data-ttu-id="7facf-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7facf-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="7facf-250">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7facf-250">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/tinfoil-security-tutorial/tutorial_general_01.png
[2]: ./media/tinfoil-security-tutorial/tutorial_general_02.png
[3]: ./media/tinfoil-security-tutorial/tutorial_general_03.png
[4]: ./media/tinfoil-security-tutorial/tutorial_general_04.png

[100]: ./media/tinfoil-security-tutorial/tutorial_general_100.png

[200]: ./media/tinfoil-security-tutorial/tutorial_general_200.png
[201]: ./media/tinfoil-security-tutorial/tutorial_general_201.png
[202]: ./media/tinfoil-security-tutorial/tutorial_general_202.png
[203]: ./media/tinfoil-security-tutorial/tutorial_general_203.png

