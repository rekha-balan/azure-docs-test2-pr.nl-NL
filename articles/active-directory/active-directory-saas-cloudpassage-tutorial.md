---
title: 'Tutorial: Azure Active Directory integration with CloudPassage | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and CloudPassage.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: bfe1f14e-74e4-4680-ac9e-f7355e1c94cc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: jeedes
ms.openlocfilehash: 7ccdf33191c95a8967fb96a67e3585a0cf112769
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564163"
---
# <a name="tutorial-azure-active-directory-integration-with-cloudpassage"></a><span data-ttu-id="99245-103">Tutorial: Azure Active Directory integration with CloudPassage</span><span class="sxs-lookup"><span data-stu-id="99245-103">Tutorial: Azure Active Directory integration with CloudPassage</span></span>
<span data-ttu-id="99245-104">The objective of this tutorial is to show you how to integrate CloudPassage with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="99245-104">The objective of this tutorial is to show you how to integrate CloudPassage with Azure Active Directory (Azure AD).</span></span>  

<span data-ttu-id="99245-105">Integrating CloudPassage with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="99245-105">Integrating CloudPassage with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="99245-106">You can control in Azure AD who has access to CloudPassage</span><span class="sxs-lookup"><span data-stu-id="99245-106">You can control in Azure AD who has access to CloudPassage</span></span> 
* <span data-ttu-id="99245-107">You can enable your users to automatically get signed-on to CloudPassage single sign-on (SS0) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="99245-107">You can enable your users to automatically get signed-on to CloudPassage single sign-on (SS0) with their Azure AD accounts</span></span>
* <span data-ttu-id="99245-108">You can manage your accounts in one central location - the Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="99245-108">You can manage your accounts in one central location - the Azure Active Directory</span></span> 

<span data-ttu-id="99245-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="99245-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="99245-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="99245-110">Prerequisites</span></span>
<span data-ttu-id="99245-111">To configure Azure AD integration with CloudPassage, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="99245-111">To configure Azure AD integration with CloudPassage, you need the following items:</span></span>

