---
title: 'Tutorial: Azure Active Directory integration with Concur | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Concur.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 1eee0a5d-24fa-4986-9aef-3c543cfe3296
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: f26cd3df50d708e6dbc003e70462b70532947a00
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858074"
---
# <a name="tutorial-azure-active-directory-integration-with-concur"></a><span data-ttu-id="7b945-103">Tutorial: Azure Active Directory integration with Concur</span><span class="sxs-lookup"><span data-stu-id="7b945-103">Tutorial: Azure Active Directory integration with Concur</span></span>

<span data-ttu-id="7b945-104">In this tutorial, you learn how to integrate Concur with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7b945-104">In this tutorial, you learn how to integrate Concur with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7b945-105">Integrating Concur with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="7b945-105">Integrating Concur with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7b945-106">You can control in Azure AD who has access to Concur</span><span class="sxs-lookup"><span data-stu-id="7b945-106">You can control in Azure AD who has access to Concur</span></span>
- <span data-ttu-id="7b945-107">You can enable your users to automatically get signed-on to Concur (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="7b945-107">You can enable your users to automatically get signed-on to Concur (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7b945-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="7b945-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7b945-109">If you want to know more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="7b945-109">If you want to know more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b945-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7b945-110">Prerequisites</span></span>

<span data-ttu-id="7b945-111">To configure Azure AD integration with Concur, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="7b945-111">To configure Azure AD integration with Concur, you need the following items:</span></span>

- <span data-ttu-id="7b945-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="7b945-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7b945-113">A Concur single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="7b945-113">A Concur single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7b945-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="7b945-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7b945-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="7b945-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7b945-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="7b945-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7b945-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7b945-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7b945-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="7b945-118">Scenario description</span></span>
<span data-ttu-id="7b945-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="7b945-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7b945-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="7b945-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7b945-121">Adding Concur from the gallery</span><span class="sxs-lookup"><span data-stu-id="7b945-121">Adding Concur from the gallery</span></span>
1. <span data-ttu-id="7b945-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7b945-122">Configuring and testing Azure AD single sign-on</span></span>

>[!NOTE]
><span data-ttu-id="7b945-123">The configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact [Concur Client support team](https://www.concur.co.in/contact) to perform.</span><span class="sxs-lookup"><span data-stu-id="7b945-123">The configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact [Concur Client support team](https://www.concur.co.in/contact) to perform.</span></span> 

## <a name="adding-concur-from-the-gallery"></a><span data-ttu-id="7b945-124">Adding Concur from the gallery</span><span class="sxs-lookup"><span data-stu-id="7b945-124">Adding Concur from the gallery</span></span>
<span data-ttu-id="7b945-125">To configure the integration of Concur into Azure AD, you need to add Concur from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="7b945-125">To configure the integration of Concur into Azure AD, you need to add Concur from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7b945-126">**To add Concur from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7b945-126">**To add Concur from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7b945-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="7b945-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="7b945-129">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="7b945-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7b945-130">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="7b945-130">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="7b945-132">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="7b945-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="7b945-134">In the search box, type **Concur**.</span><span class="sxs-lookup"><span data-stu-id="7b945-134">In the search box, type **Concur**.</span></span>

    ![Creating an Azure AD test user](./media/concur-tutorial/tutorial_concur_search.png)

1. <span data-ttu-id="7b945-136">In the results panel, select **Concur**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="7b945-136">In the results panel, select **Concur**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/concur-tutorial/tutorial_concur_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7b945-138">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7b945-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7b945-139">In this section, you configure and test Azure AD single sign-on with Concur based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="7b945-139">In this section, you configure and test Azure AD single sign-on with Concur based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7b945-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Concur is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7b945-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Concur is to a user in Azure AD.</span></span> <span data-ttu-id="7b945-141">In other words, a link relationship between an Azure AD user and the related user in Concur needs to be established.</span><span class="sxs-lookup"><span data-stu-id="7b945-141">In other words, a link relationship between an Azure AD user and the related user in Concur needs to be established.</span></span>

<span data-ttu-id="7b945-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Concur.</span><span class="sxs-lookup"><span data-stu-id="7b945-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Concur.</span></span>

<span data-ttu-id="7b945-143">To configure and test Azure AD single sign-on with Concur, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="7b945-143">To configure and test Azure AD single sign-on with Concur, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7b945-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="7b945-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="7b945-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7b945-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="7b945-146">**[Creating a Concur test user](#creating-a-concur-test-user)** - to have a counterpart of Britta Simon in Concur that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="7b945-146">**[Creating a Concur test user](#creating-a-concur-test-user)** - to have a counterpart of Britta Simon in Concur that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="7b945-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7b945-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="7b945-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="7b945-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7b945-149">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7b945-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7b945-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Concur application.</span><span class="sxs-lookup"><span data-stu-id="7b945-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Concur application.</span></span>

<span data-ttu-id="7b945-151">**To configure Azure AD single sign-on with Concur, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7b945-151">**To configure Azure AD single sign-on with Concur, perform the following steps:**</span></span>

1. <span data-ttu-id="7b945-152">In the Azure portal, on the **Concur** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="7b945-152">In the Azure portal, on the **Concur** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="7b945-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7b945-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/concur-tutorial/tutorial_concur_samlbase.png)

1. <span data-ttu-id="7b945-156">On the **Concur Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7b945-156">On the **Concur Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/concur-tutorial/tutorial_concur_url.png)

    <span data-ttu-id="7b945-158">a.</span><span class="sxs-lookup"><span data-stu-id="7b945-158">a.</span></span> <span data-ttu-id="7b945-159">In the **Sign on URL** textbox, type the value using the following pattern: `https://www.concursolutions.com/UI/SSO/<OrganizationId>`</span><span class="sxs-lookup"><span data-stu-id="7b945-159">In the **Sign on URL** textbox, type the value using the following pattern: `https://www.concursolutions.com/UI/SSO/<OrganizationId>`</span></span>

    <span data-ttu-id="7b945-160">b.</span><span class="sxs-lookup"><span data-stu-id="7b945-160">b.</span></span> <span data-ttu-id="7b945-161">In the **Identifier** textbox, type a URL using the following pattern: `https://<customer-domain>.concursolutions.com`</span><span class="sxs-lookup"><span data-stu-id="7b945-161">In the **Identifier** textbox, type a URL using the following pattern: `https://<customer-domain>.concursolutions.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7b945-162">These values are not the real.</span><span class="sxs-lookup"><span data-stu-id="7b945-162">These values are not the real.</span></span> <span data-ttu-id="7b945-163">Update these values with the actual Sign on URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="7b945-163">Update these values with the actual Sign on URL and Identifier.</span></span> <span data-ttu-id="7b945-164">Contact [Concur Client support team](https://www.concur.co.in/contact) to get these values.</span><span class="sxs-lookup"><span data-stu-id="7b945-164">Contact [Concur Client support team](https://www.concur.co.in/contact) to get these values.</span></span> 

1. <span data-ttu-id="7b945-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span><span class="sxs-lookup"><span data-stu-id="7b945-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configure Single Sign-On](./media/concur-tutorial/tutorial_concur_certificate.png) 

1. <span data-ttu-id="7b945-167">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="7b945-167">Click **Save** button.</span></span>

    <span data-ttu-id="7b945-168">![Configure Single Sign-On](./media/concur-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="7b945-168">![Configure Single Sign-On](./media/concur-tutorial/tutorial_general_400.png)
<CS></span></span>

1. <span data-ttu-id="7b945-169">To configure single sign-on on **Concur** side, you need to send the downloaded **Metadata XML** to Concur support.</span><span class="sxs-lookup"><span data-stu-id="7b945-169">To configure single sign-on on **Concur** side, you need to send the downloaded **Metadata XML** to Concur support.</span></span> <span data-ttu-id="7b945-170">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="7b945-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

  >[!NOTE]
  ><span data-ttu-id="7b945-171">The configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact [Concur Client support team](https://www.concur.co.in/contact) to perform.</span><span class="sxs-lookup"><span data-stu-id="7b945-171">The configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact [Concur Client support team](https://www.concur.co.in/contact) to perform.</span></span> 
  
<CE>

> [!TIP]
> <span data-ttu-id="7b945-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="7b945-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7b945-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="7b945-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7b945-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7b945-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7b945-175">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7b945-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="7b945-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7b945-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="7b945-178">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7b945-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7b945-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="7b945-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/concur-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="7b945-181">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="7b945-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/concur-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="7b945-183">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="7b945-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/concur-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="7b945-185">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7b945-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/concur-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7b945-187">a.</span><span class="sxs-lookup"><span data-stu-id="7b945-187">a.</span></span> <span data-ttu-id="7b945-188">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7b945-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7b945-189">b.</span><span class="sxs-lookup"><span data-stu-id="7b945-189">b.</span></span> <span data-ttu-id="7b945-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7b945-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7b945-191">c.</span><span class="sxs-lookup"><span data-stu-id="7b945-191">c.</span></span> <span data-ttu-id="7b945-192">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="7b945-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7b945-193">d.</span><span class="sxs-lookup"><span data-stu-id="7b945-193">d.</span></span> <span data-ttu-id="7b945-194">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="7b945-194">Click **Create**.</span></span>
 
### <a name="creating-a-concur-test-user"></a><span data-ttu-id="7b945-195">Creating a Concur test user</span><span class="sxs-lookup"><span data-stu-id="7b945-195">Creating a Concur test user</span></span>

<span data-ttu-id="7b945-196">Application supports the Just in time user provisioning and after authentication users are created in the application automatically.</span><span class="sxs-lookup"><span data-stu-id="7b945-196">Application supports the Just in time user provisioning and after authentication users are created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7b945-197">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7b945-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7b945-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Concur.</span><span class="sxs-lookup"><span data-stu-id="7b945-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Concur.</span></span>

![Assign User][200] 

<span data-ttu-id="7b945-200">**To assign Britta Simon to Concur, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7b945-200">**To assign Britta Simon to Concur, perform the following steps:**</span></span>

1. <span data-ttu-id="7b945-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="7b945-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="7b945-203">In the applications list, select **Concur**.</span><span class="sxs-lookup"><span data-stu-id="7b945-203">In the applications list, select **Concur**.</span></span>

    ![Configure Single Sign-On](./media/concur-tutorial/tutorial_concur_app.png) 

1. <span data-ttu-id="7b945-205">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="7b945-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="7b945-207">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="7b945-207">Click **Add** button.</span></span> <span data-ttu-id="7b945-208">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="7b945-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="7b945-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="7b945-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="7b945-211">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="7b945-211">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="7b945-212">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="7b945-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7b945-213">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="7b945-213">Testing single sign-on</span></span>

<span data-ttu-id="7b945-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="7b945-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7b945-215">When you click the Concur tile in the Access Panel, you should get login page of Concur application.</span><span class="sxs-lookup"><span data-stu-id="7b945-215">When you click the Concur tile in the Access Panel, you should get login page of Concur application.</span></span>
<span data-ttu-id="7b945-216">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7b945-216">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7b945-217">Additional resources</span><span class="sxs-lookup"><span data-stu-id="7b945-217">Additional resources</span></span>

* [<span data-ttu-id="7b945-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7b945-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="7b945-219">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7b945-219">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)
* [<span data-ttu-id="7b945-220">Configure User Provisioning</span><span class="sxs-lookup"><span data-stu-id="7b945-220">Configure User Provisioning</span></span>](concur-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/concur-tutorial/tutorial_general_01.png
[2]: ./media/concur-tutorial/tutorial_general_02.png
[3]: ./media/concur-tutorial/tutorial_general_03.png
[4]: ./media/concur-tutorial/tutorial_general_04.png

[100]: ./media/concur-tutorial/tutorial_general_100.png

[200]: ./media/concur-tutorial/tutorial_general_200.png
[201]: ./media/concur-tutorial/tutorial_general_201.png
[202]: ./media/concur-tutorial/tutorial_general_202.png
[203]: ./media/concur-tutorial/tutorial_general_203.png

