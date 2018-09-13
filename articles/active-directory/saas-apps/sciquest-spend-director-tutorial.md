---
title: 'Tutorial: Azure Active Directory integration with SciQuest Spend Director | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SciQuest Spend Director.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 9fab641b-292e-4bef-91d1-8ccc4f3a0c1f
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/12/2017
ms.author: jeedes
ms.openlocfilehash: 0ddc8a42f4e0454061fa645b8c5d465e9e8dd9bf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864639"
---
# <a name="tutorial-azure-active-directory-integration-with-sciquest-spend-director"></a><span data-ttu-id="e1ad2-103">Tutorial: Azure Active Directory integration with SciQuest Spend Director</span><span class="sxs-lookup"><span data-stu-id="e1ad2-103">Tutorial: Azure Active Directory integration with SciQuest Spend Director</span></span>

<span data-ttu-id="e1ad2-104">In this tutorial, you learn how to integrate SciQuest Spend Director with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e1ad2-104">In this tutorial, you learn how to integrate SciQuest Spend Director with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e1ad2-105">Integrating SciQuest Spend Director with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="e1ad2-105">Integrating SciQuest Spend Director with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e1ad2-106">You can control in Azure AD who has access to SciQuest Spend Director.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-106">You can control in Azure AD who has access to SciQuest Spend Director.</span></span>
- <span data-ttu-id="e1ad2-107">You can enable your users to automatically get signed-on to SciQuest Spend Director (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-107">You can enable your users to automatically get signed-on to SciQuest Spend Director (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="e1ad2-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="e1ad2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="e1ad2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1ad2-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e1ad2-110">Prerequisites</span></span>

<span data-ttu-id="e1ad2-111">To configure Azure AD integration with SciQuest Spend Director, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="e1ad2-111">To configure Azure AD integration with SciQuest Spend Director, you need the following items:</span></span>

- <span data-ttu-id="e1ad2-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="e1ad2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e1ad2-113">A SciQuest Spend Director single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="e1ad2-113">A SciQuest Spend Director single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e1ad2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e1ad2-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="e1ad2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e1ad2-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e1ad2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e1ad2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e1ad2-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="e1ad2-118">Scenario description</span></span>
<span data-ttu-id="e1ad2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e1ad2-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="e1ad2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e1ad2-121">Adding SciQuest Spend Director from the gallery</span><span class="sxs-lookup"><span data-stu-id="e1ad2-121">Adding SciQuest Spend Director from the gallery</span></span>
1. <span data-ttu-id="e1ad2-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e1ad2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sciquest-spend-director-from-the-gallery"></a><span data-ttu-id="e1ad2-123">Adding SciQuest Spend Director from the gallery</span><span class="sxs-lookup"><span data-stu-id="e1ad2-123">Adding SciQuest Spend Director from the gallery</span></span>
<span data-ttu-id="e1ad2-124">To configure the integration of SciQuest Spend Director into Azure AD, you need to add SciQuest Spend Director from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-124">To configure the integration of SciQuest Spend Director into Azure AD, you need to add SciQuest Spend Director from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e1ad2-125">**To add SciQuest Spend Director from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e1ad2-125">**To add SciQuest Spend Director from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e1ad2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="e1ad2-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e1ad2-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="e1ad2-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="e1ad2-133">In the search box, type **SciQuest Spend Director**, select **SciQuest Spend Director** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-133">In the search box, type **SciQuest Spend Director**, select **SciQuest Spend Director** from result panel then click **Add** button to add the application.</span></span>

    ![SciQuest Spend Director in the results list](./media/sciquest-spend-director-tutorial/tutorial_sciquestspenddirector_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e1ad2-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e1ad2-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="e1ad2-136">In this section, you configure and test Azure AD single sign-on with SciQuest Spend Director based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e1ad2-136">In this section, you configure and test Azure AD single sign-on with SciQuest Spend Director based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e1ad2-137">For single sign-on to work, Azure AD needs to know what the counterpart user in SciQuest Spend Director is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-137">For single sign-on to work, Azure AD needs to know what the counterpart user in SciQuest Spend Director is to a user in Azure AD.</span></span> <span data-ttu-id="e1ad2-138">In other words, a link relationship between an Azure AD user and the related user in SciQuest Spend Director needs to be established.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-138">In other words, a link relationship between an Azure AD user and the related user in SciQuest Spend Director needs to be established.</span></span>

<span data-ttu-id="e1ad2-139">In SciQuest Spend Director, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-139">In SciQuest Spend Director, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e1ad2-140">To configure and test Azure AD single sign-on with SciQuest Spend Director, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="e1ad2-140">To configure and test Azure AD single sign-on with SciQuest Spend Director, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e1ad2-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="e1ad2-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="e1ad2-143">**[Create a SciQuest Spend Director test user](#create-a-sciquest-spend-director-test-user)** - to have a counterpart of Britta Simon in SciQuest Spend Director that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-143">**[Create a SciQuest Spend Director test user](#create-a-sciquest-spend-director-test-user)** - to have a counterpart of Britta Simon in SciQuest Spend Director that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="e1ad2-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="e1ad2-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e1ad2-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e1ad2-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e1ad2-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SciQuest Spend Director application.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SciQuest Spend Director application.</span></span>

<span data-ttu-id="e1ad2-148">**To configure Azure AD single sign-on with SciQuest Spend Director, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e1ad2-148">**To configure Azure AD single sign-on with SciQuest Spend Director, perform the following steps:**</span></span>

1. <span data-ttu-id="e1ad2-149">In the Azure portal, on the **SciQuest Spend Director** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-149">In the Azure portal, on the **SciQuest Spend Director** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="e1ad2-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/sciquest-spend-director-tutorial/tutorial_sciquestspenddirector_samlbase.png)

1. <span data-ttu-id="e1ad2-153">On the **SciQuest Spend Director Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e1ad2-153">On the **SciQuest Spend Director Domain and URLs** section, perform the following steps:</span></span>

    ![SciQuest Spend Director Domain and URLs single sign-on information](./media/sciquest-spend-director-tutorial/tutorial_sciquestspenddirector_url.png)

    <span data-ttu-id="e1ad2-155">a.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-155">a.</span></span> <span data-ttu-id="e1ad2-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.sciquest.com/apps/Router/SAMLAuth/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="e1ad2-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.sciquest.com/apps/Router/SAMLAuth/<instancename>`</span></span>

    <span data-ttu-id="e1ad2-157">b.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-157">b.</span></span> <span data-ttu-id="e1ad2-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.sciquest.com`</span><span class="sxs-lookup"><span data-stu-id="e1ad2-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.sciquest.com`</span></span>

    <span data-ttu-id="e1ad2-159">c.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-159">c.</span></span> <span data-ttu-id="e1ad2-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.sciquest.com/apps/Router/ExternalAuth/Login/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="e1ad2-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.sciquest.com/apps/Router/ExternalAuth/Login/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e1ad2-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-161">These values are not real.</span></span> <span data-ttu-id="e1ad2-162">Update these values with the actual Sign-On URL, Identifier, and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-162">Update these values with the actual Sign-On URL, Identifier, and Reply URL.</span></span> <span data-ttu-id="e1ad2-163">Contact [SciQuest Spend Director Client support team](https://www.jaggaer.com/contact-us/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-163">Contact [SciQuest Spend Director Client support team](https://www.jaggaer.com/contact-us/) to get these values.</span></span> 

1. <span data-ttu-id="e1ad2-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/sciquest-spend-director-tutorial/tutorial_sciquestspenddirector_certificate.png) 

1. <span data-ttu-id="e1ad2-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/sciquest-spend-director-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="e1ad2-168">To configure single sign-on on **SciQuest Spend Director** side, you need to send the downloaded **Metadata XML** to [SciQuest Spend Director support team](https://www.jaggaer.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="e1ad2-168">To configure single sign-on on **SciQuest Spend Director** side, you need to send the downloaded **Metadata XML** to [SciQuest Spend Director support team](https://www.jaggaer.com/contact-us/).</span></span>

> [!TIP]
> <span data-ttu-id="e1ad2-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="e1ad2-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e1ad2-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e1ad2-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e1ad2-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e1ad2-172">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e1ad2-172">Create an Azure AD test user</span></span>

<span data-ttu-id="e1ad2-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="e1ad2-175">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e1ad2-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e1ad2-176">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-176">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/sciquest-spend-director-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="e1ad2-178">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-178">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/sciquest-spend-director-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="e1ad2-180">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-180">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/sciquest-spend-director-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="e1ad2-182">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e1ad2-182">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/sciquest-spend-director-tutorial/create_aaduser_04.png)

    <span data-ttu-id="e1ad2-184">a.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-184">a.</span></span> <span data-ttu-id="e1ad2-185">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-185">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e1ad2-186">b.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-186">b.</span></span> <span data-ttu-id="e1ad2-187">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-187">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="e1ad2-188">c.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-188">c.</span></span> <span data-ttu-id="e1ad2-189">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-189">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="e1ad2-190">d.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-190">d.</span></span> <span data-ttu-id="e1ad2-191">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-191">Click **Create**.</span></span>
 
### <a name="create-a-sciquest-spend-director-test-user"></a><span data-ttu-id="e1ad2-192">Create a SciQuest Spend Director test user</span><span class="sxs-lookup"><span data-stu-id="e1ad2-192">Create a SciQuest Spend Director test user</span></span>

<span data-ttu-id="e1ad2-193">The objective of this section is to create a user called Britta Simon in SciQuest Spend Director.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-193">The objective of this section is to create a user called Britta Simon in SciQuest Spend Director.</span></span>

<span data-ttu-id="e1ad2-194">You need to contact your [SciQuest Spend Director support team](https://www.jaggaer.com/contact-us/) and provide them with the details about your test account to get it created.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-194">You need to contact your [SciQuest Spend Director support team](https://www.jaggaer.com/contact-us/) and provide them with the details about your test account to get it created.</span></span>

<span data-ttu-id="e1ad2-195">Alternatively, you can also leverage just-in-time provisioning, a single sign-on feature that is supported by SciQuest Spend Director.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-195">Alternatively, you can also leverage just-in-time provisioning, a single sign-on feature that is supported by SciQuest Spend Director.</span></span>  
<span data-ttu-id="e1ad2-196">If just-in-time provisioning is enabled, users are automatically created by SciQuest Spend Director during a single sign-on attempt if they don't exist.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-196">If just-in-time provisioning is enabled, users are automatically created by SciQuest Spend Director during a single sign-on attempt if they don't exist.</span></span> <span data-ttu-id="e1ad2-197">This feature eliminates the need to manually create single sign-on counterpart users.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-197">This feature eliminates the need to manually create single sign-on counterpart users.</span></span>

<span data-ttu-id="e1ad2-198">To get just-in-time provisioning enabled, you need to contact your [SciQuest Spend Director support team](https://www.jaggaer.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="e1ad2-198">To get just-in-time provisioning enabled, you need to contact your [SciQuest Spend Director support team](https://www.jaggaer.com/contact-us/).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="e1ad2-199">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e1ad2-199">Assign the Azure AD test user</span></span>

<span data-ttu-id="e1ad2-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SciQuest Spend Director.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SciQuest Spend Director.</span></span>

![Assign the user role][200] 

<span data-ttu-id="e1ad2-202">**To assign Britta Simon to SciQuest Spend Director, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e1ad2-202">**To assign Britta Simon to SciQuest Spend Director, perform the following steps:**</span></span>

1. <span data-ttu-id="e1ad2-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="e1ad2-205">In the applications list, select **SciQuest Spend Director**.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-205">In the applications list, select **SciQuest Spend Director**.</span></span>

    ![The SciQuest Spend Director link in the Applications list](./media/sciquest-spend-director-tutorial/tutorial_sciquestspenddirector_app.png)  

1. <span data-ttu-id="e1ad2-207">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-207">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="e1ad2-209">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-209">Click **Add** button.</span></span> <span data-ttu-id="e1ad2-210">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="e1ad2-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="e1ad2-213">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-213">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="e1ad2-214">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e1ad2-215">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="e1ad2-215">Test single sign-on</span></span>

<span data-ttu-id="e1ad2-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e1ad2-217">When you click the SciQuest Spend Director tile in the Access Panel, you should get automatically signed-on to your SciQuest Spend Director application.</span><span class="sxs-lookup"><span data-stu-id="e1ad2-217">When you click the SciQuest Spend Director tile in the Access Panel, you should get automatically signed-on to your SciQuest Spend Director application.</span></span>
<span data-ttu-id="e1ad2-218">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e1ad2-218">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e1ad2-219">Additional resources</span><span class="sxs-lookup"><span data-stu-id="e1ad2-219">Additional resources</span></span>

* [<span data-ttu-id="e1ad2-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e1ad2-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="e1ad2-221">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e1ad2-221">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/sciquest-spend-director-tutorial/tutorial_general_01.png
[2]: ./media/sciquest-spend-director-tutorial/tutorial_general_02.png
[3]: ./media/sciquest-spend-director-tutorial/tutorial_general_03.png
[4]: ./media/sciquest-spend-director-tutorial/tutorial_general_04.png

[100]: ./media/sciquest-spend-director-tutorial/tutorial_general_100.png

[200]: ./media/sciquest-spend-director-tutorial/tutorial_general_200.png
[201]: ./media/sciquest-spend-director-tutorial/tutorial_general_201.png
[202]: ./media/sciquest-spend-director-tutorial/tutorial_general_202.png
[203]: ./media/sciquest-spend-director-tutorial/tutorial_general_203.png

