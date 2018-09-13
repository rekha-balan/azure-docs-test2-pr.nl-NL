---
title: 'Tutorial: Azure Active Directory integration with Hightail | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Hightail.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: e15206ac-74b0-46e4-9329-892c7d242ec0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2018
ms.author: jeedes
ms.openlocfilehash: 1151044d5c1002c808ae1214086aff5fad84a55e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864516"
---
# <a name="tutorial-azure-active-directory-integration-with-hightail"></a><span data-ttu-id="74176-103">Tutorial: Azure Active Directory integration with Hightail</span><span class="sxs-lookup"><span data-stu-id="74176-103">Tutorial: Azure Active Directory integration with Hightail</span></span>

<span data-ttu-id="74176-104">In this tutorial, you learn how to integrate Hightail with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="74176-104">In this tutorial, you learn how to integrate Hightail with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="74176-105">Integrating Hightail with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="74176-105">Integrating Hightail with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="74176-106">You can control in Azure AD who has access to Hightail</span><span class="sxs-lookup"><span data-stu-id="74176-106">You can control in Azure AD who has access to Hightail</span></span>
- <span data-ttu-id="74176-107">You can enable your users to automatically get signed-on to Hightail (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="74176-107">You can enable your users to automatically get signed-on to Hightail (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="74176-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="74176-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="74176-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="74176-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="74176-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="74176-110">Prerequisites</span></span>

<span data-ttu-id="74176-111">To configure Azure AD integration with Hightail, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="74176-111">To configure Azure AD integration with Hightail, you need the following items:</span></span>

- <span data-ttu-id="74176-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="74176-112">An Azure AD subscription</span></span>
- <span data-ttu-id="74176-113">A Hightail single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="74176-113">A Hightail single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="74176-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="74176-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="74176-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="74176-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="74176-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="74176-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="74176-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="74176-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="74176-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="74176-118">Scenario description</span></span>
<span data-ttu-id="74176-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="74176-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="74176-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="74176-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="74176-121">Adding Hightail from the gallery</span><span class="sxs-lookup"><span data-stu-id="74176-121">Adding Hightail from the gallery</span></span>
1. <span data-ttu-id="74176-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="74176-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hightail-from-the-gallery"></a><span data-ttu-id="74176-123">Adding Hightail from the gallery</span><span class="sxs-lookup"><span data-stu-id="74176-123">Adding Hightail from the gallery</span></span>
<span data-ttu-id="74176-124">To configure the integration of Hightail into Azure AD, you need to add Hightail from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="74176-124">To configure the integration of Hightail into Azure AD, you need to add Hightail from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="74176-125">**To add Hightail from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="74176-125">**To add Hightail from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="74176-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="74176-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="74176-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="74176-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="74176-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="74176-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="74176-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="74176-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="74176-133">In the search box, type **Hightail**.</span><span class="sxs-lookup"><span data-stu-id="74176-133">In the search box, type **Hightail**.</span></span>

    ![Creating an Azure AD test user](./media/hightail-tutorial/tutorial_hightail_search.png)

1. <span data-ttu-id="74176-135">In the results panel, select **Hightail**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="74176-135">In the results panel, select **Hightail**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/hightail-tutorial/tutorial_hightail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="74176-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="74176-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="74176-138">In this section, you configure and test Azure AD single sign-on with Hightail based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="74176-138">In this section, you configure and test Azure AD single sign-on with Hightail based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="74176-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Hightail is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="74176-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Hightail is to a user in Azure AD.</span></span> <span data-ttu-id="74176-140">In other words, a link relationship between an Azure AD user and the related user in Hightail needs to be established.</span><span class="sxs-lookup"><span data-stu-id="74176-140">In other words, a link relationship between an Azure AD user and the related user in Hightail needs to be established.</span></span>

<span data-ttu-id="74176-141">In Hightail, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="74176-141">In Hightail, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="74176-142">To configure and test Azure AD single sign-on with Hightail, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="74176-142">To configure and test Azure AD single sign-on with Hightail, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="74176-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="74176-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="74176-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="74176-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="74176-145">**[Creating a Hightail test user](#creating-a-hightail-test-user)** - to have a counterpart of Britta Simon in Hightail that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="74176-145">**[Creating a Hightail test user](#creating-a-hightail-test-user)** - to have a counterpart of Britta Simon in Hightail that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="74176-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="74176-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="74176-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="74176-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="74176-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="74176-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="74176-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Hightail application.</span><span class="sxs-lookup"><span data-stu-id="74176-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Hightail application.</span></span>

<span data-ttu-id="74176-150">**To configure Azure AD single sign-on with Hightail, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="74176-150">**To configure Azure AD single sign-on with Hightail, perform the following steps:**</span></span>

1. <span data-ttu-id="74176-151">In the Azure portal, on the **Hightail** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="74176-151">In the Azure portal, on the **Hightail** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="74176-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="74176-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Configure Single Sign-On](./media/hightail-tutorial/tutorial_hightail_samlbase.png)

1. <span data-ttu-id="74176-155">On the **Hightail Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="74176-155">On the **Hightail Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configure Single Sign-On](./media/hightail-tutorial/tutorial_hightail_url.png)

    <span data-ttu-id="74176-157">In the **Reply URL** textbox, type the URL as: `https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`</span><span class="sxs-lookup"><span data-stu-id="74176-157">In the **Reply URL** textbox, type the URL as: `https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`</span></span>

    > [!NOTE]
    > <span data-ttu-id="74176-158">The Reply URL value is not real value.</span><span class="sxs-lookup"><span data-stu-id="74176-158">The Reply URL value is not real value.</span></span> <span data-ttu-id="74176-159">You will update the Reply URL value with the actual Reply URL, which is explained later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="74176-159">You will update the Reply URL value with the actual Reply URL, which is explained later in the tutorial.</span></span>

1. <span data-ttu-id="74176-160">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="74176-160">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configure Single Sign-On](./media/hightail-tutorial/tutorial_hightail_url1.png)

    <span data-ttu-id="74176-162">In the **Sign On URL** textbox, type the URL as: `https://www.hightail.com/loginSSO`</span><span class="sxs-lookup"><span data-stu-id="74176-162">In the **Sign On URL** textbox, type the URL as: `https://www.hightail.com/loginSSO`</span></span>

