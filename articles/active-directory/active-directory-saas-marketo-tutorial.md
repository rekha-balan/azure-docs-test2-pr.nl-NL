---
title: 'Tutorial: Azure Active Directory integration with Marketo | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Marketo.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: b88c45f5-d288-4717-835c-ca965add8735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 6397525a602b707a1269006e95ee54606e7c1143
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563428"
---
# <a name="tutorial-azure-active-directory-integration-with-marketo"></a><span data-ttu-id="6263e-103">Tutorial: Azure Active Directory integration with Marketo</span><span class="sxs-lookup"><span data-stu-id="6263e-103">Tutorial: Azure Active Directory integration with Marketo</span></span>
<span data-ttu-id="6263e-104">In this tutorial, you learn how to integrate Marketo with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6263e-104">In this tutorial, you learn how to integrate Marketo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6263e-105">Integrating Marketo with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="6263e-105">Integrating Marketo with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="6263e-106">You can control in Azure AD who has access to Marketo</span><span class="sxs-lookup"><span data-stu-id="6263e-106">You can control in Azure AD who has access to Marketo</span></span>
* <span data-ttu-id="6263e-107">You can enable your users to automatically get signed-on to Marketo (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="6263e-107">You can enable your users to automatically get signed-on to Marketo (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="6263e-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="6263e-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="6263e-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6263e-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6263e-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6263e-110">Prerequisites</span></span>
<span data-ttu-id="6263e-111">To configure Azure AD integration with Marketo, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="6263e-111">To configure Azure AD integration with Marketo, you need the following items:</span></span>

* <span data-ttu-id="6263e-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="6263e-112">An Azure AD subscription</span></span>
* <span data-ttu-id="6263e-113">A Marketo single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="6263e-113">A Marketo single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6263e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="6263e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="6263e-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="6263e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="6263e-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="6263e-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="6263e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6263e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6263e-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="6263e-118">Scenario description</span></span>
<span data-ttu-id="6263e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="6263e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="6263e-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="6263e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6263e-121">Adding Marketo from the gallery</span><span class="sxs-lookup"><span data-stu-id="6263e-121">Adding Marketo from the gallery</span></span>
2. <span data-ttu-id="6263e-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6263e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-marketo-from-the-gallery"></a><span data-ttu-id="6263e-123">Adding Marketo from the gallery</span><span class="sxs-lookup"><span data-stu-id="6263e-123">Adding Marketo from the gallery</span></span>
<span data-ttu-id="6263e-124">To configure the integration of Marketo into Azure AD, you need to add Marketo from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="6263e-124">To configure the integration of Marketo into Azure AD, you need to add Marketo from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6263e-125">**To add Marketo from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6263e-125">**To add Marketo from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6263e-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6263e-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Active Directory][1]
2. <span data-ttu-id="6263e-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="6263e-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="6263e-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="6263e-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="6263e-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="6263e-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="6263e-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="6263e-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="6263e-135">In the search box, type **Marketo**.</span><span class="sxs-lookup"><span data-stu-id="6263e-135">In the search box, type **Marketo**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/tutorial_marketo_01.png)
7. <span data-ttu-id="6263e-137">In the results pane, select **Marketo**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="6263e-137">In the results pane, select **Marketo**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/tutorial_marketo_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6263e-139">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6263e-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6263e-140">In this section, you configure and test Azure AD single sign-on with Marketo based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6263e-140">In this section, you configure and test Azure AD single sign-on with Marketo based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6263e-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Marketo is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6263e-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Marketo is to a user in Azure AD.</span></span> <span data-ttu-id="6263e-142">In other words, a link relationship between an Azure AD user and the related user in Marketo needs to be established.</span><span class="sxs-lookup"><span data-stu-id="6263e-142">In other words, a link relationship between an Azure AD user and the related user in Marketo needs to be established.</span></span>

<span data-ttu-id="6263e-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Marketo.</span><span class="sxs-lookup"><span data-stu-id="6263e-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Marketo.</span></span>

