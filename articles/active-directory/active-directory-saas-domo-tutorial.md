---
title: 'Tutorial: Azure Active Directory integration with Domo | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Domo.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 058626e4-73b3-4dc2-86ca-b060d002d70a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: 9b4ab4ec528d185e1df47a72be16f5333c2a3c4d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540789"
---
# <a name="tutorial-azure-active-directory-integration-with-domo"></a><span data-ttu-id="5e9bf-103">Tutorial: Azure Active Directory integration with Domo</span><span class="sxs-lookup"><span data-stu-id="5e9bf-103">Tutorial: Azure Active Directory integration with Domo</span></span>
<span data-ttu-id="5e9bf-104">The objective of this tutorial is to show you how to integrate Domo with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5e9bf-104">The objective of this tutorial is to show you how to integrate Domo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5e9bf-105">Integrating Domo with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="5e9bf-105">Integrating Domo with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="5e9bf-106">You can control in Azure AD who has access to Domo</span><span class="sxs-lookup"><span data-stu-id="5e9bf-106">You can control in Azure AD who has access to Domo</span></span>
* <span data-ttu-id="5e9bf-107">You can enable your users to automatically get signed-on to Domo single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="5e9bf-107">You can enable your users to automatically get signed-on to Domo single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="5e9bf-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="5e9bf-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="5e9bf-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5e9bf-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5e9bf-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5e9bf-110">Prerequisites</span></span>
<span data-ttu-id="5e9bf-111">To configure Azure AD integration with Domo, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="5e9bf-111">To configure Azure AD integration with Domo, you need the following items:</span></span>

* <span data-ttu-id="5e9bf-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="5e9bf-112">An Azure AD subscription</span></span>
* <span data-ttu-id="5e9bf-113">A Domo single-sign on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="5e9bf-113">A Domo single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="5e9bf-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="5e9bf-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="5e9bf-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="5e9bf-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="5e9bf-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5e9bf-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5e9bf-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="5e9bf-118">Scenario Description</span></span>
<span data-ttu-id="5e9bf-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="5e9bf-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="5e9bf-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="5e9bf-121">Adding Domo from the gallery</span><span class="sxs-lookup"><span data-stu-id="5e9bf-121">Adding Domo from the gallery</span></span>
* <span data-ttu-id="5e9bf-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="5e9bf-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-domo-from-the-gallery"></a><span data-ttu-id="5e9bf-123">Adding Domo from the gallery</span><span class="sxs-lookup"><span data-stu-id="5e9bf-123">Adding Domo from the gallery</span></span>
<span data-ttu-id="5e9bf-124">To configure the integration of Domo into Azure AD, you need to add Domo from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-124">To configure the integration of Domo into Azure AD, you need to add Domo from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5e9bf-125">**To add Domo from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5e9bf-125">**To add Domo from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5e9bf-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="5e9bf-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="5e9bf-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="5e9bf-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="5e9bf-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="5e9bf-135">In the search box, type **Domo**.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-135">In the search box, type **Domo**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-domo-tutorial/tutorial_domo_01.png)
7. <span data-ttu-id="5e9bf-137">In the results pane, select **Domo**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-137">In the results pane, select **Domo**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-domo-tutorial/tutorial_domo_02.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5e9bf-139">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="5e9bf-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="5e9bf-140">The objective of this section is to show you how to configure and test Azure AD SSO with Domo based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5e9bf-140">The objective of this section is to show you how to configure and test Azure AD SSO with Domo based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5e9bf-141">For SSO to work, Azure AD needs to know what the counterpart user in Domo to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-141">For SSO to work, Azure AD needs to know what the counterpart user in Domo to an user in Azure AD is.</span></span> <span data-ttu-id="5e9bf-142">In other words, a link relationship between an Azure AD user and the related user in Domo needs to be established.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-142">In other words, a link relationship between an Azure AD user and the related user in Domo needs to be established.</span></span>

<span data-ttu-id="5e9bf-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Domo.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Domo.</span></span>

