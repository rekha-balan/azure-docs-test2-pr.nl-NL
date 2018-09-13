---
title: 'Tutorial: Azure Active Directory integration with Nomadic | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Nomadic.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 13d02b1c-d98a-40b1-824f-afa45a2deb6a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: jeedes
ms.openlocfilehash: e71d2b8da066d17621f8c5721366cea3095d28c3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553883"
---
# <a name="tutorial-azure-active-directory-integration-with-nomadic"></a><span data-ttu-id="2f925-103">Tutorial: Azure Active Directory integration with Nomadic</span><span class="sxs-lookup"><span data-stu-id="2f925-103">Tutorial: Azure Active Directory integration with Nomadic</span></span>

<span data-ttu-id="2f925-104">In this tutorial, you learn how to integrate Nomadic with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2f925-104">In this tutorial, you learn how to integrate Nomadic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2f925-105">Integrating Nomadic with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="2f925-105">Integrating Nomadic with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2f925-106">You can control in Azure AD who has access to Nomadic</span><span class="sxs-lookup"><span data-stu-id="2f925-106">You can control in Azure AD who has access to Nomadic</span></span>
- <span data-ttu-id="2f925-107">You can enable your users to automatically get signed-on to Nomadic single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="2f925-107">You can enable your users to automatically get signed-on to Nomadic single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="2f925-108">You can manage your accounts in one central location - the Azure Management portal</span><span class="sxs-lookup"><span data-stu-id="2f925-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="2f925-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2f925-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f925-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2f925-110">Prerequisites</span></span>

<span data-ttu-id="2f925-111">To configure Azure AD integration with Nomadic, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="2f925-111">To configure Azure AD integration with Nomadic, you need the following items:</span></span>

- <span data-ttu-id="2f925-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="2f925-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2f925-113">A Nomadic SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="2f925-113">A Nomadic SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="2f925-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="2f925-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
>
>

<span data-ttu-id="2f925-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="2f925-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2f925-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="2f925-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="2f925-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2f925-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2f925-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="2f925-118">Scenario description</span></span>
<span data-ttu-id="2f925-119">In this tutorial, you test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="2f925-119">In this tutorial, you test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="2f925-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="2f925-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>
 
1. <span data-ttu-id="2f925-121">Adding Nomadic from the gallery</span><span class="sxs-lookup"><span data-stu-id="2f925-121">Adding Nomadic from the gallery</span></span>
2. <span data-ttu-id="2f925-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="2f925-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-nomadic-from-the-gallery"></a><span data-ttu-id="2f925-123">Add Nomadic from the gallery</span><span class="sxs-lookup"><span data-stu-id="2f925-123">Add Nomadic from the gallery</span></span>
<span data-ttu-id="2f925-124">To configure the integration of Nomadic into Azure AD, you need to add Nomadic from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="2f925-124">To configure the integration of Nomadic into Azure AD, you need to add Nomadic from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2f925-125">**To add Nomadic from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2f925-125">**To add Nomadic from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2f925-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="2f925-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]
 
2. <span data-ttu-id="2f925-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="2f925-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2f925-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="2f925-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="2f925-131">Click **Add** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="2f925-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="2f925-133">In the search box, type **Nomadic**.</span><span class="sxs-lookup"><span data-stu-id="2f925-133">In the search box, type **Nomadic**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_001.png)

5. <span data-ttu-id="2f925-135">In the results panel, select **Nomadic**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="2f925-135">In the results panel, select **Nomadic**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_0001.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="2f925-137">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="2f925-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="2f925-138">In this section, you configure and test Azure AD SSO with Nomadic based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2f925-138">In this section, you configure and test Azure AD SSO with Nomadic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2f925-139">For SSO to work, Azure AD needs to know what the counterpart user in Nomadic is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f925-139">For SSO to work, Azure AD needs to know what the counterpart user in Nomadic is to a user in Azure AD.</span></span> <span data-ttu-id="2f925-140">In other words, a link relationship between an Azure AD user and the related user in Nomadic needs to be established.</span><span class="sxs-lookup"><span data-stu-id="2f925-140">In other words, a link relationship between an Azure AD user and the related user in Nomadic needs to be established.</span></span>

