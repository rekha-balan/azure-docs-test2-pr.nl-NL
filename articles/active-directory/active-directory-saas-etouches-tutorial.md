---
title: 'Tutorial: Azure Active Directory integration with eTouches | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and eTouches.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 76cccaa8-859c-4c16-9d1d-8a6496fc7520
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: a3d16bcb626bd8942c203d0a77bc807104b2a93c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554495"
---
# <a name="tutorial-azure-active-directory-integration-with-etouches"></a><span data-ttu-id="c3927-103">Tutorial: Azure Active Directory integration with eTouches</span><span class="sxs-lookup"><span data-stu-id="c3927-103">Tutorial: Azure Active Directory integration with eTouches</span></span>
<span data-ttu-id="c3927-104">In this tutorial, you learn how to integrate eTouches with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c3927-104">In this tutorial, you learn how to integrate eTouches with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c3927-105">Integrating eTouches with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="c3927-105">Integrating eTouches with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="c3927-106">You can control in Azure AD who has access to eTouches</span><span class="sxs-lookup"><span data-stu-id="c3927-106">You can control in Azure AD who has access to eTouches</span></span>
* <span data-ttu-id="c3927-107">You can enable your users to automatically get signed-on to eTouches single sign-on (SSO)) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="c3927-107">You can enable your users to automatically get signed-on to eTouches single sign-on (SSO)) with their Azure AD accounts</span></span>
* <span data-ttu-id="c3927-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="c3927-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="c3927-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c3927-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c3927-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c3927-110">Prerequisites</span></span>
<span data-ttu-id="c3927-111">To configure Azure AD integration with eTouches, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="c3927-111">To configure Azure AD integration with eTouches, you need the following items:</span></span>

* <span data-ttu-id="c3927-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="c3927-112">An Azure AD subscription</span></span>
* <span data-ttu-id="c3927-113">A eTouches SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="c3927-113">A eTouches SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="c3927-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="c3927-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="c3927-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="c3927-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="c3927-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="c3927-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="c3927-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c3927-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c3927-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="c3927-118">Scenario description</span></span>
<span data-ttu-id="c3927-119">In this tutorial, you test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="c3927-119">In this tutorial, you test Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="c3927-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="c3927-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c3927-121">Adding eTouches from the gallery</span><span class="sxs-lookup"><span data-stu-id="c3927-121">Adding eTouches from the gallery</span></span>
2. <span data-ttu-id="c3927-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="c3927-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-etouches-from-the-gallery"></a><span data-ttu-id="c3927-123">Adding eTouches from the gallery</span><span class="sxs-lookup"><span data-stu-id="c3927-123">Adding eTouches from the gallery</span></span>
<span data-ttu-id="c3927-124">To configure the integration of eTouches into Azure AD, you need to add eTouches from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="c3927-124">To configure the integration of eTouches into Azure AD, you need to add eTouches from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c3927-125">**To add eTouches from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c3927-125">**To add eTouches from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c3927-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c3927-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Active Directory][1]
2. <span data-ttu-id="c3927-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="c3927-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="c3927-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="c3927-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="c3927-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="c3927-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="c3927-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="c3927-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="c3927-135">In the search box, type **eTouches**.</span><span class="sxs-lookup"><span data-stu-id="c3927-135">In the search box, type **eTouches**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-etouches-tutorial/tutorial_etouches_01.png)
7. <span data-ttu-id="c3927-137">In the results pane, select **eTouches**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="c3927-137">In the results pane, select **eTouches**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-etouches-tutorial/tutorial_etouches_02.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="c3927-139">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="c3927-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="c3927-140">In this section, you configure and test Azure AD SSO with eTouches based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c3927-140">In this section, you configure and test Azure AD SSO with eTouches based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c3927-141">For SSO to work, Azure AD needs to know what the counterpart user in eTouches is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c3927-141">For SSO to work, Azure AD needs to know what the counterpart user in eTouches is to a user in Azure AD.</span></span> <span data-ttu-id="c3927-142">In other words, a link relationship between an Azure AD user and the related user in eTouches needs to be established.</span><span class="sxs-lookup"><span data-stu-id="c3927-142">In other words, a link relationship between an Azure AD user and the related user in eTouches needs to be established.</span></span>