<span data-ttu-id="5e9bf-144">To configure and test Azure AD SSO with Domo, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="5e9bf-144">To configure and test Azure AD SSO with Domo, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5e9bf-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5e9bf-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5e9bf-147">**[Creating a Domo test user](#creating-a-domo-test-user)** - to have a counterpart of Britta Simon in Domo that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-147">**[Creating a Domo test user](#creating-a-domo-test-user)** - to have a counterpart of Britta Simon in Domo that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="5e9bf-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5e9bf-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5e9bf-150">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="5e9bf-150">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="5e9bf-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure single sign-on in your Domo application.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure single sign-on in your Domo application.</span></span>

<span data-ttu-id="5e9bf-152">Domo application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-152">Domo application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="5e9bf-153">Please configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-153">Please configure the following claims for this application.</span></span> <span data-ttu-id="5e9bf-154">You can manage the values of these attributes from the **"Atrribute"** tab of the application.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-154">You can manage the values of these attributes from the **"Atrribute"** tab of the application.</span></span> <span data-ttu-id="5e9bf-155">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-155">The following screenshot shows an example for this.</span></span> 

![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-domo-tutorial/tutorial_domo_06.png) 

<span data-ttu-id="5e9bf-157">**To configure Azure AD single sign-on with Domo, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5e9bf-157">**To configure Azure AD single sign-on with Domo, perform the following steps:**</span></span>

1. <span data-ttu-id="5e9bf-158">In the Azure classic portal, on the **Domo** application integration page, in the menu on the top, click **Attributes**.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-158">In the Azure classic portal, on the **Domo** application integration page, in the menu on the top, click **Attributes**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-domo-tutorial/tutorial_general_80.png) 
2. <span data-ttu-id="5e9bf-160">On the **SAML token attributes** dialog, for each row shown in the table below, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5e9bf-160">On the **SAML token attributes** dialog, for each row shown in the table below, perform the following steps:</span></span>
   
   | <span data-ttu-id="5e9bf-161">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="5e9bf-161">Attribute Name</span></span> | <span data-ttu-id="5e9bf-162">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="5e9bf-162">Attribute Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="5e9bf-163">name</span><span class="sxs-lookup"><span data-stu-id="5e9bf-163">name</span></span> |<span data-ttu-id="5e9bf-164">user.displayname</span><span class="sxs-lookup"><span data-stu-id="5e9bf-164">user.displayname</span></span> |
   | <span data-ttu-id="5e9bf-165">email</span><span class="sxs-lookup"><span data-stu-id="5e9bf-165">email</span></span> |<span data-ttu-id="5e9bf-166">user.mail</span><span class="sxs-lookup"><span data-stu-id="5e9bf-166">user.mail</span></span> |
  1. <span data-ttu-id="5e9bf-167">Click **add user attribute** to open the **Add User Attribure** dialog.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-167">Click **add user attribute** to open the **Add User Attribure** dialog.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-domo-tutorial/tutorial_general_81.png) 
  2. <span data-ttu-id="5e9bf-169">In the **Attrubute Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-169">In the **Attrubute Name** textbox, type the attribute name shown for that row.</span></span>
  3. <span data-ttu-id="5e9bf-170">From the **Attribute Value** list, selsect the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-170">From the **Attribute Value** list, selsect the attribute value shown for that row.</span></span>
  4. <span data-ttu-id="5e9bf-171">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-171">Click **Complete**.</span></span>    
3. <span data-ttu-id="5e9bf-172">In the Azure classic portal, on the **Domo** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-172">In the Azure classic portal, on the **Domo** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
4. <span data-ttu-id="5e9bf-174">On the **How would you like users to sign on to Domo** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-174">On the **How would you like users to sign on to Domo** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-domo-tutorial/tutorial_domo_03.png) 
5. <span data-ttu-id="5e9bf-176">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5e9bf-176">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-domo-tutorial/tutorial_domo_04.png) 
  1. <span data-ttu-id="5e9bf-178">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Domo application using the following pattern: `https://<company name>.domo.com`</span><span class="sxs-lookup"><span data-stu-id="5e9bf-178">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Domo application using the following pattern: `https://<company name>.domo.com`</span></span>
  2. <span data-ttu-id="5e9bf-179">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-179">Click **Next**.</span></span>
1. <span data-ttu-id="5e9bf-180">On the **Configure single sign-on at Domo** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5e9bf-180">On the **Configure single sign-on at Domo** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-domo-tutorial/tutorial_domo_05.png)
  1. <span data-ttu-id="5e9bf-182">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-182">Click **Download certificate**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="5e9bf-183">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-183">Click **Next**.</span></span>
2. <span data-ttu-id="5e9bf-184">To get SSO configured for your application, contact your Domo support team at [support@domo.com](mailto: support@domo.com), attach the downloaded certificate and provide them with the **Issuer URL**, the **SAML SSO URL** and the **Sign Out URL**.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-184">To get SSO configured for your application, contact your Domo support team at [support@domo.com](mailto: support@domo.com), attach the downloaded certificate and provide them with the **Issuer URL**, the **SAML SSO URL** and the **Sign Out URL**.</span></span>
3. <span data-ttu-id="5e9bf-185">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-185">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
4. <span data-ttu-id="5e9bf-187">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-187">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5e9bf-189">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="5e9bf-189">Create an Azure AD test user</span></span>
<span data-ttu-id="5e9bf-190">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-190">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

![Create Azure AD User][20]

<span data-ttu-id="5e9bf-192">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5e9bf-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5e9bf-193">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-193">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-domo-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="5e9bf-195">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-195">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="5e9bf-196">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-196">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-domo-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="5e9bf-198">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-198">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-domo-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="5e9bf-200">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5e9bf-200">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-domo-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="5e9bf-202">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-202">As Type Of User, select New user in your organization.</span></span> 
  2. <span data-ttu-id="5e9bf-203">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-203">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="5e9bf-204">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-204">Click **Next**.</span></span>
6. <span data-ttu-id="5e9bf-205">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5e9bf-205">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-domo-tutorial/create_aaduser_06.png) 
  2. <span data-ttu-id="5e9bf-207">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-207">In the **First Name** textbox, type **Britta**.</span></span>  
  3. <span data-ttu-id="5e9bf-208">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-208">In the **Last Name** textbox, type, **Simon**.</span></span>
  4. <span data-ttu-id="5e9bf-209">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-209">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  5. <span data-ttu-id="5e9bf-210">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-210">In the **Role** list, select **User**.</span></span>
  6. <span data-ttu-id="5e9bf-211">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-211">Click **Next**.</span></span>
7. <span data-ttu-id="5e9bf-212">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-212">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-domo-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="5e9bf-214">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5e9bf-214">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-domo-tutorial/create_aaduser_08.png)
  1. <span data-ttu-id="5e9bf-216">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-216">Write down the value of the **New Password**.</span></span> 
  2. <span data-ttu-id="5e9bf-217">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-217">Click **Complete**.</span></span>   

