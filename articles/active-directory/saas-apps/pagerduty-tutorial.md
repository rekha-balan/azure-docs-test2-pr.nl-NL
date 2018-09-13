---
title: 'Tutorial: Azure Active Directory integration with PagerDuty | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and PagerDuty.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 0410456a-76f7-42a7-9bb5-f767de75a0e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2018
ms.author: jeedes
ms.openlocfilehash: 0e571880d9893c0027c200c6f49dc704fea09ead
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966912"
---
# <a name="tutorial-azure-active-directory-integration-with-pagerduty"></a><span data-ttu-id="264ab-103">Tutorial: Azure Active Directory integration with PagerDuty</span><span class="sxs-lookup"><span data-stu-id="264ab-103">Tutorial: Azure Active Directory integration with PagerDuty</span></span>

<span data-ttu-id="264ab-104">In this tutorial, you learn how to integrate PagerDuty with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="264ab-104">In this tutorial, you learn how to integrate PagerDuty with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="264ab-105">Integrating PagerDuty with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="264ab-105">Integrating PagerDuty with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="264ab-106">You can control in Azure AD who has access to PagerDuty</span><span class="sxs-lookup"><span data-stu-id="264ab-106">You can control in Azure AD who has access to PagerDuty</span></span>
- <span data-ttu-id="264ab-107">You can enable your users to automatically get signed-on to PagerDuty (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="264ab-107">You can enable your users to automatically get signed-on to PagerDuty (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="264ab-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="264ab-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="264ab-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="264ab-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="264ab-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="264ab-110">Prerequisites</span></span>

<span data-ttu-id="264ab-111">To configure Azure AD integration with PagerDuty, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="264ab-111">To configure Azure AD integration with PagerDuty, you need the following items:</span></span>

- <span data-ttu-id="264ab-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="264ab-112">An Azure AD subscription</span></span>
- <span data-ttu-id="264ab-113">A PagerDuty single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="264ab-113">A PagerDuty single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="264ab-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="264ab-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="264ab-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="264ab-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="264ab-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="264ab-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="264ab-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="264ab-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="264ab-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="264ab-118">Scenario description</span></span>
<span data-ttu-id="264ab-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="264ab-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="264ab-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="264ab-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="264ab-121">Adding PagerDuty from the gallery</span><span class="sxs-lookup"><span data-stu-id="264ab-121">Adding PagerDuty from the gallery</span></span>
1. <span data-ttu-id="264ab-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="264ab-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pagerduty-from-the-gallery"></a><span data-ttu-id="264ab-123">Adding PagerDuty from the gallery</span><span class="sxs-lookup"><span data-stu-id="264ab-123">Adding PagerDuty from the gallery</span></span>
<span data-ttu-id="264ab-124">To configure the integration of PagerDuty into Azure AD, you need to add PagerDuty from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="264ab-124">To configure the integration of PagerDuty into Azure AD, you need to add PagerDuty from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="264ab-125">**To add PagerDuty from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="264ab-125">**To add PagerDuty from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="264ab-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="264ab-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span>

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="264ab-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="264ab-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="264ab-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="264ab-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]

1. <span data-ttu-id="264ab-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="264ab-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="264ab-133">In the search box, type **PagerDuty**, select  **PagerDuty**  from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="264ab-133">In the search box, type **PagerDuty**, select  **PagerDuty**  from result panel then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/pagerduty-tutorial/tutorial_pagerduty_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="264ab-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="264ab-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="264ab-136">In this section, you configure and test Azure AD single sign-on with PagerDuty based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="264ab-136">In this section, you configure and test Azure AD single sign-on with PagerDuty based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="264ab-137">For single sign-on to work, Azure AD needs to know what the counterpart user in PagerDuty is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="264ab-137">For single sign-on to work, Azure AD needs to know what the counterpart user in PagerDuty is to a user in Azure AD.</span></span> <span data-ttu-id="264ab-138">In other words, a link relationship between an Azure AD user and the related user in PagerDuty needs to be established.</span><span class="sxs-lookup"><span data-stu-id="264ab-138">In other words, a link relationship between an Azure AD user and the related user in PagerDuty needs to be established.</span></span>

<span data-ttu-id="264ab-139">In PagerDuty, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="264ab-139">In PagerDuty, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="264ab-140">To configure and test Azure AD single sign-on with PagerDuty, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="264ab-140">To configure and test Azure AD single sign-on with PagerDuty, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="264ab-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="264ab-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="264ab-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="264ab-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="264ab-143">**[Create a PagerDuty test user](#create-a-pagerduty-test-user)** - to have a counterpart of Britta Simon in PagerDuty that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="264ab-143">**[Create a PagerDuty test user](#create-a-pagerduty-test-user)** - to have a counterpart of Britta Simon in PagerDuty that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="264ab-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="264ab-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="264ab-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="264ab-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="264ab-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="264ab-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="264ab-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PagerDuty application.</span><span class="sxs-lookup"><span data-stu-id="264ab-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PagerDuty application.</span></span>

<span data-ttu-id="264ab-148">**To configure Azure AD single sign-on with PagerDuty, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="264ab-148">**To configure Azure AD single sign-on with PagerDuty, perform the following steps:**</span></span>

1. <span data-ttu-id="264ab-149">In the Azure portal, on the **PagerDuty** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="264ab-149">In the Azure portal, on the **PagerDuty** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="264ab-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="264ab-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/pagerduty-tutorial/tutorial_pagerduty_samlbase.png)

1. <span data-ttu-id="264ab-153">On the **PagerDuty Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="264ab-153">On the **PagerDuty Domain and URLs** section, perform the following steps:</span></span>

    ![PagerDuty Domain and URLs single sign-on information](./media/pagerduty-tutorial/tutorial_pagerduty_url.png)

    <span data-ttu-id="264ab-155">a.</span><span class="sxs-lookup"><span data-stu-id="264ab-155">a.</span></span> <span data-ttu-id="264ab-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.pagerduty.com`</span><span class="sxs-lookup"><span data-stu-id="264ab-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.pagerduty.com`</span></span>

    <span data-ttu-id="264ab-157">b.</span><span class="sxs-lookup"><span data-stu-id="264ab-157">b.</span></span> <span data-ttu-id="264ab-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant-name>.pagerduty.com`</span><span class="sxs-lookup"><span data-stu-id="264ab-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant-name>.pagerduty.com`</span></span>

    > [!NOTE]
    > <span data-ttu-id="264ab-159">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="264ab-159">These values are not real.</span></span> <span data-ttu-id="264ab-160">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="264ab-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="264ab-161">Contact [PagerDuty Client support team](https://www.pagerduty.com/support/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="264ab-161">Contact [PagerDuty Client support team](https://www.pagerduty.com/support/) to get these values.</span></span>

1. <span data-ttu-id="264ab-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="264ab-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/pagerduty-tutorial/tutorial_pagerduty_certificate.png)

