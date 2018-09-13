---
title: 'Tutorial: Azure Active Directory integration with SmartLPA | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SmartLPA.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ed5f6580-bee6-4f44-aceb-f8f7feda3fb8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2018
ms.author: jeedes
ms.openlocfilehash: eedec7de74f3bdd7ae43d1b1eb0decd5fe83ebf6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969154"
---
# <a name="tutorial-azure-active-directory-integration-with-smartlpa"></a><span data-ttu-id="9d8a5-103">Tutorial: Azure Active Directory integration with SmartLPA</span><span class="sxs-lookup"><span data-stu-id="9d8a5-103">Tutorial: Azure Active Directory integration with SmartLPA</span></span>

<span data-ttu-id="9d8a5-104">In this tutorial, you learn how to integrate SmartLPA with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9d8a5-104">In this tutorial, you learn how to integrate SmartLPA with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9d8a5-105">Integrating SmartLPA with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="9d8a5-105">Integrating SmartLPA with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9d8a5-106">You can control in Azure AD who has access to SmartLPA.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-106">You can control in Azure AD who has access to SmartLPA.</span></span>
- <span data-ttu-id="9d8a5-107">You can enable your users to automatically get signed-on to SmartLPA (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-107">You can enable your users to automatically get signed-on to SmartLPA (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="9d8a5-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="9d8a5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="9d8a5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d8a5-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9d8a5-110">Prerequisites</span></span>

<span data-ttu-id="9d8a5-111">To configure Azure AD integration with SmartLPA, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="9d8a5-111">To configure Azure AD integration with SmartLPA, you need the following items:</span></span>

- <span data-ttu-id="9d8a5-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="9d8a5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9d8a5-113">A SmartLPA single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="9d8a5-113">A SmartLPA single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9d8a5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9d8a5-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="9d8a5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9d8a5-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9d8a5-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9d8a5-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9d8a5-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="9d8a5-118">Scenario description</span></span>
<span data-ttu-id="9d8a5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9d8a5-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="9d8a5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9d8a5-121">Adding SmartLPA from the gallery</span><span class="sxs-lookup"><span data-stu-id="9d8a5-121">Adding SmartLPA from the gallery</span></span>
2. <span data-ttu-id="9d8a5-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9d8a5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-smartlpa-from-the-gallery"></a><span data-ttu-id="9d8a5-123">Adding SmartLPA from the gallery</span><span class="sxs-lookup"><span data-stu-id="9d8a5-123">Adding SmartLPA from the gallery</span></span>
<span data-ttu-id="9d8a5-124">To configure the integration of SmartLPA into Azure AD, you need to add SmartLPA from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-124">To configure the integration of SmartLPA into Azure AD, you need to add SmartLPA from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9d8a5-125">**To add SmartLPA from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9d8a5-125">**To add SmartLPA from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9d8a5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="9d8a5-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9d8a5-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="9d8a5-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="9d8a5-133">In the search box, type **SmartLPA**, select **SmartLPA** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-133">In the search box, type **SmartLPA**, select **SmartLPA** from result panel then click **Add** button to add the application.</span></span>

    ![SmartLPA in the results list](./media/smartlpa-tutorial/tutorial_smartlpa_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9d8a5-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9d8a5-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="9d8a5-136">In this section, you configure and test Azure AD single sign-on with SmartLPA based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9d8a5-136">In this section, you configure and test Azure AD single sign-on with SmartLPA based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9d8a5-137">For single sign-on to work, Azure AD needs to know what the counterpart user in SmartLPA is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-137">For single sign-on to work, Azure AD needs to know what the counterpart user in SmartLPA is to a user in Azure AD.</span></span> <span data-ttu-id="9d8a5-138">In other words, a link relationship between an Azure AD user and the related user in SmartLPA needs to be established.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-138">In other words, a link relationship between an Azure AD user and the related user in SmartLPA needs to be established.</span></span>

<span data-ttu-id="9d8a5-139">To configure and test Azure AD single sign-on with SmartLPA, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="9d8a5-139">To configure and test Azure AD single sign-on with SmartLPA, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9d8a5-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9d8a5-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9d8a5-142">**[Create a SmartLPA test user](#create-a-smartlpa-test-user)** - to have a counterpart of Britta Simon in SmartLPA that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-142">**[Create a SmartLPA test user](#create-a-smartlpa-test-user)** - to have a counterpart of Britta Simon in SmartLPA that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9d8a5-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9d8a5-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9d8a5-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9d8a5-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="9d8a5-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SmartLPA application.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SmartLPA application.</span></span>

<span data-ttu-id="9d8a5-147">**To configure Azure AD single sign-on with SmartLPA, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9d8a5-147">**To configure Azure AD single sign-on with SmartLPA, perform the following steps:**</span></span>

1. <span data-ttu-id="9d8a5-148">In the Azure portal, on the **SmartLPA** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-148">In the Azure portal, on the **SmartLPA** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="9d8a5-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/smartlpa-tutorial/tutorial_smartlpa_samlbase.png)

3. <span data-ttu-id="9d8a5-152">On the **SmartLPA Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9d8a5-152">On the **SmartLPA Domain and URLs** section, perform the following steps:</span></span>

    ![SmartLPA Domain and URLs single sign-on information](./media/smartlpa-tutorial/tutorial_smartlpa_url.png)

    <span data-ttu-id="9d8a5-154">a.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-154">a.</span></span> <span data-ttu-id="9d8a5-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<TENANTNAME>.smartlpa.com/`</span><span class="sxs-lookup"><span data-stu-id="9d8a5-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<TENANTNAME>.smartlpa.com/`</span></span>

    <span data-ttu-id="9d8a5-156">b.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-156">b.</span></span> <span data-ttu-id="9d8a5-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<TENANTNAME>.smartlpa.com/<UNIQUE ID>`</span><span class="sxs-lookup"><span data-stu-id="9d8a5-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<TENANTNAME>.smartlpa.com/<UNIQUE ID>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9d8a5-158">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-158">These values are not real.</span></span> <span data-ttu-id="9d8a5-159">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-159">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="9d8a5-160">Contact [SmartLPA Client support team](mailto:support@smartlpa.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-160">Contact [SmartLPA Client support team](mailto:support@smartlpa.com) to get these values.</span></span>

4. <span data-ttu-id="9d8a5-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/smartlpa-tutorial/tutorial_smartlpa_certificate.png) 

5. <span data-ttu-id="9d8a5-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/smartlpa-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9d8a5-165">On the **SmartLPA Configuration** section, click **Configure SmartLPA** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-165">On the **SmartLPA Configuration** section, click **Configure SmartLPA** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9d8a5-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="9d8a5-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![SmartLPA Configuration](./media/smartlpa-tutorial/tutorial_smartlpa_configure.png) 

7. <span data-ttu-id="9d8a5-168">To configure single sign-on on **SmartLPA** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL**  to [SmartLPA support team](mailto:support@smartlpa.com).</span><span class="sxs-lookup"><span data-stu-id="9d8a5-168">To configure single sign-on on **SmartLPA** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL**  to [SmartLPA support team](mailto:support@smartlpa.com).</span></span> <span data-ttu-id="9d8a5-169">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9d8a5-170">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="9d8a5-170">Create an Azure AD test user</span></span>

<span data-ttu-id="9d8a5-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="9d8a5-173">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9d8a5-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9d8a5-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/smartlpa-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="9d8a5-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/smartlpa-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="9d8a5-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/smartlpa-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="9d8a5-180">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9d8a5-180">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/smartlpa-tutorial/create_aaduser_04.png)

    <span data-ttu-id="9d8a5-182">a.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-182">a.</span></span> <span data-ttu-id="9d8a5-183">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-183">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9d8a5-184">b.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-184">b.</span></span> <span data-ttu-id="9d8a5-185">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-185">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="9d8a5-186">c.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-186">c.</span></span> <span data-ttu-id="9d8a5-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="9d8a5-188">d.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-188">d.</span></span> <span data-ttu-id="9d8a5-189">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-189">Click **Create**.</span></span>
 
### <a name="create-a-smartlpa-test-user"></a><span data-ttu-id="9d8a5-190">Create a SmartLPA test user</span><span class="sxs-lookup"><span data-stu-id="9d8a5-190">Create a SmartLPA test user</span></span>

<span data-ttu-id="9d8a5-191">In this section, you create a user called Britta Simon in SmartLPA.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-191">In this section, you create a user called Britta Simon in SmartLPA.</span></span> <span data-ttu-id="9d8a5-192">Work with [SmartLPA support team](mailto:support@smartlpa.com) to add the users in the SmartLPA platform.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-192">Work with [SmartLPA support team](mailto:support@smartlpa.com) to add the users in the SmartLPA platform.</span></span> <span data-ttu-id="9d8a5-193">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-193">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="9d8a5-194">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="9d8a5-194">Assign the Azure AD test user</span></span>

<span data-ttu-id="9d8a5-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SmartLPA.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SmartLPA.</span></span>

![Assign the user role][200] 

<span data-ttu-id="9d8a5-197">**To assign Britta Simon to SmartLPA, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9d8a5-197">**To assign Britta Simon to SmartLPA, perform the following steps:**</span></span>

1. <span data-ttu-id="9d8a5-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="9d8a5-200">In the applications list, select **SmartLPA**.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-200">In the applications list, select **SmartLPA**.</span></span>

    ![The SmartLPA link in the Applications list](./media/smartlpa-tutorial/tutorial_smartlpa_app.png)  

3. <span data-ttu-id="9d8a5-202">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-202">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="9d8a5-204">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-204">Click **Add** button.</span></span> <span data-ttu-id="9d8a5-205">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="9d8a5-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9d8a5-208">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9d8a5-209">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="9d8a5-210">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="9d8a5-210">Test single sign-on</span></span>

<span data-ttu-id="9d8a5-211">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-211">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9d8a5-212">When you click the SmartLPA tile in the Access Panel, you should get automatically signed-on to your SmartLPA application.</span><span class="sxs-lookup"><span data-stu-id="9d8a5-212">When you click the SmartLPA tile in the Access Panel, you should get automatically signed-on to your SmartLPA application.</span></span>
<span data-ttu-id="9d8a5-213">For more information about the Access Panel, see [Introduction to the Access Panel](../active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9d8a5-213">For more information about the Access Panel, see [Introduction to the Access Panel](../active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9d8a5-214">Additional resources</span><span class="sxs-lookup"><span data-stu-id="9d8a5-214">Additional resources</span></span>

* [<span data-ttu-id="9d8a5-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9d8a5-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="9d8a5-216">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9d8a5-216">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/smartlpa-tutorial/tutorial_general_01.png
[2]: ./media/smartlpa-tutorial/tutorial_general_02.png
[3]: ./media/smartlpa-tutorial/tutorial_general_03.png
[4]: ./media/smartlpa-tutorial/tutorial_general_04.png

[100]: ./media/smartlpa-tutorial/tutorial_general_100.png

[200]: ./media/smartlpa-tutorial/tutorial_general_200.png
[201]: ./media/smartlpa-tutorial/tutorial_general_201.png
[202]: ./media/smartlpa-tutorial/tutorial_general_202.png
[203]: ./media/smartlpa-tutorial/tutorial_general_203.png