1. <span data-ttu-id="74176-163">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="74176-163">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/hightail-tutorial/tutorial_hightail_certificate.png) 

1. <span data-ttu-id="74176-165">Hightail application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="74176-165">Hightail application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="74176-166">Please configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="74176-166">Please configure the following claims for this application.</span></span> <span data-ttu-id="74176-167">You can manage the values of these attributes from the **"Attribute"** tab of the application.</span><span class="sxs-lookup"><span data-stu-id="74176-167">You can manage the values of these attributes from the **"Attribute"** tab of the application.</span></span> <span data-ttu-id="74176-168">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="74176-168">The following screenshot shows an example for this.</span></span> 

    ![Configure Single Sign-On](./media/hightail-tutorial/tutorial_hightail_attribute.png) 

1. <span data-ttu-id="74176-170">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="74176-170">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="74176-171">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="74176-171">Attribute Name</span></span> | <span data-ttu-id="74176-172">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="74176-172">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="74176-173">FirstName</span><span class="sxs-lookup"><span data-stu-id="74176-173">FirstName</span></span> | <span data-ttu-id="74176-174">user.givenname</span><span class="sxs-lookup"><span data-stu-id="74176-174">user.givenname</span></span> |
    | <span data-ttu-id="74176-175">LastName</span><span class="sxs-lookup"><span data-stu-id="74176-175">LastName</span></span> | <span data-ttu-id="74176-176">user.surname</span><span class="sxs-lookup"><span data-stu-id="74176-176">user.surname</span></span> |
    | <span data-ttu-id="74176-177">Email</span><span class="sxs-lookup"><span data-stu-id="74176-177">Email</span></span> | <span data-ttu-id="74176-178">user.mail</span><span class="sxs-lookup"><span data-stu-id="74176-178">user.mail</span></span> |    
    | <span data-ttu-id="74176-179">UserIdentity</span><span class="sxs-lookup"><span data-stu-id="74176-179">UserIdentity</span></span> | <span data-ttu-id="74176-180">user.mail</span><span class="sxs-lookup"><span data-stu-id="74176-180">user.mail</span></span> |
    
    <span data-ttu-id="74176-181">a.</span><span class="sxs-lookup"><span data-stu-id="74176-181">a.</span></span> <span data-ttu-id="74176-182">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="74176-182">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/hightail-tutorial/tutorial_officespace_04.png)

    ![Configure Single Sign-On](./media/hightail-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="74176-185">b.</span><span class="sxs-lookup"><span data-stu-id="74176-185">b.</span></span> <span data-ttu-id="74176-186">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="74176-186">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="74176-187">c.</span><span class="sxs-lookup"><span data-stu-id="74176-187">c.</span></span> <span data-ttu-id="74176-188">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="74176-188">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="74176-189">d.</span><span class="sxs-lookup"><span data-stu-id="74176-189">d.</span></span> <span data-ttu-id="74176-190">Leave the **Namespace** blank.</span><span class="sxs-lookup"><span data-stu-id="74176-190">Leave the **Namespace** blank.</span></span>

    <span data-ttu-id="74176-191">e.</span><span class="sxs-lookup"><span data-stu-id="74176-191">e.</span></span> <span data-ttu-id="74176-192">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="74176-192">Click **Ok**.</span></span>

1. <span data-ttu-id="74176-193">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="74176-193">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/hightail-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="74176-195">On the **Hightail Configuration** section, click **Configure Hightail** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="74176-195">On the **Hightail Configuration** section, click **Configure Hightail** to open **Configure sign-on** window.</span></span> <span data-ttu-id="74176-196">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="74176-196">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/hightail-tutorial/tutorial_hightail_configure.png)

    >[!NOTE]
    ><span data-ttu-id="74176-198">Before configuring the Single Sign On at Hightail app, please white list your email domain with Hightail team so that all the users who are using this domain can use Single Sign On functionality.</span><span class="sxs-lookup"><span data-stu-id="74176-198">Before configuring the Single Sign On at Hightail app, please white list your email domain with Hightail team so that all the users who are using this domain can use Single Sign On functionality.</span></span>