1. <span data-ttu-id="264ab-164">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="264ab-164">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/pagerduty-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="264ab-166">On the **PagerDuty Configuration** section, click **Configure PagerDuty** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="264ab-166">On the **PagerDuty Configuration** section, click **Configure PagerDuty** to open **Configure sign-on** window.</span></span> <span data-ttu-id="264ab-167">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="264ab-167">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![PagerDuty configuration](./media/pagerduty-tutorial/tutorial_pagerduty_configure.png)

1. <span data-ttu-id="264ab-169">In a different web browser window, log into your Pagerduty company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="264ab-169">In a different web browser window, log into your Pagerduty company site as an administrator.</span></span>

1. <span data-ttu-id="264ab-170">In the menu on the top, click **Account Settings**.</span><span class="sxs-lookup"><span data-stu-id="264ab-170">In the menu on the top, click **Account Settings**.</span></span>

    <span data-ttu-id="264ab-171">![Account Settings](./media/pagerduty-tutorial/ic778535.png "Account Settings")</span><span class="sxs-lookup"><span data-stu-id="264ab-171">![Account Settings](./media/pagerduty-tutorial/ic778535.png "Account Settings")</span></span>

1. <span data-ttu-id="264ab-172">Click **Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="264ab-172">Click **Single Sign-on**.</span></span>

    <span data-ttu-id="264ab-173">![Single sign-on](./media/pagerduty-tutorial/ic778536.png "Single sign-on")</span><span class="sxs-lookup"><span data-stu-id="264ab-173">![Single sign-on](./media/pagerduty-tutorial/ic778536.png "Single sign-on")</span></span>

