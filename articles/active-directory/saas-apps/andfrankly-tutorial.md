---
title: 'Tutorial: Azure Active Directory integration with &frankly | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and &frankly.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 1d702060-1b89-4e9d-9f01-ede4f1171c73
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 388203903f33d969a7796cf466078159e9b73ad0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870474"
---
# <a name="tutorial-azure-active-directory-integration-with-frankly"></a><span data-ttu-id="d312f-103">Tutorial: Azure Active Directory integration with &frankly</span><span class="sxs-lookup"><span data-stu-id="d312f-103">Tutorial: Azure Active Directory integration with &frankly</span></span>

<span data-ttu-id="d312f-104">In this tutorial, you learn how to integrate &frankly with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d312f-104">In this tutorial, you learn how to integrate &frankly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d312f-105">Integrating &frankly with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="d312f-105">Integrating &frankly with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d312f-106">You can control in Azure AD who has access to &frankly</span><span class="sxs-lookup"><span data-stu-id="d312f-106">You can control in Azure AD who has access to &frankly</span></span>
- <span data-ttu-id="d312f-107">You can enable your users to automatically get signed-on to &frankly (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="d312f-107">You can enable your users to automatically get signed-on to &frankly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d312f-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="d312f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d312f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="d312f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d312f-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d312f-110">Prerequisites</span></span>

<span data-ttu-id="d312f-111">To configure Azure AD integration with &frankly, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="d312f-111">To configure Azure AD integration with &frankly, you need the following items:</span></span>

- <span data-ttu-id="d312f-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="d312f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d312f-113">A &frankly single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="d312f-113">A &frankly single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d312f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="d312f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d312f-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="d312f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d312f-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="d312f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d312f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d312f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d312f-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="d312f-118">Scenario description</span></span>
<span data-ttu-id="d312f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="d312f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d312f-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="d312f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d312f-121">Adding &frankly from the gallery</span><span class="sxs-lookup"><span data-stu-id="d312f-121">Adding &frankly from the gallery</span></span>
2. <span data-ttu-id="d312f-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d312f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-frankly-from-the-gallery"></a><span data-ttu-id="d312f-123">Adding &frankly from the gallery</span><span class="sxs-lookup"><span data-stu-id="d312f-123">Adding &frankly from the gallery</span></span>
<span data-ttu-id="d312f-124">To configure the integration of &frankly into Azure AD, you need to add &frankly from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="d312f-124">To configure the integration of &frankly into Azure AD, you need to add &frankly from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d312f-125">**To add &frankly from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d312f-125">**To add &frankly from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d312f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="d312f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d312f-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="d312f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d312f-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="d312f-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="d312f-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="d312f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="d312f-133">In the search box, type **&frankly**.</span><span class="sxs-lookup"><span data-stu-id="d312f-133">In the search box, type **&frankly**.</span></span>

    ![Creating an Azure AD test user](./media/andfrankly-tutorial/tutorial_andfrankly_search.png)

5. <span data-ttu-id="d312f-135">In the results panel, select **&frankly**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="d312f-135">In the results panel, select **&frankly**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/andfrankly-tutorial/tutorial_andfrankly_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d312f-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d312f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d312f-138">In this section, you configure and test Azure AD single sign-on with &frankly based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="d312f-138">In this section, you configure and test Azure AD single sign-on with &frankly based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d312f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in &frankly is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d312f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in &frankly is to a user in Azure AD.</span></span> <span data-ttu-id="d312f-140">In other words, a link relationship between an Azure AD user and the related user in &frankly needs to be established.</span><span class="sxs-lookup"><span data-stu-id="d312f-140">In other words, a link relationship between an Azure AD user and the related user in &frankly needs to be established.</span></span>

<span data-ttu-id="d312f-141">In &frankly, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="d312f-141">In &frankly, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d312f-142">To configure and test Azure AD single sign-on with &frankly, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="d312f-142">To configure and test Azure AD single sign-on with &frankly, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d312f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="d312f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d312f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d312f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d312f-145">**[Creating a &frankly test user](#creating-a-frankly-test-user)** - to have a counterpart of Britta Simon in &frankly that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="d312f-145">**[Creating a &frankly test user](#creating-a-frankly-test-user)** - to have a counterpart of Britta Simon in &frankly that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d312f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d312f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d312f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="d312f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d312f-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d312f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d312f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your &frankly application.</span><span class="sxs-lookup"><span data-stu-id="d312f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your &frankly application.</span></span>

<span data-ttu-id="d312f-150">**To configure Azure AD single sign-on with &frankly, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d312f-150">**To configure Azure AD single sign-on with &frankly, perform the following steps:**</span></span>

1. <span data-ttu-id="d312f-151">In the Azure portal, on the **&frankly** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="d312f-151">In the Azure portal, on the **&frankly** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="d312f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d312f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/andfrankly-tutorial/tutorial_andfrankly_samlbase.png)

3. <span data-ttu-id="d312f-155">On the **&frankly Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="d312f-155">On the **&frankly Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configure Single Sign-On](./media/andfrankly-tutorial/tutorial_andfrankly_url.png)

    <span data-ttu-id="d312f-157">a.</span><span class="sxs-lookup"><span data-stu-id="d312f-157">a.</span></span> <span data-ttu-id="d312f-158">In the **Identifier** textbox, type a URL using the following pattern: `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/metadata.php/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="d312f-158">In the **Identifier** textbox, type a URL using the following pattern: `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/metadata.php/<tenant id>`</span></span>

    <span data-ttu-id="d312f-159">b.</span><span class="sxs-lookup"><span data-stu-id="d312f-159">b.</span></span> <span data-ttu-id="d312f-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/saml2-acs.php/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="d312f-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/saml2-acs.php/<tenant id>`</span></span>

