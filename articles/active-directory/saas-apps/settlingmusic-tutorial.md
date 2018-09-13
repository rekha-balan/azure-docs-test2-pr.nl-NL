---
title: 'Tutorial: Azure Active Directory integration with Settling music | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Settling music.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 6f86a8a2-4bd0-40cc-b1b4-752fce123328
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2018
ms.author: jeedes
ms.openlocfilehash: fda6ca2efb670c8087252428e417a3e0901fa748
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865064"
---
# <a name="tutorial-azure-active-directory-integration-with-settling-music"></a><span data-ttu-id="d3eb3-103">Tutorial: Azure Active Directory integration with Settling music</span><span class="sxs-lookup"><span data-stu-id="d3eb3-103">Tutorial: Azure Active Directory integration with Settling music</span></span>

<span data-ttu-id="d3eb3-104">In this tutorial, you learn how to integrate Settling music with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d3eb3-104">In this tutorial, you learn how to integrate Settling music with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d3eb3-105">Integrating Settling music with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="d3eb3-105">Integrating Settling music with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d3eb3-106">You can control in Azure AD who has access to Settling music.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-106">You can control in Azure AD who has access to Settling music.</span></span>
- <span data-ttu-id="d3eb3-107">You can enable your users to automatically get signed-on to Settling music (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-107">You can enable your users to automatically get signed-on to Settling music (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="d3eb3-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="d3eb3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="d3eb3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d3eb3-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d3eb3-110">Prerequisites</span></span>

<span data-ttu-id="d3eb3-111">To configure Azure AD integration with Settling music, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="d3eb3-111">To configure Azure AD integration with Settling music, you need the following items:</span></span>

- <span data-ttu-id="d3eb3-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="d3eb3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d3eb3-113">A Settling music single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="d3eb3-113">A Settling music single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d3eb3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d3eb3-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="d3eb3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d3eb3-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d3eb3-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d3eb3-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d3eb3-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="d3eb3-118">Scenario description</span></span>
<span data-ttu-id="d3eb3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d3eb3-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="d3eb3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d3eb3-121">Adding Settling music from the gallery</span><span class="sxs-lookup"><span data-stu-id="d3eb3-121">Adding Settling music from the gallery</span></span>
1. <span data-ttu-id="d3eb3-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d3eb3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-settling-music-from-the-gallery"></a><span data-ttu-id="d3eb3-123">Adding Settling music from the gallery</span><span class="sxs-lookup"><span data-stu-id="d3eb3-123">Adding Settling music from the gallery</span></span>
<span data-ttu-id="d3eb3-124">To configure the integration of Settling music into Azure AD, you need to add Settling music from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-124">To configure the integration of Settling music into Azure AD, you need to add Settling music from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d3eb3-125">**To add Settling music from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d3eb3-125">**To add Settling music from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d3eb3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="d3eb3-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d3eb3-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="d3eb3-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="d3eb3-133">In the search box, type **Settling music**, select **Settling music** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-133">In the search box, type **Settling music**, select **Settling music** from result panel then click **Add** button to add the application.</span></span>

    ![Settling music in the results list](./media/settlingmusic-tutorial/tutorial_settlingmusic_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d3eb3-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d3eb3-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="d3eb3-136">In this section, you configure and test Azure AD single sign-on with Settling music based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d3eb3-136">In this section, you configure and test Azure AD single sign-on with Settling music based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d3eb3-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Settling music is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Settling music is to a user in Azure AD.</span></span> <span data-ttu-id="d3eb3-138">In other words, a link relationship between an Azure AD user and the related user in Settling music needs to be established.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-138">In other words, a link relationship between an Azure AD user and the related user in Settling music needs to be established.</span></span>

<span data-ttu-id="d3eb3-139">To configure and test Azure AD single sign-on with Settling music, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="d3eb3-139">To configure and test Azure AD single sign-on with Settling music, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d3eb3-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="d3eb3-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="d3eb3-142">**[Create a Settling music test user](#create-a-settling-music-test-user)** - to have a counterpart of Britta Simon in Settling music that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-142">**[Create a Settling music test user](#create-a-settling-music-test-user)** - to have a counterpart of Britta Simon in Settling music that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="d3eb3-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="d3eb3-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d3eb3-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d3eb3-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="d3eb3-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Settling music application.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Settling music application.</span></span>

<span data-ttu-id="d3eb3-147">**To configure Azure AD single sign-on with Settling music, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d3eb3-147">**To configure Azure AD single sign-on with Settling music, perform the following steps:**</span></span>

1. <span data-ttu-id="d3eb3-148">In the Azure portal, on the **Settling music** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-148">In the Azure portal, on the **Settling music** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="d3eb3-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/settlingmusic-tutorial/tutorial_settlingmusic_samlbase.png)

1. <span data-ttu-id="d3eb3-152">On the **Settling music Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d3eb3-152">On the **Settling music Domain and URLs** section, perform the following steps:</span></span>

    ![Settling music Domain and URLs single sign-on information](./media/settlingmusic-tutorial/tutorial_settlingmusic_url.png)

    <span data-ttu-id="d3eb3-154">a.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-154">a.</span></span> <span data-ttu-id="d3eb3-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.rakurakuseisan.jp/<USERACCOUNT>/`</span><span class="sxs-lookup"><span data-stu-id="d3eb3-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.rakurakuseisan.jp/<USERACCOUNT>/`</span></span>

    <span data-ttu-id="d3eb3-156">b.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-156">b.</span></span> <span data-ttu-id="d3eb3-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.rakurakuseisan.jp/<USERACCOUNT>/`</span><span class="sxs-lookup"><span data-stu-id="d3eb3-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.rakurakuseisan.jp/<USERACCOUNT>/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d3eb3-158">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-158">These values are not real.</span></span> <span data-ttu-id="d3eb3-159">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-159">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d3eb3-160">Contact [Settling music Client support team](https://rakurakuseisan.jp/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-160">Contact [Settling music Client support team](https://rakurakuseisan.jp/) to get these values.</span></span> 
 
1. <span data-ttu-id="d3eb3-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/settlingmusic-tutorial/tutorial_settlingmusic_certificate.png) 

1. <span data-ttu-id="d3eb3-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/settlingmusic-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="d3eb3-165">On the **Settling music Configuration** section, click **Configure Settling music** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-165">On the **Settling music Configuration** section, click **Configure Settling music** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d3eb3-166">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="d3eb3-166">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Settling music Configuration](./media/settlingmusic-tutorial/tutorial_settlingmusic_configure.png) 

1. <span data-ttu-id="d3eb3-168">In a different web browser window, login to Settling music as a Security Administrator.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-168">In a different web browser window, login to Settling music as a Security Administrator.</span></span>

1. <span data-ttu-id="d3eb3-169">On top of the page, click **management** tab.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-169">On top of the page, click **management** tab.</span></span>

    ![Settling music step1](./media/settlingmusic-tutorial/tutorial_settlingmusic_step1.png)

1. <span data-ttu-id="d3eb3-171">Click on  **System setting** tab.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-171">Click on  **System setting** tab.</span></span>

    ![Settling music step2](./media/settlingmusic-tutorial/tutorial_settlingmusic_step2.png)

1. <span data-ttu-id="d3eb3-173">Switch to **Security** tab.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-173">Switch to **Security** tab.</span></span>

    ![Settling music step3](./media/settlingmusic-tutorial/tutorial_settlingmusic_step3.png)

1. <span data-ttu-id="d3eb3-175">On the **Single sign-on setting** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d3eb3-175">On the **Single sign-on setting** section, perform the following steps:</span></span>

    ![Settling music step5](./media/settlingmusic-tutorial/tutorial_settlingmusic_step4.png)

    <span data-ttu-id="d3eb3-177">a.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-177">a.</span></span> <span data-ttu-id="d3eb3-178">Click **To enable**.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-178">Click **To enable**.</span></span>

    <span data-ttu-id="d3eb3-179">b.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-179">b.</span></span> <span data-ttu-id="d3eb3-180">In the **Login URL of the ID provider** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-180">In the **Login URL of the ID provider** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="d3eb3-181">c.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-181">c.</span></span> <span data-ttu-id="d3eb3-182">In the **ID provider logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-182">In the **ID provider logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="d3eb3-183">d.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-183">d.</span></span> <span data-ttu-id="d3eb3-184">Click **Choose File** to upload the **Certificate (Base64)** which you have downloaded form Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-184">Click **Choose File** to upload the **Certificate (Base64)** which you have downloaded form Azure portal.</span></span>

    <span data-ttu-id="d3eb3-185">e.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-185">e.</span></span> <span data-ttu-id="d3eb3-186">Click the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-186">Click the **Save** button.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d3eb3-187">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d3eb3-187">Create an Azure AD test user</span></span>

<span data-ttu-id="d3eb3-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="d3eb3-190">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d3eb3-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d3eb3-191">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-191">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/settlingmusic-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="d3eb3-193">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-193">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/settlingmusic-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="d3eb3-195">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-195">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/settlingmusic-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="d3eb3-197">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d3eb3-197">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/settlingmusic-tutorial/create_aaduser_04.png)

    <span data-ttu-id="d3eb3-199">a.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-199">a.</span></span> <span data-ttu-id="d3eb3-200">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-200">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d3eb3-201">b.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-201">b.</span></span> <span data-ttu-id="d3eb3-202">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-202">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="d3eb3-203">c.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-203">c.</span></span> <span data-ttu-id="d3eb3-204">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-204">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="d3eb3-205">d.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-205">d.</span></span> <span data-ttu-id="d3eb3-206">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-206">Click **Create**.</span></span>
 
### <a name="create-a-settling-music-test-user"></a><span data-ttu-id="d3eb3-207">Create a Settling music test user</span><span class="sxs-lookup"><span data-stu-id="d3eb3-207">Create a Settling music test user</span></span>

<span data-ttu-id="d3eb3-208">In this section, you create a user called Britta Simon in Settling music.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-208">In this section, you create a user called Britta Simon in Settling music.</span></span> <span data-ttu-id="d3eb3-209">Work with [Settling music Client support team](https://rakurakuseisan.jp/) to add the users in the Settling music platform.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-209">Work with [Settling music Client support team](https://rakurakuseisan.jp/) to add the users in the Settling music platform.</span></span> <span data-ttu-id="d3eb3-210">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-210">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="d3eb3-211">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d3eb3-211">Assign the Azure AD test user</span></span>

<span data-ttu-id="d3eb3-212">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Settling music.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-212">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Settling music.</span></span>

![Assign the user role][200] 

<span data-ttu-id="d3eb3-214">**To assign Britta Simon to Settling music, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d3eb3-214">**To assign Britta Simon to Settling music, perform the following steps:**</span></span>

1. <span data-ttu-id="d3eb3-215">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-215">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="d3eb3-217">In the applications list, select **Settling music**.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-217">In the applications list, select **Settling music**.</span></span>

    ![The Settling music link in the Applications list](./media/settlingmusic-tutorial/tutorial_settlingmusic_app.png)  

1. <span data-ttu-id="d3eb3-219">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-219">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="d3eb3-221">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-221">Click **Add** button.</span></span> <span data-ttu-id="d3eb3-222">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="d3eb3-224">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-224">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="d3eb3-225">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-225">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="d3eb3-226">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="d3eb3-227">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="d3eb3-227">Test single sign-on</span></span>

<span data-ttu-id="d3eb3-228">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-228">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d3eb3-229">When you click the Settling music tile in the Access Panel, you should get automatically signed-on to your Settling music application.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-229">When you click the Settling music tile in the Access Panel, you should get automatically signed-on to your Settling music application.</span></span>
<span data-ttu-id="d3eb3-230">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d3eb3-230">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d3eb3-231">Additional resources</span><span class="sxs-lookup"><span data-stu-id="d3eb3-231">Additional resources</span></span>

* [<span data-ttu-id="d3eb3-232">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d3eb3-232">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="d3eb3-233">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d3eb3-233">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/settlingmusic-tutorial/tutorial_general_01.png
[2]: ./media/settlingmusic-tutorial/tutorial_general_02.png
[3]: ./media/settlingmusic-tutorial/tutorial_general_03.png
[4]: ./media/settlingmusic-tutorial/tutorial_general_04.png

[100]: ./media/settlingmusic-tutorial/tutorial_general_100.png

[200]: ./media/settlingmusic-tutorial/tutorial_general_200.png
[201]: ./media/settlingmusic-tutorial/tutorial_general_201.png
[202]: ./media/settlingmusic-tutorial/tutorial_general_202.png
[203]: ./media/settlingmusic-tutorial/tutorial_general_203.png

