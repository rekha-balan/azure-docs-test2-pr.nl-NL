---
title: 'Tutorial: Azure Active Directory integration with OpsGenie | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and OpsGenie.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 41b59b22-a61d-4fe6-ab0d-6c3991d1375f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: jeedes
ms.openlocfilehash: bf3f0c0d5efd193cbfa6e95247fe37289a1a78a1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550455"
---
# <a name="tutorial-azure-active-directory-integration-with-opsgenie"></a><span data-ttu-id="c67ef-103">Tutorial: Azure Active Directory integration with OpsGenie</span><span class="sxs-lookup"><span data-stu-id="c67ef-103">Tutorial: Azure Active Directory integration with OpsGenie</span></span>
<span data-ttu-id="c67ef-104">The objective of this tutorial is to show you how to integrate OpsGenie with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c67ef-104">The objective of this tutorial is to show you how to integrate OpsGenie with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c67ef-105">Integrating OpsGenie with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="c67ef-105">Integrating OpsGenie with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="c67ef-106">You can control in Azure AD who has access to OpsGenie</span><span class="sxs-lookup"><span data-stu-id="c67ef-106">You can control in Azure AD who has access to OpsGenie</span></span>
* <span data-ttu-id="c67ef-107">You can enable your users to automatically get signed-on to OpsGenie single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="c67ef-107">You can enable your users to automatically get signed-on to OpsGenie single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="c67ef-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="c67ef-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="c67ef-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c67ef-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c67ef-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c67ef-110">Prerequisites</span></span>
<span data-ttu-id="c67ef-111">To configure Azure AD integration with OpsGenie, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="c67ef-111">To configure Azure AD integration with OpsGenie, you need the following items:</span></span>

* <span data-ttu-id="c67ef-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="c67ef-112">An Azure AD subscription</span></span>
* <span data-ttu-id="c67ef-113">An OpsGenie single sign-on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="c67ef-113">An OpsGenie single sign-on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="c67ef-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="c67ef-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
>  

<span data-ttu-id="c67ef-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="c67ef-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="c67ef-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="c67ef-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="c67ef-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c67ef-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c67ef-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="c67ef-118">Scenario description</span></span>
<span data-ttu-id="c67ef-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="c67ef-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="c67ef-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="c67ef-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="c67ef-121">Adding OpsGenie from the gallery</span><span class="sxs-lookup"><span data-stu-id="c67ef-121">Adding OpsGenie from the gallery</span></span>
* <span data-ttu-id="c67ef-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="c67ef-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-opsgenie-from-the-gallery"></a><span data-ttu-id="c67ef-123">Add OpsGenie from the gallery</span><span class="sxs-lookup"><span data-stu-id="c67ef-123">Add OpsGenie from the gallery</span></span>
<span data-ttu-id="c67ef-124">To configure the integration of OpsGenie into Azure AD, you need to add OpsGenie from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="c67ef-124">To configure the integration of OpsGenie into Azure AD, you need to add OpsGenie from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c67ef-125">**To add OpsGenie from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c67ef-125">**To add OpsGenie from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c67ef-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c67ef-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="c67ef-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="c67ef-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="c67ef-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="c67ef-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="c67ef-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="c67ef-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="c67ef-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="c67ef-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="c67ef-135">In the search box, type **OpsGenie**.</span><span class="sxs-lookup"><span data-stu-id="c67ef-135">In the search box, type **OpsGenie**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_01.png)
7. <span data-ttu-id="c67ef-137">In the results pane, select **OpsGenie**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="c67ef-137">In the results pane, select **OpsGenie**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_02.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="c67ef-139">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="c67ef-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="c67ef-140">The objective of this section is to show you how to configure and test Azure AD SSO with OpsGenie based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c67ef-140">The objective of this section is to show you how to configure and test Azure AD SSO with OpsGenie based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c67ef-141">For SSO to work, Azure AD needs to know the counterpart user in OpsGenie to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c67ef-141">For SSO to work, Azure AD needs to know the counterpart user in OpsGenie to a user in Azure AD.</span></span> <span data-ttu-id="c67ef-142">In other words, a link relationship between an Azure AD user and the related user in OpsGenie needs to be established.</span><span class="sxs-lookup"><span data-stu-id="c67ef-142">In other words, a link relationship between an Azure AD user and the related user in OpsGenie needs to be established.</span></span>