4. <span data-ttu-id="d312f-161">Check **Show advanced URL settings**.</span><span class="sxs-lookup"><span data-stu-id="d312f-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="d312f-162">If you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="d312f-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configure Single Sign-On](./media/andfrankly-tutorial/tutorial_andfrankly_url1.png)

    <span data-ttu-id="d312f-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://andfrankly.com/saml/okta/?saml_sso=<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="d312f-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://andfrankly.com/saml/okta/?saml_sso=<tenant id>`</span></span>
    > [!NOTE] 
    > <span data-ttu-id="d312f-165">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="d312f-165">These values are not real.</span></span> <span data-ttu-id="d312f-166">Update these values with the actual Identifier, Sign-on, and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="d312f-166">Update these values with the actual Identifier, Sign-on, and Reply URL.</span></span> <span data-ttu-id="d312f-167">Contact [andfrankly support team](mailto:help@andfrankly.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="d312f-167">Contact [andfrankly support team](mailto:help@andfrankly.com) to get these values.</span></span>

5. <span data-ttu-id="d312f-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="d312f-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/andfrankly-tutorial/tutorial_andfrankly_certificate.png) 

6. <span data-ttu-id="d312f-170">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="d312f-170">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/andfrankly-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="d312f-172">To configure single sign-on on **&frankly** side, you need to send the downloaded **Metadata XML** to [andfrankly support team](mailto:help@andfrankly.com).</span><span class="sxs-lookup"><span data-stu-id="d312f-172">To configure single sign-on on **&frankly** side, you need to send the downloaded **Metadata XML** to [andfrankly support team](mailto:help@andfrankly.com).</span></span> 