<span data-ttu-id="c3927-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in eTouches.</span><span class="sxs-lookup"><span data-stu-id="c3927-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in eTouches.</span></span>

<span data-ttu-id="c3927-144">To configure and test Azure AD SSO with eTouches, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="c3927-144">To configure and test Azure AD SSO with eTouches, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c3927-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="c3927-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c3927-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c3927-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c3927-147">**[Creating a eTouches test user](#creating-a-predictix-price-reporting-test-user)** - to have a counterpart of Britta Simon in eTouches that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="c3927-147">**[Creating a eTouches test user](#creating-a-predictix-price-reporting-test-user)** - to have a counterpart of Britta Simon in eTouches that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="c3927-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c3927-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c3927-149">**[Testing Single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="c3927-149">**[Testing Single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="c3927-150">Configure Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="c3927-150">Configure Azure AD SSO</span></span>
<span data-ttu-id="c3927-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your eTouches application.</span><span class="sxs-lookup"><span data-stu-id="c3927-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your eTouches application.</span></span>

<span data-ttu-id="c3927-152">eTouches application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="c3927-152">eTouches application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="c3927-153">Please configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="c3927-153">Please configure the following claims for this application.</span></span> <span data-ttu-id="c3927-154">You can manage the values of these attributes from the **"Atrribute"** tab of the application.</span><span class="sxs-lookup"><span data-stu-id="c3927-154">You can manage the values of these attributes from the **"Atrribute"** tab of the application.</span></span> <span data-ttu-id="c3927-155">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="c3927-155">The following screenshot shows an example for this.</span></span> 

![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-etouches-tutorial/tutorial_etouches_07.png) 

<span data-ttu-id="c3927-157">**To configure Azure AD SSO with eTocuhes, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c3927-157">**To configure Azure AD SSO with eTocuhes, perform the following steps:**</span></span>

1. <span data-ttu-id="c3927-158">In the Azure classic portal, on the **eTouches** application integration page, in the menu on the top, click **Attributes**.</span><span class="sxs-lookup"><span data-stu-id="c3927-158">In the Azure classic portal, on the **eTouches** application integration page, in the menu on the top, click **Attributes**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-etouches-tutorial/tutorial_general_80.png) 
2. <span data-ttu-id="c3927-160">On the **SAML token attributes** dialog, for each row shown in the table below, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c3927-160">On the **SAML token attributes** dialog, for each row shown in the table below, perform the following steps:</span></span>
   
   | <span data-ttu-id="c3927-161">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="c3927-161">Attribute Name</span></span> | <span data-ttu-id="c3927-162">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="c3927-162">Attribute Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="c3927-163">Email</span><span class="sxs-lookup"><span data-stu-id="c3927-163">Email</span></span> |<span data-ttu-id="c3927-164">user.mail</span><span class="sxs-lookup"><span data-stu-id="c3927-164">user.mail</span></span> |
   
 1. <span data-ttu-id="c3927-165">Click **add user attribute** to open the **Add User Attribure** dialog.</span><span class="sxs-lookup"><span data-stu-id="c3927-165">Click **add user attribute** to open the **Add User Attribure** dialog.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-etouches-tutorial/tutorial_general_81.png) 
  2. <span data-ttu-id="c3927-167">In the **Attrubute Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="c3927-167">In the **Attrubute Name** textbox, type the attribute name shown for that row.</span></span>
  3. <span data-ttu-id="c3927-168">From the **Attribute Value** list, selsect the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="c3927-168">From the **Attribute Value** list, selsect the attribute value shown for that row.</span></span>
  4. <span data-ttu-id="c3927-169">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="c3927-169">Click **Complete**.</span></span>    
