---
title: 'Tutorial: Azure Active Directory integration with ASC Contracts | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and ASC Contracts.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: f7f54202-1581-4e55-a97e-02633ff9382d
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/21/2017
ms.author: jeedes
ms.openlocfilehash: f5eaa61af2c44265f36662e8a3b1f8ff8a747afe
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865341"
---
# <a name="tutorial-azure-active-directory-integration-with-asc-contracts"></a><span data-ttu-id="35b12-103">Tutorial: Azure Active Directory integration with ASC Contracts</span><span class="sxs-lookup"><span data-stu-id="35b12-103">Tutorial: Azure Active Directory integration with ASC Contracts</span></span>

<span data-ttu-id="35b12-104">In this tutorial, you learn how to integrate ASC Contracts with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="35b12-104">In this tutorial, you learn how to integrate ASC Contracts with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="35b12-105">Integrating ASC Contracts with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="35b12-105">Integrating ASC Contracts with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="35b12-106">You can control in Azure AD who has access to ASC Contracts</span><span class="sxs-lookup"><span data-stu-id="35b12-106">You can control in Azure AD who has access to ASC Contracts</span></span>
- <span data-ttu-id="35b12-107">You can enable your users to automatically get signed-on to ASC Contracts (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="35b12-107">You can enable your users to automatically get signed-on to ASC Contracts (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="35b12-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="35b12-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="35b12-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="35b12-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35b12-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="35b12-110">Prerequisites</span></span>

<span data-ttu-id="35b12-111">To configure Azure AD integration with ASC Contracts, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="35b12-111">To configure Azure AD integration with ASC Contracts, you need the following items:</span></span>

- <span data-ttu-id="35b12-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="35b12-112">An Azure AD subscription</span></span>
- <span data-ttu-id="35b12-113">An ASC Contracts single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="35b12-113">An ASC Contracts single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="35b12-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="35b12-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="35b12-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="35b12-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="35b12-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="35b12-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="35b12-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="35b12-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="35b12-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="35b12-118">Scenario description</span></span>
<span data-ttu-id="35b12-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="35b12-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="35b12-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="35b12-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="35b12-121">Adding ASC Contracts from the gallery</span><span class="sxs-lookup"><span data-stu-id="35b12-121">Adding ASC Contracts from the gallery</span></span>
1. <span data-ttu-id="35b12-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="35b12-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-asc-contracts-from-the-gallery"></a><span data-ttu-id="35b12-123">Adding ASC Contracts from the gallery</span><span class="sxs-lookup"><span data-stu-id="35b12-123">Adding ASC Contracts from the gallery</span></span>
<span data-ttu-id="35b12-124">To configure the integration of ASC Contracts into Azure AD, you need to add ASC Contracts from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="35b12-124">To configure the integration of ASC Contracts into Azure AD, you need to add ASC Contracts from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="35b12-125">**To add ASC Contracts from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="35b12-125">**To add ASC Contracts from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="35b12-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="35b12-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="35b12-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="35b12-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="35b12-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="35b12-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="35b12-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="35b12-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="35b12-133">In the search box, type **ASC Contracts**.</span><span class="sxs-lookup"><span data-stu-id="35b12-133">In the search box, type **ASC Contracts**.</span></span>

    ![Creating an Azure AD test user](./media/asccontracts-tutorial/tutorial_asccontracts_search.png)

1. <span data-ttu-id="35b12-135">In the results panel, select **ASC Contracts**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="35b12-135">In the results panel, select **ASC Contracts**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/asccontracts-tutorial/tutorial_asccontracts_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="35b12-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="35b12-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="35b12-138">In this section, you configure and test Azure AD single sign-on with ASC Contracts based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="35b12-138">In this section, you configure and test Azure AD single sign-on with ASC Contracts based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="35b12-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ASC Contracts is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="35b12-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ASC Contracts is to a user in Azure AD.</span></span> <span data-ttu-id="35b12-140">In other words, a link relationship between an Azure AD user and the related user in ASC Contracts needs to be established.</span><span class="sxs-lookup"><span data-stu-id="35b12-140">In other words, a link relationship between an Azure AD user and the related user in ASC Contracts needs to be established.</span></span>

<span data-ttu-id="35b12-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ASC Contracts.</span><span class="sxs-lookup"><span data-stu-id="35b12-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ASC Contracts.</span></span>

<span data-ttu-id="35b12-142">To configure and test Azure AD single sign-on with ASC Contracts, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="35b12-142">To configure and test Azure AD single sign-on with ASC Contracts, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="35b12-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="35b12-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="35b12-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="35b12-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="35b12-145">**[Creating an ASC Contracts test user](#creating-an-asc-contracts-test-user)** - to have a counterpart of Britta Simon in ASC Contracts that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="35b12-145">**[Creating an ASC Contracts test user](#creating-an-asc-contracts-test-user)** - to have a counterpart of Britta Simon in ASC Contracts that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="35b12-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="35b12-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="35b12-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="35b12-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="35b12-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="35b12-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="35b12-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ASC Contracts application.</span><span class="sxs-lookup"><span data-stu-id="35b12-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ASC Contracts application.</span></span>

<span data-ttu-id="35b12-150">**To configure Azure AD single sign-on with ASC Contracts, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="35b12-150">**To configure Azure AD single sign-on with ASC Contracts, perform the following steps:**</span></span>

1. <span data-ttu-id="35b12-151">In the Azure portal, on the **ASC Contracts** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="35b12-151">In the Azure portal, on the **ASC Contracts** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="35b12-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="35b12-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/asccontracts-tutorial/tutorial_asccontracts_samlbase.png)

1. <span data-ttu-id="35b12-155">On the **ASC Contracts Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="35b12-155">On the **ASC Contracts Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/asccontracts-tutorial/tutorial_asccontracts_url.png)

    <span data-ttu-id="35b12-157">a.</span><span class="sxs-lookup"><span data-stu-id="35b12-157">a.</span></span> <span data-ttu-id="35b12-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.asccontracts.com/shibboleth`</span><span class="sxs-lookup"><span data-stu-id="35b12-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.asccontracts.com/shibboleth`</span></span>

    <span data-ttu-id="35b12-159">b.</span><span class="sxs-lookup"><span data-stu-id="35b12-159">b.</span></span> <span data-ttu-id="35b12-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.asccontracts.com/shibboleth.sso/login`</span><span class="sxs-lookup"><span data-stu-id="35b12-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.asccontracts.com/shibboleth.sso/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="35b12-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="35b12-161">These values are not real.</span></span> <span data-ttu-id="35b12-162">Update these values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="35b12-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="35b12-163">Contact ASC Networks Inc. (ASC) team at **613.599.6178** to get these values.</span><span class="sxs-lookup"><span data-stu-id="35b12-163">Contact ASC Networks Inc. (ASC) team at **613.599.6178** to get these values.</span></span>

1. <span data-ttu-id="35b12-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="35b12-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/asccontracts-tutorial/tutorial_asccontracts_certificate.png) 

