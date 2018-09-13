---
title: 'Tutorial: Azure Active Directory integration with BenSelect | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and BenSelect.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: ffa17478-3ea1-4356-a289-545b5b9a4494
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: jeedes
ms.openlocfilehash: 141cd3fe539fdedada7949d1202ee20a44754108
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554788"
---
# <a name="tutorial-azure-active-directory-integration-with-benselect"></a><span data-ttu-id="54930-103">Tutorial: Azure Active Directory integration with BenSelect</span><span class="sxs-lookup"><span data-stu-id="54930-103">Tutorial: Azure Active Directory integration with BenSelect</span></span>
<span data-ttu-id="54930-104">In this tutorial, you learn how to integrate BenSelect with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="54930-104">In this tutorial, you learn how to integrate BenSelect with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="54930-105">Integrating BenSelect with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="54930-105">Integrating BenSelect with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="54930-106">You can control in Azure AD who has access to BenSelect</span><span class="sxs-lookup"><span data-stu-id="54930-106">You can control in Azure AD who has access to BenSelect</span></span>
* <span data-ttu-id="54930-107">You can enable your users to automatically get signed-on to BenSelect single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="54930-107">You can enable your users to automatically get signed-on to BenSelect single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="54930-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="54930-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="54930-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="54930-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="54930-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="54930-110">Prerequisites</span></span>
<span data-ttu-id="54930-111">To configure Azure AD integration with BenSelect, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="54930-111">To configure Azure AD integration with BenSelect, you need the following items:</span></span>

* <span data-ttu-id="54930-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="54930-112">An Azure AD subscription</span></span>
* <span data-ttu-id="54930-113">A BenSelect single-sign on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="54930-113">A BenSelect single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="54930-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="54930-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
>  

<span data-ttu-id="54930-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="54930-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="54930-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="54930-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="54930-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="54930-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="54930-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="54930-118">Scenario Description</span></span>
<span data-ttu-id="54930-119">In this tutorial, you test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="54930-119">In this tutorial, you test Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="54930-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="54930-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="54930-121">Adding BenSelect from the gallery</span><span class="sxs-lookup"><span data-stu-id="54930-121">Adding BenSelect from the gallery</span></span>
* <span data-ttu-id="54930-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="54930-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-benselect-from-the-gallery"></a><span data-ttu-id="54930-123">Adding BenSelect from the gallery</span><span class="sxs-lookup"><span data-stu-id="54930-123">Adding BenSelect from the gallery</span></span>
<span data-ttu-id="54930-124">To configure the integration of BenSelect into Azure AD, you need to add BenSelect from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="54930-124">To configure the integration of BenSelect into Azure AD, you need to add BenSelect from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="54930-125">**To add BenSelect from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="54930-125">**To add BenSelect from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="54930-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="54930-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Active Directory][1]
2. <span data-ttu-id="54930-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="54930-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="54930-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="54930-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="54930-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="54930-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="54930-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="54930-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="54930-135">In the search box, type **BenSelect**.</span><span class="sxs-lookup"><span data-stu-id="54930-135">In the search box, type **BenSelect**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_benselect_01.png)
7. <span data-ttu-id="54930-137">In the results pane, select **BenSelect**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="54930-137">In the results pane, select **BenSelect**, and then click **Complete** to add the application.</span></span>
   
    ![Selecting the app in the gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_benselect_001.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="54930-139">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="54930-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="54930-140">In this section, you configure and test Azure AD single sign-on with BenSelect based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="54930-140">In this section, you configure and test Azure AD single sign-on with BenSelect based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="54930-141">For single sign-on to work, Azure AD needs to know what the counterpart user in BenSelect is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="54930-141">For single sign-on to work, Azure AD needs to know what the counterpart user in BenSelect is to a user in Azure AD.</span></span> <span data-ttu-id="54930-142">In other words, a link relationship between an Azure AD user and the related user in BenSelect needs to be established.</span><span class="sxs-lookup"><span data-stu-id="54930-142">In other words, a link relationship between an Azure AD user and the related user in BenSelect needs to be established.</span></span>

<span data-ttu-id="54930-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in BenSelect.</span><span class="sxs-lookup"><span data-stu-id="54930-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in BenSelect.</span></span>

<span data-ttu-id="54930-144">To configure and test Azure AD single sign-on with BenSelect, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="54930-144">To configure and test Azure AD single sign-on with BenSelect, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="54930-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="54930-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="54930-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="54930-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="54930-147">**[Creating a BenSelect test user](#creating-a-benselect-test-user)** - to have a counterpart of Britta Simon in BenSelect that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="54930-147">**[Creating a BenSelect test user](#creating-a-benselect-test-user)** - to have a counterpart of Britta Simon in BenSelect that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="54930-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="54930-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="54930-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="54930-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="54930-150">Configure Azure AD Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="54930-150">Configure Azure AD Single Sign-On</span></span>
<span data-ttu-id="54930-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure SSO in your BenSelect application.</span><span class="sxs-lookup"><span data-stu-id="54930-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure SSO in your BenSelect application.</span></span>

<span data-ttu-id="54930-152">BenSelect application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="54930-152">BenSelect application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="54930-153">Please configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="54930-153">Please configure the following claims for this application.</span></span> <span data-ttu-id="54930-154">You can manage the values of these attributes from the "**Atrribute**" tab of the application.</span><span class="sxs-lookup"><span data-stu-id="54930-154">You can manage the values of these attributes from the "**Atrribute**" tab of the application.</span></span> <span data-ttu-id="54930-155">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="54930-155">The following screenshot shows an example for this.</span></span> 

![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_benselect_06.png)

<span data-ttu-id="54930-157">**To configure Azure AD single sign-on with BenSelect, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="54930-157">**To configure Azure AD single sign-on with BenSelect, perform the following steps:**</span></span>

1. <span data-ttu-id="54930-158">In the Azure classic portal, on the **BenSelect** application integration page, in the menu on the top, click **Attributes**.</span><span class="sxs-lookup"><span data-stu-id="54930-158">In the Azure classic portal, on the **BenSelect** application integration page, in the menu on the top, click **Attributes**.</span></span>
   
     ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_benselect_07.png)
2. <span data-ttu-id="54930-160">On the **SAML token attributes** dialog, for each row shown in the table below, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="54930-160">On the **SAML token attributes** dialog, for each row shown in the table below, perform the following steps:</span></span>
   
   | <span data-ttu-id="54930-161">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="54930-161">Attribute Name</span></span> | <span data-ttu-id="54930-162">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="54930-162">Attribute Value</span></span> |
   | --- | --- |
   | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier |<span data-ttu-id="54930-163">extractmailprefix([userprincipalname])</span><span class="sxs-lookup"><span data-stu-id="54930-163">extractmailprefix([userprincipalname])</span></span> |
  1. <span data-ttu-id="54930-164">Click **add user attribute** to open the **Add User Attribure** dialog.</span><span class="sxs-lookup"><span data-stu-id="54930-164">Click **add user attribute** to open the **Add User Attribure** dialog.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_benselect_08.png)
  2. <span data-ttu-id="54930-166">In the **Attribute Name** textbox, type the attribute name shown for that row</span><span class="sxs-lookup"><span data-stu-id="54930-166">In the **Attribute Name** textbox, type the attribute name shown for that row</span></span> 
  3. <span data-ttu-id="54930-167">From the **Attribute Value** list, type ExtractMailPrefix().</span><span class="sxs-lookup"><span data-stu-id="54930-167">From the **Attribute Value** list, type ExtractMailPrefix().</span></span>
  4. <span data-ttu-id="54930-168">From the **Mail** list, type User.userprincipalname.</span><span class="sxs-lookup"><span data-stu-id="54930-168">From the **Mail** list, type User.userprincipalname.</span></span>
  5. <span data-ttu-id="54930-169">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="54930-169">Click **Complete**.</span></span>
