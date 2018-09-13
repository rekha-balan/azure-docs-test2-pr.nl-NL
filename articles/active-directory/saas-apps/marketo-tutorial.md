---
title: 'Tutorial: Azure Active Directory integration with Marketo | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Marketo.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: b88c45f5-d288-4717-835c-ca965add8735
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: bd647601249e22942596e78b66d0322857f3eaa4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969211"
---
# <a name="tutorial-azure-active-directory-integration-with-marketo"></a><span data-ttu-id="8f505-103">Tutorial: Azure Active Directory integration with Marketo</span><span class="sxs-lookup"><span data-stu-id="8f505-103">Tutorial: Azure Active Directory integration with Marketo</span></span>

<span data-ttu-id="8f505-104">In this tutorial, you learn how to integrate Marketo with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8f505-104">In this tutorial, you learn how to integrate Marketo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8f505-105">Integrating Marketo with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="8f505-105">Integrating Marketo with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8f505-106">You can control in Azure AD who has access to Marketo</span><span class="sxs-lookup"><span data-stu-id="8f505-106">You can control in Azure AD who has access to Marketo</span></span>
- <span data-ttu-id="8f505-107">You can enable your users to automatically get signed-on to Marketo (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="8f505-107">You can enable your users to automatically get signed-on to Marketo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8f505-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="8f505-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8f505-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="8f505-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f505-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8f505-110">Prerequisites</span></span>

<span data-ttu-id="8f505-111">To configure Azure AD integration with Marketo, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="8f505-111">To configure Azure AD integration with Marketo, you need the following items:</span></span>

- <span data-ttu-id="8f505-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="8f505-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8f505-113">A Marketo single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="8f505-113">A Marketo single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8f505-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="8f505-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8f505-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="8f505-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8f505-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="8f505-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8f505-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8f505-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8f505-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="8f505-118">Scenario description</span></span>
<span data-ttu-id="8f505-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="8f505-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8f505-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="8f505-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8f505-121">Adding Marketo from the gallery</span><span class="sxs-lookup"><span data-stu-id="8f505-121">Adding Marketo from the gallery</span></span>
1. <span data-ttu-id="8f505-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8f505-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-marketo-from-the-gallery"></a><span data-ttu-id="8f505-123">Adding Marketo from the gallery</span><span class="sxs-lookup"><span data-stu-id="8f505-123">Adding Marketo from the gallery</span></span>
<span data-ttu-id="8f505-124">To configure the integration of Marketo into Azure AD, you need to add Marketo from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="8f505-124">To configure the integration of Marketo into Azure AD, you need to add Marketo from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8f505-125">**To add Marketo from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8f505-125">**To add Marketo from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8f505-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="8f505-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="8f505-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="8f505-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8f505-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="8f505-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="8f505-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="8f505-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="8f505-133">In the search box, type **Marketo**.</span><span class="sxs-lookup"><span data-stu-id="8f505-133">In the search box, type **Marketo**.</span></span>

    ![Creating an Azure AD test user](./media/marketo-tutorial/tutorial_marketo_search.png)

1. <span data-ttu-id="8f505-135">In the results panel, select **Marketo**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="8f505-135">In the results panel, select **Marketo**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/marketo-tutorial/tutorial_marketo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8f505-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8f505-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8f505-138">In this section, you configure and test Azure AD single sign-on with Marketo based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="8f505-138">In this section, you configure and test Azure AD single sign-on with Marketo based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8f505-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Marketo is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8f505-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Marketo is to a user in Azure AD.</span></span> <span data-ttu-id="8f505-140">In other words, a link relationship between an Azure AD user and the related user in Marketo needs to be established.</span><span class="sxs-lookup"><span data-stu-id="8f505-140">In other words, a link relationship between an Azure AD user and the related user in Marketo needs to be established.</span></span>

<span data-ttu-id="8f505-141">In Marketo, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="8f505-141">In Marketo, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8f505-142">To configure and test Azure AD single sign-on with Marketo, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="8f505-142">To configure and test Azure AD single sign-on with Marketo, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8f505-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="8f505-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="8f505-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8f505-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="8f505-145">**[Creating a Marketo test user](#creating-a-marketo-test-user)** - to have a counterpart of Britta Simon in Marketo that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="8f505-145">**[Creating a Marketo test user](#creating-a-marketo-test-user)** - to have a counterpart of Britta Simon in Marketo that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="8f505-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8f505-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="8f505-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="8f505-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8f505-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8f505-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8f505-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Marketo application.</span><span class="sxs-lookup"><span data-stu-id="8f505-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Marketo application.</span></span>

<span data-ttu-id="8f505-150">**To configure Azure AD single sign-on with Marketo, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8f505-150">**To configure Azure AD single sign-on with Marketo, perform the following steps:**</span></span>

1. <span data-ttu-id="8f505-151">In the Azure portal, on the **Marketo** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="8f505-151">In the Azure portal, on the **Marketo** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="8f505-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8f505-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/marketo-tutorial/tutorial_marketo_samlbase.png)

1. <span data-ttu-id="8f505-155">On the **Marketo Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8f505-155">On the **Marketo Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/marketo-tutorial/tutorial_marketo_url.png)

    <span data-ttu-id="8f505-157">a.</span><span class="sxs-lookup"><span data-stu-id="8f505-157">a.</span></span> <span data-ttu-id="8f505-158">In the **Identifier** textbox, type a URL using the following pattern: `https://saml.marketo.com/sp`</span><span class="sxs-lookup"><span data-stu-id="8f505-158">In the **Identifier** textbox, type a URL using the following pattern: `https://saml.marketo.com/sp`</span></span>

    <span data-ttu-id="8f505-159">b.</span><span class="sxs-lookup"><span data-stu-id="8f505-159">b.</span></span> <span data-ttu-id="8f505-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://login.marketo.com/saml/assertion/\<munchkinid\>`</span><span class="sxs-lookup"><span data-stu-id="8f505-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://login.marketo.com/saml/assertion/\<munchkinid\>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8f505-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="8f505-161">These values are not real.</span></span> <span data-ttu-id="8f505-162">Update these values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="8f505-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="8f505-163">Contact [Marketo support team](http://investors.marketo.com/contactus.cfm) to get these values.</span><span class="sxs-lookup"><span data-stu-id="8f505-163">Contact [Marketo support team](http://investors.marketo.com/contactus.cfm) to get these values.</span></span>
 
1. <span data-ttu-id="8f505-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="8f505-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/marketo-tutorial/tutorial_marketo_certificate.png) 

