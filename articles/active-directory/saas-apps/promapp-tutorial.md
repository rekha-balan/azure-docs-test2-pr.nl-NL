---
title: 'Tutorial: Azure Active Directory integration with Promapp | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Promapp.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 418d0601-6e7a-4997-a683-73fa30a2cfb5
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/17/2017
ms.author: jeedes
ms.openlocfilehash: 6bcd1add3985112fe60aab22f1799e40ad8889b2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867273"
---
# <a name="tutorial-azure-active-directory-integration-with-promapp"></a><span data-ttu-id="32606-103">Tutorial: Azure Active Directory integration with Promapp</span><span class="sxs-lookup"><span data-stu-id="32606-103">Tutorial: Azure Active Directory integration with Promapp</span></span>

<span data-ttu-id="32606-104">In this tutorial, you learn how to integrate Promapp with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="32606-104">In this tutorial, you learn how to integrate Promapp with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="32606-105">Integrating Promapp with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="32606-105">Integrating Promapp with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="32606-106">You can control in Azure AD who has access to Promapp</span><span class="sxs-lookup"><span data-stu-id="32606-106">You can control in Azure AD who has access to Promapp</span></span>
- <span data-ttu-id="32606-107">You can enable your users to automatically get signed-on to Promapp (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="32606-107">You can enable your users to automatically get signed-on to Promapp (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="32606-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="32606-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="32606-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="32606-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32606-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="32606-110">Prerequisites</span></span>

<span data-ttu-id="32606-111">To configure Azure AD integration with Promapp, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="32606-111">To configure Azure AD integration with Promapp, you need the following items:</span></span>

- <span data-ttu-id="32606-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="32606-112">An Azure AD subscription</span></span>
- <span data-ttu-id="32606-113">A Promapp single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="32606-113">A Promapp single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="32606-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="32606-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="32606-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="32606-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="32606-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="32606-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="32606-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="32606-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="32606-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="32606-118">Scenario description</span></span>
<span data-ttu-id="32606-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="32606-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="32606-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="32606-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="32606-121">Adding Promapp from the gallery</span><span class="sxs-lookup"><span data-stu-id="32606-121">Adding Promapp from the gallery</span></span>
1. <span data-ttu-id="32606-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="32606-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-promapp-from-the-gallery"></a><span data-ttu-id="32606-123">Adding Promapp from the gallery</span><span class="sxs-lookup"><span data-stu-id="32606-123">Adding Promapp from the gallery</span></span>
<span data-ttu-id="32606-124">To configure the integration of Promapp into Azure AD, you need to add Promapp from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="32606-124">To configure the integration of Promapp into Azure AD, you need to add Promapp from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="32606-125">**To add Promapp from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="32606-125">**To add Promapp from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="32606-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="32606-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="32606-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="32606-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="32606-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="32606-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="32606-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="32606-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="32606-133">In the search box, type **Promapp**.</span><span class="sxs-lookup"><span data-stu-id="32606-133">In the search box, type **Promapp**.</span></span>

    ![Creating an Azure AD test user](./media/promapp-tutorial/tutorial_promapp_search.png)

1. <span data-ttu-id="32606-135">In the results panel, select **Promapp**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="32606-135">In the results panel, select **Promapp**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/promapp-tutorial/tutorial_promapp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="32606-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="32606-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="32606-138">In this section, you configure and test Azure AD single sign-on with Promapp based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="32606-138">In this section, you configure and test Azure AD single sign-on with Promapp based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="32606-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Promapp is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32606-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Promapp is to a user in Azure AD.</span></span> <span data-ttu-id="32606-140">In other words, a link relationship between an Azure AD user and the related user in Promapp needs to be established.</span><span class="sxs-lookup"><span data-stu-id="32606-140">In other words, a link relationship between an Azure AD user and the related user in Promapp needs to be established.</span></span>

<span data-ttu-id="32606-141">In Promapp, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="32606-141">In Promapp, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="32606-142">To configure and test Azure AD single sign-on with Promapp, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="32606-142">To configure and test Azure AD single sign-on with Promapp, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="32606-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="32606-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="32606-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="32606-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="32606-145">**[Creating a Promapp test user](#creating-a-promapp-test-user)** - to have a counterpart of Britta Simon in Promapp that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="32606-145">**[Creating a Promapp test user](#creating-a-promapp-test-user)** - to have a counterpart of Britta Simon in Promapp that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="32606-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="32606-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="32606-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="32606-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="32606-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="32606-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="32606-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Promapp application.</span><span class="sxs-lookup"><span data-stu-id="32606-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Promapp application.</span></span>

<span data-ttu-id="32606-150">**To configure Azure AD single sign-on with Promapp, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="32606-150">**To configure Azure AD single sign-on with Promapp, perform the following steps:**</span></span>

1. <span data-ttu-id="32606-151">In the Azure portal, on the **Promapp** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="32606-151">In the Azure portal, on the **Promapp** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="32606-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="32606-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/promapp-tutorial/tutorial_promapp_samlbase.png)

1. <span data-ttu-id="32606-155">On the **Promapp Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="32606-155">On the **Promapp Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configure Single Sign-On](./media/promapp-tutorial/tutorial_promapp_url.png)

    <span data-ttu-id="32606-157">a.</span><span class="sxs-lookup"><span data-stu-id="32606-157">a.</span></span> <span data-ttu-id="32606-158">In the **Identifier** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="32606-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://go.promapp.com/TENANTNAME/`|
    | `https://au.promapp.com/TENANTNAME/`|
    | `https://us.promapp.com/TENANTNAME/`|
    | `https://eu.promapp.com/TENANTNAME/`|
    | `https://ca.promapp.com/TENANTNAME/`|
    
    > [!NOTE] 
    > <span data-ttu-id="32606-159">Presently Azure AD integration with Promapp has only been configured for service initiated authentication e.g. going to a Promapp URL initiates the authentication process.</span><span class="sxs-lookup"><span data-stu-id="32606-159">Presently Azure AD integration with Promapp has only been configured for service initiated authentication e.g. going to a Promapp URL initiates the authentication process.</span></span> <span data-ttu-id="32606-160">However the Reply URL is a required field.</span><span class="sxs-lookup"><span data-stu-id="32606-160">However the Reply URL is a required field.</span></span>
    
    <span data-ttu-id="32606-161">b.</span><span class="sxs-lookup"><span data-stu-id="32606-161">b.</span></span> <span data-ttu-id="32606-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://DOMAINNAME.promapp.com/azuread/saml/authenticate.aspx`</span><span class="sxs-lookup"><span data-stu-id="32606-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://DOMAINNAME.promapp.com/azuread/saml/authenticate.aspx`</span></span>

1. <span data-ttu-id="32606-163">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="32606-163">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configure Single Sign-On](./media/promapp-tutorial/tutorial_promapp_url1.png)

    <span data-ttu-id="32606-165">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://DOMAINNAME.promapp.com/TENANTNAME/saml/authenticate`</span><span class="sxs-lookup"><span data-stu-id="32606-165">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://DOMAINNAME.promapp.com/TENANTNAME/saml/authenticate`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="32606-166">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="32606-166">These values are not real.</span></span> <span data-ttu-id="32606-167">Update these values with the actual Sign-On URL, Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="32606-167">Update these values with the actual Sign-On URL, Identifier and Reply URL.</span></span> <span data-ttu-id="32606-168">Contact [Promapp Client support team](https://www.promapp.com/about-us/contact-us/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="32606-168">Contact [Promapp Client support team](https://www.promapp.com/about-us/contact-us/) to get these values.</span></span>

