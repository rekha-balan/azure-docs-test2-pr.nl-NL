---
title: 'Tutorial: Azure Active Directory integration with MCM | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and MCM.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 7f00799d-e3e9-4ba9-ae4a-fbca843ac5db
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: 5ddd28838e7db7b7f2798b18028aba56246fda4c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871225"
---
# <a name="tutorial-azure-active-directory-integration-with-mcm"></a><span data-ttu-id="7a5aa-103">Tutorial: Azure Active Directory integration with MCM</span><span class="sxs-lookup"><span data-stu-id="7a5aa-103">Tutorial: Azure Active Directory integration with MCM</span></span>

<span data-ttu-id="7a5aa-104">In this tutorial, you learn how to integrate MCM with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7a5aa-104">In this tutorial, you learn how to integrate MCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7a5aa-105">Integrating MCM with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="7a5aa-105">Integrating MCM with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7a5aa-106">You can control in Azure AD who has access to MCM</span><span class="sxs-lookup"><span data-stu-id="7a5aa-106">You can control in Azure AD who has access to MCM</span></span>
- <span data-ttu-id="7a5aa-107">You can enable your users to automatically get signed-on to MCM (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="7a5aa-107">You can enable your users to automatically get signed-on to MCM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7a5aa-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="7a5aa-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7a5aa-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="7a5aa-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a5aa-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7a5aa-110">Prerequisites</span></span>

<span data-ttu-id="7a5aa-111">To configure Azure AD integration with MCM, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="7a5aa-111">To configure Azure AD integration with MCM, you need the following items:</span></span>

- <span data-ttu-id="7a5aa-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="7a5aa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7a5aa-113">A MCM single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="7a5aa-113">A MCM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7a5aa-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7a5aa-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="7a5aa-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7a5aa-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7a5aa-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7a5aa-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7a5aa-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="7a5aa-118">Scenario description</span></span>
<span data-ttu-id="7a5aa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7a5aa-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="7a5aa-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7a5aa-121">Adding MCM from the gallery</span><span class="sxs-lookup"><span data-stu-id="7a5aa-121">Adding MCM from the gallery</span></span>
1. <span data-ttu-id="7a5aa-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7a5aa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mcm-from-the-gallery"></a><span data-ttu-id="7a5aa-123">Adding MCM from the gallery</span><span class="sxs-lookup"><span data-stu-id="7a5aa-123">Adding MCM from the gallery</span></span>
<span data-ttu-id="7a5aa-124">To configure the integration of MCM into Azure AD, you need to add MCM from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-124">To configure the integration of MCM into Azure AD, you need to add MCM from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7a5aa-125">**To add MCM from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7a5aa-125">**To add MCM from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7a5aa-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="7a5aa-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7a5aa-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="7a5aa-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="7a5aa-133">In the search box, type **MCM**.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-133">In the search box, type **MCM**.</span></span>

    ![Creating an Azure AD test user](./media/mcm-tutorial/tutorial_mcm_search.png)

1. <span data-ttu-id="7a5aa-135">In the results panel, select **MCM**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-135">In the results panel, select **MCM**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/mcm-tutorial/tutorial_mcm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7a5aa-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7a5aa-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7a5aa-138">In this section, you configure and test Azure AD single sign-on with MCM based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7a5aa-138">In this section, you configure and test Azure AD single sign-on with MCM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7a5aa-139">For single sign-on to work, Azure AD needs to know what the counterpart user in MCM is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-139">For single sign-on to work, Azure AD needs to know what the counterpart user in MCM is to a user in Azure AD.</span></span> <span data-ttu-id="7a5aa-140">In other words, a link relationship between an Azure AD user and the related user in MCM needs to be established.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-140">In other words, a link relationship between an Azure AD user and the related user in MCM needs to be established.</span></span>

<span data-ttu-id="7a5aa-141">In MCM, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-141">In MCM, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7a5aa-142">To configure and test Azure AD single sign-on with MCM, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="7a5aa-142">To configure and test Azure AD single sign-on with MCM, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7a5aa-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="7a5aa-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="7a5aa-145">**[Creating a MCM test user](#creating-a-mcm-test-user)** - to have a counterpart of Britta Simon in MCM that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-145">**[Creating a MCM test user](#creating-a-mcm-test-user)** - to have a counterpart of Britta Simon in MCM that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="7a5aa-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="7a5aa-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7a5aa-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7a5aa-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7a5aa-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your MCM application.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your MCM application.</span></span>

<span data-ttu-id="7a5aa-150">**To configure Azure AD single sign-on with MCM, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7a5aa-150">**To configure Azure AD single sign-on with MCM, perform the following steps:**</span></span>

1. <span data-ttu-id="7a5aa-151">In the Azure portal, on the **MCM** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-151">In the Azure portal, on the **MCM** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="7a5aa-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/mcm-tutorial/tutorial_mcm_samlbase.png)

1. <span data-ttu-id="7a5aa-155">On the **MCM Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7a5aa-155">On the **MCM Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/mcm-tutorial/tutorial_mcm_url.png)

    <span data-ttu-id="7a5aa-157">a.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-157">a.</span></span> <span data-ttu-id="7a5aa-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://myaba.co.uk/client-access/<companyname>/saml.php`</span><span class="sxs-lookup"><span data-stu-id="7a5aa-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://myaba.co.uk/client-access/<companyname>/saml.php`</span></span>

    <span data-ttu-id="7a5aa-159">b.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-159">b.</span></span> <span data-ttu-id="7a5aa-160">In the **Identifier** textbox, type a URL using the following pattern: `https://myaba.co.uk/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="7a5aa-160">In the **Identifier** textbox, type a URL using the following pattern: `https://myaba.co.uk/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7a5aa-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-161">These values are not real.</span></span> <span data-ttu-id="7a5aa-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="7a5aa-163">Contact [MCM Client support team](http://mcmtechnology.com/support/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-163">Contact [MCM Client support team](http://mcmtechnology.com/support/) to get these values.</span></span> 
 
1. <span data-ttu-id="7a5aa-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/mcm-tutorial/tutorial_mcm_certificate.png) 

1. <span data-ttu-id="7a5aa-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/mcm-tutorial/tutorial_general_400.png) 

1. <span data-ttu-id="7a5aa-168">To configure single sign-on on **MCM** side, you need to send the downloaded **Metadata XML** to [MCM support team](http://mcmtechnology.com/support/).</span><span class="sxs-lookup"><span data-stu-id="7a5aa-168">To configure single sign-on on **MCM** side, you need to send the downloaded **Metadata XML** to [MCM support team](http://mcmtechnology.com/support/).</span></span> <span data-ttu-id="7a5aa-169">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="7a5aa-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="7a5aa-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7a5aa-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7a5aa-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7a5aa-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7a5aa-173">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7a5aa-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="7a5aa-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="7a5aa-176">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7a5aa-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7a5aa-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/mcm-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="7a5aa-179">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/mcm-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="7a5aa-181">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/mcm-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="7a5aa-183">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7a5aa-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/mcm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7a5aa-185">a.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-185">a.</span></span> <span data-ttu-id="7a5aa-186">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7a5aa-187">b.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-187">b.</span></span> <span data-ttu-id="7a5aa-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7a5aa-189">c.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-189">c.</span></span> <span data-ttu-id="7a5aa-190">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7a5aa-191">d.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-191">d.</span></span> <span data-ttu-id="7a5aa-192">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-192">Click **Create**.</span></span>
 
### <a name="creating-a-mcm-test-user"></a><span data-ttu-id="7a5aa-193">Creating a MCM test user</span><span class="sxs-lookup"><span data-stu-id="7a5aa-193">Creating a MCM test user</span></span>

<span data-ttu-id="7a5aa-194">In this section, you create a user called Britta Simon in MCM.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-194">In this section, you create a user called Britta Simon in MCM.</span></span> <span data-ttu-id="7a5aa-195">Work with [MCM support team](http://mcmtechnology.com/support/) to add the users in the MCM platform.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-195">Work with [MCM support team](http://mcmtechnology.com/support/) to add the users in the MCM platform.</span></span>

> [!NOTE]
> <span data-ttu-id="7a5aa-196">You can use any other MCM user account creation tools or APIs provided by MCM to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-196">You can use any other MCM user account creation tools or APIs provided by MCM to provision AAD user accounts.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7a5aa-197">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7a5aa-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7a5aa-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to MCM.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to MCM.</span></span>

![Assign User][200] 

<span data-ttu-id="7a5aa-200">**To assign Britta Simon to MCM, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7a5aa-200">**To assign Britta Simon to MCM, perform the following steps:**</span></span>

1. <span data-ttu-id="7a5aa-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="7a5aa-203">In the applications list, select **MCM**.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-203">In the applications list, select **MCM**.</span></span>

    ![Configure Single Sign-On](./media/mcm-tutorial/tutorial_mcm_app.png) 

1. <span data-ttu-id="7a5aa-205">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="7a5aa-207">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-207">Click **Add** button.</span></span> <span data-ttu-id="7a5aa-208">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="7a5aa-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="7a5aa-211">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-211">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="7a5aa-212">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7a5aa-213">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="7a5aa-213">Testing single sign-on</span></span>

<span data-ttu-id="7a5aa-214">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-214">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7a5aa-215">When you click the MCM tile in the Access Panel, you should get automatically signed-on to your MCM application.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-215">When you click the MCM tile in the Access Panel, you should get automatically signed-on to your MCM application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7a5aa-216">Additional resources</span><span class="sxs-lookup"><span data-stu-id="7a5aa-216">Additional resources</span></span>

* [<span data-ttu-id="7a5aa-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7a5aa-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="7a5aa-218">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7a5aa-218">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/mcm-tutorial/tutorial_general_01.png
[2]: ./media/mcm-tutorial/tutorial_general_02.png
[3]: ./media/mcm-tutorial/tutorial_general_03.png
[4]: ./media/mcm-tutorial/tutorial_general_04.png

[100]: ./media/mcm-tutorial/tutorial_general_100.png

[200]: ./media/mcm-tutorial/tutorial_general_200.png
[201]: ./media/mcm-tutorial/tutorial_general_201.png
[202]: ./media/mcm-tutorial/tutorial_general_202.png
[203]: ./media/mcm-tutorial/tutorial_general_203.png

