---
title: 'Tutorial: Azure Active Directory integration with ZIVVER | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and ZIVVER.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 64cb7ea0-df6c-4963-84d8-6f435980e2de
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: b86a797fe092eccb097c6fbb34f1de7ee341c418
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866425"
---
# <a name="tutorial-azure-active-directory-integration-with-zivver"></a><span data-ttu-id="51fde-103">Tutorial: Azure Active Directory integration with ZIVVER</span><span class="sxs-lookup"><span data-stu-id="51fde-103">Tutorial: Azure Active Directory integration with ZIVVER</span></span>

<span data-ttu-id="51fde-104">In this tutorial, you learn how to integrate ZIVVER with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="51fde-104">In this tutorial, you learn how to integrate ZIVVER with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="51fde-105">Integrating ZIVVER with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="51fde-105">Integrating ZIVVER with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="51fde-106">You can control in Azure AD who has access to ZIVVER.</span><span class="sxs-lookup"><span data-stu-id="51fde-106">You can control in Azure AD who has access to ZIVVER.</span></span>
- <span data-ttu-id="51fde-107">You can enable your users to automatically get signed-on to ZIVVER (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="51fde-107">You can enable your users to automatically get signed-on to ZIVVER (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="51fde-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="51fde-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="51fde-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="51fde-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="51fde-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="51fde-110">Prerequisites</span></span>

<span data-ttu-id="51fde-111">To configure Azure AD integration with ZIVVER, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="51fde-111">To configure Azure AD integration with ZIVVER, you need the following items:</span></span>

- <span data-ttu-id="51fde-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="51fde-112">An Azure AD subscription</span></span>
- <span data-ttu-id="51fde-113">A ZIVVER single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="51fde-113">A ZIVVER single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="51fde-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="51fde-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="51fde-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="51fde-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="51fde-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="51fde-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="51fde-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="51fde-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="51fde-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="51fde-118">Scenario description</span></span>
<span data-ttu-id="51fde-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="51fde-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="51fde-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="51fde-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="51fde-121">Adding ZIVVER from the gallery</span><span class="sxs-lookup"><span data-stu-id="51fde-121">Adding ZIVVER from the gallery</span></span>
2. <span data-ttu-id="51fde-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="51fde-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zivver-from-the-gallery"></a><span data-ttu-id="51fde-123">Adding ZIVVER from the gallery</span><span class="sxs-lookup"><span data-stu-id="51fde-123">Adding ZIVVER from the gallery</span></span>
<span data-ttu-id="51fde-124">To configure the integration of ZIVVER into Azure AD, you need to add ZIVVER from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="51fde-124">To configure the integration of ZIVVER into Azure AD, you need to add ZIVVER from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="51fde-125">**To add ZIVVER from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="51fde-125">**To add ZIVVER from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="51fde-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="51fde-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="51fde-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="51fde-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="51fde-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="51fde-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="51fde-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="51fde-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="51fde-133">In the search box, type **ZIVVER**, select **ZIVVER** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="51fde-133">In the search box, type **ZIVVER**, select **ZIVVER** from result panel then click **Add** button to add the application.</span></span>

    ![ZIVVER in the results list](./media/zivver-tutorial/tutorial_zivver_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="51fde-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="51fde-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="51fde-136">In this section, you configure and test Azure AD single sign-on with ZIVVER based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="51fde-136">In this section, you configure and test Azure AD single sign-on with ZIVVER based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="51fde-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ZIVVER is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="51fde-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ZIVVER is to a user in Azure AD.</span></span> <span data-ttu-id="51fde-138">In other words, a link relationship between an Azure AD user and the related user in ZIVVER needs to be established.</span><span class="sxs-lookup"><span data-stu-id="51fde-138">In other words, a link relationship between an Azure AD user and the related user in ZIVVER needs to be established.</span></span>

<span data-ttu-id="51fde-139">In ZIVVER, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="51fde-139">In ZIVVER, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="51fde-140">To configure and test Azure AD single sign-on with ZIVVER, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="51fde-140">To configure and test Azure AD single sign-on with ZIVVER, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="51fde-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="51fde-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="51fde-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="51fde-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="51fde-143">**[Create a ZIVVER test user](#create-a-zivver-test-user)** - to have a counterpart of Britta Simon in ZIVVER that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="51fde-143">**[Create a ZIVVER test user](#create-a-zivver-test-user)** - to have a counterpart of Britta Simon in ZIVVER that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="51fde-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="51fde-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="51fde-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="51fde-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="51fde-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="51fde-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="51fde-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ZIVVER application.</span><span class="sxs-lookup"><span data-stu-id="51fde-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ZIVVER application.</span></span>

<span data-ttu-id="51fde-148">**To configure Azure AD single sign-on with ZIVVER, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="51fde-148">**To configure Azure AD single sign-on with ZIVVER, perform the following steps:**</span></span>

1. <span data-ttu-id="51fde-149">In the Azure portal, on the **ZIVVER** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="51fde-149">In the Azure portal, on the **ZIVVER** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="51fde-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="51fde-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/zivver-tutorial/tutorial_zivver_samlbase.png)

3. <span data-ttu-id="51fde-153">On the **ZIVVER Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="51fde-153">On the **ZIVVER Domain and URLs** section, perform the following steps:</span></span>

    ![ZIVVER Domain and URLs single sign-on information](./media/zivver-tutorial/tutorial_zivver_url.png)

    <span data-ttu-id="51fde-155">In the **Identifier** textbox, type the URL: `https://app.zivver.com/SAML/Zivver`</span><span class="sxs-lookup"><span data-stu-id="51fde-155">In the **Identifier** textbox, type the URL: `https://app.zivver.com/SAML/Zivver`</span></span>

4. <span data-ttu-id="51fde-156">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="51fde-156">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/zivver-tutorial/tutorial_zivver_certificate.png) 

5. <span data-ttu-id="51fde-158">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="51fde-158">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/zivver-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="51fde-160">To configure single sign-on on **ZIVVER** side, you need to send the downloaded **Metadata XML** to [ZIVVER support team](https://support.zivver.com).</span><span class="sxs-lookup"><span data-stu-id="51fde-160">To configure single sign-on on **ZIVVER** side, you need to send the downloaded **Metadata XML** to [ZIVVER support team](https://support.zivver.com).</span></span> <span data-ttu-id="51fde-161">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="51fde-161">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="51fde-162">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="51fde-162">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="51fde-163">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="51fde-163">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="51fde-164">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="51fde-164">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="51fde-165">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="51fde-165">Create an Azure AD test user</span></span>

<span data-ttu-id="51fde-166">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="51fde-166">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="51fde-168">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="51fde-168">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="51fde-169">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="51fde-169">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/zivver-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="51fde-171">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="51fde-171">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/zivver-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="51fde-173">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="51fde-173">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/zivver-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="51fde-175">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="51fde-175">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/zivver-tutorial/create_aaduser_04.png)

    <span data-ttu-id="51fde-177">a.</span><span class="sxs-lookup"><span data-stu-id="51fde-177">a.</span></span> <span data-ttu-id="51fde-178">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="51fde-178">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="51fde-179">b.</span><span class="sxs-lookup"><span data-stu-id="51fde-179">b.</span></span> <span data-ttu-id="51fde-180">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="51fde-180">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="51fde-181">c.</span><span class="sxs-lookup"><span data-stu-id="51fde-181">c.</span></span> <span data-ttu-id="51fde-182">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="51fde-182">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="51fde-183">d.</span><span class="sxs-lookup"><span data-stu-id="51fde-183">d.</span></span> <span data-ttu-id="51fde-184">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="51fde-184">Click **Create**.</span></span>
  
### <a name="create-a-zivver-test-user"></a><span data-ttu-id="51fde-185">Create a ZIVVER test user</span><span class="sxs-lookup"><span data-stu-id="51fde-185">Create a ZIVVER test user</span></span>

<span data-ttu-id="51fde-186">In this section, you create a user called Britta Simon in ZIVVER.</span><span class="sxs-lookup"><span data-stu-id="51fde-186">In this section, you create a user called Britta Simon in ZIVVER.</span></span> <span data-ttu-id="51fde-187">Work with [ZIVVER support team](https://support.zivver.com) to add the users in the ZIVVER platform.</span><span class="sxs-lookup"><span data-stu-id="51fde-187">Work with [ZIVVER support team](https://support.zivver.com) to add the users in the ZIVVER platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="51fde-188">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="51fde-188">Assign the Azure AD test user</span></span>

<span data-ttu-id="51fde-189">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ZIVVER.</span><span class="sxs-lookup"><span data-stu-id="51fde-189">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ZIVVER.</span></span>

![Assign the user role][200] 

<span data-ttu-id="51fde-191">**To assign Britta Simon to ZIVVER, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="51fde-191">**To assign Britta Simon to ZIVVER, perform the following steps:**</span></span>

1. <span data-ttu-id="51fde-192">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="51fde-192">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="51fde-194">In the applications list, select **ZIVVER**.</span><span class="sxs-lookup"><span data-stu-id="51fde-194">In the applications list, select **ZIVVER**.</span></span>

    ![The ZIVVER link in the Applications list](./media/zivver-tutorial/tutorial_zivver_app.png)  

3. <span data-ttu-id="51fde-196">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="51fde-196">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="51fde-198">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="51fde-198">Click **Add** button.</span></span> <span data-ttu-id="51fde-199">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="51fde-199">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="51fde-201">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="51fde-201">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="51fde-202">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="51fde-202">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="51fde-203">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="51fde-203">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="51fde-204">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="51fde-204">Test single sign-on</span></span>

<span data-ttu-id="51fde-205">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="51fde-205">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="51fde-206">When you click the ZIVVER tile in the Access Panel, you should get automatically signed-on to your ZIVVER application.</span><span class="sxs-lookup"><span data-stu-id="51fde-206">When you click the ZIVVER tile in the Access Panel, you should get automatically signed-on to your ZIVVER application.</span></span>
<span data-ttu-id="51fde-207">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="51fde-207">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="51fde-208">Additional resources</span><span class="sxs-lookup"><span data-stu-id="51fde-208">Additional resources</span></span>

* [<span data-ttu-id="51fde-209">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="51fde-209">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="51fde-210">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="51fde-210">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/zivver-tutorial/tutorial_general_01.png
[2]: ./media/zivver-tutorial/tutorial_general_02.png
[3]: ./media/zivver-tutorial/tutorial_general_03.png
[4]: ./media/zivver-tutorial/tutorial_general_04.png

[100]: ./media/zivver-tutorial/tutorial_general_100.png

[200]: ./media/zivver-tutorial/tutorial_general_200.png
[201]: ./media/zivver-tutorial/tutorial_general_201.png
[202]: ./media/zivver-tutorial/tutorial_general_202.png
[203]: ./media/zivver-tutorial/tutorial_general_203.png

