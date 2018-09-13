---
title: 'Tutorial: Azure Active Directory integration with CloudPassage | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and CloudPassage.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: bfe1f14e-74e4-4680-ac9e-f7355e1c94cc
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: c44b9345da32f907efacfe2b7bb1cf09de0a6345
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865879"
---
# <a name="tutorial-azure-active-directory-integration-with-cloudpassage"></a><span data-ttu-id="11c02-103">Tutorial: Azure Active Directory integration with CloudPassage</span><span class="sxs-lookup"><span data-stu-id="11c02-103">Tutorial: Azure Active Directory integration with CloudPassage</span></span>

<span data-ttu-id="11c02-104">In this tutorial, you learn how to integrate CloudPassage with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="11c02-104">In this tutorial, you learn how to integrate CloudPassage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="11c02-105">Integrating CloudPassage with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="11c02-105">Integrating CloudPassage with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="11c02-106">You can control in Azure AD who has access to CloudPassage</span><span class="sxs-lookup"><span data-stu-id="11c02-106">You can control in Azure AD who has access to CloudPassage</span></span>
- <span data-ttu-id="11c02-107">You can enable your users to automatically get signed-on to CloudPassage (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="11c02-107">You can enable your users to automatically get signed-on to CloudPassage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="11c02-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="11c02-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="11c02-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="11c02-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="11c02-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="11c02-110">Prerequisites</span></span>

<span data-ttu-id="11c02-111">To configure Azure AD integration with CloudPassage, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="11c02-111">To configure Azure AD integration with CloudPassage, you need the following items:</span></span>

- <span data-ttu-id="11c02-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="11c02-112">An Azure AD subscription</span></span>
- <span data-ttu-id="11c02-113">A CloudPassage single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="11c02-113">A CloudPassage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="11c02-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="11c02-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="11c02-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="11c02-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="11c02-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="11c02-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="11c02-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="11c02-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="11c02-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="11c02-118">Scenario description</span></span>
<span data-ttu-id="11c02-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="11c02-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="11c02-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="11c02-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="11c02-121">Adding CloudPassage from the gallery</span><span class="sxs-lookup"><span data-stu-id="11c02-121">Adding CloudPassage from the gallery</span></span>
1. <span data-ttu-id="11c02-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="11c02-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cloudpassage-from-the-gallery"></a><span data-ttu-id="11c02-123">Adding CloudPassage from the gallery</span><span class="sxs-lookup"><span data-stu-id="11c02-123">Adding CloudPassage from the gallery</span></span>
<span data-ttu-id="11c02-124">To configure the integration of CloudPassage into Azure AD, you need to add CloudPassage from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="11c02-124">To configure the integration of CloudPassage into Azure AD, you need to add CloudPassage from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="11c02-125">**To add CloudPassage from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="11c02-125">**To add CloudPassage from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="11c02-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="11c02-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="11c02-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="11c02-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="11c02-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="11c02-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="11c02-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="11c02-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="11c02-133">In the search box, type **CloudPassage**.</span><span class="sxs-lookup"><span data-stu-id="11c02-133">In the search box, type **CloudPassage**.</span></span>

    ![Creating an Azure AD test user](./media/cloudpassage-tutorial/tutorial_cloudpassage_search.png)

1. <span data-ttu-id="11c02-135">In the results panel, select **CloudPassage**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="11c02-135">In the results panel, select **CloudPassage**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/cloudpassage-tutorial/tutorial_cloudpassage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="11c02-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="11c02-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="11c02-138">In this section, you configure and test Azure AD single sign-on with CloudPassage based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="11c02-138">In this section, you configure and test Azure AD single sign-on with CloudPassage based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="11c02-139">For single sign-on to work, Azure AD needs to know what the counterpart user in CloudPassage is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="11c02-139">For single sign-on to work, Azure AD needs to know what the counterpart user in CloudPassage is to a user in Azure AD.</span></span> <span data-ttu-id="11c02-140">In other words, a link relationship between an Azure AD user and the related user in CloudPassage needs to be established.</span><span class="sxs-lookup"><span data-stu-id="11c02-140">In other words, a link relationship between an Azure AD user and the related user in CloudPassage needs to be established.</span></span>

<span data-ttu-id="11c02-141">In CloudPassage, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="11c02-141">In CloudPassage, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="11c02-142">To configure and test Azure AD single sign-on with CloudPassage, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="11c02-142">To configure and test Azure AD single sign-on with CloudPassage, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="11c02-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="11c02-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="11c02-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="11c02-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="11c02-145">**[Creating a CloudPassage test user](#creating-a-cloudpassage-test-user)** - to have a counterpart of Britta Simon in CloudPassage that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="11c02-145">**[Creating a CloudPassage test user](#creating-a-cloudpassage-test-user)** - to have a counterpart of Britta Simon in CloudPassage that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="11c02-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="11c02-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="11c02-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="11c02-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="11c02-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="11c02-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="11c02-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your CloudPassage application.</span><span class="sxs-lookup"><span data-stu-id="11c02-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your CloudPassage application.</span></span>

<span data-ttu-id="11c02-150">**To configure Azure AD single sign-on with CloudPassage, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="11c02-150">**To configure Azure AD single sign-on with CloudPassage, perform the following steps:**</span></span>

1. <span data-ttu-id="11c02-151">In the Azure portal, on the **CloudPassage** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="11c02-151">In the Azure portal, on the **CloudPassage** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="11c02-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="11c02-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/cloudpassage-tutorial/tutorial_cloudpassage_samlbase.png)

1. <span data-ttu-id="11c02-155">On the **CloudPassage Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="11c02-155">On the **CloudPassage Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/cloudpassage-tutorial/tutorial_cloudpassage_url.png)

    <span data-ttu-id="11c02-157">a.</span><span class="sxs-lookup"><span data-stu-id="11c02-157">a.</span></span> <span data-ttu-id="11c02-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://portal.cloudpassage.com/saml/init/accountid`</span><span class="sxs-lookup"><span data-stu-id="11c02-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://portal.cloudpassage.com/saml/init/accountid`</span></span>

    <span data-ttu-id="11c02-159">b.</span><span class="sxs-lookup"><span data-stu-id="11c02-159">b.</span></span> <span data-ttu-id="11c02-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://portal.cloudpassage.com/saml/consume/accountid`.</span><span class="sxs-lookup"><span data-stu-id="11c02-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://portal.cloudpassage.com/saml/consume/accountid`.</span></span> <span data-ttu-id="11c02-161">You can get your value for this attribute by clicking **SSO Setup documentation** in the **Single Sign-on Settings** section of your CloudPassage portal.</span><span class="sxs-lookup"><span data-stu-id="11c02-161">You can get your value for this attribute by clicking **SSO Setup documentation** in the **Single Sign-on Settings** section of your CloudPassage portal.</span></span>

    ![Configure Single Sign-On](./media/cloudpassage-tutorial/tutorial_cloudpassage_05.png)
     
    > [!NOTE] 
    > <span data-ttu-id="11c02-163">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="11c02-163">These values are not real.</span></span> <span data-ttu-id="11c02-164">Update these values with the actual Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="11c02-164">Update these values with the actual Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="11c02-165">Contact [CloudPassage Client support team](https://www.cloudpassage.com/company/contact/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="11c02-165">Contact [CloudPassage Client support team](https://www.cloudpassage.com/company/contact/) to get these values.</span></span> 

1. <span data-ttu-id="11c02-166">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="11c02-166">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/cloudpassage-tutorial/tutorial_cloudpassage_certificate.png) 