* <span data-ttu-id="99245-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="99245-112">An Azure AD subscription</span></span>
* <span data-ttu-id="99245-113">A CloudPassage SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="99245-113">A CloudPassage SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="99245-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="99245-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="99245-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="99245-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="99245-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="99245-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="99245-117">If you don't have an Azure AD test environment, you can get a free [one-month trial subscription](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="99245-117">If you don't have an Azure AD test environment, you can get a free [one-month trial subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="99245-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="99245-118">Scenario Description</span></span>
<span data-ttu-id="99245-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="99245-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>  

<span data-ttu-id="99245-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="99245-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="99245-121">Adding CloudPassage from the gallery</span><span class="sxs-lookup"><span data-stu-id="99245-121">Adding CloudPassage from the gallery</span></span> 
2. <span data-ttu-id="99245-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="99245-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-cloudpassage-from-the-gallery"></a><span data-ttu-id="99245-123">Add CloudPassage from the gallery</span><span class="sxs-lookup"><span data-stu-id="99245-123">Add CloudPassage from the gallery</span></span>
<span data-ttu-id="99245-124">To configure the integration of CloudPassage into Azure AD, you need to add CloudPassage from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="99245-124">To configure the integration of CloudPassage into Azure AD, you need to add CloudPassage from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="99245-125">**To add CloudPassage from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="99245-125">**To add CloudPassage from the gallery, perform the following steps:**</span></span>
1. <span data-ttu-id="99245-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="99245-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="99245-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="99245-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="99245-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="99245-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="99245-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="99245-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="99245-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="99245-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="99245-135">In the search box, type **CloudPassage**.</span><span class="sxs-lookup"><span data-stu-id="99245-135">In the search box, type **CloudPassage**.</span></span>
   
    ![Applications][5]
7. <span data-ttu-id="99245-137">In the results pane, select **CloudPassage**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="99245-137">In the results pane, select **CloudPassage**, and then click **Complete** to add the application.</span></span>
   
    ![Applications][6]

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="99245-139">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="99245-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="99245-140">The objective of this section is to show you how to configure and test Azure AD SSO with CloudPassage based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="99245-140">The objective of this section is to show you how to configure and test Azure AD SSO with CloudPassage based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="99245-141">For SSO to work, Azure AD needs to know what the counterpart user in CloudPassage to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="99245-141">For SSO to work, Azure AD needs to know what the counterpart user in CloudPassage to an user in Azure AD is.</span></span> <span data-ttu-id="99245-142">In other words, a link relationship between an Azure AD user and the related user in CloudPassage needs to be established.</span><span class="sxs-lookup"><span data-stu-id="99245-142">In other words, a link relationship between an Azure AD user and the related user in CloudPassage needs to be established.</span></span>  

<span data-ttu-id="99245-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="99245-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in CloudPassage.</span></span>

<span data-ttu-id="99245-144">To configure and test Azure AD SSO with CloudPassage, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="99245-144">To configure and test Azure AD SSO with CloudPassage, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="99245-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="99245-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="99245-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="99245-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="99245-147">**[Creating a CloudPassage test user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in CloudPassage that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="99245-147">**[Creating a CloudPassage test user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in CloudPassage that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="99245-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="99245-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="99245-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="99245-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="99245-150">Configure Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="99245-150">Configure Azure AD SSO</span></span>
<span data-ttu-id="99245-151">The objective of this section is to enable Azure AD SSO in the Azure AD classic portal and to configure SSO in your CloudPassage application.</span><span class="sxs-lookup"><span data-stu-id="99245-151">The objective of this section is to enable Azure AD SSO in the Azure AD classic portal and to configure SSO in your CloudPassage application.</span></span>  

<span data-ttu-id="99245-152">Your CloudPassage application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span><span class="sxs-lookup"><span data-stu-id="99245-152">Your CloudPassage application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> 

<span data-ttu-id="99245-153">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="99245-153">The following screenshot shows an example for this.</span></span>

![Configure Single Sign-On][21]

<span data-ttu-id="99245-155">**To configure Azure AD single sign-on with CloudPassage, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="99245-155">**To configure Azure AD single sign-on with CloudPassage, perform the following steps:**</span></span>

1. <span data-ttu-id="99245-156">In the Azure AD classic portal, on the **CloudPassage** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="99245-156">In the Azure AD classic portal, on the **CloudPassage** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][7]
2. <span data-ttu-id="99245-158">On the **How would you like users to sign on to CloudPassage** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="99245-158">On the **How would you like users to sign on to CloudPassage** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On][8]
3. <span data-ttu-id="99245-160">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="99245-160">On the **Configure App Settings** dialog page, perform the following steps:</span></span> 
   
    ![Configure App Settings][9]   
  1. <span data-ttu-id="99245-162">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your CloudPassage app (e.g.: *https://portal.cloudpassage.com/saml/init/accountid*).</span><span class="sxs-lookup"><span data-stu-id="99245-162">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your CloudPassage app (e.g.: *https://portal.cloudpassage.com/saml/init/accountid*).</span></span>  
  2. <span data-ttu-id="99245-163">In the **Reply URL** textbox, type your AssertionConsumerService URL (e.g.: *https://portal.cloudpassage.com/saml/consume/accountid*).</span><span class="sxs-lookup"><span data-stu-id="99245-163">In the **Reply URL** textbox, type your AssertionConsumerService URL (e.g.: *https://portal.cloudpassage.com/saml/consume/accountid*).</span></span> <span data-ttu-id="99245-164">You can get your value for this attribute by clicking **SSO Setup documentation** in the **Single Sign-on Settings** section of your CloudPassage portal.</span><span class="sxs-lookup"><span data-stu-id="99245-164">You can get your value for this attribute by clicking **SSO Setup documentation** in the **Single Sign-on Settings** section of your CloudPassage portal.</span></span>
  
    ![Configure Single Sign-On][10]   
  3. <span data-ttu-id="99245-166">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="99245-166">Click **Next**.</span></span>
4. <span data-ttu-id="99245-167">On the **Configure single sign-on at CloudPassage** page, click **Download certificate**, and then save the certificate file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="99245-167">On the **Configure single sign-on at CloudPassage** page, click **Download certificate**, and then save the certificate file locally on your computer.</span></span> 
   
    ![Configure Single Sign-On][11]
5. <span data-ttu-id="99245-169">In a different browser window, sign-on to your CloudPassage company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="99245-169">In a different browser window, sign-on to your CloudPassage company site as administrator.</span></span>
6. <span data-ttu-id="99245-170">In the menu on the top, click **Settings**, and then click **Site Administration**.</span><span class="sxs-lookup"><span data-stu-id="99245-170">In the menu on the top, click **Settings**, and then click **Site Administration**.</span></span> 
   
    ![Configure Single Sign-On][12]
7. <span data-ttu-id="99245-172">Click the **Authentication Settings** tab.</span><span class="sxs-lookup"><span data-stu-id="99245-172">Click the **Authentication Settings** tab.</span></span> 
   
    ![Configure Single Sign-On][13]
8. <span data-ttu-id="99245-174">In the **Single Sign-on Settings** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="99245-174">In the **Single Sign-on Settings** section, perform the following steps:</span></span> 
   
    ![Configure Single Sign-On][14]
  1. <span data-ttu-id="99245-176">In the Azure classic portal, on the **Configure single sign-on at CloudPassage** dialog page, copy the **Issuer URL** value, and then paste it into the **SAML issuer URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="99245-176">In the Azure classic portal, on the **Configure single sign-on at CloudPassage** dialog page, copy the **Issuer URL** value, and then paste it into the **SAML issuer URL** textbox.</span></span>
  2. <span data-ttu-id="99245-177">In the Azure classic portal, on the **Configure single sign-on at CloudPassage** dialog page, copy the **Service Provider (SP) initiated endpoint** value, and then paste it into the **SAML endpoint URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="99245-177">In the Azure classic portal, on the **Configure single sign-on at CloudPassage** dialog page, copy the **Service Provider (SP) initiated endpoint** value, and then paste it into the **SAML endpoint URL** textbox.</span></span>
  3. <span data-ttu-id="99245-178">In the Azure classic portal, on the **Configure single sign-on at CloudPassage** dialog page, copy the **Logout URL** value, and then paste it into the **Logout landing page** textbox.</span><span class="sxs-lookup"><span data-stu-id="99245-178">In the Azure classic portal, on the **Configure single sign-on at CloudPassage** dialog page, copy the **Logout URL** value, and then paste it into the **Logout landing page** textbox.</span></span>
  4. <span data-ttu-id="99245-179">Create a **base-64** encoded file from your downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="99245-179">Create a **base-64** encoded file from your downloaded certificate.</span></span> 

    >[AZURE.TIP] <span data-ttu-id="99245-180">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="99245-180">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>
  5. <span data-ttu-id="99245-181">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it into the **x 509 certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="99245-181">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it into the **x 509 certificate** textbox.</span></span>
  6. <span data-ttu-id="99245-182">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="99245-182">Click **Save**.</span></span>


1. <span data-ttu-id="99245-183">On the Azure AD classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="99245-183">On the Azure AD classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![Configure Single Sign-On][15]
2. <span data-ttu-id="99245-185">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="99245-185">On the **Single sign-on confirmation** page, click **Complete**.</span></span> 
   
   ![Configure Single Sign-On][16]
3. <span data-ttu-id="99245-187">In the nu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span><span class="sxs-lookup"><span data-stu-id="99245-187">In the nu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span></span> 
   
   ![Configure Single Sign-On][17]
4. <span data-ttu-id="99245-189">To add the required user attributes, for each row in the table below, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="99245-189">To add the required user attributes, for each row in the table below, perform the following steps:</span></span> 
   
   | <span data-ttu-id="99245-190">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="99245-190">Attribute Name</span></span> | <span data-ttu-id="99245-191">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="99245-191">Attribute Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="99245-192">firstname</span><span class="sxs-lookup"><span data-stu-id="99245-192">firstname</span></span> |<span data-ttu-id="99245-193">user.givenname</span><span class="sxs-lookup"><span data-stu-id="99245-193">user.givenname</span></span> |
   | <span data-ttu-id="99245-194">lastname</span><span class="sxs-lookup"><span data-stu-id="99245-194">lastname</span></span> |<span data-ttu-id="99245-195">user.surname</span><span class="sxs-lookup"><span data-stu-id="99245-195">user.surname</span></span> |
   | <span data-ttu-id="99245-196">email</span><span class="sxs-lookup"><span data-stu-id="99245-196">email</span></span> |<span data-ttu-id="99245-197">user.mail</span><span class="sxs-lookup"><span data-stu-id="99245-197">user.mail</span></span> |
  1. <span data-ttu-id="99245-198">Click **add user attribute**.</span><span class="sxs-lookup"><span data-stu-id="99245-198">Click **add user attribute**.</span></span> 

    ![Configure Single Sign-On][18]
  2. <span data-ttu-id="99245-200">In the **Attribute Name** textbox, type the attribute name shown for that row and as **Attribure Value**, select the attribute value shown for that row .</span><span class="sxs-lookup"><span data-stu-id="99245-200">In the **Attribute Name** textbox, type the attribute name shown for that row and as **Attribure Value**, select the attribute value shown for that row .</span></span> 

    ![Configure Single Sign-On][19]
  3. <span data-ttu-id="99245-202">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="99245-202">Click **Complete**.</span></span>
1. <span data-ttu-id="99245-203">In the toolbar on the bottom, click **Apply Changes**.</span><span class="sxs-lookup"><span data-stu-id="99245-203">In the toolbar on the bottom, click **Apply Changes**.</span></span> 
   
   ![Configure Single Sign-On][20]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="99245-205">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="99245-205">Create an Azure AD test user</span></span>
<span data-ttu-id="99245-206">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="99245-206">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cloudpassage-tutorial/create_aaduser_01.png)

<span data-ttu-id="99245-208">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="99245-208">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="99245-209">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="99245-209">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cloudpassage-tutorial/create_aaduser_02.png) 
2. <span data-ttu-id="99245-211">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="99245-211">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="99245-212">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="99245-212">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cloudpassage-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="99245-214">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="99245-214">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cloudpassage-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="99245-216">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="99245-216">On the **Tell us about this user** dialog page, perform the following steps:</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cloudpassage-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="99245-218">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="99245-218">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="99245-219">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="99245-219">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="99245-220">Click Next.</span><span class="sxs-lookup"><span data-stu-id="99245-220">Click Next.</span></span>
6. <span data-ttu-id="99245-221">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="99245-221">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cloudpassage-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="99245-223">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="99245-223">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="99245-224">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="99245-224">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="99245-225">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="99245-225">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="99245-226">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="99245-226">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="99245-227">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="99245-227">Click **Next**.</span></span>
7. <span data-ttu-id="99245-228">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="99245-228">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cloudpassage-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="99245-230">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="99245-230">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cloudpassage-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="99245-232">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="99245-232">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="99245-233">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="99245-233">Click **Complete**.</span></span>   

### <a name="create-a-cloudpassage-test-user"></a><span data-ttu-id="99245-234">Create a CloudPassage test user</span><span class="sxs-lookup"><span data-stu-id="99245-234">Create a CloudPassage test user</span></span>
<span data-ttu-id="99245-235">The objective of this section is to create a user called Britta Simon in CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="99245-235">The objective of this section is to create a user called Britta Simon in CloudPassage.</span></span>

<span data-ttu-id="99245-236">**To create a user called Britta Simon in CloudPassage, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="99245-236">**To create a user called Britta Simon in CloudPassage, perform the following steps:**</span></span>
1. <span data-ttu-id="99245-237">Sign-on to your **CloudPassage** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="99245-237">Sign-on to your **CloudPassage** company site as an administrator.</span></span> 
2. <span data-ttu-id="99245-238">In the toolbar on the top, click **Settings**, and then click **Site Administration**.</span><span class="sxs-lookup"><span data-stu-id="99245-238">In the toolbar on the top, click **Settings**, and then click **Site Administration**.</span></span> 
   
   ![Creating a CloudPassage test user][22] 
3. <span data-ttu-id="99245-240">Click the **Users** tab, and then click **Add New User**.</span><span class="sxs-lookup"><span data-stu-id="99245-240">Click the **Users** tab, and then click **Add New User**.</span></span> 
   
   ![Creating a CloudPassage test user][23]
4. <span data-ttu-id="99245-242">In the **Add New User** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="99245-242">In the **Add New User** section, perform the following steps:</span></span> 
   
   ![Creating a CloudPassage test user][24]
  1. <span data-ttu-id="99245-244">In the **First Name** textbox, type Britta.</span><span class="sxs-lookup"><span data-stu-id="99245-244">In the **First Name** textbox, type Britta.</span></span> 
  2. <span data-ttu-id="99245-245">In the **Last Name** textbox, type Simon.</span><span class="sxs-lookup"><span data-stu-id="99245-245">In the **Last Name** textbox, type Simon.</span></span>
  3. <span data-ttu-id="99245-246">In the **Username** textbox, the **Email** textbox and the **Retype Email** textbox, type Britta's user name in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="99245-246">In the **Username** textbox, the **Email** textbox and the **Retype Email** textbox, type Britta's user name in Azure AD.</span></span>
  4. <span data-ttu-id="99245-247">As **Access Type**, select **Enable Halo Portal Access**.</span><span class="sxs-lookup"><span data-stu-id="99245-247">As **Access Type**, select **Enable Halo Portal Access**.</span></span>
  5. <span data-ttu-id="99245-248">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="99245-248">Click **Add**.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="99245-249">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="99245-249">Assign the Azure AD test user</span></span>
<span data-ttu-id="99245-250">The objective of this section is to enable Britta Simon to use Azure SSO by granting her access to CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="99245-250">The objective of this section is to enable Britta Simon to use Azure SSO by granting her access to CloudPassage.</span></span>

![Assign User][30]

<span data-ttu-id="99245-252">**To assign Britta Simon to CloudPassage, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="99245-252">**To assign Britta Simon to CloudPassage, perform the following steps:**</span></span>

1. <span data-ttu-id="99245-253">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="99245-253">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][26]
2. <span data-ttu-id="99245-255">In the applications list, select **CloudPassage**.</span><span class="sxs-lookup"><span data-stu-id="99245-255">In the applications list, select **CloudPassage**.</span></span>
   
    ![Assign User][27]
