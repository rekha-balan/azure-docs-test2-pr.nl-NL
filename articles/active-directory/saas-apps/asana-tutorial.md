---
title: 'Tutorial: Azure Active Directory integration with Asana | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Asana.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 837e38fe-8f55-475c-87f4-6394dc1fee2b
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2018
ms.author: jeedes
ms.openlocfilehash: f5ea7a330891d4befeb6388bbe7f37b2a4aa848f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869884"
---
# <a name="tutorial-azure-active-directory-integration-with-asana"></a><span data-ttu-id="9dace-103">Tutorial: Azure Active Directory integration with Asana</span><span class="sxs-lookup"><span data-stu-id="9dace-103">Tutorial: Azure Active Directory integration with Asana</span></span>

<span data-ttu-id="9dace-104">In this tutorial, you learn how to integrate Asana with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9dace-104">In this tutorial, you learn how to integrate Asana with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9dace-105">Integrating Asana with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="9dace-105">Integrating Asana with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9dace-106">You can control in Azure AD who has access to Asana</span><span class="sxs-lookup"><span data-stu-id="9dace-106">You can control in Azure AD who has access to Asana</span></span>
- <span data-ttu-id="9dace-107">You can enable your users to automatically get signed-on to Asana (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="9dace-107">You can enable your users to automatically get signed-on to Asana (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9dace-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="9dace-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9dace-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="9dace-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9dace-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9dace-110">Prerequisites</span></span>

<span data-ttu-id="9dace-111">To configure Azure AD integration with Asana, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="9dace-111">To configure Azure AD integration with Asana, you need the following items:</span></span>

- <span data-ttu-id="9dace-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="9dace-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9dace-113">An Asana single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="9dace-113">An Asana single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9dace-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="9dace-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9dace-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="9dace-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9dace-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="9dace-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9dace-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9dace-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9dace-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="9dace-118">Scenario description</span></span>
<span data-ttu-id="9dace-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="9dace-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>
<span data-ttu-id="9dace-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="9dace-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9dace-121">Adding Asana from the gallery</span><span class="sxs-lookup"><span data-stu-id="9dace-121">Adding Asana from the gallery</span></span>
1. <span data-ttu-id="9dace-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9dace-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-asana-from-the-gallery"></a><span data-ttu-id="9dace-123">Adding Asana from the gallery</span><span class="sxs-lookup"><span data-stu-id="9dace-123">Adding Asana from the gallery</span></span>
<span data-ttu-id="9dace-124">To configure the integration of Asana into Azure AD, you need to add Asana from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="9dace-124">To configure the integration of Asana into Azure AD, you need to add Asana from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9dace-125">**To add Asana from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9dace-125">**To add Asana from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9dace-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="9dace-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="9dace-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="9dace-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9dace-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="9dace-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]

1. <span data-ttu-id="9dace-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="9dace-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="9dace-133">In the search box, type **Asana**, select **Asana** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="9dace-133">In the search box, type **Asana**, select **Asana** from result panel then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/asana-tutorial/tutorial_asana_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9dace-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9dace-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="9dace-136">In this section, you configure and test Azure AD single sign-on with Asana based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="9dace-136">In this section, you configure and test Azure AD single sign-on with Asana based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9dace-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Asana is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9dace-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Asana is to a user in Azure AD.</span></span> <span data-ttu-id="9dace-138">In other words, a link relationship between an Azure AD user and the related user in Asana needs to be established.</span><span class="sxs-lookup"><span data-stu-id="9dace-138">In other words, a link relationship between an Azure AD user and the related user in Asana needs to be established.</span></span>

<span data-ttu-id="9dace-139">In Asana, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="9dace-139">In Asana, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9dace-140">To configure and test Azure AD single sign-on with Asana, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="9dace-140">To configure and test Azure AD single sign-on with Asana, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9dace-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="9dace-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="9dace-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9dace-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="9dace-143">**[Create an Asana test user](#create-an-asana-test-user)** - to have a counterpart of Britta Simon in Asana that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="9dace-143">**[Create an Asana test user](#create-an-asana-test-user)** - to have a counterpart of Britta Simon in Asana that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="9dace-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9dace-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="9dace-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="9dace-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9dace-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9dace-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="9dace-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Asana application.</span><span class="sxs-lookup"><span data-stu-id="9dace-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Asana application.</span></span>

<span data-ttu-id="9dace-148">**To configure Azure AD single sign-on with Asana, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9dace-148">**To configure Azure AD single sign-on with Asana, perform the following steps:**</span></span>

1. <span data-ttu-id="9dace-149">In the Azure portal, on the **Asana** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="9dace-149">In the Azure portal, on the **Asana** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="9dace-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9dace-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/asana-tutorial/tutorial_asana_samlbase.png)

1. <span data-ttu-id="9dace-153">On the **Asana Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9dace-153">On the **Asana Domain and URLs** section, perform the following steps:</span></span>

    ![Asana Domain and URLs single sign-on information](./media/asana-tutorial/tutorial_asana_url.png)

    <span data-ttu-id="9dace-155">a.</span><span class="sxs-lookup"><span data-stu-id="9dace-155">a.</span></span> <span data-ttu-id="9dace-156">In the **Sign-on URL** textbox, type URL: `https://app.asana.com/`</span><span class="sxs-lookup"><span data-stu-id="9dace-156">In the **Sign-on URL** textbox, type URL: `https://app.asana.com/`</span></span>

    <span data-ttu-id="9dace-157">b.</span><span class="sxs-lookup"><span data-stu-id="9dace-157">b.</span></span> <span data-ttu-id="9dace-158">In the **Identifier** textbox, type value: `https://app.asana.com/`</span><span class="sxs-lookup"><span data-stu-id="9dace-158">In the **Identifier** textbox, type value: `https://app.asana.com/`</span></span>

1. <span data-ttu-id="9dace-159">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="9dace-159">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/asana-tutorial/tutorial_asana_certificate.png)