1. <span data-ttu-id="11c02-168">Your CloudPassage application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span><span class="sxs-lookup"><span data-stu-id="11c02-168">Your CloudPassage application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="11c02-169">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="11c02-169">The following screenshot shows an example for this.</span></span>
   
   ![Configure Single Sign-On](./media/cloudpassage-tutorial/tutorial_cloudpassage_25.png) 

1. <span data-ttu-id="11c02-171">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="11c02-171">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>

    | <span data-ttu-id="11c02-172">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="11c02-172">Attribute Name</span></span> | <span data-ttu-id="11c02-173">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="11c02-173">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="11c02-174">firstname</span><span class="sxs-lookup"><span data-stu-id="11c02-174">firstname</span></span> |<span data-ttu-id="11c02-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="11c02-175">user.givenname</span></span> |
    | <span data-ttu-id="11c02-176">lastname</span><span class="sxs-lookup"><span data-stu-id="11c02-176">lastname</span></span> |<span data-ttu-id="11c02-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="11c02-177">user.surname</span></span> |
    | <span data-ttu-id="11c02-178">email</span><span class="sxs-lookup"><span data-stu-id="11c02-178">email</span></span> |<span data-ttu-id="11c02-179">user.mail</span><span class="sxs-lookup"><span data-stu-id="11c02-179">user.mail</span></span> |
    
    <span data-ttu-id="11c02-180">a.</span><span class="sxs-lookup"><span data-stu-id="11c02-180">a.</span></span> <span data-ttu-id="11c02-181">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="11c02-181">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/cloudpassage-tutorial/tutorial_attribute_04.png)
    
    ![Configure Single Sign-On](./media/cloudpassage-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="11c02-184">b.</span><span class="sxs-lookup"><span data-stu-id="11c02-184">b.</span></span> <span data-ttu-id="11c02-185">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="11c02-185">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="11c02-186">c.</span><span class="sxs-lookup"><span data-stu-id="11c02-186">c.</span></span> <span data-ttu-id="11c02-187">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="11c02-187">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="11c02-188">d.</span><span class="sxs-lookup"><span data-stu-id="11c02-188">d.</span></span> <span data-ttu-id="11c02-189">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="11c02-189">Click **Ok**.</span></span>

1. <span data-ttu-id="11c02-190">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="11c02-190">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/cloudpassage-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="11c02-192">On the **CloudPassage Configuration** section, click **Configure CloudPassage** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="11c02-192">On the **CloudPassage Configuration** section, click **Configure CloudPassage** to open **Configure sign-on** window.</span></span> <span data-ttu-id="11c02-193">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="11c02-193">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/cloudpassage-tutorial/tutorial_cloudpassage_configure.png) 

