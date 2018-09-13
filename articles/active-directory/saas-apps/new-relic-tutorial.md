---
title: 'Tutorial: Azure Active Directory integration with New Relic | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and New Relic.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 3186b9a8-f4d8-45e2-ad82-6275f95e7aa6
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/31/2017
ms.author: jeedes
ms.openlocfilehash: 80bd77504f1b2ab5b6e5c781eadb7c2cd4c99220
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869273"
---
# <a name="tutorial-azure-active-directory-integration-with-new-relic"></a><span data-ttu-id="25f1f-103">Tutorial: Azure Active Directory integration with New Relic</span><span class="sxs-lookup"><span data-stu-id="25f1f-103">Tutorial: Azure Active Directory integration with New Relic</span></span>

<span data-ttu-id="25f1f-104">In this tutorial, you learn how to integrate New Relic with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="25f1f-104">In this tutorial, you learn how to integrate New Relic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="25f1f-105">Integrating New Relic with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="25f1f-105">Integrating New Relic with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="25f1f-106">You can control in Azure AD who has access to New Relic.</span><span class="sxs-lookup"><span data-stu-id="25f1f-106">You can control in Azure AD who has access to New Relic.</span></span>
- <span data-ttu-id="25f1f-107">You can enable your users to automatically get signed-on to New Relic (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="25f1f-107">You can enable your users to automatically get signed-on to New Relic (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="25f1f-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="25f1f-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="25f1f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="25f1f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="25f1f-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="25f1f-110">Prerequisites</span></span>

<span data-ttu-id="25f1f-111">To configure Azure AD integration with New Relic, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="25f1f-111">To configure Azure AD integration with New Relic, you need the following items:</span></span>

- <span data-ttu-id="25f1f-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="25f1f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="25f1f-113">A New Relic single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="25f1f-113">A New Relic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="25f1f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="25f1f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="25f1f-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="25f1f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="25f1f-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="25f1f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="25f1f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="25f1f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="25f1f-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="25f1f-118">Scenario description</span></span>
<span data-ttu-id="25f1f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="25f1f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="25f1f-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="25f1f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="25f1f-121">Adding New Relic from the gallery</span><span class="sxs-lookup"><span data-stu-id="25f1f-121">Adding New Relic from the gallery</span></span>
1. <span data-ttu-id="25f1f-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="25f1f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-new-relic-from-the-gallery"></a><span data-ttu-id="25f1f-123">Adding New Relic from the gallery</span><span class="sxs-lookup"><span data-stu-id="25f1f-123">Adding New Relic from the gallery</span></span>
<span data-ttu-id="25f1f-124">To configure the integration of New Relic into Azure AD, you need to add New Relic from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="25f1f-124">To configure the integration of New Relic into Azure AD, you need to add New Relic from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="25f1f-125">**To add New Relic from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="25f1f-125">**To add New Relic from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="25f1f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="25f1f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="25f1f-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="25f1f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="25f1f-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="25f1f-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="25f1f-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="25f1f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="25f1f-133">In the search box, type **New Relic**, select **New Relic** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="25f1f-133">In the search box, type **New Relic**, select **New Relic** from result panel then click **Add** button to add the application.</span></span>

    ![New Relic in the results list](./media/new-relic-tutorial/tutorial_new-relic_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="25f1f-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="25f1f-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="25f1f-136">In this section, you configure and test Azure AD single sign-on with New Relic based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="25f1f-136">In this section, you configure and test Azure AD single sign-on with New Relic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="25f1f-137">For single sign-on to work, Azure AD needs to know what the counterpart user in New Relic is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="25f1f-137">For single sign-on to work, Azure AD needs to know what the counterpart user in New Relic is to a user in Azure AD.</span></span> <span data-ttu-id="25f1f-138">In other words, a link relationship between an Azure AD user and the related user in New Relic needs to be established.</span><span class="sxs-lookup"><span data-stu-id="25f1f-138">In other words, a link relationship between an Azure AD user and the related user in New Relic needs to be established.</span></span>

<span data-ttu-id="25f1f-139">In New Relic, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="25f1f-139">In New Relic, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="25f1f-140">To configure and test Azure AD single sign-on with New Relic, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="25f1f-140">To configure and test Azure AD single sign-on with New Relic, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="25f1f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="25f1f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="25f1f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="25f1f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="25f1f-143">**[Create a New Relic test user](#create-a-new-relic-test-user)** - to have a counterpart of Britta Simon in New Relic that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="25f1f-143">**[Create a New Relic test user](#create-a-new-relic-test-user)** - to have a counterpart of Britta Simon in New Relic that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="25f1f-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="25f1f-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="25f1f-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="25f1f-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="25f1f-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="25f1f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="25f1f-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your New Relic application.</span><span class="sxs-lookup"><span data-stu-id="25f1f-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your New Relic application.</span></span>

<span data-ttu-id="25f1f-148">**To configure Azure AD single sign-on with New Relic, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="25f1f-148">**To configure Azure AD single sign-on with New Relic, perform the following steps:**</span></span>

1. <span data-ttu-id="25f1f-149">In the Azure portal, on the **New Relic** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="25f1f-149">In the Azure portal, on the **New Relic** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="25f1f-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="25f1f-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/new-relic-tutorial/tutorial_new-relic_samlbase.png)

1. <span data-ttu-id="25f1f-153">On the **New Relic Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="25f1f-153">On the **New Relic Domain and URLs** section, perform the following steps:</span></span>

    ![New Relic Domain and URLs single sign-on information](./media/new-relic-tutorial/tutorial_new-relic_url.png)

    <span data-ttu-id="25f1f-155">a.</span><span class="sxs-lookup"><span data-stu-id="25f1f-155">a.</span></span> <span data-ttu-id="25f1f-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://rpm.newrelic.com/accounts/{acc_id}/sso/saml/login` - Be sure to substitute your own New Relic Account ID.</span><span class="sxs-lookup"><span data-stu-id="25f1f-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://rpm.newrelic.com/accounts/{acc_id}/sso/saml/login` - Be sure to substitute your own New Relic Account ID.</span></span>

    <span data-ttu-id="25f1f-157">b.</span><span class="sxs-lookup"><span data-stu-id="25f1f-157">b.</span></span> <span data-ttu-id="25f1f-158">In the **Identifier** textbox, type the value: `rpm.newrelic.com`</span><span class="sxs-lookup"><span data-stu-id="25f1f-158">In the **Identifier** textbox, type the value: `rpm.newrelic.com`</span></span>

1. <span data-ttu-id="25f1f-159">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="25f1f-159">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/new-relic-tutorial/tutorial_new-relic_certificate.png) 

1. <span data-ttu-id="25f1f-161">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="25f1f-161">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/new-relic-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="25f1f-163">On the **New Relic Configuration** section, click **Configure New Relic** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="25f1f-163">On the **New Relic Configuration** section, click **Configure New Relic** to open **Configure sign-on** window.</span></span> <span data-ttu-id="25f1f-164">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="25f1f-164">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![New Relic Configuration](./media/new-relic-tutorial/tutorial_new-relic_configure.png) 

1. <span data-ttu-id="25f1f-166">In a different web browser window, sign on to your **New Relic** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="25f1f-166">In a different web browser window, sign on to your **New Relic** company site as administrator.</span></span>

1. <span data-ttu-id="25f1f-167">In the menu on the top, click **Account Settings**.</span><span class="sxs-lookup"><span data-stu-id="25f1f-167">In the menu on the top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="25f1f-168">![Account Settings](./media/new-relic-tutorial/ic797036.png "Account Settings")</span><span class="sxs-lookup"><span data-stu-id="25f1f-168">![Account Settings](./media/new-relic-tutorial/ic797036.png "Account Settings")</span></span>

1. <span data-ttu-id="25f1f-169">Click the **Security and authentication** tab, and then click the **Single sign on** tab.</span><span class="sxs-lookup"><span data-stu-id="25f1f-169">Click the **Security and authentication** tab, and then click the **Single sign on** tab.</span></span>
   
    <span data-ttu-id="25f1f-170">![Single Sign-On](./media/new-relic-tutorial/ic797037.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="25f1f-170">![Single Sign-On](./media/new-relic-tutorial/ic797037.png "Single Sign-On")</span></span>

1. <span data-ttu-id="25f1f-171">On the SAML dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="25f1f-171">On the SAML dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="25f1f-172">![SAML](./media/new-relic-tutorial/ic797038.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="25f1f-172">![SAML](./media/new-relic-tutorial/ic797038.png "SAML")</span></span>
   
   <span data-ttu-id="25f1f-173">a.</span><span class="sxs-lookup"><span data-stu-id="25f1f-173">a.</span></span> <span data-ttu-id="25f1f-174">Click **Choose File** to upload your downloaded Azure Active Directory certificate.</span><span class="sxs-lookup"><span data-stu-id="25f1f-174">Click **Choose File** to upload your downloaded Azure Active Directory certificate.</span></span>

   <span data-ttu-id="25f1f-175">b.</span><span class="sxs-lookup"><span data-stu-id="25f1f-175">b.</span></span> <span data-ttu-id="25f1f-176">In the **Remote login URL** textbox,  paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="25f1f-176">In the **Remote login URL** textbox,  paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="25f1f-177">c.</span><span class="sxs-lookup"><span data-stu-id="25f1f-177">c.</span></span> <span data-ttu-id="25f1f-178">In the **Logout landing URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="25f1f-178">In the **Logout landing URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

   <span data-ttu-id="25f1f-179">d.</span><span class="sxs-lookup"><span data-stu-id="25f1f-179">d.</span></span> <span data-ttu-id="25f1f-180">Click **Save my changes**.</span><span class="sxs-lookup"><span data-stu-id="25f1f-180">Click **Save my changes**.</span></span>

> [!TIP]
> <span data-ttu-id="25f1f-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="25f1f-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="25f1f-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="25f1f-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="25f1f-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="25f1f-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="25f1f-184">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="25f1f-184">Create an Azure AD test user</span></span>

<span data-ttu-id="25f1f-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="25f1f-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="25f1f-187">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="25f1f-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="25f1f-188">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="25f1f-188">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/new-relic-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="25f1f-190">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="25f1f-190">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/new-relic-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="25f1f-192">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="25f1f-192">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/new-relic-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="25f1f-194">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="25f1f-194">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/new-relic-tutorial/create_aaduser_04.png)

    <span data-ttu-id="25f1f-196">a.</span><span class="sxs-lookup"><span data-stu-id="25f1f-196">a.</span></span> <span data-ttu-id="25f1f-197">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="25f1f-197">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="25f1f-198">b.</span><span class="sxs-lookup"><span data-stu-id="25f1f-198">b.</span></span> <span data-ttu-id="25f1f-199">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="25f1f-199">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="25f1f-200">c.</span><span class="sxs-lookup"><span data-stu-id="25f1f-200">c.</span></span> <span data-ttu-id="25f1f-201">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="25f1f-201">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="25f1f-202">d.</span><span class="sxs-lookup"><span data-stu-id="25f1f-202">d.</span></span> <span data-ttu-id="25f1f-203">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="25f1f-203">Click **Create**.</span></span>
 
### <a name="create-a-new-relic-test-user"></a><span data-ttu-id="25f1f-204">Create a New Relic test user</span><span class="sxs-lookup"><span data-stu-id="25f1f-204">Create a New Relic test user</span></span>

<span data-ttu-id="25f1f-205">In order to enable Azure Active Directory users to log in to New Relic, they must be provisioned into New Relic.</span><span class="sxs-lookup"><span data-stu-id="25f1f-205">In order to enable Azure Active Directory users to log in to New Relic, they must be provisioned into New Relic.</span></span> <span data-ttu-id="25f1f-206">In the case of New Relic, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="25f1f-206">In the case of New Relic, provisioning is a manual task.</span></span>

<span data-ttu-id="25f1f-207">**To provision a user account to New Relic, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="25f1f-207">**To provision a user account to New Relic, perform the following steps:**</span></span>

1. <span data-ttu-id="25f1f-208">Log in to your **New Relic** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="25f1f-208">Log in to your **New Relic** company site as administrator.</span></span>

1. <span data-ttu-id="25f1f-209">In the menu on the top, click **Account Settings**.</span><span class="sxs-lookup"><span data-stu-id="25f1f-209">In the menu on the top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="25f1f-210">![Account Settings](./media/new-relic-tutorial/ic797040.png "Account Settings")</span><span class="sxs-lookup"><span data-stu-id="25f1f-210">![Account Settings](./media/new-relic-tutorial/ic797040.png "Account Settings")</span></span>

1. <span data-ttu-id="25f1f-211">In the **Account** pane on the left side, click **Summary**, and then click **Add user**.</span><span class="sxs-lookup"><span data-stu-id="25f1f-211">In the **Account** pane on the left side, click **Summary**, and then click **Add user**.</span></span>
   
    <span data-ttu-id="25f1f-212">![Account Settings](./media/new-relic-tutorial/ic797041.png "Account Settings")</span><span class="sxs-lookup"><span data-stu-id="25f1f-212">![Account Settings](./media/new-relic-tutorial/ic797041.png "Account Settings")</span></span>

1. <span data-ttu-id="25f1f-213">On the **Active users** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="25f1f-213">On the **Active users** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="25f1f-214">![Active Users](./media/new-relic-tutorial/ic797042.png "Active Users")</span><span class="sxs-lookup"><span data-stu-id="25f1f-214">![Active Users](./media/new-relic-tutorial/ic797042.png "Active Users")</span></span>
   
    <span data-ttu-id="25f1f-215">a.</span><span class="sxs-lookup"><span data-stu-id="25f1f-215">a.</span></span> <span data-ttu-id="25f1f-216">In the **Email** textbox, type the email address of a valid Azure Active Directory user you want to provision.</span><span class="sxs-lookup"><span data-stu-id="25f1f-216">In the **Email** textbox, type the email address of a valid Azure Active Directory user you want to provision.</span></span>

    <span data-ttu-id="25f1f-217">b.</span><span class="sxs-lookup"><span data-stu-id="25f1f-217">b.</span></span> <span data-ttu-id="25f1f-218">As **Role** select **User**.</span><span class="sxs-lookup"><span data-stu-id="25f1f-218">As **Role** select **User**.</span></span>

    <span data-ttu-id="25f1f-219">c.</span><span class="sxs-lookup"><span data-stu-id="25f1f-219">c.</span></span> <span data-ttu-id="25f1f-220">Click **Add this user**.</span><span class="sxs-lookup"><span data-stu-id="25f1f-220">Click **Add this user**.</span></span>

>[!NOTE]
><span data-ttu-id="25f1f-221">You can use any other New Relic user account creation tools or APIs provided by New Relic to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="25f1f-221">You can use any other New Relic user account creation tools or APIs provided by New Relic to provision AAD user accounts.</span></span>
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="25f1f-222">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="25f1f-222">Assign the Azure AD test user</span></span>

<span data-ttu-id="25f1f-223">In this section, you enable Britta Simon to use Azure single sign-on by granting access to New Relic.</span><span class="sxs-lookup"><span data-stu-id="25f1f-223">In this section, you enable Britta Simon to use Azure single sign-on by granting access to New Relic.</span></span>

![Assign the user role][200] 

<span data-ttu-id="25f1f-225">**To assign Britta Simon to New Relic, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="25f1f-225">**To assign Britta Simon to New Relic, perform the following steps:**</span></span>

1. <span data-ttu-id="25f1f-226">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="25f1f-226">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="25f1f-228">In the applications list, select **New Relic**.</span><span class="sxs-lookup"><span data-stu-id="25f1f-228">In the applications list, select **New Relic**.</span></span>

    ![The New Relic link in the Applications list](./media/new-relic-tutorial/tutorial_new-relic_app.png)  

1. <span data-ttu-id="25f1f-230">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="25f1f-230">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="25f1f-232">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="25f1f-232">Click **Add** button.</span></span> <span data-ttu-id="25f1f-233">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="25f1f-233">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="25f1f-235">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="25f1f-235">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="25f1f-236">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="25f1f-236">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="25f1f-237">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="25f1f-237">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="25f1f-238">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="25f1f-238">Test single sign-on</span></span>

<span data-ttu-id="25f1f-239">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="25f1f-239">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="25f1f-240">When you click the New Relic tile in the Access Panel, you should get automatically signed-on to your New Relic application.</span><span class="sxs-lookup"><span data-stu-id="25f1f-240">When you click the New Relic tile in the Access Panel, you should get automatically signed-on to your New Relic application.</span></span>
<span data-ttu-id="25f1f-241">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="25f1f-241">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="25f1f-242">Additional resources</span><span class="sxs-lookup"><span data-stu-id="25f1f-242">Additional resources</span></span>

* [<span data-ttu-id="25f1f-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="25f1f-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="25f1f-244">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="25f1f-244">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/new-relic-tutorial/tutorial_general_01.png
[2]: ./media/new-relic-tutorial/tutorial_general_02.png
[3]: ./media/new-relic-tutorial/tutorial_general_03.png
[4]: ./media/new-relic-tutorial/tutorial_general_04.png

[100]: ./media/new-relic-tutorial/tutorial_general_100.png

[200]: ./media/new-relic-tutorial/tutorial_general_200.png
[201]: ./media/new-relic-tutorial/tutorial_general_201.png
[202]: ./media/new-relic-tutorial/tutorial_general_202.png
[203]: ./media/new-relic-tutorial/tutorial_general_203.png