1. <span data-ttu-id="35b12-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="35b12-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/asccontracts-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="35b12-168">To configure single sign-on on **ASC Contracts** side, call ASC Networks Inc. (ASC) support at **613.599.6178** and provide them with the downloaded **Metadata XML**.</span><span class="sxs-lookup"><span data-stu-id="35b12-168">To configure single sign-on on **ASC Contracts** side, call ASC Networks Inc. (ASC) support at **613.599.6178** and provide them with the downloaded **Metadata XML**.</span></span> <span data-ttu-id="35b12-169">They set this application up to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="35b12-169">They set this application up to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="35b12-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="35b12-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="35b12-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="35b12-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="35b12-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="35b12-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="35b12-173">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="35b12-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="35b12-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="35b12-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="35b12-176">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="35b12-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="35b12-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="35b12-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/asccontracts-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="35b12-179">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="35b12-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/asccontracts-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="35b12-181">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="35b12-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/asccontracts-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="35b12-183">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="35b12-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/asccontracts-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="35b12-185">a.</span><span class="sxs-lookup"><span data-stu-id="35b12-185">a.</span></span> <span data-ttu-id="35b12-186">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="35b12-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="35b12-187">b.</span><span class="sxs-lookup"><span data-stu-id="35b12-187">b.</span></span> <span data-ttu-id="35b12-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="35b12-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="35b12-189">c.</span><span class="sxs-lookup"><span data-stu-id="35b12-189">c.</span></span> <span data-ttu-id="35b12-190">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="35b12-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="35b12-191">d.</span><span class="sxs-lookup"><span data-stu-id="35b12-191">d.</span></span> <span data-ttu-id="35b12-192">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="35b12-192">Click **Create**.</span></span>
 
