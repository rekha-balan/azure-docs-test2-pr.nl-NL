---
title: 'Tutorial: Azure Active Directory integration with Leapsome | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Leapsome.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: cb523e97-add8-4289-b106-927bf1a02188
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2018
ms.author: jeedes
ms.openlocfilehash: e55d161b7c95118736f4443c3fed0312418feee7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868023"
---
# <a name="tutorial-azure-active-directory-integration-with-leapsome"></a><span data-ttu-id="371be-103">Tutorial: Azure Active Directory integration with Leapsome</span><span class="sxs-lookup"><span data-stu-id="371be-103">Tutorial: Azure Active Directory integration with Leapsome</span></span>

<span data-ttu-id="371be-104">In this tutorial, you learn how to integrate Leapsome with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="371be-104">In this tutorial, you learn how to integrate Leapsome with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="371be-105">Integrating Leapsome with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="371be-105">Integrating Leapsome with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="371be-106">You can control in Azure AD who has access to Leapsome.</span><span class="sxs-lookup"><span data-stu-id="371be-106">You can control in Azure AD who has access to Leapsome.</span></span>
- <span data-ttu-id="371be-107">You can enable your users to automatically get signed-on to Leapsome (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="371be-107">You can enable your users to automatically get signed-on to Leapsome (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="371be-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="371be-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="371be-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="371be-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="371be-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="371be-110">Prerequisites</span></span>

<span data-ttu-id="371be-111">To configure Azure AD integration with Leapsome, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="371be-111">To configure Azure AD integration with Leapsome, you need the following items:</span></span>

- <span data-ttu-id="371be-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="371be-112">An Azure AD subscription</span></span>
- <span data-ttu-id="371be-113">A Leapsome single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="371be-113">A Leapsome single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="371be-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="371be-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="371be-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="371be-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="371be-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="371be-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="371be-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="371be-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="371be-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="371be-118">Scenario description</span></span>
<span data-ttu-id="371be-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="371be-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="371be-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="371be-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="371be-121">Adding Leapsome from the gallery</span><span class="sxs-lookup"><span data-stu-id="371be-121">Adding Leapsome from the gallery</span></span>
1. <span data-ttu-id="371be-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="371be-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-leapsome-from-the-gallery"></a><span data-ttu-id="371be-123">Adding Leapsome from the gallery</span><span class="sxs-lookup"><span data-stu-id="371be-123">Adding Leapsome from the gallery</span></span>
<span data-ttu-id="371be-124">To configure the integration of Leapsome into Azure AD, you need to add Leapsome from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="371be-124">To configure the integration of Leapsome into Azure AD, you need to add Leapsome from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="371be-125">**To add Leapsome from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="371be-125">**To add Leapsome from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="371be-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="371be-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="371be-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="371be-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="371be-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="371be-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="371be-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="371be-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="371be-133">In the search box, type **Leapsome**, select **Leapsome** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="371be-133">In the search box, type **Leapsome**, select **Leapsome** from result panel then click **Add** button to add the application.</span></span>

    ![Leapsome in the results list](./media/leapsome-tutorial/tutorial_leapsome_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="371be-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="371be-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="371be-136">In this section, you configure and test Azure AD single sign-on with Leapsome based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="371be-136">In this section, you configure and test Azure AD single sign-on with Leapsome based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="371be-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Leapsome is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="371be-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Leapsome is to a user in Azure AD.</span></span> <span data-ttu-id="371be-138">In other words, a link relationship between an Azure AD user and the related user in Leapsome needs to be established.</span><span class="sxs-lookup"><span data-stu-id="371be-138">In other words, a link relationship between an Azure AD user and the related user in Leapsome needs to be established.</span></span>

<span data-ttu-id="371be-139">To configure and test Azure AD single sign-on with Leapsome, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="371be-139">To configure and test Azure AD single sign-on with Leapsome, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="371be-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="371be-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="371be-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="371be-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="371be-142">**[Create a Leapsome test user](#create-a-leapsome-test-user)** - to have a counterpart of Britta Simon in Leapsome that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="371be-142">**[Create a Leapsome test user](#create-a-leapsome-test-user)** - to have a counterpart of Britta Simon in Leapsome that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="371be-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="371be-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="371be-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="371be-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="371be-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="371be-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="371be-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Leapsome application.</span><span class="sxs-lookup"><span data-stu-id="371be-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Leapsome application.</span></span>

<span data-ttu-id="371be-147">**To configure Azure AD single sign-on with Leapsome, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="371be-147">**To configure Azure AD single sign-on with Leapsome, perform the following steps:**</span></span>

1. <span data-ttu-id="371be-148">In the Azure portal, on the **Leapsome** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="371be-148">In the Azure portal, on the **Leapsome** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="371be-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="371be-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/leapsome-tutorial/tutorial_leapsome_samlbase.png)

1. <span data-ttu-id="371be-152">On the **Leapsome Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="371be-152">On the **Leapsome Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Leapsome Domain and URLs single sign-on information](./media/leapsome-tutorial/tutorial_leapsome_url.png)

    <span data-ttu-id="371be-154">a.</span><span class="sxs-lookup"><span data-stu-id="371be-154">a.</span></span> <span data-ttu-id="371be-155">In the **Identifier** textbox, type a URL: `https://www.leapsome.com`</span><span class="sxs-lookup"><span data-stu-id="371be-155">In the **Identifier** textbox, type a URL: `https://www.leapsome.com`</span></span>

    <span data-ttu-id="371be-156">b.</span><span class="sxs-lookup"><span data-stu-id="371be-156">b.</span></span> <span data-ttu-id="371be-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.leapsome.com/api/users/auth/saml/<CLIENTID>/assert`</span><span class="sxs-lookup"><span data-stu-id="371be-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.leapsome.com/api/users/auth/saml/<CLIENTID>/assert`</span></span>

1. <span data-ttu-id="371be-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="371be-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Leapsome Domain and URLs single sign-on information](./media/leapsome-tutorial/tutorial_leapsome_url1.png)

    <span data-ttu-id="371be-160">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.leapsome.com/api/users/auth/saml/<CLIENTID>/login`</span><span class="sxs-lookup"><span data-stu-id="371be-160">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.leapsome.com/api/users/auth/saml/<CLIENTID>/login`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="371be-161">The preceding Reply URL and Sign-on URL value is not real value.</span><span class="sxs-lookup"><span data-stu-id="371be-161">The preceding Reply URL and Sign-on URL value is not real value.</span></span> <span data-ttu-id="371be-162">You will update these with the actual values, which is explained later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="371be-162">You will update these with the actual values, which is explained later in the tutorial.</span></span>

1. <span data-ttu-id="371be-163">Leapsome application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="371be-163">Leapsome application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="371be-164">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="371be-164">Configure the following claims for this application.</span></span> <span data-ttu-id="371be-165">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="371be-165">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="371be-166">The following screenshot shows an example.</span><span class="sxs-lookup"><span data-stu-id="371be-166">The following screenshot shows an example.</span></span>
    
    ![Configure Single Sign-On](./media/leapsome-tutorial/tutorial_Leapsome_attribute.png)

1. <span data-ttu-id="371be-168">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="371be-168">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="371be-169">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="371be-169">Attribute Name</span></span> | <span data-ttu-id="371be-170">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="371be-170">Attribute Value</span></span> | <span data-ttu-id="371be-171">Namespace</span><span class="sxs-lookup"><span data-stu-id="371be-171">Namespace</span></span> |
    | ---------------| --------------- | --------- |   
    | <span data-ttu-id="371be-172">firstname</span><span class="sxs-lookup"><span data-stu-id="371be-172">firstname</span></span> | <span data-ttu-id="371be-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="371be-173">user.givenname</span></span> | http://schemas.xmlsoap.org/ws/2005/05/identity/claims |
    | <span data-ttu-id="371be-174">lastname</span><span class="sxs-lookup"><span data-stu-id="371be-174">lastname</span></span> | <span data-ttu-id="371be-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="371be-175">user.surname</span></span> | http://schemas.xmlsoap.org/ws/2005/05/identity/claims |
    | <span data-ttu-id="371be-176">title</span><span class="sxs-lookup"><span data-stu-id="371be-176">title</span></span> | <span data-ttu-id="371be-177">user.jobtitle</span><span class="sxs-lookup"><span data-stu-id="371be-177">user.jobtitle</span></span> | http://schemas.xmlsoap.org/ws/2005/05/identity/claims |
    | <span data-ttu-id="371be-178">picture</span><span class="sxs-lookup"><span data-stu-id="371be-178">picture</span></span> | <span data-ttu-id="371be-179">URL to the employee's picture</span><span class="sxs-lookup"><span data-stu-id="371be-179">URL to the employee's picture</span></span> | http://schemas.xmlsoap.org/ws/2005/05/identity/claims |

    > [!Note]
    > <span data-ttu-id="371be-180">The value of picture attribute is not real.</span><span class="sxs-lookup"><span data-stu-id="371be-180">The value of picture attribute is not real.</span></span> <span data-ttu-id="371be-181">Update this value with actual picture URL.</span><span class="sxs-lookup"><span data-stu-id="371be-181">Update this value with actual picture URL.</span></span> <span data-ttu-id="371be-182">To get this value contact [Leapsome Client support team](mailto:support@leapsome.com).</span><span class="sxs-lookup"><span data-stu-id="371be-182">To get this value contact [Leapsome Client support team](mailto:support@leapsome.com).</span></span>
    
    <span data-ttu-id="371be-183">a.</span><span class="sxs-lookup"><span data-stu-id="371be-183">a.</span></span> <span data-ttu-id="371be-184">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="371be-184">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/leapsome-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On](./media/leapsome-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="371be-187">b.</span><span class="sxs-lookup"><span data-stu-id="371be-187">b.</span></span> <span data-ttu-id="371be-188">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="371be-188">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="371be-189">c.</span><span class="sxs-lookup"><span data-stu-id="371be-189">c.</span></span> <span data-ttu-id="371be-190">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="371be-190">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="371be-191">d.</span><span class="sxs-lookup"><span data-stu-id="371be-191">d.</span></span> <span data-ttu-id="371be-192">In the **Namespace** textbox, type the namespace uri for that row.</span><span class="sxs-lookup"><span data-stu-id="371be-192">In the **Namespace** textbox, type the namespace uri for that row.</span></span>
    
    <span data-ttu-id="371be-193">e.</span><span class="sxs-lookup"><span data-stu-id="371be-193">e.</span></span> <span data-ttu-id="371be-194">Click **Ok**</span><span class="sxs-lookup"><span data-stu-id="371be-194">Click **Ok**</span></span>

1. <span data-ttu-id="371be-195">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="371be-195">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/leapsome-tutorial/tutorial_leapsome_certificate.png) 

1. <span data-ttu-id="371be-197">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="371be-197">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/leapsome-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="371be-199">On the **Leapsome Configuration** section, click **Configure Leapsome** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="371be-199">On the **Leapsome Configuration** section, click **Configure Leapsome** to open **Configure sign-on** window.</span></span> <span data-ttu-id="371be-200">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="371be-200">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Leapsome Configuration](./media/leapsome-tutorial/tutorial_leapsome_configure.png)

1. <span data-ttu-id="371be-202">In a different web browser window, log in to Leapsome as a Security Administrator.</span><span class="sxs-lookup"><span data-stu-id="371be-202">In a different web browser window, log in to Leapsome as a Security Administrator.</span></span>

1. <span data-ttu-id="371be-203">On the top right, Click on Settings logo and then click **Admin Settings**.</span><span class="sxs-lookup"><span data-stu-id="371be-203">On the top right, Click on Settings logo and then click **Admin Settings**.</span></span> 

    ![Leapsome set](./media/leapsome-tutorial/tutorial_leapsome_admin.png)

1. <span data-ttu-id="371be-205">On the left menu bar click **Single Sign On (SSO)**, and on the **SAML-based single sign-on (SSO)** page perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="371be-205">On the left menu bar click **Single Sign On (SSO)**, and on the **SAML-based single sign-on (SSO)** page perform the following steps:</span></span>
    
    ![Leapsome saml](./media/leapsome-tutorial/tutorial_leapsome_samlsettings.png)

    <span data-ttu-id="371be-207">a.</span><span class="sxs-lookup"><span data-stu-id="371be-207">a.</span></span> <span data-ttu-id="371be-208">Select **Enable SAML-based single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="371be-208">Select **Enable SAML-based single sign-on**.</span></span>

    <span data-ttu-id="371be-209">b.</span><span class="sxs-lookup"><span data-stu-id="371be-209">b.</span></span> <span data-ttu-id="371be-210">Copy the **Login URL (point your users here to start login)** value and paste it into the **Sign-on URL** textbox in **Leapsome Domain and URLs** section on Azure portal.</span><span class="sxs-lookup"><span data-stu-id="371be-210">Copy the **Login URL (point your users here to start login)** value and paste it into the **Sign-on URL** textbox in **Leapsome Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="371be-211">c.</span><span class="sxs-lookup"><span data-stu-id="371be-211">c.</span></span> <span data-ttu-id="371be-212">Copy the **Reply URL (recieves response from your identity provider)** value and paste it into the **Reply URL** textbox in  **Leapsome Domain and URLs** section on Azure portal.</span><span class="sxs-lookup"><span data-stu-id="371be-212">Copy the **Reply URL (recieves response from your identity provider)** value and paste it into the **Reply URL** textbox in  **Leapsome Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="371be-213">d.</span><span class="sxs-lookup"><span data-stu-id="371be-213">d.</span></span> <span data-ttu-id="371be-214">In the **SSO Login URL (provided by identity provider)** textbox, paste the value of **SAML Single Sign-On Service URL**, which you copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="371be-214">In the **SSO Login URL (provided by identity provider)** textbox, paste the value of **SAML Single Sign-On Service URL**, which you copied from the Azure portal.</span></span>

    <span data-ttu-id="371be-215">e.</span><span class="sxs-lookup"><span data-stu-id="371be-215">e.</span></span> <span data-ttu-id="371be-216">Copy the Certificate that you have downloaded from Azure portal without --BEGIN CERTIFICATE and END CERTIFICATE-- comments and paste it in the **Certificate (provided by identity provider)** textbox.</span><span class="sxs-lookup"><span data-stu-id="371be-216">Copy the Certificate that you have downloaded from Azure portal without --BEGIN CERTIFICATE and END CERTIFICATE-- comments and paste it in the **Certificate (provided by identity provider)** textbox.</span></span>

    <span data-ttu-id="371be-217">f.</span><span class="sxs-lookup"><span data-stu-id="371be-217">f.</span></span> <span data-ttu-id="371be-218">Click **UPDATE SSO SETTINGS**.</span><span class="sxs-lookup"><span data-stu-id="371be-218">Click **UPDATE SSO SETTINGS**.</span></span>
    
### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="371be-219">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="371be-219">Create an Azure AD test user</span></span>

<span data-ttu-id="371be-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="371be-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="371be-222">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="371be-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="371be-223">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="371be-223">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/leapsome-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="371be-225">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="371be-225">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/leapsome-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="371be-227">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="371be-227">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/leapsome-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="371be-229">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="371be-229">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/leapsome-tutorial/create_aaduser_04.png)

    <span data-ttu-id="371be-231">a.</span><span class="sxs-lookup"><span data-stu-id="371be-231">a.</span></span> <span data-ttu-id="371be-232">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="371be-232">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="371be-233">b.</span><span class="sxs-lookup"><span data-stu-id="371be-233">b.</span></span> <span data-ttu-id="371be-234">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="371be-234">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="371be-235">c.</span><span class="sxs-lookup"><span data-stu-id="371be-235">c.</span></span> <span data-ttu-id="371be-236">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="371be-236">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="371be-237">d.</span><span class="sxs-lookup"><span data-stu-id="371be-237">d.</span></span> <span data-ttu-id="371be-238">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="371be-238">Click **Create**.</span></span>
 
### <a name="create-a-leapsome-test-user"></a><span data-ttu-id="371be-239">Create a Leapsome test user</span><span class="sxs-lookup"><span data-stu-id="371be-239">Create a Leapsome test user</span></span>

<span data-ttu-id="371be-240">In this section, you create a user called Britta Simon in Leapsome.</span><span class="sxs-lookup"><span data-stu-id="371be-240">In this section, you create a user called Britta Simon in Leapsome.</span></span> <span data-ttu-id="371be-241">Work with [Leapsome Client support team](mailto:support@leapsome.com) to add the users or the domain, which needs to be whitelisted in the Leapsome platform.</span><span class="sxs-lookup"><span data-stu-id="371be-241">Work with [Leapsome Client support team](mailto:support@leapsome.com) to add the users or the domain, which needs to be whitelisted in the Leapsome platform.</span></span> <span data-ttu-id="371be-242">If the domain is added by the team, users will get automatically provisioned to the Leapsome platform.</span><span class="sxs-lookup"><span data-stu-id="371be-242">If the domain is added by the team, users will get automatically provisioned to the Leapsome platform.</span></span> <span data-ttu-id="371be-243">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="371be-243">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="371be-244">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="371be-244">Assign the Azure AD test user</span></span>

<span data-ttu-id="371be-245">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Leapsome.</span><span class="sxs-lookup"><span data-stu-id="371be-245">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Leapsome.</span></span>

![Assign the user role][200] 

<span data-ttu-id="371be-247">**To assign Britta Simon to Leapsome, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="371be-247">**To assign Britta Simon to Leapsome, perform the following steps:**</span></span>

1. <span data-ttu-id="371be-248">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="371be-248">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="371be-250">In the applications list, select **Leapsome**.</span><span class="sxs-lookup"><span data-stu-id="371be-250">In the applications list, select **Leapsome**.</span></span>

    ![The Leapsome link in the Applications list](./media/leapsome-tutorial/tutorial_leapsome_app.png)  

1. <span data-ttu-id="371be-252">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="371be-252">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="371be-254">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="371be-254">Click **Add** button.</span></span> <span data-ttu-id="371be-255">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="371be-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="371be-257">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="371be-257">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="371be-258">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="371be-258">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="371be-259">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="371be-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="371be-260">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="371be-260">Test single sign-on</span></span>

<span data-ttu-id="371be-261">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="371be-261">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="371be-262">When you click the Leapsome tile in the Access Panel, you should get automatically signed-on to your Leapsome application.</span><span class="sxs-lookup"><span data-stu-id="371be-262">When you click the Leapsome tile in the Access Panel, you should get automatically signed-on to your Leapsome application.</span></span>
<span data-ttu-id="371be-263">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="371be-263">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="371be-264">Additional resources</span><span class="sxs-lookup"><span data-stu-id="371be-264">Additional resources</span></span>

* [<span data-ttu-id="371be-265">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="371be-265">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="371be-266">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="371be-266">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/leapsome-tutorial/tutorial_general_01.png
[2]: ./media/leapsome-tutorial/tutorial_general_02.png
[3]: ./media/leapsome-tutorial/tutorial_general_03.png
[4]: ./media/leapsome-tutorial/tutorial_general_04.png

[100]: ./media/leapsome-tutorial/tutorial_general_100.png

[200]: ./media/leapsome-tutorial/tutorial_general_200.png
[201]: ./media/leapsome-tutorial/tutorial_general_201.png
[202]: ./media/leapsome-tutorial/tutorial_general_202.png
[203]: ./media/leapsome-tutorial/tutorial_general_203.png