1. <span data-ttu-id="11c02-195">In a different browser window, sign-on to your CloudPassage company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="11c02-195">In a different browser window, sign-on to your CloudPassage company site as administrator.</span></span>

1. <span data-ttu-id="11c02-196">In the menu on the top, click **Settings**, and then click **Site Administration**.</span><span class="sxs-lookup"><span data-stu-id="11c02-196">In the menu on the top, click **Settings**, and then click **Site Administration**.</span></span> 
   
    ![Configure Single Sign-On][12]

1. <span data-ttu-id="11c02-198">Click the **Authentication Settings** tab.</span><span class="sxs-lookup"><span data-stu-id="11c02-198">Click the **Authentication Settings** tab.</span></span> 
   
    ![Configure Single Sign-On][13]

1. <span data-ttu-id="11c02-200">In the **Single Sign-on Settings** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="11c02-200">In the **Single Sign-on Settings** section, perform the following steps:</span></span> 
   
    ![Configure Single Sign-On][14]

    <span data-ttu-id="11c02-202">a.</span><span class="sxs-lookup"><span data-stu-id="11c02-202">a.</span></span> <span data-ttu-id="11c02-203">Select **Enable Single sign-on(SSO)(SSO Setup Documentation)** checkbox.</span><span class="sxs-lookup"><span data-stu-id="11c02-203">Select **Enable Single sign-on(SSO)(SSO Setup Documentation)** checkbox.</span></span>
    
    <span data-ttu-id="11c02-204">b.</span><span class="sxs-lookup"><span data-stu-id="11c02-204">b.</span></span> <span data-ttu-id="11c02-205">Paste **SAML Entity ID** into the **SAML issuer URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="11c02-205">Paste **SAML Entity ID** into the **SAML issuer URL** textbox.</span></span>
  
    <span data-ttu-id="11c02-206">c.</span><span class="sxs-lookup"><span data-stu-id="11c02-206">c.</span></span> <span data-ttu-id="11c02-207">Paste **SAML Single Sign-On Service URL** into the **SAML endpoint URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="11c02-207">Paste **SAML Single Sign-On Service URL** into the **SAML endpoint URL** textbox.</span></span>
  
    <span data-ttu-id="11c02-208">d.</span><span class="sxs-lookup"><span data-stu-id="11c02-208">d.</span></span> <span data-ttu-id="11c02-209">Paste **Sign-Out URL** into the **Logout landing page** textbox.</span><span class="sxs-lookup"><span data-stu-id="11c02-209">Paste **Sign-Out URL** into the **Logout landing page** textbox.</span></span>
  
    <span data-ttu-id="11c02-210">e.</span><span class="sxs-lookup"><span data-stu-id="11c02-210">e.</span></span> <span data-ttu-id="11c02-211">Open your downloaded certificate in notepad, copy the content of downloaded certificate into your clipboard, and then paste it into the **x 509 certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="11c02-211">Open your downloaded certificate in notepad, copy the content of downloaded certificate into your clipboard, and then paste it into the **x 509 certificate** textbox.</span></span>
  
    <span data-ttu-id="11c02-212">f.</span><span class="sxs-lookup"><span data-stu-id="11c02-212">f.</span></span> <span data-ttu-id="11c02-213">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="11c02-213">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="11c02-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="11c02-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="11c02-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="11c02-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="11c02-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="11c02-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="11c02-217">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="11c02-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="11c02-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="11c02-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="11c02-220">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="11c02-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="11c02-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="11c02-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/cloudpassage-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="11c02-223">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="11c02-223">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/cloudpassage-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="11c02-225">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="11c02-225">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/cloudpassage-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="11c02-227">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="11c02-227">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/cloudpassage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="11c02-229">a.</span><span class="sxs-lookup"><span data-stu-id="11c02-229">a.</span></span> <span data-ttu-id="11c02-230">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="11c02-230">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="11c02-231">b.</span><span class="sxs-lookup"><span data-stu-id="11c02-231">b.</span></span> <span data-ttu-id="11c02-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="11c02-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="11c02-233">c.</span><span class="sxs-lookup"><span data-stu-id="11c02-233">c.</span></span> <span data-ttu-id="11c02-234">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="11c02-234">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="11c02-235">d.</span><span class="sxs-lookup"><span data-stu-id="11c02-235">d.</span></span> <span data-ttu-id="11c02-236">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="11c02-236">Click **Create**.</span></span>
 
