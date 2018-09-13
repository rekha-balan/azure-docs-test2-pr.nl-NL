---
title: 'Tutorial: Azure Active Directory integration with direct | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and direct.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 7c2cd1f0-d14c-42f0-94a8-9b800008b285
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/06/2018
ms.author: jeedes
ms.openlocfilehash: 7e693a721e5556970607fafd8ff187d3b06c913e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868424"
---
# <a name="tutorial-azure-active-directory-integration-with-direct"></a><span data-ttu-id="d49b4-103">Tutorial: Azure Active Directory integration with direct</span><span class="sxs-lookup"><span data-stu-id="d49b4-103">Tutorial: Azure Active Directory integration with direct</span></span>

<span data-ttu-id="d49b4-104">In this tutorial, you learn how to integrate direct with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d49b4-104">In this tutorial, you learn how to integrate direct with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d49b4-105">Integrating direct with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="d49b4-105">Integrating direct with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d49b4-106">You can control in Azure AD who has access to direct</span><span class="sxs-lookup"><span data-stu-id="d49b4-106">You can control in Azure AD who has access to direct</span></span>
- <span data-ttu-id="d49b4-107">You can enable your users to automatically get signed-on to direct (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="d49b4-107">You can enable your users to automatically get signed-on to direct (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d49b4-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="d49b4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d49b4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="d49b4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d49b4-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d49b4-110">Prerequisites</span></span>

<span data-ttu-id="d49b4-111">To configure Azure AD integration with direct, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="d49b4-111">To configure Azure AD integration with direct, you need the following items:</span></span>

- <span data-ttu-id="d49b4-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="d49b4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d49b4-113">A direct single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="d49b4-113">A direct single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d49b4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="d49b4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d49b4-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="d49b4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d49b4-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="d49b4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d49b4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d49b4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d49b4-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="d49b4-118">Scenario description</span></span>

<span data-ttu-id="d49b4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="d49b4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>
<span data-ttu-id="d49b4-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="d49b4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d49b4-121">Adding direct from the gallery</span><span class="sxs-lookup"><span data-stu-id="d49b4-121">Adding direct from the gallery</span></span>
2. <span data-ttu-id="d49b4-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d49b4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-direct-from-the-gallery"></a><span data-ttu-id="d49b4-123">Adding direct from the gallery</span><span class="sxs-lookup"><span data-stu-id="d49b4-123">Adding direct from the gallery</span></span>

<span data-ttu-id="d49b4-124">To configure the integration of direct into Azure AD, you need to add direct from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="d49b4-124">To configure the integration of direct into Azure AD, you need to add direct from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d49b4-125">**To add direct from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d49b4-125">**To add direct from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d49b4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="d49b4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d49b4-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="d49b4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d49b4-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="d49b4-129">Then go to **All applications**.</span></span>

    ![Applications][2]

3. <span data-ttu-id="d49b4-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="d49b4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="d49b4-133">In the search box, type **direct**.</span><span class="sxs-lookup"><span data-stu-id="d49b4-133">In the search box, type **direct**.</span></span> <span data-ttu-id="d49b4-134">Select **direct** from the results panel, and then select the **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="d49b4-134">Select **direct** from the results panel, and then select the **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/direct-tutorial/tutorial_direct_addfromgallery.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d49b4-136">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d49b4-136">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="d49b4-137">In this section, you configure and test Azure AD single sign-on with direct based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="d49b4-137">In this section, you configure and test Azure AD single sign-on with direct based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d49b4-138">For single sign-on to work, Azure AD needs to know what the counterpart user in direct is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d49b4-138">For single sign-on to work, Azure AD needs to know what the counterpart user in direct is to a user in Azure AD.</span></span> <span data-ttu-id="d49b4-139">In other words, a link relationship between an Azure AD user and the related user in direct needs to be established.</span><span class="sxs-lookup"><span data-stu-id="d49b4-139">In other words, a link relationship between an Azure AD user and the related user in direct needs to be established.</span></span>

<span data-ttu-id="d49b4-140">In direct, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="d49b4-140">In direct, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d49b4-141">To configure and test Azure AD single sign-on with direct, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="d49b4-141">To configure and test Azure AD single sign-on with direct, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d49b4-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="d49b4-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d49b4-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d49b4-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d49b4-144">**[Creating a direct test user](#creating-a-direct-test-user)** - to have a counterpart of Britta Simon in direct that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="d49b4-144">**[Creating a direct test user](#creating-a-direct-test-user)** - to have a counterpart of Britta Simon in direct that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d49b4-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d49b4-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d49b4-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="d49b4-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d49b4-147">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d49b4-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d49b4-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your direct application.</span><span class="sxs-lookup"><span data-stu-id="d49b4-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your direct application.</span></span>

<span data-ttu-id="d49b4-149">**To configure Azure AD single sign-on with direct, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d49b4-149">**To configure Azure AD single sign-on with direct, perform the following steps:**</span></span>

1. <span data-ttu-id="d49b4-150">In the Azure portal, on the **direct** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="d49b4-150">In the Azure portal, on the **direct** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="d49b4-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d49b4-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/direct-tutorial/tutorial_direct_samlbase.png)

3. <span data-ttu-id="d49b4-154">On the **direct Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="d49b4-154">On the **direct Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configure Single Sign-On](./media/direct-tutorial/tutorial_direct_url.png)

    <span data-ttu-id="d49b4-156">In the **Identifier** textbox, type the URL: `https://direct4b.com/`</span><span class="sxs-lookup"><span data-stu-id="d49b4-156">In the **Identifier** textbox, type the URL: `https://direct4b.com/`</span></span>

4. <span data-ttu-id="d49b4-157">Check **Show advanced URL settings**, If you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="d49b4-157">Check **Show advanced URL settings**, If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configure Single Sign-On](./media/direct-tutorial/tutorial_direct_url1.png)

     <span data-ttu-id="d49b4-159">In the **Sign-on URL** textbox, type the URL: `https://direct4b.com/sso`</span><span class="sxs-lookup"><span data-stu-id="d49b4-159">In the **Sign-on URL** textbox, type the URL: `https://direct4b.com/sso`</span></span> 