1. <span data-ttu-id="9dace-161">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="9dace-161">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/asana-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="9dace-163">On the **Asana Configuration** section, click **Configure Asana** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="9dace-163">On the **Asana Configuration** section, click **Configure Asana** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9dace-164">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="9dace-164">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Asana Configuration](./media/asana-tutorial/tutorial_asana_configure.png)

1. <span data-ttu-id="9dace-166">In a different browser window, sign-on to your Asana application.</span><span class="sxs-lookup"><span data-stu-id="9dace-166">In a different browser window, sign-on to your Asana application.</span></span> <span data-ttu-id="9dace-167">To configure SSO in Asana, access the workspace settings by clicking the workspace name on the top right corner of the screen.</span><span class="sxs-lookup"><span data-stu-id="9dace-167">To configure SSO in Asana, access the workspace settings by clicking the workspace name on the top right corner of the screen.</span></span> <span data-ttu-id="9dace-168">Then, click on **\<your workspace name\> Settings**.</span><span class="sxs-lookup"><span data-stu-id="9dace-168">Then, click on **\<your workspace name\> Settings**.</span></span>

    ![Asana sso settings](./media/asana-tutorial/tutorial_asana_09.png)

1. <span data-ttu-id="9dace-170">On the **Organization settings** window, click **Administration**.</span><span class="sxs-lookup"><span data-stu-id="9dace-170">On the **Organization settings** window, click **Administration**.</span></span> <span data-ttu-id="9dace-171">Then, click **Members must log in via SAML** to enable the SSO configuration.</span><span class="sxs-lookup"><span data-stu-id="9dace-171">Then, click **Members must log in via SAML** to enable the SSO configuration.</span></span> <span data-ttu-id="9dace-172">The perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9dace-172">The perform the following steps:</span></span>

    ![Configure Single Sign-On Organization settings](./media/asana-tutorial/tutorial_asana_10.png)  

     <span data-ttu-id="9dace-174">a.</span><span class="sxs-lookup"><span data-stu-id="9dace-174">a.</span></span> <span data-ttu-id="9dace-175">In the **Sign-in page URL** textbox, paste the **SAML Single Sign-On Service URL**.</span><span class="sxs-lookup"><span data-stu-id="9dace-175">In the **Sign-in page URL** textbox, paste the **SAML Single Sign-On Service URL**.</span></span>

     <span data-ttu-id="9dace-176">b.</span><span class="sxs-lookup"><span data-stu-id="9dace-176">b.</span></span> <span data-ttu-id="9dace-177">Right click the certificate downloaded from Azure portal, then open the certificate file using Notepad or your preferred text editor.</span><span class="sxs-lookup"><span data-stu-id="9dace-177">Right click the certificate downloaded from Azure portal, then open the certificate file using Notepad or your preferred text editor.</span></span> <span data-ttu-id="9dace-178">Copy the content between the begin and the end certificate title and paste it in the **X.509 Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="9dace-178">Copy the content between the begin and the end certificate title and paste it in the **X.509 Certificate** textbox.</span></span>

