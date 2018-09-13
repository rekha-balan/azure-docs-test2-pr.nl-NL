---
title: 'Tutorial: Azure Active Directory integration with SD Elements | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SD Elements.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: f0386307-bb3b-4810-8d4b-d0bfebda04f4
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 4d5c830df47ff212d2f4d93eb48001ce3a3e2207
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864989"
---
# <a name="tutorial-azure-active-directory-integration-with-sd-elements"></a><span data-ttu-id="1a28c-103">Tutorial: Azure Active Directory integration with SD Elements</span><span class="sxs-lookup"><span data-stu-id="1a28c-103">Tutorial: Azure Active Directory integration with SD Elements</span></span>

<span data-ttu-id="1a28c-104">In this tutorial, you learn how to integrate SD Elements with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1a28c-104">In this tutorial, you learn how to integrate SD Elements with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1a28c-105">Integrating SD Elements with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="1a28c-105">Integrating SD Elements with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1a28c-106">You can control in Azure AD who has access to SD Elements</span><span class="sxs-lookup"><span data-stu-id="1a28c-106">You can control in Azure AD who has access to SD Elements</span></span>
- <span data-ttu-id="1a28c-107">You can enable your users to automatically get signed-on to SD Elements (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="1a28c-107">You can enable your users to automatically get signed-on to SD Elements (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1a28c-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="1a28c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1a28c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="1a28c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1a28c-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1a28c-110">Prerequisites</span></span>

<span data-ttu-id="1a28c-111">To configure Azure AD integration with SD Elements, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="1a28c-111">To configure Azure AD integration with SD Elements, you need the following items:</span></span>

- <span data-ttu-id="1a28c-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="1a28c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1a28c-113">A SD Elements single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="1a28c-113">A SD Elements single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1a28c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="1a28c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1a28c-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="1a28c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1a28c-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="1a28c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1a28c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1a28c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1a28c-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="1a28c-118">Scenario description</span></span>
<span data-ttu-id="1a28c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="1a28c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1a28c-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="1a28c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1a28c-121">Adding SD Elements from the gallery</span><span class="sxs-lookup"><span data-stu-id="1a28c-121">Adding SD Elements from the gallery</span></span>
1. <span data-ttu-id="1a28c-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1a28c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sd-elements-from-the-gallery"></a><span data-ttu-id="1a28c-123">Adding SD Elements from the gallery</span><span class="sxs-lookup"><span data-stu-id="1a28c-123">Adding SD Elements from the gallery</span></span>
<span data-ttu-id="1a28c-124">To configure the integration of SD Elements into Azure AD, you need to add SD Elements from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="1a28c-124">To configure the integration of SD Elements into Azure AD, you need to add SD Elements from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1a28c-125">**To add SD Elements from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1a28c-125">**To add SD Elements from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1a28c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="1a28c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="1a28c-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="1a28c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1a28c-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="1a28c-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="1a28c-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="1a28c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="1a28c-133">In the search box, type **SD Elements**.</span><span class="sxs-lookup"><span data-stu-id="1a28c-133">In the search box, type **SD Elements**.</span></span>

    ![Creating an Azure AD test user](./media/sd-elements-tutorial/tutorial_sdelements_search.png)

1. <span data-ttu-id="1a28c-135">In the results panel, select **SD Elements**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="1a28c-135">In the results panel, select **SD Elements**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/sd-elements-tutorial/tutorial_sdelements_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1a28c-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1a28c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1a28c-138">In this section, you configure and test Azure AD single sign-on with SD Elements based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1a28c-138">In this section, you configure and test Azure AD single sign-on with SD Elements based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1a28c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SD Elements is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1a28c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SD Elements is to a user in Azure AD.</span></span> <span data-ttu-id="1a28c-140">In other words, a link relationship between an Azure AD user and the related user in SD Elements needs to be established.</span><span class="sxs-lookup"><span data-stu-id="1a28c-140">In other words, a link relationship between an Azure AD user and the related user in SD Elements needs to be established.</span></span>

<span data-ttu-id="1a28c-141">In SD Elements, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="1a28c-141">In SD Elements, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1a28c-142">To configure and test Azure AD single sign-on with SD Elements, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="1a28c-142">To configure and test Azure AD single sign-on with SD Elements, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1a28c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="1a28c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="1a28c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1a28c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="1a28c-145">**[Creating a SD Elements test user](#creating-a-sd-elements-test-user)** - to have a counterpart of Britta Simon in SD Elements that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="1a28c-145">**[Creating a SD Elements test user](#creating-a-sd-elements-test-user)** - to have a counterpart of Britta Simon in SD Elements that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="1a28c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1a28c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="1a28c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="1a28c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1a28c-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1a28c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1a28c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SD Elements application.</span><span class="sxs-lookup"><span data-stu-id="1a28c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SD Elements application.</span></span>

<span data-ttu-id="1a28c-150">**To configure Azure AD single sign-on with SD Elements, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1a28c-150">**To configure Azure AD single sign-on with SD Elements, perform the following steps:**</span></span>

1. <span data-ttu-id="1a28c-151">In the Azure portal, on the **SD Elements** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="1a28c-151">In the Azure portal, on the **SD Elements** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="1a28c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1a28c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/sd-elements-tutorial/tutorial_sdelements_samlbase.png)

1. <span data-ttu-id="1a28c-155">On the **SD Elements Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1a28c-155">On the **SD Elements Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/sd-elements-tutorial/tutorial_sdelements_url.png)

    <span data-ttu-id="1a28c-157">a.</span><span class="sxs-lookup"><span data-stu-id="1a28c-157">a.</span></span> <span data-ttu-id="1a28c-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.sdelements.com/sso/saml2/metadata`</span><span class="sxs-lookup"><span data-stu-id="1a28c-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.sdelements.com/sso/saml2/metadata`</span></span>

    <span data-ttu-id="1a28c-159">b.</span><span class="sxs-lookup"><span data-stu-id="1a28c-159">b.</span></span> <span data-ttu-id="1a28c-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<tenantname>.sdelements.com/sso/saml2/acs/`</span><span class="sxs-lookup"><span data-stu-id="1a28c-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<tenantname>.sdelements.com/sso/saml2/acs/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1a28c-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="1a28c-161">These values are not real.</span></span> <span data-ttu-id="1a28c-162">Update these values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="1a28c-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="1a28c-163">Contact [SD Elements support team](mailto:support@sdelements.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="1a28c-163">Contact [SD Elements support team](mailto:support@sdelements.com) to get these values.</span></span>

1. <span data-ttu-id="1a28c-164">SD Elements application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="1a28c-164">SD Elements application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="1a28c-165">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="1a28c-165">Configure the following claims for this application.</span></span> <span data-ttu-id="1a28c-166">You can manage the values of these attributes from the **"User Attribute"** tab of the application.</span><span class="sxs-lookup"><span data-stu-id="1a28c-166">You can manage the values of these attributes from the **"User Attribute"** tab of the application.</span></span> <span data-ttu-id="1a28c-167">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="1a28c-167">The following screenshot shows an example for this.</span></span>

    ![Configure Single Sign-On](./media/sd-elements-tutorial/tutorial_sdelements_attribute.png)

1. <span data-ttu-id="1a28c-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1a28c-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span> 

    | <span data-ttu-id="1a28c-170">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="1a28c-170">Attribute Name</span></span> | <span data-ttu-id="1a28c-171">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="1a28c-171">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="1a28c-172">email</span><span class="sxs-lookup"><span data-stu-id="1a28c-172">email</span></span> |<span data-ttu-id="1a28c-173">user.mail</span><span class="sxs-lookup"><span data-stu-id="1a28c-173">user.mail</span></span> |
    | <span data-ttu-id="1a28c-174">firstname</span><span class="sxs-lookup"><span data-stu-id="1a28c-174">firstname</span></span> |<span data-ttu-id="1a28c-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="1a28c-175">user.givenname</span></span> |
    | <span data-ttu-id="1a28c-176">lastname</span><span class="sxs-lookup"><span data-stu-id="1a28c-176">lastname</span></span> |<span data-ttu-id="1a28c-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="1a28c-177">user.surname</span></span> |

    <span data-ttu-id="1a28c-178">a.</span><span class="sxs-lookup"><span data-stu-id="1a28c-178">a.</span></span> <span data-ttu-id="1a28c-179">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="1a28c-179">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/sd-elements-tutorial/tutorial_officespace_04.png)

    ![Configure Single Sign-On](./media/sd-elements-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="1a28c-182">b.</span><span class="sxs-lookup"><span data-stu-id="1a28c-182">b.</span></span> <span data-ttu-id="1a28c-183">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="1a28c-183">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="1a28c-184">c.</span><span class="sxs-lookup"><span data-stu-id="1a28c-184">c.</span></span> <span data-ttu-id="1a28c-185">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="1a28c-185">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="1a28c-186">d.</span><span class="sxs-lookup"><span data-stu-id="1a28c-186">d.</span></span> <span data-ttu-id="1a28c-187">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="1a28c-187">Click **Ok**.</span></span>
 
1. <span data-ttu-id="1a28c-188">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="1a28c-188">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/sd-elements-tutorial/tutorial_sdelements_certificate.png) 

1. <span data-ttu-id="1a28c-190">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="1a28c-190">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/sd-elements-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="1a28c-192">On the **SD Elements Configuration** section, click **Configure SD Elements** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="1a28c-192">On the **SD Elements Configuration** section, click **Configure SD Elements** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1a28c-193">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="1a28c-193">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/sd-elements-tutorial/tutorial_sdelements_configure.png)

1. <span data-ttu-id="1a28c-195">To get single sign-on enabled, contact your [SD Elements support team](mailto:support@sdelements.com) and provide them with the downloaded certificate file.</span><span class="sxs-lookup"><span data-stu-id="1a28c-195">To get single sign-on enabled, contact your [SD Elements support team](mailto:support@sdelements.com) and provide them with the downloaded certificate file.</span></span> 

1. <span data-ttu-id="1a28c-196">In a different browser window, sign-on to your SD Elements tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="1a28c-196">In a different browser window, sign-on to your SD Elements tenant as an administrator.</span></span>

1. <span data-ttu-id="1a28c-197">In the menu on the top, click **System**, and then **Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="1a28c-197">In the menu on the top, click **System**, and then **Single Sign-on**.</span></span> 
   
    ![Configure Single Sign-On](./media/sd-elements-tutorial/tutorial_sd-elements_09.png) 

1. <span data-ttu-id="1a28c-199">On the **Single Sign-On Settings** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1a28c-199">On the **Single Sign-On Settings** dialog, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](./media/sd-elements-tutorial/tutorial_sd-elements_10.png) 
   
    <span data-ttu-id="1a28c-201">a.</span><span class="sxs-lookup"><span data-stu-id="1a28c-201">a.</span></span> <span data-ttu-id="1a28c-202">As **SSO Type**, select **SAML**.</span><span class="sxs-lookup"><span data-stu-id="1a28c-202">As **SSO Type**, select **SAML**.</span></span>
   
    <span data-ttu-id="1a28c-203">b.</span><span class="sxs-lookup"><span data-stu-id="1a28c-203">b.</span></span> <span data-ttu-id="1a28c-204">In the **Identity Provider Entity ID** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1a28c-204">In the **Identity Provider Entity ID** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 
   
    <span data-ttu-id="1a28c-205">c.</span><span class="sxs-lookup"><span data-stu-id="1a28c-205">c.</span></span> <span data-ttu-id="1a28c-206">In the **Identity Provider Single Sign-On Service** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1a28c-206">In the **Identity Provider Single Sign-On Service** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span> 
   
    <span data-ttu-id="1a28c-207">d.</span><span class="sxs-lookup"><span data-stu-id="1a28c-207">d.</span></span> <span data-ttu-id="1a28c-208">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="1a28c-208">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="1a28c-209">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="1a28c-209">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1a28c-210">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="1a28c-210">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1a28c-211">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1a28c-211">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1a28c-212">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1a28c-212">Creating an Azure AD test user</span></span>
<span data-ttu-id="1a28c-213">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1a28c-213">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="1a28c-215">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1a28c-215">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1a28c-216">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="1a28c-216">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/sd-elements-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="1a28c-218">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="1a28c-218">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/sd-elements-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="1a28c-220">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="1a28c-220">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/sd-elements-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="1a28c-222">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1a28c-222">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/sd-elements-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1a28c-224">a.</span><span class="sxs-lookup"><span data-stu-id="1a28c-224">a.</span></span> <span data-ttu-id="1a28c-225">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1a28c-225">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1a28c-226">b.</span><span class="sxs-lookup"><span data-stu-id="1a28c-226">b.</span></span> <span data-ttu-id="1a28c-227">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1a28c-227">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1a28c-228">c.</span><span class="sxs-lookup"><span data-stu-id="1a28c-228">c.</span></span> <span data-ttu-id="1a28c-229">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="1a28c-229">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1a28c-230">d.</span><span class="sxs-lookup"><span data-stu-id="1a28c-230">d.</span></span> <span data-ttu-id="1a28c-231">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="1a28c-231">Click **Create**.</span></span>
 
### <a name="creating-a-sd-elements-test-user"></a><span data-ttu-id="1a28c-232">Creating a SD Elements test user</span><span class="sxs-lookup"><span data-stu-id="1a28c-232">Creating a SD Elements test user</span></span>

<span data-ttu-id="1a28c-233">The objective of this section is to create a user called Britta Simon in SD Elements.</span><span class="sxs-lookup"><span data-stu-id="1a28c-233">The objective of this section is to create a user called Britta Simon in SD Elements.</span></span> <span data-ttu-id="1a28c-234">In the case of SD Elements, creating SD Elements users is a manual task.</span><span class="sxs-lookup"><span data-stu-id="1a28c-234">In the case of SD Elements, creating SD Elements users is a manual task.</span></span>

<span data-ttu-id="1a28c-235">**To create Britta Simon in SD Elements, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1a28c-235">**To create Britta Simon in SD Elements, perform the following steps:**</span></span>

1. <span data-ttu-id="1a28c-236">In a web browser window, sign-on to your SD Elements company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="1a28c-236">In a web browser window, sign-on to your SD Elements company site as an administrator.</span></span>

1. <span data-ttu-id="1a28c-237">In the menu on the top, click **User Management**, and then **Users**.</span><span class="sxs-lookup"><span data-stu-id="1a28c-237">In the menu on the top, click **User Management**, and then **Users**.</span></span>
   
    ![Creating a SD Elements test user](./media/sd-elements-tutorial/tutorial_sd-elements_11.png) 

1. <span data-ttu-id="1a28c-239">Click **Add New User**.</span><span class="sxs-lookup"><span data-stu-id="1a28c-239">Click **Add New User**.</span></span>
   
    ![Creating a SD Elements test user](./media/sd-elements-tutorial/tutorial_sd-elements_12.png)
 
1. <span data-ttu-id="1a28c-241">On the **Add New User** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1a28c-241">On the **Add New User** dialog, perform the following steps:</span></span>
   
    ![Creating a SD Elements test user](./media/sd-elements-tutorial/tutorial_sd-elements_13.png) 
   
    <span data-ttu-id="1a28c-243">a.</span><span class="sxs-lookup"><span data-stu-id="1a28c-243">a.</span></span> <span data-ttu-id="1a28c-244">In the **E-mail** textbox, enter the email of user like **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="1a28c-244">In the **E-mail** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="1a28c-245">b.</span><span class="sxs-lookup"><span data-stu-id="1a28c-245">b.</span></span> <span data-ttu-id="1a28c-246">In the **First Name** textbox, enter the first name of user like **Britta**.</span><span class="sxs-lookup"><span data-stu-id="1a28c-246">In the **First Name** textbox, enter the first name of user like **Britta**.</span></span>
   
    <span data-ttu-id="1a28c-247">c.</span><span class="sxs-lookup"><span data-stu-id="1a28c-247">c.</span></span> <span data-ttu-id="1a28c-248">In the **Last Name** textbox, enter the last name of user like **Simon**.</span><span class="sxs-lookup"><span data-stu-id="1a28c-248">In the **Last Name** textbox, enter the last name of user like **Simon**.</span></span>
   
    <span data-ttu-id="1a28c-249">d.</span><span class="sxs-lookup"><span data-stu-id="1a28c-249">d.</span></span> <span data-ttu-id="1a28c-250">As **Role**, select **User**.</span><span class="sxs-lookup"><span data-stu-id="1a28c-250">As **Role**, select **User**.</span></span> 
   
    <span data-ttu-id="1a28c-251">e.</span><span class="sxs-lookup"><span data-stu-id="1a28c-251">e.</span></span> <span data-ttu-id="1a28c-252">Click **Create User**.</span><span class="sxs-lookup"><span data-stu-id="1a28c-252">Click **Create User**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1a28c-253">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1a28c-253">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1a28c-254">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SD Elements.</span><span class="sxs-lookup"><span data-stu-id="1a28c-254">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SD Elements.</span></span>

![Assign User][200] 

<span data-ttu-id="1a28c-256">**To assign Britta Simon to SD Elements, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1a28c-256">**To assign Britta Simon to SD Elements, perform the following steps:**</span></span>

1. <span data-ttu-id="1a28c-257">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="1a28c-257">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="1a28c-259">In the applications list, select **SD Elements**.</span><span class="sxs-lookup"><span data-stu-id="1a28c-259">In the applications list, select **SD Elements**.</span></span>

    ![Configure Single Sign-On](./media/sd-elements-tutorial/tutorial_sdelements_app.png) 

1. <span data-ttu-id="1a28c-261">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="1a28c-261">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="1a28c-263">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="1a28c-263">Click **Add** button.</span></span> <span data-ttu-id="1a28c-264">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="1a28c-264">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="1a28c-266">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="1a28c-266">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="1a28c-267">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="1a28c-267">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="1a28c-268">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="1a28c-268">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1a28c-269">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="1a28c-269">Testing single sign-on</span></span>

<span data-ttu-id="1a28c-270">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="1a28c-270">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>
  
<span data-ttu-id="1a28c-271">When you click the SD Elements tile in the Access Panel, you should get automatically signed-on to your SD Elements application.</span><span class="sxs-lookup"><span data-stu-id="1a28c-271">When you click the SD Elements tile in the Access Panel, you should get automatically signed-on to your SD Elements application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1a28c-272">Additional resources</span><span class="sxs-lookup"><span data-stu-id="1a28c-272">Additional resources</span></span>

* [<span data-ttu-id="1a28c-273">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1a28c-273">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="1a28c-274">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1a28c-274">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/sd-elements-tutorial/tutorial_general_01.png
[2]: ./media/sd-elements-tutorial/tutorial_general_02.png
[3]: ./media/sd-elements-tutorial/tutorial_general_03.png
[4]: ./media/sd-elements-tutorial/tutorial_general_04.png

[100]: ./media/sd-elements-tutorial/tutorial_general_100.png

[200]: ./media/sd-elements-tutorial/tutorial_general_200.png
[201]: ./media/sd-elements-tutorial/tutorial_general_201.png
[202]: ./media/sd-elements-tutorial/tutorial_general_202.png
[203]: ./media/sd-elements-tutorial/tutorial_general_203.png

