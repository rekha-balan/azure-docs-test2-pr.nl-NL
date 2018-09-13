---
title: 'Tutorial: Azure Active Directory integration with Moxtra | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Moxtra.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 2aed2d4b-1dcd-4839-8fed-9419d107c61c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: jeedes
ms.openlocfilehash: a5ff803dc1e88b0012e3ceb448f55aa4fb7f2b36
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555463"
---
# <a name="tutorial-azure-active-directory-integration-with-moxtra"></a><span data-ttu-id="24f48-103">Tutorial: Azure Active Directory integration with Moxtra</span><span class="sxs-lookup"><span data-stu-id="24f48-103">Tutorial: Azure Active Directory integration with Moxtra</span></span>
<span data-ttu-id="24f48-104">The objective of this tutorial is to show you how to integrate Moxtra with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="24f48-104">The objective of this tutorial is to show you how to integrate Moxtra with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="24f48-105">Integrating Moxtra with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="24f48-105">Integrating Moxtra with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="24f48-106">You can control in Azure AD who has access to Moxtra</span><span class="sxs-lookup"><span data-stu-id="24f48-106">You can control in Azure AD who has access to Moxtra</span></span> 
* <span data-ttu-id="24f48-107">You can enable your users to automatically get signed-on to Moxtra single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="24f48-107">You can enable your users to automatically get signed-on to Moxtra single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="24f48-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="24f48-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="24f48-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="24f48-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24f48-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="24f48-110">Prerequisites</span></span>
<span data-ttu-id="24f48-111">To configure Azure AD integration with Moxtra, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="24f48-111">To configure Azure AD integration with Moxtra, you need the following items:</span></span>

* <span data-ttu-id="24f48-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="24f48-112">An Azure AD subscription</span></span>
* <span data-ttu-id="24f48-113">A Moxtra single-sign (SSO) on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="24f48-113">A Moxtra single-sign (SSO) on enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="24f48-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="24f48-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="24f48-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="24f48-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="24f48-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="24f48-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="24f48-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="24f48-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="24f48-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="24f48-118">Scenario Description</span></span>
<span data-ttu-id="24f48-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="24f48-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="24f48-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="24f48-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="24f48-121">Adding Moxtra from the gallery</span><span class="sxs-lookup"><span data-stu-id="24f48-121">Adding Moxtra from the gallery</span></span> 
2. <span data-ttu-id="24f48-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="24f48-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-moxtra-from-the-gallery"></a><span data-ttu-id="24f48-123">Adding Moxtra from the gallery</span><span class="sxs-lookup"><span data-stu-id="24f48-123">Adding Moxtra from the gallery</span></span>
<span data-ttu-id="24f48-124">To configure the integration of Moxtra into Azure AD, you need to add Moxtra from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="24f48-124">To configure the integration of Moxtra into Azure AD, you need to add Moxtra from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="24f48-125">**To add Moxtra from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="24f48-125">**To add Moxtra from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="24f48-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="24f48-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="24f48-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="24f48-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="24f48-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="24f48-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="24f48-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="24f48-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="24f48-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="24f48-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="24f48-135">In the search box, type **Moxtra**.</span><span class="sxs-lookup"><span data-stu-id="24f48-135">In the search box, type **Moxtra**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_01.png)
7. <span data-ttu-id="24f48-137">In the results pane, select **Moxtra**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="24f48-137">In the results pane, select **Moxtra**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_02.png)

## <a name="configuring-and-testing-azure-ad-sso"></a><span data-ttu-id="24f48-139">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="24f48-139">Configuring and testing Azure AD SSO</span></span>
<span data-ttu-id="24f48-140">The objective of this section is to show you how to configure and test Azure AD sSSO with Moxtra based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="24f48-140">The objective of this section is to show you how to configure and test Azure AD sSSO with Moxtra based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="24f48-141">For SSO to work, Azure AD needs to know what the counterpart user in Moxtra to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="24f48-141">For SSO to work, Azure AD needs to know what the counterpart user in Moxtra to an user in Azure AD is.</span></span> <span data-ttu-id="24f48-142">In other words, a link relationship between an Azure AD user and the related user in Moxtra needs to be established.</span><span class="sxs-lookup"><span data-stu-id="24f48-142">In other words, a link relationship between an Azure AD user and the related user in Moxtra needs to be established.</span></span>

<span data-ttu-id="24f48-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Moxtra.</span><span class="sxs-lookup"><span data-stu-id="24f48-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Moxtra.</span></span>