<span data-ttu-id="2f925-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Nomadic.</span><span class="sxs-lookup"><span data-stu-id="2f925-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Nomadic.</span></span>

<span data-ttu-id="2f925-142">To configure and test Azure AD SSO with Nomadic, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="2f925-142">To configure and test Azure AD SSO with Nomadic, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2f925-143">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="2f925-143">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2f925-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2f925-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2f925-145">**[Creating a Nomadic test user](#creating-a-nomadic-test-user)** - to have a counterpart of Britta Simon in Nomadic that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="2f925-145">**[Creating a Nomadic test user](#creating-a-nomadic-test-user)** - to have a counterpart of Britta Simon in Nomadic that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="2f925-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="2f925-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2f925-147">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="2f925-147">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2f925-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="2f925-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2f925-149">In this section, you enable Azure AD SSO in the Azure Management portal and configure single sign-on in your Nomadic application.</span><span class="sxs-lookup"><span data-stu-id="2f925-149">In this section, you enable Azure AD SSO in the Azure Management portal and configure single sign-on in your Nomadic application.</span></span>

<span data-ttu-id="2f925-150">**To configure Azure AD SSO with Nomadic, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2f925-150">**To configure Azure AD SSO with Nomadic, perform the following steps:**</span></span>

1. <span data-ttu-id="2f925-151">In the Azure Management portal, on the **Nomadic** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="2f925-151">In the Azure Management portal, on the **Nomadic** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="2f925-153">On the **Single sign-on** dialog page, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span><span class="sxs-lookup"><span data-stu-id="2f925-153">On the **Single sign-on** dialog page, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_01.png)

3. <span data-ttu-id="2f925-155">On the **Nomadic Domain and URLs** section perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2f925-155">On the **Nomadic Domain and URLs** section perform the following steps:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_02.png)
  1. <span data-ttu-id="2f925-157">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.nomadic.fm/signin`</span><span class="sxs-lookup"><span data-stu-id="2f925-157">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.nomadic.fm/signin`</span></span>
  2. <span data-ttu-id="2f925-158">In the **Identifer** textbox, type a URL using the following pattern: `https://<company name>.nomadic.fm/auth/saml2/sp`</span><span class="sxs-lookup"><span data-stu-id="2f925-158">In the **Identifer** textbox, type a URL using the following pattern: `https://<company name>.nomadic.fm/auth/saml2/sp`</span></span>

     >[!NOTE] 
     ><span data-ttu-id="2f925-159">These are not the real values.</span><span class="sxs-lookup"><span data-stu-id="2f925-159">These are not the real values.</span></span> <span data-ttu-id="2f925-160">You have to update these values with the actual Sign On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="2f925-160">You have to update these values with the actual Sign On URL and Identifier.</span></span> <span data-ttu-id="2f925-161">Contact [Nomadic support team](mailto:help@nomadic.fm) to get these values.</span><span class="sxs-lookup"><span data-stu-id="2f925-161">Contact [Nomadic support team](mailto:help@nomadic.fm) to get these values.</span></span>
     >
     >

4. <span data-ttu-id="2f925-162">On the **SAML Signing Certificate** section, click **Create new certificate**.</span><span class="sxs-lookup"><span data-stu-id="2f925-162">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_03.png)    

5. <span data-ttu-id="2f925-164">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span><span class="sxs-lookup"><span data-stu-id="2f925-164">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="2f925-165">Then click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="2f925-165">Then click **Save** button.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadic-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="2f925-167">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="2f925-167">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_04.png)

7. <span data-ttu-id="2f925-169">On the pop-up **Rollover certificate** window, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="2f925-169">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadic-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="2f925-171">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="2f925-171">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_05.png) 

