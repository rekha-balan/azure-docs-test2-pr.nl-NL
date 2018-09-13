---
title: 'Tutorial: Azure Active Directory integration with People | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and People.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7c9b6202-11dd-4bb6-a679-8fb0a7a0ef4e
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: jeedes
ms.openlocfilehash: eac41b0c3def42f2417e7c033c645d8785a5f08b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857079"
---
# <a name="tutorial-azure-active-directory-integration-with-people"></a><span data-ttu-id="41b48-103">Tutorial: Azure Active Directory integration with People</span><span class="sxs-lookup"><span data-stu-id="41b48-103">Tutorial: Azure Active Directory integration with People</span></span>

<span data-ttu-id="41b48-104">In this tutorial, you learn how to integrate People with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="41b48-104">In this tutorial, you learn how to integrate People with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="41b48-105">Integrating People with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="41b48-105">Integrating People with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="41b48-106">You can control in Azure AD who has access to People</span><span class="sxs-lookup"><span data-stu-id="41b48-106">You can control in Azure AD who has access to People</span></span>
- <span data-ttu-id="41b48-107">You can enable your users to automatically get signed-on to People (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="41b48-107">You can enable your users to automatically get signed-on to People (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="41b48-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="41b48-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="41b48-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="41b48-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41b48-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="41b48-110">Prerequisites</span></span>

<span data-ttu-id="41b48-111">To configure Azure AD integration with People, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="41b48-111">To configure Azure AD integration with People, you need the following items:</span></span>

- <span data-ttu-id="41b48-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="41b48-112">An Azure AD subscription</span></span>
- <span data-ttu-id="41b48-113">A People single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="41b48-113">A People single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="41b48-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="41b48-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="41b48-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="41b48-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="41b48-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="41b48-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="41b48-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="41b48-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="41b48-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="41b48-118">Scenario description</span></span>
<span data-ttu-id="41b48-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="41b48-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="41b48-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="41b48-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="41b48-121">Adding People from the gallery</span><span class="sxs-lookup"><span data-stu-id="41b48-121">Adding People from the gallery</span></span>
1. <span data-ttu-id="41b48-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="41b48-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-people-from-the-gallery"></a><span data-ttu-id="41b48-123">Adding People from the gallery</span><span class="sxs-lookup"><span data-stu-id="41b48-123">Adding People from the gallery</span></span>
<span data-ttu-id="41b48-124">To configure the integration of People into Azure AD, you need to add People from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="41b48-124">To configure the integration of People into Azure AD, you need to add People from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="41b48-125">**To add People from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="41b48-125">**To add People from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="41b48-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="41b48-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="41b48-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="41b48-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="41b48-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="41b48-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="41b48-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="41b48-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="41b48-133">In the search box, type **People**.</span><span class="sxs-lookup"><span data-stu-id="41b48-133">In the search box, type **People**.</span></span>

    ![Creating an Azure AD test user](./media/people-tutorial/tutorial_people_search.png)

1. <span data-ttu-id="41b48-135">In the results panel, select **People**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="41b48-135">In the results panel, select **People**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/people-tutorial/tutorial_people_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="41b48-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="41b48-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="41b48-138">In this section, you configure and test Azure AD single sign-on with People based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="41b48-138">In this section, you configure and test Azure AD single sign-on with People based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="41b48-139">For single sign-on to work, Azure AD needs to know what the counterpart user in People is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="41b48-139">For single sign-on to work, Azure AD needs to know what the counterpart user in People is to a user in Azure AD.</span></span> <span data-ttu-id="41b48-140">In other words, a link relationship between an Azure AD user and the related user in People needs to be established.</span><span class="sxs-lookup"><span data-stu-id="41b48-140">In other words, a link relationship between an Azure AD user and the related user in People needs to be established.</span></span>

<span data-ttu-id="41b48-141">In People, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="41b48-141">In People, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="41b48-142">To configure and test Azure AD single sign-on with People, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="41b48-142">To configure and test Azure AD single sign-on with People, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="41b48-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="41b48-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="41b48-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="41b48-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="41b48-145">**[Creating a People test user](#creating-a-people-test-user)** - to have a counterpart of Britta Simon in People that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="41b48-145">**[Creating a People test user](#creating-a-people-test-user)** - to have a counterpart of Britta Simon in People that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="41b48-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="41b48-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="41b48-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="41b48-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="41b48-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="41b48-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="41b48-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your People application.</span><span class="sxs-lookup"><span data-stu-id="41b48-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your People application.</span></span>

<span data-ttu-id="41b48-150">**To configure Azure AD single sign-on with People, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="41b48-150">**To configure Azure AD single sign-on with People, perform the following steps:**</span></span>

1. <span data-ttu-id="41b48-151">In the Azure portal, on the **People** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="41b48-151">In the Azure portal, on the **People** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="41b48-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="41b48-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/people-tutorial/tutorial_people_samlbase.png)

1. <span data-ttu-id="41b48-155">On the **People Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="41b48-155">On the **People Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/people-tutorial/tutorial_people_url.png)

    <span data-ttu-id="41b48-157">a.</span><span class="sxs-lookup"><span data-stu-id="41b48-157">a.</span></span> <span data-ttu-id="41b48-158">In the **Sign-on URL** textbox, type a URL using the following pattern:  `https://<company name>.peoplehr.net`</span><span class="sxs-lookup"><span data-stu-id="41b48-158">In the **Sign-on URL** textbox, type a URL using the following pattern:  `https://<company name>.peoplehr.net`</span></span>

    <span data-ttu-id="41b48-159">b.</span><span class="sxs-lookup"><span data-stu-id="41b48-159">b.</span></span> <span data-ttu-id="41b48-160">In the **Identifier** textbox, type the URL: `https://www.peoplehr.com`</span><span class="sxs-lookup"><span data-stu-id="41b48-160">In the **Identifier** textbox, type the URL: `https://www.peoplehr.com`</span></span>

    <span data-ttu-id="41b48-161">c.</span><span class="sxs-lookup"><span data-stu-id="41b48-161">c.</span></span> <span data-ttu-id="41b48-162">In the **Reply URL** textbox, type a URL using the following pattern:  `https://<company name>.peoplehr.net/Pages/Saml/ConsumeAzureAD.aspx`</span><span class="sxs-lookup"><span data-stu-id="41b48-162">In the **Reply URL** textbox, type a URL using the following pattern:  `https://<company name>.peoplehr.net/Pages/Saml/ConsumeAzureAD.aspx`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="41b48-163">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="41b48-163">These values are not real.</span></span> <span data-ttu-id="41b48-164">Update these values with the actual Reply URL and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="41b48-164">Update these values with the actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="41b48-165">Contact [People Client support team](mailto:customerservices@peoplehr.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="41b48-165">Contact [People Client support team](mailto:customerservices@peoplehr.com) to get these values.</span></span> 

1. <span data-ttu-id="41b48-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="41b48-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/people-tutorial/tutorial_people_certificate.png) 

1. <span data-ttu-id="41b48-168">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="41b48-168">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/people-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="41b48-170">To get SSO configured for your application, you need to sign-on to your People tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="41b48-170">To get SSO configured for your application, you need to sign-on to your People tenant as an administrator.</span></span>
   
1. <span data-ttu-id="41b48-171">In the menu on the left side, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="41b48-171">In the menu on the left side, click **Settings**.</span></span>

    ![Configure Single Sign-On](./media/people-tutorial/tutorial_people_001.png)

1. <span data-ttu-id="41b48-173">Click **Company**.</span><span class="sxs-lookup"><span data-stu-id="41b48-173">Click **Company**.</span></span>

    ![Configure Single Sign-On](./media/people-tutorial/tutorial_people_002.png)

1. <span data-ttu-id="41b48-175">On the **Upload 'Single Sign On' SAML meta-data file**, click **Browse** to upload the downloaded metadata file.</span><span class="sxs-lookup"><span data-stu-id="41b48-175">On the **Upload 'Single Sign On' SAML meta-data file**, click **Browse** to upload the downloaded metadata file.</span></span>

    ![Configure Single Sign-On](./media/people-tutorial/tutorial_people_003.png)

> [!TIP]
> <span data-ttu-id="41b48-177">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="41b48-177">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="41b48-178">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="41b48-178">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="41b48-179">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="41b48-179">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="41b48-180">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="41b48-180">Creating an Azure AD test user</span></span>
<span data-ttu-id="41b48-181">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="41b48-181">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="41b48-183">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="41b48-183">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="41b48-184">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="41b48-184">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/people-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="41b48-186">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="41b48-186">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/people-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="41b48-188">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="41b48-188">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/people-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="41b48-190">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="41b48-190">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/people-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="41b48-192">a.</span><span class="sxs-lookup"><span data-stu-id="41b48-192">a.</span></span> <span data-ttu-id="41b48-193">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="41b48-193">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="41b48-194">b.</span><span class="sxs-lookup"><span data-stu-id="41b48-194">b.</span></span> <span data-ttu-id="41b48-195">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="41b48-195">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="41b48-196">c.</span><span class="sxs-lookup"><span data-stu-id="41b48-196">c.</span></span> <span data-ttu-id="41b48-197">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="41b48-197">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="41b48-198">d.</span><span class="sxs-lookup"><span data-stu-id="41b48-198">d.</span></span> <span data-ttu-id="41b48-199">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="41b48-199">Click **Create**.</span></span>
 
### <a name="creating-a-people-test-user"></a><span data-ttu-id="41b48-200">Creating a People test user</span><span class="sxs-lookup"><span data-stu-id="41b48-200">Creating a People test user</span></span>

<span data-ttu-id="41b48-201">In this section, you create a user called Britta Simon in People.</span><span class="sxs-lookup"><span data-stu-id="41b48-201">In this section, you create a user called Britta Simon in People.</span></span> <span data-ttu-id="41b48-202">Work with [People Client support team](mailto:customerservices@peoplehr.com) to add the users in the People platform.</span><span class="sxs-lookup"><span data-stu-id="41b48-202">Work with [People Client support team](mailto:customerservices@peoplehr.com) to add the users in the People platform.</span></span> <span data-ttu-id="41b48-203">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="41b48-203">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="41b48-204">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="41b48-204">Assigning the Azure AD test user</span></span>

<span data-ttu-id="41b48-205">In this section, you enable Britta Simon to use Azure single sign-on by granting access to People.</span><span class="sxs-lookup"><span data-stu-id="41b48-205">In this section, you enable Britta Simon to use Azure single sign-on by granting access to People.</span></span>

![Assign User][200] 

<span data-ttu-id="41b48-207">**To assign Britta Simon to People, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="41b48-207">**To assign Britta Simon to People, perform the following steps:**</span></span>

1. <span data-ttu-id="41b48-208">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="41b48-208">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="41b48-210">In the applications list, select **People**.</span><span class="sxs-lookup"><span data-stu-id="41b48-210">In the applications list, select **People**.</span></span>

    ![Configure Single Sign-On](./media/people-tutorial/tutorial_people_app.png) 

1. <span data-ttu-id="41b48-212">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="41b48-212">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="41b48-214">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="41b48-214">Click **Add** button.</span></span> <span data-ttu-id="41b48-215">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="41b48-215">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="41b48-217">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="41b48-217">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="41b48-218">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="41b48-218">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="41b48-219">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="41b48-219">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="41b48-220">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="41b48-220">Testing single sign-on</span></span>

<span data-ttu-id="41b48-221">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="41b48-221">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="41b48-222">When you click the People tile in the Access Panel, you should get automatically signed-on to your People application.</span><span class="sxs-lookup"><span data-stu-id="41b48-222">When you click the People tile in the Access Panel, you should get automatically signed-on to your People application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="41b48-223">Additional resources</span><span class="sxs-lookup"><span data-stu-id="41b48-223">Additional resources</span></span>

* [<span data-ttu-id="41b48-224">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="41b48-224">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="41b48-225">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="41b48-225">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/people-tutorial/tutorial_general_01.png
[2]: ./media/people-tutorial/tutorial_general_02.png
[3]: ./media/people-tutorial/tutorial_general_03.png
[4]: ./media/people-tutorial/tutorial_general_04.png

[100]: ./media/people-tutorial/tutorial_general_100.png

[200]: ./media/people-tutorial/tutorial_general_200.png
[201]: ./media/people-tutorial/tutorial_general_201.png
[202]: ./media/people-tutorial/tutorial_general_202.png
[203]: ./media/people-tutorial/tutorial_general_203.png