1. <span data-ttu-id="264ab-174">On the **Enable Single Sign-on (SSO)** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="264ab-174">On the **Enable Single Sign-on (SSO)** page, perform the following steps:</span></span>

    <span data-ttu-id="264ab-175">![Enable single sign-on](./media/pagerduty-tutorial/ic778537.png "Enable single sign-on")</span><span class="sxs-lookup"><span data-stu-id="264ab-175">![Enable single sign-on](./media/pagerduty-tutorial/ic778537.png "Enable single sign-on")</span></span>

    <span data-ttu-id="264ab-176">a.</span><span class="sxs-lookup"><span data-stu-id="264ab-176">a.</span></span> <span data-ttu-id="264ab-177">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox</span><span class="sxs-lookup"><span data-stu-id="264ab-177">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox</span></span>
  
    <span data-ttu-id="264ab-178">b.</span><span class="sxs-lookup"><span data-stu-id="264ab-178">b.</span></span> <span data-ttu-id="264ab-179">In the **Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="264ab-179">In the **Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="264ab-180">c.</span><span class="sxs-lookup"><span data-stu-id="264ab-180">c.</span></span> <span data-ttu-id="264ab-181">In the **Logout URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="264ab-181">In the **Logout URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="264ab-182">d.</span><span class="sxs-lookup"><span data-stu-id="264ab-182">d.</span></span> <span data-ttu-id="264ab-183">Select **Allow username/password login**.</span><span class="sxs-lookup"><span data-stu-id="264ab-183">Select **Allow username/password login**.</span></span>

    <span data-ttu-id="264ab-184">e.</span><span class="sxs-lookup"><span data-stu-id="264ab-184">e.</span></span> <span data-ttu-id="264ab-185">Select **Require EXACT authentication context comparison** checkbox.</span><span class="sxs-lookup"><span data-stu-id="264ab-185">Select **Require EXACT authentication context comparison** checkbox.</span></span>

    <span data-ttu-id="264ab-186">f.</span><span class="sxs-lookup"><span data-stu-id="264ab-186">f.</span></span> <span data-ttu-id="264ab-187">Click **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="264ab-187">Click **Save Changes**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="264ab-188">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="264ab-188">Create an Azure AD test user</span></span>

<span data-ttu-id="264ab-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="264ab-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create an Azure AD test user][100]