1. <span data-ttu-id="74176-199">In another browser window, open the **Hightail** admin portal.</span><span class="sxs-lookup"><span data-stu-id="74176-199">In another browser window, open the **Hightail** admin portal.</span></span>

1. <span data-ttu-id="74176-200">Click on **User icon** from the top right corner of the page.</span><span class="sxs-lookup"><span data-stu-id="74176-200">Click on **User icon** from the top right corner of the page.</span></span> 

    ![Configure Single Sign-On](./media/hightail-tutorial/configure1.png)

1. <span data-ttu-id="74176-202">Click **View Admin Console** tab.</span><span class="sxs-lookup"><span data-stu-id="74176-202">Click **View Admin Console** tab.</span></span>

    ![Configure Single Sign-On](./media/hightail-tutorial/configure2.png)

1. <span data-ttu-id="74176-204">In the menu on the top, click the **SAML** tab and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="74176-204">In the menu on the top, click the **SAML** tab and perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/hightail-tutorial/configure3.png)

    <span data-ttu-id="74176-206">a.</span><span class="sxs-lookup"><span data-stu-id="74176-206">a.</span></span> <span data-ttu-id="74176-207">In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="74176-207">In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** copied from Azure portal.</span></span>

    <span data-ttu-id="74176-208">b.</span><span class="sxs-lookup"><span data-stu-id="74176-208">b.</span></span> <span data-ttu-id="74176-209">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **SAML Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="74176-209">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **SAML Certificate** textbox.</span></span>

    <span data-ttu-id="74176-210">c.</span><span class="sxs-lookup"><span data-stu-id="74176-210">c.</span></span> <span data-ttu-id="74176-211">Click **COPY** to copy the SAML consumer URL for your instance and paste it in **Reply URL** textbox in **Hightail Domain and URLs** section on Azure portal.</span><span class="sxs-lookup"><span data-stu-id="74176-211">Click **COPY** to copy the SAML consumer URL for your instance and paste it in **Reply URL** textbox in **Hightail Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="74176-212">d.</span><span class="sxs-lookup"><span data-stu-id="74176-212">d.</span></span> <span data-ttu-id="74176-213">Click **Save Configurations**.</span><span class="sxs-lookup"><span data-stu-id="74176-213">Click **Save Configurations**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="74176-214">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="74176-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="74176-215">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="74176-215">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="74176-217">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="74176-217">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="74176-218">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="74176-218">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/hightail-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="74176-220">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="74176-220">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/hightail-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="74176-222">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="74176-222">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/hightail-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="74176-224">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="74176-224">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/hightail-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="74176-226">a.</span><span class="sxs-lookup"><span data-stu-id="74176-226">a.</span></span> <span data-ttu-id="74176-227">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="74176-227">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="74176-228">b.</span><span class="sxs-lookup"><span data-stu-id="74176-228">b.</span></span> <span data-ttu-id="74176-229">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="74176-229">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="74176-230">c.</span><span class="sxs-lookup"><span data-stu-id="74176-230">c.</span></span> <span data-ttu-id="74176-231">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="74176-231">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="74176-232">d.</span><span class="sxs-lookup"><span data-stu-id="74176-232">d.</span></span> <span data-ttu-id="74176-233">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="74176-233">Click **Create**.</span></span>
 
