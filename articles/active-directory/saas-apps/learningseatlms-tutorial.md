---
title: 'Tutorial: Azure Active Directory integration with Learning Seat LMS  | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Learning Seat LMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: bb056fcf-4135-478e-85b1-5015d1f07b85
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: jeedes
ms.openlocfilehash: 1043c8f7468fd7775ff1e38d12a3dce0b379c915
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867456"
---
# <a name="tutorial-azure-active-directory-integration-with-learning-seat-lms"></a><span data-ttu-id="65f0b-103">Tutorial: Azure Active Directory integration with Learning Seat LMS</span><span class="sxs-lookup"><span data-stu-id="65f0b-103">Tutorial: Azure Active Directory integration with Learning Seat LMS</span></span>

<span data-ttu-id="65f0b-104">In this tutorial, you learn how to integrate Learning Seat LMS with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="65f0b-104">In this tutorial, you learn how to integrate Learning Seat LMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="65f0b-105">Integrating Learning Seat LMS with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="65f0b-105">Integrating Learning Seat LMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="65f0b-106">You can control in Azure AD who has access to Learning Seat LMS</span><span class="sxs-lookup"><span data-stu-id="65f0b-106">You can control in Azure AD who has access to Learning Seat LMS</span></span>
- <span data-ttu-id="65f0b-107">You can enable your users to automatically get signed-on to Learning Seat LMS (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="65f0b-107">You can enable your users to automatically get signed-on to Learning Seat LMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="65f0b-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="65f0b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="65f0b-109">If you want to know more details about SaaS app integration with Azure AD, see.</span><span class="sxs-lookup"><span data-stu-id="65f0b-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="65f0b-110">[What is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="65f0b-110">[What is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65f0b-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="65f0b-111">Prerequisites</span></span>

<span data-ttu-id="65f0b-112">To configure Azure AD integration with Learning Seat LMS, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="65f0b-112">To configure Azure AD integration with Learning Seat LMS, you need the following items:</span></span>

- <span data-ttu-id="65f0b-113">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="65f0b-113">An Azure AD subscription</span></span>
- <span data-ttu-id="65f0b-114">A Learning Seat LMS single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="65f0b-114">A Learning Seat LMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="65f0b-115">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="65f0b-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="65f0b-116">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="65f0b-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="65f0b-117">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="65f0b-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="65f0b-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="65f0b-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="65f0b-119">Scenario description</span><span class="sxs-lookup"><span data-stu-id="65f0b-119">Scenario description</span></span>
<span data-ttu-id="65f0b-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="65f0b-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="65f0b-121">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="65f0b-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="65f0b-122">Adding Learning Seat LMS from the gallery</span><span class="sxs-lookup"><span data-stu-id="65f0b-122">Adding Learning Seat LMS from the gallery</span></span>
1. <span data-ttu-id="65f0b-123">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="65f0b-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learning-seat-lms-from-the-gallery"></a><span data-ttu-id="65f0b-124">Adding Learning Seat LMS from the gallery</span><span class="sxs-lookup"><span data-stu-id="65f0b-124">Adding Learning Seat LMS from the gallery</span></span>
<span data-ttu-id="65f0b-125">To configure the integration of Learning Seat LMS into Azure AD, you need to add Learning Seat LMS from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="65f0b-125">To configure the integration of Learning Seat LMS into Azure AD, you need to add Learning Seat LMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="65f0b-126">**To add Learning Seat LMS from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="65f0b-126">**To add Learning Seat LMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="65f0b-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="65f0b-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="65f0b-129">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="65f0b-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="65f0b-130">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="65f0b-130">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="65f0b-132">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="65f0b-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="65f0b-134">In the search box, type **Learning Seat LMS**.</span><span class="sxs-lookup"><span data-stu-id="65f0b-134">In the search box, type **Learning Seat LMS**.</span></span>

    ![Creating an Azure AD test user](./media/learningseatlms-tutorial/tutorial_learnconnect_search.png)

1. <span data-ttu-id="65f0b-136">In the results panel, select **Learning Seat LMS**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="65f0b-136">In the results panel, select **Learning Seat LMS**, and then click **Add** button to add the application.</span></span>


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="65f0b-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="65f0b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="65f0b-138">In this section, you configure and test Azure AD single sign-on with Learning Seat LMS based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="65f0b-138">In this section, you configure and test Azure AD single sign-on with Learning Seat LMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="65f0b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Learning Seat LMS is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65f0b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Learning Seat LMS is to a user in Azure AD.</span></span> <span data-ttu-id="65f0b-140">In other words, a link relationship between an Azure AD user and the related user in Learning Seat LMS needs to be established.</span><span class="sxs-lookup"><span data-stu-id="65f0b-140">In other words, a link relationship between an Azure AD user and the related user in Learning Seat LMS needs to be established.</span></span>

<span data-ttu-id="65f0b-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="65f0b-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Learning Seat LMS.</span></span>

<span data-ttu-id="65f0b-142">To configure and test Azure AD single sign-on with Learning Seat LMS, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="65f0b-142">To configure and test Azure AD single sign-on with Learning Seat LMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="65f0b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="65f0b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="65f0b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="65f0b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="65f0b-145">**[Creating a Learning Seat LMS test user](#creating-a-learnconnect-test-user)** - to have a counterpart of Britta Simon in Learning Seat LMS that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="65f0b-145">**[Creating a Learning Seat LMS test user](#creating-a-learnconnect-test-user)** - to have a counterpart of Britta Simon in Learning Seat LMS that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="65f0b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="65f0b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="65f0b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="65f0b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="65f0b-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="65f0b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="65f0b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Learning Seat LMS application.</span><span class="sxs-lookup"><span data-stu-id="65f0b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Learning Seat LMS application.</span></span>

<span data-ttu-id="65f0b-150">**To configure Azure AD single sign-on with Learning Seat LMS, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="65f0b-150">**To configure Azure AD single sign-on with Learning Seat LMS, perform the following steps:**</span></span>

1. <span data-ttu-id="65f0b-151">In the Azure portal, on the **Learning Seat LMS** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="65f0b-151">In the Azure portal, on the **Learning Seat LMS** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="65f0b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="65f0b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/learningseatlms-tutorial/tutorial_learnconnect_samlbase.png)

1. <span data-ttu-id="65f0b-155">On the **Learning Seat LMS Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="65f0b-155">On the **Learning Seat LMS Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configure Single Sign-On](./media/learningseatlms-tutorial/tutorial_learnconnect_url.png)

    <span data-ttu-id="65f0b-157">a.</span><span class="sxs-lookup"><span data-stu-id="65f0b-157">a.</span></span> <span data-ttu-id="65f0b-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.learningseatlms.com`</span><span class="sxs-lookup"><span data-stu-id="65f0b-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.learningseatlms.com`</span></span>

    <span data-ttu-id="65f0b-159">b.</span><span class="sxs-lookup"><span data-stu-id="65f0b-159">b.</span></span> <span data-ttu-id="65f0b-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.learningseatlms.com/Account/AssertionConsumerService`</span><span class="sxs-lookup"><span data-stu-id="65f0b-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.learningseatlms.com/Account/AssertionConsumerService`</span></span>