<span data-ttu-id="6263e-144">To configure and test Azure AD single sign-on with Marketo, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="6263e-144">To configure and test Azure AD single sign-on with Marketo, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6263e-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="6263e-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6263e-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6263e-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6263e-147">**[Creating a Marketo test user](#creating-a-predictix-price-reporting-test-user)** - to have a counterpart of Britta Simon in Marketo that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="6263e-147">**[Creating a Marketo test user](#creating-a-predictix-price-reporting-test-user)** - to have a counterpart of Britta Simon in Marketo that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="6263e-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6263e-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6263e-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="6263e-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6263e-150">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6263e-150">Configuring Azure AD single sign-on</span></span>
<span data-ttu-id="6263e-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Marketo application.</span><span class="sxs-lookup"><span data-stu-id="6263e-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Marketo application.</span></span>

<span data-ttu-id="6263e-152">**To configure Azure AD single sign-on with Marketo, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6263e-152">**To configure Azure AD single sign-on with Marketo, perform the following steps:**</span></span>

1. <span data-ttu-id="6263e-153">In the classic portal, on the **Marketo** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="6263e-153">In the classic portal, on the **Marketo** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="6263e-155">On the **How would you like users to sign on to Marketo** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6263e-155">On the **How would you like users to sign on to Marketo** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/tutorial_marketo_03.png) 
3. <span data-ttu-id="6263e-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6263e-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/tutorial_marketo_04.png) 
   
    <span data-ttu-id="6263e-159">a.</span><span class="sxs-lookup"><span data-stu-id="6263e-159">a.</span></span> <span data-ttu-id="6263e-160">In the **Identifier** textbox, type the URL using the following pattern: `https://saml.marketo.com/sp`</span><span class="sxs-lookup"><span data-stu-id="6263e-160">In the **Identifier** textbox, type the URL using the following pattern: `https://saml.marketo.com/sp`</span></span>
   
    <span data-ttu-id="6263e-161">b.</span><span class="sxs-lookup"><span data-stu-id="6263e-161">b.</span></span> <span data-ttu-id="6263e-162">In the **Reply URL** textbox, type the URL using the following pattern: `https://login.marketo.com/saml/assertion/\<munchkinid\>`</span><span class="sxs-lookup"><span data-stu-id="6263e-162">In the **Reply URL** textbox, type the URL using the following pattern: `https://login.marketo.com/saml/assertion/\<munchkinid\>`</span></span>
   
    <span data-ttu-id="6263e-163">c.</span><span class="sxs-lookup"><span data-stu-id="6263e-163">c.</span></span> <span data-ttu-id="6263e-164">click **Next**</span><span class="sxs-lookup"><span data-stu-id="6263e-164">click **Next**</span></span>
4. <span data-ttu-id="6263e-165">On the **Configure single sign-on at Marketo** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6263e-165">On the **Configure single sign-on at Marketo** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/tutorial_marketo_05.png)
   
    <span data-ttu-id="6263e-167">a.</span><span class="sxs-lookup"><span data-stu-id="6263e-167">a.</span></span> <span data-ttu-id="6263e-168">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="6263e-168">Click **Download certificate**, and then save the file on your computer.</span></span>
   
    <span data-ttu-id="6263e-169">b.</span><span class="sxs-lookup"><span data-stu-id="6263e-169">b.</span></span> <span data-ttu-id="6263e-170">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6263e-170">Click **Next**.</span></span>
5. <span data-ttu-id="6263e-171">To get Munchkin Id of your application, log in to Marketo using admin credentials and perform following actions:</span><span class="sxs-lookup"><span data-stu-id="6263e-171">To get Munchkin Id of your application, log in to Marketo using admin credentials and perform following actions:</span></span>
   
    <span data-ttu-id="6263e-172">a.</span><span class="sxs-lookup"><span data-stu-id="6263e-172">a.</span></span> <span data-ttu-id="6263e-173">Login to Marketo app using admin credentials.</span><span class="sxs-lookup"><span data-stu-id="6263e-173">Login to Marketo app using admin credentials.</span></span>
   
    <span data-ttu-id="6263e-174">b.</span><span class="sxs-lookup"><span data-stu-id="6263e-174">b.</span></span> <span data-ttu-id="6263e-175">Click on the Admin button on the top navigation pane.</span><span class="sxs-lookup"><span data-stu-id="6263e-175">Click on the Admin button on the top navigation pane.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="6263e-177">c.</span><span class="sxs-lookup"><span data-stu-id="6263e-177">c.</span></span> <span data-ttu-id="6263e-178">Navigate to the Integration menu and click on the Munchkin link</span><span class="sxs-lookup"><span data-stu-id="6263e-178">Navigate to the Integration menu and click on the Munchkin link</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/tutorial_marketo_11.png)
   
    <span data-ttu-id="6263e-180">d.</span><span class="sxs-lookup"><span data-stu-id="6263e-180">d.</span></span> <span data-ttu-id="6263e-181">Copy the Munchkin Id shown on the screen and complete your Reply URL in the Azure AD configuration wizard.</span><span class="sxs-lookup"><span data-stu-id="6263e-181">Copy the Munchkin Id shown on the screen and complete your Reply URL in the Azure AD configuration wizard.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/tutorial_marketo_12.png)
