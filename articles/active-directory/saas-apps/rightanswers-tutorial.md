---
title: 'Tutorial: Azure Active Directory integration with RightAnswers | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and RightAnswers.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 7f09e25a-a716-41e1-8ca3-fd00e3d1b8cc
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: fc589554b6ce2bb3d6aa1f52d9eb697c211d2a88
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867967"
---
# <a name="tutorial-azure-active-directory-integration-with-rightanswers"></a><span data-ttu-id="bdc59-103">Tutorial: Azure Active Directory integration with RightAnswers</span><span class="sxs-lookup"><span data-stu-id="bdc59-103">Tutorial: Azure Active Directory integration with RightAnswers</span></span>

<span data-ttu-id="bdc59-104">In this tutorial, you learn how to integrate RightAnswers with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bdc59-104">In this tutorial, you learn how to integrate RightAnswers with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bdc59-105">Integrating RightAnswers with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="bdc59-105">Integrating RightAnswers with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bdc59-106">You can control in Azure AD who has access to RightAnswers</span><span class="sxs-lookup"><span data-stu-id="bdc59-106">You can control in Azure AD who has access to RightAnswers</span></span>
- <span data-ttu-id="bdc59-107">You can enable your users to automatically get signed-on to RightAnswers (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="bdc59-107">You can enable your users to automatically get signed-on to RightAnswers (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bdc59-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="bdc59-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="bdc59-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="bdc59-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bdc59-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bdc59-110">Prerequisites</span></span>

<span data-ttu-id="bdc59-111">To configure Azure AD integration with RightAnswers, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="bdc59-111">To configure Azure AD integration with RightAnswers, you need the following items:</span></span>

- <span data-ttu-id="bdc59-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="bdc59-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bdc59-113">A RightAnswers single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="bdc59-113">A RightAnswers single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bdc59-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="bdc59-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bdc59-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="bdc59-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bdc59-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="bdc59-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bdc59-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bdc59-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bdc59-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="bdc59-118">Scenario description</span></span>
<span data-ttu-id="bdc59-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="bdc59-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bdc59-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="bdc59-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bdc59-121">Adding RightAnswers from the gallery</span><span class="sxs-lookup"><span data-stu-id="bdc59-121">Adding RightAnswers from the gallery</span></span>
1. <span data-ttu-id="bdc59-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="bdc59-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rightanswers-from-the-gallery"></a><span data-ttu-id="bdc59-123">Adding RightAnswers from the gallery</span><span class="sxs-lookup"><span data-stu-id="bdc59-123">Adding RightAnswers from the gallery</span></span>
<span data-ttu-id="bdc59-124">To configure the integration of RightAnswers into Azure AD, you need to add RightAnswers from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="bdc59-124">To configure the integration of RightAnswers into Azure AD, you need to add RightAnswers from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bdc59-125">**To add RightAnswers from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bdc59-125">**To add RightAnswers from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bdc59-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="bdc59-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="bdc59-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="bdc59-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bdc59-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="bdc59-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="bdc59-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="bdc59-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="bdc59-133">In the search box, type **RightAnswers**.</span><span class="sxs-lookup"><span data-stu-id="bdc59-133">In the search box, type **RightAnswers**.</span></span>

    ![Creating an Azure AD test user](./media/rightanswers-tutorial/tutorial_rightanswers_search.png)

1. <span data-ttu-id="bdc59-135">In the results panel, select **RightAnswers**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="bdc59-135">In the results panel, select **RightAnswers**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/rightanswers-tutorial/tutorial_rightanswers_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bdc59-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="bdc59-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bdc59-138">In this section, you configure and test Azure AD single sign-on with RightAnswers based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="bdc59-138">In this section, you configure and test Azure AD single sign-on with RightAnswers based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bdc59-139">For single sign-on to work, Azure AD needs to know what the counterpart user in RightAnswers is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bdc59-139">For single sign-on to work, Azure AD needs to know what the counterpart user in RightAnswers is to a user in Azure AD.</span></span> <span data-ttu-id="bdc59-140">In other words, a link relationship between an Azure AD user and the related user in RightAnswers needs to be established.</span><span class="sxs-lookup"><span data-stu-id="bdc59-140">In other words, a link relationship between an Azure AD user and the related user in RightAnswers needs to be established.</span></span>

<span data-ttu-id="bdc59-141">In RightAnswers, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="bdc59-141">In RightAnswers, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="bdc59-142">To configure and test Azure AD single sign-on with RightAnswers, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="bdc59-142">To configure and test Azure AD single sign-on with RightAnswers, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bdc59-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="bdc59-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="bdc59-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bdc59-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="bdc59-145">**[Creating a RightAnswers test user](#creating-a-rightanswers-test-user)** - to have a counterpart of Britta Simon in RightAnswers that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="bdc59-145">**[Creating a RightAnswers test user](#creating-a-rightanswers-test-user)** - to have a counterpart of Britta Simon in RightAnswers that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="bdc59-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="bdc59-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="bdc59-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="bdc59-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bdc59-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="bdc59-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bdc59-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RightAnswers application.</span><span class="sxs-lookup"><span data-stu-id="bdc59-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RightAnswers application.</span></span>

<span data-ttu-id="bdc59-150">**To configure Azure AD single sign-on with RightAnswers, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bdc59-150">**To configure Azure AD single sign-on with RightAnswers, perform the following steps:**</span></span>

1. <span data-ttu-id="bdc59-151">In the Azure portal, on the **RightAnswers** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="bdc59-151">In the Azure portal, on the **RightAnswers** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="bdc59-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="bdc59-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/rightanswers-tutorial/tutorial_rightanswers_samlbase.png)

1. <span data-ttu-id="bdc59-155">On the **RightAnswers Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="bdc59-155">On the **RightAnswers Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/rightanswers-tutorial/tutorial_rightanswers_url.png)

    <span data-ttu-id="bdc59-157">a.</span><span class="sxs-lookup"><span data-stu-id="bdc59-157">a.</span></span> <span data-ttu-id="bdc59-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.rightanswers.com/portal/ss/`</span><span class="sxs-lookup"><span data-stu-id="bdc59-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.rightanswers.com/portal/ss/`</span></span>

    <span data-ttu-id="bdc59-159">b.</span><span class="sxs-lookup"><span data-stu-id="bdc59-159">b.</span></span> <span data-ttu-id="bdc59-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.rightanswers.com:<identifier>/portal`</span><span class="sxs-lookup"><span data-stu-id="bdc59-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.rightanswers.com:<identifier>/portal`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bdc59-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="bdc59-161">These values are not real.</span></span> <span data-ttu-id="bdc59-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="bdc59-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="bdc59-163">Contact [RightAnswers Client support team](https://www.rightanswers.com/contact-us/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="bdc59-163">Contact [RightAnswers Client support team](https://www.rightanswers.com/contact-us/) to get these values.</span></span> 
 
1. <span data-ttu-id="bdc59-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="bdc59-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/rightanswers-tutorial/tutorial_rightanswers_certificate.png) 