<span data-ttu-id="c67ef-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in OpsGenie.</span><span class="sxs-lookup"><span data-stu-id="c67ef-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in OpsGenie.</span></span>

<span data-ttu-id="c67ef-144">To configure and test Azure AD SSO with OpsGenie, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="c67ef-144">To configure and test Azure AD SSO with OpsGenie, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c67ef-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="c67ef-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c67ef-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c67ef-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c67ef-147">**[Creating a OpsGenie test user](#creating-a-opsgenie-test-user)** - to have a counterpart of Britta Simon in OpsGenie that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="c67ef-147">**[Creating a OpsGenie test user](#creating-a-opsgenie-test-user)** - to have a counterpart of Britta Simon in OpsGenie that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="c67ef-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c67ef-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c67ef-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="c67ef-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c67ef-150">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c67ef-150">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="c67ef-151">The objective of this section is to enable Azure AD SSO in the Azure Classic portal and to configure SSO in your OpsGenie application.</span><span class="sxs-lookup"><span data-stu-id="c67ef-151">The objective of this section is to enable Azure AD SSO in the Azure Classic portal and to configure SSO in your OpsGenie application.</span></span>

<span data-ttu-id="c67ef-152">**To configure Azure AD single sign-on with OpsGenie, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c67ef-152">**To configure Azure AD single sign-on with OpsGenie, perform the following steps:**</span></span>

1. <span data-ttu-id="c67ef-153">In the Azure classic portal, on the **OpsGenie** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="c67ef-153">In the Azure classic portal, on the **OpsGenie** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="c67ef-155">On the **How would you like users to sign on to OpsGenie** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c67ef-155">On the **How would you like users to sign on to OpsGenie** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_03.png) 
3. <span data-ttu-id="c67ef-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c67ef-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_04.png)
  1. <span data-ttu-id="c67ef-159">In the Sign On URL textbox, type the URL used by your users to sign-on to your OpsGenie application using the following pattern: **“https://app.opsgenie.com/auth/login”**.</span><span class="sxs-lookup"><span data-stu-id="c67ef-159">In the Sign On URL textbox, type the URL used by your users to sign-on to your OpsGenie application using the following pattern: **“https://app.opsgenie.com/auth/login”**.</span></span>

    >[!NOTE] 
    ><span data-ttu-id="c67ef-160">Please contact your [OpsGenie support team](mailto:support@opsgenie.com) if you need your Sign On URL.</span><span class="sxs-lookup"><span data-stu-id="c67ef-160">Please contact your [OpsGenie support team](mailto:support@opsgenie.com) if you need your Sign On URL.</span></span>
    >

  2. <span data-ttu-id="c67ef-161">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c67ef-161">Click **Next**.</span></span>

4. <span data-ttu-id="c67ef-162">On the **Configure single sign-on at OpsGenie** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c67ef-162">On the **Configure single sign-on at OpsGenie** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_05.png)   
  1. <span data-ttu-id="c67ef-164">Click **Download Certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="c67ef-164">Click **Download Certificate**, and then save the file on your computer.</span></span> <span data-ttu-id="c67ef-165">We will need this certificate and Metadata URLs (Entity ID, SSO Sign In URL and Sign Out URL) to set up SSO on OpsGenie side.</span><span class="sxs-lookup"><span data-stu-id="c67ef-165">We will need this certificate and Metadata URLs (Entity ID, SSO Sign In URL and Sign Out URL) to set up SSO on OpsGenie side.</span></span>
  2. <span data-ttu-id="c67ef-166">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c67ef-166">Click **Next**.</span></span>
5. <span data-ttu-id="c67ef-167">Open another browser instance, and then log-in to OpsGenie as an administrator.</span><span class="sxs-lookup"><span data-stu-id="c67ef-167">Open another browser instance, and then log-in to OpsGenie as an administrator.</span></span>
6. <span data-ttu-id="c67ef-168">Click **Settings**, and then click the **Single Sign On** tab.</span><span class="sxs-lookup"><span data-stu-id="c67ef-168">Click **Settings**, and then click the **Single Sign On** tab.</span></span>
   
    ![OpsGenie Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_06.png) 
7. <span data-ttu-id="c67ef-170">To enable SSO, select **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="c67ef-170">To enable SSO, select **Enabled**.</span></span>
   
    ![OpsGenie Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_07.png) 
8. <span data-ttu-id="c67ef-172">In the **Provider** section, click the **Azure Active Directory** tab.</span><span class="sxs-lookup"><span data-stu-id="c67ef-172">In the **Provider** section, click the **Azure Active Directory** tab.</span></span>
   
    ![OpsGenie Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_08.png) 
9. <span data-ttu-id="c67ef-174">On the Azure Active Directory dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c67ef-174">On the Azure Active Directory dialog page, perform the following steps:</span></span>
   
    ![OpsGenie Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_09.png)  
  1. <span data-ttu-id="c67ef-176">In the Azure classic portal, on the **Configure single sign-on at OpsGenie** dialog page, copy the **Single Sign On Service URL** value, and then paste it into the **SAML 2.0 Endpoint** textbox.</span><span class="sxs-lookup"><span data-stu-id="c67ef-176">In the Azure classic portal, on the **Configure single sign-on at OpsGenie** dialog page, copy the **Single Sign On Service URL** value, and then paste it into the **SAML 2.0 Endpoint** textbox.</span></span>
  2. <span data-ttu-id="c67ef-177">Create a base-64 encoded file from your downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="c67ef-177">Create a base-64 encoded file from your downloaded certificate.</span></span>      
   
    >[!NOTE]
    ><span data-ttu-id="c67ef-178">For more details, see [How to convert a binary certificate into a text file](https://www.youtube.com/watch?v=PlgrzUZ-Y1o&feature=youtu.be).</span><span class="sxs-lookup"><span data-stu-id="c67ef-178">For more details, see [How to convert a binary certificate into a text file](https://www.youtube.com/watch?v=PlgrzUZ-Y1o&feature=youtu.be).</span></span>
    >

  3. <span data-ttu-id="c67ef-179">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it into the **X.500 Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="c67ef-179">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it into the **X.500 Certificate** textbox.</span></span>
  4. <span data-ttu-id="c67ef-180">Click **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="c67ef-180">Click **Save Changes**.</span></span>
10. <span data-ttu-id="c67ef-181">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c67ef-181">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
11. <span data-ttu-id="c67ef-183">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="c67ef-183">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c67ef-185">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="c67ef-185">Create an Azure AD test user</span></span>
<span data-ttu-id="c67ef-186">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c67ef-186">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="c67ef-188">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c67ef-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c67ef-189">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c67ef-189">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-opsgenie-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="c67ef-191">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="c67ef-191">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="c67ef-192">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="c67ef-192">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-opsgenie-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="c67ef-194">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="c67ef-194">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-opsgenie-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="c67ef-196">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c67ef-196">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-opsgenie-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="c67ef-198">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="c67ef-198">As Type Of User, select New user in your organization.</span></span>  
  2. <span data-ttu-id="c67ef-199">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c67ef-199">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="c67ef-200">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c67ef-200">Click **Next**.</span></span>
6. <span data-ttu-id="c67ef-201">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c67ef-201">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-opsgenie-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="c67ef-203">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="c67ef-203">In the **First Name** textbox, type **Britta**.</span></span>    
  2. <span data-ttu-id="c67ef-204">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="c67ef-204">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="c67ef-205">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c67ef-205">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="c67ef-206">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="c67ef-206">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="c67ef-207">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c67ef-207">Click **Next**.</span></span>
7. <span data-ttu-id="c67ef-208">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="c67ef-208">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-opsgenie-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="c67ef-210">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c67ef-210">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-opsgenie-tutorial/create_aaduser_08.png) 
   1. <span data-ttu-id="c67ef-212">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="c67ef-212">Write down the value of the **New Password**.</span></span>
   2. <span data-ttu-id="c67ef-213">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="c67ef-213">Click **Complete**.</span></span>   

### <a name="create-a-opsgenie-test-user"></a><span data-ttu-id="c67ef-214">Create a OpsGenie test user</span><span class="sxs-lookup"><span data-stu-id="c67ef-214">Create a OpsGenie test user</span></span>
<span data-ttu-id="c67ef-215">The objective of this section is to create a user called Britta Simon in OpsGenie.</span><span class="sxs-lookup"><span data-stu-id="c67ef-215">The objective of this section is to create a user called Britta Simon in OpsGenie.</span></span> 

1. <span data-ttu-id="c67ef-216">In a web browser window, log into your OpsGenie tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="c67ef-216">In a web browser window, log into your OpsGenie tenant as an administrator.</span></span>
2. <span data-ttu-id="c67ef-217">Navigate to Users list by clicking **User** in left panel.</span><span class="sxs-lookup"><span data-stu-id="c67ef-217">Navigate to Users list by clicking **User** in left panel.</span></span>
   
   ![OpsGenie Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_10.png) 
3. <span data-ttu-id="c67ef-219">Click "**Add User**".</span><span class="sxs-lookup"><span data-stu-id="c67ef-219">Click "**Add User**".</span></span>
4. <span data-ttu-id="c67ef-220">On the **Add User** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c67ef-220">On the **Add User** dialog, perform the following steps:</span></span>
   
   ![OpsGenie Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_11.png) 
  1. <span data-ttu-id="c67ef-222">In the **Email** textbox, type Britta's email address in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c67ef-222">In the **Email** textbox, type Britta's email address in Azure Active Directory.</span></span>
  2. <span data-ttu-id="c67ef-223">In the **Full Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c67ef-223">In the **Full Name** textbox, type **Britta Simon**.</span></span>
  3. <span data-ttu-id="c67ef-224">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="c67ef-224">Click **Save**.</span></span> 

>[!NOTE]
><span data-ttu-id="c67ef-225">Britta will get an email with instructions for setting up her profile.</span><span class="sxs-lookup"><span data-stu-id="c67ef-225">Britta will get an email with instructions for setting up her profile.</span></span>
>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="c67ef-226">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="c67ef-226">Assign the Azure AD test user</span></span>
<span data-ttu-id="c67ef-227">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to OpsGenie.</span><span class="sxs-lookup"><span data-stu-id="c67ef-227">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to OpsGenie.</span></span>

![Assign User][200] 

<span data-ttu-id="c67ef-229">**To assign Britta Simon to OpsGenie, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c67ef-229">**To assign Britta Simon to OpsGenie, perform the following steps:**</span></span>

1. <span data-ttu-id="c67ef-230">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="c67ef-230">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="c67ef-232">In the applications list, select **OpsGenie**.</span><span class="sxs-lookup"><span data-stu-id="c67ef-232">In the applications list, select **OpsGenie**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_50.png) 
3. <span data-ttu-id="c67ef-234">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="c67ef-234">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="c67ef-236">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c67ef-236">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="c67ef-237">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="c67ef-237">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="c67ef-239">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="c67ef-239">Test single sign-on</span></span>
<span data-ttu-id="c67ef-240">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="c67ef-240">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="c67ef-241">When you click the OpsGenie tile in the Access Panel, you should get automatically signed-on to your OpsGenie application.</span><span class="sxs-lookup"><span data-stu-id="c67ef-241">When you click the OpsGenie tile in the Access Panel, you should get automatically signed-on to your OpsGenie application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c67ef-242">Additional resources</span><span class="sxs-lookup"><span data-stu-id="c67ef-242">Additional resources</span></span>
* [<span data-ttu-id="c67ef-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c67ef-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c67ef-244">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c67ef-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-opsgenie-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-opsgenie-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-opsgenie-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-opsgenie-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-opsgenie-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-opsgenie-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-opsgenie-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-opsgenie-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-opsgenie-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-opsgenie-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-opsgenie-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-opsgenie-tutorial/tutorial_general_205.png