9. <span data-ttu-id="2f925-173">To get SSO configured for your application, contact [Nomadic support team](mailto:help@nomadic.fm) and provide them with the downloaded **metadata**.</span><span class="sxs-lookup"><span data-stu-id="2f925-173">To get SSO configured for your application, contact [Nomadic support team](mailto:help@nomadic.fm) and provide them with the downloaded **metadata**.</span></span>
  
### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="2f925-174">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="2f925-174">Create an Azure AD test user</span></span>
<span data-ttu-id="2f925-175">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2f925-175">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="2f925-177">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2f925-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2f925-178">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="2f925-178">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadic-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2f925-180">Go to **Users and groups** and click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="2f925-180">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadic-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2f925-182">At the top of the dialog click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="2f925-182">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadic-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2f925-184">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2f925-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadic-tutorial/create_aaduser_04.png) 
  1. <span data-ttu-id="2f925-186">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2f925-186">In the **Name** textbox, type **BrittaSimon**.</span></span>
  2. <span data-ttu-id="2f925-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2f925-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>
  3. <span data-ttu-id="2f925-188">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="2f925-188">Select **Show Password** and write down the value of the **Password**.</span></span>
  4. <span data-ttu-id="2f925-189">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="2f925-189">Click **Create**.</span></span> 

### <a name="create-a-nomadic-test-user"></a><span data-ttu-id="2f925-190">Create a Nomadic test user</span><span class="sxs-lookup"><span data-stu-id="2f925-190">Create a Nomadic test user</span></span>

<span data-ttu-id="2f925-191">In this section, you create a user called Britta Simon in Nomadic.</span><span class="sxs-lookup"><span data-stu-id="2f925-191">In this section, you create a user called Britta Simon in Nomadic.</span></span> <span data-ttu-id="2f925-192">Please work with [Nomadic support team](mailto:help@nomadic.fm) to add the users in the Nomadic platform.</span><span class="sxs-lookup"><span data-stu-id="2f925-192">Please work with [Nomadic support team](mailto:help@nomadic.fm) to add the users in the Nomadic platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="2f925-193">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="2f925-193">Assign the Azure AD test user</span></span>

<span data-ttu-id="2f925-194">In this section, you enable Britta Simon to use Azure SSO by granting her access to Nomadic.</span><span class="sxs-lookup"><span data-stu-id="2f925-194">In this section, you enable Britta Simon to use Azure SSO by granting her access to Nomadic.</span></span>

![Assign User][200] 

<span data-ttu-id="2f925-196">**To assign Britta Simon to Nomadic, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2f925-196">**To assign Britta Simon to Nomadic, perform the following steps:**</span></span>

1. <span data-ttu-id="2f925-197">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="2f925-197">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="2f925-199">In the applications list, select **Nomadic**.</span><span class="sxs-lookup"><span data-stu-id="2f925-199">In the applications list, select **Nomadic**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_50.png) 

3. <span data-ttu-id="2f925-201">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="2f925-201">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="2f925-203">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="2f925-203">Click **Add** button.</span></span> <span data-ttu-id="2f925-204">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="2f925-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="2f925-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="2f925-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2f925-207">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="2f925-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2f925-208">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="2f925-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    

### <a name="test-single-sign-on"></a><span data-ttu-id="2f925-209">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="2f925-209">Test single sign-on</span></span>

<span data-ttu-id="2f925-210">In this section, you test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="2f925-210">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="2f925-211">When you click the Nomadic tile in the Access Panel, you should get automatically signed-on to your Nomadic application.</span><span class="sxs-lookup"><span data-stu-id="2f925-211">When you click the Nomadic tile in the Access Panel, you should get automatically signed-on to your Nomadic application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2f925-212">Additional resources</span><span class="sxs-lookup"><span data-stu-id="2f925-212">Additional resources</span></span>

* [<span data-ttu-id="2f925-213">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2f925-213">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2f925-214">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2f925-214">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadic-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadic-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadic-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadic-tutorial/tutorial_general_04.png

[100]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadic-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadic-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadic-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadic-tutorial/tutorial_general_202.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadic-tutorial/tutorial_general_203.png























