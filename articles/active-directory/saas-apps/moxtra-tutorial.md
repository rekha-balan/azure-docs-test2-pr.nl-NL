---
title: 'Tutorial: Azure Active Directory integration with Moxtra | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Moxtra.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 2aed2d4b-1dcd-4839-8fed-9419d107c61c
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: efb9d72de3b408ce741ed96aa2aecd2ed45e293c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871194"
---
# <a name="tutorial-azure-active-directory-integration-with-moxtra"></a><span data-ttu-id="a9654-103">Tutorial: Azure Active Directory integration with Moxtra</span><span class="sxs-lookup"><span data-stu-id="a9654-103">Tutorial: Azure Active Directory integration with Moxtra</span></span>

<span data-ttu-id="a9654-104">In this tutorial, you learn how to integrate Moxtra with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a9654-104">In this tutorial, you learn how to integrate Moxtra with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a9654-105">Integrating Moxtra with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="a9654-105">Integrating Moxtra with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a9654-106">You can control in Azure AD who has access to Moxtra</span><span class="sxs-lookup"><span data-stu-id="a9654-106">You can control in Azure AD who has access to Moxtra</span></span>
- <span data-ttu-id="a9654-107">You can enable your users to automatically get signed-on to Moxtra (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="a9654-107">You can enable your users to automatically get signed-on to Moxtra (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a9654-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="a9654-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a9654-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="a9654-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a9654-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a9654-110">Prerequisites</span></span>

<span data-ttu-id="a9654-111">To configure Azure AD integration with Moxtra, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="a9654-111">To configure Azure AD integration with Moxtra, you need the following items:</span></span>

- <span data-ttu-id="a9654-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="a9654-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a9654-113">A Moxtra single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="a9654-113">A Moxtra single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a9654-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="a9654-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a9654-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="a9654-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a9654-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="a9654-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a9654-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a9654-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a9654-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="a9654-118">Scenario description</span></span>
<span data-ttu-id="a9654-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="a9654-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a9654-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="a9654-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a9654-121">Adding Moxtra from the gallery</span><span class="sxs-lookup"><span data-stu-id="a9654-121">Adding Moxtra from the gallery</span></span>
1. <span data-ttu-id="a9654-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a9654-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moxtra-from-the-gallery"></a><span data-ttu-id="a9654-123">Adding Moxtra from the gallery</span><span class="sxs-lookup"><span data-stu-id="a9654-123">Adding Moxtra from the gallery</span></span>
<span data-ttu-id="a9654-124">To configure the integration of Moxtra into Azure AD, you need to add Moxtra from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="a9654-124">To configure the integration of Moxtra into Azure AD, you need to add Moxtra from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a9654-125">**To add Moxtra from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a9654-125">**To add Moxtra from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a9654-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a9654-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="a9654-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="a9654-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a9654-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a9654-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="a9654-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="a9654-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="a9654-133">In the search box, type **Moxtra**.</span><span class="sxs-lookup"><span data-stu-id="a9654-133">In the search box, type **Moxtra**.</span></span>

    ![Creating an Azure AD test user](./media/moxtra-tutorial/tutorial_moxtra_search.png)

1. <span data-ttu-id="a9654-135">In the results panel, select **Moxtra**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="a9654-135">In the results panel, select **Moxtra**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/moxtra-tutorial/tutorial_moxtra_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a9654-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a9654-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a9654-138">In this section, you configure and test Azure AD single sign-on with Moxtra based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a9654-138">In this section, you configure and test Azure AD single sign-on with Moxtra based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a9654-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Moxtra is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a9654-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Moxtra is to a user in Azure AD.</span></span> <span data-ttu-id="a9654-140">In other words, a link relationship between an Azure AD user and the related user in Moxtra needs to be established.</span><span class="sxs-lookup"><span data-stu-id="a9654-140">In other words, a link relationship between an Azure AD user and the related user in Moxtra needs to be established.</span></span>

<span data-ttu-id="a9654-141">In Moxtra, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="a9654-141">In Moxtra, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a9654-142">To configure and test Azure AD single sign-on with Moxtra, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="a9654-142">To configure and test Azure AD single sign-on with Moxtra, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a9654-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="a9654-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="a9654-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a9654-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="a9654-145">**[Creating a Moxtra test user](#creating-a-moxtra-test-user)** - to have a counterpart of Britta Simon in Moxtra that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="a9654-145">**[Creating a Moxtra test user](#creating-a-moxtra-test-user)** - to have a counterpart of Britta Simon in Moxtra that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="a9654-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a9654-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="a9654-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="a9654-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a9654-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a9654-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a9654-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Moxtra application.</span><span class="sxs-lookup"><span data-stu-id="a9654-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Moxtra application.</span></span>

<span data-ttu-id="a9654-150">**To configure Azure AD single sign-on with Moxtra, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a9654-150">**To configure Azure AD single sign-on with Moxtra, perform the following steps:**</span></span>

1. <span data-ttu-id="a9654-151">In the Azure portal, on the **Moxtra** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="a9654-151">In the Azure portal, on the **Moxtra** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="a9654-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a9654-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/moxtra-tutorial/tutorial_moxtra_samlbase.png)

1. <span data-ttu-id="a9654-155">On the **Moxtra Domain and URLs** section, perform the following step:</span><span class="sxs-lookup"><span data-stu-id="a9654-155">On the **Moxtra Domain and URLs** section, perform the following step:</span></span>

    ![Configure Single Sign-On](./media/moxtra-tutorial/tutorial_moxtra_url.png)

    <span data-ttu-id="a9654-157">In the **Sign-on URL** textbox, type a URL as: `https://www.moxtra.com/service/#login`</span><span class="sxs-lookup"><span data-stu-id="a9654-157">In the **Sign-on URL** textbox, type a URL as: `https://www.moxtra.com/service/#login`</span></span>

1. <span data-ttu-id="a9654-158">Moxtra application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="a9654-158">Moxtra application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="a9654-159">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="a9654-159">Configure the following claims for this application.</span></span> <span data-ttu-id="a9654-160">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="a9654-160">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="a9654-161">The following screenshot shows an example for this configuration.</span><span class="sxs-lookup"><span data-stu-id="a9654-161">The following screenshot shows an example for this configuration.</span></span> 

    ![Configure Single Sign-On](./media/moxtra-tutorial/tutorial_moxtra_attributes.png)
    
1. <span data-ttu-id="a9654-163">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a9654-163">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="a9654-164">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="a9654-164">Attribute Name</span></span> | <span data-ttu-id="a9654-165">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="a9654-165">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="a9654-166">firstname</span><span class="sxs-lookup"><span data-stu-id="a9654-166">firstname</span></span> | <span data-ttu-id="a9654-167">user.givenname</span><span class="sxs-lookup"><span data-stu-id="a9654-167">user.givenname</span></span> |
    | <span data-ttu-id="a9654-168">lastname</span><span class="sxs-lookup"><span data-stu-id="a9654-168">lastname</span></span> | <span data-ttu-id="a9654-169">user.surname</span><span class="sxs-lookup"><span data-stu-id="a9654-169">user.surname</span></span> |
    | <span data-ttu-id="a9654-170">idpid</span><span class="sxs-lookup"><span data-stu-id="a9654-170">idpid</span></span>    | <span data-ttu-id="a9654-171">< SAML Entity ID ></span><span class="sxs-lookup"><span data-stu-id="a9654-171">< SAML Entity ID ></span></span> 

    > [!Note]
    > <span data-ttu-id="a9654-172">The value of **idpid** attribute is not real.</span><span class="sxs-lookup"><span data-stu-id="a9654-172">The value of **idpid** attribute is not real.</span></span> <span data-ttu-id="a9654-173">You can get the actual value from **Quick reference** section under **Moxtra Configuration**.</span><span class="sxs-lookup"><span data-stu-id="a9654-173">You can get the actual value from **Quick reference** section under **Moxtra Configuration**.</span></span>
    
    <span data-ttu-id="a9654-174">a.</span><span class="sxs-lookup"><span data-stu-id="a9654-174">a.</span></span> <span data-ttu-id="a9654-175">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="a9654-175">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/moxtra-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="a9654-177">b.</span><span class="sxs-lookup"><span data-stu-id="a9654-177">b.</span></span> <span data-ttu-id="a9654-178">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="a9654-178">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    ![Configure Single Sign-On](./media/moxtra-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="a9654-180">c.</span><span class="sxs-lookup"><span data-stu-id="a9654-180">c.</span></span> <span data-ttu-id="a9654-181">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="a9654-181">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="a9654-182">d.</span><span class="sxs-lookup"><span data-stu-id="a9654-182">d.</span></span> <span data-ttu-id="a9654-183">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="a9654-183">Click **Ok**.</span></span>
    
1. <span data-ttu-id="a9654-184">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="a9654-184">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/moxtra-tutorial/tutorial_moxtra_certificate.png) 

1. <span data-ttu-id="a9654-186">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="a9654-186">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/moxtra-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="a9654-188">On the **Moxtra Configuration** section, click **Configure Moxtra** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="a9654-188">On the **Moxtra Configuration** section, click **Configure Moxtra** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a9654-189">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="a9654-189">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/moxtra-tutorial/tutorial_moxtra_configure.png) 

1. <span data-ttu-id="a9654-191">In another browser window, sign on to your Moxtra company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="a9654-191">In another browser window, sign on to your Moxtra company site as an administrator.</span></span>

1. <span data-ttu-id="a9654-192">In the toolbar on the left, click **Admin Console > SAML Single Sign-on**, and then click **New**.</span><span class="sxs-lookup"><span data-stu-id="a9654-192">In the toolbar on the left, click **Admin Console > SAML Single Sign-on**, and then click **New**.</span></span>
   
    ![Configure Single Sign-On](./media/moxtra-tutorial/tutorial_moxtra_06.png) 

1. <span data-ttu-id="a9654-194">On the **SAML** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a9654-194">On the **SAML** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](./media/moxtra-tutorial/tutorial_moxtra_08.png)   
 
    <span data-ttu-id="a9654-196">a.</span><span class="sxs-lookup"><span data-stu-id="a9654-196">a.</span></span> <span data-ttu-id="a9654-197">In the **Name** textbox, type a name for your configuration (e.g.: *SAML*).</span><span class="sxs-lookup"><span data-stu-id="a9654-197">In the **Name** textbox, type a name for your configuration (e.g.: *SAML*).</span></span> 
  
    <span data-ttu-id="a9654-198">b.</span><span class="sxs-lookup"><span data-stu-id="a9654-198">b.</span></span> <span data-ttu-id="a9654-199">In the **IdP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a9654-199">In the **IdP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="a9654-200">c.</span><span class="sxs-lookup"><span data-stu-id="a9654-200">c.</span></span> <span data-ttu-id="a9654-201">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a9654-201">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="a9654-202">d.</span><span class="sxs-lookup"><span data-stu-id="a9654-202">d.</span></span> <span data-ttu-id="a9654-203">In the **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span><span class="sxs-lookup"><span data-stu-id="a9654-203">In the **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span> 
 
    <span data-ttu-id="a9654-204">e.</span><span class="sxs-lookup"><span data-stu-id="a9654-204">e.</span></span> <span data-ttu-id="a9654-205">In the **NameID Format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="a9654-205">In the **NameID Format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span> 
 
    <span data-ttu-id="a9654-206">f.</span><span class="sxs-lookup"><span data-stu-id="a9654-206">f.</span></span> <span data-ttu-id="a9654-207">Open certificate which you have downloaded from Azure portal in notepad, copy the content, and then paste it into the **Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="a9654-207">Open certificate which you have downloaded from Azure portal in notepad, copy the content, and then paste it into the **Certificate** textbox.</span></span>    
 
    <span data-ttu-id="a9654-208">g.</span><span class="sxs-lookup"><span data-stu-id="a9654-208">g.</span></span> <span data-ttu-id="a9654-209">In the SAML email domain textbox, type your SAML email domain.</span><span class="sxs-lookup"><span data-stu-id="a9654-209">In the SAML email domain textbox, type your SAML email domain.</span></span>    
  
    >[!NOTE]
    ><span data-ttu-id="a9654-210">To see the steps to verify the domain, click the "**i**" below.</span><span class="sxs-lookup"><span data-stu-id="a9654-210">To see the steps to verify the domain, click the "**i**" below.</span></span>

    <span data-ttu-id="a9654-211">h.</span><span class="sxs-lookup"><span data-stu-id="a9654-211">h.</span></span> <span data-ttu-id="a9654-212">Click **Update**.</span><span class="sxs-lookup"><span data-stu-id="a9654-212">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="a9654-213">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="a9654-213">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a9654-214">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="a9654-214">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a9654-215">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a9654-215">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a9654-216">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a9654-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="a9654-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a9654-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="a9654-219">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a9654-219">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a9654-220">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a9654-220">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/moxtra-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="a9654-222">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="a9654-222">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/moxtra-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="a9654-224">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="a9654-224">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/moxtra-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="a9654-226">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a9654-226">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/moxtra-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a9654-228">a.</span><span class="sxs-lookup"><span data-stu-id="a9654-228">a.</span></span> <span data-ttu-id="a9654-229">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a9654-229">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a9654-230">b.</span><span class="sxs-lookup"><span data-stu-id="a9654-230">b.</span></span> <span data-ttu-id="a9654-231">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a9654-231">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a9654-232">c.</span><span class="sxs-lookup"><span data-stu-id="a9654-232">c.</span></span> <span data-ttu-id="a9654-233">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="a9654-233">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a9654-234">d.</span><span class="sxs-lookup"><span data-stu-id="a9654-234">d.</span></span> <span data-ttu-id="a9654-235">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a9654-235">Click **Create**.</span></span>
 
### <a name="creating-a-moxtra-test-user"></a><span data-ttu-id="a9654-236">Creating a Moxtra test user</span><span class="sxs-lookup"><span data-stu-id="a9654-236">Creating a Moxtra test user</span></span>

<span data-ttu-id="a9654-237">The objective of this section is to create a user called Britta Simon in Moxtra.</span><span class="sxs-lookup"><span data-stu-id="a9654-237">The objective of this section is to create a user called Britta Simon in Moxtra.</span></span>

<span data-ttu-id="a9654-238">**To create a user called Britta Simon in Moxtra, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a9654-238">**To create a user called Britta Simon in Moxtra, perform the following steps:**</span></span>

1. <span data-ttu-id="a9654-239">Sign on to your Moxtra company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="a9654-239">Sign on to your Moxtra company site as an administrator.</span></span>

1. <span data-ttu-id="a9654-240">In the toolbar on the left, click **Admin Console > User Management**, and then **Add User**.</span><span class="sxs-lookup"><span data-stu-id="a9654-240">In the toolbar on the left, click **Admin Console > User Management**, and then **Add User**.</span></span>
   
    ![Configure Single Sign-On](./media/moxtra-tutorial/tutorial_moxtra_10.png) 

1. <span data-ttu-id="a9654-242">On the **Add User** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a9654-242">On the **Add User** dialog, perform the following steps:</span></span>
  
    <span data-ttu-id="a9654-243">a.</span><span class="sxs-lookup"><span data-stu-id="a9654-243">a.</span></span> <span data-ttu-id="a9654-244">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="a9654-244">In the **First Name** textbox, type **Britta**.</span></span>
  
    <span data-ttu-id="a9654-245">b.</span><span class="sxs-lookup"><span data-stu-id="a9654-245">b.</span></span> <span data-ttu-id="a9654-246">In the **Last Name** textbox, type **Simon**.</span><span class="sxs-lookup"><span data-stu-id="a9654-246">In the **Last Name** textbox, type **Simon**.</span></span>
  
    <span data-ttu-id="a9654-247">c.</span><span class="sxs-lookup"><span data-stu-id="a9654-247">c.</span></span> <span data-ttu-id="a9654-248">In the **Email** textbox, type Britta's email address same as on Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a9654-248">In the **Email** textbox, type Britta's email address same as on Azure portal.</span></span>
  
    <span data-ttu-id="a9654-249">d.</span><span class="sxs-lookup"><span data-stu-id="a9654-249">d.</span></span> <span data-ttu-id="a9654-250">In the **Division** textbox, type **Dev**.</span><span class="sxs-lookup"><span data-stu-id="a9654-250">In the **Division** textbox, type **Dev**.</span></span>
  
    <span data-ttu-id="a9654-251">e.</span><span class="sxs-lookup"><span data-stu-id="a9654-251">e.</span></span> <span data-ttu-id="a9654-252">In the **Department** textbox, type **IT**.</span><span class="sxs-lookup"><span data-stu-id="a9654-252">In the **Department** textbox, type **IT**.</span></span>
  
    <span data-ttu-id="a9654-253">f.</span><span class="sxs-lookup"><span data-stu-id="a9654-253">f.</span></span> <span data-ttu-id="a9654-254">Select **Administrator**.</span><span class="sxs-lookup"><span data-stu-id="a9654-254">Select **Administrator**.</span></span>
  
    <span data-ttu-id="a9654-255">g.</span><span class="sxs-lookup"><span data-stu-id="a9654-255">g.</span></span> <span data-ttu-id="a9654-256">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="a9654-256">Click **Add**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a9654-257">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a9654-257">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a9654-258">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Moxtra.</span><span class="sxs-lookup"><span data-stu-id="a9654-258">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Moxtra.</span></span>

![Assign User][200] 

<span data-ttu-id="a9654-260">**To assign Britta Simon to Moxtra, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a9654-260">**To assign Britta Simon to Moxtra, perform the following steps:**</span></span>

1. <span data-ttu-id="a9654-261">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a9654-261">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="a9654-263">In the applications list, select **Moxtra**.</span><span class="sxs-lookup"><span data-stu-id="a9654-263">In the applications list, select **Moxtra**.</span></span>

    ![Configure Single Sign-On](./media/moxtra-tutorial/tutorial_moxtra_app.png) 

1. <span data-ttu-id="a9654-265">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="a9654-265">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="a9654-267">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="a9654-267">Click **Add** button.</span></span> <span data-ttu-id="a9654-268">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a9654-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="a9654-270">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="a9654-270">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="a9654-271">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="a9654-271">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="a9654-272">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a9654-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a9654-273">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="a9654-273">Testing single sign-on</span></span>

<span data-ttu-id="a9654-274">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a9654-274">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a9654-275">When you click the Moxtra tile in the Access Panel, you should get automatically signed-on to your Moxtra application.</span><span class="sxs-lookup"><span data-stu-id="a9654-275">When you click the Moxtra tile in the Access Panel, you should get automatically signed-on to your Moxtra application.</span></span>
<span data-ttu-id="a9654-276">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a9654-276">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a9654-277">Additional resources</span><span class="sxs-lookup"><span data-stu-id="a9654-277">Additional resources</span></span>

* [<span data-ttu-id="a9654-278">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a9654-278">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="a9654-279">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a9654-279">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/moxtra-tutorial/tutorial_general_01.png
[2]: ./media/moxtra-tutorial/tutorial_general_02.png
[3]: ./media/moxtra-tutorial/tutorial_general_03.png
[4]: ./media/moxtra-tutorial/tutorial_general_04.png

[100]: ./media/moxtra-tutorial/tutorial_general_100.png

[200]: ./media/moxtra-tutorial/tutorial_general_200.png
[201]: ./media/moxtra-tutorial/tutorial_general_201.png
[202]: ./media/moxtra-tutorial/tutorial_general_202.png
[203]: ./media/moxtra-tutorial/tutorial_general_203.png