### <a name="creating-a-cloudpassage-test-user"></a><span data-ttu-id="11c02-237">Creating a CloudPassage test user</span><span class="sxs-lookup"><span data-stu-id="11c02-237">Creating a CloudPassage test user</span></span>

<span data-ttu-id="11c02-238">The objective of this section is to create a user called Britta Simon in CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="11c02-238">The objective of this section is to create a user called Britta Simon in CloudPassage.</span></span>

<span data-ttu-id="11c02-239">**To create a user called Britta Simon in CloudPassage, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="11c02-239">**To create a user called Britta Simon in CloudPassage, perform the following steps:**</span></span>

1. <span data-ttu-id="11c02-240">Sign-on to your **CloudPassage** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="11c02-240">Sign-on to your **CloudPassage** company site as an administrator.</span></span> 

1. <span data-ttu-id="11c02-241">In the toolbar on the top, click **Settings**, and then click **Site Administration**.</span><span class="sxs-lookup"><span data-stu-id="11c02-241">In the toolbar on the top, click **Settings**, and then click **Site Administration**.</span></span> 
   
   ![Creating a CloudPassage test user][22] 

1. <span data-ttu-id="11c02-243">Click the **Users** tab, and then click **Add New User**.</span><span class="sxs-lookup"><span data-stu-id="11c02-243">Click the **Users** tab, and then click **Add New User**.</span></span> 
   
   ![Creating a CloudPassage test user][23]