### <a name="creating-an-asc-contracts-test-user"></a><span data-ttu-id="35b12-193">Creating an ASC Contracts test user</span><span class="sxs-lookup"><span data-stu-id="35b12-193">Creating an ASC Contracts test user</span></span>

<span data-ttu-id="35b12-194">Work with ASC Networks Inc. (ASC) support team at **613.599.6178** to get the users added in the ASC Contracts platform.</span><span class="sxs-lookup"><span data-stu-id="35b12-194">Work with ASC Networks Inc. (ASC) support team at **613.599.6178** to get the users added in the ASC Contracts platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="35b12-195">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="35b12-195">Assigning the Azure AD test user</span></span>

<span data-ttu-id="35b12-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ASC Contracts.</span><span class="sxs-lookup"><span data-stu-id="35b12-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ASC Contracts.</span></span>

![Assign User][200] 

<span data-ttu-id="35b12-198">**To assign Britta Simon to ASC Contracts, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="35b12-198">**To assign Britta Simon to ASC Contracts, perform the following steps:**</span></span>

1. <span data-ttu-id="35b12-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="35b12-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="35b12-201">In the applications list, select **ASC Contracts**.</span><span class="sxs-lookup"><span data-stu-id="35b12-201">In the applications list, select **ASC Contracts**.</span></span>

    ![Configure Single Sign-On](./media/asccontracts-tutorial/tutorial_asccontracts_app.png) 

1. <span data-ttu-id="35b12-203">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="35b12-203">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="35b12-205">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="35b12-205">Click **Add** button.</span></span> <span data-ttu-id="35b12-206">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="35b12-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="35b12-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="35b12-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="35b12-209">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="35b12-209">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="35b12-210">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="35b12-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="35b12-211">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="35b12-211">Testing single sign-on</span></span>

<span data-ttu-id="35b12-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="35b12-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="35b12-213">When you click the ASC Contracts tile in the Access Panel, you should get automatically signed-on to your ASC Contracts application.</span><span class="sxs-lookup"><span data-stu-id="35b12-213">When you click the ASC Contracts tile in the Access Panel, you should get automatically signed-on to your ASC Contracts application.</span></span> <span data-ttu-id="35b12-214">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="35b12-214">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="35b12-215">Additional resources</span><span class="sxs-lookup"><span data-stu-id="35b12-215">Additional resources</span></span>

* [<span data-ttu-id="35b12-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="35b12-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="35b12-217">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="35b12-217">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/asccontracts-tutorial/tutorial_general_01.png
[2]: ./media/asccontracts-tutorial/tutorial_general_02.png
[3]: ./media/asccontracts-tutorial/tutorial_general_03.png
[4]: ./media/asccontracts-tutorial/tutorial_general_04.png

[100]: ./media/asccontracts-tutorial/tutorial_general_100.png

[200]: ./media/asccontracts-tutorial/tutorial_general_200.png
[201]: ./media/asccontracts-tutorial/tutorial_general_201.png
[202]: ./media/asccontracts-tutorial/tutorial_general_202.png
[203]: ./media/asccontracts-tutorial/tutorial_general_203.png
