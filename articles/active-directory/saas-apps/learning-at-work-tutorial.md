---
title: 'Tutorial: Azure Active Directory integration with Learning at Work | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Learning at Work.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 1d607174-bea1-4f40-8233-54cabe02c66a
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: jeedes
ms.openlocfilehash: 35b02adade9f202480e3649fbfcb24d18c765aa1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856325"
---
# <a name="tutorial-azure-active-directory-integration-with-learning-at-work"></a><span data-ttu-id="eeaab-103">Tutorial: Azure Active Directory integration with Learning at Work</span><span class="sxs-lookup"><span data-stu-id="eeaab-103">Tutorial: Azure Active Directory integration with Learning at Work</span></span>

<span data-ttu-id="eeaab-104">In this tutorial, you learn how to integrate Learning at Work with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="eeaab-104">In this tutorial, you learn how to integrate Learning at Work with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="eeaab-105">Integrating Learning at Work with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="eeaab-105">Integrating Learning at Work with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="eeaab-106">You can control in Azure AD who has access to Learning at Work</span><span class="sxs-lookup"><span data-stu-id="eeaab-106">You can control in Azure AD who has access to Learning at Work</span></span>
- <span data-ttu-id="eeaab-107">You can enable your users to automatically get signed-on to Learning at Work (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="eeaab-107">You can enable your users to automatically get signed-on to Learning at Work (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="eeaab-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="eeaab-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="eeaab-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="eeaab-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eeaab-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="eeaab-110">Prerequisites</span></span>

<span data-ttu-id="eeaab-111">To configure Azure AD integration with Learning at Work, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="eeaab-111">To configure Azure AD integration with Learning at Work, you need the following items:</span></span>

- <span data-ttu-id="eeaab-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="eeaab-112">An Azure AD subscription</span></span>
- <span data-ttu-id="eeaab-113">A Learning at Work single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="eeaab-113">A Learning at Work single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="eeaab-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="eeaab-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="eeaab-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="eeaab-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="eeaab-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="eeaab-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="eeaab-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eeaab-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="eeaab-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="eeaab-118">Scenario description</span></span>
<span data-ttu-id="eeaab-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="eeaab-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="eeaab-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="eeaab-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="eeaab-121">Adding Learning at Work from the gallery</span><span class="sxs-lookup"><span data-stu-id="eeaab-121">Adding Learning at Work from the gallery</span></span>
1. <span data-ttu-id="eeaab-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="eeaab-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learning-at-work-from-the-gallery"></a><span data-ttu-id="eeaab-123">Adding Learning at Work from the gallery</span><span class="sxs-lookup"><span data-stu-id="eeaab-123">Adding Learning at Work from the gallery</span></span>
<span data-ttu-id="eeaab-124">To configure the integration of Learning at Work into Azure AD, you need to add Learning at Work from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="eeaab-124">To configure the integration of Learning at Work into Azure AD, you need to add Learning at Work from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="eeaab-125">**To add Learning at Work from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="eeaab-125">**To add Learning at Work from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="eeaab-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="eeaab-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="eeaab-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="eeaab-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="eeaab-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="eeaab-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="eeaab-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="eeaab-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="eeaab-133">In the search box, type **Learning at Work**.</span><span class="sxs-lookup"><span data-stu-id="eeaab-133">In the search box, type **Learning at Work**.</span></span>

    ![Creating an Azure AD test user](./media/learning-at-work-tutorial/tutorial_learningatwork_search.png)

1. <span data-ttu-id="eeaab-135">In the results panel, select **Learning at Work**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="eeaab-135">In the results panel, select **Learning at Work**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/learning-at-work-tutorial/tutorial_learningatwork_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="eeaab-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="eeaab-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="eeaab-138">In this section, you configure and test Azure AD single sign-on with Learning at Work based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="eeaab-138">In this section, you configure and test Azure AD single sign-on with Learning at Work based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="eeaab-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Learning at Work is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eeaab-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Learning at Work is to a user in Azure AD.</span></span> <span data-ttu-id="eeaab-140">In other words, a link relationship between an Azure AD user and the related user in Learning at Work needs to be established.</span><span class="sxs-lookup"><span data-stu-id="eeaab-140">In other words, a link relationship between an Azure AD user and the related user in Learning at Work needs to be established.</span></span>

<span data-ttu-id="eeaab-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Learning at Work.</span><span class="sxs-lookup"><span data-stu-id="eeaab-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Learning at Work.</span></span>

<span data-ttu-id="eeaab-142">To configure and test Azure AD single sign-on with Learning at Work, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="eeaab-142">To configure and test Azure AD single sign-on with Learning at Work, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="eeaab-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="eeaab-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="eeaab-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="eeaab-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="eeaab-145">**[Creating a Learning at Work test user](#creating-a-learning-at-work-test-user)** - to have a counterpart of Britta Simon in Learning at Work that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="eeaab-145">**[Creating a Learning at Work test user](#creating-a-learning-at-work-test-user)** - to have a counterpart of Britta Simon in Learning at Work that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="eeaab-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="eeaab-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="eeaab-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="eeaab-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="eeaab-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="eeaab-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="eeaab-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Learning at Work application.</span><span class="sxs-lookup"><span data-stu-id="eeaab-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Learning at Work application.</span></span>

<span data-ttu-id="eeaab-150">**To configure Azure AD single sign-on with Learning at Work, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="eeaab-150">**To configure Azure AD single sign-on with Learning at Work, perform the following steps:**</span></span>

1. <span data-ttu-id="eeaab-151">In the Azure portal, on the **Learning at Work** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="eeaab-151">In the Azure portal, on the **Learning at Work** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="eeaab-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="eeaab-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/learning-at-work-tutorial/tutorial_learningatwork_samlbase.png)

1. <span data-ttu-id="eeaab-155">On the **Learning at Work Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="eeaab-155">On the **Learning at Work Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/learning-at-work-tutorial/tutorial_learningatwork_url.png)

    <span data-ttu-id="eeaab-157">a.</span><span class="sxs-lookup"><span data-stu-id="eeaab-157">a.</span></span> <span data-ttu-id="eeaab-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.sabacloud.com/Saba/Web/<company code>`</span><span class="sxs-lookup"><span data-stu-id="eeaab-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.sabacloud.com/Saba/Web/<company code>`</span></span>

    <span data-ttu-id="eeaab-159">b.</span><span class="sxs-lookup"><span data-stu-id="eeaab-159">b.</span></span> <span data-ttu-id="eeaab-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.sabacloud.com/Saba/saml/SSO/alias/<company name>`</span><span class="sxs-lookup"><span data-stu-id="eeaab-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.sabacloud.com/Saba/saml/SSO/alias/<company name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="eeaab-161">These values are not the real.</span><span class="sxs-lookup"><span data-stu-id="eeaab-161">These values are not the real.</span></span> <span data-ttu-id="eeaab-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="eeaab-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="eeaab-163">Contact [Learning at Work Client support team](https://www.learninga-z.com/site/contact/support) to get these values.</span><span class="sxs-lookup"><span data-stu-id="eeaab-163">Contact [Learning at Work Client support team](https://www.learninga-z.com/site/contact/support) to get these values.</span></span> 
 
1. <span data-ttu-id="eeaab-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="eeaab-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/learning-at-work-tutorial/tutorial_learningatwork_certificate.png) 