3. <span data-ttu-id="54930-170">In the menu on the top, click **Quick Start**.</span><span class="sxs-lookup"><span data-stu-id="54930-170">In the menu on the top, click **Quick Start**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_benselect_09.png)
4. <span data-ttu-id="54930-172">On the **How would you like users to sign on to BenSelect** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="54930-172">On the **How would you like users to sign on to BenSelect** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_benselect_03.png) 
5. <span data-ttu-id="54930-174">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="54930-174">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_benselect_04.png) 
   1. <span data-ttu-id="54930-176">In the **Reply URL** textbox, type the URL using the following pattern: `https://www.benselect.com/enroll/login.aspx?Path={<tenant name>}`</span><span class="sxs-lookup"><span data-stu-id="54930-176">In the **Reply URL** textbox, type the URL using the following pattern: `https://www.benselect.com/enroll/login.aspx?Path={<tenant name>}`</span></span>
   2. <span data-ttu-id="54930-177">click **Next**.</span><span class="sxs-lookup"><span data-stu-id="54930-177">click **Next**.</span></span>
6. <span data-ttu-id="54930-178">On the **Configure single sign-on at BenSelect** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="54930-178">On the **Configure single sign-on at BenSelect** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_benselect_05.png)
  1. <span data-ttu-id="54930-180">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="54930-180">Click **Download certificate**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="54930-181">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="54930-181">Click **Next**.</span></span>