3. <span data-ttu-id="c3927-170">In the classic portal, on the **eTouches** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="c3927-170">In the classic portal, on the **eTouches** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
4. <span data-ttu-id="c3927-172">On the **How would you like users to sign on to eTouches** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c3927-172">On the **How would you like users to sign on to eTouches** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-etouches-tutorial/tutorial_etouches_03.png) 
5. <span data-ttu-id="c3927-174">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c3927-174">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-etouches-tutorial/tutorial_etouches_04.png)   
  1. <span data-ttu-id="c3927-176">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your eTouches application using the following pattern: **https://www.eiseverywhere.com/saml/accounts/?sso&accountid=\<accountid\>**.</span><span class="sxs-lookup"><span data-stu-id="c3927-176">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your eTouches application using the following pattern: **https://www.eiseverywhere.com/saml/accounts/?sso&accountid=\<accountid\>**.</span></span>
  2. <span data-ttu-id="c3927-177">click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c3927-177">click **Next**.</span></span>
6. <span data-ttu-id="c3927-178">On the **Configure single sign-on at eTouches** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c3927-178">On the **Configure single sign-on at eTouches** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-etouches-tutorial/tutorial_etouches_05.png)  
  1. <span data-ttu-id="c3927-180">Click **Download metadata**, and then save the file on your computer.0</span><span class="sxs-lookup"><span data-stu-id="c3927-180">Click **Download metadata**, and then save the file on your computer.0</span></span>
  2. <span data-ttu-id="c3927-181">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c3927-181">Click **Next**.</span></span>
7. <span data-ttu-id="c3927-182">To get SSO configured for your application, perform the following steps in the eTouches application:</span><span class="sxs-lookup"><span data-stu-id="c3927-182">To get SSO configured for your application, perform the following steps in the eTouches application:</span></span>  
  1. <span data-ttu-id="c3927-183">Login to **eTouches** application using the Admin rights.</span><span class="sxs-lookup"><span data-stu-id="c3927-183">Login to **eTouches** application using the Admin rights.</span></span> 
  2. <span data-ttu-id="c3927-184">Go to the **SAML** Configuration.</span><span class="sxs-lookup"><span data-stu-id="c3927-184">Go to the **SAML** Configuration.</span></span>
  3. <span data-ttu-id="c3927-185">In the **General Settings** section paste the Azure AD Federation Metadata content into the textbox.</span><span class="sxs-lookup"><span data-stu-id="c3927-185">In the **General Settings** section paste the Azure AD Federation Metadata content into the textbox.</span></span>
  4. <span data-ttu-id="c3927-186">Click on the **Save & Stay** button.</span><span class="sxs-lookup"><span data-stu-id="c3927-186">Click on the **Save & Stay** button.</span></span>
  5. <span data-ttu-id="c3927-187">Click on the **Update Metadata** button in the SAML Metadata section.</span><span class="sxs-lookup"><span data-stu-id="c3927-187">Click on the **Update Metadata** button in the SAML Metadata section.</span></span> 
  6. <span data-ttu-id="c3927-188">This will open the page and will perform SSO.</span><span class="sxs-lookup"><span data-stu-id="c3927-188">This will open the page and will perform SSO.</span></span> <span data-ttu-id="c3927-189">Once the SSO is working then you can setup the username.</span><span class="sxs-lookup"><span data-stu-id="c3927-189">Once the SSO is working then you can setup the username.</span></span>
  7. <span data-ttu-id="c3927-190">In the **Username** field select the **emailaddress** as shown in the image below.</span><span class="sxs-lookup"><span data-stu-id="c3927-190">In the **Username** field select the **emailaddress** as shown in the image below.</span></span> 
  8. <span data-ttu-id="c3927-191">Copy the **SSO URL / ACS** value and put it into the Azure AD application configuration wizard Sign On URL textbox.</span><span class="sxs-lookup"><span data-stu-id="c3927-191">Copy the **SSO URL / ACS** value and put it into the Azure AD application configuration wizard Sign On URL textbox.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-etouches-tutorial/tutorial_etouches_06.png)
