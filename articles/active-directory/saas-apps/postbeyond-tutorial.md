---
title: 'Tutorial: Azure Active Directory integration with PostBeyond | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and PostBeyond.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 09992f08-ec50-4472-997f-ccbe719039e8
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 724956bd2b39fe5d1c06606953b02bd733d3da3c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870652"
---
# <a name="tutorial-azure-active-directory-integration-with-postbeyond"></a><span data-ttu-id="71840-103">Tutorial: Azure Active Directory integration with PostBeyond</span><span class="sxs-lookup"><span data-stu-id="71840-103">Tutorial: Azure Active Directory integration with PostBeyond</span></span>

<span data-ttu-id="71840-104">In this tutorial, you learn how to integrate PostBeyond with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="71840-104">In this tutorial, you learn how to integrate PostBeyond with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="71840-105">Integrating PostBeyond with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="71840-105">Integrating PostBeyond with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="71840-106">You can control in Azure AD who has access to PostBeyond</span><span class="sxs-lookup"><span data-stu-id="71840-106">You can control in Azure AD who has access to PostBeyond</span></span>
- <span data-ttu-id="71840-107">You can enable your users to automatically get signed-on to PostBeyond (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="71840-107">You can enable your users to automatically get signed-on to PostBeyond (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="71840-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="71840-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="71840-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="71840-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="71840-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="71840-110">Prerequisites</span></span>

<span data-ttu-id="71840-111">To configure Azure AD integration with PostBeyond, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="71840-111">To configure Azure AD integration with PostBeyond, you need the following items:</span></span>

- <span data-ttu-id="71840-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="71840-112">An Azure AD subscription</span></span>
- <span data-ttu-id="71840-113">A PostBeyond single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="71840-113">A PostBeyond single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="71840-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="71840-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="71840-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="71840-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="71840-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="71840-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="71840-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="71840-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="71840-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="71840-118">Scenario description</span></span>
<span data-ttu-id="71840-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="71840-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="71840-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="71840-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="71840-121">Adding PostBeyond from the gallery</span><span class="sxs-lookup"><span data-stu-id="71840-121">Adding PostBeyond from the gallery</span></span>
1. <span data-ttu-id="71840-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="71840-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-postbeyond-from-the-gallery"></a><span data-ttu-id="71840-123">Adding PostBeyond from the gallery</span><span class="sxs-lookup"><span data-stu-id="71840-123">Adding PostBeyond from the gallery</span></span>
<span data-ttu-id="71840-124">To configure the integration of PostBeyond into Azure AD, you need to add PostBeyond from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="71840-124">To configure the integration of PostBeyond into Azure AD, you need to add PostBeyond from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="71840-125">**To add PostBeyond from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="71840-125">**To add PostBeyond from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="71840-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="71840-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="71840-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="71840-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="71840-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="71840-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="71840-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="71840-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="71840-133">In the search box, type **PostBeyond**.</span><span class="sxs-lookup"><span data-stu-id="71840-133">In the search box, type **PostBeyond**.</span></span>

    ![Creating an Azure AD test user](./media/postbeyond-tutorial/tutorial_postbeyond_search.png)

1. <span data-ttu-id="71840-135">In the results panel, select **PostBeyond**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="71840-135">In the results panel, select **PostBeyond**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/postbeyond-tutorial/tutorial_postbeyond_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="71840-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="71840-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="71840-138">In this section, you configure and test Azure AD single sign-on with PostBeyond based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="71840-138">In this section, you configure and test Azure AD single sign-on with PostBeyond based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="71840-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PostBeyond is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="71840-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PostBeyond is to a user in Azure AD.</span></span> <span data-ttu-id="71840-140">In other words, a link relationship between an Azure AD user and the related user in PostBeyond needs to be established.</span><span class="sxs-lookup"><span data-stu-id="71840-140">In other words, a link relationship between an Azure AD user and the related user in PostBeyond needs to be established.</span></span>

<span data-ttu-id="71840-141">In PostBeyond, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="71840-141">In PostBeyond, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="71840-142">To configure and test Azure AD single sign-on with PostBeyond, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="71840-142">To configure and test Azure AD single sign-on with PostBeyond, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="71840-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="71840-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="71840-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="71840-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="71840-145">**[Creating a PostBeyond test user](#creating-a-postbeyond-test-user)** - to have a counterpart of Britta Simon in PostBeyond that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="71840-145">**[Creating a PostBeyond test user](#creating-a-postbeyond-test-user)** - to have a counterpart of Britta Simon in PostBeyond that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="71840-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="71840-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="71840-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="71840-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="71840-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="71840-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="71840-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PostBeyond application.</span><span class="sxs-lookup"><span data-stu-id="71840-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PostBeyond application.</span></span>

<span data-ttu-id="71840-150">**To configure Azure AD single sign-on with PostBeyond, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="71840-150">**To configure Azure AD single sign-on with PostBeyond, perform the following steps:**</span></span>

1. <span data-ttu-id="71840-151">In the Azure portal, on the **PostBeyond** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="71840-151">In the Azure portal, on the **PostBeyond** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="71840-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="71840-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/postbeyond-tutorial/tutorial_postbeyond_samlbase.png)

1. <span data-ttu-id="71840-155">On the **PostBeyond Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="71840-155">On the **PostBeyond Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/postbeyond-tutorial/tutorial_postbeyond_url.png)

    <span data-ttu-id="71840-157">a.</span><span class="sxs-lookup"><span data-stu-id="71840-157">a.</span></span> <span data-ttu-id="71840-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.postbeyond.com`</span><span class="sxs-lookup"><span data-stu-id="71840-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.postbeyond.com`</span></span>

    <span data-ttu-id="71840-159">b.</span><span class="sxs-lookup"><span data-stu-id="71840-159">b.</span></span> <span data-ttu-id="71840-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.postbeyond.com`</span><span class="sxs-lookup"><span data-stu-id="71840-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.postbeyond.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="71840-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="71840-161">These values are not real.</span></span> <span data-ttu-id="71840-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="71840-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="71840-163">Contact [PostBeyond Client support team](mailto:sso@postbeyond.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="71840-163">Contact [PostBeyond Client support team](mailto:sso@postbeyond.com) to get these values.</span></span> 
 
1. <span data-ttu-id="71840-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="71840-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/postbeyond-tutorial/tutorial_postbeyond_certificate.png) 

1. <span data-ttu-id="71840-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="71840-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/postbeyond-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="71840-168">On the **PostBeyond Configuration** section, click **Configure PostBeyond** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="71840-168">On the **PostBeyond Configuration** section, click **Configure PostBeyond** to open **Configure sign-on** window.</span></span> <span data-ttu-id="71840-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="71840-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/postbeyond-tutorial/tutorial_postbeyond_configure.png) 