1. <span data-ttu-id="8f505-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="8f505-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/marketo-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="8f505-168">On the **Marketo Configuration** section, click **Configure Marketo** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="8f505-168">On the **Marketo Configuration** section, click **Configure Marketo** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8f505-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="8f505-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/marketo-tutorial/tutorial_marketo_configure.png) 

1. <span data-ttu-id="8f505-171">To get Munchkin Id of your application, log in to Marketo using admin credentials and perform following actions:</span><span class="sxs-lookup"><span data-stu-id="8f505-171">To get Munchkin Id of your application, log in to Marketo using admin credentials and perform following actions:</span></span>
   
    <span data-ttu-id="8f505-172">a.</span><span class="sxs-lookup"><span data-stu-id="8f505-172">a.</span></span> <span data-ttu-id="8f505-173">Log in to Marketo app using admin credentials.</span><span class="sxs-lookup"><span data-stu-id="8f505-173">Log in to Marketo app using admin credentials.</span></span>
   
    <span data-ttu-id="8f505-174">b.</span><span class="sxs-lookup"><span data-stu-id="8f505-174">b.</span></span> <span data-ttu-id="8f505-175">Click the **Admin** button on the top navigation pane.</span><span class="sxs-lookup"><span data-stu-id="8f505-175">Click the **Admin** button on the top navigation pane.</span></span>
   
    ![Configure Single Sign-On](./media/marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="8f505-177">c.</span><span class="sxs-lookup"><span data-stu-id="8f505-177">c.</span></span> <span data-ttu-id="8f505-178">Navigate to the Integration menu and click the **Munchkin link**.</span><span class="sxs-lookup"><span data-stu-id="8f505-178">Navigate to the Integration menu and click the **Munchkin link**.</span></span>
   
    ![Configure Single Sign-On](./media/marketo-tutorial/tutorial_marketo_11.png)
   
    <span data-ttu-id="8f505-180">d.</span><span class="sxs-lookup"><span data-stu-id="8f505-180">d.</span></span> <span data-ttu-id="8f505-181">Copy the Munchkin Id shown on the screen and complete your Reply URL in the Azure AD configuration wizard.</span><span class="sxs-lookup"><span data-stu-id="8f505-181">Copy the Munchkin Id shown on the screen and complete your Reply URL in the Azure AD configuration wizard.</span></span>
   
    ![Configure Single Sign-On](./media/marketo-tutorial/tutorial_marketo_12.png) 

1. <span data-ttu-id="8f505-183">To configure the SSO in the application, follow the below steps:</span><span class="sxs-lookup"><span data-stu-id="8f505-183">To configure the SSO in the application, follow the below steps:</span></span>
   
    <span data-ttu-id="8f505-184">a.</span><span class="sxs-lookup"><span data-stu-id="8f505-184">a.</span></span> <span data-ttu-id="8f505-185">Log in to Marketo app using admin credentials.</span><span class="sxs-lookup"><span data-stu-id="8f505-185">Log in to Marketo app using admin credentials.</span></span>
   
    <span data-ttu-id="8f505-186">b.</span><span class="sxs-lookup"><span data-stu-id="8f505-186">b.</span></span> <span data-ttu-id="8f505-187">Click the **Admin** button on the top navigation pane.</span><span class="sxs-lookup"><span data-stu-id="8f505-187">Click the **Admin** button on the top navigation pane.</span></span>
   
    ![Configure Single Sign-On](./media/marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="8f505-189">c.</span><span class="sxs-lookup"><span data-stu-id="8f505-189">c.</span></span> <span data-ttu-id="8f505-190">Navigate to the Integration menu and click **Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="8f505-190">Navigate to the Integration menu and click **Single Sign On**.</span></span>
   
    ![Configure Single Sign-On](./media/marketo-tutorial/tutorial_marketo_07.png) 
   
    <span data-ttu-id="8f505-192">d.</span><span class="sxs-lookup"><span data-stu-id="8f505-192">d.</span></span> <span data-ttu-id="8f505-193">To enable the SAML Settings, click **Edit** button.</span><span class="sxs-lookup"><span data-stu-id="8f505-193">To enable the SAML Settings, click **Edit** button.</span></span>
   
    ![Configure Single Sign-On](./media/marketo-tutorial/tutorial_marketo_08.png) 
   
    <span data-ttu-id="8f505-195">e.</span><span class="sxs-lookup"><span data-stu-id="8f505-195">e.</span></span> <span data-ttu-id="8f505-196">**Enabled** Single Sign-On settings.</span><span class="sxs-lookup"><span data-stu-id="8f505-196">**Enabled** Single Sign-On settings.</span></span>
   
    <span data-ttu-id="8f505-197">f.</span><span class="sxs-lookup"><span data-stu-id="8f505-197">f.</span></span> <span data-ttu-id="8f505-198">Paste the **SAML Entity ID**, in the **Issuer ID** textbox.</span><span class="sxs-lookup"><span data-stu-id="8f505-198">Paste the **SAML Entity ID**, in the **Issuer ID** textbox.</span></span>
   
    <span data-ttu-id="8f505-199">g.</span><span class="sxs-lookup"><span data-stu-id="8f505-199">g.</span></span> <span data-ttu-id="8f505-200">In the **Entity ID** textbox, enter the URL as `http://saml.marketo.com/sp`.</span><span class="sxs-lookup"><span data-stu-id="8f505-200">In the **Entity ID** textbox, enter the URL as `http://saml.marketo.com/sp`.</span></span>
   
    <span data-ttu-id="8f505-201">h.</span><span class="sxs-lookup"><span data-stu-id="8f505-201">h.</span></span> <span data-ttu-id="8f505-202">Select the User ID Location as **Name Identifier element**.</span><span class="sxs-lookup"><span data-stu-id="8f505-202">Select the User ID Location as **Name Identifier element**.</span></span>
   
    ![Configure Single Sign-On](./media/marketo-tutorial/tutorial_marketo_09.png)
   
    > [!NOTE]
    > <span data-ttu-id="8f505-204">If your User Identifier is not UPN value then change the value in the Attribute tab.</span><span class="sxs-lookup"><span data-stu-id="8f505-204">If your User Identifier is not UPN value then change the value in the Attribute tab.</span></span>
   
    <span data-ttu-id="8f505-205">i.</span><span class="sxs-lookup"><span data-stu-id="8f505-205">i.</span></span> <span data-ttu-id="8f505-206">Upload the certificate, which you have downloaded from Azure AD configuration wizard.</span><span class="sxs-lookup"><span data-stu-id="8f505-206">Upload the certificate, which you have downloaded from Azure AD configuration wizard.</span></span> <span data-ttu-id="8f505-207">**Save** the settings.</span><span class="sxs-lookup"><span data-stu-id="8f505-207">**Save** the settings.</span></span>
   
    <span data-ttu-id="8f505-208">j.</span><span class="sxs-lookup"><span data-stu-id="8f505-208">j.</span></span> <span data-ttu-id="8f505-209">Edit the Redirect Pages settings.</span><span class="sxs-lookup"><span data-stu-id="8f505-209">Edit the Redirect Pages settings.</span></span>
   
    <span data-ttu-id="8f505-210">k.</span><span class="sxs-lookup"><span data-stu-id="8f505-210">k.</span></span> <span data-ttu-id="8f505-211">Paste the **SAML Single Sign-On Service URL** in the **Login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="8f505-211">Paste the **SAML Single Sign-On Service URL** in the **Login URL** textbox.</span></span>
   
    <span data-ttu-id="8f505-212">l.</span><span class="sxs-lookup"><span data-stu-id="8f505-212">l.</span></span> <span data-ttu-id="8f505-213">Paste the **Sign-Out URL** in the **Logout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="8f505-213">Paste the **Sign-Out URL** in the **Logout URL** textbox.</span></span>
   
    <span data-ttu-id="8f505-214">m.</span><span class="sxs-lookup"><span data-stu-id="8f505-214">m.</span></span> <span data-ttu-id="8f505-215">In the **Error URL**, copy your **Marketo instance URL** and click **Save** button to save settings.</span><span class="sxs-lookup"><span data-stu-id="8f505-215">In the **Error URL**, copy your **Marketo instance URL** and click **Save** button to save settings.</span></span>
   
    ![Configure Single Sign-On](./media/marketo-tutorial/tutorial_marketo_10.png)

1. <span data-ttu-id="8f505-217">To enable the SSO for users, complete the following actions:</span><span class="sxs-lookup"><span data-stu-id="8f505-217">To enable the SSO for users, complete the following actions:</span></span>
   
    <span data-ttu-id="8f505-218">a.</span><span class="sxs-lookup"><span data-stu-id="8f505-218">a.</span></span> <span data-ttu-id="8f505-219">Log in to Marketo app using admin credentials.</span><span class="sxs-lookup"><span data-stu-id="8f505-219">Log in to Marketo app using admin credentials.</span></span>
   
    <span data-ttu-id="8f505-220">b.</span><span class="sxs-lookup"><span data-stu-id="8f505-220">b.</span></span> <span data-ttu-id="8f505-221">Click the **Admin** button on the top navigation pane.</span><span class="sxs-lookup"><span data-stu-id="8f505-221">Click the **Admin** button on the top navigation pane.</span></span>
   
    ![Configure Single Sign-On](./media/marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="8f505-223">c.</span><span class="sxs-lookup"><span data-stu-id="8f505-223">c.</span></span> <span data-ttu-id="8f505-224">Navigate to the **Security** menu and click **Login Settings**.</span><span class="sxs-lookup"><span data-stu-id="8f505-224">Navigate to the **Security** menu and click **Login Settings**.</span></span>
   
    ![Configure Single Sign-On](./media/marketo-tutorial/tutorial_marketo_13.png)
   
    <span data-ttu-id="8f505-226">d.</span><span class="sxs-lookup"><span data-stu-id="8f505-226">d.</span></span> <span data-ttu-id="8f505-227">Check the **Require SSO** option and **Save** the settings.</span><span class="sxs-lookup"><span data-stu-id="8f505-227">Check the **Require SSO** option and **Save** the settings.</span></span>
   
    ![Configure Single Sign-On](./media/marketo-tutorial/tutorial_marketo_14.png)

> [!TIP]
> <span data-ttu-id="8f505-229">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="8f505-229">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8f505-230">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="8f505-230">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8f505-231">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8f505-231">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8f505-232">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8f505-232">Creating an Azure AD test user</span></span>
<span data-ttu-id="8f505-233">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8f505-233">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="8f505-235">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8f505-235">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8f505-236">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="8f505-236">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/marketo-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="8f505-238">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="8f505-238">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/marketo-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="8f505-240">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="8f505-240">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/marketo-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="8f505-242">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8f505-242">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/marketo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8f505-244">a.</span><span class="sxs-lookup"><span data-stu-id="8f505-244">a.</span></span> <span data-ttu-id="8f505-245">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8f505-245">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8f505-246">b.</span><span class="sxs-lookup"><span data-stu-id="8f505-246">b.</span></span> <span data-ttu-id="8f505-247">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8f505-247">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8f505-248">c.</span><span class="sxs-lookup"><span data-stu-id="8f505-248">c.</span></span> <span data-ttu-id="8f505-249">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="8f505-249">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8f505-250">d.</span><span class="sxs-lookup"><span data-stu-id="8f505-250">d.</span></span> <span data-ttu-id="8f505-251">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="8f505-251">Click **Create**.</span></span>
 
### <a name="creating-a-marketo-test-user"></a><span data-ttu-id="8f505-252">Creating a Marketo test user</span><span class="sxs-lookup"><span data-stu-id="8f505-252">Creating a Marketo test user</span></span>

<span data-ttu-id="8f505-253">In this section, you create a user called Britta Simon in Marketo.</span><span class="sxs-lookup"><span data-stu-id="8f505-253">In this section, you create a user called Britta Simon in Marketo.</span></span> <span data-ttu-id="8f505-254">follow these steps to create a user in Marketo platform.</span><span class="sxs-lookup"><span data-stu-id="8f505-254">follow these steps to create a user in Marketo platform.</span></span>

1. <span data-ttu-id="8f505-255">Log in to Marketo app using admin credentials.</span><span class="sxs-lookup"><span data-stu-id="8f505-255">Log in to Marketo app using admin credentials.</span></span>

1. <span data-ttu-id="8f505-256">Click the **Admin** button on the top navigation pane.</span><span class="sxs-lookup"><span data-stu-id="8f505-256">Click the **Admin** button on the top navigation pane.</span></span>
   
    ![Configure Single Sign-On](./media/marketo-tutorial/tutorial_marketo_06.png) 

1. <span data-ttu-id="8f505-258">Navigate to the **Security** menu and click **Users & Roles**</span><span class="sxs-lookup"><span data-stu-id="8f505-258">Navigate to the **Security** menu and click **Users & Roles**</span></span>
   
    ![Configure Single Sign-On](./media/marketo-tutorial/tutorial_marketo_19.png)  

1. <span data-ttu-id="8f505-260">Click the **Invite New User** link on the Users tab</span><span class="sxs-lookup"><span data-stu-id="8f505-260">Click the **Invite New User** link on the Users tab</span></span>
   
    ![Configure Single Sign-On](./media/marketo-tutorial/tutorial_marketo_15.png) 

1. <span data-ttu-id="8f505-262">In the Invite New User wizard fill the following information</span><span class="sxs-lookup"><span data-stu-id="8f505-262">In the Invite New User wizard fill the following information</span></span>
   
    <span data-ttu-id="8f505-263">a.</span><span class="sxs-lookup"><span data-stu-id="8f505-263">a.</span></span> <span data-ttu-id="8f505-264">Enter the user **Email** address in the textbox</span><span class="sxs-lookup"><span data-stu-id="8f505-264">Enter the user **Email** address in the textbox</span></span>
   
    ![Configure Single Sign-On](./media/marketo-tutorial/tutorial_marketo_16.png)
   
    <span data-ttu-id="8f505-266">b.</span><span class="sxs-lookup"><span data-stu-id="8f505-266">b.</span></span> <span data-ttu-id="8f505-267">Enter the **First Name** in the textbox</span><span class="sxs-lookup"><span data-stu-id="8f505-267">Enter the **First Name** in the textbox</span></span>
   
    <span data-ttu-id="8f505-268">c.</span><span class="sxs-lookup"><span data-stu-id="8f505-268">c.</span></span> <span data-ttu-id="8f505-269">Enter the **Last Name**  in the textbox</span><span class="sxs-lookup"><span data-stu-id="8f505-269">Enter the **Last Name**  in the textbox</span></span>
   
    <span data-ttu-id="8f505-270">d.</span><span class="sxs-lookup"><span data-stu-id="8f505-270">d.</span></span> <span data-ttu-id="8f505-271">Click **Next**</span><span class="sxs-lookup"><span data-stu-id="8f505-271">Click **Next**</span></span>

1. <span data-ttu-id="8f505-272">In the **Permissions** tab, select the **userRoles** and click **Next**</span><span class="sxs-lookup"><span data-stu-id="8f505-272">In the **Permissions** tab, select the **userRoles** and click **Next**</span></span>
   
    ![Configure Single Sign-On](./media/marketo-tutorial/tutorial_marketo_17.png)
1. <span data-ttu-id="8f505-274">Click the **Send** button to send the user invitation</span><span class="sxs-lookup"><span data-stu-id="8f505-274">Click the **Send** button to send the user invitation</span></span>
   
    ![Configure Single Sign-On](./media/marketo-tutorial/tutorial_marketo_18.png)

1. <span data-ttu-id="8f505-276">User receives the email notification and has to click the link and change the password to activate the account.</span><span class="sxs-lookup"><span data-stu-id="8f505-276">User receives the email notification and has to click the link and change the password to activate the account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8f505-277">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8f505-277">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8f505-278">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Marketo.</span><span class="sxs-lookup"><span data-stu-id="8f505-278">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Marketo.</span></span>

![Assign User][200] 

<span data-ttu-id="8f505-280">**To assign Britta Simon to Marketo, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8f505-280">**To assign Britta Simon to Marketo, perform the following steps:**</span></span>

1. <span data-ttu-id="8f505-281">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="8f505-281">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="8f505-283">In the applications list, select **Marketo**.</span><span class="sxs-lookup"><span data-stu-id="8f505-283">In the applications list, select **Marketo**.</span></span>

    ![Configure Single Sign-On](./media/marketo-tutorial/tutorial_marketo_app.png) 

1. <span data-ttu-id="8f505-285">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="8f505-285">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="8f505-287">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="8f505-287">Click **Add** button.</span></span> <span data-ttu-id="8f505-288">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="8f505-288">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="8f505-290">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="8f505-290">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="8f505-291">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="8f505-291">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="8f505-292">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="8f505-292">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8f505-293">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="8f505-293">Testing single sign-on</span></span>

<span data-ttu-id="8f505-294">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="8f505-294">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8f505-295">When you click the Marketo tile in the Access Panel, you should get automatically signed-on to your Marketo application.</span><span class="sxs-lookup"><span data-stu-id="8f505-295">When you click the Marketo tile in the Access Panel, you should get automatically signed-on to your Marketo application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8f505-296">Additional resources</span><span class="sxs-lookup"><span data-stu-id="8f505-296">Additional resources</span></span>

* [<span data-ttu-id="8f505-297">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8f505-297">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="8f505-298">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8f505-298">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/marketo-tutorial/tutorial_general_01.png
[2]: ./media/marketo-tutorial/tutorial_general_02.png
[3]: ./media/marketo-tutorial/tutorial_general_03.png
[4]: ./media/marketo-tutorial/tutorial_general_04.png

[100]: ./media/marketo-tutorial/tutorial_general_100.png

[200]: ./media/marketo-tutorial/tutorial_general_200.png
[201]: ./media/marketo-tutorial/tutorial_general_201.png
[202]: ./media/marketo-tutorial/tutorial_general_202.png
[203]: ./media/marketo-tutorial/tutorial_general_203.png