3. <span data-ttu-id="99245-257">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="99245-257">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][25]
4. <span data-ttu-id="99245-259">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="99245-259">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="99245-260">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="99245-260">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][29]

### <a name="test-single-sign-on"></a><span data-ttu-id="99245-262">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="99245-262">Test single sign-on</span></span>
<span data-ttu-id="99245-263">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="99245-263">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="99245-264">When you click the CloudPassage tile in the Access Panel, you should get automatically signed-on to your CloudPassage application.</span><span class="sxs-lookup"><span data-stu-id="99245-264">When you click the CloudPassage tile in the Access Panel, you should get automatically signed-on to your CloudPassage application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="99245-265">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="99245-265">Additional Resources</span></span>
* [<span data-ttu-id="99245-266">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="99245-266">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="99245-267">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="99245-267">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cloudpassage-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cloudpassage-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cloudpassage-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cloudpassage-tutorial/tutorial_general_04.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_01.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_02.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cloudpassage-tutorial/tutorial_general_05.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_03.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_04.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_05.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_06.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_07.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_08.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_09.png
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_10.png
[16]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_11.png
[17]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cloudpassage-tutorial/tutorial_general_10.png
[18]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cloudpassage-tutorial/tutorial_general_11.png
[19]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cloudpassage-tutorial/tutorial_general_12.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cloudpassage-tutorial/tutorial_general_14.png
[21]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_14.png
[22]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_15.png
[23]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_16.png
[24]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_17.png
[25]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cloudpassage-tutorial/tutorial_general_15.png
[26]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_12.png
[27]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_13.png
[28]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_15.png
[29]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cloudpassage-tutorial/tutorial_general_16.png
[30]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cloudpassage-tutorial/tutorial_general_17.png



























































