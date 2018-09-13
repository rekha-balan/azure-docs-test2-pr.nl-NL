---
title: 'Tutorial: Azure Active Directory integration with JobScore | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and JobScore.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 30f51b32-e55c-4c66-96e8-50a2f9c2194a
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 8fbe30d37c8fb906c829d5e76771155dfeb76fce
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867617"
---
# <a name="tutorial-azure-active-directory-integration-with-jobscore"></a><span data-ttu-id="82075-103">Tutorial: Azure Active Directory integration with JobScore</span><span class="sxs-lookup"><span data-stu-id="82075-103">Tutorial: Azure Active Directory integration with JobScore</span></span>

<span data-ttu-id="82075-104">In this tutorial, you learn how to integrate JobScore with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="82075-104">In this tutorial, you learn how to integrate JobScore with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="82075-105">Integrating JobScore with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="82075-105">Integrating JobScore with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="82075-106">You can control in Azure AD who has access to JobScore</span><span class="sxs-lookup"><span data-stu-id="82075-106">You can control in Azure AD who has access to JobScore</span></span>
- <span data-ttu-id="82075-107">You can enable your users to automatically get signed-on to JobScore (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="82075-107">You can enable your users to automatically get signed-on to JobScore (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="82075-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="82075-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="82075-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="82075-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82075-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="82075-110">Prerequisites</span></span>

<span data-ttu-id="82075-111">To configure Azure AD integration with JobScore, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="82075-111">To configure Azure AD integration with JobScore, you need the following items:</span></span>

- <span data-ttu-id="82075-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="82075-112">An Azure AD subscription</span></span>
- <span data-ttu-id="82075-113">A JobScore single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="82075-113">A JobScore single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="82075-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="82075-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="82075-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="82075-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="82075-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="82075-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="82075-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="82075-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="82075-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="82075-118">Scenario description</span></span>
<span data-ttu-id="82075-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="82075-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="82075-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="82075-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="82075-121">Adding JobScore from the gallery</span><span class="sxs-lookup"><span data-stu-id="82075-121">Adding JobScore from the gallery</span></span>
1. <span data-ttu-id="82075-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="82075-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jobscore-from-the-gallery"></a><span data-ttu-id="82075-123">Adding JobScore from the gallery</span><span class="sxs-lookup"><span data-stu-id="82075-123">Adding JobScore from the gallery</span></span>
<span data-ttu-id="82075-124">To configure the integration of JobScore into Azure AD, you need to add JobScore from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="82075-124">To configure the integration of JobScore into Azure AD, you need to add JobScore from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="82075-125">**To add JobScore from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="82075-125">**To add JobScore from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="82075-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="82075-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="82075-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="82075-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="82075-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="82075-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="82075-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="82075-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="82075-133">In the search box, type **JobScore**.</span><span class="sxs-lookup"><span data-stu-id="82075-133">In the search box, type **JobScore**.</span></span>

    ![Creating an Azure AD test user](./media/jobscore-tutorial/tutorial_jobscore_search.png)

1. <span data-ttu-id="82075-135">In the results panel, select **JobScore**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="82075-135">In the results panel, select **JobScore**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/jobscore-tutorial/tutorial_jobscore_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="82075-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="82075-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="82075-138">In this section, you configure and test Azure AD single sign-on with JobScore based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="82075-138">In this section, you configure and test Azure AD single sign-on with JobScore based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="82075-139">For single sign-on to work, Azure AD needs to know what the counterpart user in JobScore is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="82075-139">For single sign-on to work, Azure AD needs to know what the counterpart user in JobScore is to a user in Azure AD.</span></span> <span data-ttu-id="82075-140">In other words, a link relationship between an Azure AD user and the related user in JobScore needs to be established.</span><span class="sxs-lookup"><span data-stu-id="82075-140">In other words, a link relationship between an Azure AD user and the related user in JobScore needs to be established.</span></span>

<span data-ttu-id="82075-141">In JobScore, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="82075-141">In JobScore, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="82075-142">To configure and test Azure AD single sign-on with JobScore, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="82075-142">To configure and test Azure AD single sign-on with JobScore, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="82075-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="82075-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="82075-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="82075-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="82075-145">**[Creating a JobScore test user](#creating-a-jobscore-test-user)** - to have a counterpart of Britta Simon in JobScore that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="82075-145">**[Creating a JobScore test user](#creating-a-jobscore-test-user)** - to have a counterpart of Britta Simon in JobScore that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="82075-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="82075-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="82075-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="82075-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="82075-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="82075-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="82075-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your JobScore application.</span><span class="sxs-lookup"><span data-stu-id="82075-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your JobScore application.</span></span>

<span data-ttu-id="82075-150">**To configure Azure AD single sign-on with JobScore, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="82075-150">**To configure Azure AD single sign-on with JobScore, perform the following steps:**</span></span>

1. <span data-ttu-id="82075-151">In the Azure portal, on the **JobScore** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="82075-151">In the Azure portal, on the **JobScore** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="82075-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="82075-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/jobscore-tutorial/tutorial_jobscore_samlbase.png)

1. <span data-ttu-id="82075-155">On the **JobScore Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="82075-155">On the **JobScore Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/jobscore-tutorial/tutorial_jobscore_url.png)

    <span data-ttu-id="82075-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://hire.jobscore.com/auth/adfs/<company name>`</span><span class="sxs-lookup"><span data-stu-id="82075-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://hire.jobscore.com/auth/adfs/<company name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="82075-158">This value is not real.</span><span class="sxs-lookup"><span data-stu-id="82075-158">This value is not real.</span></span> <span data-ttu-id="82075-159">Update this value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="82075-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="82075-160">Contact [JobScore Client support team](mailto:support@jobscore.com) to get this value.</span><span class="sxs-lookup"><span data-stu-id="82075-160">Contact [JobScore Client support team](mailto:support@jobscore.com) to get this value.</span></span> 
 
1. <span data-ttu-id="82075-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="82075-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/jobscore-tutorial/tutorial_jobscore_certificate.png) 