6. <span data-ttu-id="6263e-183">To configure the SSO in the application, please follow the below steps:</span><span class="sxs-lookup"><span data-stu-id="6263e-183">To configure the SSO in the application, please follow the below steps:</span></span>
   
    <span data-ttu-id="6263e-184">a.</span><span class="sxs-lookup"><span data-stu-id="6263e-184">a.</span></span> <span data-ttu-id="6263e-185">Login to Marketo app using admin credentials.</span><span class="sxs-lookup"><span data-stu-id="6263e-185">Login to Marketo app using admin credentials.</span></span>
   
    <span data-ttu-id="6263e-186">b.</span><span class="sxs-lookup"><span data-stu-id="6263e-186">b.</span></span> <span data-ttu-id="6263e-187">Click on the Admin button on the top navigation pane.</span><span class="sxs-lookup"><span data-stu-id="6263e-187">Click on the Admin button on the top navigation pane.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="6263e-189">c.</span><span class="sxs-lookup"><span data-stu-id="6263e-189">c.</span></span> <span data-ttu-id="6263e-190">Navigate to the Integration menu and click on Single Sign On</span><span class="sxs-lookup"><span data-stu-id="6263e-190">Navigate to the Integration menu and click on Single Sign On</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/tutorial_marketo_07.png) 
   
    <span data-ttu-id="6263e-192">d.</span><span class="sxs-lookup"><span data-stu-id="6263e-192">d.</span></span> <span data-ttu-id="6263e-193">To enable the SAML Settings click on Edit button</span><span class="sxs-lookup"><span data-stu-id="6263e-193">To enable the SAML Settings click on Edit button</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/tutorial_marketo_08.png) 
   
    <span data-ttu-id="6263e-195">e.</span><span class="sxs-lookup"><span data-stu-id="6263e-195">e.</span></span> <span data-ttu-id="6263e-196">**Enable** Single Sign-On settings</span><span class="sxs-lookup"><span data-stu-id="6263e-196">**Enable** Single Sign-On settings</span></span>
   
    <span data-ttu-id="6263e-197">f.</span><span class="sxs-lookup"><span data-stu-id="6263e-197">f.</span></span> <span data-ttu-id="6263e-198">Enter the Issuer ID, whihc you have copied from Azure AD configuration wizard.</span><span class="sxs-lookup"><span data-stu-id="6263e-198">Enter the Issuer ID, whihc you have copied from Azure AD configuration wizard.</span></span>
   
    <span data-ttu-id="6263e-199">g.</span><span class="sxs-lookup"><span data-stu-id="6263e-199">g.</span></span> <span data-ttu-id="6263e-200">In the Entity ID textbox enter the URL as **http://saml.marketo.com/sp**</span><span class="sxs-lookup"><span data-stu-id="6263e-200">In the Entity ID textbox enter the URL as **http://saml.marketo.com/sp**</span></span>
   
    <span data-ttu-id="6263e-201">h.</span><span class="sxs-lookup"><span data-stu-id="6263e-201">h.</span></span> <span data-ttu-id="6263e-202">Select the User ID Location as **Name Identifier element**</span><span class="sxs-lookup"><span data-stu-id="6263e-202">Select the User ID Location as **Name Identifier element**</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/tutorial_marketo_09.png)
   
    > [!NOTE]
    > <span data-ttu-id="6263e-204">If your User Identifier is not UPN value then change the value in the Attribute tab.</span><span class="sxs-lookup"><span data-stu-id="6263e-204">If your User Identifier is not UPN value then change the value in the Attribute tab.</span></span>
    > 
    > 
   
    <span data-ttu-id="6263e-205">i.</span><span class="sxs-lookup"><span data-stu-id="6263e-205">i.</span></span> <span data-ttu-id="6263e-206">Upload the certificate which you have downloaded from Azure AD configuration wizard.</span><span class="sxs-lookup"><span data-stu-id="6263e-206">Upload the certificate which you have downloaded from Azure AD configuration wizard.</span></span> <span data-ttu-id="6263e-207">Save the settings.</span><span class="sxs-lookup"><span data-stu-id="6263e-207">Save the settings.</span></span>
   
    <span data-ttu-id="6263e-208">j.</span><span class="sxs-lookup"><span data-stu-id="6263e-208">j.</span></span> <span data-ttu-id="6263e-209">Edit the Redirect Pages settings</span><span class="sxs-lookup"><span data-stu-id="6263e-209">Edit the Redirect Pages settings</span></span>
   
    <span data-ttu-id="6263e-210">k.</span><span class="sxs-lookup"><span data-stu-id="6263e-210">k.</span></span> <span data-ttu-id="6263e-211">Copy the Login URL from Azure AD configuration wizard in the **Login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="6263e-211">Copy the Login URL from Azure AD configuration wizard in the **Login URL** textbox.</span></span>
   
    <span data-ttu-id="6263e-212">l.</span><span class="sxs-lookup"><span data-stu-id="6263e-212">l.</span></span> <span data-ttu-id="6263e-213">Copy the Logout URL from Azure AD configuration wizard in the **Logout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="6263e-213">Copy the Logout URL from Azure AD configuration wizard in the **Logout URL** textbox.</span></span>
   
    <span data-ttu-id="6263e-214">m.</span><span class="sxs-lookup"><span data-stu-id="6263e-214">m.</span></span> <span data-ttu-id="6263e-215">In the Error URL copy your Marketo instance URL and click on Save button to save settings.</span><span class="sxs-lookup"><span data-stu-id="6263e-215">In the Error URL copy your Marketo instance URL and click on Save button to save settings.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/tutorial_marketo_10.png)

