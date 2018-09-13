---
title: 'Tutorial: Azure Active Directory integration with Adaptive Insights | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Adaptive Insights.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 13af9d00-116a-41b8-8ca0-4870b31e224c
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/14/2018
ms.author: jeedes
ms.openlocfilehash: 307c3cf258a74d1ddfb409f0d5b22d9e1fd6bf4b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966316"
---
# <a name="tutorial-azure-active-directory-integration-with-adaptive-insights"></a><span data-ttu-id="c03a4-103">Tutorial: Azure Active Directory integration with Adaptive Insights</span><span class="sxs-lookup"><span data-stu-id="c03a4-103">Tutorial: Azure Active Directory integration with Adaptive Insights</span></span>

<span data-ttu-id="c03a4-104">In this tutorial, you learn how to integrate Adaptive Insights with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c03a4-104">In this tutorial, you learn how to integrate Adaptive Insights with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c03a4-105">Integrating Adaptive Insights with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="c03a4-105">Integrating Adaptive Insights with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c03a4-106">You can control in Azure AD who has access to Adaptive Insights</span><span class="sxs-lookup"><span data-stu-id="c03a4-106">You can control in Azure AD who has access to Adaptive Insights</span></span>
- <span data-ttu-id="c03a4-107">You can enable your users to automatically get signed-on to Adaptive Insights (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="c03a4-107">You can enable your users to automatically get signed-on to Adaptive Insights (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c03a4-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="c03a4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c03a4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="c03a4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c03a4-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c03a4-110">Prerequisites</span></span>

<span data-ttu-id="c03a4-111">To configure Azure AD integration with Adaptive Insights, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="c03a4-111">To configure Azure AD integration with Adaptive Insights, you need the following items:</span></span>

- <span data-ttu-id="c03a4-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="c03a4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c03a4-113">An Adaptive Insights single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="c03a4-113">An Adaptive Insights single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c03a4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="c03a4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c03a4-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="c03a4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c03a4-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="c03a4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c03a4-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c03a4-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c03a4-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="c03a4-118">Scenario description</span></span>
<span data-ttu-id="c03a4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="c03a4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c03a4-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="c03a4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c03a4-121">Adding Adaptive Insights from the gallery</span><span class="sxs-lookup"><span data-stu-id="c03a4-121">Adding Adaptive Insights from the gallery</span></span>
2. <span data-ttu-id="c03a4-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c03a4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adaptive-insights-from-the-gallery"></a><span data-ttu-id="c03a4-123">Adding Adaptive Insights from the gallery</span><span class="sxs-lookup"><span data-stu-id="c03a4-123">Adding Adaptive Insights from the gallery</span></span>
<span data-ttu-id="c03a4-124">To configure the integration of Adaptive Insights into Azure AD, you need to add Adaptive Insights from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="c03a4-124">To configure the integration of Adaptive Insights into Azure AD, you need to add Adaptive Insights from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c03a4-125">**To add Adaptive Insights from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c03a4-125">**To add Adaptive Insights from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c03a4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="c03a4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c03a4-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="c03a4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c03a4-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="c03a4-129">Then go to **All applications**.</span></span>

    ![Applications][2]

3. <span data-ttu-id="c03a4-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="c03a4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="c03a4-133">In the search box, type **Adaptive Insights**, select **Adaptive Insights** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="c03a4-133">In the search box, type **Adaptive Insights**, select **Adaptive Insights** from result panel then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/adaptivesuite-tutorial/tutorial_adaptivesuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c03a4-135">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c03a4-135">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c03a4-136">In this section, you configure and test Azure AD single sign-on with Adaptive Insights based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="c03a4-136">In this section, you configure and test Azure AD single sign-on with Adaptive Insights based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c03a4-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Adaptive Insights is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c03a4-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Adaptive Insights is to a user in Azure AD.</span></span> <span data-ttu-id="c03a4-138">In other words, a link relationship between an Azure AD user and the related user in Adaptive Insights needs to be established.</span><span class="sxs-lookup"><span data-stu-id="c03a4-138">In other words, a link relationship between an Azure AD user and the related user in Adaptive Insights needs to be established.</span></span>

<span data-ttu-id="c03a4-139">To configure and test Azure AD single sign-on with Adaptive Insights, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="c03a4-139">To configure and test Azure AD single sign-on with Adaptive Insights, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c03a4-140">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="c03a4-140">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c03a4-141">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c03a4-141">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c03a4-142">**[Creating an Adaptive Insights test user](#creating-an-adaptive-insights-test-user)** - to have a counterpart of Britta Simon in Adaptive Insights that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="c03a4-142">**[Creating an Adaptive Insights test user](#creating-an-adaptive-insights-test-user)** - to have a counterpart of Britta Simon in Adaptive Insights that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c03a4-143">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c03a4-143">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c03a4-144">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="c03a4-144">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c03a4-145">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c03a4-145">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c03a4-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Adaptive Insights application.</span><span class="sxs-lookup"><span data-stu-id="c03a4-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Adaptive Insights application.</span></span>

<span data-ttu-id="c03a4-147">**To configure Azure AD single sign-on with Adaptive Insights, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c03a4-147">**To configure Azure AD single sign-on with Adaptive Insights, perform the following steps:**</span></span>

1. <span data-ttu-id="c03a4-148">In the Azure portal, on the **Adaptive Insights** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="c03a4-148">In the Azure portal, on the **Adaptive Insights** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="c03a4-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c03a4-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Configure Single Sign-On](./media/adaptivesuite-tutorial/tutorial_adaptivesuite_samlbase.png)

3. <span data-ttu-id="c03a4-152">On the **Adaptive Insights Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c03a4-152">On the **Adaptive Insights Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/adaptivesuite-tutorial/tutorial_adaptivesuite_url.png)

    <span data-ttu-id="c03a4-154">a.</span><span class="sxs-lookup"><span data-stu-id="c03a4-154">a.</span></span> <span data-ttu-id="c03a4-155">In the **Identifier(Entity ID)** textbox, type a URL using the following pattern: `https://login.adaptiveinsights.com:443/samlsso/<unique-id>`</span><span class="sxs-lookup"><span data-stu-id="c03a4-155">In the **Identifier(Entity ID)** textbox, type a URL using the following pattern: `https://login.adaptiveinsights.com:443/samlsso/<unique-id>`</span></span>

    <span data-ttu-id="c03a4-156">b.</span><span class="sxs-lookup"><span data-stu-id="c03a4-156">b.</span></span> <span data-ttu-id="c03a4-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://login.adaptiveinsights.com:443/samlsso/<unique-id>`</span><span class="sxs-lookup"><span data-stu-id="c03a4-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://login.adaptiveinsights.com:443/samlsso/<unique-id>`</span></span>

    >[!NOTE]
    > <span data-ttu-id="c03a4-158">You can get Identifier(Entity ID) and Reply URL values from the Adaptive Insights’s **SAML SSO Settings** page.</span><span class="sxs-lookup"><span data-stu-id="c03a4-158">You can get Identifier(Entity ID) and Reply URL values from the Adaptive Insights’s **SAML SSO Settings** page.</span></span>

4. <span data-ttu-id="c03a4-159">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="c03a4-159">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/adaptivesuite-tutorial/tutorial_adaptivesuite_certificate.png)

5. <span data-ttu-id="c03a4-161">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="c03a4-161">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/adaptivesuite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c03a4-163">On the **Adaptive Insights Configuration** section, click **Configure Adaptive Insights** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="c03a4-163">On the **Adaptive Insights Configuration** section, click **Configure Adaptive Insights** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c03a4-164">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="c03a4-164">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/adaptivesuite-tutorial/tutorial_adaptivesuite_configure.png) 

7. <span data-ttu-id="c03a4-166">In a different web browser window, log in to your Adaptive Insights company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="c03a4-166">In a different web browser window, log in to your Adaptive Insights company site as an administrator.</span></span>

8. <span data-ttu-id="c03a4-167">Go to **Admin**.</span><span class="sxs-lookup"><span data-stu-id="c03a4-167">Go to **Admin**.</span></span>

    <span data-ttu-id="c03a4-168">![Admin](./media/adaptivesuite-tutorial/IC805644.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="c03a4-168">![Admin](./media/adaptivesuite-tutorial/IC805644.png "Admin")</span></span>

9. <span data-ttu-id="c03a4-169">In the **Users and Roles** section, click **Manage SAML SSO Settings**.</span><span class="sxs-lookup"><span data-stu-id="c03a4-169">In the **Users and Roles** section, click **Manage SAML SSO Settings**.</span></span>

    <span data-ttu-id="c03a4-170">![Manage SAML SSO Settings](./media/adaptivesuite-tutorial/IC805645.png "Manage SAML SSO Settings")</span><span class="sxs-lookup"><span data-stu-id="c03a4-170">![Manage SAML SSO Settings](./media/adaptivesuite-tutorial/IC805645.png "Manage SAML SSO Settings")</span></span>

10. <span data-ttu-id="c03a4-171">On the **SAML SSO Settings** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c03a4-171">On the **SAML SSO Settings** page, perform the following steps:</span></span>

    <span data-ttu-id="c03a4-172">![SAML SSO Settings](./media/adaptivesuite-tutorial/IC805646.png "SAML SSO Settings")</span><span class="sxs-lookup"><span data-stu-id="c03a4-172">![SAML SSO Settings](./media/adaptivesuite-tutorial/IC805646.png "SAML SSO Settings")</span></span>

    <span data-ttu-id="c03a4-173">a.</span><span class="sxs-lookup"><span data-stu-id="c03a4-173">a.</span></span> <span data-ttu-id="c03a4-174">In the **Identity provider name** textbox, type a name for your configuration.</span><span class="sxs-lookup"><span data-stu-id="c03a4-174">In the **Identity provider name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="c03a4-175">b.</span><span class="sxs-lookup"><span data-stu-id="c03a4-175">b.</span></span> <span data-ttu-id="c03a4-176">Paste the **SAML Entity ID** value copied from Azure portal into the **Identity provider Entity ID** textbox.</span><span class="sxs-lookup"><span data-stu-id="c03a4-176">Paste the **SAML Entity ID** value copied from Azure portal into the **Identity provider Entity ID** textbox.</span></span>

    <span data-ttu-id="c03a4-177">c.</span><span class="sxs-lookup"><span data-stu-id="c03a4-177">c.</span></span> <span data-ttu-id="c03a4-178">Paste the **SAML Single Sign-On Service URL** value copied from Azure portal into the **Identity provider SSO URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="c03a4-178">Paste the **SAML Single Sign-On Service URL** value copied from Azure portal into the **Identity provider SSO URL** textbox.</span></span>

    <span data-ttu-id="c03a4-179">d.</span><span class="sxs-lookup"><span data-stu-id="c03a4-179">d.</span></span> <span data-ttu-id="c03a4-180">Paste the **SAML Single Sign-On Service URL** value copied from Azure portal into the **Custom logout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="c03a4-180">Paste the **SAML Single Sign-On Service URL** value copied from Azure portal into the **Custom logout URL** textbox.</span></span>

    <span data-ttu-id="c03a4-181">e.</span><span class="sxs-lookup"><span data-stu-id="c03a4-181">e.</span></span> <span data-ttu-id="c03a4-182">To upload your downloaded certificate, click **Choose file**.</span><span class="sxs-lookup"><span data-stu-id="c03a4-182">To upload your downloaded certificate, click **Choose file**.</span></span>

    <span data-ttu-id="c03a4-183">f.</span><span class="sxs-lookup"><span data-stu-id="c03a4-183">f.</span></span> <span data-ttu-id="c03a4-184">Select the following, for:</span><span class="sxs-lookup"><span data-stu-id="c03a4-184">Select the following, for:</span></span>

    * <span data-ttu-id="c03a4-185">**SAML user id**, select **User’s Adaptive Insights user name**.</span><span class="sxs-lookup"><span data-stu-id="c03a4-185">**SAML user id**, select **User’s Adaptive Insights user name**.</span></span>

    * <span data-ttu-id="c03a4-186">**SAML user id location**, select **User id in NameID of Subject**.</span><span class="sxs-lookup"><span data-stu-id="c03a4-186">**SAML user id location**, select **User id in NameID of Subject**.</span></span>

    * <span data-ttu-id="c03a4-187">**SAML NameID format**, select **Email address**.</span><span class="sxs-lookup"><span data-stu-id="c03a4-187">**SAML NameID format**, select **Email address**.</span></span>

    * <span data-ttu-id="c03a4-188">**Enable SAML**, select **Allow SAML SSO and direct Adaptive Insights login**.</span><span class="sxs-lookup"><span data-stu-id="c03a4-188">**Enable SAML**, select **Allow SAML SSO and direct Adaptive Insights login**.</span></span>

    <span data-ttu-id="c03a4-189">g.</span><span class="sxs-lookup"><span data-stu-id="c03a4-189">g.</span></span> <span data-ttu-id="c03a4-190">Copy **Adaptive Insights SSO URL** and paste into the **Identifier(Entity ID)** and **Reply URL** textboxes in the **Adaptive Insights Domain and URLs** section in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c03a4-190">Copy **Adaptive Insights SSO URL** and paste into the **Identifier(Entity ID)** and **Reply URL** textboxes in the **Adaptive Insights Domain and URLs** section in the Azure portal.</span></span>

    <span data-ttu-id="c03a4-191">h.</span><span class="sxs-lookup"><span data-stu-id="c03a4-191">h.</span></span> <span data-ttu-id="c03a4-192">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="c03a4-192">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c03a4-193">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="c03a4-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="c03a4-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c03a4-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="c03a4-196">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c03a4-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c03a4-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="c03a4-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/adaptivesuite-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c03a4-199">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="c03a4-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>

    ![Creating an Azure AD test user](./media/adaptivesuite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c03a4-201">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="c03a4-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>

    ![Creating an Azure AD test user](./media/adaptivesuite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c03a4-203">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c03a4-203">On the **User** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](./media/adaptivesuite-tutorial/create_aaduser_04.png)

    <span data-ttu-id="c03a4-205">a.</span><span class="sxs-lookup"><span data-stu-id="c03a4-205">a.</span></span> <span data-ttu-id="c03a4-206">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c03a4-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c03a4-207">b.</span><span class="sxs-lookup"><span data-stu-id="c03a4-207">b.</span></span> <span data-ttu-id="c03a4-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c03a4-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c03a4-209">c.</span><span class="sxs-lookup"><span data-stu-id="c03a4-209">c.</span></span> <span data-ttu-id="c03a4-210">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="c03a4-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c03a4-211">d.</span><span class="sxs-lookup"><span data-stu-id="c03a4-211">d.</span></span> <span data-ttu-id="c03a4-212">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="c03a4-212">Click **Create**.</span></span>

### <a name="creating-an-adaptive-insights-test-user"></a><span data-ttu-id="c03a4-213">Creating an Adaptive Insights test user</span><span class="sxs-lookup"><span data-stu-id="c03a4-213">Creating an Adaptive Insights test user</span></span>

<span data-ttu-id="c03a4-214">To enable Azure AD users to log in to Adaptive Insights, they must be provisioned into Adaptive Insights.</span><span class="sxs-lookup"><span data-stu-id="c03a4-214">To enable Azure AD users to log in to Adaptive Insights, they must be provisioned into Adaptive Insights.</span></span> <span data-ttu-id="c03a4-215">In the case of Adaptive Insights, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="c03a4-215">In the case of Adaptive Insights, provisioning is a manual task.</span></span>

<span data-ttu-id="c03a4-216">**To configure user provisioning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c03a4-216">**To configure user provisioning, perform the following steps:**</span></span> 

1. <span data-ttu-id="c03a4-217">Log in to your **Adaptive Insights** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="c03a4-217">Log in to your **Adaptive Insights** company site as an administrator.</span></span>
2. <span data-ttu-id="c03a4-218">Go to **Admin**.</span><span class="sxs-lookup"><span data-stu-id="c03a4-218">Go to **Admin**.</span></span>

   <span data-ttu-id="c03a4-219">![Admin](./media/adaptivesuite-tutorial/IC805644.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="c03a4-219">![Admin](./media/adaptivesuite-tutorial/IC805644.png "Admin")</span></span>
3. <span data-ttu-id="c03a4-220">In the **Users and Roles** section, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="c03a4-220">In the **Users and Roles** section, click **Add User**.</span></span>

   <span data-ttu-id="c03a4-221">![Add User](./media/adaptivesuite-tutorial/IC805648.png "Add User")</span><span class="sxs-lookup"><span data-stu-id="c03a4-221">![Add User](./media/adaptivesuite-tutorial/IC805648.png "Add User")</span></span>
4. <span data-ttu-id="c03a4-222">In the **New User** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c03a4-222">In the **New User** section, perform the following steps:</span></span>

   <span data-ttu-id="c03a4-223">![Submit](./media/adaptivesuite-tutorial/IC805649.png "Submit")</span><span class="sxs-lookup"><span data-stu-id="c03a4-223">![Submit](./media/adaptivesuite-tutorial/IC805649.png "Submit")</span></span>

   <span data-ttu-id="c03a4-224">a.</span><span class="sxs-lookup"><span data-stu-id="c03a4-224">a.</span></span> <span data-ttu-id="c03a4-225">Type the **Name**, **Login**, **Email**, **Password** of a valid Azure Active Directory user you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="c03a4-225">Type the **Name**, **Login**, **Email**, **Password** of a valid Azure Active Directory user you want to provision into the related textboxes.</span></span>

   <span data-ttu-id="c03a4-226">b.</span><span class="sxs-lookup"><span data-stu-id="c03a4-226">b.</span></span> <span data-ttu-id="c03a4-227">Select a **Role**.</span><span class="sxs-lookup"><span data-stu-id="c03a4-227">Select a **Role**.</span></span>

   <span data-ttu-id="c03a4-228">c.</span><span class="sxs-lookup"><span data-stu-id="c03a4-228">c.</span></span> <span data-ttu-id="c03a4-229">Click **Submit**.</span><span class="sxs-lookup"><span data-stu-id="c03a4-229">Click **Submit**.</span></span>

>[!NOTE]
><span data-ttu-id="c03a4-230">You can use any other Adaptive Insights user account creation tools or APIs provided by Adaptive Insights to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="c03a4-230">You can use any other Adaptive Insights user account creation tools or APIs provided by Adaptive Insights to provision AAD user accounts.</span></span>
>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c03a4-231">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="c03a4-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c03a4-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Adaptive Insights.</span><span class="sxs-lookup"><span data-stu-id="c03a4-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Adaptive Insights.</span></span>

![Assign User][200]

<span data-ttu-id="c03a4-234">**To assign Britta Simon to Adaptive Insights, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c03a4-234">**To assign Britta Simon to Adaptive Insights, perform the following steps:**</span></span>

1. <span data-ttu-id="c03a4-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="c03a4-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201]

2. <span data-ttu-id="c03a4-237">In the applications list, select **Adaptive Insights**.</span><span class="sxs-lookup"><span data-stu-id="c03a4-237">In the applications list, select **Adaptive Insights**.</span></span>

    ![Configure Single Sign-On](./media/adaptivesuite-tutorial/tutorial_adaptivesuite_app.png)

3. <span data-ttu-id="c03a4-239">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="c03a4-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202]

4. <span data-ttu-id="c03a4-241">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="c03a4-241">Click **Add** button.</span></span> <span data-ttu-id="c03a4-242">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="c03a4-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="c03a4-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="c03a4-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c03a4-245">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="c03a4-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c03a4-246">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="c03a4-246">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="c03a4-247">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="c03a4-247">Testing single sign-on</span></span>

<span data-ttu-id="c03a4-248">The objective of this section is to test your Microsoft Azure AD Single Sign-On configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="c03a4-248">The objective of this section is to test your Microsoft Azure AD Single Sign-On configuration using the Access Panel.</span></span>

<span data-ttu-id="c03a4-249">When you click the Adaptive Insights tile in the Access Panel, you should get automatically signed-on to your Adaptive Insights application.</span><span class="sxs-lookup"><span data-stu-id="c03a4-249">When you click the Adaptive Insights tile in the Access Panel, you should get automatically signed-on to your Adaptive Insights application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c03a4-250">Additional resources</span><span class="sxs-lookup"><span data-stu-id="c03a4-250">Additional resources</span></span>

* [<span data-ttu-id="c03a4-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c03a4-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="c03a4-252">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c03a4-252">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/adaptivesuite-tutorial/tutorial_general_01.png
[2]: ./media/adaptivesuite-tutorial/tutorial_general_02.png
[3]: ./media/adaptivesuite-tutorial/tutorial_general_03.png
[4]: ./media/adaptivesuite-tutorial/tutorial_general_04.png

[100]: ./media/adaptivesuite-tutorial/tutorial_general_100.png

[200]: ./media/adaptivesuite-tutorial/tutorial_general_200.png
[201]: ./media/adaptivesuite-tutorial/tutorial_general_201.png
[202]: ./media/adaptivesuite-tutorial/tutorial_general_202.png
[203]: ./media/adaptivesuite-tutorial/tutorial_general_203.png