1. <span data-ttu-id="9dace-179">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="9dace-179">Click **Save**.</span></span> <span data-ttu-id="9dace-180">Go to [Asana guide for setting up SSO](https://asana.com/guide/help/premium/authentication#gl-saml) if you need further assistance.</span><span class="sxs-lookup"><span data-stu-id="9dace-180">Go to [Asana guide for setting up SSO](https://asana.com/guide/help/premium/authentication#gl-saml) if you need further assistance.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9dace-181">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="9dace-181">Create an Azure AD test user</span></span>

<span data-ttu-id="9dace-182">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9dace-182">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create an Azure AD test user][100]

<span data-ttu-id="9dace-184">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9dace-184">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9dace-185">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="9dace-185">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![The Azure Active Directory button](./media/asana-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="9dace-187">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="9dace-187">To display the list of users, go to **Users and groups** and click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/asana-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="9dace-189">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="9dace-189">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>

    ![Creating an Azure AD test user](./media/asana-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="9dace-191">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9dace-191">On the **User** dialog page, perform the following steps:</span></span>

    ![The Add button](./media/asana-tutorial/create_aaduser_04.png)

    <span data-ttu-id="9dace-193">a.</span><span class="sxs-lookup"><span data-stu-id="9dace-193">a.</span></span> <span data-ttu-id="9dace-194">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9dace-194">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9dace-195">b.</span><span class="sxs-lookup"><span data-stu-id="9dace-195">b.</span></span> <span data-ttu-id="9dace-196">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9dace-196">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9dace-197">c.</span><span class="sxs-lookup"><span data-stu-id="9dace-197">c.</span></span> <span data-ttu-id="9dace-198">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="9dace-198">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9dace-199">d.</span><span class="sxs-lookup"><span data-stu-id="9dace-199">d.</span></span> <span data-ttu-id="9dace-200">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="9dace-200">Click **Create**.</span></span>

### <a name="create-an-asana-test-user"></a><span data-ttu-id="9dace-201">Create an Asana test user</span><span class="sxs-lookup"><span data-stu-id="9dace-201">Create an Asana test user</span></span>

<span data-ttu-id="9dace-202">The objective of this section is to create a user called Britta Simon in Asana.</span><span class="sxs-lookup"><span data-stu-id="9dace-202">The objective of this section is to create a user called Britta Simon in Asana.</span></span> <span data-ttu-id="9dace-203">Asana supports automatic user provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="9dace-203">Asana supports automatic user provisioning, which is by default enabled.</span></span> <span data-ttu-id="9dace-204">You can find more details [here](asana-provisioning-tutorial.md) on how to configure automatic user provisioning.</span><span class="sxs-lookup"><span data-stu-id="9dace-204">You can find more details [here](asana-provisioning-tutorial.md) on how to configure automatic user provisioning.</span></span>

<span data-ttu-id="9dace-205">**If you need to create user manually, please perform following steps:**</span><span class="sxs-lookup"><span data-stu-id="9dace-205">**If you need to create user manually, please perform following steps:**</span></span>

<span data-ttu-id="9dace-206">In this section, you create a user called Britta Simon in Asana.</span><span class="sxs-lookup"><span data-stu-id="9dace-206">In this section, you create a user called Britta Simon in Asana.</span></span>

1. <span data-ttu-id="9dace-207">On **Asana**, go to the **Teams** section on the left panel.</span><span class="sxs-lookup"><span data-stu-id="9dace-207">On **Asana**, go to the **Teams** section on the left panel.</span></span> <span data-ttu-id="9dace-208">Click the plus sign button.</span><span class="sxs-lookup"><span data-stu-id="9dace-208">Click the plus sign button.</span></span>

    ![Creating an Azure AD test user](./media/asana-tutorial/tutorial_asana_12.png)

1. <span data-ttu-id="9dace-210">Type the email britta.simon@contoso.com in the text box and then select **Invite**.</span><span class="sxs-lookup"><span data-stu-id="9dace-210">Type the email britta.simon@contoso.com in the text box and then select **Invite**.</span></span>

1. <span data-ttu-id="9dace-211">Click **Send Invite**.</span><span class="sxs-lookup"><span data-stu-id="9dace-211">Click **Send Invite**.</span></span> <span data-ttu-id="9dace-212">The new user will receive an email into her email account.</span><span class="sxs-lookup"><span data-stu-id="9dace-212">The new user will receive an email into her email account.</span></span> <span data-ttu-id="9dace-213">She will need to create and validate the account.</span><span class="sxs-lookup"><span data-stu-id="9dace-213">She will need to create and validate the account.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="9dace-214">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="9dace-214">Assign the Azure AD test user</span></span>

<span data-ttu-id="9dace-215">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Asana.</span><span class="sxs-lookup"><span data-stu-id="9dace-215">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Asana.</span></span>

![Assign the user role][200]

<span data-ttu-id="9dace-217">**To assign Britta Simon to Asana, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9dace-217">**To assign Britta Simon to Asana, perform the following steps:**</span></span>

1. <span data-ttu-id="9dace-218">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="9dace-218">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201]

1. <span data-ttu-id="9dace-220">In the applications list, select **Asana**.</span><span class="sxs-lookup"><span data-stu-id="9dace-220">In the applications list, select **Asana**.</span></span>

    ![The Asana link in the Applications list](./media/asana-tutorial/tutorial_asana_app.png)

1. <span data-ttu-id="9dace-222">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="9dace-222">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="9dace-224">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="9dace-224">Click **Add** button.</span></span> <span data-ttu-id="9dace-225">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="9dace-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="9dace-227">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="9dace-227">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="9dace-228">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="9dace-228">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="9dace-229">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="9dace-229">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="9dace-230">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="9dace-230">Test single sign-on</span></span>

<span data-ttu-id="9dace-231">The objective of this section is to test your Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9dace-231">The objective of this section is to test your Azure AD single sign-on.</span></span>

<span data-ttu-id="9dace-232">Go to Asana login page.</span><span class="sxs-lookup"><span data-stu-id="9dace-232">Go to Asana login page.</span></span> <span data-ttu-id="9dace-233">In the Email address textbox, insert the email address britta.simon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="9dace-233">In the Email address textbox, insert the email address britta.simon@contoso.com.</span></span> <span data-ttu-id="9dace-234">Leave the password textbox in blank and then click **Log In**.</span><span class="sxs-lookup"><span data-stu-id="9dace-234">Leave the password textbox in blank and then click **Log In**.</span></span> <span data-ttu-id="9dace-235">You will be redirected to Azure AD login page.</span><span class="sxs-lookup"><span data-stu-id="9dace-235">You will be redirected to Azure AD login page.</span></span> <span data-ttu-id="9dace-236">Complete your Azure AD credentials.</span><span class="sxs-lookup"><span data-stu-id="9dace-236">Complete your Azure AD credentials.</span></span> <span data-ttu-id="9dace-237">Now, you are logged in on Asana.</span><span class="sxs-lookup"><span data-stu-id="9dace-237">Now, you are logged in on Asana.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9dace-238">Additional resources</span><span class="sxs-lookup"><span data-stu-id="9dace-238">Additional resources</span></span>

* [<span data-ttu-id="9dace-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9dace-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="9dace-240">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9dace-240">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)
* [<span data-ttu-id="9dace-241">Configure User Provisioning</span><span class="sxs-lookup"><span data-stu-id="9dace-241">Configure User Provisioning</span></span>](asana-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/asana-tutorial/tutorial_general_01.png
[2]: ./media/asana-tutorial/tutorial_general_02.png
[3]: ./media/asana-tutorial/tutorial_general_03.png
[4]: ./media/asana-tutorial/tutorial_general_04.png

[100]: ./media/asana-tutorial/tutorial_general_100.png

[200]: ./media/asana-tutorial/tutorial_general_200.png
[201]: ./media/asana-tutorial/tutorial_general_201.png
[202]: ./media/asana-tutorial/tutorial_general_202.png
[203]: ./media/asana-tutorial/tutorial_general_203.png
[10]: ./media/asana-tutorial/tutorial_general_060.png
[11]: ./media/asana-tutorial/tutorial_general_070.png