1. <span data-ttu-id="32606-169">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="32606-169">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/promapp-tutorial/tutorial_promapp_certificate.png) 

1. <span data-ttu-id="32606-171">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="32606-171">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/promapp-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="32606-173">On the **Promapp Configuration** section, click **Configure Promapp** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="32606-173">On the **Promapp Configuration** section, click **Configure Promapp** to open **Configure sign-on** window.</span></span> <span data-ttu-id="32606-174">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="32606-174">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/promapp-tutorial/tutorial_promapp_configure.png) 

1. <span data-ttu-id="32606-176">Sign-on to your Promapp company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="32606-176">Sign-on to your Promapp company site as administrator.</span></span> 

1. <span data-ttu-id="32606-177">In the menu on the top, click **Admin**.</span><span class="sxs-lookup"><span data-stu-id="32606-177">In the menu on the top, click **Admin**.</span></span> 
   
    ![Azure AD Single Sign-On][12]

1. <span data-ttu-id="32606-179">Click **Configure**.</span><span class="sxs-lookup"><span data-stu-id="32606-179">Click **Configure**.</span></span> 
   
    ![Azure AD Single Sign-On][13]

1. <span data-ttu-id="32606-181">On the **Security** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="32606-181">On the **Security** dialog, perform the following steps:</span></span>
   
    ![Azure AD Single Sign-On][14]
    
    <span data-ttu-id="32606-183">a.</span><span class="sxs-lookup"><span data-stu-id="32606-183">a.</span></span> <span data-ttu-id="32606-184">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **SSO-Login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="32606-184">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **SSO-Login URL** textbox.</span></span>
    
    <span data-ttu-id="32606-185">b.</span><span class="sxs-lookup"><span data-stu-id="32606-185">b.</span></span> <span data-ttu-id="32606-186">As **SSO - Single Sign-on Mode**, select **Optional**, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="32606-186">As **SSO - Single Sign-on Mode**, select **Optional**, and then click **Save**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="32606-187">**Optional** mode is for testing only.</span><span class="sxs-lookup"><span data-stu-id="32606-187">**Optional** mode is for testing only.</span></span> <span data-ttu-id="32606-188">Once you are happy with the configuration, Select **Required** mode to enforce all users to authenticate using Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32606-188">Once you are happy with the configuration, Select **Required** mode to enforce all users to authenticate using Azure AD.</span></span>

    <span data-ttu-id="32606-189">c.</span><span class="sxs-lookup"><span data-stu-id="32606-189">c.</span></span> <span data-ttu-id="32606-190">Open the downloaded certificate in notepad, copy the certificate content without the first line (-----**BEGIN CERTIFICATE**-----) and the last line (-----**END CERTIFICATE**-----), paste it into the **SSO-x.509 Certificate** textbox, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="32606-190">Open the downloaded certificate in notepad, copy the certificate content without the first line (-----**BEGIN CERTIFICATE**-----) and the last line (-----**END CERTIFICATE**-----), paste it into the **SSO-x.509 Certificate** textbox, and then click **Save**.</span></span>
        