> [!TIP]
> <span data-ttu-id="d312f-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="d312f-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d312f-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="d312f-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d312f-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d312f-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d312f-176">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d312f-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="d312f-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d312f-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="d312f-179">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d312f-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d312f-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="d312f-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/andfrankly-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d312f-182">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="d312f-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/andfrankly-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d312f-184">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="d312f-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/andfrankly-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d312f-186">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d312f-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/andfrankly-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d312f-188">a.</span><span class="sxs-lookup"><span data-stu-id="d312f-188">a.</span></span> <span data-ttu-id="d312f-189">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d312f-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d312f-190">b.</span><span class="sxs-lookup"><span data-stu-id="d312f-190">b.</span></span> <span data-ttu-id="d312f-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d312f-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d312f-192">c.</span><span class="sxs-lookup"><span data-stu-id="d312f-192">c.</span></span> <span data-ttu-id="d312f-193">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="d312f-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d312f-194">d.</span><span class="sxs-lookup"><span data-stu-id="d312f-194">d.</span></span> <span data-ttu-id="d312f-195">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="d312f-195">Click **Create**.</span></span>
 
### <a name="creating-a-frankly-test-user"></a><span data-ttu-id="d312f-196">Creating a &frankly test user</span><span class="sxs-lookup"><span data-stu-id="d312f-196">Creating a &frankly test user</span></span>

<span data-ttu-id="d312f-197">In this section, you create a user called Britta Simon in &frankly.</span><span class="sxs-lookup"><span data-stu-id="d312f-197">In this section, you create a user called Britta Simon in &frankly.</span></span> <span data-ttu-id="d312f-198">Work with  [andfrankly support team](mailto:help@andfrankly.com) to add the users in the &frankly platform.</span><span class="sxs-lookup"><span data-stu-id="d312f-198">Work with  [andfrankly support team](mailto:help@andfrankly.com) to add the users in the &frankly platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d312f-199">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d312f-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d312f-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to &frankly.</span><span class="sxs-lookup"><span data-stu-id="d312f-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to &frankly.</span></span>

![Assign User][200] 

<span data-ttu-id="d312f-202">**To assign Britta Simon to &frankly, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d312f-202">**To assign Britta Simon to &frankly, perform the following steps:**</span></span>

1. <span data-ttu-id="d312f-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="d312f-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="d312f-205">In the applications list, select **&frankly**.</span><span class="sxs-lookup"><span data-stu-id="d312f-205">In the applications list, select **&frankly**.</span></span>

    ![Configure Single Sign-On](./media/andfrankly-tutorial/tutorial_andfrankly_app.png) 

3. <span data-ttu-id="d312f-207">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="d312f-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="d312f-209">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="d312f-209">Click **Add** button.</span></span> <span data-ttu-id="d312f-210">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="d312f-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="d312f-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="d312f-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d312f-213">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="d312f-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d312f-214">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="d312f-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d312f-215">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="d312f-215">Testing single sign-on</span></span>

<span data-ttu-id="d312f-216">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="d312f-216">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="d312f-217">When you click the &frankly tile in the Access Panel, you should get automatically signed-on to your &frankly application</span><span class="sxs-lookup"><span data-stu-id="d312f-217">When you click the &frankly tile in the Access Panel, you should get automatically signed-on to your &frankly application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d312f-218">Additional resources</span><span class="sxs-lookup"><span data-stu-id="d312f-218">Additional resources</span></span>

* [<span data-ttu-id="d312f-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d312f-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="d312f-220">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d312f-220">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/andfrankly-tutorial/tutorial_general_01.png
[2]: ./media/andfrankly-tutorial/tutorial_general_02.png
[3]: ./media/andfrankly-tutorial/tutorial_general_03.png
[4]: ./media/andfrankly-tutorial/tutorial_general_04.png

[100]: ./media/andfrankly-tutorial/tutorial_general_100.png

[200]: ./media/andfrankly-tutorial/tutorial_general_200.png
[201]: ./media/andfrankly-tutorial/tutorial_general_201.png
[202]: ./media/andfrankly-tutorial/tutorial_general_202.png
[203]: ./media/andfrankly-tutorial/tutorial_general_203.png