7. <span data-ttu-id="54930-182">To get SSO configured for your application, contact your BenSelect support team via [support@selerix.com](mailto:support@selerix.com) and provide them with the following:</span><span class="sxs-lookup"><span data-stu-id="54930-182">To get SSO configured for your application, contact your BenSelect support team via [support@selerix.com](mailto:support@selerix.com) and provide them with the following:</span></span>
   * <span data-ttu-id="54930-183">The downloaded certificate</span><span class="sxs-lookup"><span data-stu-id="54930-183">The downloaded certificate</span></span>
   * <span data-ttu-id="54930-184">The SAML SSO URL</span><span class="sxs-lookup"><span data-stu-id="54930-184">The SAML SSO URL</span></span>
   * <span data-ttu-id="54930-185">The Sign Out URL</span><span class="sxs-lookup"><span data-stu-id="54930-185">The Sign Out URL</span></span> 
   * <span data-ttu-id="54930-186">The Issuer</span><span class="sxs-lookup"><span data-stu-id="54930-186">The Issuer</span></span> 
     
   >[!NOTE]
   ><span data-ttu-id="54930-187">You need to mention that this integration requires the SHA256 algorithm (SHA1 is not supported) to set the SSO on the appropriate server like app2101 etc.</span><span class="sxs-lookup"><span data-stu-id="54930-187">You need to mention that this integration requires the SHA256 algorithm (SHA1 is not supported) to set the SSO on the appropriate server like app2101 etc.</span></span> 
   > 
8. <span data-ttu-id="54930-188">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="54930-188">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
9. <span data-ttu-id="54930-190">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="54930-190">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="54930-192">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="54930-192">Create an Azure AD test user</span></span>
<span data-ttu-id="54930-193">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="54930-193">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="54930-195">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="54930-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="54930-196">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="54930-196">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="54930-198">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="54930-198">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="54930-199">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="54930-199">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="54930-201">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="54930-201">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="54930-203">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="54930-203">On the **Tell us about this user** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/create_aaduser_05.png)    
  1. <span data-ttu-id="54930-205">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="54930-205">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="54930-206">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="54930-206">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="54930-207">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="54930-207">Click **Next**.</span></span>
6. <span data-ttu-id="54930-208">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="54930-208">On the **User Profile** dialog page, perform the following steps:</span></span>

   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/create_aaduser_06.png)   
  1. <span data-ttu-id="54930-210">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="54930-210">In the **First Name** textbox, type **Britta**.</span></span> 
  2. <span data-ttu-id="54930-211">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="54930-211">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="54930-212">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="54930-212">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="54930-213">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="54930-213">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="54930-214">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="54930-214">Click **Next**.</span></span>
7. <span data-ttu-id="54930-215">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="54930-215">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="54930-217">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="54930-217">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/create_aaduser_08.png) 
   1. <span data-ttu-id="54930-219">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="54930-219">Write down the value of the **New Password**.</span></span>
   2. <span data-ttu-id="54930-220">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="54930-220">Click **Complete**.</span></span>   

### <a name="create-an-benselect-test-user"></a><span data-ttu-id="54930-221">Create an BenSelect test user</span><span class="sxs-lookup"><span data-stu-id="54930-221">Create an BenSelect test user</span></span>
<span data-ttu-id="54930-222">The objective of this section is to create a user called Britta Simon in BenSelect.</span><span class="sxs-lookup"><span data-stu-id="54930-222">The objective of this section is to create a user called Britta Simon in BenSelect.</span></span> <span data-ttu-id="54930-223">Please work with BenSelect support team to add the users in the BenSelect account.</span><span class="sxs-lookup"><span data-stu-id="54930-223">Please work with BenSelect support team to add the users in the BenSelect account.</span></span>

>[!NOTE]
><span data-ttu-id="54930-224">If you need to create an user manually, you need to contact the BenSelect support team via <mailto:support@selerix.com>.</span><span class="sxs-lookup"><span data-stu-id="54930-224">If you need to create an user manually, you need to contact the BenSelect support team via <mailto:support@selerix.com>.</span></span>
>  

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="54930-225">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="54930-225">Assign the Azure AD test user</span></span>
<span data-ttu-id="54930-226">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to BenSelect.</span><span class="sxs-lookup"><span data-stu-id="54930-226">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to BenSelect.</span></span>

![Assign User][200] 

<span data-ttu-id="54930-228">**To assign Britta Simon to BenSelect, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="54930-228">**To assign Britta Simon to BenSelect, perform the following steps:**</span></span>

1. <span data-ttu-id="54930-229">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="54930-229">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="54930-231">In the applications list, select **BenSelect**.</span><span class="sxs-lookup"><span data-stu-id="54930-231">In the applications list, select **BenSelect**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_benselect_50.png) 
3. <span data-ttu-id="54930-233">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="54930-233">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]
4. <span data-ttu-id="54930-235">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="54930-235">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="54930-236">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="54930-236">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="54930-238">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="54930-238">Test single sign-on</span></span>
<span data-ttu-id="54930-239">In this section, you test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="54930-239">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="54930-240">When you click the BenSelect tile in the Access Panel, you should get automatically signed-on to your BenSelect application.</span><span class="sxs-lookup"><span data-stu-id="54930-240">When you click the BenSelect tile in the Access Panel, you should get automatically signed-on to your BenSelect application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="54930-241">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="54930-241">Additional Resources</span></span>
* [<span data-ttu-id="54930-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="54930-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="54930-243">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="54930-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_general_205.png





