<span data-ttu-id="24f48-144">To configure and test Azure AD single sign-on with Moxtra, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="24f48-144">To configure and test Azure AD single sign-on with Moxtra, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="24f48-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="24f48-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="24f48-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="24f48-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="24f48-147">**[Creating a Moxtra test user](#creating-a-moxtra-test-user)** - to have a counterpart of Britta Simon in Moxtra that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="24f48-147">**[Creating a Moxtra test user](#creating-a-moxtra-test-user)** - to have a counterpart of Britta Simon in Moxtra that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="24f48-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="24f48-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="24f48-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="24f48-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="24f48-150">Configure Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="24f48-150">Configure Azure AD SSO</span></span>
<span data-ttu-id="24f48-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure SSO in your Moxtra application.</span><span class="sxs-lookup"><span data-stu-id="24f48-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure SSO in your Moxtra application.</span></span> 

<span data-ttu-id="24f48-152">Your Moxtra application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your saml token attributes configuration.</span><span class="sxs-lookup"><span data-stu-id="24f48-152">Your Moxtra application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your saml token attributes configuration.</span></span> <span data-ttu-id="24f48-153">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="24f48-153">The following screenshot shows an example for this.</span></span>

![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_09.png) 

<span data-ttu-id="24f48-155">**To configure Azure AD single sign-on with Moxtra, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="24f48-155">**To configure Azure AD single sign-on with Moxtra, perform the following steps:**</span></span>

1. <span data-ttu-id="24f48-156">In the Azure classic portal, on the **Moxtra** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="24f48-156">In the Azure classic portal, on the **Moxtra** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="24f48-158">On the **How would you like users to sign on to Moxtra** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="24f48-158">On the **How would you like users to sign on to Moxtra** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_03.png) 
3. <span data-ttu-id="24f48-160">On the **Configure App Settings** dialog page, perform the following steps:.</span><span class="sxs-lookup"><span data-stu-id="24f48-160">On the **Configure App Settings** dialog page, perform the following steps:.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_04.png) 
  1. <span data-ttu-id="24f48-162">In the **Sign On URL** textbox, type the following URL: **https://www.moxtra.com/service/#login**.</span><span class="sxs-lookup"><span data-stu-id="24f48-162">In the **Sign On URL** textbox, type the following URL: **https://www.moxtra.com/service/#login**.</span></span> 
  2. <span data-ttu-id="24f48-163">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="24f48-163">Click **Next**.</span></span>
4. <span data-ttu-id="24f48-164">On the **Configure single sign-on at Moxtra** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="24f48-164">On the **Configure single sign-on at Moxtra** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_05.png) 
  1. <span data-ttu-id="24f48-166">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="24f48-166">Click **Download certificate**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="24f48-167">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="24f48-167">Click **Next**.</span></span>
5. <span data-ttu-id="24f48-168">In another browser window, sign on to your Moxtra company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="24f48-168">In another browser window, sign on to your Moxtra company site as an administrator.</span></span>
6. <span data-ttu-id="24f48-169">In the toolbar on the left, click **Admin Console > SAML Single Sign-on**, and then **New**.</span><span class="sxs-lookup"><span data-stu-id="24f48-169">In the toolbar on the left, click **Admin Console > SAML Single Sign-on**, and then **New**.</span></span>
   
  ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_06.png) 
7. <span data-ttu-id="24f48-171">On the **SAML** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="24f48-171">On the **SAML** page, perform the following steps:</span></span>
   
  ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_08.png)   
  1. <span data-ttu-id="24f48-173">In the **Name** textbox, type a name for your configuration (e.g.: *SAML*).</span><span class="sxs-lookup"><span data-stu-id="24f48-173">In the **Name** textbox, type a name for your configuration (e.g.: *SAML*).</span></span> 
  2. <span data-ttu-id="24f48-174">In the Azure classic portal, on the **Configure single sign-on at Moxtra** dialog page, copy the **Entity ID** value, and then paste it into the **IdP Entity ID** textbox.</span><span class="sxs-lookup"><span data-stu-id="24f48-174">In the Azure classic portal, on the **Configure single sign-on at Moxtra** dialog page, copy the **Entity ID** value, and then paste it into the **IdP Entity ID** textbox.</span></span> 
  3. <span data-ttu-id="24f48-175">In the Azure classic portal, on the **Configure single sign-on at Moxtra** dialog page, copy the **Remote Login URL** value, and then paste it into the **Login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="24f48-175">In the Azure classic portal, on the **Configure single sign-on at Moxtra** dialog page, copy the **Remote Login URL** value, and then paste it into the **Login URL** textbox.</span></span> 
  4. <span data-ttu-id="24f48-176">In the **AuthnContextClassRef** textbox, tyoe **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span><span class="sxs-lookup"><span data-stu-id="24f48-176">In the **AuthnContextClassRef** textbox, tyoe **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span> 
  5. <span data-ttu-id="24f48-177">In the Azure classic portal, on the **Configure single sign-on at Moxtra** dialog page, copy the **Name Identifier Format** value, and then paste it into the **NameID Format** textbox.</span><span class="sxs-lookup"><span data-stu-id="24f48-177">In the Azure classic portal, on the **Configure single sign-on at Moxtra** dialog page, copy the **Name Identifier Format** value, and then paste it into the **NameID Format** textbox.</span></span> 
  6. <span data-ttu-id="24f48-178">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="24f48-178">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **Certificate** textbox.</span></span>    
  7. <span data-ttu-id="24f48-179">In the SAML email domain textbox, type your SAML email domain.</span><span class="sxs-lookup"><span data-stu-id="24f48-179">In the SAML email domain textbox, type your SAML email domain.</span></span>    
   
   >[!NOTE]
   ><span data-ttu-id="24f48-180">To see the steps to verify the domain, click the "**i**" below.</span><span class="sxs-lookup"><span data-stu-id="24f48-180">To see the steps to verify the domain, click the "**i**" below.</span></span>
   >  
  8. <span data-ttu-id="24f48-181">Click **Update**.</span><span class="sxs-lookup"><span data-stu-id="24f48-181">Click **Update**.</span></span>