### <a name="create-a-domo-test-user"></a><span data-ttu-id="5e9bf-218">Create a Domo test user</span><span class="sxs-lookup"><span data-stu-id="5e9bf-218">Create a Domo test user</span></span>
<span data-ttu-id="5e9bf-219">The objective of this section is to create a user called Britta Simon in Domo.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-219">The objective of this section is to create a user called Britta Simon in Domo.</span></span> <span data-ttu-id="5e9bf-220">Domo supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-220">Domo supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="5e9bf-221">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-221">There is no action item for you in this section.</span></span> <span data-ttu-id="5e9bf-222">A new user will be created during an attempt to access Domo if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-222">A new user will be created during an attempt to access Domo if it doesn't exist yet.</span></span> <span data-ttu-id="5e9bf-223">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="5e9bf-223">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="5e9bf-224">If you need to create an user manually, you need to contact the Domo support team.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-224">If you need to create an user manually, you need to contact the Domo support team.</span></span> 
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="5e9bf-225">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="5e9bf-225">Assign the Azure AD test user</span></span>
<span data-ttu-id="5e9bf-226">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Domo.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-226">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Domo.</span></span>

![Assign User][200] 

<span data-ttu-id="5e9bf-228">**To assign Britta Simon to Domo, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5e9bf-228">**To assign Britta Simon to Domo, perform the following steps:**</span></span>

1. <span data-ttu-id="5e9bf-229">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-229">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="5e9bf-231">In the applications list, select **Domo**.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-231">In the applications list, select **Domo**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-domo-tutorial/tutorial_domo_50.png) 
3. <span data-ttu-id="5e9bf-233">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-233">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="5e9bf-235">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-235">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="5e9bf-236">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-236">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="5e9bf-238">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="5e9bf-238">Test single sign-on</span></span>
<span data-ttu-id="5e9bf-239">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-239">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="5e9bf-240">When you click the Domo tile in the Access Panel, you should get automatically signed-on to your Domo application.</span><span class="sxs-lookup"><span data-stu-id="5e9bf-240">When you click the Domo tile in the Access Panel, you should get automatically signed-on to your Domo application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5e9bf-241">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="5e9bf-241">Additional Resources</span></span>
* [<span data-ttu-id="5e9bf-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5e9bf-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5e9bf-243">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5e9bf-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-domo-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-domo-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-domo-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-domo-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-domo-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-domo-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-domo-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-domo-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-domo-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-domo-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-domo-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-domo-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-domo-tutorial/tutorial_general_205.png




