7. <span data-ttu-id="6263e-217">To enable the SSO for users, complete the following actions:</span><span class="sxs-lookup"><span data-stu-id="6263e-217">To enable the SSO for users, complete the following actions:</span></span>
   
    <span data-ttu-id="6263e-218">a.</span><span class="sxs-lookup"><span data-stu-id="6263e-218">a.</span></span> <span data-ttu-id="6263e-219">Login to Marketo app using admin credentials.</span><span class="sxs-lookup"><span data-stu-id="6263e-219">Login to Marketo app using admin credentials.</span></span>
   
    <span data-ttu-id="6263e-220">b.</span><span class="sxs-lookup"><span data-stu-id="6263e-220">b.</span></span> <span data-ttu-id="6263e-221">Click on the **Admin** button on the top navigation pane.</span><span class="sxs-lookup"><span data-stu-id="6263e-221">Click on the **Admin** button on the top navigation pane.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="6263e-223">c.</span><span class="sxs-lookup"><span data-stu-id="6263e-223">c.</span></span> <span data-ttu-id="6263e-224">Navigate to the **Security** menu and click on **Login Settings**</span><span class="sxs-lookup"><span data-stu-id="6263e-224">Navigate to the **Security** menu and click on **Login Settings**</span></span> 
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/tutorial_marketo_13.png)
   
    <span data-ttu-id="6263e-226">d.</span><span class="sxs-lookup"><span data-stu-id="6263e-226">d.</span></span> <span data-ttu-id="6263e-227">Check the **Require SSO** option and Save the settings.</span><span class="sxs-lookup"><span data-stu-id="6263e-227">Check the **Require SSO** option and Save the settings.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/tutorial_marketo_14.png)