1. <span data-ttu-id="71840-171">To configure single sign-on on **PostBeyond** side, you need to send the downloaded **Certificate(Base64)**, **SAML Entity ID**, **SAML Single Sign-On Service URL** and **Sign-Out URL** to [PostBeyond support team](mailto:sso@postbeyond.com).</span><span class="sxs-lookup"><span data-stu-id="71840-171">To configure single sign-on on **PostBeyond** side, you need to send the downloaded **Certificate(Base64)**, **SAML Entity ID**, **SAML Single Sign-On Service URL** and **Sign-Out URL** to [PostBeyond support team](mailto:sso@postbeyond.com).</span></span> <span data-ttu-id="71840-172">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="71840-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="71840-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="71840-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="71840-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="71840-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="71840-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="71840-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="71840-176">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="71840-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="71840-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="71840-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="71840-179">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="71840-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="71840-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="71840-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/postbeyond-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="71840-182">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="71840-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/postbeyond-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="71840-184">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="71840-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/postbeyond-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="71840-186">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="71840-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/postbeyond-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="71840-188">a.</span><span class="sxs-lookup"><span data-stu-id="71840-188">a.</span></span> <span data-ttu-id="71840-189">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="71840-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="71840-190">b.</span><span class="sxs-lookup"><span data-stu-id="71840-190">b.</span></span> <span data-ttu-id="71840-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="71840-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="71840-192">c.</span><span class="sxs-lookup"><span data-stu-id="71840-192">c.</span></span> <span data-ttu-id="71840-193">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="71840-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="71840-194">d.</span><span class="sxs-lookup"><span data-stu-id="71840-194">d.</span></span> <span data-ttu-id="71840-195">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="71840-195">Click **Create**.</span></span>
 