8. <span data-ttu-id="c3927-193">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c3927-193">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
9. <span data-ttu-id="c3927-195">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="c3927-195">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  

    ![Azure AD Single Sign-On][11]


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c3927-197">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="c3927-197">Create an Azure AD test user</span></span>
<span data-ttu-id="c3927-198">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c3927-198">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="c3927-200">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c3927-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c3927-201">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c3927-201">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-etouches-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="c3927-203">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="c3927-203">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="c3927-204">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="c3927-204">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-etouches-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="c3927-206">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="c3927-206">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-etouches-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="c3927-208">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c3927-208">On the **Tell us about this user** dialog page, perform the following steps:</span></span>

 ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-etouches-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="c3927-210">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="c3927-210">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="c3927-211">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c3927-211">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="c3927-212">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c3927-212">Click **Next**.</span></span>
6. <span data-ttu-id="c3927-213">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c3927-213">On the **User Profile** dialog page, perform the following steps:</span></span>

 ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-etouches-tutorial/create_aaduser_06.png)  
  1. <span data-ttu-id="c3927-215">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="c3927-215">In the **First Name** textbox, type **Britta**.</span></span>   
  2. <span data-ttu-id="c3927-216">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="c3927-216">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="c3927-217">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c3927-217">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="c3927-218">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="c3927-218">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="c3927-219">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c3927-219">Click **Next**.</span></span>
7. <span data-ttu-id="c3927-220">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="c3927-220">On the **Get temporary password** dialog page, click **create**.</span></span>
   
  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-etouches-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="c3927-222">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c3927-222">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-etouches-tutorial/create_aaduser_08.png)   
  1. <span data-ttu-id="c3927-224">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="c3927-224">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="c3927-225">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="c3927-225">Click **Complete**.</span></span>   

### <a name="create-an-etouches-test-user"></a><span data-ttu-id="c3927-226">Create an eTouches test user</span><span class="sxs-lookup"><span data-stu-id="c3927-226">Create an eTouches test user</span></span>
<span data-ttu-id="c3927-227">In this section, you create a user called Britta Simon in eTouches.</span><span class="sxs-lookup"><span data-stu-id="c3927-227">In this section, you create a user called Britta Simon in eTouches.</span></span> <span data-ttu-id="c3927-228">Please work with eTouches support team to add the users in the eTouches platform.</span><span class="sxs-lookup"><span data-stu-id="c3927-228">Please work with eTouches support team to add the users in the eTouches platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="c3927-229">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="c3927-229">Assign the Azure AD test user</span></span>
<span data-ttu-id="c3927-230">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to eTouches.</span><span class="sxs-lookup"><span data-stu-id="c3927-230">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to eTouches.</span></span>

![Assign User][200] 

<span data-ttu-id="c3927-232">**To assign Britta Simon to eTouches, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c3927-232">**To assign Britta Simon to eTouches, perform the following steps:**</span></span>

1. <span data-ttu-id="c3927-233">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="c3927-233">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="c3927-235">In the applications list, select **eTouches**.</span><span class="sxs-lookup"><span data-stu-id="c3927-235">In the applications list, select **eTouches**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-etouches-tutorial/tutorial_etouches_50.png) 
3. <span data-ttu-id="c3927-237">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="c3927-237">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]
4. <span data-ttu-id="c3927-239">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c3927-239">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="c3927-240">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="c3927-240">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="c3927-242">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="c3927-242">Test single sign-on</span></span>
<span data-ttu-id="c3927-243">In this section, you test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="c3927-243">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="c3927-244">When you click the eTouches tile in the Access Panel, you should get automatically signed-on to your eTouches application.</span><span class="sxs-lookup"><span data-stu-id="c3927-244">When you click the eTouches tile in the Access Panel, you should get automatically signed-on to your eTouches application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c3927-245">Additional resources</span><span class="sxs-lookup"><span data-stu-id="c3927-245">Additional resources</span></span>
* [<span data-ttu-id="c3927-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c3927-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c3927-247">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c3927-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-etouches-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-etouches-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-etouches-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-etouches-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-etouches-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-etouches-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-etouches-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-etouches-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-etouches-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-etouches-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-etouches-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-etouches-tutorial/tutorial_general_205.png





