8. <span data-ttu-id="6263e-229">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6263e-229">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
9. <span data-ttu-id="6263e-231">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="6263e-231">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6263e-233">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="6263e-233">Creating an Azure AD test user</span></span>
<span data-ttu-id="6263e-234">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6263e-234">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="6263e-236">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6263e-236">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6263e-237">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6263e-237">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="6263e-239">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="6263e-239">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="6263e-240">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="6263e-240">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="6263e-242">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="6263e-242">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="6263e-244">On the **Tell us about this user** dialog page, perform the following steps:  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/create_aaduser_05.png)</span><span class="sxs-lookup"><span data-stu-id="6263e-244">On the **Tell us about this user** dialog page, perform the following steps:  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/create_aaduser_05.png)</span></span> 
   
    <span data-ttu-id="6263e-245">a.</span><span class="sxs-lookup"><span data-stu-id="6263e-245">a.</span></span> <span data-ttu-id="6263e-246">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="6263e-246">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="6263e-247">b.</span><span class="sxs-lookup"><span data-stu-id="6263e-247">b.</span></span> <span data-ttu-id="6263e-248">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6263e-248">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="6263e-249">c.</span><span class="sxs-lookup"><span data-stu-id="6263e-249">c.</span></span> <span data-ttu-id="6263e-250">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6263e-250">Click **Next**.</span></span>
6. <span data-ttu-id="6263e-251">On the **User Profile** dialog page, perform the following steps:  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/create_aaduser_06.png)</span><span class="sxs-lookup"><span data-stu-id="6263e-251">On the **User Profile** dialog page, perform the following steps:  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/create_aaduser_06.png)</span></span> 
   
    <span data-ttu-id="6263e-252">a.</span><span class="sxs-lookup"><span data-stu-id="6263e-252">a.</span></span> <span data-ttu-id="6263e-253">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="6263e-253">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="6263e-254">b.</span><span class="sxs-lookup"><span data-stu-id="6263e-254">b.</span></span> <span data-ttu-id="6263e-255">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="6263e-255">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="6263e-256">c.</span><span class="sxs-lookup"><span data-stu-id="6263e-256">c.</span></span> <span data-ttu-id="6263e-257">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="6263e-257">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="6263e-258">d.</span><span class="sxs-lookup"><span data-stu-id="6263e-258">d.</span></span> <span data-ttu-id="6263e-259">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="6263e-259">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="6263e-260">e.</span><span class="sxs-lookup"><span data-stu-id="6263e-260">e.</span></span> <span data-ttu-id="6263e-261">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6263e-261">Click **Next**.</span></span>

7. <span data-ttu-id="6263e-262">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="6263e-262">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="6263e-264">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6263e-264">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="6263e-266">a.</span><span class="sxs-lookup"><span data-stu-id="6263e-266">a.</span></span> <span data-ttu-id="6263e-267">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="6263e-267">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="6263e-268">b.</span><span class="sxs-lookup"><span data-stu-id="6263e-268">b.</span></span> <span data-ttu-id="6263e-269">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="6263e-269">Click **Complete**.</span></span>   

### <a name="creating-an-marketo-test-user"></a><span data-ttu-id="6263e-270">Creating an Marketo test user</span><span class="sxs-lookup"><span data-stu-id="6263e-270">Creating an Marketo test user</span></span>
<span data-ttu-id="6263e-271">In this section, you create a user called Britta Simon in Marketo.</span><span class="sxs-lookup"><span data-stu-id="6263e-271">In this section, you create a user called Britta Simon in Marketo.</span></span> <span data-ttu-id="6263e-272">Please follow these steps to create a user in Marketo platform.</span><span class="sxs-lookup"><span data-stu-id="6263e-272">Please follow these steps to create a user in Marketo platform.</span></span>