### <a name="creating-a-hightail-test-user"></a><span data-ttu-id="74176-234">Creating a Hightail test user</span><span class="sxs-lookup"><span data-stu-id="74176-234">Creating a Hightail test user</span></span>

<span data-ttu-id="74176-235">The objective of this section is to create a user called Britta Simon in Hightail.</span><span class="sxs-lookup"><span data-stu-id="74176-235">The objective of this section is to create a user called Britta Simon in Hightail.</span></span> 

<span data-ttu-id="74176-236">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="74176-236">There is no action item for you in this section.</span></span> <span data-ttu-id="74176-237">Hightail supports just-in-time user provisioning based on the custom claims.</span><span class="sxs-lookup"><span data-stu-id="74176-237">Hightail supports just-in-time user provisioning based on the custom claims.</span></span> <span data-ttu-id="74176-238">If you have configured the custom claims as shown in the section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** above, a user is automatically created in the application it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="74176-238">If you have configured the custom claims as shown in the section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** above, a user is automatically created in the application it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="74176-239">If you need to create a user manually, you need to contact the [Hightail support team](mailto:support@hightail.com).</span><span class="sxs-lookup"><span data-stu-id="74176-239">If you need to create a user manually, you need to contact the [Hightail support team](mailto:support@hightail.com).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="74176-240">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="74176-240">Assigning the Azure AD test user</span></span>

<span data-ttu-id="74176-241">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Hightail.</span><span class="sxs-lookup"><span data-stu-id="74176-241">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Hightail.</span></span>

![Assign User][200] 

<span data-ttu-id="74176-243">**To assign Britta Simon to Hightail, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="74176-243">**To assign Britta Simon to Hightail, perform the following steps:**</span></span>

1. <span data-ttu-id="74176-244">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="74176-244">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="74176-246">In the applications list, select **Hightail**.</span><span class="sxs-lookup"><span data-stu-id="74176-246">In the applications list, select **Hightail**.</span></span>

    ![Configure Single Sign-On](./media/hightail-tutorial/tutorial_hightail_app.png) 

1. <span data-ttu-id="74176-248">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="74176-248">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202]

1. <span data-ttu-id="74176-250">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="74176-250">Click **Add** button.</span></span> <span data-ttu-id="74176-251">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="74176-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="74176-253">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="74176-253">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="74176-254">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="74176-254">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="74176-255">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="74176-255">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="74176-256">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="74176-256">Testing single sign-on</span></span>

<span data-ttu-id="74176-257">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="74176-257">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="74176-258">When you click the Hightail tile in the Access Panel, you should get automatically signed-on to your Hightail application.</span><span class="sxs-lookup"><span data-stu-id="74176-258">When you click the Hightail tile in the Access Panel, you should get automatically signed-on to your Hightail application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="74176-259">Additional resources</span><span class="sxs-lookup"><span data-stu-id="74176-259">Additional resources</span></span>

* [<span data-ttu-id="74176-260">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="74176-260">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="74176-261">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="74176-261">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/hightail-tutorial/tutorial_general_01.png
[2]: ./media/hightail-tutorial/tutorial_general_02.png
[3]: ./media/hightail-tutorial/tutorial_general_03.png
[4]: ./media/hightail-tutorial/tutorial_general_04.png

[100]: ./media/hightail-tutorial/tutorial_general_100.png

[200]: ./media/hightail-tutorial/tutorial_general_200.png
[201]: ./media/hightail-tutorial/tutorial_general_201.png
[202]: ./media/hightail-tutorial/tutorial_general_202.png
[203]: ./media/hightail-tutorial/tutorial_general_203.png

