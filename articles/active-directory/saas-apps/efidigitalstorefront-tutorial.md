---
title: 'Tutorial: Azure Active Directory integration with EFI Digital StoreFront | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and EFI Digital StoreFront.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 33c148fc-d490-4bb9-90c1-d5933679ce4e
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/08/2017
ms.author: jeedes
ms.openlocfilehash: 6959521b0f700a0afafef0950e9cb336488cc94b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864764"
---
# <a name="tutorial-azure-active-directory-integration-with-efi-digital-storefront"></a><span data-ttu-id="a1b48-103">Tutorial: Azure Active Directory integration with EFI Digital StoreFront</span><span class="sxs-lookup"><span data-stu-id="a1b48-103">Tutorial: Azure Active Directory integration with EFI Digital StoreFront</span></span>

<span data-ttu-id="a1b48-104">In this tutorial, you learn how to integrate EFI Digital StoreFront with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a1b48-104">In this tutorial, you learn how to integrate EFI Digital StoreFront with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a1b48-105">Integrating EFI Digital StoreFront with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="a1b48-105">Integrating EFI Digital StoreFront with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a1b48-106">You can control in Azure AD who has access to EFI Digital StoreFront.</span><span class="sxs-lookup"><span data-stu-id="a1b48-106">You can control in Azure AD who has access to EFI Digital StoreFront.</span></span>
- <span data-ttu-id="a1b48-107">You can enable your users to automatically get signed-on to EFI Digital StoreFront (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="a1b48-107">You can enable your users to automatically get signed-on to EFI Digital StoreFront (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="a1b48-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a1b48-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="a1b48-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="a1b48-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a1b48-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a1b48-110">Prerequisites</span></span>

<span data-ttu-id="a1b48-111">To configure Azure AD integration with EFI Digital StoreFront, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="a1b48-111">To configure Azure AD integration with EFI Digital StoreFront, you need the following items:</span></span>

- <span data-ttu-id="a1b48-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="a1b48-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a1b48-113">A EFI Digital StoreFront single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="a1b48-113">A EFI Digital StoreFront single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a1b48-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="a1b48-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a1b48-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="a1b48-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a1b48-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="a1b48-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a1b48-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a1b48-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a1b48-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="a1b48-118">Scenario description</span></span>
<span data-ttu-id="a1b48-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="a1b48-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a1b48-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="a1b48-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a1b48-121">Adding EFI Digital StoreFront from the gallery</span><span class="sxs-lookup"><span data-stu-id="a1b48-121">Adding EFI Digital StoreFront from the gallery</span></span>
1. <span data-ttu-id="a1b48-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a1b48-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-efi-digital-storefront-from-the-gallery"></a><span data-ttu-id="a1b48-123">Adding EFI Digital StoreFront from the gallery</span><span class="sxs-lookup"><span data-stu-id="a1b48-123">Adding EFI Digital StoreFront from the gallery</span></span>
<span data-ttu-id="a1b48-124">To configure the integration of EFI Digital StoreFront into Azure AD, you need to add EFI Digital StoreFront from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="a1b48-124">To configure the integration of EFI Digital StoreFront into Azure AD, you need to add EFI Digital StoreFront from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a1b48-125">**To add EFI Digital StoreFront from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a1b48-125">**To add EFI Digital StoreFront from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a1b48-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a1b48-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="a1b48-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="a1b48-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a1b48-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a1b48-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="a1b48-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="a1b48-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="a1b48-133">In the search box, type **EFI Digital StoreFront**, select **EFI Digital StoreFront** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="a1b48-133">In the search box, type **EFI Digital StoreFront**, select **EFI Digital StoreFront** from result panel then click **Add** button to add the application.</span></span>

    ![EFI Digital StoreFront in the results list](./media/efidigitalstorefront-tutorial/tutorial_efidigital_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a1b48-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a1b48-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="a1b48-136">In this section, you configure and test Azure AD single sign-on with EFI Digital StoreFront based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a1b48-136">In this section, you configure and test Azure AD single sign-on with EFI Digital StoreFront based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a1b48-137">For single sign-on to work, Azure AD needs to know what the counterpart user in EFI Digital StoreFront is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a1b48-137">For single sign-on to work, Azure AD needs to know what the counterpart user in EFI Digital StoreFront is to a user in Azure AD.</span></span> <span data-ttu-id="a1b48-138">In other words, a link relationship between an Azure AD user and the related user in EFI Digital StoreFront needs to be established.</span><span class="sxs-lookup"><span data-stu-id="a1b48-138">In other words, a link relationship between an Azure AD user and the related user in EFI Digital StoreFront needs to be established.</span></span>

<span data-ttu-id="a1b48-139">In EFI Digital StoreFront, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="a1b48-139">In EFI Digital StoreFront, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a1b48-140">To configure and test Azure AD single sign-on with EFI Digital StoreFront, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="a1b48-140">To configure and test Azure AD single sign-on with EFI Digital StoreFront, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a1b48-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="a1b48-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="a1b48-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a1b48-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="a1b48-143">**[Create a EFI Digital StoreFront test user](#create-a-efi-digital-storefront-test-user)** - to have a counterpart of Britta Simon in EFI Digital StoreFront that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="a1b48-143">**[Create a EFI Digital StoreFront test user](#create-a-efi-digital-storefront-test-user)** - to have a counterpart of Britta Simon in EFI Digital StoreFront that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="a1b48-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a1b48-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="a1b48-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="a1b48-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a1b48-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a1b48-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a1b48-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your EFI Digital StoreFront application.</span><span class="sxs-lookup"><span data-stu-id="a1b48-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your EFI Digital StoreFront application.</span></span>

<span data-ttu-id="a1b48-148">**To configure Azure AD single sign-on with EFI Digital StoreFront, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a1b48-148">**To configure Azure AD single sign-on with EFI Digital StoreFront, perform the following steps:**</span></span>

1. <span data-ttu-id="a1b48-149">In the Azure portal, on the **EFI Digital StoreFront** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="a1b48-149">In the Azure portal, on the **EFI Digital StoreFront** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="a1b48-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a1b48-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/efidigitalstorefront-tutorial/tutorial_efidigital_samlbase.png)

1. <span data-ttu-id="a1b48-153">On the **EFI Digital StoreFront Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a1b48-153">On the **EFI Digital StoreFront Domain and URLs** section, perform the following steps:</span></span>

    ![EFI Digital StoreFront Domain and URLs single sign-on information](./media/efidigitalstorefront-tutorial/tutorial_efidigital_url.png)

    <span data-ttu-id="a1b48-155">a.</span><span class="sxs-lookup"><span data-stu-id="a1b48-155">a.</span></span> <span data-ttu-id="a1b48-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.myprintdesk.net/DSF`</span><span class="sxs-lookup"><span data-stu-id="a1b48-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.myprintdesk.net/DSF`</span></span>

    <span data-ttu-id="a1b48-157">b.</span><span class="sxs-lookup"><span data-stu-id="a1b48-157">b.</span></span> <span data-ttu-id="a1b48-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.myprintdesk.net/DSF/asp4/`</span><span class="sxs-lookup"><span data-stu-id="a1b48-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.myprintdesk.net/DSF/asp4/`</span></span>

1. <span data-ttu-id="a1b48-159">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="a1b48-159">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/efidigitalstorefront-tutorial/tutorial_efidigital_certificate.png) 

1. <span data-ttu-id="a1b48-161">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="a1b48-161">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/efidigitalstorefront-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="a1b48-163">To configure single sign-on on **EFI Digital StoreFront** side, you need to send the downloaded **Metadata XML** to [EFI Digital StoreFront support team](http://www.efi.com/products/productivity-software/ecommerce-web-to-print/efi-digital-storefront/support/).</span><span class="sxs-lookup"><span data-stu-id="a1b48-163">To configure single sign-on on **EFI Digital StoreFront** side, you need to send the downloaded **Metadata XML** to [EFI Digital StoreFront support team](http://www.efi.com/products/productivity-software/ecommerce-web-to-print/efi-digital-storefront/support/).</span></span> <span data-ttu-id="a1b48-164">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="a1b48-164">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="a1b48-165">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="a1b48-165">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a1b48-166">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="a1b48-166">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a1b48-167">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a1b48-167">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a1b48-168">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a1b48-168">Create an Azure AD test user</span></span>

<span data-ttu-id="a1b48-169">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a1b48-169">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="a1b48-171">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a1b48-171">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a1b48-172">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="a1b48-172">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/efidigitalstorefront-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="a1b48-174">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="a1b48-174">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/efidigitalstorefront-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="a1b48-176">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="a1b48-176">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/efidigitalstorefront-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="a1b48-178">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a1b48-178">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/efidigitalstorefront-tutorial/create_aaduser_04.png)

    <span data-ttu-id="a1b48-180">a.</span><span class="sxs-lookup"><span data-stu-id="a1b48-180">a.</span></span> <span data-ttu-id="a1b48-181">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a1b48-181">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a1b48-182">b.</span><span class="sxs-lookup"><span data-stu-id="a1b48-182">b.</span></span> <span data-ttu-id="a1b48-183">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a1b48-183">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="a1b48-184">c.</span><span class="sxs-lookup"><span data-stu-id="a1b48-184">c.</span></span> <span data-ttu-id="a1b48-185">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="a1b48-185">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="a1b48-186">d.</span><span class="sxs-lookup"><span data-stu-id="a1b48-186">d.</span></span> <span data-ttu-id="a1b48-187">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a1b48-187">Click **Create**.</span></span>
 
### <a name="create-a-efi-digital-storefront-test-user"></a><span data-ttu-id="a1b48-188">Create a EFI Digital StoreFront test user</span><span class="sxs-lookup"><span data-stu-id="a1b48-188">Create a EFI Digital StoreFront test user</span></span>

<span data-ttu-id="a1b48-189">In this section, you create a user called Britta Simon in EFI Digital StoreFront.</span><span class="sxs-lookup"><span data-stu-id="a1b48-189">In this section, you create a user called Britta Simon in EFI Digital StoreFront.</span></span> <span data-ttu-id="a1b48-190">Work with [EFI Digital StoreFront support team](http://www.efi.com/products/productivity-software/ecommerce-web-to-print/efi-digital-storefront/support/) to add the users in the EFI Digital StoreFront platform.</span><span class="sxs-lookup"><span data-stu-id="a1b48-190">Work with [EFI Digital StoreFront support team](http://www.efi.com/products/productivity-software/ecommerce-web-to-print/efi-digital-storefront/support/) to add the users in the EFI Digital StoreFront platform.</span></span> <span data-ttu-id="a1b48-191">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a1b48-191">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="a1b48-192">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a1b48-192">Assign the Azure AD test user</span></span>

<span data-ttu-id="a1b48-193">In this section, you enable Britta Simon to use Azure single sign-on by granting access to EFI Digital StoreFront.</span><span class="sxs-lookup"><span data-stu-id="a1b48-193">In this section, you enable Britta Simon to use Azure single sign-on by granting access to EFI Digital StoreFront.</span></span>

![Assign the user role][200] 

<span data-ttu-id="a1b48-195">**To assign Britta Simon to EFI Digital StoreFront, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a1b48-195">**To assign Britta Simon to EFI Digital StoreFront, perform the following steps:**</span></span>

1. <span data-ttu-id="a1b48-196">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a1b48-196">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="a1b48-198">In the applications list, select **EFI Digital StoreFront**.</span><span class="sxs-lookup"><span data-stu-id="a1b48-198">In the applications list, select **EFI Digital StoreFront**.</span></span>

    ![The EFI Digital StoreFront link in the Applications list](./media/efidigitalstorefront-tutorial/tutorial_efidigital_app.png)  

1. <span data-ttu-id="a1b48-200">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="a1b48-200">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="a1b48-202">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="a1b48-202">Click **Add** button.</span></span> <span data-ttu-id="a1b48-203">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a1b48-203">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="a1b48-205">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="a1b48-205">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="a1b48-206">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="a1b48-206">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="a1b48-207">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a1b48-207">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a1b48-208">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="a1b48-208">Test single sign-on</span></span>

<span data-ttu-id="a1b48-209">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a1b48-209">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a1b48-210">When you click the EFI Digital StoreFront tile in the Access Panel, you should get automatically signed-on to your EFI Digital StoreFront application.</span><span class="sxs-lookup"><span data-stu-id="a1b48-210">When you click the EFI Digital StoreFront tile in the Access Panel, you should get automatically signed-on to your EFI Digital StoreFront application.</span></span>
<span data-ttu-id="a1b48-211">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a1b48-211">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a1b48-212">Additional resources</span><span class="sxs-lookup"><span data-stu-id="a1b48-212">Additional resources</span></span>

* [<span data-ttu-id="a1b48-213">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a1b48-213">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="a1b48-214">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a1b48-214">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/efidigitalstorefront-tutorial/tutorial_general_01.png
[2]: ./media/efidigitalstorefront-tutorial/tutorial_general_02.png
[3]: ./media/efidigitalstorefront-tutorial/tutorial_general_03.png
[4]: ./media/efidigitalstorefront-tutorial/tutorial_general_04.png

[100]: ./media/efidigitalstorefront-tutorial/tutorial_general_100.png

[200]: ./media/efidigitalstorefront-tutorial/tutorial_general_200.png
[201]: ./media/efidigitalstorefront-tutorial/tutorial_general_201.png
[202]: ./media/efidigitalstorefront-tutorial/tutorial_general_202.png
[203]: ./media/efidigitalstorefront-tutorial/tutorial_general_203.png