> [!TIP]
> <span data-ttu-id="32606-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="32606-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="32606-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="32606-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="32606-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="32606-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="32606-194">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="32606-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="32606-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="32606-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="32606-197">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="32606-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="32606-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="32606-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/promapp-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="32606-200">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="32606-200">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/promapp-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="32606-202">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="32606-202">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/promapp-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="32606-204">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="32606-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/promapp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="32606-206">a.</span><span class="sxs-lookup"><span data-stu-id="32606-206">a.</span></span> <span data-ttu-id="32606-207">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="32606-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="32606-208">b.</span><span class="sxs-lookup"><span data-stu-id="32606-208">b.</span></span> <span data-ttu-id="32606-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="32606-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="32606-210">c.</span><span class="sxs-lookup"><span data-stu-id="32606-210">c.</span></span> <span data-ttu-id="32606-211">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="32606-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="32606-212">d.</span><span class="sxs-lookup"><span data-stu-id="32606-212">d.</span></span> <span data-ttu-id="32606-213">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="32606-213">Click **Create**.</span></span>
 
### <a name="creating-a-promapp-test-user"></a><span data-ttu-id="32606-214">Creating a Promapp test user</span><span class="sxs-lookup"><span data-stu-id="32606-214">Creating a Promapp test user</span></span>

<span data-ttu-id="32606-215">The Promapp application supports Just-in-Time provisioning.</span><span class="sxs-lookup"><span data-stu-id="32606-215">The Promapp application supports Just-in-Time provisioning.</span></span> <span data-ttu-id="32606-216">This means, a user account is automatically created if necessary during an attempt to access the application using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="32606-216">This means, a user account is automatically created if necessary during an attempt to access the application using the Access Panel.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="32606-217">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="32606-217">Assigning the Azure AD test user</span></span>

<span data-ttu-id="32606-218">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Promapp.</span><span class="sxs-lookup"><span data-stu-id="32606-218">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Promapp.</span></span>

![Assign User][200] 

<span data-ttu-id="32606-220">**To assign Britta Simon to Promapp, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="32606-220">**To assign Britta Simon to Promapp, perform the following steps:**</span></span>

1. <span data-ttu-id="32606-221">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="32606-221">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="32606-223">In the applications list, select **Promapp**.</span><span class="sxs-lookup"><span data-stu-id="32606-223">In the applications list, select **Promapp**.</span></span>

    ![Configure Single Sign-On](./media/promapp-tutorial/tutorial_promapp_app.png) 

1. <span data-ttu-id="32606-225">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="32606-225">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="32606-227">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="32606-227">Click **Add** button.</span></span> <span data-ttu-id="32606-228">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="32606-228">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="32606-230">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="32606-230">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="32606-231">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="32606-231">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="32606-232">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="32606-232">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="32606-233">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="32606-233">Testing single sign-on</span></span>

<span data-ttu-id="32606-234">To test your application in **SP** initiated mode, you will need to initiate the authentication from your Promapp site.</span><span class="sxs-lookup"><span data-stu-id="32606-234">To test your application in **SP** initiated mode, you will need to initiate the authentication from your Promapp site.</span></span> <span data-ttu-id="32606-235">This can be done by clicking the 'Login with Single Sign-on' button on your Login page whilst **Optional** mode is enabled.</span><span class="sxs-lookup"><span data-stu-id="32606-235">This can be done by clicking the 'Login with Single Sign-on' button on your Login page whilst **Optional** mode is enabled.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="32606-236">Additional resources</span><span class="sxs-lookup"><span data-stu-id="32606-236">Additional resources</span></span>

* [<span data-ttu-id="32606-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="32606-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="32606-238">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="32606-238">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/promapp-tutorial/tutorial_general_01.png
[2]: ./media/promapp-tutorial/tutorial_general_02.png
[3]: ./media/promapp-tutorial/tutorial_general_03.png
[4]: ./media/promapp-tutorial/tutorial_general_04.png
[12]: ./media/promapp-tutorial/tutorial_promapp_05.png
[13]: ./media/promapp-tutorial/tutorial_promapp_06.png
[14]: ./media/promapp-tutorial/tutorial_promapp_07.png

[100]: ./media/promapp-tutorial/tutorial_general_100.png

[200]: ./media/promapp-tutorial/tutorial_general_200.png
[201]: ./media/promapp-tutorial/tutorial_general_201.png
[202]: ./media/promapp-tutorial/tutorial_general_202.png
[203]: ./media/promapp-tutorial/tutorial_general_203.png