8. <span data-ttu-id="24f48-182">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="24f48-182">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
  ![Azure AD Single Sign-On][10]
9. <span data-ttu-id="24f48-184">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="24f48-184">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
  
  ![Azure AD Single Sign-On][11]
19. <span data-ttu-id="24f48-186">To add custom attribute mappings to your saml token attributes configuration, in the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span><span class="sxs-lookup"><span data-stu-id="24f48-186">To add custom attribute mappings to your saml token attributes configuration, in the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span></span> 
   
  ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_general_80.png) 
11. <span data-ttu-id="24f48-188">For each data row in the table below, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="24f48-188">For each data row in the table below, perform the following steps:</span></span>
   
     | <span data-ttu-id="24f48-189">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="24f48-189">Attribute Name</span></span> | <span data-ttu-id="24f48-190">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="24f48-190">Attribute Value</span></span> |
     | --- | --- |
     | <span data-ttu-id="24f48-191">firstname</span><span class="sxs-lookup"><span data-stu-id="24f48-191">firstname</span></span> |<span data-ttu-id="24f48-192">givenname</span><span class="sxs-lookup"><span data-stu-id="24f48-192">givenname</span></span> |
     | <span data-ttu-id="24f48-193">lastname</span><span class="sxs-lookup"><span data-stu-id="24f48-193">lastname</span></span> |<span data-ttu-id="24f48-194">surname</span><span class="sxs-lookup"><span data-stu-id="24f48-194">surname</span></span> |
     | <span data-ttu-id="24f48-195">idpid</span><span class="sxs-lookup"><span data-stu-id="24f48-195">idpid</span></span> |<span data-ttu-id="24f48-196">*\<the **Entity ID** value from the **Configure single sign-on at Moxtra** dialog in the Azure classic portal \>*</span><span class="sxs-lookup"><span data-stu-id="24f48-196">*\<the **Entity ID** value from the **Configure single sign-on at Moxtra** dialog in the Azure classic portal \>*</span></span> |
  1. <span data-ttu-id="24f48-197">Click add user attribute</span><span class="sxs-lookup"><span data-stu-id="24f48-197">Click add user attribute</span></span> 

     ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_general_81.png) 
  2. <span data-ttu-id="24f48-199">On the **Add User Attribute** dialog, type the attribute name and attribute value shown for that row in the table.</span><span class="sxs-lookup"><span data-stu-id="24f48-199">On the **Add User Attribute** dialog, type the attribute name and attribute value shown for that row in the table.</span></span> 

     ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_general_82.png) 
  3. <span data-ttu-id="24f48-201">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="24f48-201">Click **Complete**.</span></span>
12. <span data-ttu-id="24f48-202">Click **Apply Changes**.</span><span class="sxs-lookup"><span data-stu-id="24f48-202">Click **Apply Changes**.</span></span> 
   
  ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_general_84.png) 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="24f48-204">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="24f48-204">Create an Azure AD test user</span></span>
<span data-ttu-id="24f48-205">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="24f48-205">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

![Create Azure AD User][20]

<span data-ttu-id="24f48-207">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="24f48-207">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="24f48-208">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="24f48-208">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/create_aaduser_09.png)  
2. <span data-ttu-id="24f48-210">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="24f48-210">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="24f48-211">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="24f48-211">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="24f48-213">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="24f48-213">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="24f48-215">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="24f48-215">On the **Tell us about this user** dialog page, perform the following steps:</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/create_aaduser_05.png)  
  1. <span data-ttu-id="24f48-217">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="24f48-217">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="24f48-218">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="24f48-218">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="24f48-219">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="24f48-219">Click **Next**.</span></span>