<span data-ttu-id="264ab-191">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="264ab-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="264ab-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="264ab-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![The Azure Active Directory button](./media/pagerduty-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="264ab-194">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="264ab-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![The "Users and groups" and "All users" links](./media/pagerduty-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="264ab-196">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="264ab-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![The Add button](./media/pagerduty-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="264ab-198">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="264ab-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![The User dialog box](./media/pagerduty-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="264ab-200">a.</span><span class="sxs-lookup"><span data-stu-id="264ab-200">a.</span></span> <span data-ttu-id="264ab-201">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="264ab-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="264ab-202">b.</span><span class="sxs-lookup"><span data-stu-id="264ab-202">b.</span></span> <span data-ttu-id="264ab-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="264ab-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="264ab-204">c.</span><span class="sxs-lookup"><span data-stu-id="264ab-204">c.</span></span> <span data-ttu-id="264ab-205">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="264ab-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="264ab-206">d.</span><span class="sxs-lookup"><span data-stu-id="264ab-206">d.</span></span> <span data-ttu-id="264ab-207">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="264ab-207">Click **Create**.</span></span>
 
### <a name="create-a-pagerduty-test-user"></a><span data-ttu-id="264ab-208">Create a PagerDuty test user</span><span class="sxs-lookup"><span data-stu-id="264ab-208">Create a PagerDuty test user</span></span>

<span data-ttu-id="264ab-209">To enable Azure AD users to log in to PagerDuty, they must be provisioned into PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="264ab-209">To enable Azure AD users to log in to PagerDuty, they must be provisioned into PagerDuty.</span></span>  
<span data-ttu-id="264ab-210">In the case of PagerDuty, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="264ab-210">In the case of PagerDuty, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="264ab-211">You can use any other Pagerduty user account creation tools or APIs provided by Pagerduty to provision Azure Active Directory user accounts.</span><span class="sxs-lookup"><span data-stu-id="264ab-211">You can use any other Pagerduty user account creation tools or APIs provided by Pagerduty to provision Azure Active Directory user accounts.</span></span>

<span data-ttu-id="264ab-212">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="264ab-212">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="264ab-213">Log in to your **Pagerduty** tenant.</span><span class="sxs-lookup"><span data-stu-id="264ab-213">Log in to your **Pagerduty** tenant.</span></span>

1. <span data-ttu-id="264ab-214">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="264ab-214">In the menu on the top, click **Users**.</span></span>

1. <span data-ttu-id="264ab-215">Click **Add Users**.</span><span class="sxs-lookup"><span data-stu-id="264ab-215">Click **Add Users**.</span></span>
   
    <span data-ttu-id="264ab-216">![Add Users](./media/pagerduty-tutorial/ic778539.png "Add Users")</span><span class="sxs-lookup"><span data-stu-id="264ab-216">![Add Users](./media/pagerduty-tutorial/ic778539.png "Add Users")</span></span>

1.  <span data-ttu-id="264ab-217">On the **Invite your team** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="264ab-217">On the **Invite your team** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="264ab-218">![Invite your team](./media/pagerduty-tutorial/ic778540.png "Invite your team")</span><span class="sxs-lookup"><span data-stu-id="264ab-218">![Invite your team](./media/pagerduty-tutorial/ic778540.png "Invite your team")</span></span>

    <span data-ttu-id="264ab-219">a.</span><span class="sxs-lookup"><span data-stu-id="264ab-219">a.</span></span> <span data-ttu-id="264ab-220">Type the **First and Last Name** of user like **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="264ab-220">Type the **First and Last Name** of user like **Britta Simon**.</span></span> 
   
    <span data-ttu-id="264ab-221">b.</span><span class="sxs-lookup"><span data-stu-id="264ab-221">b.</span></span> <span data-ttu-id="264ab-222">Enter **Email** address of user like **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="264ab-222">Enter **Email** address of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="264ab-223">c.</span><span class="sxs-lookup"><span data-stu-id="264ab-223">c.</span></span> <span data-ttu-id="264ab-224">Click **Add**, and then click **Send Invites**.</span><span class="sxs-lookup"><span data-stu-id="264ab-224">Click **Add**, and then click **Send Invites**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="264ab-225">All added users will receive an invite to create a PagerDuty account.</span><span class="sxs-lookup"><span data-stu-id="264ab-225">All added users will receive an invite to create a PagerDuty account.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="264ab-226">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="264ab-226">Assign the Azure AD test user</span></span>

<span data-ttu-id="264ab-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="264ab-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PagerDuty.</span></span>

![Assign the user role][200]

<span data-ttu-id="264ab-229">**To assign Britta Simon to PagerDuty, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="264ab-229">**To assign Britta Simon to PagerDuty, perform the following steps:**</span></span>

1. <span data-ttu-id="264ab-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="264ab-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="264ab-232">In the applications list, select **PagerDuty**.</span><span class="sxs-lookup"><span data-stu-id="264ab-232">In the applications list, select **PagerDuty**.</span></span>

    ![The PagerDuty link in the Applications list](./media/pagerduty-tutorial/tutorial_pagerduty_app.png) 

1. <span data-ttu-id="264ab-234">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="264ab-234">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="264ab-236">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="264ab-236">Click **Add** button.</span></span> <span data-ttu-id="264ab-237">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="264ab-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="264ab-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="264ab-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="264ab-240">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="264ab-240">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="264ab-241">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="264ab-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="264ab-242">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="264ab-242">Test single sign-on</span></span>

<span data-ttu-id="264ab-243">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="264ab-243">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="264ab-244">When you click the PagerDuty tile in the Access Panelyou should get automatically signed-on to your PagerDuty application.</span><span class="sxs-lookup"><span data-stu-id="264ab-244">When you click the PagerDuty tile in the Access Panelyou should get automatically signed-on to your PagerDuty application.</span></span>

<span data-ttu-id="264ab-245">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="264ab-245">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="264ab-246">Additional resources</span><span class="sxs-lookup"><span data-stu-id="264ab-246">Additional resources</span></span>

* [<span data-ttu-id="264ab-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="264ab-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="264ab-248">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="264ab-248">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/pagerduty-tutorial/tutorial_general_01.png
[2]: ./media/pagerduty-tutorial/tutorial_general_02.png
[3]: ./media/pagerduty-tutorial/tutorial_general_03.png
[4]: ./media/pagerduty-tutorial/tutorial_general_04.png

[100]: ./media/pagerduty-tutorial/tutorial_general_100.png

[200]: ./media/pagerduty-tutorial/tutorial_general_200.png
[201]: ./media/pagerduty-tutorial/tutorial_general_201.png
[202]: ./media/pagerduty-tutorial/tutorial_general_202.png
[203]: ./media/pagerduty-tutorial/tutorial_general_203.png