5. <span data-ttu-id="d49b4-160">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="d49b4-160">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/direct-tutorial/tutorial_direct_certificate.png) 

6. <span data-ttu-id="d49b4-162">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="d49b4-162">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/direct-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="d49b4-164">To configure single sign-on on **direct** side, you need to send the downloaded **Metadata XML** to [direct support team](https://direct4b.com/ja/support.html#inquiry).</span><span class="sxs-lookup"><span data-stu-id="d49b4-164">To configure single sign-on on **direct** side, you need to send the downloaded **Metadata XML** to [direct support team](https://direct4b.com/ja/support.html#inquiry).</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d49b4-165">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d49b4-165">Creating an Azure AD test user</span></span>

<span data-ttu-id="d49b4-166">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d49b4-166">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="d49b4-168">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d49b4-168">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d49b4-169">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="d49b4-169">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/direct-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d49b4-171">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="d49b4-171">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/direct-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d49b4-173">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="d49b4-173">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>

    ![Creating an Azure AD test user](./media/direct-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d49b4-175">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d49b4-175">On the **User** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](./media/direct-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d49b4-177">a.</span><span class="sxs-lookup"><span data-stu-id="d49b4-177">a.</span></span> <span data-ttu-id="d49b4-178">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d49b4-178">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d49b4-179">b.</span><span class="sxs-lookup"><span data-stu-id="d49b4-179">b.</span></span> <span data-ttu-id="d49b4-180">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d49b4-180">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d49b4-181">c.</span><span class="sxs-lookup"><span data-stu-id="d49b4-181">c.</span></span> <span data-ttu-id="d49b4-182">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="d49b4-182">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d49b4-183">d.</span><span class="sxs-lookup"><span data-stu-id="d49b4-183">d.</span></span> <span data-ttu-id="d49b4-184">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="d49b4-184">Click **Create**.</span></span>

### <a name="creating-a-direct-test-user"></a><span data-ttu-id="d49b4-185">Creating a direct test user</span><span class="sxs-lookup"><span data-stu-id="d49b4-185">Creating a direct test user</span></span>

<span data-ttu-id="d49b4-186">In this section, you create a user called Britta Simon in direct.</span><span class="sxs-lookup"><span data-stu-id="d49b4-186">In this section, you create a user called Britta Simon in direct.</span></span> <span data-ttu-id="d49b4-187">Work with [direct support team](https://direct4b.com/ja/support.html#inquiry) to add the users in the direct platform.</span><span class="sxs-lookup"><span data-stu-id="d49b4-187">Work with [direct support team](https://direct4b.com/ja/support.html#inquiry) to add the users in the direct platform.</span></span> <span data-ttu-id="d49b4-188">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d49b4-188">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d49b4-189">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d49b4-189">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d49b4-190">In this section, you enable Britta Simon to use Azure single sign-on by granting access to direct.</span><span class="sxs-lookup"><span data-stu-id="d49b4-190">In this section, you enable Britta Simon to use Azure single sign-on by granting access to direct.</span></span>

![Assign User][200] 

<span data-ttu-id="d49b4-192">**To assign Britta Simon to direct, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d49b4-192">**To assign Britta Simon to direct, perform the following steps:**</span></span>

1. <span data-ttu-id="d49b4-193">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="d49b4-193">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="d49b4-195">In the applications list, select **direct**.</span><span class="sxs-lookup"><span data-stu-id="d49b4-195">In the applications list, select **direct**.</span></span>

    ![Configure Single Sign-On](./media/direct-tutorial/tutorial_direct_app.png) 

3. <span data-ttu-id="d49b4-197">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="d49b4-197">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="d49b4-199">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="d49b4-199">Click **Add** button.</span></span> <span data-ttu-id="d49b4-200">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="d49b4-200">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="d49b4-202">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="d49b4-202">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d49b4-203">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="d49b4-203">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d49b4-204">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="d49b4-204">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="d49b4-205">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="d49b4-205">Testing single sign-on</span></span>

<span data-ttu-id="d49b4-206">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="d49b4-206">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

1. <span data-ttu-id="d49b4-207">If you wish to test in **IDP Initiated Mode**:</span><span class="sxs-lookup"><span data-stu-id="d49b4-207">If you wish to test in **IDP Initiated Mode**:</span></span>

    <span data-ttu-id="d49b4-208">When you click the **direct** tile in the Access Panel, you should get automatically signed-on to your **direct** application.</span><span class="sxs-lookup"><span data-stu-id="d49b4-208">When you click the **direct** tile in the Access Panel, you should get automatically signed-on to your **direct** application.</span></span>

2. <span data-ttu-id="d49b4-209">If you wish to test in **SP Initiated Mode**:</span><span class="sxs-lookup"><span data-stu-id="d49b4-209">If you wish to test in **SP Initiated Mode**:</span></span>

    <span data-ttu-id="d49b4-210">a.</span><span class="sxs-lookup"><span data-stu-id="d49b4-210">a.</span></span> <span data-ttu-id="d49b4-211">Click on the **direct** tile in the Access Panel and you will be redirected to the application sign-on page.</span><span class="sxs-lookup"><span data-stu-id="d49b4-211">Click on the **direct** tile in the Access Panel and you will be redirected to the application sign-on page.</span></span>

    <span data-ttu-id="d49b4-212">b.</span><span class="sxs-lookup"><span data-stu-id="d49b4-212">b.</span></span> <span data-ttu-id="d49b4-213">Input your `subdomain` in the textbox displayed and press '次へ (Next)' and you should get automatically signed-on to your **direct** application .</span><span class="sxs-lookup"><span data-stu-id="d49b4-213">Input your `subdomain` in the textbox displayed and press '次へ (Next)' and you should get automatically signed-on to your **direct** application .</span></span>

<span data-ttu-id="d49b4-214">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d49b4-214">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d49b4-215">Additional resources</span><span class="sxs-lookup"><span data-stu-id="d49b4-215">Additional resources</span></span>

* [<span data-ttu-id="d49b4-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d49b4-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="d49b4-217">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d49b4-217">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/direct-tutorial/tutorial_general_01.png
[2]: ./media/direct-tutorial/tutorial_general_02.png
[3]: ./media/direct-tutorial/tutorial_general_03.png
[4]: ./media/direct-tutorial/tutorial_general_04.png

[100]: ./media/direct-tutorial/tutorial_general_100.png

[200]: ./media/direct-tutorial/tutorial_general_200.png
[201]: ./media/direct-tutorial/tutorial_general_201.png
[202]: ./media/direct-tutorial/tutorial_general_202.png
[203]: ./media/direct-tutorial/tutorial_general_203.png