6. <span data-ttu-id="24f48-220">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="24f48-220">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="24f48-222">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="24f48-222">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="24f48-223">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="24f48-223">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="24f48-224">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="24f48-224">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="24f48-225">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="24f48-225">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="24f48-226">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="24f48-226">Click **Next**.</span></span>
7. <span data-ttu-id="24f48-227">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="24f48-227">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="24f48-229">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="24f48-229">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="24f48-231">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="24f48-231">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="24f48-232">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="24f48-232">Click **Complete**.</span></span>   

### <a name="create-a-moxtra-test-user"></a><span data-ttu-id="24f48-233">Create a Moxtra test user</span><span class="sxs-lookup"><span data-stu-id="24f48-233">Create a Moxtra test user</span></span>
<span data-ttu-id="24f48-234">The objective of this section is to create a user called Britta Simon in Moxtra.</span><span class="sxs-lookup"><span data-stu-id="24f48-234">The objective of this section is to create a user called Britta Simon in Moxtra.</span></span>

<span data-ttu-id="24f48-235">**To create a user called Britta Simon in Moxtra, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="24f48-235">**To create a user called Britta Simon in Moxtra, perform the following steps:**</span></span>

1. <span data-ttu-id="24f48-236">Sign-on to your Moxtra company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="24f48-236">Sign-on to your Moxtra company site as an administrator.</span></span>
2. <span data-ttu-id="24f48-237">In the toolbar on the left, click **Admin Console > User Management**, and then **Add User**.</span><span class="sxs-lookup"><span data-stu-id="24f48-237">In the toolbar on the left, click **Admin Console > User Management**, and then **Add User**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_10.png) 
3. <span data-ttu-id="24f48-239">On the **Add User** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="24f48-239">On the **Add User** dialog, perform the following steps:</span></span>
  1. <span data-ttu-id="24f48-240">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="24f48-240">In the **First Name** textbox, type **Britta**.</span></span>
  2. <span data-ttu-id="24f48-241">In the **Last Name** textbox, type **Simon**.</span><span class="sxs-lookup"><span data-stu-id="24f48-241">In the **Last Name** textbox, type **Simon**.</span></span>
  3. <span data-ttu-id="24f48-242">In the **Email** textbox, type Britta's email address in the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="24f48-242">In the **Email** textbox, type Britta's email address in the Azure classic portal.</span></span>
  4. <span data-ttu-id="24f48-243">In the **Division** textbox, type **Dev**.</span><span class="sxs-lookup"><span data-stu-id="24f48-243">In the **Division** textbox, type **Dev**.</span></span>
  5. <span data-ttu-id="24f48-244">In the **Department** textbox, type **IT**.</span><span class="sxs-lookup"><span data-stu-id="24f48-244">In the **Department** textbox, type **IT**.</span></span>
  6. <span data-ttu-id="24f48-245">Select **Adminitrator**.</span><span class="sxs-lookup"><span data-stu-id="24f48-245">Select **Adminitrator**.</span></span>
  7. <span data-ttu-id="24f48-246">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="24f48-246">Click **Add**.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="24f48-247">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="24f48-247">Assign the Azure AD test user</span></span>
<span data-ttu-id="24f48-248">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Moxtra.</span><span class="sxs-lookup"><span data-stu-id="24f48-248">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Moxtra.</span></span>

![Assign User][200] 

<span data-ttu-id="24f48-250">**To assign Britta Simon to Moxtra, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="24f48-250">**To assign Britta Simon to Moxtra, perform the following steps:**</span></span>

1. <span data-ttu-id="24f48-251">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="24f48-251">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="24f48-253">In the applications list, select **Moxtra**.</span><span class="sxs-lookup"><span data-stu-id="24f48-253">In the applications list, select **Moxtra**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_50.png) 
3. <span data-ttu-id="24f48-255">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="24f48-255">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="24f48-257">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="24f48-257">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="24f48-258">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="24f48-258">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="24f48-260">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="24f48-260">Test single sign-on</span></span>
<span data-ttu-id="24f48-261">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="24f48-261">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="24f48-262">When you click the Moxtra tile in the Access Panel, you should get automatically signed-on to your Moxtra application.</span><span class="sxs-lookup"><span data-stu-id="24f48-262">When you click the Moxtra tile in the Access Panel, you should get automatically signed-on to your Moxtra application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="24f48-263">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="24f48-263">Additional Resources</span></span>
* [<span data-ttu-id="24f48-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="24f48-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="24f48-265">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="24f48-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_general_205.png







