1. <span data-ttu-id="eeaab-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="eeaab-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/learning-at-work-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="eeaab-168">On the **Learning at Work Configuration** section, click **Configure Learning at Work** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="eeaab-168">On the **Learning at Work Configuration** section, click **Configure Learning at Work** to open **Configure sign-on** window.</span></span> <span data-ttu-id="eeaab-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="eeaab-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/learning-at-work-tutorial/tutorial_learningatwork_configure.png) 

1. <span data-ttu-id="eeaab-171">To configure single sign-on on **Learning at Work** side, you need to send the downloaded **Metadata XML**, **SAML Entity ID**, **SAML Single Sign-On Service URL**, and **Sign-Out URL** to [Learning at Work support](https://www.learninga-z.com/site/contact/support).</span><span class="sxs-lookup"><span data-stu-id="eeaab-171">To configure single sign-on on **Learning at Work** side, you need to send the downloaded **Metadata XML**, **SAML Entity ID**, **SAML Single Sign-On Service URL**, and **Sign-Out URL** to [Learning at Work support](https://www.learninga-z.com/site/contact/support).</span></span>

> [!TIP]
> <span data-ttu-id="eeaab-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="eeaab-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="eeaab-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="eeaab-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="eeaab-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="eeaab-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="eeaab-175">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="eeaab-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="eeaab-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="eeaab-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="eeaab-178">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="eeaab-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="eeaab-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="eeaab-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/learning-at-work-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="eeaab-181">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="eeaab-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/learning-at-work-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="eeaab-183">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="eeaab-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/learning-at-work-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="eeaab-185">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="eeaab-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/learning-at-work-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="eeaab-187">a.</span><span class="sxs-lookup"><span data-stu-id="eeaab-187">a.</span></span> <span data-ttu-id="eeaab-188">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="eeaab-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="eeaab-189">b.</span><span class="sxs-lookup"><span data-stu-id="eeaab-189">b.</span></span> <span data-ttu-id="eeaab-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="eeaab-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="eeaab-191">c.</span><span class="sxs-lookup"><span data-stu-id="eeaab-191">c.</span></span> <span data-ttu-id="eeaab-192">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="eeaab-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="eeaab-193">d.</span><span class="sxs-lookup"><span data-stu-id="eeaab-193">d.</span></span> <span data-ttu-id="eeaab-194">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="eeaab-194">Click **Create**.</span></span>
 
### <a name="creating-a-learning-at-work-test-user"></a><span data-ttu-id="eeaab-195">Creating a Learning at Work test user</span><span class="sxs-lookup"><span data-stu-id="eeaab-195">Creating a Learning at Work test user</span></span>

<span data-ttu-id="eeaab-196">In this section, you create a user called Britta Simon in Learning at Work.</span><span class="sxs-lookup"><span data-stu-id="eeaab-196">In this section, you create a user called Britta Simon in Learning at Work.</span></span> <span data-ttu-id="eeaab-197">Work with [Learning at Work support](https://www.learninga-z.com/site/contact/support) to add the users in the Learning at Work platform.</span><span class="sxs-lookup"><span data-stu-id="eeaab-197">Work with [Learning at Work support](https://www.learninga-z.com/site/contact/support) to add the users in the Learning at Work platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="eeaab-198">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="eeaab-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="eeaab-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Learning at Work.</span><span class="sxs-lookup"><span data-stu-id="eeaab-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Learning at Work.</span></span>

![Assign User][200] 

<span data-ttu-id="eeaab-201">**To assign Britta Simon to Learning at Work, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="eeaab-201">**To assign Britta Simon to Learning at Work, perform the following steps:**</span></span>

1. <span data-ttu-id="eeaab-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="eeaab-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="eeaab-204">In the applications list, select **Learning at Work**.</span><span class="sxs-lookup"><span data-stu-id="eeaab-204">In the applications list, select **Learning at Work**.</span></span>

    ![Configure Single Sign-On](./media/learning-at-work-tutorial/tutorial_learningatwork_app.png) 

1. <span data-ttu-id="eeaab-206">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="eeaab-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="eeaab-208">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="eeaab-208">Click **Add** button.</span></span> <span data-ttu-id="eeaab-209">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="eeaab-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="eeaab-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="eeaab-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="eeaab-212">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="eeaab-212">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="eeaab-213">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="eeaab-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="eeaab-214">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="eeaab-214">Testing single sign-on</span></span>

<span data-ttu-id="eeaab-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="eeaab-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="eeaab-216">When you click the Learning at Work tile in the Access Panel, you should get automatically signed-on to your Learning at Work application.</span><span class="sxs-lookup"><span data-stu-id="eeaab-216">When you click the Learning at Work tile in the Access Panel, you should get automatically signed-on to your Learning at Work application.</span></span>
<span data-ttu-id="eeaab-217">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="eeaab-217">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="eeaab-218">Additional resources</span><span class="sxs-lookup"><span data-stu-id="eeaab-218">Additional resources</span></span>

* [<span data-ttu-id="eeaab-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eeaab-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="eeaab-220">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="eeaab-220">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/learning-at-work-tutorial/tutorial_general_01.png
[2]: ./media/learning-at-work-tutorial/tutorial_general_02.png
[3]: ./media/learning-at-work-tutorial/tutorial_general_03.png
[4]: ./media/learning-at-work-tutorial/tutorial_general_04.png

[100]: ./media/learning-at-work-tutorial/tutorial_general_100.png

[200]: ./media/learning-at-work-tutorial/tutorial_general_200.png
[201]: ./media/learning-at-work-tutorial/tutorial_general_201.png
[202]: ./media/learning-at-work-tutorial/tutorial_general_202.png
[203]: ./media/learning-at-work-tutorial/tutorial_general_203.png