### <a name="creating-a-postbeyond-test-user"></a><span data-ttu-id="71840-196">Creating a PostBeyond test user</span><span class="sxs-lookup"><span data-stu-id="71840-196">Creating a PostBeyond test user</span></span>

<span data-ttu-id="71840-197">In this section, you create a user called Britta Simon in PostBeyond.</span><span class="sxs-lookup"><span data-stu-id="71840-197">In this section, you create a user called Britta Simon in PostBeyond.</span></span> <span data-ttu-id="71840-198">If you don't know how to add Britta Simon in PostBeyond, please work with [PostBeyond support team](mailto:sso@postbeyond.com) to add the test user and enable SSO.</span><span class="sxs-lookup"><span data-stu-id="71840-198">If you don't know how to add Britta Simon in PostBeyond, please work with [PostBeyond support team](mailto:sso@postbeyond.com) to add the test user and enable SSO.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="71840-199">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="71840-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="71840-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PostBeyond.</span><span class="sxs-lookup"><span data-stu-id="71840-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PostBeyond.</span></span>

![Assign User][200] 

<span data-ttu-id="71840-202">**To assign Britta Simon to PostBeyond, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="71840-202">**To assign Britta Simon to PostBeyond, perform the following steps:**</span></span>

1. <span data-ttu-id="71840-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="71840-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="71840-205">In the applications list, select **PostBeyond**.</span><span class="sxs-lookup"><span data-stu-id="71840-205">In the applications list, select **PostBeyond**.</span></span>

    ![Configure Single Sign-On](./media/postbeyond-tutorial/tutorial_postbeyond_app.png) 

1. <span data-ttu-id="71840-207">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="71840-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="71840-209">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="71840-209">Click **Add** button.</span></span> <span data-ttu-id="71840-210">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="71840-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="71840-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="71840-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="71840-213">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="71840-213">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="71840-214">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="71840-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="71840-215">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="71840-215">Testing single sign-on</span></span>

<span data-ttu-id="71840-216">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="71840-216">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="71840-217">When you click the PostBeyond tile in the Access Panel, you should get to the PostBeyond sign in page.</span><span class="sxs-lookup"><span data-stu-id="71840-217">When you click the PostBeyond tile in the Access Panel, you should get to the PostBeyond sign in page.</span></span> <span data-ttu-id="71840-218">Click on **Sign in with Office 365**, enter your Azure AD credentials.</span><span class="sxs-lookup"><span data-stu-id="71840-218">Click on **Sign in with Office 365**, enter your Azure AD credentials.</span></span> <span data-ttu-id="71840-219">Then, you should be logged in into PostBeyond.</span><span class="sxs-lookup"><span data-stu-id="71840-219">Then, you should be logged in into PostBeyond.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="71840-220">Additional resources</span><span class="sxs-lookup"><span data-stu-id="71840-220">Additional resources</span></span>

* [<span data-ttu-id="71840-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="71840-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="71840-222">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="71840-222">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/postbeyond-tutorial/tutorial_general_01.png
[2]: ./media/postbeyond-tutorial/tutorial_general_02.png
[3]: ./media/postbeyond-tutorial/tutorial_general_03.png
[4]: ./media/postbeyond-tutorial/tutorial_general_04.png

[100]: ./media/postbeyond-tutorial/tutorial_general_100.png

[200]: ./media/postbeyond-tutorial/tutorial_general_200.png
[201]: ./media/postbeyond-tutorial/tutorial_general_201.png
[202]: ./media/postbeyond-tutorial/tutorial_general_202.png
[203]: ./media/postbeyond-tutorial/tutorial_general_203.png