1. <span data-ttu-id="6263e-273">Login to Marketo app using admin credentials.</span><span class="sxs-lookup"><span data-stu-id="6263e-273">Login to Marketo app using admin credentials.</span></span>
2. <span data-ttu-id="6263e-274">Click on the **Admin** button on the top navigation pane.</span><span class="sxs-lookup"><span data-stu-id="6263e-274">Click on the **Admin** button on the top navigation pane.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
3. <span data-ttu-id="6263e-276">Navigate to the **Security** menu and click on **Users & Roles**</span><span class="sxs-lookup"><span data-stu-id="6263e-276">Navigate to the **Security** menu and click on **Users & Roles**</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/tutorial_marketo_19.png)  
4. <span data-ttu-id="6263e-278">Click on the **Invite New User** link on the Users tab</span><span class="sxs-lookup"><span data-stu-id="6263e-278">Click on the **Invite New User** link on the Users tab</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/tutorial_marketo_15.png) 
5. <span data-ttu-id="6263e-280">In the Invite New User wizard fill the following information</span><span class="sxs-lookup"><span data-stu-id="6263e-280">In the Invite New User wizard fill the following information</span></span>
   
    <span data-ttu-id="6263e-281">a.</span><span class="sxs-lookup"><span data-stu-id="6263e-281">a.</span></span> <span data-ttu-id="6263e-282">Enter the user **Email** address in the textbox</span><span class="sxs-lookup"><span data-stu-id="6263e-282">Enter the user **Email** address in the textbox</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/tutorial_marketo_16.png)
   
    <span data-ttu-id="6263e-284">b.</span><span class="sxs-lookup"><span data-stu-id="6263e-284">b.</span></span> <span data-ttu-id="6263e-285">Enter the **First Name** in the textbox</span><span class="sxs-lookup"><span data-stu-id="6263e-285">Enter the **First Name** in the textbox</span></span>
   
    <span data-ttu-id="6263e-286">c.</span><span class="sxs-lookup"><span data-stu-id="6263e-286">c.</span></span> <span data-ttu-id="6263e-287">Enter the **Last Name**  in the textbox</span><span class="sxs-lookup"><span data-stu-id="6263e-287">Enter the **Last Name**  in the textbox</span></span>
   
    <span data-ttu-id="6263e-288">d.</span><span class="sxs-lookup"><span data-stu-id="6263e-288">d.</span></span> <span data-ttu-id="6263e-289">Click on Next</span><span class="sxs-lookup"><span data-stu-id="6263e-289">Click on Next</span></span>
6. <span data-ttu-id="6263e-290">In the **Permissions** tab select the user Roles and click Next</span><span class="sxs-lookup"><span data-stu-id="6263e-290">In the **Permissions** tab select the user Roles and click Next</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/tutorial_marketo_17.png)
7. <span data-ttu-id="6263e-292">Click on the Send button to send the user invitation</span><span class="sxs-lookup"><span data-stu-id="6263e-292">Click on the Send button to send the user invitation</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/tutorial_marketo_18.png)
8. <span data-ttu-id="6263e-294">User will receive the email notification and has to click on the link and change the password to activate the account.</span><span class="sxs-lookup"><span data-stu-id="6263e-294">User will receive the email notification and has to click on the link and change the password to activate the account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6263e-295">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="6263e-295">Assigning the Azure AD test user</span></span>
<span data-ttu-id="6263e-296">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Marketo.</span><span class="sxs-lookup"><span data-stu-id="6263e-296">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Marketo.</span></span>

![Assign User][200] 

<span data-ttu-id="6263e-298">**To assign Britta Simon to Marketo, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6263e-298">**To assign Britta Simon to Marketo, perform the following steps:**</span></span>

1. <span data-ttu-id="6263e-299">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="6263e-299">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="6263e-301">In the applications list, select **Marketo**.</span><span class="sxs-lookup"><span data-stu-id="6263e-301">In the applications list, select **Marketo**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/tutorial_marketo_50.png) 
3. <span data-ttu-id="6263e-303">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="6263e-303">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]
4. <span data-ttu-id="6263e-305">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="6263e-305">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="6263e-306">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="6263e-306">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="6263e-308">Testing Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="6263e-308">Testing Single Sign-On</span></span>
<span data-ttu-id="6263e-309">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="6263e-309">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6263e-310">When you click the Marketo tile in the Access Panel, you should get automatically signed-on to your Marketo application.</span><span class="sxs-lookup"><span data-stu-id="6263e-310">When you click the Marketo tile in the Access Panel, you should get automatically signed-on to your Marketo application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6263e-311">Additional resources</span><span class="sxs-lookup"><span data-stu-id="6263e-311">Additional resources</span></span>
* [<span data-ttu-id="6263e-312">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6263e-312">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6263e-313">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6263e-313">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-marketo-tutorial/tutorial_general_205.png










