1. <span data-ttu-id="65f0b-161">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="65f0b-161">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configure Single Sign-On](./media/learningseatlms-tutorial/tutorial_learnconnect_url2.png)

    <span data-ttu-id="65f0b-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.learningseatlms.com`</span><span class="sxs-lookup"><span data-stu-id="65f0b-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.learningseatlms.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="65f0b-164">These values are not the real values.</span><span class="sxs-lookup"><span data-stu-id="65f0b-164">These values are not the real values.</span></span> <span data-ttu-id="65f0b-165">Update these values with the actual Identifier, Reply URL and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="65f0b-165">Update these values with the actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="65f0b-166">Contact [Learning Seat support team](http://help.learningseatlms.com/help) to get these values.</span><span class="sxs-lookup"><span data-stu-id="65f0b-166">Contact [Learning Seat support team](http://help.learningseatlms.com/help) to get these values.</span></span> 

1. <span data-ttu-id="65f0b-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="65f0b-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/learningseatlms-tutorial/tutorial_learnconnect_certificate.png) 

1. <span data-ttu-id="65f0b-169">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="65f0b-169">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/learningseatlms-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="65f0b-171">To configure single sign-on on **Learning Seat LMS** side, you need to send the downloaded **Metadata XML** to [Learning Seat support team](http://help.learningseatlms.com/help).</span><span class="sxs-lookup"><span data-stu-id="65f0b-171">To configure single sign-on on **Learning Seat LMS** side, you need to send the downloaded **Metadata XML** to [Learning Seat support team](http://help.learningseatlms.com/help).</span></span>

> [!TIP]
> <span data-ttu-id="65f0b-172">You can now read a concise version of these instructions inside the [Azure  portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="65f0b-172">You can now read a concise version of these instructions inside the [Azure  portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="65f0b-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="65f0b-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="65f0b-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="65f0b-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="65f0b-175">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="65f0b-175">Creating an Azure AD test user</span></span>

<span data-ttu-id="65f0b-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="65f0b-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="65f0b-178">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="65f0b-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="65f0b-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="65f0b-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/learningseatlms-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="65f0b-181">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="65f0b-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/learningseatlms-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="65f0b-183">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="65f0b-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/learningseatlms-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="65f0b-185">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="65f0b-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/learningseatlms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="65f0b-187">a.</span><span class="sxs-lookup"><span data-stu-id="65f0b-187">a.</span></span> <span data-ttu-id="65f0b-188">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="65f0b-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="65f0b-189">b.</span><span class="sxs-lookup"><span data-stu-id="65f0b-189">b.</span></span> <span data-ttu-id="65f0b-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="65f0b-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="65f0b-191">c.</span><span class="sxs-lookup"><span data-stu-id="65f0b-191">c.</span></span> <span data-ttu-id="65f0b-192">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="65f0b-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="65f0b-193">d.</span><span class="sxs-lookup"><span data-stu-id="65f0b-193">d.</span></span> <span data-ttu-id="65f0b-194">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="65f0b-194">Click **Create**.</span></span>
 
### <a name="creating-a-learning-seat-lms-test-user"></a><span data-ttu-id="65f0b-195">Creating a Learning Seat LMS test user</span><span class="sxs-lookup"><span data-stu-id="65f0b-195">Creating a Learning Seat LMS test user</span></span>

<span data-ttu-id="65f0b-196">In this section, you create a user called Britta Simon in Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="65f0b-196">In this section, you create a user called Britta Simon in Learning Seat LMS.</span></span> <span data-ttu-id="65f0b-197">Contact [Learning Seat support team](http://help.learningseatlms.com/help) with all the user information to add the users in the Learning Seat LMS application.</span><span class="sxs-lookup"><span data-stu-id="65f0b-197">Contact [Learning Seat support team](http://help.learningseatlms.com/help) with all the user information to add the users in the Learning Seat LMS application.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="65f0b-198">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="65f0b-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="65f0b-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="65f0b-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Learning Seat LMS.</span></span>

![Assign User][200] 

<span data-ttu-id="65f0b-201">**To assign Britta Simon to Learning Seat LMS, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="65f0b-201">**To assign Britta Simon to Learning Seat LMS, perform the following steps:**</span></span>

1. <span data-ttu-id="65f0b-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="65f0b-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="65f0b-204">In the applications list, select **Learning Seat LMS**.</span><span class="sxs-lookup"><span data-stu-id="65f0b-204">In the applications list, select **Learning Seat LMS**.</span></span>

    ![Configure Single Sign-On](./media/learningseatlms-tutorial/tutorial_learnconnect_app.png) 

1. <span data-ttu-id="65f0b-206">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="65f0b-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="65f0b-208">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="65f0b-208">Click **Add** button.</span></span> <span data-ttu-id="65f0b-209">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="65f0b-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="65f0b-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="65f0b-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="65f0b-212">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="65f0b-212">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="65f0b-213">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="65f0b-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="65f0b-214">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="65f0b-214">Testing single sign-on</span></span>

<span data-ttu-id="65f0b-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="65f0b-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span> 

<span data-ttu-id="65f0b-216">Click the Learning Seat LMS tile in the Access Panel, you will be automatically signed-on to your Learning Seat LMS application.</span><span class="sxs-lookup"><span data-stu-id="65f0b-216">Click the Learning Seat LMS tile in the Access Panel, you will be automatically signed-on to your Learning Seat LMS application.</span></span> <span data-ttu-id="65f0b-217">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="65f0b-217">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="65f0b-218">Additional resources</span><span class="sxs-lookup"><span data-stu-id="65f0b-218">Additional resources</span></span>

* [<span data-ttu-id="65f0b-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="65f0b-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="65f0b-220">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="65f0b-220">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/learnconnect-tutorial/tutorial_general_01.png
[2]: ./media/learnconnect-tutorial/tutorial_general_02.png
[3]: ./media/learnconnect-tutorial/tutorial_general_03.png
[4]: ./media/learnconnect-tutorial/tutorial_general_04.png

[100]: ./media/learnconnect-tutorial/tutorial_general_100.png

[200]: ./media/learnconnect-tutorial/tutorial_general_200.png
[201]: ./media/learnconnect-tutorial/tutorial_general_201.png
[202]: ./media/learnconnect-tutorial/tutorial_general_202.png
[203]: ./media/learnconnect-tutorial/tutorial_general_203.png