1. <span data-ttu-id="11c02-245">In the **Add New User** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="11c02-245">In the **Add New User** section, perform the following steps:</span></span> 
   
   ![Creating a CloudPassage test user][24]
    
    <span data-ttu-id="11c02-247">a.</span><span class="sxs-lookup"><span data-stu-id="11c02-247">a.</span></span> <span data-ttu-id="11c02-248">In the **First Name** textbox, type Britta.</span><span class="sxs-lookup"><span data-stu-id="11c02-248">In the **First Name** textbox, type Britta.</span></span> 
  
    <span data-ttu-id="11c02-249">b.</span><span class="sxs-lookup"><span data-stu-id="11c02-249">b.</span></span> <span data-ttu-id="11c02-250">In the **Last Name** textbox, type Simon.</span><span class="sxs-lookup"><span data-stu-id="11c02-250">In the **Last Name** textbox, type Simon.</span></span>
  
    <span data-ttu-id="11c02-251">c.</span><span class="sxs-lookup"><span data-stu-id="11c02-251">c.</span></span> <span data-ttu-id="11c02-252">In the **Username** textbox, the **Email** textbox and the **Retype Email** textbox, type Britta's user name in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="11c02-252">In the **Username** textbox, the **Email** textbox and the **Retype Email** textbox, type Britta's user name in Azure AD.</span></span>
  
    <span data-ttu-id="11c02-253">d.</span><span class="sxs-lookup"><span data-stu-id="11c02-253">d.</span></span> <span data-ttu-id="11c02-254">As **Access Type**, select **Enable Halo Portal Access**.</span><span class="sxs-lookup"><span data-stu-id="11c02-254">As **Access Type**, select **Enable Halo Portal Access**.</span></span>
  
    <span data-ttu-id="11c02-255">e.</span><span class="sxs-lookup"><span data-stu-id="11c02-255">e.</span></span> <span data-ttu-id="11c02-256">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="11c02-256">Click **Add**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="11c02-257">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="11c02-257">Assigning the Azure AD test user</span></span>

<span data-ttu-id="11c02-258">In this section, you enable Britta Simon to use Azure single sign-on by granting access to CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="11c02-258">In this section, you enable Britta Simon to use Azure single sign-on by granting access to CloudPassage.</span></span>

![Assign User][200] 

<span data-ttu-id="11c02-260">**To assign Britta Simon to CloudPassage, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="11c02-260">**To assign Britta Simon to CloudPassage, perform the following steps:**</span></span>

1. <span data-ttu-id="11c02-261">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="11c02-261">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="11c02-263">In the applications list, select **CloudPassage**.</span><span class="sxs-lookup"><span data-stu-id="11c02-263">In the applications list, select **CloudPassage**.</span></span>

    ![Configure Single Sign-On](./media/cloudpassage-tutorial/tutorial_cloudpassage_app.png) 

1. <span data-ttu-id="11c02-265">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="11c02-265">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="11c02-267">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="11c02-267">Click **Add** button.</span></span> <span data-ttu-id="11c02-268">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="11c02-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="11c02-270">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="11c02-270">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="11c02-271">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="11c02-271">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="11c02-272">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="11c02-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="11c02-273">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="11c02-273">Testing single sign-on</span></span>

<span data-ttu-id="11c02-274">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="11c02-274">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="11c02-275">When you click the CloudPassage tile in the Access Panel, you should get automatically signed-on to your CloudPassage application.</span><span class="sxs-lookup"><span data-stu-id="11c02-275">When you click the CloudPassage tile in the Access Panel, you should get automatically signed-on to your CloudPassage application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="11c02-276">Additional resources</span><span class="sxs-lookup"><span data-stu-id="11c02-276">Additional resources</span></span>

* [<span data-ttu-id="11c02-277">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="11c02-277">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="11c02-278">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="11c02-278">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/cloudpassage-tutorial/tutorial_general_01.png
[2]: ./media/cloudpassage-tutorial/tutorial_general_02.png
[3]: ./media/cloudpassage-tutorial/tutorial_general_03.png
[4]: ./media/cloudpassage-tutorial/tutorial_general_04.png
[12]: ./media/cloudpassage-tutorial/tutorial_cloudpassage_07.png
[13]: ./media/cloudpassage-tutorial/tutorial_cloudpassage_08.png
[14]: ./media/cloudpassage-tutorial/tutorial_cloudpassage_09.png
[15]: ./media/cloudpassage-tutorial/tutorial_cloudpassage_10.png
[22]: ./media/cloudpassage-tutorial/tutorial_cloudpassage_15.png
[23]: ./media/cloudpassage-tutorial/tutorial_cloudpassage_16.png
[24]: ./media/cloudpassage-tutorial/tutorial_cloudpassage_17.png

[100]: ./media/cloudpassage-tutorial/tutorial_general_100.png

[200]: ./media/cloudpassage-tutorial/tutorial_general_200.png
[201]: ./media/cloudpassage-tutorial/tutorial_general_201.png
[202]: ./media/cloudpassage-tutorial/tutorial_general_202.png
[203]: ./media/cloudpassage-tutorial/tutorial_general_203.png