1. <span data-ttu-id="bdc59-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="bdc59-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/rightanswers-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="bdc59-168">To configure single sign-on on **RightAnswers** side, you need to send the downloaded **Metadata XML** to [RightAnswers support team](https://www.rightanswers.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="bdc59-168">To configure single sign-on on **RightAnswers** side, you need to send the downloaded **Metadata XML** to [RightAnswers support team](https://www.rightanswers.com/contact-us/).</span></span>

    >[!NOTE]
    ><span data-ttu-id="bdc59-169">Your RightAnswers support team has to do the actual SSO configuration.</span><span class="sxs-lookup"><span data-stu-id="bdc59-169">Your RightAnswers support team has to do the actual SSO configuration.</span></span>
    ><span data-ttu-id="bdc59-170">You will get a notification when SSO has been enabled for your subscription.</span><span class="sxs-lookup"><span data-stu-id="bdc59-170">You will get a notification when SSO has been enabled for your subscription.</span></span>

> [!TIP]
> <span data-ttu-id="bdc59-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="bdc59-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bdc59-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="bdc59-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bdc59-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bdc59-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bdc59-174">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="bdc59-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="bdc59-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bdc59-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="bdc59-177">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bdc59-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bdc59-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="bdc59-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/rightanswers-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="bdc59-180">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="bdc59-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/rightanswers-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="bdc59-182">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="bdc59-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/rightanswers-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="bdc59-184">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="bdc59-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/rightanswers-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bdc59-186">a.</span><span class="sxs-lookup"><span data-stu-id="bdc59-186">a.</span></span> <span data-ttu-id="bdc59-187">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bdc59-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bdc59-188">b.</span><span class="sxs-lookup"><span data-stu-id="bdc59-188">b.</span></span> <span data-ttu-id="bdc59-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bdc59-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bdc59-190">c.</span><span class="sxs-lookup"><span data-stu-id="bdc59-190">c.</span></span> <span data-ttu-id="bdc59-191">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="bdc59-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="bdc59-192">d.</span><span class="sxs-lookup"><span data-stu-id="bdc59-192">d.</span></span> <span data-ttu-id="bdc59-193">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="bdc59-193">Click **Create**.</span></span>
 
### <a name="creating-a-rightanswers-test-user"></a><span data-ttu-id="bdc59-194">Creating a RightAnswers test user</span><span class="sxs-lookup"><span data-stu-id="bdc59-194">Creating a RightAnswers test user</span></span>

<span data-ttu-id="bdc59-195">To enable Azure AD users to log in to RightAnswers, they must be provisioned into RightAnswers.</span><span class="sxs-lookup"><span data-stu-id="bdc59-195">To enable Azure AD users to log in to RightAnswers, they must be provisioned into RightAnswers.</span></span> <span data-ttu-id="bdc59-196">When RightAnswers, provisioning is an automated task so there is no action item for you.</span><span class="sxs-lookup"><span data-stu-id="bdc59-196">When RightAnswers, provisioning is an automated task so there is no action item for you.</span></span>

<span data-ttu-id="bdc59-197">Users are automatically created if necessary during the first single sign-on attempt.</span><span class="sxs-lookup"><span data-stu-id="bdc59-197">Users are automatically created if necessary during the first single sign-on attempt.</span></span>

>[!NOTE]
><span data-ttu-id="bdc59-198">You can use any other RightAnswers user account creation tools or APIs provided by RightAnswers to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="bdc59-198">You can use any other RightAnswers user account creation tools or APIs provided by RightAnswers to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="bdc59-199">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="bdc59-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="bdc59-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RightAnswers.</span><span class="sxs-lookup"><span data-stu-id="bdc59-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RightAnswers.</span></span>

![Assign User][200] 

<span data-ttu-id="bdc59-202">**To assign Britta Simon to RightAnswers, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bdc59-202">**To assign Britta Simon to RightAnswers, perform the following steps:**</span></span>

1. <span data-ttu-id="bdc59-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="bdc59-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="bdc59-205">In the applications list, select **RightAnswers**.</span><span class="sxs-lookup"><span data-stu-id="bdc59-205">In the applications list, select **RightAnswers**.</span></span>

    ![Configure Single Sign-On](./media/rightanswers-tutorial/tutorial_rightanswers_app.png) 

1. <span data-ttu-id="bdc59-207">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="bdc59-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="bdc59-209">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="bdc59-209">Click **Add** button.</span></span> <span data-ttu-id="bdc59-210">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="bdc59-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="bdc59-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="bdc59-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="bdc59-213">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="bdc59-213">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="bdc59-214">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="bdc59-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bdc59-215">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="bdc59-215">Testing single sign-on</span></span>

<span data-ttu-id="bdc59-216">If you want to test your SSO settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="bdc59-216">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="bdc59-217">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bdc59-217">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>
## <a name="additional-resources"></a><span data-ttu-id="bdc59-218">Additional resources</span><span class="sxs-lookup"><span data-stu-id="bdc59-218">Additional resources</span></span>

* [<span data-ttu-id="bdc59-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bdc59-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="bdc59-220">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bdc59-220">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/rightanswers-tutorial/tutorial_general_01.png
[2]: ./media/rightanswers-tutorial/tutorial_general_02.png
[3]: ./media/rightanswers-tutorial/tutorial_general_03.png
[4]: ./media/rightanswers-tutorial/tutorial_general_04.png

[100]: ./media/rightanswers-tutorial/tutorial_general_100.png

[200]: ./media/rightanswers-tutorial/tutorial_general_200.png
[201]: ./media/rightanswers-tutorial/tutorial_general_201.png
[202]: ./media/rightanswers-tutorial/tutorial_general_202.png
[203]: ./media/rightanswers-tutorial/tutorial_general_203.png

