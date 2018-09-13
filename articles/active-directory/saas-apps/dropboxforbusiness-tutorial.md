---
title: 'Tutorial: Azure Active Directory integration with Dropbox for Business | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Dropbox for Business.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 63502412-758b-4b46-a580-0e8e130791a1
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/20/2018
ms.author: jeedes
ms.openlocfilehash: eadf6724891d348c2ea3654bcf19ef0d74078049
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867022"
---
# <a name="tutorial-azure-active-directory-integration-with-dropbox-for-business"></a><span data-ttu-id="5f189-103">Tutorial: Azure Active Directory integration with Dropbox for Business</span><span class="sxs-lookup"><span data-stu-id="5f189-103">Tutorial: Azure Active Directory integration with Dropbox for Business</span></span>

<span data-ttu-id="5f189-104">In this tutorial, you learn how to integrate Dropbox for Business with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5f189-104">In this tutorial, you learn how to integrate Dropbox for Business with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5f189-105">Integrating Dropbox for Business with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="5f189-105">Integrating Dropbox for Business with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5f189-106">You can control in Azure AD who has access to Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="5f189-106">You can control in Azure AD who has access to Dropbox for Business.</span></span>
- <span data-ttu-id="5f189-107">You can enable your users to automatically get signed-on to Dropbox for Business (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="5f189-107">You can enable your users to automatically get signed-on to Dropbox for Business (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="5f189-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="5f189-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="5f189-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="5f189-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5f189-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5f189-110">Prerequisites</span></span>

<span data-ttu-id="5f189-111">To configure Azure AD integration with Dropbox for Business, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="5f189-111">To configure Azure AD integration with Dropbox for Business, you need the following items:</span></span>

- <span data-ttu-id="5f189-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="5f189-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5f189-113">A Dropbox for Business single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="5f189-113">A Dropbox for Business single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5f189-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="5f189-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5f189-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="5f189-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5f189-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="5f189-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5f189-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5f189-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5f189-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="5f189-118">Scenario description</span></span>

<span data-ttu-id="5f189-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="5f189-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>
<span data-ttu-id="5f189-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="5f189-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5f189-121">Adding Dropbox for Business from the gallery</span><span class="sxs-lookup"><span data-stu-id="5f189-121">Adding Dropbox for Business from the gallery</span></span>
2. <span data-ttu-id="5f189-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="5f189-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-dropbox-for-business-from-the-gallery"></a><span data-ttu-id="5f189-123">Adding Dropbox for Business from the gallery</span><span class="sxs-lookup"><span data-stu-id="5f189-123">Adding Dropbox for Business from the gallery</span></span>

<span data-ttu-id="5f189-124">To configure the integration of Dropbox for Business into Azure AD, you need to add Dropbox for Business from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="5f189-124">To configure the integration of Dropbox for Business into Azure AD, you need to add Dropbox for Business from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5f189-125">**To add Dropbox for Business from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5f189-125">**To add Dropbox for Business from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5f189-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="5f189-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span>

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="5f189-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="5f189-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5f189-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="5f189-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]

3. <span data-ttu-id="5f189-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="5f189-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="5f189-133">In the search box, type **Dropbox for Business**, select **Dropbox for Business** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="5f189-133">In the search box, type **Dropbox for Business**, select **Dropbox for Business** from result panel then click **Add** button to add the application.</span></span>

    ![Dropbox for Business in the results list](./media/dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5f189-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="5f189-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="5f189-136">In this section, you configure and test Azure AD single sign-on with Dropbox for Business based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5f189-136">In this section, you configure and test Azure AD single sign-on with Dropbox for Business based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5f189-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Dropbox for Business is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5f189-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Dropbox for Business is to a user in Azure AD.</span></span> <span data-ttu-id="5f189-138">In other words, a link relationship between an Azure AD user and the related user in Dropbox for Business needs to be established.</span><span class="sxs-lookup"><span data-stu-id="5f189-138">In other words, a link relationship between an Azure AD user and the related user in Dropbox for Business needs to be established.</span></span>

<span data-ttu-id="5f189-139">In Dropbox for Business, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="5f189-139">In Dropbox for Business, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5f189-140">To configure and test Azure AD single sign-on with Dropbox for Business, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="5f189-140">To configure and test Azure AD single sign-on with Dropbox for Business, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5f189-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="5f189-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5f189-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5f189-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5f189-143">**[Create a Dropbox for Business test user](#create-a-dropbox-for-business-test-user)** - to have a counterpart of Britta Simon in Dropbox for Business that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="5f189-143">**[Create a Dropbox for Business test user](#create-a-dropbox-for-business-test-user)** - to have a counterpart of Britta Simon in Dropbox for Business that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5f189-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5f189-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5f189-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="5f189-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5f189-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="5f189-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="5f189-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Dropbox for Business application.</span><span class="sxs-lookup"><span data-stu-id="5f189-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Dropbox for Business application.</span></span>

<span data-ttu-id="5f189-148">**To configure Azure AD single sign-on with Dropbox for Business, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5f189-148">**To configure Azure AD single sign-on with Dropbox for Business, perform the following steps:**</span></span>

1. <span data-ttu-id="5f189-149">In the Azure portal, on the **Dropbox for Business** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="5f189-149">In the Azure portal, on the **Dropbox for Business** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="5f189-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5f189-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_samlbase.png)

3. <span data-ttu-id="5f189-153">On the **Dropbox for Business Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5f189-153">On the **Dropbox for Business Domain and URLs** section, perform the following steps:</span></span>

    ![Dropbox for Business Domain and URLs single sign-on information](./media/dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_url1.png)

    <span data-ttu-id="5f189-155">a.</span><span class="sxs-lookup"><span data-stu-id="5f189-155">a.</span></span> <span data-ttu-id="5f189-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.dropbox.com/sso/<id>`</span><span class="sxs-lookup"><span data-stu-id="5f189-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.dropbox.com/sso/<id>`</span></span>

    <span data-ttu-id="5f189-157">b.</span><span class="sxs-lookup"><span data-stu-id="5f189-157">b.</span></span> <span data-ttu-id="5f189-158">In the **Identifier** textbox, type a value: `Dropbox`</span><span class="sxs-lookup"><span data-stu-id="5f189-158">In the **Identifier** textbox, type a value: `Dropbox`</span></span>

    > [!NOTE]
    > <span data-ttu-id="5f189-159">The preceding Sign-on URL value is not real value.</span><span class="sxs-lookup"><span data-stu-id="5f189-159">The preceding Sign-on URL value is not real value.</span></span> <span data-ttu-id="5f189-160">You will update the value with the actual Sign-on URL, which is explained later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="5f189-160">You will update the value with the actual Sign-on URL, which is explained later in the tutorial.</span></span>

4. <span data-ttu-id="5f189-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="5f189-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_certificate.png) 

5. <span data-ttu-id="5f189-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="5f189-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/dropboxforbusiness-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5f189-165">On the **Dropbox for Business Configuration** section, click **Configure Dropbox for Business** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="5f189-165">On the **Dropbox for Business Configuration** section, click **Configure Dropbox for Business** to open **Configure sign-on** window.</span></span> <span data-ttu-id="5f189-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="5f189-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Dropbox for Business Configuration](./media/dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_configure.png) 

7. <span data-ttu-id="5f189-168">To configure single sign-on on **Dropbox for Business** side, Go on your Dropbox for Business tenant and sign on to your Dropbox for business tenant.</span><span class="sxs-lookup"><span data-stu-id="5f189-168">To configure single sign-on on **Dropbox for Business** side, Go on your Dropbox for Business tenant and sign on to your Dropbox for business tenant.</span></span>

    <span data-ttu-id="5f189-169">![Configure single sign-on](./media/dropboxforbusiness-tutorial/ic769509.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="5f189-169">![Configure single sign-on](./media/dropboxforbusiness-tutorial/ic769509.png "Configure single sign-on")</span></span>

8. <span data-ttu-id="5f189-170">Click on the **User Icon** and select **Settings** tab.</span><span class="sxs-lookup"><span data-stu-id="5f189-170">Click on the **User Icon** and select **Settings** tab.</span></span>

    <span data-ttu-id="5f189-171">![Configure single sign-on](./media/dropboxforbusiness-tutorial/configure1.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="5f189-171">![Configure single sign-on](./media/dropboxforbusiness-tutorial/configure1.png "Configure single sign-on")</span></span>

9. <span data-ttu-id="5f189-172">In the navigation pane on the left side, click **Admin console**.</span><span class="sxs-lookup"><span data-stu-id="5f189-172">In the navigation pane on the left side, click **Admin console**.</span></span>

    <span data-ttu-id="5f189-173">![Configure single sign-on](./media/dropboxforbusiness-tutorial/configure2.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="5f189-173">![Configure single sign-on](./media/dropboxforbusiness-tutorial/configure2.png "Configure single sign-on")</span></span>

10. <span data-ttu-id="5f189-174">On the **Admin console**, click **Settings** in the left navigation pane.</span><span class="sxs-lookup"><span data-stu-id="5f189-174">On the **Admin console**, click **Settings** in the left navigation pane.</span></span>

    <span data-ttu-id="5f189-175">![Configure single sign-on](./media/dropboxforbusiness-tutorial/configure3.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="5f189-175">![Configure single sign-on](./media/dropboxforbusiness-tutorial/configure3.png "Configure single sign-on")</span></span>

11. <span data-ttu-id="5f189-176">Select **Single sign-on** option under the **Authentication** section.</span><span class="sxs-lookup"><span data-stu-id="5f189-176">Select **Single sign-on** option under the **Authentication** section.</span></span>

    <span data-ttu-id="5f189-177">![Configure single sign-on](./media/dropboxforbusiness-tutorial/configure4.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="5f189-177">![Configure single sign-on](./media/dropboxforbusiness-tutorial/configure4.png "Configure single sign-on")</span></span>

12. <span data-ttu-id="5f189-178">In the **Single sign-on** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5f189-178">In the **Single sign-on** section, perform the following steps:</span></span>  

    <span data-ttu-id="5f189-179">![Configure single sign-on](./media/dropboxforbusiness-tutorial/configure5.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="5f189-179">![Configure single sign-on](./media/dropboxforbusiness-tutorial/configure5.png "Configure single sign-on")</span></span>

    <span data-ttu-id="5f189-180">a.</span><span class="sxs-lookup"><span data-stu-id="5f189-180">a.</span></span> <span data-ttu-id="5f189-181">Select **Required** as a option from the dropdown for the **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="5f189-181">Select **Required** as a option from the dropdown for the **Single sign-on**.</span></span>

    <span data-ttu-id="5f189-182">b.</span><span class="sxs-lookup"><span data-stu-id="5f189-182">b.</span></span> <span data-ttu-id="5f189-183">Click on **Add sign-in URL** and in the **Identity provider sign-in URL** textbox, paste the **SAML Single Sign-On Service URL** value which you have copied from the Azure portal and then select **Done**.</span><span class="sxs-lookup"><span data-stu-id="5f189-183">Click on **Add sign-in URL** and in the **Identity provider sign-in URL** textbox, paste the **SAML Single Sign-On Service URL** value which you have copied from the Azure portal and then select **Done**.</span></span>

    <span data-ttu-id="5f189-184">![Configure single sign-on](./media/dropboxforbusiness-tutorial/configure6.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="5f189-184">![Configure single sign-on](./media/dropboxforbusiness-tutorial/configure6.png "Configure single sign-on")</span></span>

    <span data-ttu-id="5f189-185">c.</span><span class="sxs-lookup"><span data-stu-id="5f189-185">c.</span></span> <span data-ttu-id="5f189-186">Click **Upload certificate**, and then browse to your **Base64 encoded certificate file** which you have downloaded from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="5f189-186">Click **Upload certificate**, and then browse to your **Base64 encoded certificate file** which you have downloaded from the Azure portal.</span></span>

    <span data-ttu-id="5f189-187">d.</span><span class="sxs-lookup"><span data-stu-id="5f189-187">d.</span></span> <span data-ttu-id="5f189-188">Click on **Copy link** and paste the copied value into the **Sign-on URL** textbox of **Dropbox for Business Domain and URLs** section on Azure portal.</span><span class="sxs-lookup"><span data-stu-id="5f189-188">Click on **Copy link** and paste the copied value into the **Sign-on URL** textbox of **Dropbox for Business Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="5f189-189">e.</span><span class="sxs-lookup"><span data-stu-id="5f189-189">e.</span></span> <span data-ttu-id="5f189-190">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="5f189-190">Click **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5f189-191">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="5f189-191">Create an Azure AD test user</span></span>

<span data-ttu-id="5f189-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5f189-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="5f189-194">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5f189-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5f189-195">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="5f189-195">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/dropboxforbusiness-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="5f189-197">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="5f189-197">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/dropboxforbusiness-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="5f189-199">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="5f189-199">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/dropboxforbusiness-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="5f189-201">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5f189-201">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/dropboxforbusiness-tutorial/create_aaduser_04.png)

    <span data-ttu-id="5f189-203">a.</span><span class="sxs-lookup"><span data-stu-id="5f189-203">a.</span></span> <span data-ttu-id="5f189-204">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5f189-204">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5f189-205">b.</span><span class="sxs-lookup"><span data-stu-id="5f189-205">b.</span></span> <span data-ttu-id="5f189-206">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5f189-206">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="5f189-207">c.</span><span class="sxs-lookup"><span data-stu-id="5f189-207">c.</span></span> <span data-ttu-id="5f189-208">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="5f189-208">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="5f189-209">d.</span><span class="sxs-lookup"><span data-stu-id="5f189-209">d.</span></span> <span data-ttu-id="5f189-210">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="5f189-210">Click **Create**.</span></span>
 
### <a name="create-a-dropbox-for-business-test-user"></a><span data-ttu-id="5f189-211">Create a Dropbox for Business test user</span><span class="sxs-lookup"><span data-stu-id="5f189-211">Create a Dropbox for Business test user</span></span>

<span data-ttu-id="5f189-212">In this section, a user called Britta Simon is created in Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="5f189-212">In this section, a user called Britta Simon is created in Dropbox for Business.</span></span> <span data-ttu-id="5f189-213">Dropbox for Business supports just-in-time provisioning, which is enabled by default.</span><span class="sxs-lookup"><span data-stu-id="5f189-213">Dropbox for Business supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="5f189-214">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="5f189-214">There is no action item for you in this section.</span></span> <span data-ttu-id="5f189-215">If a user doesn't already exist in Dropbox for Business, a new one is created when you attempt to access Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="5f189-215">If a user doesn't already exist in Dropbox for Business, a new one is created when you attempt to access Dropbox for Business.</span></span>

>[!Note]
><span data-ttu-id="5f189-216">If you need to create a user manually, Contact [Dropbox for Business Client support team](https://www.dropbox.com/business/contact)</span><span class="sxs-lookup"><span data-stu-id="5f189-216">If you need to create a user manually, Contact [Dropbox for Business Client support team](https://www.dropbox.com/business/contact)</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="5f189-217">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="5f189-217">Assign the Azure AD test user</span></span>

<span data-ttu-id="5f189-218">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="5f189-218">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Dropbox for Business.</span></span>

![Assign the user role][200] 

<span data-ttu-id="5f189-220">**To assign Britta Simon to Dropbox for Business, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5f189-220">**To assign Britta Simon to Dropbox for Business, perform the following steps:**</span></span>

1. <span data-ttu-id="5f189-221">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="5f189-221">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="5f189-223">In the applications list, select **Dropbox for Business**.</span><span class="sxs-lookup"><span data-stu-id="5f189-223">In the applications list, select **Dropbox for Business**.</span></span>

    ![The Dropbox for Business link in the Applications list](./media/dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_app.png)  

1. <span data-ttu-id="5f189-225">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="5f189-225">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="5f189-227">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="5f189-227">Click **Add** button.</span></span> <span data-ttu-id="5f189-228">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="5f189-228">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="5f189-230">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="5f189-230">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="5f189-231">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="5f189-231">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="5f189-232">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="5f189-232">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="5f189-233">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="5f189-233">Test single sign-on</span></span>

<span data-ttu-id="5f189-234">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="5f189-234">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5f189-235">When you click the Dropbox for Business tile in the Access Panel, you should get login page of your Dropbox for Business application.</span><span class="sxs-lookup"><span data-stu-id="5f189-235">When you click the Dropbox for Business tile in the Access Panel, you should get login page of your Dropbox for Business application.</span></span>
 

## <a name="additional-resources"></a><span data-ttu-id="5f189-236">Additional resources</span><span class="sxs-lookup"><span data-stu-id="5f189-236">Additional resources</span></span>

* [<span data-ttu-id="5f189-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5f189-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="5f189-238">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5f189-238">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/dropboxforbusiness-tutorial/tutorial_general_01.png
[2]: ./media/dropboxforbusiness-tutorial/tutorial_general_02.png
[3]: ./media/dropboxforbusiness-tutorial/tutorial_general_03.png
[4]: ./media/dropboxforbusiness-tutorial/tutorial_general_04.png

[100]: ./media/dropboxforbusiness-tutorial/tutorial_general_100.png

[200]: ./media/dropboxforbusiness-tutorial/tutorial_general_200.png
[201]: ./media/dropboxforbusiness-tutorial/tutorial_general_201.png
[202]: ./media/dropboxforbusiness-tutorial/tutorial_general_202.png
[203]: ./media/dropboxforbusiness-tutorial/tutorial_general_203.png

