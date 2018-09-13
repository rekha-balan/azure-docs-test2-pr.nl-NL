---
title: 'Tutorial: Azure Active Directory integration with 15Five | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and 15Five.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 2fb301c2-7d7a-4046-8ee1-7dc9e7684806
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 3cc0d9122fd7335bc29c7f35c1163cb39d3481b8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867641"
---
# <a name="tutorial-azure-active-directory-integration-with-15five"></a><span data-ttu-id="73fad-103">Tutorial: Azure Active Directory integration with 15Five</span><span class="sxs-lookup"><span data-stu-id="73fad-103">Tutorial: Azure Active Directory integration with 15Five</span></span>

<span data-ttu-id="73fad-104">In this tutorial, you learn how to integrate 15Five with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="73fad-104">In this tutorial, you learn how to integrate 15Five with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="73fad-105">Integrating 15Five with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="73fad-105">Integrating 15Five with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="73fad-106">You can control in Azure AD who has access to 15Five</span><span class="sxs-lookup"><span data-stu-id="73fad-106">You can control in Azure AD who has access to 15Five</span></span>
- <span data-ttu-id="73fad-107">You can enable your users to automatically get signed-on to 15Five (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="73fad-107">You can enable your users to automatically get signed-on to 15Five (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="73fad-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="73fad-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="73fad-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="73fad-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="73fad-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="73fad-110">Prerequisites</span></span>

<span data-ttu-id="73fad-111">To configure Azure AD integration with 15Five, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="73fad-111">To configure Azure AD integration with 15Five, you need the following items:</span></span>

- <span data-ttu-id="73fad-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="73fad-112">An Azure AD subscription</span></span>
- <span data-ttu-id="73fad-113">A 15Five single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="73fad-113">A 15Five single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="73fad-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="73fad-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="73fad-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="73fad-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="73fad-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="73fad-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="73fad-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="73fad-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="73fad-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="73fad-118">Scenario description</span></span>
<span data-ttu-id="73fad-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="73fad-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="73fad-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="73fad-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="73fad-121">Adding 15Five from the gallery</span><span class="sxs-lookup"><span data-stu-id="73fad-121">Adding 15Five from the gallery</span></span>
2. <span data-ttu-id="73fad-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="73fad-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-15five-from-the-gallery"></a><span data-ttu-id="73fad-123">Adding 15Five from the gallery</span><span class="sxs-lookup"><span data-stu-id="73fad-123">Adding 15Five from the gallery</span></span>
<span data-ttu-id="73fad-124">To configure the integration of 15Five into Azure AD, you need to add 15Five from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="73fad-124">To configure the integration of 15Five into Azure AD, you need to add 15Five from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="73fad-125">**To add 15Five from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="73fad-125">**To add 15Five from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="73fad-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="73fad-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="73fad-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="73fad-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="73fad-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="73fad-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="73fad-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="73fad-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="73fad-133">In the search box, type **15Five**.</span><span class="sxs-lookup"><span data-stu-id="73fad-133">In the search box, type **15Five**.</span></span>

    ![Creating an Azure AD test user](./media/15five-tutorial/tutorial_15five_search.png)

5. <span data-ttu-id="73fad-135">In the results panel, select **15Five**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="73fad-135">In the results panel, select **15Five**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/15five-tutorial/tutorial_15five_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="73fad-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="73fad-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="73fad-138">In this section, you configure and test Azure AD single sign-on with 15Five based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="73fad-138">In this section, you configure and test Azure AD single sign-on with 15Five based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="73fad-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 15Five is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="73fad-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 15Five is to a user in Azure AD.</span></span> <span data-ttu-id="73fad-140">In other words, a link relationship between an Azure AD user and the related user in 15Five needs to be established.</span><span class="sxs-lookup"><span data-stu-id="73fad-140">In other words, a link relationship between an Azure AD user and the related user in 15Five needs to be established.</span></span>

<span data-ttu-id="73fad-141">In 15Five, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="73fad-141">In 15Five, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="73fad-142">To configure and test Azure AD single sign-on with 15Five, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="73fad-142">To configure and test Azure AD single sign-on with 15Five, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="73fad-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="73fad-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="73fad-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="73fad-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="73fad-145">**[Creating a 15Five test user](#creating-a-15five-test-user)** - to have a counterpart of Britta Simon in 15Five that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="73fad-145">**[Creating a 15Five test user](#creating-a-15five-test-user)** - to have a counterpart of Britta Simon in 15Five that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="73fad-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="73fad-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="73fad-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="73fad-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="73fad-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="73fad-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="73fad-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 15Five application.</span><span class="sxs-lookup"><span data-stu-id="73fad-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 15Five application.</span></span>

<span data-ttu-id="73fad-150">**To configure Azure AD single sign-on with 15Five, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="73fad-150">**To configure Azure AD single sign-on with 15Five, perform the following steps:**</span></span>

1. <span data-ttu-id="73fad-151">In the Azure portal, on the **15Five** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="73fad-151">In the Azure portal, on the **15Five** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="73fad-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="73fad-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/15five-tutorial/tutorial_15five_samlbase.png)

3. <span data-ttu-id="73fad-155">On the **15Five Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="73fad-155">On the **15Five Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/15five-tutorial/tutorial_15five_url.png)

    <span data-ttu-id="73fad-157">a.</span><span class="sxs-lookup"><span data-stu-id="73fad-157">a.</span></span> <span data-ttu-id="73fad-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.15five.com`</span><span class="sxs-lookup"><span data-stu-id="73fad-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.15five.com`</span></span>

    <span data-ttu-id="73fad-159">b.</span><span class="sxs-lookup"><span data-stu-id="73fad-159">b.</span></span> <span data-ttu-id="73fad-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.15five.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="73fad-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.15five.com/saml2/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="73fad-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="73fad-161">These values are not real.</span></span> <span data-ttu-id="73fad-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="73fad-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="73fad-163">Contact [15Five Client support team](https://www.15five.com/contact/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="73fad-163">Contact [15Five Client support team](https://www.15five.com/contact/) to get these values.</span></span> 
 
4. <span data-ttu-id="73fad-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="73fad-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/15five-tutorial/tutorial_15five_certificate.png) 

5. <span data-ttu-id="73fad-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="73fad-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/15five-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="73fad-168">To configure single sign-on on **15Five** side, you need to send the downloaded **Metadata XML** to [15Five support team](https://www.15five.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="73fad-168">To configure single sign-on on **15Five** side, you need to send the downloaded **Metadata XML** to [15Five support team](https://www.15five.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="73fad-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="73fad-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="73fad-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="73fad-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="73fad-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="73fad-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="73fad-172">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="73fad-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="73fad-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="73fad-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="73fad-175">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="73fad-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="73fad-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="73fad-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/15five-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="73fad-178">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="73fad-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/15five-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="73fad-180">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="73fad-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/15five-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="73fad-182">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="73fad-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/15five-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="73fad-184">a.</span><span class="sxs-lookup"><span data-stu-id="73fad-184">a.</span></span> <span data-ttu-id="73fad-185">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="73fad-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="73fad-186">b.</span><span class="sxs-lookup"><span data-stu-id="73fad-186">b.</span></span> <span data-ttu-id="73fad-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="73fad-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="73fad-188">c.</span><span class="sxs-lookup"><span data-stu-id="73fad-188">c.</span></span> <span data-ttu-id="73fad-189">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="73fad-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="73fad-190">d.</span><span class="sxs-lookup"><span data-stu-id="73fad-190">d.</span></span> <span data-ttu-id="73fad-191">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="73fad-191">Click **Create**.</span></span>
 
### <a name="creating-a-15five-test-user"></a><span data-ttu-id="73fad-192">Creating a 15Five test user</span><span class="sxs-lookup"><span data-stu-id="73fad-192">Creating a 15Five test user</span></span>

<span data-ttu-id="73fad-193">To enable Azure AD users to log in to 15Five, they must be provisioned into 15Five.</span><span class="sxs-lookup"><span data-stu-id="73fad-193">To enable Azure AD users to log in to 15Five, they must be provisioned into 15Five.</span></span> <span data-ttu-id="73fad-194">When 15Five, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="73fad-194">When 15Five, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="73fad-195">To configure user provisioning, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="73fad-195">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="73fad-196">Log in to your **15Five** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="73fad-196">Log in to your **15Five** company site as administrator.</span></span>

2. <span data-ttu-id="73fad-197">Go to **Manage Company**.</span><span class="sxs-lookup"><span data-stu-id="73fad-197">Go to **Manage Company**.</span></span>
   
    <span data-ttu-id="73fad-198">![Manage Company](./media/15five-tutorial/IC784675.png "Manage Company")</span><span class="sxs-lookup"><span data-stu-id="73fad-198">![Manage Company](./media/15five-tutorial/IC784675.png "Manage Company")</span></span>

3. <span data-ttu-id="73fad-199">Go to **People \> Add People**.</span><span class="sxs-lookup"><span data-stu-id="73fad-199">Go to **People \> Add People**.</span></span>
   
    <span data-ttu-id="73fad-200">![People](./media/15five-tutorial/IC784676.png "People")</span><span class="sxs-lookup"><span data-stu-id="73fad-200">![People](./media/15five-tutorial/IC784676.png "People")</span></span>

4. <span data-ttu-id="73fad-201">In the Add New Person section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="73fad-201">In the Add New Person section, perform the following steps:</span></span>
   
    <span data-ttu-id="73fad-202">![Add New Person](./media/15five-tutorial/IC784677.png "Add New Person")</span><span class="sxs-lookup"><span data-stu-id="73fad-202">![Add New Person](./media/15five-tutorial/IC784677.png "Add New Person")</span></span>
   
    <span data-ttu-id="73fad-203">a.</span><span class="sxs-lookup"><span data-stu-id="73fad-203">a.</span></span> <span data-ttu-id="73fad-204">Type the **First Name**, **Last Name**, **Title**, **Email address** of a valid Azure Active Directory account you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="73fad-204">Type the **First Name**, **Last Name**, **Title**, **Email address** of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>

    <span data-ttu-id="73fad-205">b.</span><span class="sxs-lookup"><span data-stu-id="73fad-205">b.</span></span> <span data-ttu-id="73fad-206">Click **Done**.</span><span class="sxs-lookup"><span data-stu-id="73fad-206">Click **Done**.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="73fad-207">The Azure AD account holder receives an email including a link to confirm the account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="73fad-207">The Azure AD account holder receives an email including a link to confirm the account before it becomes active.</span></span>
   
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="73fad-208">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="73fad-208">Assigning the Azure AD test user</span></span>

<span data-ttu-id="73fad-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 15Five.</span><span class="sxs-lookup"><span data-stu-id="73fad-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 15Five.</span></span>

![Assign User][200] 

<span data-ttu-id="73fad-211">**To assign Britta Simon to 15Five, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="73fad-211">**To assign Britta Simon to 15Five, perform the following steps:**</span></span>

1. <span data-ttu-id="73fad-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="73fad-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="73fad-214">In the applications list, select **15Five**.</span><span class="sxs-lookup"><span data-stu-id="73fad-214">In the applications list, select **15Five**.</span></span>

    ![Configure Single Sign-On](./media/15five-tutorial/tutorial_15five_app.png) 

3. <span data-ttu-id="73fad-216">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="73fad-216">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="73fad-218">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="73fad-218">Click **Add** button.</span></span> <span data-ttu-id="73fad-219">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="73fad-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="73fad-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="73fad-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="73fad-222">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="73fad-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="73fad-223">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="73fad-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="73fad-224">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="73fad-224">Testing single sign-on</span></span>

<span data-ttu-id="73fad-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="73fad-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="73fad-226">When you click the 15Five tile in the Access Panel, you should get login page of 15Five application.</span><span class="sxs-lookup"><span data-stu-id="73fad-226">When you click the 15Five tile in the Access Panel, you should get login page of 15Five application.</span></span>
<span data-ttu-id="73fad-227">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="73fad-227">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="73fad-228">Additional resources</span><span class="sxs-lookup"><span data-stu-id="73fad-228">Additional resources</span></span>

* [<span data-ttu-id="73fad-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="73fad-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="73fad-230">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="73fad-230">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/15five-tutorial/tutorial_general_01.png
[2]: ./media/15five-tutorial/tutorial_general_02.png
[3]: ./media/15five-tutorial/tutorial_general_03.png
[4]: ./media/15five-tutorial/tutorial_general_04.png

[100]: ./media/15five-tutorial/tutorial_general_100.png

[200]: ./media/15five-tutorial/tutorial_general_200.png
[201]: ./media/15five-tutorial/tutorial_general_201.png
[202]: ./media/15five-tutorial/tutorial_general_202.png
[203]: ./media/15five-tutorial/tutorial_general_203.png

