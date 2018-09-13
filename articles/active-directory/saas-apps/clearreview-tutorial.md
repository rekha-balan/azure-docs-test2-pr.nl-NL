---
title: 'Tutorial: Azure Active Directory integration with Clear Review | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Clear Review.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8264159a-11a2-4a8c-8285-4efea0adac8c
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/12/2018
ms.author: jeedes
ms.openlocfilehash: 604a557a91176c08a361ffd058adda63f53b30fc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864714"
---
# <a name="tutorial-azure-active-directory-integration-with-clear-review"></a><span data-ttu-id="94653-103">Tutorial: Azure Active Directory integration with Clear Review</span><span class="sxs-lookup"><span data-stu-id="94653-103">Tutorial: Azure Active Directory integration with Clear Review</span></span>

<span data-ttu-id="94653-104">In this tutorial, you learn how to integrate Clear Review with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="94653-104">In this tutorial, you learn how to integrate Clear Review with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="94653-105">Integrating Clear Review with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="94653-105">Integrating Clear Review with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="94653-106">You can control in Azure AD who has access to Clear Review.</span><span class="sxs-lookup"><span data-stu-id="94653-106">You can control in Azure AD who has access to Clear Review.</span></span>
- <span data-ttu-id="94653-107">You can enable your users to automatically get signed-on to Clear Review (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="94653-107">You can enable your users to automatically get signed-on to Clear Review (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="94653-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="94653-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="94653-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="94653-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="94653-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="94653-110">Prerequisites</span></span>

<span data-ttu-id="94653-111">To configure Azure AD integration with Clear Review, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="94653-111">To configure Azure AD integration with Clear Review, you need the following items:</span></span>

- <span data-ttu-id="94653-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="94653-112">An Azure AD subscription</span></span>
- <span data-ttu-id="94653-113">A Clear Review single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="94653-113">A Clear Review single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="94653-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="94653-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="94653-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="94653-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="94653-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="94653-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="94653-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="94653-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="94653-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="94653-118">Scenario description</span></span>
<span data-ttu-id="94653-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="94653-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="94653-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="94653-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="94653-121">Adding Clear Review from the gallery</span><span class="sxs-lookup"><span data-stu-id="94653-121">Adding Clear Review from the gallery</span></span>
1. <span data-ttu-id="94653-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="94653-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-clear-review-from-the-gallery"></a><span data-ttu-id="94653-123">Adding Clear Review from the gallery</span><span class="sxs-lookup"><span data-stu-id="94653-123">Adding Clear Review from the gallery</span></span>
<span data-ttu-id="94653-124">To configure the integration of Clear Review into Azure AD, you need to add Clear Review from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="94653-124">To configure the integration of Clear Review into Azure AD, you need to add Clear Review from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="94653-125">**To add Clear Review from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="94653-125">**To add Clear Review from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="94653-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="94653-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="94653-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="94653-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="94653-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="94653-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="94653-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="94653-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="94653-133">In the search box, type **Clear Review**, select **Clear Review** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="94653-133">In the search box, type **Clear Review**, select **Clear Review** from result panel then click **Add** button to add the application.</span></span>

    ![Clear Review in the results list](./media/clearreview-tutorial/tutorial_clearreview_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="94653-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="94653-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="94653-136">In this section, you configure and test Azure AD single sign-on with Clear Review based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="94653-136">In this section, you configure and test Azure AD single sign-on with Clear Review based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="94653-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Clear Review is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="94653-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Clear Review is to a user in Azure AD.</span></span> <span data-ttu-id="94653-138">In other words, a link relationship between an Azure AD user and the related user in Clear Review needs to be established.</span><span class="sxs-lookup"><span data-stu-id="94653-138">In other words, a link relationship between an Azure AD user and the related user in Clear Review needs to be established.</span></span>

<span data-ttu-id="94653-139">In Clear Review, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="94653-139">In Clear Review, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="94653-140">To configure and test Azure AD single sign-on with Clear Review, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="94653-140">To configure and test Azure AD single sign-on with Clear Review, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="94653-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="94653-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="94653-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="94653-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="94653-143">**[Create a Clear Review test user](#create-a-clear-review-test-user)** - to have a counterpart of Britta Simon in Clear Review that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="94653-143">**[Create a Clear Review test user](#create-a-clear-review-test-user)** - to have a counterpart of Britta Simon in Clear Review that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="94653-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="94653-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="94653-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="94653-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="94653-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="94653-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="94653-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Clear Review application.</span><span class="sxs-lookup"><span data-stu-id="94653-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Clear Review application.</span></span>

<span data-ttu-id="94653-148">**To configure Azure AD single sign-on with Clear Review, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="94653-148">**To configure Azure AD single sign-on with Clear Review, perform the following steps:**</span></span>

1. <span data-ttu-id="94653-149">In the Azure portal, on the **Clear Review** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="94653-149">In the Azure portal, on the **Clear Review** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="94653-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="94653-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/clearreview-tutorial/tutorial_clearreview_samlbase.png)

1. <span data-ttu-id="94653-153">On the **Clear Review Domain and URLs** section, perform the following steps if you wish to configure the application in **IdP initiated** mode:</span><span class="sxs-lookup"><span data-stu-id="94653-153">On the **Clear Review Domain and URLs** section, perform the following steps if you wish to configure the application in **IdP initiated** mode:</span></span>

    ![Clear Review Domain and URLs single sign-on information](./media/clearreview-tutorial/tutorial_clearreview_url.png)

    <span data-ttu-id="94653-155">a.</span><span class="sxs-lookup"><span data-stu-id="94653-155">a.</span></span> <span data-ttu-id="94653-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<customer name>.clearreview.com/sso/metadata/`</span><span class="sxs-lookup"><span data-stu-id="94653-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<customer name>.clearreview.com/sso/metadata/`</span></span>

    <span data-ttu-id="94653-157">b.</span><span class="sxs-lookup"><span data-stu-id="94653-157">b.</span></span> <span data-ttu-id="94653-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<customer name>.clearreview.com/sso/acs/`</span><span class="sxs-lookup"><span data-stu-id="94653-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<customer name>.clearreview.com/sso/acs/`</span></span>

1. <span data-ttu-id="94653-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="94653-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Clear Review Domain and URLs single sign-on information](./media/clearreview-tutorial/tutorial_clearreview_url_sp.png)

    <span data-ttu-id="94653-161">In the **Sign-on URL** textbox, type a URL using the following pattern:`https://<customer name>.clearreview.com`</span><span class="sxs-lookup"><span data-stu-id="94653-161">In the **Sign-on URL** textbox, type a URL using the following pattern:`https://<customer name>.clearreview.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="94653-162">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="94653-162">These values are not real.</span></span> <span data-ttu-id="94653-163">Update these values with the actual Sign-on URL, Identifier, and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="94653-163">Update these values with the actual Sign-on URL, Identifier, and Reply URL.</span></span> <span data-ttu-id="94653-164">Contact [Clear Review support team](https://clearreview.com/contact/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="94653-164">Contact [Clear Review support team](https://clearreview.com/contact/) to get these values.</span></span>

1. <span data-ttu-id="94653-165">Clear Review application expect the unique user identifier value in the Name Identifier claim.</span><span class="sxs-lookup"><span data-stu-id="94653-165">Clear Review application expect the unique user identifier value in the Name Identifier claim.</span></span> <span data-ttu-id="94653-166">You should map the user identifier value to **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="94653-166">You should map the user identifier value to **user.mail**.</span></span>

    ![The Attribute Section](./media/clearreview-tutorial/attribute.png)


1. <span data-ttu-id="94653-168">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="94653-168">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/clearreview-tutorial/tutorial_clearreview_certificate.png)

1. <span data-ttu-id="94653-170">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="94653-170">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/clearreview-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="94653-172">On the **Clear Review Configuration** section, click **Configure Clear Review** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="94653-172">On the **Clear Review Configuration** section, click **Configure Clear Review** to open **Configure sign-on** window.</span></span> <span data-ttu-id="94653-173">Copy the **Sign-Out URL ,SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="94653-173">Copy the **Sign-Out URL ,SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Clear Review Configuration](./media/clearreview-tutorial/tutorial_clearreview_configure.png) 

1. <span data-ttu-id="94653-175">To configure single sign-on on **Clear Review** side, open the **Clear Review** portal with admin credentials.</span><span class="sxs-lookup"><span data-stu-id="94653-175">To configure single sign-on on **Clear Review** side, open the **Clear Review** portal with admin credentials.</span></span>

1. <span data-ttu-id="94653-176">Select **Admin** from the left navigation.</span><span class="sxs-lookup"><span data-stu-id="94653-176">Select **Admin** from the left navigation.</span></span>

    ![Configure Single Sign-On Save button](./media/clearreview-tutorial/tutorial_clearreview_app_admin1.png)

1. <span data-ttu-id="94653-178">Select **Change** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="94653-178">Select **Change** at the bottom of the page.</span></span>

    ![Configure Single Sign-On Save button](./media/clearreview-tutorial/tutorial_clearreview_app_admin2.png)

1. <span data-ttu-id="94653-180">Perform following steps on **Single Sign-On Settings** page</span><span class="sxs-lookup"><span data-stu-id="94653-180">Perform following steps on **Single Sign-On Settings** page</span></span>

    ![Configure Single Sign-On Save button](./media/clearreview-tutorial/tutorial_clearreview_app_admin3.png)

    <span data-ttu-id="94653-182">a.</span><span class="sxs-lookup"><span data-stu-id="94653-182">a.</span></span> <span data-ttu-id="94653-183">In the **Issuer URL** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="94653-183">In the **Issuer URL** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="94653-184">b.</span><span class="sxs-lookup"><span data-stu-id="94653-184">b.</span></span> <span data-ttu-id="94653-185">In the **SAML Endpoint** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="94653-185">In the **SAML Endpoint** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>    

    <span data-ttu-id="94653-186">c.</span><span class="sxs-lookup"><span data-stu-id="94653-186">c.</span></span> <span data-ttu-id="94653-187">In the **SLO Endpoint** textbox, paste the value of **Sign-On Service URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="94653-187">In the **SLO Endpoint** textbox, paste the value of **Sign-On Service URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="94653-188">d.</span><span class="sxs-lookup"><span data-stu-id="94653-188">d.</span></span> <span data-ttu-id="94653-189">Open the downloaded certificate in notepad and paste the content in the **X.509 Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="94653-189">Open the downloaded certificate in notepad and paste the content in the **X.509 Certificate** textbox.</span></span>   

1. <span data-ttu-id="94653-190">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="94653-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="94653-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="94653-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="94653-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="94653-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="94653-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="94653-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="94653-194">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="94653-194">Create an Azure AD test user</span></span>

<span data-ttu-id="94653-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="94653-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="94653-197">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="94653-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="94653-198">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="94653-198">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/clearreview-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="94653-200">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="94653-200">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/clearreview-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="94653-202">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="94653-202">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/clearreview-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="94653-204">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="94653-204">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/clearreview-tutorial/create_aaduser_04.png)

    <span data-ttu-id="94653-206">a.</span><span class="sxs-lookup"><span data-stu-id="94653-206">a.</span></span> <span data-ttu-id="94653-207">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="94653-207">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="94653-208">b.</span><span class="sxs-lookup"><span data-stu-id="94653-208">b.</span></span> <span data-ttu-id="94653-209">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="94653-209">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="94653-210">c.</span><span class="sxs-lookup"><span data-stu-id="94653-210">c.</span></span> <span data-ttu-id="94653-211">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="94653-211">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="94653-212">d.</span><span class="sxs-lookup"><span data-stu-id="94653-212">d.</span></span> <span data-ttu-id="94653-213">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="94653-213">Click **Create**.</span></span>
  
### <a name="create-a-clear-review-test-user"></a><span data-ttu-id="94653-214">Create a Clear Review test user</span><span class="sxs-lookup"><span data-stu-id="94653-214">Create a Clear Review test user</span></span>

<span data-ttu-id="94653-215">In this section, you create a user called Britta Simon in Clear Review.</span><span class="sxs-lookup"><span data-stu-id="94653-215">In this section, you create a user called Britta Simon in Clear Review.</span></span> <span data-ttu-id="94653-216">Please work with [Clear Review support team](https://clearreview.com/contact/) to add the users in the Clear Review platform.</span><span class="sxs-lookup"><span data-stu-id="94653-216">Please work with [Clear Review support team](https://clearreview.com/contact/) to add the users in the Clear Review platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="94653-217">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="94653-217">Assign the Azure AD test user</span></span>

<span data-ttu-id="94653-218">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Clear Review.</span><span class="sxs-lookup"><span data-stu-id="94653-218">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Clear Review.</span></span>

![Assign the user role][200] 

<span data-ttu-id="94653-220">**To assign Britta Simon to Clear Review, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="94653-220">**To assign Britta Simon to Clear Review, perform the following steps:**</span></span>

1. <span data-ttu-id="94653-221">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="94653-221">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="94653-223">In the applications list, select **Clear Review**.</span><span class="sxs-lookup"><span data-stu-id="94653-223">In the applications list, select **Clear Review**.</span></span>

    ![The Clear Review link in the Applications list](./media/clearreview-tutorial/tutorial_clearreview_app.png)  

1. <span data-ttu-id="94653-225">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="94653-225">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="94653-227">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="94653-227">Click **Add** button.</span></span> <span data-ttu-id="94653-228">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="94653-228">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="94653-230">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="94653-230">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="94653-231">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="94653-231">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="94653-232">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="94653-232">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="94653-233">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="94653-233">Test single sign-on</span></span>

<span data-ttu-id="94653-234">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="94653-234">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="94653-235">When you click the Clear Review tile in the Access Panel, you should get automatically signed-on to your Clear Review application.</span><span class="sxs-lookup"><span data-stu-id="94653-235">When you click the Clear Review tile in the Access Panel, you should get automatically signed-on to your Clear Review application.</span></span>
<span data-ttu-id="94653-236">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="94653-236">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="94653-237">Additional resources</span><span class="sxs-lookup"><span data-stu-id="94653-237">Additional resources</span></span>

* [<span data-ttu-id="94653-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="94653-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="94653-239">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="94653-239">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/clearreview-tutorial/tutorial_general_01.png
[2]: ./media/clearreview-tutorial/tutorial_general_02.png
[3]: ./media/clearreview-tutorial/tutorial_general_03.png
[4]: ./media/clearreview-tutorial/tutorial_general_04.png

[100]: ./media/clearreview-tutorial/tutorial_general_100.png

[200]: ./media/clearreview-tutorial/tutorial_general_200.png
[201]: ./media/clearreview-tutorial/tutorial_general_201.png
[202]: ./media/clearreview-tutorial/tutorial_general_202.png
[203]: ./media/clearreview-tutorial/tutorial_general_203.png