1. <span data-ttu-id="82075-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="82075-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/jobscore-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="82075-165">To configure single sign-on on **JobScore** side, you need to send the downloaded **Metadata XML** to [JobScore support team](mailto:support@jobscore.com).</span><span class="sxs-lookup"><span data-stu-id="82075-165">To configure single sign-on on **JobScore** side, you need to send the downloaded **Metadata XML** to [JobScore support team](mailto:support@jobscore.com).</span></span> 

> [!TIP]
> <span data-ttu-id="82075-166">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="82075-166">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="82075-167">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="82075-167">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="82075-168">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="82075-168">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="82075-169">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="82075-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="82075-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="82075-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="82075-172">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="82075-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="82075-173">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="82075-173">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/jobscore-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="82075-175">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="82075-175">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/jobscore-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="82075-177">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="82075-177">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/jobscore-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="82075-179">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="82075-179">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/jobscore-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="82075-181">a.</span><span class="sxs-lookup"><span data-stu-id="82075-181">a.</span></span> <span data-ttu-id="82075-182">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="82075-182">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="82075-183">b.</span><span class="sxs-lookup"><span data-stu-id="82075-183">b.</span></span> <span data-ttu-id="82075-184">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="82075-184">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="82075-185">c.</span><span class="sxs-lookup"><span data-stu-id="82075-185">c.</span></span> <span data-ttu-id="82075-186">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="82075-186">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="82075-187">d.</span><span class="sxs-lookup"><span data-stu-id="82075-187">d.</span></span> <span data-ttu-id="82075-188">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="82075-188">Click **Create**.</span></span>
 
### <a name="creating-a-jobscore-test-user"></a><span data-ttu-id="82075-189">Creating a JobScore test user</span><span class="sxs-lookup"><span data-stu-id="82075-189">Creating a JobScore test user</span></span>

<span data-ttu-id="82075-190">In this section, you create a user called Britta Simon in JobScore.</span><span class="sxs-lookup"><span data-stu-id="82075-190">In this section, you create a user called Britta Simon in JobScore.</span></span> <span data-ttu-id="82075-191">Work with [JobScore support team](mailto:support@jobscore.com) to add the users in the JobScore platform.</span><span class="sxs-lookup"><span data-stu-id="82075-191">Work with [JobScore support team](mailto:support@jobscore.com) to add the users in the JobScore platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="82075-192">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="82075-192">Assigning the Azure AD test user</span></span>

<span data-ttu-id="82075-193">In this section, you enable Britta Simon to use Azure single sign-on by granting access to JobScore.</span><span class="sxs-lookup"><span data-stu-id="82075-193">In this section, you enable Britta Simon to use Azure single sign-on by granting access to JobScore.</span></span>

![Assign User][200] 

<span data-ttu-id="82075-195">**To assign Britta Simon to JobScore, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="82075-195">**To assign Britta Simon to JobScore, perform the following steps:**</span></span>

1. <span data-ttu-id="82075-196">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="82075-196">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="82075-198">In the applications list, select **JobScore**.</span><span class="sxs-lookup"><span data-stu-id="82075-198">In the applications list, select **JobScore**.</span></span>

    ![Configure Single Sign-On](./media/jobscore-tutorial/tutorial_jobscore_app.png) 

1. <span data-ttu-id="82075-200">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="82075-200">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="82075-202">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="82075-202">Click **Add** button.</span></span> <span data-ttu-id="82075-203">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="82075-203">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="82075-205">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="82075-205">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="82075-206">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="82075-206">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="82075-207">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="82075-207">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="82075-208">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="82075-208">Testing single sign-on</span></span>

<span data-ttu-id="82075-209">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="82075-209">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="82075-210">When you click the JobScore tile in the Access Panel, you should get automatically signed-on to your JobScore application.</span><span class="sxs-lookup"><span data-stu-id="82075-210">When you click the JobScore tile in the Access Panel, you should get automatically signed-on to your JobScore application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="82075-211">Additional resources</span><span class="sxs-lookup"><span data-stu-id="82075-211">Additional resources</span></span>

* [<span data-ttu-id="82075-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="82075-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="82075-213">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="82075-213">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/jobscore-tutorial/tutorial_general_01.png
[2]: ./media/jobscore-tutorial/tutorial_general_02.png
[3]: ./media/jobscore-tutorial/tutorial_general_03.png
[4]: ./media/jobscore-tutorial/tutorial_general_04.png

[100]: ./media/jobscore-tutorial/tutorial_general_100.png

[200]: ./media/jobscore-tutorial/tutorial_general_200.png
[201]: ./media/jobscore-tutorial/tutorial_general_201.png
[202]: ./media/jobscore-tutorial/tutorial_general_202.png
[203]: ./media/jobscore-tutorial/tutorial_general_203.png

