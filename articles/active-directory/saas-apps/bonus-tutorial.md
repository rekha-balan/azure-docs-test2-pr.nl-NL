---
title: 'Tutorial: Azure Active Directory integration with Bonusly | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Bonusly.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 29fea32a-fa20-47b2-9e24-26feb47b0ae6
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 175c00d36491fbf43149aef9a590219b330581c1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870150"
---
# <a name="tutorial-azure-active-directory-integration-with-bonusly"></a><span data-ttu-id="c250b-103">Tutorial: Azure Active Directory integration with Bonusly</span><span class="sxs-lookup"><span data-stu-id="c250b-103">Tutorial: Azure Active Directory integration with Bonusly</span></span>

<span data-ttu-id="c250b-104">In this tutorial, you learn how to integrate Bonusly with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c250b-104">In this tutorial, you learn how to integrate Bonusly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c250b-105">Integrating Bonusly with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="c250b-105">Integrating Bonusly with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c250b-106">You can control in Azure AD who has access to Bonusly</span><span class="sxs-lookup"><span data-stu-id="c250b-106">You can control in Azure AD who has access to Bonusly</span></span>
- <span data-ttu-id="c250b-107">You can enable your users to automatically get signed-on to Bonusly (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="c250b-107">You can enable your users to automatically get signed-on to Bonusly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c250b-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="c250b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c250b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="c250b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c250b-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c250b-110">Prerequisites</span></span>

<span data-ttu-id="c250b-111">To configure Azure AD integration with Bonusly, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="c250b-111">To configure Azure AD integration with Bonusly, you need the following items:</span></span>

- <span data-ttu-id="c250b-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="c250b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c250b-113">A Bonusly single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="c250b-113">A Bonusly single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c250b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="c250b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c250b-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="c250b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c250b-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="c250b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c250b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c250b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c250b-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="c250b-118">Scenario description</span></span>
<span data-ttu-id="c250b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="c250b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c250b-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="c250b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c250b-121">Adding Bonusly from the gallery</span><span class="sxs-lookup"><span data-stu-id="c250b-121">Adding Bonusly from the gallery</span></span>
1. <span data-ttu-id="c250b-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c250b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bonusly-from-the-gallery"></a><span data-ttu-id="c250b-123">Adding Bonusly from the gallery</span><span class="sxs-lookup"><span data-stu-id="c250b-123">Adding Bonusly from the gallery</span></span>
<span data-ttu-id="c250b-124">To configure the integration of Bonusly into Azure AD, you need to add Bonusly from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="c250b-124">To configure the integration of Bonusly into Azure AD, you need to add Bonusly from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c250b-125">**To add Bonusly from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c250b-125">**To add Bonusly from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c250b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="c250b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="c250b-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="c250b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c250b-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="c250b-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="c250b-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="c250b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="c250b-133">In the search box, type **Bonusly**, select **Bonusly** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="c250b-133">In the search box, type **Bonusly**, select **Bonusly** from result panel then click **Add** button to add the application.</span></span>

    ![Bonusly in the results list](./media/bonus-tutorial/tutorial_bonusly_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c250b-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c250b-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="c250b-136">In this section, you configure and test Azure AD single sign-on with Bonusly based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c250b-136">In this section, you configure and test Azure AD single sign-on with Bonusly based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c250b-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Bonusly is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c250b-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Bonusly is to a user in Azure AD.</span></span> <span data-ttu-id="c250b-138">In other words, a link relationship between an Azure AD user and the related user in Bonusly needs to be established.</span><span class="sxs-lookup"><span data-stu-id="c250b-138">In other words, a link relationship between an Azure AD user and the related user in Bonusly needs to be established.</span></span>

<span data-ttu-id="c250b-139">In Bonusly, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="c250b-139">In Bonusly, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c250b-140">To configure and test Azure AD single sign-on with Bonusly, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="c250b-140">To configure and test Azure AD single sign-on with Bonusly, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c250b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="c250b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="c250b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c250b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="c250b-143">**[Create a Bonusly test user](#create-a-bonusly-test-user)** - to have a counterpart of Britta Simon in Bonusly that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="c250b-143">**[Create a Bonusly test user](#create-a-bonusly-test-user)** - to have a counterpart of Britta Simon in Bonusly that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="c250b-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c250b-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="c250b-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="c250b-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c250b-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c250b-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c250b-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bonusly application.</span><span class="sxs-lookup"><span data-stu-id="c250b-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bonusly application.</span></span>

<span data-ttu-id="c250b-148">**To configure Azure AD single sign-on with Bonusly, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c250b-148">**To configure Azure AD single sign-on with Bonusly, perform the following steps:**</span></span>

1. <span data-ttu-id="c250b-149">In the Azure portal, on the **Bonusly** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="c250b-149">In the Azure portal, on the **Bonusly** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="c250b-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c250b-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/bonus-tutorial/tutorial_bonusly_samlbase.png)

1. <span data-ttu-id="c250b-153">On the **Bonusly Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c250b-153">On the **Bonusly Domain and URLs** section, perform the following steps:</span></span>

    ![Bonusly Domain and URLs single sign-on information](./media/bonus-tutorial/tutorial_bonusly_url.png)

    <span data-ttu-id="c250b-155">In the **Reply URL** textbox, type a URL using the following pattern: `https://Bonus.ly/saml/<tenant-name>`</span><span class="sxs-lookup"><span data-stu-id="c250b-155">In the **Reply URL** textbox, type a URL using the following pattern: `https://Bonus.ly/saml/<tenant-name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c250b-156">The value is not real.</span><span class="sxs-lookup"><span data-stu-id="c250b-156">The value is not real.</span></span> <span data-ttu-id="c250b-157">Update the value with the actual Reply URL.</span><span class="sxs-lookup"><span data-stu-id="c250b-157">Update the value with the actual Reply URL.</span></span> <span data-ttu-id="c250b-158">Contact [Bonusly support team](https://bonus.ly/contact) to get the value.</span><span class="sxs-lookup"><span data-stu-id="c250b-158">Contact [Bonusly support team](https://bonus.ly/contact) to get the value.</span></span>
 
1. <span data-ttu-id="c250b-159">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value from the certificate.</span><span class="sxs-lookup"><span data-stu-id="c250b-159">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value from the certificate.</span></span>

    ![The Certificate download link](./media/bonus-tutorial/tutorial_bonusly_certificate.png) 

1. <span data-ttu-id="c250b-161">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="c250b-161">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/bonus-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="c250b-163">On the **Bonusly Configuration** section, click **Configure Bonusly** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="c250b-163">On the **Bonusly Configuration** section, click **Configure Bonusly** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c250b-164">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="c250b-164">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Bonusly Configuration](./media/bonus-tutorial/tutorial_bonusly_configure.png) 

1. <span data-ttu-id="c250b-166">In a different browser window, log in to your **Bonusly** tenant.</span><span class="sxs-lookup"><span data-stu-id="c250b-166">In a different browser window, log in to your **Bonusly** tenant.</span></span>

1. <span data-ttu-id="c250b-167">In the toolbar on the top, click **Settings**, and then select **Integrations and apps**.</span><span class="sxs-lookup"><span data-stu-id="c250b-167">In the toolbar on the top, click **Settings**, and then select **Integrations and apps**.</span></span>
   
    <span data-ttu-id="c250b-168">![Bonusly Social Section](./media/bonus-tutorial/ic773686.png "Bonusly")</span><span class="sxs-lookup"><span data-stu-id="c250b-168">![Bonusly Social Section](./media/bonus-tutorial/ic773686.png "Bonusly")</span></span>
1. <span data-ttu-id="c250b-169">Under **Single Sign-On**, select **SAML**.</span><span class="sxs-lookup"><span data-stu-id="c250b-169">Under **Single Sign-On**, select **SAML**.</span></span>

1. <span data-ttu-id="c250b-170">On the **SAML** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c250b-170">On the **SAML** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="c250b-171">![Bonusly Saml Dialog page](./media/bonus-tutorial/ic773687.png "Bonusly")</span><span class="sxs-lookup"><span data-stu-id="c250b-171">![Bonusly Saml Dialog page](./media/bonus-tutorial/ic773687.png "Bonusly")</span></span>
   
    <span data-ttu-id="c250b-172">a.</span><span class="sxs-lookup"><span data-stu-id="c250b-172">a.</span></span> <span data-ttu-id="c250b-173">In the **IdP SSO target URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c250b-173">In the **IdP SSO target URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="c250b-174">b.</span><span class="sxs-lookup"><span data-stu-id="c250b-174">b.</span></span> <span data-ttu-id="c250b-175">In the **IdP Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c250b-175">In the **IdP Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="c250b-176">c.</span><span class="sxs-lookup"><span data-stu-id="c250b-176">c.</span></span> <span data-ttu-id="c250b-177">In the **IdP Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c250b-177">In the **IdP Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="c250b-178">d.</span><span class="sxs-lookup"><span data-stu-id="c250b-178">d.</span></span> <span data-ttu-id="c250b-179">Paste the **Thumbprint** value copied from Azure portal into the **Cert Fingerprint** textbox.</span><span class="sxs-lookup"><span data-stu-id="c250b-179">Paste the **Thumbprint** value copied from Azure portal into the **Cert Fingerprint** textbox.</span></span>
   
1. <span data-ttu-id="c250b-180">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="c250b-180">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="c250b-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="c250b-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c250b-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="c250b-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c250b-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c250b-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c250b-184">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="c250b-184">Create an Azure AD test user</span></span>
<span data-ttu-id="c250b-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c250b-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create an Azure AD test user][100]

<span data-ttu-id="c250b-187">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c250b-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c250b-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="c250b-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![The Azure Active Directory button](./media/bonus-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="c250b-190">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="c250b-190">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![The "Users and groups" and "All users" links](./media/bonus-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="c250b-192">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="c250b-192">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![The Add button](./media/bonus-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="c250b-194">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c250b-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![The User dialog box](./media/bonus-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c250b-196">a.</span><span class="sxs-lookup"><span data-stu-id="c250b-196">a.</span></span> <span data-ttu-id="c250b-197">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c250b-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c250b-198">b.</span><span class="sxs-lookup"><span data-stu-id="c250b-198">b.</span></span> <span data-ttu-id="c250b-199">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c250b-199">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c250b-200">c.</span><span class="sxs-lookup"><span data-stu-id="c250b-200">c.</span></span> <span data-ttu-id="c250b-201">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="c250b-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c250b-202">d.</span><span class="sxs-lookup"><span data-stu-id="c250b-202">d.</span></span> <span data-ttu-id="c250b-203">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="c250b-203">Click **Create**.</span></span>
 
### <a name="create-a-bonusly-test-user"></a><span data-ttu-id="c250b-204">Create a Bonusly test user</span><span class="sxs-lookup"><span data-stu-id="c250b-204">Create a Bonusly test user</span></span>

<span data-ttu-id="c250b-205">In order to enable Azure AD users to log in to Bonusly, they must be provisioned into Bonusly.</span><span class="sxs-lookup"><span data-stu-id="c250b-205">In order to enable Azure AD users to log in to Bonusly, they must be provisioned into Bonusly.</span></span> <span data-ttu-id="c250b-206">In the case of Bonusly, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="c250b-206">In the case of Bonusly, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="c250b-207">You can use any other Bonusly user account creation tools or APIs provided by Bonusly to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="c250b-207">You can use any other Bonusly user account creation tools or APIs provided by Bonusly to provision AAD user accounts.</span></span>
>  

<span data-ttu-id="c250b-208">**To configure user provisioning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c250b-208">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="c250b-209">In a web browser window, log in to your Bonusly tenant.</span><span class="sxs-lookup"><span data-stu-id="c250b-209">In a web browser window, log in to your Bonusly tenant.</span></span>

1. <span data-ttu-id="c250b-210">Click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="c250b-210">Click **Settings**.</span></span>
 
    <span data-ttu-id="c250b-211">![Settings](./media/bonus-tutorial/ic781041.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="c250b-211">![Settings](./media/bonus-tutorial/ic781041.png "Settings")</span></span>

1. <span data-ttu-id="c250b-212">Click the **Users and bonuses** tab.</span><span class="sxs-lookup"><span data-stu-id="c250b-212">Click the **Users and bonuses** tab.</span></span>
   
    <span data-ttu-id="c250b-213">![Users and bonuses](./media/bonus-tutorial/ic781042.png "Users and bonuses")</span><span class="sxs-lookup"><span data-stu-id="c250b-213">![Users and bonuses](./media/bonus-tutorial/ic781042.png "Users and bonuses")</span></span>

1. <span data-ttu-id="c250b-214">Click **Manage Users**.</span><span class="sxs-lookup"><span data-stu-id="c250b-214">Click **Manage Users**.</span></span>
   
    <span data-ttu-id="c250b-215">![Manage Users](./media/bonus-tutorial/ic781043.png "Manage Users")</span><span class="sxs-lookup"><span data-stu-id="c250b-215">![Manage Users](./media/bonus-tutorial/ic781043.png "Manage Users")</span></span>

1. <span data-ttu-id="c250b-216">Click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="c250b-216">Click **Add User**.</span></span>
   
    <span data-ttu-id="c250b-217">![Add User](./media/bonus-tutorial/ic781044.png "Add User")</span><span class="sxs-lookup"><span data-stu-id="c250b-217">![Add User](./media/bonus-tutorial/ic781044.png "Add User")</span></span>

1. <span data-ttu-id="c250b-218">On the **Add User** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c250b-218">On the **Add User** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="c250b-219">![Add User](./media/bonus-tutorial/ic781045.png "Add User")</span><span class="sxs-lookup"><span data-stu-id="c250b-219">![Add User](./media/bonus-tutorial/ic781045.png "Add User")</span></span>  

    <span data-ttu-id="c250b-220">a.</span><span class="sxs-lookup"><span data-stu-id="c250b-220">a.</span></span> <span data-ttu-id="c250b-221">In the **First name** textbox, enter the first name of user like **Britta**.</span><span class="sxs-lookup"><span data-stu-id="c250b-221">In the **First name** textbox, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="c250b-222">b.</span><span class="sxs-lookup"><span data-stu-id="c250b-222">b.</span></span> <span data-ttu-id="c250b-223">In the **Last name** textbox, enter the last name of user like **Simon**.</span><span class="sxs-lookup"><span data-stu-id="c250b-223">In the **Last name** textbox, enter the last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="c250b-224">c.</span><span class="sxs-lookup"><span data-stu-id="c250b-224">c.</span></span> <span data-ttu-id="c250b-225">In the **Email** textbox, enter the email of user like **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="c250b-225">In the **Email** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="c250b-226">d.</span><span class="sxs-lookup"><span data-stu-id="c250b-226">d.</span></span> <span data-ttu-id="c250b-227">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="c250b-227">Click **Save**.</span></span>
   
     >[!NOTE]
     ><span data-ttu-id="c250b-228">The Azure AD account holder receives an email that includes a link to confirm the account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="c250b-228">The Azure AD account holder receives an email that includes a link to confirm the account before it becomes active.</span></span>
     >  

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="c250b-229">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="c250b-229">Assign the Azure AD test user</span></span>

<span data-ttu-id="c250b-230">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Bonusly.</span><span class="sxs-lookup"><span data-stu-id="c250b-230">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Bonusly.</span></span>

![Assign the user role][200] 

<span data-ttu-id="c250b-232">**To assign Britta Simon to Bonusly, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c250b-232">**To assign Britta Simon to Bonusly, perform the following steps:**</span></span>

1. <span data-ttu-id="c250b-233">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="c250b-233">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="c250b-235">In the applications list, select **Bonusly**.</span><span class="sxs-lookup"><span data-stu-id="c250b-235">In the applications list, select **Bonusly**.</span></span>

    ![The Bonusly link in the Applications list](./media/bonus-tutorial/tutorial_bonusly_app.png) 

1. <span data-ttu-id="c250b-237">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="c250b-237">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202] 

1. <span data-ttu-id="c250b-239">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="c250b-239">Click **Add** button.</span></span> <span data-ttu-id="c250b-240">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="c250b-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="c250b-242">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="c250b-242">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="c250b-243">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="c250b-243">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="c250b-244">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="c250b-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c250b-245">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="c250b-245">Test single sign-on</span></span>

<span data-ttu-id="c250b-246">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="c250b-246">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c250b-247">When you click the Bonusly tile in the Access Panel, you should get automatically signed-on to your Bonusly application.</span><span class="sxs-lookup"><span data-stu-id="c250b-247">When you click the Bonusly tile in the Access Panel, you should get automatically signed-on to your Bonusly application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c250b-248">Additional resources</span><span class="sxs-lookup"><span data-stu-id="c250b-248">Additional resources</span></span>

* [<span data-ttu-id="c250b-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c250b-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="c250b-250">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c250b-250">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/bonus-tutorial/tutorial_general_01.png
[2]: ./media/bonus-tutorial/tutorial_general_02.png
[3]: ./media/bonus-tutorial/tutorial_general_03.png
[4]: ./media/bonus-tutorial/tutorial_general_04.png

[100]: ./media/bonus-tutorial/tutorial_general_100.png

[200]: ./media/bonus-tutorial/tutorial_general_200.png
[201]: ./media/bonus-tutorial/tutorial_general_201.png
[202]: ./media/bonus-tutorial/tutorial_general_202.png
[203]: ./media/bonus-tutorial/tutorial_general_203.png

