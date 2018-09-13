---
title: 'Tutorial: Azure Active Directory integration with QPrism | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and QPrism.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 72ab75ba-132b-4f83-a34b-d28b81b6d7bc
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/23/2018
ms.author: jeedes
ms.openlocfilehash: ddf22491d7531daecf4448e62e8594c3326d7b77
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869327"
---
# <a name="tutorial-azure-active-directory-integration-with-qprism"></a><span data-ttu-id="792c5-103">Tutorial: Azure Active Directory integration with QPrism</span><span class="sxs-lookup"><span data-stu-id="792c5-103">Tutorial: Azure Active Directory integration with QPrism</span></span>

<span data-ttu-id="792c5-104">In this tutorial, you learn how to integrate QPrism with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="792c5-104">In this tutorial, you learn how to integrate QPrism with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="792c5-105">Integrating QPrism with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="792c5-105">Integrating QPrism with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="792c5-106">You can control in Azure AD who has access to QPrism.</span><span class="sxs-lookup"><span data-stu-id="792c5-106">You can control in Azure AD who has access to QPrism.</span></span>
- <span data-ttu-id="792c5-107">You can enable your users to automatically get signed on to QPrism (single sign-on) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="792c5-107">You can enable your users to automatically get signed on to QPrism (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="792c5-108">You can manage your accounts in one central location: the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="792c5-108">You can manage your accounts in one central location: the Azure portal.</span></span>

<span data-ttu-id="792c5-109">For more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="792c5-109">For more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="792c5-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="792c5-110">Prerequisites</span></span>

<span data-ttu-id="792c5-111">To configure Azure AD integration with QPrism, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="792c5-111">To configure Azure AD integration with QPrism, you need the following items:</span></span>

- <span data-ttu-id="792c5-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="792c5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="792c5-113">A QPrism single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="792c5-113">A QPrism single sign-on enabled subscription</span></span>

<span data-ttu-id="792c5-114">To test the steps in this tutorial, follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="792c5-114">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="792c5-115">Don't use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="792c5-115">Don't use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="792c5-116">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="792c5-116">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="792c5-117">Scenario description</span><span class="sxs-lookup"><span data-stu-id="792c5-117">Scenario description</span></span>
<span data-ttu-id="792c5-118">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="792c5-118">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="792c5-119">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="792c5-119">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="792c5-120">Adding QPrism from the gallery</span><span class="sxs-lookup"><span data-stu-id="792c5-120">Adding QPrism from the gallery</span></span>
1. <span data-ttu-id="792c5-121">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="792c5-121">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-qprism-from-the-gallery"></a><span data-ttu-id="792c5-122">Add QPrism from the gallery</span><span class="sxs-lookup"><span data-stu-id="792c5-122">Add QPrism from the gallery</span></span>
<span data-ttu-id="792c5-123">To configure the integration of QPrism into Azure AD, you need to add QPrism from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="792c5-123">To configure the integration of QPrism into Azure AD, you need to add QPrism from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="792c5-124">**To add QPrism from the gallery:**</span><span class="sxs-lookup"><span data-stu-id="792c5-124">**To add QPrism from the gallery:**</span></span>

1. <span data-ttu-id="792c5-125">In the [Azure portal](https://portal.azure.com), in the left pane, select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="792c5-125">In the [Azure portal](https://portal.azure.com), in the left pane, select **Azure Active Directory**.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="792c5-127">Navigate to **Enterprise applications** > **All applications**.</span><span class="sxs-lookup"><span data-stu-id="792c5-127">Navigate to **Enterprise applications** > **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="792c5-129">To add a new application, at the top of the dialog box, select **New application**.</span><span class="sxs-lookup"><span data-stu-id="792c5-129">To add a new application, at the top of the dialog box, select **New application**.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="792c5-131">In the search box, type **QPrism**, and select **QPrism** from result panel.</span><span class="sxs-lookup"><span data-stu-id="792c5-131">In the search box, type **QPrism**, and select **QPrism** from result panel.</span></span> <span data-ttu-id="792c5-132">Then click **Add** to add the application.</span><span class="sxs-lookup"><span data-stu-id="792c5-132">Then click **Add** to add the application.</span></span>

    ![QPrism in the results list](./media/qprism-tutorial/tutorial_qprism_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="792c5-134">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="792c5-134">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="792c5-135">In this section, you configure and test Azure AD single sign-on with QPrism, based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="792c5-135">In this section, you configure and test Azure AD single sign-on with QPrism, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="792c5-136">For single sign-on to work, Azure AD needs to know who the counterpart user in QPrism is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="792c5-136">For single sign-on to work, Azure AD needs to know who the counterpart user in QPrism is to a user in Azure AD.</span></span> <span data-ttu-id="792c5-137">In other words, there must be a linked relationship between an Azure AD user and the related user in QPrism.</span><span class="sxs-lookup"><span data-stu-id="792c5-137">In other words, there must be a linked relationship between an Azure AD user and the related user in QPrism.</span></span>

<span data-ttu-id="792c5-138">To establish this relationship, in QPrism, assign the value of the **user name** in Azure AD as the value of the **Username**.</span><span class="sxs-lookup"><span data-stu-id="792c5-138">To establish this relationship, in QPrism, assign the value of the **user name** in Azure AD as the value of the **Username**.</span></span>

<span data-ttu-id="792c5-139">To configure and test Azure AD single sign-on with QPrism, complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="792c5-139">To configure and test Azure AD single sign-on with QPrism, complete the following building blocks:</span></span>

1. <span data-ttu-id="792c5-140">[Configure Azure AD single sign-on](#configure-azure-ad-single-sign-on) to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="792c5-140">[Configure Azure AD single sign-on](#configure-azure-ad-single-sign-on) to enable your users to use this feature.</span></span>
1. <span data-ttu-id="792c5-141">[Create an Azure AD test user](#create-an-azure-ad-test-user) to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="792c5-141">[Create an Azure AD test user](#create-an-azure-ad-test-user) to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="792c5-142">[Create a QPrism test user](#create-a-qprism-test-user) to have a counterpart of Britta Simon in QPrism who is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="792c5-142">[Create a QPrism test user](#create-a-qprism-test-user) to have a counterpart of Britta Simon in QPrism who is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="792c5-143">[Assign the Azure AD test user](#assign-the-azure-ad-test-user) to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="792c5-143">[Assign the Azure AD test user](#assign-the-azure-ad-test-user) to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="792c5-144">[Test single sign-on](#test-single-sign-on) to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="792c5-144">[Test single sign-on](#test-single-sign-on) to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="792c5-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="792c5-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="792c5-146">In this section, you enable Azure AD single sign-on in the Azure portal, and configure single sign-on in your QPrism application.</span><span class="sxs-lookup"><span data-stu-id="792c5-146">In this section, you enable Azure AD single sign-on in the Azure portal, and configure single sign-on in your QPrism application.</span></span>

1. <span data-ttu-id="792c5-147">In the Azure portal, on the **QPrism** application integration page, select **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="792c5-147">In the Azure portal, on the **QPrism** application integration page, select **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="792c5-149">On the **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="792c5-149">On the **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/qprism-tutorial/tutorial_qprism_samlbase.png)

1. <span data-ttu-id="792c5-151">In the **QPrism Domain and URLs** section, do the following:</span><span class="sxs-lookup"><span data-stu-id="792c5-151">In the **QPrism Domain and URLs** section, do the following:</span></span>

    ![QPrism Domain and URLs single sign-on information](./media/qprism-tutorial/tutorial_qprism_url.png)

    <span data-ttu-id="792c5-153">a.</span><span class="sxs-lookup"><span data-stu-id="792c5-153">a.</span></span> <span data-ttu-id="792c5-154">In the **Sign-on URL** text box, type a URL that uses the following pattern: `https://<customer domain>.qmyzone.com/login`</span><span class="sxs-lookup"><span data-stu-id="792c5-154">In the **Sign-on URL** text box, type a URL that uses the following pattern: `https://<customer domain>.qmyzone.com/login`</span></span>

    <span data-ttu-id="792c5-155">b.</span><span class="sxs-lookup"><span data-stu-id="792c5-155">b.</span></span> <span data-ttu-id="792c5-156">In the **Identifier** text box, type a URL that uses the following pattern: `https://<customer domain>.qmyzone.com/metadata.php`</span><span class="sxs-lookup"><span data-stu-id="792c5-156">In the **Identifier** text box, type a URL that uses the following pattern: `https://<customer domain>.qmyzone.com/metadata.php`</span></span>
         
    > [!NOTE] 
    > <span data-ttu-id="792c5-157">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="792c5-157">These values are not real.</span></span> <span data-ttu-id="792c5-158">Update these values with the actual identifier and sign-on URL.</span><span class="sxs-lookup"><span data-stu-id="792c5-158">Update these values with the actual identifier and sign-on URL.</span></span> <span data-ttu-id="792c5-159">Contact [QPrism Client support team](mailto:qsupport-ce@quatrro.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="792c5-159">Contact [QPrism Client support team](mailto:qsupport-ce@quatrro.com) to get these values.</span></span> 

1. <span data-ttu-id="792c5-160">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span><span class="sxs-lookup"><span data-stu-id="792c5-160">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span></span>

     ![The Certificate download link](./media/qprism-tutorial/tutorial_qprism_certificate.png)

1. <span data-ttu-id="792c5-162">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="792c5-162">Select **Save**.</span></span>

    ![Configure single sign-on Save button](./media/qprism-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="792c5-164">To configure single sign-on on **QPrism** side, you need to send the **App Federation Metadata Url** to [QPrism support team](mailto:qsupport-ce@quatrro.com).</span><span class="sxs-lookup"><span data-stu-id="792c5-164">To configure single sign-on on **QPrism** side, you need to send the **App Federation Metadata Url** to [QPrism support team](mailto:qsupport-ce@quatrro.com).</span></span> <span data-ttu-id="792c5-165">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="792c5-165">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="792c5-166">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="792c5-166">Create an Azure AD test user</span></span>

<span data-ttu-id="792c5-167">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="792c5-167">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="792c5-169">**To create a test user in Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="792c5-169">**To create a test user in Azure AD:**</span></span>

1. <span data-ttu-id="792c5-170">In the Azure portal, in the left pane, select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="792c5-170">In the Azure portal, in the left pane, select **Azure Active Directory**.</span></span>

    ![The Azure Active Directory button](./media/qprism-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="792c5-172">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="792c5-172">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/qprism-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="792c5-174">To open the **User** dialog box, at the top of the **All Users** dialog box, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="792c5-174">To open the **User** dialog box, at the top of the **All Users** dialog box, select **Add**.</span></span>

    ![The Add button](./media/qprism-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="792c5-176">In the **User** dialog box, do the following:</span><span class="sxs-lookup"><span data-stu-id="792c5-176">In the **User** dialog box, do the following:</span></span>

    ![The User dialog box](./media/qprism-tutorial/create_aaduser_04.png)

    <span data-ttu-id="792c5-178">a.</span><span class="sxs-lookup"><span data-stu-id="792c5-178">a.</span></span> <span data-ttu-id="792c5-179">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="792c5-179">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="792c5-180">b.</span><span class="sxs-lookup"><span data-stu-id="792c5-180">b.</span></span> <span data-ttu-id="792c5-181">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="792c5-181">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="792c5-182">c.</span><span class="sxs-lookup"><span data-stu-id="792c5-182">c.</span></span> <span data-ttu-id="792c5-183">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="792c5-183">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="792c5-184">d.</span><span class="sxs-lookup"><span data-stu-id="792c5-184">d.</span></span> <span data-ttu-id="792c5-185">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="792c5-185">Select **Create**.</span></span>
 
### <a name="create-a-qprism-test-user"></a><span data-ttu-id="792c5-186">Create a QPrism test user</span><span class="sxs-lookup"><span data-stu-id="792c5-186">Create a QPrism test user</span></span>

<span data-ttu-id="792c5-187">In this section, you create a user called Britta Simon in QPrism.</span><span class="sxs-lookup"><span data-stu-id="792c5-187">In this section, you create a user called Britta Simon in QPrism.</span></span> <span data-ttu-id="792c5-188">Work with the [QPrism support team](mailto:qsupport-ce@quatrro.com) to add users in the QPrism platform.</span><span class="sxs-lookup"><span data-stu-id="792c5-188">Work with the [QPrism support team](mailto:qsupport-ce@quatrro.com) to add users in the QPrism platform.</span></span> <span data-ttu-id="792c5-189">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="792c5-189">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="792c5-190">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="792c5-190">Assign the Azure AD test user</span></span>

<span data-ttu-id="792c5-191">In this section, you enable Britta Simon to use Azure single sign-on by granting access to QPrism.</span><span class="sxs-lookup"><span data-stu-id="792c5-191">In this section, you enable Britta Simon to use Azure single sign-on by granting access to QPrism.</span></span>

![Assign the user role][200] 

<span data-ttu-id="792c5-193">**To assign Britta Simon to QPrism:**</span><span class="sxs-lookup"><span data-stu-id="792c5-193">**To assign Britta Simon to QPrism:**</span></span>

1. <span data-ttu-id="792c5-194">In the Azure portal, open the applications view, and then navigate to the directory view.</span><span class="sxs-lookup"><span data-stu-id="792c5-194">In the Azure portal, open the applications view, and then navigate to the directory view.</span></span> <span data-ttu-id="792c5-195">Go to **Enterprise applications**, and select **All applications**.</span><span class="sxs-lookup"><span data-stu-id="792c5-195">Go to **Enterprise applications**, and select **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="792c5-197">In the applications list, select **QPrism**.</span><span class="sxs-lookup"><span data-stu-id="792c5-197">In the applications list, select **QPrism**.</span></span>

    ![The QPrism link in the applications list](./media/qprism-tutorial/tutorial_qprism_app.png)  

1. <span data-ttu-id="792c5-199">In the menu on the left, select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="792c5-199">In the menu on the left, select **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="792c5-201">Select **Add**.</span><span class="sxs-lookup"><span data-stu-id="792c5-201">Select **Add**.</span></span> <span data-ttu-id="792c5-202">Then, under **Add Assignment**, select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="792c5-202">Then, under **Add Assignment**, select **Users and groups**.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="792c5-204">On the **Users and groups** dialog box, select **Britta Simon** in the **Users** list.</span><span class="sxs-lookup"><span data-stu-id="792c5-204">On the **Users and groups** dialog box, select **Britta Simon** in the **Users** list.</span></span>

1. <span data-ttu-id="792c5-205">On the **Users and groups** dialog box, select **Select**.</span><span class="sxs-lookup"><span data-stu-id="792c5-205">On the **Users and groups** dialog box, select **Select**.</span></span>

1. <span data-ttu-id="792c5-206">Under **Add Assignment**, select **Assign**.</span><span class="sxs-lookup"><span data-stu-id="792c5-206">Under **Add Assignment**, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="792c5-207">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="792c5-207">Test single sign-on</span></span>

<span data-ttu-id="792c5-208">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="792c5-208">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="792c5-209">In the Access Panel, when you select the QPrism tile, you should get automatically signed on to your QPrism application.</span><span class="sxs-lookup"><span data-stu-id="792c5-209">In the Access Panel, when you select the QPrism tile, you should get automatically signed on to your QPrism application.</span></span>
<span data-ttu-id="792c5-210">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="792c5-210">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="792c5-211">Additional resources</span><span class="sxs-lookup"><span data-stu-id="792c5-211">Additional resources</span></span>

* [<span data-ttu-id="792c5-212">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="792c5-212">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="792c5-213">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="792c5-213">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/qprism-tutorial/tutorial_general_01.png
[2]: ./media/qprism-tutorial/tutorial_general_02.png
[3]: ./media/qprism-tutorial/tutorial_general_03.png
[4]: ./media/qprism-tutorial/tutorial_general_04.png

[100]: ./media/qprism-tutorial/tutorial_general_100.png

[200]: ./media/qprism-tutorial/tutorial_general_200.png
[201]: ./media/qprism-tutorial/tutorial_general_201.png
[202]: ./media/qprism-tutorial/tutorial_general_202.png
[203]: ./media/qprism-tutorial/tutorial_general_203.png

